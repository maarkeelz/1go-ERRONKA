# Datu-Basearen Diseinua eta Normalizazioa - Memoria Teknikoa

> **Modulua:** Datu-Baseak Kudeatzea (SISA 1)  
> **Taldea:** 6. Taldea  

---

## 1. Streaming Plataformaren Eskakizunak

Ikus-entzunezkoen plataforma batek behar hauek asetzen ditu:
* Bezero bakoitzak kontu nagusi bat sortzen du (`Accounts`), herrialde eta autentifikazio-datuekin.
* Kontu beraren barruan hainbat profil pertsonalizatu egon daitezke (`Profiles`), adin-kontrolarekin (`Is_Kids`).
* Harpidetza-plan desberdinak daude (`Plans`), gehienezko pantaila eta kalitate mugarekin.
* Katalogoak filmak eta serieak biltzen ditu (`Titles`), denboraldi eta atal bakoitzaren iraupenarekin (`Episodes`).
* Genero anitzak esleitu daitezke N:M erlazio baten bidez (`Title_Genres`).
* Ikustaldi bakoitzaren aurrerapena segundotan erregistratzen da (`Watch_History`).

---

## 2. E-R Proposamenak eta Hautatutako Eredua

### 2.1. 1. Proposamena (Baztertua)
* **Entitateak:** `USERS`, `USER ROLES`, `ROLES`, `PLANS`, `SUBSCRIPTIONS`, `CONTENT`, `VIEWS`.
* **Muga Nagusia:** Erabiltzailea eta rola taula elkartu batean zeuden, baina ez zuen baimentzen kontu batek hainbat ikusle-profil independente izatea (gomendioak nahastu egiten ziren). Gainera, atalak eta serieak ezin ziren bereizi.

### 2.2. 2. Proposamena (Hautatua eta Inplementatua)
* **Entitateak:** `Accounts`, `Profiles`, `Plans`, `Subscriptions`, `Titles`, `Episodes`, `Genres`, `Title_Genres`, `Watch_History`.
* **Abantailak:** Kontuak eta profilak argi banatuta daude, serieak eta filmak zehaztasunez kudeatzen dira eta ikustaldi bakoitzak zein segundotan gelditu den gordetzen du.

---

## 3. Eredu Erlazionala eta 3NF Normalizazioa

* **Accounts:** (`Account_ID` [PK], `Email`, `Password_Hash`, `Country`, `Created_At`)
* **Profiles:** (`Profile_ID` [PK], `Account_ID` [FK], `Name`, `Is_Kids`)
* **Plans:** (`Plan_ID` [PK], `Name`, `Monthly_Price`, `Max_Screens`, `Video_Quality`)
* **Subscriptions:** (`Subscription_ID` [PK], `Account_ID` [FK], `Plan_ID` [FK], `Start_Date`, `End_Date`, `Status`)
* **Titles:** (`Title_ID` [PK], `Name`, `Type`, `Release_Year`, `Age_Rating`)
* **Episodes:** (`Episode_ID` [PK], `Title_ID` [FK], `Season`, `Ep_Number`, `Duration_Min`)
* **Genres:** (`Genre_ID` [PK], `Name`)
* **Title_Genres:** (`Title_ID` [PK, FK], `Genre_ID` [PK, FK])
* **Watch_History:** (`Watch_ID` [PK], `Profile_ID` [FK], `Episode_ID` [FK], `Watched_At`, `Progress_Sec`)

### Normalizazio Garapena
* **1NF:** Eremu guztiak atomikoak dira (generoak taula elkartu baten bidez banatuta).
* **2NF:** Atributu guztiak PK osoaren menpekoak dira (ez zati batekiko).
* **3NF:** Dependentzia iragankor guztiak ezabatuta daude.

---

## 4. Microsoft Access Inplementazioa

* Erreferentzia-osotasuna aktibatuta dago erlazio guztietan.
* **Txertaketa ordena:** `Plans`, `Genres`, `Accounts` -> `Titles` -> `Subscriptions`, `Profiles` -> `Episodes` -> `Title_Genres` -> `Watch_History`.
* **Ezabatze ordena:** `Watch_History` -> `Title_Genres`, `Episodes` -> `Profiles`, `Subscriptions` -> `Titles`, `Plans`, `Genres`, `Accounts`.
