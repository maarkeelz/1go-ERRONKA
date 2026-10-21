# Sareak eta Kableatu Egituratua - Memoria Teknikoa

> **Modulua:** Sareak Planifikatzea eta Administratzea (SISA 1)  
> **Taldea:** 6. Taldea  

---

## 1. 1. eta 2. OSI Geruzak Muntaian

### 1.1. Geruza Fisikoa (1. Geruza)
* **Bitarteko Fisikoa:** UTP Cat 6 (Kobre bidezko 4 pare bihurritu). 250 MHz arteko maiztasun-banda eta 1 Gbps abiadura bermatzen ditu.
* **Konektoreak:** RJ-45 arrak (patch kableen muturretan) eta RJ-45 emeak (Keystone moduluak patch panelean).
* **Funtzioa:** Bit-sekuentziak pultsu elektriko bihurtzea eta zaratarekiko blindatzea.

### 1.2. Datu-Loturaren Geruza (2. Geruza)
* **Helbideratzea:** 48 biteko MAC helbide fisikoak (adib. IsardVDIko sare-txartela: `52:54:00:1e:ab:f1`).
* **Hardwarea:** 2. geruzako switch-a. Switch-ak MAC helbideen taula dinamikoa eraikitzen du (CAM taula) talka-domeinuak banatzeko.
* **Trama Egitura:** Ethernet II trama, karga erabilgarria eta FCS (Frame Check Sequence).

---

## 2. Kableatu Egituratua: Muntaia eta Tester Emaitzak

### 2.1. T568B Estandarraren Muntaia
Kableatu egituratuaren patch kable guztiak T568B arauaren arabera muntatu dira:
1. Zuri - Laranja
2. Laranja
3. Zuri - Berdea
4. Urdina
5. Zuri - Urdina
6. Berdea
7. Zuri - Marroia
8. Marroia

### 2.2. Testerraren Egiaztapena
Tester bidez 1etik 8rako pin guztiek jarraitutasun elektriko egokia dutela baieztatu da.

---

## 3. ASCII Kodeketa eta CRC-6-GSM Kalkulua

### 3.1. Probako Pasahitza: `Admin_123`
* **Kate erabilia:** `Admin_123`
* **ASCII Bitarra (72 bit):**
  `01000001 01100100 01101101 01101001 01101110 01011111 00110001 00110010 00110011`
* **Karaktereka:**
  - `A`: 65 -> `01000001` (0x41)
  - `d`: 100 -> `01100100` (0x64)
  - `m`: 109 -> `01101101` (0x6D)
  - `i`: 105 -> `01101001` (0x69)
  - `n`: 110 -> `01101110` (0x6E)
  - `_`: 95 -> `01011111` (0x5F)
  - `1`: 49 -> `00110001` (0x31)
  - `2`: 50 -> `00110010` (0x32)
  - `3`: 51 -> `00110011` (0x33)

### 3.2. CRC-6-GSM Polinomio Sortzailea
* **Polinomioa:** $G(x) = x^6 + x^5 + x^3 + x^2 + x + 1$
* **Bit Bitartekoa:** `1101111` (7 biteko zatitzailea)
* **Kalkulua:**
  1. 72 biteko datu-kateari 6 zero gehitzen zaizkio amaieran ($x^6$): 78 biteko katea.
  2. Modulo-2 zatiketa (XOR logika) aplikatzen da $1101111$-rekin.
  3. Lortutako 6 biteko hondarra: **`011010`** (Hamartarra: `26`, Hamaseitarra: `0x1A`).

---

## 4. Seinale Modulazioak

* **ASK(2):** Anplitudearen modulazioa. '1' uhin altua, '0' uhin nulua.
* **FSK(2):** Maiztasunaren modulazioa. '1' maiztasun handia, '0' maiztasun txikia.
* **PSK(2):** Fasearen modulazioa (BPSK). 180 graduko fase-jauzia egoera aldatzean.
* **Manchester:** Seinale digitala oinarri-bandan. Trantsizioa bit bakoitzaren erdialdean sinkronizazioa bermatzeko.

---

## 5. Konektibitate Probak

* **Kablez (Ethernet):** Ping `192.168.70.2` (WindowsServer6Taldea) -> 0 % galera, batez besteko latentzia < 1 ms.
* **Wi-Fi (5 GHz):** Ping `192.168.70.2` -> 0 % galera, batez besteko latentzia 3.2 ms.
* **Mugikorreko Sarbidea:** Smartphone bidez `http://192.168.70.2` atarira sartzea baieztatu da.
