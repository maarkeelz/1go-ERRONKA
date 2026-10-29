---
layout: default
title: "Markatze Lengoaiak"
---

# Markatze Lengoaiak: Proiektuaren eta Karpetaren Dokumentazioa

Dokumentu honek SISA 1 zikloko 1. Erronkaren web proiektuaren egitura osoa, karpetako osagaiak, erabilitako teknologiak eta fitxategi bakoitzaren helburua zehazten ditu.

---

## 1. Proiektuaren Deskribapena eta Testuingurua

* **Zikloa:** Sareko Informatika Sistemen Administrazioa (SISA 1).
* **Erronka:** 1. Erronka Integratua — *«Informazioaren digitalizazio webgunea»*.
* **Taldea:** 6. Taldea.
* **Ikasturtea:** 2026/2027.
* **Helburua:** Enpresa simulatu baten azpiegitura informatiko osoa (Sareak, Datu-baseak, Sistema Eragileak eta Digitalizazioa) aurkezten duen webgune estatiko semantikoa eta moldagarria garatzea, eta haren dokumentazio teknikoa GitHub Pages bidez argitaratzea.

---

## 2. Karpetaren Egitura Orokorra

Proiektua biltegi bakar batean antolatuta dago, bide erlatiboak erabiliz eramangarritasuna (portabilitatea) bermatzeko. Karpeta nagusiak ondorengo zuhaitz-egitura dauka:

```text
1go-ERRONKA/
├── _config.yml              # GitHub Pages / Jekyll konfigurazioa
├── index.html               # Webgunearen hasierako orria (Ataria)
├── sareak.html              # Sareen azpiegitura eta seinaleak
├── datu-baseak.html         # Streaming datu-basearen diseinua eta 3NF
├── sistema-eragileak.html   # Windows Server, erabiltzaileak, RAID eta backup
├── digitalizazioa.html      # IT/OT, THD teknologiak eta GitHub Projects
├── markatze.html              # Markatze Lengoaiak moduluaren dokumentazio orokorra
│
├── css/
│   └── estiloak.css         # Webgune osoko estilo-orri orokorra (CSS3)
│
├── img/                     # Baliabide grafikoak eta ebidentziak
│   ├── orokorrak/           # Webguneko logo bektoriala (SVG)
│   ├── sareak/              # Seinaleak, CRC kalkuluak eta eskemen irudiak
│   ├── datu-baseak/         # E-R diagramak eta Access erlazioak
│   ├── sistema-eragileak/   # Zerbitzariaren konfigurazioaren kapturak
│   └── digitalizazioa/      # Kanban, Gantt eta GitHub planifikazioaren irudiak
│
└── doc/                     # GitHub Pages-erako memoria teknikoak (Markdown)
    ├── index.md             # Dokumentazioaren aurkibide nagusia
    ├── Sareak.md            # Sareak moduluaren memoria zehatza
    ├── Datu Baseak.md       # Datu-baseak moduluaren memoria zehatza
    ├── Digitalizazioa.md    # Digitalizazioa moduluaren memoria zehatza
    ├── Sistema Eragileak.md # Sistema eragileak moduluaren memoria
    ├── Markatze.md          # Markatze Lengoaiak txostena
    └── files/
        └── Streaming.accdb  # Microsoft Access datu-basearen fitxategia
```

---

## 3. Webguneko Fitxategi Nagusiak (HTML5)

Webguneko orri guztiak HTML5 estandarrean garatuta daude, etiketa semantikoak erabiliz (`<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`).

### 3.1. `index.html` (Hasiera)
* **Helburua:** Proiektuaren aurkezpen orri nagusia da.
* **Edukiak:**
  * Erronkaren helburu orokorra eta lortu nahi diren xedeak.
  * Modulu guztietara sartzeko txartel interaktiboak (`.flex-kaxak` bidez antolatuta).
  * Zerbitzariaren fitxa tekniko laburtua (Izena: `WindowsServer6Taldea`, IP: `192.168.70.2`, VirtualBox / IsardVDI parametroak, Windows Server eta IIS 80 ataka).
  * Nabigazio-menua eta oin-oharra (footer).

### 3.2. `sareak.html` (Sareak)
* **Helburua:** Sare fisikoko muntaia eta geruza fisiko/loturako kontzeptuak azaltzea.
* **Edukiak:**
  * OSI ereduaren 1. eta 2. geruzen azalpena rack-eko muntaian (UTP Cat 6, RJ-45, switch-a eta MAC helbidea: `52:54:00:1e:ab:f1`).
  * T568B kableatuaren pin-out taula eta testerraren bidezko jarraitutasun emaitzak.
  * `Admin_121` sistemako pasahitzaren ASCII bihurketa (72 bit).
  * CRC-6-GSM errore-kontrolaren kalkulua eta egiaztapena ($G(x) = x^6 + x^5 + x^3 + x^2 + x + 1$).
  * Modulazio digitalak (ASK, FSK, PSK eta Manchester) eta horien irudiak.
  * Ping bidezko konektibitate probak (kable bidez, Wi-Fi bidez eta gailu mugikorretik sarbidea).

### 3.3. `datu-baseak.html` (Datu-baseak)
* **Helburua:** Streaming zerbitzu baten datu-base erlazionalaren diseinu osoa erakustea.
* **Edukiak:**
  * Beharren analisia eta DBKG baten abantailak kalkulu-orri lauekin alderatuta.
  * Bi Entitate-Erlazio (E-R) proposamen: baztertutako eredua vs hautatutako eredua (`er-eredua-baztertua.jpg` eta `database.png`).
  * Eredu erlazionala taula formatuan, Lehen Mailako Gakoak (PK) eta Kanpoko Gakoak (FK) etiketatuta.
  * 3. Forma Normalerainoko (3NF) justifikazio teorikoa eta praktikoa.
  * Datuen erlazio-egitura: `Accounts`, `Profiles`, `Plans`, `Subscriptions`, `Renewals`, `Content`, `Genres`, `Content_Genres`, `Films`, `Series`, `Seasons`, `Episodes`, `Film_Views` eta `Episode_Views`.
  * Microsoft Access-erako txertatze eta ezabatze hurrenkera egokia (guraso-seme mendekotasunak).

### 3.4. `sistema-eragileak.html` (Sistema Eragileak)
* **Helburua:** Windows Server zerbitzariaren konfigurazioa, segurtasuna eta hedapena dokumentatzea.
* **Edukiak:**
  * Birtualizazio ingurunea (6 vCPU, 6 GB RAM, Vlan 70, Virtio diskoa).
  * Sarearen konfigurazioa: IP estatikoa (`192.168.70.2`), Atebidea (`192.168.70.254`), DNSak (`8.8.8.8` / `6.6.6.6`).
  * Tokiko erabiltzaileak (`Editorea`, `Irakurlea`) eta taldeak (`Erronka Editoreak`, `Erronka Irakurleak`).
  * Pasahitz eta kontu-blokeo politikak `secpol.msc` bidez.
  * NTFS baimenen esleipena karpetetan (`C:\Erronka Proba`).
  * Biltegiratze aurreratua: disko dinamikoak, RAID 1 (Ispilua) eta RAID 5 (Paritatea).
  * IIS web zerbitzariaren instalazioa, karpeta RAID bolumenean kokatzea eta Windows Defender Firewall sarrerako araua (PowerShell komandoz).
  * Windows Server Backup instalazioa eta hondamenen aurreko berreskuratze simulazioa.

### 3.5. `digitalizazioa.html` (Digitalizazioa)
* **Helburua:** Enpresaren eraldaketa digitala eta proiektuaren kudeaketa arina aurkeztea.
* **Edukiak:**
  * Digitalizazioaren hiru mailak: Digitization (digitalizatzea), Digitalization (prozesuak automatizatzea) eta Digital Transformation (eraldaketa digitala).
  * IT (Informazioaren Teknologiak) vs OT (Teknologia Operatiboak) konparaketa sakona taula bidez.
  * Industria 4.0ko Teknologia Gaitzaile Digitalak (THD): Cloud Computing, IoT, Big Data, Adimen Artifiziala, Zibersegurtasuna eta Green IT.
  * Proiektuaren planifikazioa eta jarraipena GitHub Projects bidez (Kanban metodologia: To Do, In Progress, In Review, Done).

---

## 4. Estiloak eta Diseinua (`css/estiloak.css`)

Webgune osoak estilo-orri bakar eta bateratua erabiltzen du (`css/estiloak.css`), Markatzeko Lengoaiak moduluaren **UD-02** unitateko edukiak zorrotz jarraituz:

* **Kutxa-eredua (Box Model):** `box-sizing: border-box;` orokorra erabiltzen da elementuen zabalera eta betegarriak (padding) zehatz kontrolatzeko.
* **Tipografia:** Taldearen erabakiz, tipografia (`"Times New Roman", Times, serif`) ezarri da testu arrunt zein izenburuetan. Kode zatientzat, ordea, `Courier New` erabiltzea erabaki dugu.
* **Kolore-paleta:** 
  * Goiburua eta oina: `#2b2b2b` (ikatz-gris iluna).
  * Atzeko planoa: `#eeeeee` (gris argi neutroa).
  * Atal nagusiak: `#ffffff` (txuria, ertz gris diskretuarekin).
  * Acentuazio-kolorea: `#c0392b` (gorri adreilua, goiburu-marretan, aktiboetan eta botoietan).
* **Flexbox Egiturak:** Kutxen banaketa dinamikoa (`display: flex; flex-wrap: wrap; gap: 12px;`) `.flex-kaxak` eta `.kaxa` klaseen bidez gauzatu da, txartelak lerrokatzeko.
* **Taulak:** Kolapso-ertzekin (`border-collapse: collapse;`), padding egokiekin eta goiburu nabarmenduekin, datu teknikoak argi irakurtzeko.
* **Diseinu Moldagarria (Responsive Web Design):** Media query baten bidez (`@media (max-width: 768px)`), pantaila txikietan eta gailu mugikorretan menua eta flexbox zutabeak bertikalki pilatzen dira, edukiaren irakurgarritasuna bermatuz.

---

## 5. Baliabide Grafikoak (`img/`)

Irudi guztiak tematikoki antolatuta daude azpikarpetetan, erraz aurkitzeko:

| Karpeta | Deskribapena | Fitxategi aipagarriak |
|---|---|---|
| `img/orokorrak/` | Webguneko elementu orokorrak | `logo.svg`. |
| `img/sareak/` | Sareetako kalkulu eta eskema errealak | `crc-kalkulua.jpg`, `crc-baieztapena.jpg`, `psk-ask-fsk.jpg`, `manchester-normala-diferentziala.jpg`. |
| `img/datu-baseak/` | E-R diagramak eta Access harremanak | `er-eredua-baztertua.jpg`, `database.png`, `accs-rela.jpg`, `datubaseak.png`. |
| `img/sistema-eragileak/` | Zerbitzariaren ebidentzia errealak | `isardvdi-makina.png`, `ip-konfigurazioa.png`, `windows-update.png`, `pasahitz-politikak.png`, `blokeo-politikak.png`, `tokiko-erabiltzaileak.png`, `tokiko-taldeak.png`, `ntfs-baimenak-proba.png`, `raid-kudeaketa.png`, `backup-instalazioa.png`. |
| `img/digitalizazioa/` | Kudeaketa arinaren ebidentziak | `kanban.jpg`, `gantt1.jpg`, `gantt2.jpg`, `milestones.jpg`, `labels.jpg`, `repo.jpg`. |

---

## 6. Dokumentazio Karpetaren Kudeaketa (`doc/`) eta GitHub Pages

Erronkaren beste eskakizun garrantzitsu bat dokumentazioa Markdown lengoaiaz idaztea eta GitHub Pages bidez hedatzea da:

* **`_config.yml`:** Jekyll motorra konfiguratzen du, `.md` fitxategiak web-orri bihur daitezen automatikoki.
* **`doc/index.md`:** Dokumentazioaren orri nagusia, modulu bakoitzeko txostenetara eramaten duten estekekin.
* **`doc/Sareak.md`:** Sareetako memoria integrala (Kableatua, OSI, ASCII kodeketa, CRC-6, modulazioak eta ping-ak).
* **`doc/Digitalizazioa.md`:** Digitalizazioaren txosten teorikoa eta praktikoa (IT vs OT, THD kontzeptuak, Gantt eta GitHub Projects kudeaketa).
* **`doc/Datu Baseak.md`:** Streaming datu-basearen memoria sakona (E-R erabakiak, Access-eko taulak, datu-motak eta erlazioak).
* **`doc/Sistema Eragileak.md`:** Zerbitzariaren instalazio eta mantentze gida.
* **`doc/files/Streaming.accdb`:** Microsoft Access formatuko fitxategi fisikoa, irakasleek zuzenean deskargatu eta erlazioak egiaztatu ahal izateko.


