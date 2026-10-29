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

### 4.2. Inaktibitateagatiko saio-blokeoa

Windows Server-en saioa automatikoki blokeatzeko direktiba konfiguratu dugu.

| Parametroa | Balioa |
|---|---|
| Inaktibitate-muga | 300 segundo |
| Minututan | 5 minutu |

Neurri honen helburua da erabiltzaileak saioa irekita utzi eta ordenagailutik urruntzen denean baimenik gabeko erabilera zailtzea.

Ezarritako denboran ordenagailua erabili gabe utzi dugu, eta saioa automatikoki blokeatzen dela egiaztatu dugu. Saioa berriro erabiltzeko, desblokeatu egin behar da.

![Inaktibitateagatiko Saio Blokeoa](../img/sistema-eragileak/doc%20img/image36.png)

## 5. Erabiltzaileak, Taldeak eta Baimenak

### 5.1. Erabiltzaileak eta taldeak sortzea

Lau erabiltzaile sortu ditugu, eta bakoitza bere eginkizunari dagokion taldean sartu dugu.

| Erabiltzailea | Eginkizuna |
|---|---|
| Ane Garcia | Datu-baseen kudeaketa. |
| Ibai Asensio | Webgunearen edizioa. |
| Unai Lopez | Dokumentazioaren edizioa. |
| Leire Martin | Proiektuaren irakurketa. |

Eginkizun horiek antolatzeko, datu-baseen kudeatzaileen, dokumentazio-editoreen, proiektu-irakurleen eta web-editoreen taldeak sortu ditugu.

Taldeen izen zehatzak eta kideak pantaila-argazkietan ikus daitezke. Konfigurazioaren xehetasun gehiago Administrari Gidan jasota daude.

![Erabiltzaileak](../img/sistema-eragileak/doc%20img/image35.png)
![Taldeak](../img/sistema-eragileak/doc%20img/image15.png)

### 5.2. Karpetetako NTFS baimenak

Proiektuko fitxategietarako sarbidea taldeen bidez antolatu dugu. Talde bakoitzari bere lanerako behar dituen baimenak esleitu dizkiogu.

#### Lan-karpetetako edizio-baimenak

Talde arduradun bakoitzak bere lan-karpetan aldatzeko baimena du.

| Karpeta | Taldea | Baimena |
|---|---|---|
| `R:\Webgunea` | Web Editoreak | Aldatzea (`Modificar`). |
| `M:\Erronka\Datu Baseak` | DatuBaseak Kudeatzaileak | Aldatzea (`Modificar`). |
| `M:\Erronka\Dokumentazioa` | Dokumentazio Editoreak | Aldatzea (`Modificar`). |

Sarrera horietan honako baimen hauek markatuta daude:

- Aldatzea.
- Irakurtzea eta exekutatzea.
- Karpetaren edukia zerrendatzea.
- Irakurtzea.
- Idaztea.

`Control total` aukera ez dago markatuta.

#### Erronka karpetako irakurketa-baimenak

`M:\Erronka` karpetan, ondorengo taldeei irakurtzeko sarbidea eman diegu:

| Taldea | Konfiguratutako baimenak |
|---|---|
| Web Editoreak | Irakurtzea eta exekutatzea, karpetaren edukia zerrendatzea eta irakurtzea. |
| Dokumentazio Editoreak | Irakurtzea eta exekutatzea, karpetaren edukia zerrendatzea eta irakurtzea. |
| DatuBaseak Kudeatzaileak | Irakurtzea eta exekutatzea, karpetaren edukia zerrendatzea eta irakurtzea. |
| Proiektu Irakurleak | Irakurtzea eta exekutatzea, karpetaren edukia zerrendatzea eta irakurtzea. |

Sarrera horietan ez ditugu idazteko, aldatzeko edo kontrol osoa izateko baimenak markatu.

Edizio-taldeek beren lan-azpikarpetetan dituzten aldatzeko baimenak aurreko taulan jasota daude.

#### Webguneko irakurketa-baimenak

`R:\Webgunea` karpetan, web-editoreez gain, beste talde batzuek ere irakurtzeko sarbidea dute:

| Taldea | Konfiguratutako baimenak |
|---|---|
| Proiektu Irakurleak | Irakurtzea eta exekutatzea, karpetaren edukia zerrendatzea eta irakurtzea. |
| DatuBaseak Kudeatzaileak | Irakurtzea eta exekutatzea, karpetaren edukia zerrendatzea eta irakurtzea. |
| Dokumentazio Editoreak | Irakurtzea eta exekutatzea, karpetaren edukia zerrendatzea eta irakurtzea. |

Talde horien sarreretan ez ditugu idazteko edo aldatzeko baimenak markatu. Web Editoreak taldeak, berriz, webgunearen karpetan aldatzeko baimena du.

#### Baimenen aplikazio-eremua

Erakutsitako baimen-sarrera guztiak `Permitir` motakoak dira, eta honako eremu honetan aplikatzeko konfiguratu ditugu:

```text
Esta carpeta, subcarpetas y archivos
```

Hau da, karpetari, azpikar petei eta fitxategiei aplikatzen zaizkie.

#### Konfigurazioaren ebidentzia

![Baimenak](../img/sistema-eragileak/doc%20img/image3.png)
![Baimenak](../img/sistema-eragileak/doc%20img/image6.png)
![Baimenak](../img/sistema-eragileak/doc%20img/image8.png)
![Baimenak](../img/sistema-eragileak/doc%20img/image11.png)
![Baimenak](../img/sistema-eragileak/doc%20img/image13.png)
![Baimenak](../img/sistema-eragileak/doc%20img/image25.png)
![Baimenak](../img/sistema-eragileak/doc%20img/image29.png)
![Baimenak](../img/sistema-eragileak/doc%20img/image32.png)
![Baimenak](../img/sistema-eragileak/doc%20img/image38.png)
![Baimenak](../img/sistema-eragileak/doc%20img/image43.png)

## 6. Diskoak eta RAID Bolumenak

### 6.1. Disko gehigarriak

VirtualBox-en hiru disko berri gehitu ditugu, bakoitza 20 GB-koa. Windows Server-en GPT partizio-estiloarekin hasieratu ditugu

![Diskoak Gehitu](../img/sistema-eragileak/doc%20img/image20.png)

### 6.2. RAID 1 eta RAID 5

Bi RAID bolumen sortu ditugu:

| RAID mota | Erabilitako diskoak | Disko bakoitzean erabilitako espazioa |
|---|---|---|
| RAID 1 — Ispilua | 2 disko | 5 GB |
| RAID 5 — Paritatea | 3 disko | 10 GB |

Diskoetan esleitu gabeko espazioa utzi dugu, etorkizunean behar izanez gero erabiltzeko.

![Diskoak Gehitu](../img/sistema-eragileak/doc%20img/image10.png)

### 6.3. Proiektuko fitxategien antolaketa

Erronkaren fitxategiak bi RAID bolumenetan antolatu ditugu:

| Bolumena | Karpeta | Edukia |
|---|---|---|
| RAID 1 | `M:\Erronka` | Datu-basea, dokumentazioa, planifikazioa eta aurkezpena. |
| RAID 5 | `R:\Webgunea` | Webgunearen HTML fitxategiak, estilo-orriak eta irudiak. |

IIS webgunearen bide fisikoa `R:\Webgunea` karpetara lotu dugu.

### 6.4. Egiaztapena

Fitxategi errealak ireki eta gorde ditugu, eta webgunea IIS bidez atzitu dugu. Egiaztapen horiek bolumenen erabilera eta webgunearen argitalpena erakusten dituzte.

## 7. Windows Server Backup

### 7.1. Instalazioa

Windows Server Backup instalatu dugu zerbitzarian.

![Windows Server Backup Instalatu](../img/sistema-eragileak/doc%20img/image33.png)

### 7.2. Babeskopiaren konfigurazioa

Windows Server Backup erabiliz, ondorengo karpeten babeskopia konfiguratu dugu:

- `M:\Erronka`: datu-basea, dokumentazioa, planifikazioa eta aurkezpena.
- `R:\Webgunea`: IISen argitaratutako webgunearen fitxategiak.

Kopiak RAID bolumenetatik bereizitako helmuga batean gordetzen dira.

Eguneroko exekuzioa programatu dugu, makina piztuta eta laneko fitxategiak gordeta egongo diren ordutegi batean.

Access datu-basearen fitxategia babeskopia egin aurretik itxiko da.

![Windows Server Backup Konfiguratu](../img/sistema-eragileak/doc%20img/image30.png)
![Windows Server Backup Konfiguratu](../img/sistema-eragileak/doc%20img/image39.png)

### 7.3. Egiaztapena

Programatutako exekuzioaren emaitza eta erregistroa berrikusi ditugu.

![Windows Server Backup Egiaztatu](../img/sistema-eragileak/doc%20img/image4.png)

## 8. Cobian Reflector Bidezko Babeskopiak

### 8.1. Instalazioa

Cobian Reflector hirugarrenen babeskopia-tresna gisa instalatu dugu.

Zerbitzu modua hautatu dugu, kopien exekuzioa erabiltzailearen interfazea irekita edukitzearen mende ez egoteko.

Konfigurazio honetan, jatorria eta helmuga makina bereko unitate lokaletan daude.

![Windows Server Backup Egiaztatu](../img/sistema-eragileak/doc%20img/image12.png)



