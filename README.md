# 🛡️ Defense Logistics (DefLog)

**DefLog** je informacioni sistem za nabavke i logistiku u sektoru odbrane. Obuhvata tokove od tendera i ponuda, preko ugovora i narudžbina, do isporuke, testiranja, sertifikacije i održavanja vojne opreme u jedinicama i magacinima. Cilj je centralizacija podataka, transparentnost i sledljivost uz kontrolu rokova, troškova i kvaliteta.

---

## 📚 Sadržaj
- [Opis i ciljevi](#opis-i-ciljevi)
- [Specifikacija (KT1)](#specifikacija-kt1)
- [Entiteti i odnosi (sažetak)](#entiteti-i-odnosi-sažetak)
- [Obim projekta](#obim-projekta)
- [Obavezni EER koncepti](#obavezni-eer-koncepti)
- [Plan kontrolnih tačaka](#plan-kontrolnih-tačaka)
- [CASE alat i dijagrami](#case-alat-i-dijagrami)
- [Licenca i autori](#licenca-i-autori)

---

## 🎯 Opis i ciljevi
- **Domen:** nabavke i logistika u odbrani (tender → ponuda → ugovor → narudžbina → isporuka → testiranje → sertifikat → održavanje).
- **Problem:** rasejani i nepovezani podaci, bez end-to-end sledljivosti i kontrole rokova/troškova/kvaliteta.
- **Cilj:** centralizovan IS sa jasnim pravilima i ulogama, kompletnom sledljivošću i temeljem za ER model i implementaciju.

---

## ✅ Specifikacija (KT1)
Sadrži:  
**(A)** kratak opis domena, motivaciju i cilj; **(B)** uočene klase realnih entiteta i njihove odnose; **(C)** obim (~15 tipova entiteta sa pripadajućim poveznicima, po uzoru na „Košarku“); **(D)** primenu koncepata: *gerund, rekurzivni TP, slabi ID-zavisan, IS-A, kategorizacija*.  
*Referenca: smernice kursa za sadržaj KT1 i obim.*  

---

## 🧩 Entiteti i odnosi (sažetak)
**Entiteti (primeri):** Kompanija, Tender, Ponuda (*gerund*), Ugovor, Narudžbina, Stavka narudžbine (*slabi*), Proizvod, Komponenta (*slabi*), Kategorija proizvoda (*kategorizacija*), Isporuka, Magacin, Testiranje, Sertifikat, Održavanje, Osoba (IS-A: Oficir, Civilni radnik), Vojna jedinica.

**Odnosi (primeri kardinalnosti):**
- Kompanija ↔ Tender preko **Ponude** (*M:N*, Ponuda nosi atribute).
- Prihvaćena **Ponuda** → **Ugovor** (*1:1*).
- **Ugovor** → **Narudžbina** (*1:M*).
- **Narudžbina** → **Stavka narudžbine** (*1:M*, identifikujući).
- **Stavka** → **Proizvod** (*M:1*).
- **Proizvod** → **Kategorija proizvoda** (*M:1*).
- **Proizvod** → **Komponenta** (*1:M*, identifikujući).
- **Narudžbina** → **Isporuka** (*1:M*), **Isporuka** → **Magacin** (*M:1*).
- **Proizvod** → **Testiranje** (*1:M*), **Testiranje** → **Sertifikat** (*1:0..1*).
- **Proizvod** → **Održavanje** (*1:M*, izvršilac je **Osoba** u **Vojnoj jedinici**).
- **Oficir** → **Oficir** (rekurzivni *1:M*, nadređen–podređen).
- **Osoba** IS-A **Oficir**, **Civilni radnik** (računa se kao **1 TE** u obimu). 

---

## 📏 Obim projekta
Obim je usklađen sa smernicama: **≈15 tipova entiteta** sa pripadajućim tipovima poveznika (IS-A hijerarhija se računa kao **jedan** TE). Ovaj okvir služi kao ciljna veličina šeme proizašle iz specifikacije. 

---

## 🧠 Obavezni EER koncepti
- **Gerund**: *Ponuda* (povezuje Kompaniju i Tender, nosi atribute).
- **Rekurzivni TP**: Oficir —nadređen→ Oficir (*1:M*).
- **Slabi ID-zavisni TE**: *Stavka narudžbine* (identifikujuća veza sa Narudžbinom), *Komponenta* (identifikujuća veza sa Proizvodom).
- **IS-A hijerarhija**: Osoba → Oficir, Civilni radnik.
- **Kategorizacija**: Proizvod → Kategorija proizvoda.  
*Obavezno je da se svi ovi koncepti pojave barem jednom u šemi.* 

---

## 🗺️ Plan kontrolnih tačaka
- **KT1 – Specifikacija** (ovaj dokument).  
- **KT2 – ER dijagram + opis TE/TP** (SQL Developer Data Modeler).  
- **Final – Relacioni model + SQL skripte + implementacija i test podaci.** 

---

## 🛠️ CASE alat i dijagrami
- Za crtanje ER dijagrama koristi se **SQL Developer Data Modeler**.  
- Voditi računa o čitljivosti (po potrebi duplicirati TE radi manjeg presecanja linija).  
- ER dijagram je osnova za generisanje relacionog modela i SQL skripti na finalu.  

---

## 📄 Licenca i autori
- **Licenca:** MIT  
- **Autor:** _Bogdan Ljubinković_ — _SV2/2023_.  
- **Predmet/Asistent:** Baze podataka — _Veljko Bubnjević_. 

