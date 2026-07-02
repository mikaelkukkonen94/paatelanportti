# Työntekijäportaalin käyttöönotto

Sivustolle on lisätty ylläpitopohja osoitteeseen `/admin/`.

Tämä portaali on tarkoitettu Netlify Identity + Git Gateway -kirjautumiseen. Sen avulla henkilökunta voi muokata:

- viikon lounaslistaa
- tapahtumakalenteria
- kahvion ja keittiön ruokalistaa
- sivuston kuvia, kuten herokuvaa, galleriaa, menu-kuvia ja tapahtumajulisteita

## Tärkeää

Portaali ei voi tallentaa muutoksia turvallisesti pelkällä käsin Netlifyyn pudotetulla zip-paketilla. Jotta työntekijät voivat kirjautua, vaihtaa kuvia ja päivittää sisältöjä itse, sivusto kannattaa liittää GitHubiin ja Netlifyssä pitää ottaa käyttöön:

1. Identity
2. Git Gateway
3. kutsutut käyttäjät eli työntekijöiden sähköpostit

Kun nämä on tehty, työntekijät menevät osoitteeseen:

`https://paatelanportti.com/admin/`

ja kirjautuvat omalla kutsutulla sähköpostillaan.
