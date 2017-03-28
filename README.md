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

## Client

En [klient](http://docs.identityserver.io/en/release/configuration/clients.html) er en applikasjon som kan forespørre tokens fra STS-en. De mest sentrale informasjonselementene for en klient er som følger:
-	En unik klientidentifikator
-	En hemmelighet, hvis nødvendig
-	Tillatte grant types
-	URL-er til hvilke nettleseren skal omdirigeres (tilbake) til etter å ha vært innom STS-en for inn- eller utlogging
-	Tillatte scopes
-	[Øvrige informasjonselementer](http://docs.identityserver.io/en/release/reference/client.html)

### Input

| Parameter | Datatype | Påkrevd | Defaultverdi | Beskrivelse |
| --- | --- | --- | --- | --- |
| client_id | string | Kun ved oppdatering | | OIDC-standard |
| client_name | string | Ja | | OIDC-standard - Må være unikt |
| redirect_uris | string | Nei | | OIDC-standard | Må være https |
| grant_types | string[] | Ja | | OIDC-standard - authorization_code, client_credentials, hybrid, implicit |
| absolute_refresh_token_lifetime | int | Nei | 2 592 000 | |
| access_token_lifetime | int | Nei | 3600 | |
| access_token_type | string | Nei | jwt | jwt, reference |
| allow_access_tokens_via_browser | boolean | Nei | false | |
| allow_refresh_token | boolean | Nei | false | |
| always_include_user_claims_in_identity_token | boolean | Nei | false | |
| always_send_client_claims | boolean | Nei | false | |
| authorization_code_lifetime | int | Nei | 300 | |
| identity_provider_restrictions | string[] | Nei | | |
| identity_token_lifetime | int | Nei | 300 | |
| logout_uri | string | Hvis redirect-basert grant-type | | |
| post_logout_redirect_uris | string[] | Nei | | |
| refresh_token_expiration | string | Nei | absolute | absolute, sliding |
| refresh_token_usage | string | Nei | one_time_only | one_time_only, reuse |
| require_client_secret | boolean | Nei | false | |
| sliding_refresh_token_lifetime | int | Nei | 1 296 000 | |
| client_claims | ClientClaim[] | Nei | | |
| scopes | string[] | Nei | | Tillatte scopes - globale eller definert som Identity Resource eller under API Resources |
| create_secret | boolean | Nei | false | For generering av client_secret |

### Output

| Parameter | Datatype | Beskrivelse |
| --- | --- | --- |
| client_id | string | OIDC-standard - Generert id |
| client_name | string | OIDC-standard |
| redirect_uris | string | OIDC-standard  |
| grant_types | string[] | OIDC-standard |
| absolute_refresh_token_lifetime | int | |
| access_token_lifetime | int | |
| access_token_type | string | |
| allow_access_tokens_via_browser | boolean | |
| allow_refresh_token | boolean | |
| always_include_user_claims_in_identity_token | boolean | |
| always_send_client_claims | boolean | |
| authorization_code_lifetime | int | |
| identity_provider_restrictions | string[] | |
| identity_token_lifetime | int | |
| logout_uri | string | |
| post_logout_redirect_uris | string[] | |
| refresh_token_expiration | string | |
| refresh_token_usage | string | |
| require_client_secret | boolean | |
| sliding_refresh_token_lifetime | int | |
| client_claims | ClientClaim[] | |
| scopes | string[] | Nei | |
| create_secret | boolean | |
