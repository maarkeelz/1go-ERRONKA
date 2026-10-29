---
layout: default
title: "Sistema Eragileak"
---

# Sistema Eragileak: Windows Server Zerbitzariaren Dokumentazioa

Dokumentu honetan gure Windows Server zerbitzariaren instalazioa, konfigurazioa, segurtasuna, biltegiratzea, babeskopiak eta webgunearen argitalpena azaltzen ditugu.

## 1. Makina Birtuala

VirtualBox erabiliz, Windows Server instalatu dugu `Windows Server Erronka` izeneko makina birtualean.

Makina birtualaren ezaugarriak dagokion pantaila-argazkian jasota daude.

![VirtualBox Parametroak](../img/sistema-eragileak/doc%20img/image18.png)
![Windows Server Instalazioa](../img/sistema-eragileak/doc%20img/image27.png)

## 2. Ekipoaren Izena eta IP Helbidea

Windows Server instalatu ondoren, ekipoaren izena eta sare-konfigurazioa aldatu ditugu.

| Parametroa | Balioa |
|---|---|
| Ekipoaren izena | WindowsServer6Taldea |
| IP helbidea | 192.168.70.2 |

![Ekipoaren Izena](../img/sistema-eragileak/doc%20img/image19.png)
![IP-a Aldatu](../img/sistema-eragileak/doc%20img/image37.png)

## 3. Windows Update Eguneraketak

Hasierako konfigurazioa amaitzeko, Windows Server-en zain zeuden eguneraketak instalatu ditugu.

![Eguneraketak Instalatu](../img/sistema-eragileak/doc%20img/image21.png)

## 4. Tokiko Segurtasun-direktibak

Tokiko segurtasun-direktibak aldatu ditugu, pasahitzen erabilera kontrolatzeko.

Konfigurazioaren bidez:

- Pasahitz luzeagoak eta konplexuagoak erabiltzea ezarri dugu.
- Aurreko pasahitzen berrerabilpena mugatu dugu.
- Pasahitzen biltegiratzearekin lotutako beharrezkoak ez diren arriskuak saihestu ditugu.
- Pasahitzen gehieneko indarraldia 90 egunetan ezarri dugu, praktika honetarako hartutako erabaki gisa.

![Tokiko Segurtasun Direktibak](../img/sistema-eragileak/doc%20img/image34.png)

### 4.1. Kontuak blokeatzeko direktibak

Tokiko segurtasun-direktibetan (`secpol.msc`), kontuak blokeatzeko arauak konfiguratu ditugu, saioa hasteko huts egindako saiakerak mugatzeko.

| Direktiba | Ezarritako balioa |
|---|---|
| Kontua blokeatzeko atalasea | Saioa hasteko 10 saiakera oker. |
| Kontuaren blokeoaren iraupena | 15 minutu. |
| Saiakera okerren kontagailua berrezartzeko denbora | 10 minutu. |
| Administratzaile-kontua blokeatzea baimentzea | Gaituta. |

![Kontuak Blokeatzeko Direktibak](../img/sistema-eragileak/doc%20img/image34.png)


