# wsl2 mit GUI
getestet 11/2021 mit Windows 11  
> Infos gibt es hier: https://github.com/microsoft/wslg/  
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

**Wie beende ich eine Linux Instanz?**
Öffne einfach ein PowerShell Fenster mit Adminrechten.  
`wsl --list --verbose`  
Du bekommst alle installierten Linux Instanzen angezeigt.  
`wsl -t Debian`  beendet die Debian Instanz.  
