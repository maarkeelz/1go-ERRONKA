# Windows Server 2019 - Administrari Gida

> **Zikloa:** Sareko Informatika Sistemen Administrazioa (SISA 1)  
> **Erronka:** 1. Erronka Integratua  
> **Taldea:** 6. Taldea  
> **Zerbitzaria:** `WindowsServer6Taldea`  
> **Data:** 2026ko Urria  

---

## Aurkibidea

1. [Windows Zerbitzariaren Oinarrizko Datuak](#1-windows-zerbitzariaren-oinarrizko-datuak)
2. [Sare-Parametroak eta IsardVDI Hardwarea](#2-sare-parametroak-eta-isardvdi-hardwarea)
3. [Tokiko Erabiltzaileak eta Taldeak](#3-tokiko-erabiltzaileak-eta-taldeak)
4. [Segurtasun Zuzentarau Lokalak (secpol.msc)](#4-segurtasun-zuzentarau-lokalak-secpolmsc)
5. [Karpeten Egitura eta NTFS Baimenak](#5-karpeten-egitura-eta-ntfs-baimenak)
6. [Windows Server Backup eta Berreskuratzea](#6-windows-server-backup-eta-berreskuratzea)
7. [IIS Web Zerbitzaria eta Windows Defender Firewall](#7-iis-web-zerbitzaria-eta-windows-defender-firewall)

---

## 1. Windows Zerbitzariaren Oinarrizko Datuak

* **Makina Birtualaren Izena (IsardVDI):** `Windows Server Erronka`
* **Deskribapena:** `1.Erronka 6 Taldea`
* **Ekipoaren Izena (Hostname):** `WindowsServer6Taldea`
* **Lan-taldea (Workgroup):** `WORKGROUP`
* **Sistema Eragilea:** Windows Server 2019 Standard (1809) interfaze grafikoarekin (GUI).
* **Eguneraketak:** Windows Update bidez azken eguneratze metatuak (.NET 3.5/4.7.2/4.8, Defender Antivirus) instalatuta.

---

## 2. Sare-Parametroak eta IsardVDI Hardwarea

### 2.1. IsardVDI Baliabideak
* **vCPU kopurua:** 6 vCPU
* **RAM Memoria:** 16 GB
* **Disko Busa:** Virtio
* **Abioa (Boot):** Hard Disk
* **Bideoa:** Default
* **Sare-interfazea:** Vlan 70 (MAC helbidea: `52:54:00:1e:ab:f1`)

### 2.2. IPv4 Helbideratze Estatikoa
* **IP Helbidea:** `192.168.70.2`
* **Sare-Maskara:** `255.255.255.0` (/24)
* **Atebide Lehenetsia (Gateway):** `192.168.70.254`
* **DNS Zerbitzari Nagusia:** `8.8.8.8` (Google DNS)
* **DNS Zerbitzari Alternatiboa:** `6.6.6.6`

---

## 3. Tokiko Erabiltzaileak eta Taldeak

Segurtasun-irizpideak jarraituz, bi erabiltzaile eta bi talde sortu dira zerbitzarian funtzioak argi banatzeko:

### 3.1. Erabiltzaileen Kredentzialak eta Datuak

| Erabiltzaile Izena | Pasahitza | Talde Nagusia | Izen Osoa | Deskribapena / Funtzioa |
|---|---|---|---|---|
| `Editorea` | `Admin_123` | `Erronka Editoreak` | Erronka Editorea | Erronkako fitxategiak kudeatzeko eta editatzeko erabiltzailea. |
| `Irakurlea` | `Admin_123` | `Erronka Irakurleak` | Erronka Irakurlea | Erronkako fitxategiak soilik irakurtzeko baimena duen erabiltzailea. |
| `Administrador` | *(Sistemakoa)* | `Administradores` | Zerbitzariaren Administratzailea | Kontrol osoa zerbitzari osoan. |

### 3.2. Tokiko Taldeen Egitura

* **`Erronka Editoreak`:** Kide bakarra: `Editorea`. Fitxategiak sortu, aldatu eta ezabatzeko baimena.
* **`Erronka Irakurleak`:** Kide bakarra: `Irakurlea`. Fitxategiak irakurri eta exekutatzeko soilik baimena.

---

## 4. Segurtasun Zuzentarau Lokalak (`secpol.msc`)

Sistemaren segurtasuna indartzeko, Segurtasun Zuzentarau Lokalak konfiguratu dira:

### 4.1. Pasahitz Gidalerroak (Directiva de contraseñas)
* **Pasahitzen historia (Historial):** 24 pasahitz gogoratu (ezin da azken 24 pasahitzetako bat berrerabili).
* **Konplexutasun-baldintzak:** Gaituta (maiuskulak, minuskulak, zenbakiak eta karaktere bereziak beharrezkoak).
* **Gutxieneko luzera:** 8 karaktere.
* **Gehieneko indarraldia:** 90 egun.
* **Gutxieneko indarraldia:** 1 egun (egun berean ezin da behin baino gehiagotan aldatu historia saihesteko).
* **Zifraketa itzulgarria:** Desgaituta.

### 4.2. Kontua Blokeatzeko Gidalerroak (Directiva de bloqueo de cuenta)
* **Blokeo-muga (Umbral de bloqueo):** 10 saio-hasiera saiakera oker.
* **Blokeoaren iraupena (Duración del bloqueo):** 15 minutu.
* **Kontagailua berrezartzeko epea:** 10 minutu igaro ondoren.

---

## 5. Karpeten Egitura eta NTFS Baimenak

### 5.1. Hasierako Proba-Karpeta (`C:\Erronka Proba`)
Baimenen portaera egiaztatzeko sortutako behin-behineko karpeta:

* **`Erronka Editoreak`:** Modificar (Aldatu, idatzi, ezabatu).
* **`Erronka Irakurleak`:** Lectura y ejecución (Irakurri eta exekutatu soilik).
* **`Administradores`:** Control total (Kontrol osoa).
* **`CREATOR OWNER`:** Control total (Sortzaileak bere fitxategietan kontrol osoa).
* **`Usuarios`:** Lectura y ejecución / Especial.

### 5.2. Ekoizpeneko Web Karpeta (Etorkizuneko RAID Bolumenean)
Behin RAID bolumena konfiguratuta, webguneko fitxategiak bertara mugituko dira baimen hierarkiko berdinekin:
* Bide-izena: `E:\web-erronka\`
* IIS zerbitzariak fitxategiak irakurtzeko baimena izango du eta `Erronka Editoreak` taldeak edukia eguneratzeko baimena.

---

## 6. Windows Server Backup eta Berreskuratzea

### 6.1. Funtzionalitatearen Instalazioa
* **Ezaugarria:** *Copias de seguridad de Windows Server* instalatuta `WindowsServer6Taldea` zerbitzarian Zerbitzari Kudeatzailearen bidez.

### 6.2. Babeskopia Estrategia
* **Maiztasuna:** Eguneroko babeskopia automatikoak programatuta kanpoko disko batera.
* **Edukia:** Sistemaren egoera (System State) eta web-karpetak.
* **Berreskuratze simulazioa:** Fitxategi bat ezabatzean jatorrizko egoerara leheneratzeko proba arrakastaz burutu da.

---

## 7. IIS Web Zerbitzaria eta Windows Defender Firewall

### 7.1. IIS Konfigurazioa
* **Zerbitzua:** Internet Information Services (IIS).
* **Lotura:** HTTP, 80 ataka, `192.168.70.2` helbidean.
* **Lehenetsitako dokumentua:** `index.html`.

### 7.2. Firewall Sarrerako Araua
Sareko beste ordenagailu eta mugikorretatik webgunera sartu ahal izateko araua:

```powershell
New-NetFirewallRule -Name "IIS-HTTP-Inbound" `
  -DisplayName "IIS Web Zerbitzaria (Port 80 HTTP)" `
  -Enabled True `
  -Direction Inbound `
  -Protocol TCP `
  -LocalPort 80 `
  -Action Allow
```
