# Tutorial: Streaming von PC-Spielen auf Raspberry Pi 4

## Vorraussetzungen

* Raspberry Pi 4B (4 GB)
* microSD-Karte
* XboX One Controller
* TV 
* Windows 10 PC
* NVIDIA GeForce Experience

## Raspberry PI Setup 

1. Raspberry Pi Imager herunterladen: https://www.raspberrypi.org/software/
2. Bootbare microSD-Karte mit `Raspberry Pi OS with desktop 5.1` erstellen
3. Raspberry Pi per HDMI an den TV anschließen (HDMI-Port am nächsten zum USB-C-Port verwenden)

## Software-Setup

1. Aktualisierung
```
sudo apt-get update
sudo apt-get upgrade
```
    
2. Konfiguration öffnen
```
sudo nano /boot/config.txt
```
3. Konfigurationswerte anpassen (Referenz: https://www.raspberrypi.org/documentation/computers/config_txt.html)
```
# Overscan (Schwarzen Rand um Bildschrim verhindern)
disable_overscan=1

# HDMI-Modus setzen (CEA (1) für Fernseher, DMT (2) für Displays)
hdmi_group=1

#Modus CEA-16 entspricht 1080p, 60 Hz, 16:9
hdmi_mode=16

# HDMI-Einstellungen forcieren (andernfalls werden manche Einstellungen ignoriert)
hdmi_force_mode=1

# Modus wählen (DVI ohne Sound = 1, HDMI mit Sound = 2)
hdmi_drive=2

# Maximale Taktfrequenz erhöhen (max. ist 2170 Mhz CPU, 750 Mhz GPU)
arm_freq=2000
over_voltage=6
gpu_freq=650

# Grafikspeicher festlegen (max. ist 512 MB)
gpu_mem=512

# Audio aktivieren
dtparam=audio=on
```

3. Neustarten um Einstellungen anzuwenden

## Moonlight Setup

1. Installieren der Software (Referenz: https://github.com/moonlight-stream/moonlight-qt)
```
curl -1sLf 'https://dl.cloudsmith.io/public/moonlight-game-streaming/moonlight-qt/setup.deb.sh' | sudo -E bash
sudo apt install moonlight-qt
```
2. Aktualisieren
```
sudo apt-get update
sudo apt-get upgrade
```
3. Software starten (optional)
```
moonlight-qt
```
5. Konfiguration automatischen Start von Moonlight nach Boot öffnen
```
sudo nano /etc/xdg/xsession/LXDE-pi/autostart
```
5. Konfiguration anpassen
```
@lxterminal --command="moonlight-qt"
```

## Software-Einstellungen

* Auflösung und FPS auf 1080p@60FPS ändern
* Video Bitrate auf 50 Mbps (zu hohe oder niedrige Werte sorgen für Probleme)

## Tipps

* `L1 + Start + Select + R1` beendet Moonlight
