# Installation Wireguard Linux Client


## Linux Mint

    snap install wireguard-ammp

## Allgemeines

Die jeweilige client.conf Datei muss nach /etc/wireguard/wg0.conf kopiert werden

Danach kann mit den beiden Scripten wireguard_connect.sh und wireguard_disconnect.sh der Tunnel auf- und abgebaut werden

# Installation Wireguard Raspi Server

**Achtung:** Mit Kernel 5.4.x funktioniert das Bauen von Wireguard aus den Quellen nicht mehr!

Es muss wie folgt vorgangen werden:

- Sicherstellen, dass wireguard nicht via apt installiert ist

    apt-cache policy wireguard*

- Kernelquellen installieren
    
    apt install raspberrypi-kernel-headers
   
- Prüfen, dass Kernel und Quellen in gleicher Version vorliegen (Versionen in Ausgabe vergleichen

    apt-cache policy raspberrypi-kernel*

- jetzt testing repo hinzufügen

    echo "deb http://archive.raspbian.org/raspbian testing main" | sudo tee --append /etc/apt/sources.list.d/testing.list
    apt update

- jetzt erscheint mögliches Update von sehr vielen Paketen    
- Paket Prio für testing runtersetzen

        printf 'Package: *\nPin: release a=testing\nPin-Priority: 50\n' | sudo tee --append /etc/apt/preferences.d/limit-testing
        apt update

- jetzt sollten alle Pakete wieder auf dem aktuellen Stand sein        
- wireguard aus testing installieren

    apt install wireguard

- das dauert sehr lange, da die dkms Module gebaut werden
- nach Installation prüfen ob die binaries vorliegen

    which wg wg-quick    
    /usr/bin/wg
    /usr/bin/wg-quick

- jetzt weitermachen mit normaler Konfiguration von wireguard


# Quellen

https://emanuelduss.ch/2018/09/wireguard-vpn-road-warrior-setup/
https://www.sigmdel.ca/michel/ha/wireguard/wireguard_02_en.html
