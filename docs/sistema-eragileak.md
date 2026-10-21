# Sistema Eragileak eta Zerbitzaria - Memoria Teknikoa

> **Modulua:** Sistema Eragileak Ezartzea (SISA 1)  
> **Taldea:** 6. Taldea  
> **Zerbitzaria:** `WindowsServer6Taldea` (192.168.70.2)  

---

## 1. IsardVDI Birtualizazioa eta Windows Server

* **Plataforma:** IsardVDI (KVM/QEMU hiperbisorea).
* **Makina Birtualaren Izena:** `Windows Server Erronka`
* **Deskribapena:** `1.Erronka 6 Taldea`
* **Baliabideak:** 6 vCPU, 16 GB RAM, Virtio disko-busa, Hard Disk boot.
* **Sare-interfazea:** Vlan 70 (MAC helbidea: `52:54:00:1e:ab:f1`).
* **Sare Parametroak:**
  - Ekipoaren Izena: `WindowsServer6Taldea` (WORKGROUP)
  - IP Estatikoa: `192.168.70.2`
  - Sare-Maskara: `255.255.255.0` (/24)
  - Atebidea: `192.168.70.254`
  - DNS Nagusia: `8.8.8.8` • DNS Alternatiboa: `6.6.6.6`
* **Eguneraketak:** Windows Server 2019 eguneratze metatuak, .NET 3.5/4.7.2/4.8 eta Defender Antivirus instalatuta.

---

## 2. Segurtasun Zuzentarauak eta NTFS Baimenak

* **Pasahitz Gidalerroak (`secpol.msc`):**
  - Gutxieneko luzera: 8 karaktere.
  - Konplexutasuna: Gaituta.
  - Gehieneko indarraldia: 90 egun.
  - Gutxieneko indarraldia: 1 egun.
  - Historiala: 24 pasahitz.
  - Zifraketa itzulgarria: Desgaituta.
* **Kontuak Blokeatzeko Gidalerroak:**
  - Blokeo-muga: 10 saiakera oker.
  - Blokeoaren iraupena: 15 minutu.
  - Berrezartzeko epea: 10 minutu.
* **Tokiko Erabiltzaileak eta Taldeak:**
  - `Editorea` (`Erronka Editorea`): `Erronka Editoreak` taldean.
  - `Irakurlea` (`Erronka Irakurlea`): `Erronka Irakurleak` taldean.
  - Pasahitza: `Admin_123`
* **Proba Karpeta (`C:\Erronka Proba`):**
  - `Erronka Editoreak`: Modificar.
  - `Erronka Irakurleak`: Lectura y ejecución.
  - `Administradores` eta `CREATOR OWNER`: Control total.

---

## 3. Disko-Kudeaketa eta RAID Sistemak

* **Disko Gehigarriak:** 3 disko dinamiko (20 GB bakoitza).
* **RAID 1 (Ispilua):** 2 disko erabilita, edukiera erabilgarria % 50. Webgunea eta fitxategi kritikoak hemen ostatatuko dira.
* **RAID 5 (Paritatea):** 3 disko erabilita, edukiera erabilgarria % 66. Irakurketa azkarra eta paritate bidezko segurtasuna.

---

## 4. IIS Web Zerbitzaria eta Windows Defender Firewall

* **Zerbitzaria:** Internet Information Services (IIS).
* **Lotura:** HTTP, 80 ataka, `192.168.70.2` helbidean.
* **Firewall Araua:** `IIS-HTTP-Inbound` araua gaitu da PowerShell bidez.

---

## 5. Babeskopiak eta Berreskuratze Prozedura

* **Windows Server Backup:** *Copias de seguridad de Windows Server* ezaugarria instalatuta `WindowsServer6Taldea` zerbitzarian.
* **Estrategia:** Eguneroko babeskopia osoak eta sistemaren egoera programatuta.
* **Berreskuratze Proba:** `index.html` ezabatu ostean jatorrizko egoerara leheneratu da inolako datu-galerarik gabe.
