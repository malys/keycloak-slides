---
title: Keycloak 
theme: league
revealOptions:
    slideNumber: true
#https://github.com/hakimel/reveal.js/wiki/Keyboard-Shortcuts
# S Speaker Notes view
# Alt+ click zoom
# Esc slide overview
---

# Keycloak 
<img class="centerImage" src="./img/keycloak_icon_512px.png" alt="Keycloak" style="width: 40%;"/>

Note:
    http://webpro.github.io/reveal-md/
    reveal-md Readme.md  -w
    # add C:\Program Files (x86)\Nodist\bin\node_modules\reveal-md\lib\print.js "" over ${printPluginPath}
    reveal-md Readme.md --static ./docs
    "http://localhost:1948/archi.keycloak.prez.md?print-pdf" => print chrome

----
## RH-SSO

RedHat supported version of Keycloak.

----
* Production ready
    * compatibility
* Maintainability
    * 1 minor release a year (2019- 7.3)
    * 3 major releases a year (2019 - 7.0, 6.0, 5.0)

---
## Why delegate security layer?

<img class="centerImage" src="./img/security.jpg" alt="Keycloak" style="width: 60%;"/>

----
* Open source
* security skills
* extended features
* provided updates

Note:
    Gatekeeper
    I'm expert i code my login page for mobile apps, Kerberos
    expert not infallible

----

* Cost
    * integration over development
    * configuration

---
## IAM: security component

<img class="centerImage" src="./img/BackBox_Software_Identity_And_Access_Management.jpg" alt="Keycloak" style="width: 60%;"/>

Note:
    IAM
----

* Authentication (AuthN)
* Authorization (AuthZ)
* Auditing
* Administration

Note:
    identification
    role
    Traçabilité
    Maintenabilité
----
### Definition

* Single Sign On (SSO)
* Single Log Out (SLO)
<img class="centerImage" src="./img/sso.png" alt="Keycloak" style="width: 60%;"/>


----
## Authentication/Authorization mechanisms

----

### Basic Auth

<img class="centerImage" src="./img/kilt.jmg.jpg" alt="Keycloak" style="width: 60%;"/>
----

* Easy integration

*Authorization Basic Base64(user:password)*

----
* 1 query -> 1 authentication check
    * DDoS attack
* Unencrypted password (HTTPS)
    * Password interception
* Authorization only    

----

## OAuth 2.0

<img class="centerImage" src="./img/oauth2.png"  style="width: 40%;"/>

----
* Released in 2006: 2.0
* Oriented simplicity

Note:
    IETF OAuth Working Group.

----
* High security flows
    * use token (limited lifetime)
    * n queries -> 1 password transmission
* 1 query -> 1 token check

----
* JSON Web Tokens

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
eyJzdWIiOiIxMjM0...iaWF0IjoxNTE2MjM5MDIyfQ.
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

----
```
{
  "alg": "HS256",
  "typ": "JWT"
}
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```

----
* Large adoption

Google, Facebook, ...


----
* More complex to integrate
* No authentication information
    * No SSO or SLO
    * No standard API for identity

----
### OpenID Connect

<img class="centerImage" src="./img/openidConnect.jpg"  style="width: 40%;"/>
----

* Developed by OpenID Foundation
    * modern use cases
* Released in 2014: 1.0
* OpenID Connect is an identity layer on top of the OAuth 2.0.


Note:
    SPA
    Mobile
    Microservice

----

* OAuth 2.O
* IDToken (JWT tokens) (user info  + API)
* Discovery and self registration
* SSO/ SLO
* Back/Front channel
* Identity broker (google, delegation)
* n query -> 1 password transmission
* 1 query -> authorization + authentication

Note:
    JWT -> pronounce JOT
    integrity no confidential

----

* More complex to integrate

----

### Security Assertion Markup Language 2.0

* Developed by OASIS (consortium)
* Released in 2005: 2.0
* Authentication (AuthN)
* Authorization (AuthZ)

----
* Tested and feedback

* Complex to integrate

---

## Supported mechanisms
----
  
* OAuth 2.0
* SAML 2.0
* OpenID Connect 1.0

---

## Focus on OIDC

----

### Glossary
----

#### Elements
----

##### Realm

<img class="centerImage" src="./img/realm.jpg"  style="width: 60%;"/>

Note:
    Territoire
    Who are you? Rights ? Dress code
----

##### Client

<img class="centerImage" src="./img/client.jpg"  style="width: 40%;"/>

Note:
    Configuration liée à une application ou une famille d'appli
    
----
##### Role

<img class="centerImage" src="./img/role.jpg"  style="width: 60%;"/>

Note: 
    Droit

----
##### Claims

<img class="centerImage" src="./img/claim.jpg"  style="width: 60%;"/>

Note: 
    Attribut déclaré
    2FA phone number
    ##### Scope
    <img class="centerImage" src="./img/scope.png"  style="width: 30%;"/>

----

#### OIDC actors
----

<img class="centerImage" src="./img/RessourceOwner.png"  style="width: 30%;"/>

Note:
    Consommateur ou propriétaire de la resource
----
<img class="centerImage" src="./img/RelyParty.png"  style="width: 30%;"/>


Note:
    Façade gérant le flux d'authentification
----
<img class="centerImage" src="./img/ResourceServer.png"  style="width: 30%;"/>


Note:
    Serveur de ressources (confonfu avec le RP) 

----
<img class="centerImage" src="./img/IdentityProvider.png"  style="width: 30%;"/>

Note:
    Keycloak: gestionnaire
    https://www.youtube.com/watch?v=6DxRTJN1Ffo
    https://www.youtube.com/watch?v=1ZX7554l8hY

----

### OIDC Grants

<img class="centerImage" src="./img/communication.png"  style="width: 100%;"/>


Note:
    acteurs communiquent pour former un processus d'authentification et d'authorisation

----

<img class="centerImage" src="./img/Grant.png"  style="width: 100%;"/>

Note:
    2 étapes ou 3 étapes

----

#### Access type
----

<img class="centerImage" src="./img/confidential.png"  style="width: 40%;"/>

----
<img class="centerImage" src="./img/public.png"  style="width: 60%;"/>
----

#### Channel
----

<img class="centerImage" src="./img/BackFront.png"  style="width: 100%;"/>

----

### Grants

----

### Client credentials (2)

<img class="centerImage" src="./img/clientCredentials.png"  style="width: 100%;"/>

Note:
    compte de service
    client -> confidential -> secret

----

```

- post:
    url: "/auth/realms/{{ realm }}/protocol/openid-connect/token"
    body:   'grant_type=client_credentials&
            client_id={{ cliendId }}&
            client_secret={{ secret }}'
    capture:
    - json: "$.access_token"
    - json: "$.refresh_token"
```  

Note: 
    access token
    refresh token

----

```
- post:
    url: "/auth/realms/{{ realm }}/protocol/openid-connect/userinfo"
    headers:
      "Authorization": "Bearer {{ access_token }}"
```

----

### Resource owner credentials (2)

grant_type: password

Note:
    Legacy compatibility
    Basic auth

----

<img class="centerImage" src="./img/resourceGrant.png"  style="width: 100%;"/>
----

### Implicit (2)

<img class="centerImage" src="./img/implicit.png"  style="width: 100%;"/>

Note:
    Access token + IDToken direct
    without refresh token
    token in redirect_uri

----

### Authorization Code (3)

<img class="centerImage" src="./img/authorizationGrant.png"  style="width: 100%;"/>

----

[Demo](https://openidconnect.net/)

Note:
    admin https://xxx/auth/admin/master/console/#/realms
    Config:
        https://xxx/auth/realms/demo/protocol/openid-connect/auth

        https://xxx/auth/realms/demo/.well-known/openid-configuration
        client: public
    https://tools.ietf.org/html/rfc7517    
    * kid: identifiant de la clé    
    * access
    * refresh
    * IDToken
    * Offline Token
    * Claims
    --> Hybrid
    Implicit / Authorization
    The authorization server will respond with both a code (which the client can exchange for tokens on a secure channel) and a token. A common use case for the hybrid flow is using the code to get an access token on the server, and directly consuming an ID token on the client.

---

### Integration guideline

----

##### Flow

----

|                   | Authorization code | Client  credentials | Resource owner
|---                | ---                | ---                 | ---
|Web App (Template) |        |                     | 
|SPA                |              |                     | 
|Backend (API)      |                    |               | 
|Mobile             |        |                     | 
|CLI                |                    |                     | 

Note:
    * Implicit: No refresh token, access token long life
        * token in redirect_uri
    * Resource owner credentials: legacy or CLI

----

|                   | Authorization code | Client  credentials | Resource owner
|---                | ---                | ---                 | ---
|Web App (Template) | confidential       |                     | 
|SPA                |              |                     | 
|Backend (API)      |                    |             | 
|Mobile             |        |                     | 
|CLI                |                    |                     | 

Note:
    * Implicit: No refresh token, access token long life
        * token in redirect_uri
    * Resource owner credentials: legacy or CLI

----

|                   | Authorization code | Client  credentials | Resource owner
|---                | ---                | ---                 | ---
|Web App (Template) | confidential       |                     | 
|SPA                | public             |                     | 
|Backend (API)      |                    |              | 
|Mobile             |        |                     | 
|CLI                |                    |                     | 

Note:
    * Implicit: No refresh token, access token long life
        * token in redirect_uri
    * Resource owner credentials: legacy or CLI

----

|                   | Authorization code | Client  credentials | Resource owner
|---                | ---                | ---                 | ---
|Web App (Template) | confidential       |                     | 
|SPA                | public             |                     | 
|Backend (API)      |                    | API Key             | 
|Mobile             |        |                     | 
|CLI                |                    |                     | 

Note:
    * Implicit: No refresh token, access token long life
        * token in redirect_uri
    * Resource owner credentials: legacy or CLI

----

|                   | Authorization code | Client  credentials | Resource owner
|---                | ---                | ---                 | ---
|Web App (Template) | confidential       |                     | 
|SPA                | public             |                     | 
|Backend (API)      |                    | API Key             | 
|Mobile             | confidential       |                     | 
|CLI                |                    |                     | 

Note:
    * Implicit: No refresh token, access token long life
        * token in redirect_uri
    * Resource owner credentials: legacy or CLI

----

|                   | Authorization code | Client  credentials | Resource owner
|---                | ---                | ---                 | ---
|Web App (Template) | confidential       |                     | 
|SPA                | public             |                     | 
|Backend (API)      |                    | API Key             | 
|Mobile             | confidential       |                     | 
|CLI                | public             |                     | compatibility

Note:
    * Implicit: No refresh token, access token long life
        * token in redirect_uri
    * Resource owner credentials: legacy or CLI
        
----
##### Architecture / Security

----
**use ONLY OIDC standard endpoints**

*(exclude Keycloak admin API use)*

<img class="centerImage" src="./img/keycloak_no.png"  style="width: 40%;"/>

Note:
    Portability
    adhérence avec faible Keycloak
    Security

----

**define UNIQUE responsibility and UNIQUE owner for data**

*(unique user reference)*

<img class="centerImage" src="./img/spaghetti-781795_640.jpg"  style="width: 40%;"/>


Note:
    limit complexity
    easy architecture

----

|                                   | Keycloak              | Application         |
|---                                | ---                   | ---                 |
|New microservice (light)           | users,roles,claims    | (1)                 |
|New microservice (complex)         |                  |   |
|Legacy application                 |                    |   |

Note:
    (1) No user management UI
    (2) Synchronization (user: full, roles/claims: partial)

----

|                                   | Keycloak              | Application         |
|---                                | ---                   | ---                 |
|New microservice (light)           | users,roles,claims    | (1)                 |
|New microservice (complex)         | (2)                   | users,roles,claims  |
|Legacy application                 | (2)                   | users,roles,claims  |

Note:
    (1) No user management UI
    (2) Synchronization (user: full, roles/claims: partial)    

----

**split public and private resources**

*(Front office for administration and another for customers = 2 APIs)*

<img class="centerImage" src="./img/publicPrivate.jpg"  style="width: 60%;"/>
 
----
**One realm by security strategy**

<img class="centerImage" src="./img/europe.jpg"  style="width: 60%;"/>

Note:
    Password rule, expiration

----
**One application container by realm**

<img class="centerImage" src="./img/microservice.png"  style="width: 60%;"/>

Note:
    NOT 1 container -> 2 realms
    domain architecture


----
**One style guide by realm**

*(Unique corporate identity for login and email)*

<img class="centerImage" src="./img/website-1624028_640.png"  style="width: 60%;"/>

----
**Clean and easy users management**

<img class="centerImage" src="./img/clean-571679_640.jpg"  style="width: 60%;"/>

----
* Mandatory, unique, case insensitive username
* Mandatory, unique, case insensitive and validated email address
* Efficient and limited roles definition
* Limited claims definition
    (not use personal data if not  necessary)

----
**Developer platform**
*(docker image + dev shared profile)*

<img class="centerImage" src="./img/entrepreneur-593352_640.jpg"  style="width: 60%;"/>

----

##### Business

----

**Business domains and trademarks isolation**


<img class="centerImage" src="./img/white-label-3790523_640.jpg"  style="width: 60%;"/>

Note:
    SSO Monetique Luma
    While label isolated
 
----
**Limit account duplication**


<img class="centerImage" src="./img/stormtrooper-1343772_640.jpg"  style="width: 70%;"/>

Note:
    Internal realm

---

## Extensions
----

### Theme

<img class="centerImage" src="./img/CollectTemplate.png"  style="width: 80%;"/>

----
### Federation
----

<img class="centerImage" src="./img/federation1.png"  style="width: 60%;"/>
<img class="centerImage" src="./img/federation2.png"  style="width: 60%;"/>
---

## Adapters
----

* Java
* JBossEAP/Wildfly
* Spring
* NodeJS
----

* Keycloak GateKeeper

Note:
    Architecture

----

* API Gateway
* Service Mesh

---

<img class="centerImage" src="./img/thank-you-2490552_1280.png"  style="width: 100%;"/>

---

<img class="centerImage" src="./img/question-mark-1872665_1280.jpg"  style="width: 100%;"/>
