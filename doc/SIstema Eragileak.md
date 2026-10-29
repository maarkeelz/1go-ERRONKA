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

![Cobian Reflector Instalatzen](../img/sistema-eragileak/doc%20img/image5.png)

### 8.2. Babeskopia-zeregina

`Erronkaren Babeskopia` izeneko zeregina sortu dugu.

Kopia osoa hautatu dugu, jatorrizko karpetetako fitxategi guztiak eta azpikarpetak gordetzeko.

Kopia bereiziak sortzeko aukera aktibatu dugu. Horrela, exekuzio bakoitzak data eta ordua dituen bertsio bat sortzen du.

![Cobian Reflector Zeregina  ](../img/sistema-eragileak/doc%20img/image12.png)

### 8.3. Jatorriak eta helmuga

| Mota | Karpeta |
|---|---|
| Lehen jatorria | `M:\Erronka` |
| Bigarren jatorria | `R:\Webgunea` |
| Helmuga | `C:\Cobian Reflector KOPIAK` |

Bi jatorriak zeregin berean konfiguratu ditugu.

![Cobian Reflector Jatorriak eta Helmuga  ](../img/sistema-eragileak/doc%20img/image14.png)

### 8.4. Exekuzio automatikoa

Zeregina egunero 08:15ean automatikoki exekutatzeko programatu dugu.

Ordu horretan:

- Zerbitzaria piztuta egon behar da.
- Taldeak laneko fitxategiak aurrez gordeta utziko ditu.
- Exekuzioa Windows Server Backup tresnaren ordutegiarekin ez gainjartzeko antolatu dugu.

![Cobian Reflector Automatikoki](../img/sistema-eragileak/doc%20img/image16.png)

### 8.5. Bertsioen kontserbazioa

Azken hiru kopia osoak mantentzea konfiguratu dugu, helmugako espazio erabilgarria kontuan hartuta.

Kopiak konpresiorik gabe gordetzen dira, fitxategiak errazago berrikusi eta berreskuratzeko.

Ispilu modua desgaituta mantendu dugu, jatorrian egindako ezabatzeak helmugara automatikoki ez zabaltzeko.

![Cobian Reflector Dinamiko](../img/sistema-eragileak/doc%20img/image7.png)
![Cobian Reflector Dinamiko](../img/sistema-eragileak/doc%20img/image31.png)

### 8.6. Lehenengo exekuzioaren egiaztapena

Zeregina eskuz exekutatu dugu hasierako konfigurazioa egiaztatzeko.

Amaitzean:

1. Exekuzioaren erregistroa berrikusi dugu.
2. Helmugan kopiatutako karpetak egiaztatu ditugu.
3. Kopiatutako fitxategiak egiaztatu ditugu.
4. Emaitza pantaila-argazkian jaso dugu.

![Lehenengo exekuzioaren Egiaztapena](../img/sistema-eragileak/doc%20img/image23.png)
![Lehenengo exekuzioaren Egiaztapena 2](../img/sistema-eragileak/doc%20img/image17.png)

## 9. Fitxategi Bat Berreskuratzea

### 9.1. Fitxategia hautatzea

Cobian Reflector-ek sortutako babeskopia ireki dugu eta webguneko index fitxategia hautatu dugu.

Fitxategia babeskopiaren karpetan dagoela egiaztatu dugu, eta ez jatorrizko lan-karpetan.

![Aukeratutako Fitxategia](../img/sistema-eragileak/doc%20img/image48.png)

### 9.2. Beste kokapen batean berreskuratzea

Hautatutako fitxategia babeskopiatik kopiatu eta ondorengo karpetan gorde dugu:

```text
M:\Berreskuratzea
```

Jatorrizko fitxategia eta babeskopian gordetako bertsioa aldatu gabe mantendu ditugu.

Berreskuratzea beste kokapen batean egin dugu, laneko fitxategia ustekabean gainidaztea saihesteko.

![Aukeratutako Fitxategia Berreskuratzen](../img/sistema-eragileak/doc%20img/image1.png)

### 9.3. Berreskuratutako edukia egiaztatzea

Berreskuratutako index fitxategia ireki eta haren edukia berrikusi dugu.

Fitxategia irekitzen dela eta hautatutako babeskopiari dagokion informazioa eskuragarri dagoela egiaztatu dugu.

Proba honetan CSS fitxategiak ez ditugu berreskuratu; horregatik, orria jatorrizko diseinurik gabe ikusten da.

Egiaztapen honek fitxategi horren berreskuratzea frogatzen du. Ez du babeskopiako fitxategi guztien edo sistema osoaren berreskuratzea frogatzen.

![Berreskuratutako Fitxategia Egiaztatzen](../img/sistema-eragileak/doc%20img/image2.png)

## 10. IIS Web-zerbitzaria

### 10.1. Webgunearen fitxategiak kokatzea

Webgunearen HTML fitxategiak, estilo-orriak eta irudiak ondorengo karpetan kokatu ditugu:

```text
R:\Webgunea
```

Karpeta RAID bolumenean dago, eta IIS webgunearen erro-direktorio gisa erabiltzen dugu.

![IIS Web Zerbitzaria Fitxategiak Kokatzen](../img/sistema-eragileak/doc%20img/image42.png)

### 10.2. IIS prestatzea

Windows Server-en IIS rola eta administrazio-kontsola prestatu ditugu.

Eduki estatikoa eta dokumentu lehenetsia erabiltzeko konfigurazioa egiaztatu dugu.

![IIS Web Zerbitzaria Prestatzen](../img/sistema-eragileak/doc%20img/image28.png)

### 10.3. Webgunea sortzea

IISen `Erronka` izeneko webgunea sortu dugu.

| Parametroa | Konfigurazioa |
|---|---|
| Webgunearen izena | Erronka |
| Bide fisikoa | `R:\Webgunea` |
| Protokoloa | HTTP |
| Ataka | 80 |
| Ostalari-izena | Hutsik |

Hasierako egiaztapenetarako ostalari-izena hutsik utzi dugu, zerbitzariaren IP helbidearen bidez sartzeko.

![IIS Web Zerbitzaria Sortzen](../img/sistema-eragileak/doc%20img/image45.png)

### 10.4. Hasierako dokumentua

`index.html` dokumentu lehenetsi gisa konfiguratu dugu.

Horrela, webgunearen helbidera sartzean hasierako orria zuzenean erakusten da.

![IIS Web Zerbitzaria Hasierako Dokumentua](../img/sistema-eragileak/doc%20img/image24.png)

### 10.5. Autentifikazioa eta NTFS baimenak

Autentifikazio anonimoa gaituta utzi dugu, webgunea erabiltzaile-izena eta pasahitza eskatu gabe kontsultatzeko.

Sarbide anonimoak aplikazio-taldearen identitatea erabiltzen du.

Ondorengo identitateari irakurtzeko eta exekutatzeko baimenak eman dizkiogu webgunearen karpetan:

```text
IIS AppPool\Erronka
```

Ez diogu webguneko fitxategiak aldatzeko baimenik eman.

![IIS Web Zerbitzaria Baimenak](../img/sistema-eragileak/doc%20img/image26.png)
![IIS Web Zerbitzaria Baimenak](../img/sistema-eragileak/doc%20img/image22.png)

### 10.6. Tokiko egiaztapena

Zerbitzariko arakatzailean ondorengo helbidea ireki dugu:

```text
http://localhost
```

Webgunea IIS bidez kargatzen dela egiaztatu dugu. Halaber, estiloak, irudiak eta nabigazio-estekak berrikusi ditugu.

![Tokiko Egiaztapenak](../img/sistema-eragileak/doc%20img/image47.png)

## 11. Suebakiaren Konfigurazioa

Windows Defender suebakian HTTP trafikorako sarrera-araua egiaztatu dugu.

| Parametroa | Konfigurazioa |
|---|---|
| Noranzkoa | Sarrerako trafikoa |
| Protokoloa | TCP |
| Tokiko ataka | 80 |
| Ekintza | Konexioa baimentzea |

Araua erabilitako sare-profilean aplikatzen dela egiaztatu dugu.

Suebakia gaituta mantendu dugu; ez dugu babes osoa desgaitu webgunera sartzeko

![World Wide Web](../img/sistema-eragileak/doc%20img/image41.png)


## 12. Sareko Sarbidearen Egiaztapena

Beste gailu batetik zerbitzariaren IP helbidera sartu gara, HTTP erabiliz:

```text
http://192.168.70.2
```

Ondoren, haririk gabeko konexioa duen gailu batetik ere sarbidea egiaztatu dugu.

Bi probetan ondorengo elementuak berrikusi ditugu:

- Hasierako orria.
- Nabigazio-menua.
- Irudiak.
- Estiloak.

Probaren helbidea eta emaitza pantaila-argazkietan jaso ditugu.

![Sare Bidezko Sarbidea Egiaztatzen](../img/sistema-eragileak/doc%20img/image9.png)

## 13. Haririk Gabeko Konexiorako Routerraren Konfigurazioa

Routerra sarbide-puntu gisa konfiguratu dugu eta ikasgelako sarera konektatu dugu.

Ondoren:

1. Haririk gabeko sareari izena jarri diogu.
2. Sarbide-pasahitza ezarri dugu.
3. Mugikorra Wi-Fi sarera konektatu dugu.
4. Mugikorreko arakatzailean zerbitzariaren IP helbidea sartu dugu.
5. Webgunerako sarbidea egiaztatu dugu.

Erabilitako helbidea:

```text
http://192.168.70.2
```

![Router Konfigurazioa](../img/sistema-eragileak/doc%20img/image46.png)
![Hari Gabeko Froga](../img/sistema-eragileak/doc%20img/image44.jpg)


