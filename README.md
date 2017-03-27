# Dynamic Client Registration
FIA tilbyr et REST API for administrasjon av klienter og ressurser.

## Identity Resource

En [identitetsressurs](http://docs.identityserver.io/en/release/reference/identity_resource.html) er et stykke data som tilhører en bruker, som for eksempel navn, e-postadresse og fødselsnummer. Det er et én-til- én forhold mellom identitetsressurser og tilhørende scope. En identitetsressurs kan imidlertid være tilknyttet flere claims, som representeres i utstedte identity tokens, eller hentes via UserProfile-endepunktet. Det finnes en mengde standardressurser i IdentityServer, men man kan også [konfigurere spesialtilpassede identitetsressurser](http://docs.identityserver.io/en/release/configuration/resources.html).

### Input

| Parameter | Datatype | Påkrevd | Beskrivelse |
| --- | --- | --- | --- |
| identity_resource_id | string | Kun ved oppdatering |
| name | string | Ja | Må være unikt |
| display_name | string | Nei | For bruk i consent screen |
| description | string | Nei | For bruk i consent screen |
| claims | string[] | Nei | For identity_token |

### Output

| Parameter | Datatype | Beskrivelse |
| --- | --- | --- |
| identity_resource_id | string | Generert id |
| name | string | |
| display_name | string | |
| description | string | |
| claims | string[] | |

## API Resource

En [API-ressurs](http://docs.identityserver.io/en/release/reference/api_resource.html) er et tjenestegrensesnitt som STS-en beskytter. I motsetning til identitetsressurser kan en API-ressurs være tilknyttet flere [scopes](http://docs.identityserver.io/en/release/configuration/resources.html), som igjen kan være konfigurert med [scope secrets](http://docs.identityserver.io/en/release/topics/secrets.html), som videre er en forutsetning for å kunne bruke utstedt reference token mot Introspection-endepunktet.

API-ressurser kan være tilknyttet flere claims, som representeres i utstedte access tokens.

### Input

| Parameter | Datatype | Påkrevd | Beskrivelse |
| --- | --- | --- | --- |
| api_respource_id | string | Kun ved oppdatering | |
| name | string | Ja | Må være unikt |
| display_name | string | Nei | For bruk i consent screen |
| description | string | Nei | For bruk i consent screen |
| claims | string[] | Nei | For access_token |
| scopes | Scope[] | Nei | |
| create_secret | boolean | Nei | For generering av API secret for bruk mot introspection endpoint |

#### Scope

```json
{
  "name": "",
  "display_name": "",
  "description": "",
  "user_claims": []
}
```

### Output

| Parameter | Datatype | Beskrivelse |
| --- | --- | --- |
| api_respource_id | string | Generert id |
| name | string | |
| display_name | string | |
| description | string | |
| claims | string[] | |
| scopes | Scope[] | |
| secret | string | Eventuelt generert API secret |
