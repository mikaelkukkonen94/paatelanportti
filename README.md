# Paatelan Portti - julkaisupaketti

Tämä kansio sisältää sivuston julkaisuun tarvittavat tiedostot.

## Tärkeät yhteystiedot

- Puhelin ja WhatsApp: `040 755 7155`
- Tarjouslomakkeen sähköposti: `ravintola@paatelanportti.com`
- Osoite: `Äänekoskentie 842, 44200 Suolahti`

## Lounaslista

Menu-osion lounaslista päivittyy tiedostosta `weekly-menu.json`.

Kokin tai ylläpitäjän tarvitsee vaihtaa vain `menu`-tekstit. Päivämäärän voi
päivittää kohtaan `updated`, jotta tiedetään milloin lista on viimeksi
vaihdettu.

Muoto:

```json
{
  "updated": "2026-06-28",
  "items": [
    { "day": "Ma", "menu": "Vaihtuva lounas tai päivänkeitto" },
    { "day": "Ti", "menu": "Vaihtuva lounas tai päivänkeitto" },
    { "day": "Ke", "menu": "Vaihtuva lounas tai päivänkeitto" },
    { "day": "To", "menu": "Vaihtuva lounas tai päivänkeitto" },
    { "day": "Pe", "menu": "Vaihtuva lounas tai päivänkeitto" }
  ]
}
```

## Tapahtumakalenteri

Juhlaosion tapahtumakalenteri päivittyy tiedostosta `events-calendar.json`.
Torstain ja perjantain karaoket voi pitää vakiona. Lauantain kohtaan voi lisätä
viikonlopun esiintyjän, tanssi-illan tai elävän musiikin tiedot.

Muoto:

```json
{
  "updated": "2026-06-28",
  "items": [
    {
      "day": "Torstaisin",
      "time": "klo 18.00",
      "title": "Kanavakaraoke",
      "description": "Vetäjänä tuttu Timo Kolu."
    }
  ]
}
```

Kun `weekly-menu.json` tai `events-calendar.json` on muutettu, julkaise koko
`outputs`-kansio uudestaan Netlifyyn. Sen jälkeen muutokset näkyvät kaikille
asiakkaille.

## Tarjous- ja palautelomakkeet

Lomakkeet on tehty Netlify-yhteensopiviksi:

- tarjouslomakkeen nimi: `tilaisuus-tarjouspyynto`
- asiakaspalautelomakkeen nimi: `asiakaspalaute`
- kiitossivu: `kiitos.html`
- ilmoitukset ohjataan Netlifyssä sähköpostiin `ravintola@paatelanportti.com`

Sama ohje löytyy erillisenä tiedostona: `NETLIFY-LOMAKEASETUKSET.md`.

## Julkaisu Netlifyyn

1. Vie koko `outputs`-kansio Netlifyyn.
2. Netlify käyttää tiedostoa `netlify.toml`.
3. Publish directory on `.` eli tämän kansion juuri.
4. Tarkista julkaistu sivu puhelimella ja tietokoneella.
5. Testaa puhelu-, WhatsApp-, kartta- ja lomakelinkit.
