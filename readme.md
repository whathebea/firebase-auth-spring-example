## Configuração simples para validação de JWT do Firebase no Spring (2023)
Devido a atualização no Spring Security, WebSecurityConfigurerAdapter foi deprecado. Portanto, eu realizei a atualização [desse tutorial](https://medium.com/comsystoreply/authentication-with-firebase-auth-and-spring-security-fcb2c1dc96d) para a versão atual do Spring Security.
**É NECESSÁRIO REALIZAR A CRIAÇÃO DO PROJETO NO FIREBASE**

Fazer a chamada:

    curl --location --request POST 'https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword?key=(CHAVE_API)
    ' \
    --header 'content-type: application/json' \
    --data-raw '{
        "email": "SEU_EMAIL",
        "password": "SUA_SENHA",
        "returnSecureToken": true
    }'

**RESPOSTA DA CHAMADA:**

    {
        "kind": "identitytoolkit#VerifyPasswordResponse",
        "localId": "LOCALID",
        "email": "EMAIL",
        "displayName": "",
        "idToken": "TOKEN_QUE_USAREMOS_NA_CHAMADA",
        "registered": true,
        "refreshToken": "REFRESH_TOKEN",
        "expiresIn": "3600"
    }

**CHAMADA NA API SPRING BOOT**

    curl --location --request GET 'http://localhost:8080/hello' \
    
    --header 'Authorization: Bearer SEU_ID_TOKEN' \

**RESULTADO ESPERADO:** 200 OK - BODY: "Hello World!"


**RESULTADO SEM AUTENTICAÇÃO:** 401 UNAUTHORIZED - BODY: Vazio

_A URL padrão das chaves do firebase se encontra como uma propriedade no application.properties_