---
# required metadata

title: Validar la creación de reflejo del puerto | Microsoft Advanced Threat Analytics
description: Se describe cómo validar que la creación de reflejo del puerto está bien configurada
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: ebd41719-c91a-4fdd-bcab-2affa2a2cace

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Validar la creación de reflejo del puerto
> [!NOTE] Este artículo solo es relevante si implementa puertas de enlace de ATA en lugar de puertas de enlace ligeras de ATA. Para determinar si tiene que usar puertas de enlace de ATA, consulte [Choosing the right gateways for your deployment (Elección de las puertas de enlace adecuadas para la implementación)](/advanced-threat-analytics/plan-design/ata-capacity-planning#Choosing-the-right-gateway-type-for-your-deployment)
 
Los siguientes pasos le guiarán a través del proceso para validar que la creación de reflejo del puerto está correctamente configurada. Para que ATA funcione correctamente, la puerta de enlace de ATA debe ser capaz de ver el tráfico hacia y desde el controlador de dominio. El origen de datos principal que usa ATA es la inspección profunda de paquetes del tráfico de red hacia y desde los controladores de dominio. Para que ATA vea el tráfico de red, hay que configurar la creación de reflejo del puerto. La creación de reflejo del puerto copia el tráfico de un puerto (puerto de origen) en otro puerto (puerto de destino).

## Validar la creación de reflejo del puerto mediante un script de Windows PowerShell

1. Guarde el texto de este script en un archivo denominado ATAdiag.ps1.
2. Ejecute este script desde la puerta de enlace de ATA.
El script genera tráfico ICMP desde la puerta de enlace de ATA al controlador de dominio y busca ese tráfico en la NIC de captura en el controlador de dominio.
Si la puerta de enlace de ATA ve tráfico ICMP con una dirección IP de destino idéntica a la dirección IP del controlador de dominio que ha especificado en la consola de ATA, considera configurada la creación de reflejo del puerto. 

Ejemplo de cómo ejecutar el script:

    # ATAdiag.ps1 -CaptureIP n.n.n.n -DCIP n.n.n.n -TestCount n
    
    param([parameter(Mandatory=$true)][string]$CaptureIP, [parameter(Mandatory=$true)][string]$DCIP, [int]$PingCount = 10)

    # Set variables
    
        $ErrorActionPreference = "stop"
    $starttime = get-date
    $byteIn = new-object byte[] 4
    $byteOut = new-object byte[] 4
    $byteData = new-object byte[] 4096  # size of data
    
    $byteIn[0] = 1  # for promiscuous mode
    $byteIn[1-3] = 0
    $byteOut[0-3] = 0



    # Convert network data to host format
        function NetworkToHostUInt16 ($value)
        {
        [Array]::Reverse($value)
        [BitConverter]::ToUInt16($value,0)
        }
    
    function NetworkToHostUInt32 ($value)
        {
        [Array]::Reverse($value)
        [BitConverter]::ToUInt32($value,0)
        }
    
    function ByteToString ($value)
        {
        $AsciiEncoding = new-object system.text.asciiencoding
        $AsciiEncoding.GetString($value)
            }
    
    Write-Host "Testing Port Mirroring..." -ForegroundColor Yellow
    Write-Host ""
    Write-Host "Here is a summary of the connection we will test." -ForegroundColor Yellow

    # Initialize a first ping connection
    Test-Connection -Count 1 -ComputerName $DCIP -ea SilentlyContinue
    Write-Host ""
    
    Write-Host "Press any key to continue..." -ForegroundColor Red
    [void][System.Console]::ReadKey($true)
    Write-Host ""
    Write-Host "Sending ICMP and Capturing data..." -ForegroundColor Yellow
    
    # Open a socket
    
    $socket = new-object system.net.sockets.socket([Net.Sockets.AddressFamily]::InterNetwork,[Net.Sockets.SocketType]::Raw,[Net.Sockets.ProtocolType]::IP)
    
    # Include the IP header
    $socket.setsocketoption("IP","HeaderIncluded",$true)
    
    $socket.ReceiveBufferSize = 10000
    
    $ipendpoint = new-object system.net.ipendpoint([net.ipaddress]"$CaptureIP",0)
    $socket.bind($ipendpoint)
    
    # Enable promiscuous mode
    [void]$socket.iocontrol([net.sockets.iocontrolcode]::ReceiveAll,$byteIn,$byteOut)
    
    # Initialize test variables
    $tests = 0
    $TestResult = "Noise"
    $OneSuccess = 0
    
    while ($tests -le $PingCount)
        {
        if (!$socket.Available)  # see if any packets are in the queue
            {
            start-sleep -milliseconds 500
            continue
            }
    
    # Capture traffic
        $rcv = $socket.receive($byteData,0,$byteData.length,[net.sockets.socketflags]::None)
    
    # Decode the header so we can read ICMP
    
        $MemoryStream = new-object System.IO.MemoryStream($byteData,0,$rcv)
        $BinaryReader = new-object System.IO.BinaryReader($MemoryStream)
    
    # Set IP version & header length
        $VersionAndHeaderLength = $BinaryReader.ReadByte()
    
        # TOS
        $TypeOfService= $BinaryReader.ReadByte()
    
        # More values, and the Protocol Number for ICMP traffic
        # Convert network format of big-endian to host format of little-endian 
        $TotalLength = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
    
        $Identification = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
        $FlagsAndOffset = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
        $TTL = $BinaryReader.ReadByte()
        $ProtocolNumber = $BinaryReader.ReadByte()
        $Checksum = [Net.IPAddress]::NetworkToHostOrder($BinaryReader.ReadInt16())
    
        # The source and destination IP addresses
        $SourceIPAddress = $BinaryReader.ReadUInt32()
        $DestinationIPAddress = $BinaryReader.ReadUInt32()
    
        # The source and destimation ports
        $sourcePort = [uint16]0
        $destPort = [uint16]0
            
        # Close the stream reader
        $BinaryReader.Close()
        $memorystream.Close()
    
        # Cast DCIP into an IPaddress type
        $DCIPP = [ipaddress] $DCIP
        $DestinationIPAddressP = [ipaddress] $DestinationIPAddress
    
        #Ping the DC at the end after starting the capture
        Test-Connection -Count 1 -ComputerName $DCIP -ea SilentlyContinue | Out-Null
            
        # This is the match logic - check to see if Destination IP from the Ping sent matches the DCIP entered by in the ATA Console  
        # The only way the ATA Gateway should see a destination of the DC is if Port Spanning is configured
        
            if ($DestinationIPAddressP -eq $DCIPP)  # is the destination IP eq to the DC IP? 
            {
            $TestResult = "Port Spanning success!"
            $OneSuccess = 1
            } else {
                $TestResult = "Noise"
            }
        
        # Put source, destination, test result in Powershell object
        
        new-object psobject | add-member -pass noteproperty CaptureSource $([system.net.ipaddress]$SourceIPAddress) | add-member -pass noteproperty CaptureDestination $([system.net.ipaddress]$DestinationIPAddress) | Add-Member -pass NoteProperty Result $TestResult | Format-List | Out-Host
        #Count tests
        $tests ++
        }
    
        If ($OneSuccess -eq 1){
            Write-Host "Port Spanning Success!" -ForegroundColor Green
            Write-Host ""
            Write-Host "At least one packet which was addressed to the DC, was picked up by the Gateway." -ForegroundColor Yellow
            Write-Host "A little noise is OK, but if you don't see a majority of successes, you might want to re-run." -ForegroundColor Yellow
        } Else {
            Write-Host "No joy, all noise.  You may want to re-run, increase the number of Ping Counts, or check your config." -ForegroundColor Red
        }
    
    Write-Host ""
    Write-Host "Press any key to continue..." -ForegroundColor Red
    [void][System.Console]::ReadKey($true)
    
    
## Validar la creación de reflejo del puerto con Net Mon
1.  Instalar [Monitor de red de Microsoft 3.4](http://www.microsoft.com/download/details.aspx?id=4865).

    > [!IMPORTANT]
    > No instale el Analizador de mensajes de Microsoft ni ningún otro software de captura de tráfico en la puerta de enlace de ATA.

2.  Abra el Monitor de red y cree una pestaña de captura nueva.

    1.  Seleccione únicamente el adaptador de red de **captura** o el adaptador de red que esté conectado al puerto del conmutador configurado como puerto de destino de creación de reflejo del puerto.

    2.  Asegúrese de que la opción Modo P está habilitada.

    3.  Haga clic en **Nueva captura**.

        ![Imagen de creación de pestaña de captura nueva](media/ATA-Port-Mirroring-Capture.jpg)

3.  En la ventana de filtro de visualización, escriba el siguiente filtro: **KerberosV5 OR LDAP** y, después, haga clic en **Aplicar**..

    ![Imagen de aplicación del filtro KerberosV5 or LDAP](media/ATA-Port-Mirroring-filter-settings.jpg)

4.  Haga clic en **Iniciar** para iniciar la sesión de captura. Si no ve el tráfico hacia y desde el controlador de dominio, repase la configuración de creación de reflejo del puerto.

    ![Imagen de inicio de la sesión de captura](media/ATA-Port-Mirroring-Capture-traffic.jpg)

    > [!NOTE]
    > Es importante asegurarse de que ve el tráfico tanto hacia como desde los controladores de dominio.
    

5.  Si solo ve el tráfico en una dirección, acuda a sus equipos de red o de virtualización para que le ayuden a solucionar el problema de configuración de creación de reflejo del puerto.

## Véase también

- [Configurar la creación de reflejo del puerto](configure-port-mirroring.md)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


