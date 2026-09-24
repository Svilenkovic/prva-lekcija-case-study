<a href="https://prvalekcija.com/"><img src="media/cover.jpg" alt="Prva Lekcija, naslovna strana na laptopu i telefonu" width="100%"></a>

# Prva Lekcija

Sajt za pripremu učenika za hrvatsku državnu maturu u Zagrebu, sa nalozima i materijalom koji se isporučuje tek kad Stripe potvrdi uplatu.

**[prvalekcija.com](https://prvalekcija.com/)** · [Studija slučaja](https://svilenkovic.rs/radovi/prva-lekcija) · [English](README.md)

> [!NOTE]
> Klijentski projekat. Izvorni kod pripada klijentu i čuva se u privatnom repozitorijumu. Ova stranica opisuje šta sam uradio i kako.

<table>
  <tr><td><b>Klijent</b></td><td>Prva Lekcija</td></tr>
  <tr><td><b>Delatnost</b></td><td>Priprema za hrvatsku državnu maturu: instrukcije, eseji i online predavanja</td></tr>
  <tr><td><b>Lokacija</b></td><td>Zagreb, Hrvatska</td></tr>
  <tr><td><b>Vrsta</b></td><td>Sajt sa nalozima i online naplatom</td></tr>
  <tr><td><b>Moj deo posla</b></td><td>Dizajn, izrada, naplata, SEO, hosting i održavanje</td></tr>
  <tr><td><b>Tehnologije</b></td><td>PHP 8.3, MariaDB, Stripe Checkout, nginx, Tailwind</td></tr>
</table>

## O projektu

Prva Lekcija iz Zagreba sprema učenike za hrvatsku državnu maturu: instrukcije, eseji pisani po službenim kriterijima bodovanja i online predavanja iz matematike i fizike. Sajt je na hrvatskom i morao je da prodaje digitalni materijal. Učenik plati karticom i odmah dobije fajl, koji posle nalazi na svom nalogu, sa bilo kog uređaja, ili u mejlu ako je kupio bez naloga.

U naplati pregledač ne odlučuje ni o čemu. Sa sajta odlazi samo oznaka proizvoda; server upisuje kupovinu u stanju pending pre nego što otvori Stripe Checkout, a jedna funkcija je uslovnim upisom prebacuje u completed. Tu funkciju zovu i povratna strana i Stripe webhook, pa se materijal isporuči tačno jednom. Nijedno od njih ne veruje zahtevu: povratna strana ponovo pita Stripe za sesiju, a webhook mora da ima ispravan potpis.

## Šta sam uradio

- Registracija, prijava i nalog sa spiskom kupovina, uz ograničenje pokušaja prijave, nov ID sesije posle prijave i CSRF token na svakoj izmeni
- Mali Stripe klijent na cURL-u sa fiksiranom verzijom API-ja umesto celog SDK-a; podaci o kartici nikad ne stižu na ovaj server
- Isključeno Stripe-ovo automatsko preračunavanje valute, pošto je prava kupovina pokazala da posetilac van evrozone vidi preračunat iznos po lošijem kursu od cene na sajtu
- Kontakt forma je ranije ispisivala potvrdu, a ništa nije slala; sada proverava podatke na serveru, ima polje-mamac i limit po IP adresi i upisuje poruku u bazu pre slanja mejla
- Keš strana u nginx-u za anonimne posetioce; sesija se nastavlja samo ako njen kolačić već postoji, pa slučajni posetilac ne dobija kolačić koji bi zaobišao keš
- Admin panel za korisnike, proizvode, kupovine i poruke, sa dnevnikom izmena i pravilom da administrator ne može da obriše sebe ni da sebi oduzme prava

## Merenja

| | Performanse | Pristupačnost | Dobre prakse | SEO |
| :-- | :-: | :-: | :-: | :-: |
| Telefon | 100 | 100 | 100 | 100 |
| Desktop | 100 | 100 | 100 | 100 |

PageSpeed Insights, laboratorijsko merenje živog sajta, septembar 2026. Sigurnosna zaglavlja: 6 od 6. HTML validator: bez grešaka. axe provera pristupačnosti: bez prekršaja. Strukturisani podaci: `EducationalOrganization`.

## Snimci ekrana

<table>
  <tr>
    <td width="68%" valign="top"><img src="media/desktop.webp" alt="Prva Lekcija, naslovna strana na ekranu širine 1440 px"></td>
    <td width="32%" valign="top"><img src="media/mobile.webp" alt="Prva Lekcija, naslovna strana na telefonu"></td>
  </tr>
</table>

<img src="media/inner-1.webp" alt="Naši materijali: instrukcije, eseji i online predavanja, svaki sa svojom stranom">
<sub>Naši materijali: instrukcije, eseji i online predavanja, svaki sa svojom stranom</sub>

<img src="media/inner-2.webp" alt="Kontakt: forma koja upit prvo upiše u bazu, pa tek onda pokuša da pošalje mejl">
<sub>Kontakt: forma koja upit prvo upiše u bazu, pa tek onda pokuša da pošalje mejl</sub>

---

<sub>Izrada: [D. Svilenković](https://svilenkovic.rs).</sub>
