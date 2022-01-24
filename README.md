# wsl2 mit GUI
getestet 11/2021 mit Windows 11 Home  
>Achtung: Nachdem WSL2 aktiviert wurde, funktionierten danach einige virtuelle Maschinen mit GUI in Oracle VirtualBox (mit den Versionen 6.1.26 bis 32 erlebt) nicht mehr.  
>In Windows mussten danach in der Systemsteuerung unter "Windows-Features aktivieren oder deaktivieren" die Häkchen bei "Windows-Hypervisor-Plattform" und "Windows-Subsystem für Linux" entfernt und der Rechner neu gestartet werden. Erst danach funktionierten die virtuellen Linux Maschinen mit GUI, z.B. Ubuntu 20.04 Gnome, wieder.  

> Infos zu WSL2 mit GUI gibt es hier: https://github.com/microsoft/wslg/  
* starte Windows PowerShell und aktualisiere WSL mit:   
`wsl --update`  
* lass dir die im Microsoft Store verfügbaren und einfach installierbaren Linux Distributionen anzeigen:  
`wsl --list --online`  
(Stand 17.11.2021)   
```
Die folgende Liste enthält die gültigen Distributionen, die installiert werden können.
Führen Sie die Installation mithilfe des Befehls „wsl --install -d <Distribution>“ aus.

NAME            FRIENDLY NAME
Ubuntu          Ubuntu
Debian          Debian GNU/Linux
kali-linux      Kali Linux Rolling
openSUSE-42     openSUSE Leap 42
SLES-12         SUSE Linux Enterprise Server v12
Ubuntu-16.04    Ubuntu 16.04 LTS
Ubuntu-18.04    Ubuntu 18.04 LTS
Ubuntu-20.04    Ubuntu 20.04 LTS
```

Beispiel:  
`wsl --install -d Debian`  
**Debian wird jetzt automatisch installiert und gestartet**  
`sudo apt update -y && sudo apt upgrade -y`  
`sudo apt install obs-studio`  
**OBS Studio starten:**  
`obs`  
>Aktuell (12/2021) wird aus den Debian Paketquellen eine mehrere Monate ältere Version von OBS-Studio installiert, die für mich nicht ausreichte und im Vergleich zur aktuellen Windows-Variante einige Nachteile hat. Interessant fand ich aber, das in Linux unter Windows auch anspruchsvolle Desktopanwendungen laufen.   

**Wie beende ich eine Linux Instanz?**
Öffne einfach ein PowerShell Fenster mit Adminrechten.  
`wsl --list --verbose`  
Du bekommst alle installierten Linux Instanzen angezeigt.  
`wsl --terminate Debian`  beendet die Debian Instanz.  

### wsl1 oder wsl2 nutzen?
WSL 1 und WSL 2 nutzen unterschiedliche Virtualisierungen und unterscheiden sich in der Architektur. Je nach Anwendungsfall macht die eine oder andere Version Sinn.  
`wsl --set-default-version 2`  
`wsl --set-default-version 1`  
`wsl --set-version <distro_name> 2`  
`wsl --list --verbose` 

### Zugriff von WSL 2 zu Windows (Stand 01/2022)
In Windows ist im Gegensatz zu Linux die Firewall standartgemäß aktiviert und verhindert z.B. einen Ping von WSL zum Windows Host. Eine Lösung ist:
**Powerschell als Admin öffnen und:**
`PS C:\WINDOWS\system32> New-NetFirewallRule -DisplayName "WSL" -Direction Inbound  -InterfaceAlias "vEthernet (WSL)"  -Action Allow`  

Im Folgenden will ich über ein eigenes VPN (WireGuard), SRT-Videostreams mit srt-live-transmit unter OS Ubuntu Core 20.04 empfangen, Statistikdaten in einer Datenbank erfassen und in einer Webanwendung darstellen und den Videostream, als UDP-Stream, dann an Windows 11 weitergeben, um ihn dann dort in OBS-Studio weiterzubearbeiten. Deshalb muss die Windows Firewall für WSL geöffnet werden.    

--- 
Das Folgende gehört eigentlich in ein anderes Repositorie:  
### SRT-Tools installieren
Für eine spezielle Anwendung:
```
C:\WINDOWS\system32>wsl --list --verbose
  NAME            STATE           VERSION
* Ubuntu-20.04    Running         2
```
```
torichter@DESKTOP-107L9GO:~$ uname -a
Linux DESKTOP-107L9GO 5.10.16.3-microsoft-standard-WSL2 #1 SMP Fri Apr 2 22:23:49 UTC 2021 x86_64 x86_64 x86_64 GNU/Linux
sudo apt update
sudo apt install srt-tools
```
danach müsste Folgendes vorhanden sein:
```
/usr/bin/srt-ffplay
/usr/bin/srt-file-transmit
/usr/bin/srt-live-transmit
/usr/bin/srt-tunnel
/usr/bin/stransmit
```
