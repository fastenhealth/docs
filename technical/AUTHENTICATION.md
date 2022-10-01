# Authentication

## OAuth/Smart-on-FHIR
- https://build.fhir.org/ig/HL7/smart-app-launch/scopes-and-launch-context.html
- [https://usefulangle.com/post/4/javascript-communication-parent-child-window](https://usefulangle.com/post/4/javascript-communication-parent-child-window)
- [https://build.fhir.org/ig/HL7/smart-app-launch/app-launch.html](https://build.fhir.org/ig/HL7/smart-app-launch/app-launch.html)
- [https://auth0.com/docs/flows/concepts/auth-code-pkce](https://auth0.com/docs/flows/concepts/auth-code-pkce)
- [https://build.fhir.org/ig/HL7/smart-app-launch/example-app-launch-public.html#step-5-access-token](https://build.fhir.org/ig/HL7/smart-app-launch/example-app-launch-public.html#step-5-access-token)
- 



```mermaid
sequenceDiagram
    participant User
    participant Fasten App
    participant Lighthouse
    participant Medical Record Source
	

    User->>Fasten App: 1. Click login link.

	Fasten App->>Lighthouse: 2. Request Source configuration information

    loop challenge
    Fasten App->Fasten App: 3. Generate code verifier and code challenge.
    end
    
    Fasten App->>Medical Record Source: 4. Authorization code request and code challenge to authorize.
    Medical Record Source->>User: 5. Redirect to login/authorization prompt.

	loop wait-for-code
    Fasten App->Lighthouse: 6. Check if authorization code available
    end

    User->>Medical Record Source: 7. Authenticate and consent
    Medical Record Source->>Lighthouse: 8. Authorization code stored.
    Fasten App->>Medical Record Source: 9. Authorization code and code verifier sent for OAuth token.
    
    loop validate
    Medical Record Source->Medical Record Source: 10. Validate code verifier and challenge.
    end
    
    Medical Record Source->>User: 11. ID token, access token and, optionally, refresh token
    User->>Fasten App: 12. Store access token and request patient medical records.
    Fasten App->>Medical Record Source: 13. Electronic medical records retrieved
    Fasten App->>User: 14. Response.

```





> The PKCE authorization code flow adds a secret (a `code_verifier` generated using SHA-256) created by the client application that is verified by the authorization server. The client application creates a transform value (hash string) of the `code_verifier` called the `code_challenge` which is sent using HTTPS to retrieve an authorization code. A malicious attacker can intercept this code, but cannot exchange it for a token without the `code_verifier`.
> 
> https://andrewowen.net/blog/creating-diagrams-with-mermaid/

The Fasten Lighthouse service acts like a man-in-the-middle, however it only has access to the (temporary) `authroization_code` (not the `code_verifier`). The `authorization_code` is stored in the database temporarily, and returned to the user who can then trade the `authorization_code` **AND** `code_verifier` for an `access_token`.


## Gin/Angular/JWT
- https://betterprogramming.pub/how-to-create-a-simple-web-login-using-gin-for-golang-9ac46a5b0f89
- https://dev.to/nikola/jwt-authentication-in-an-angular-application-with-a-go-backend--13cg
- https://developer.okta.com/blog/2021/02/17/building-and-securing-a-go-and-gin-web-application
- https://codewithmukesh.com/blog/jwt-authentication-in-golang/
- https://github.com/golang-jwt/jwt



```mermaid
sequenceDiagram
    participant User
    participant Fasten App
    participant Lighthouse
    participant Medical Record Source
	

    User->>Fasten App: 1. Click login link.

	Fasten App->>Lighthouse: 2. Request Source configuration information

    loop challenge
    Fasten App->Fasten App: 3. Generate code verifier and code challenge.
    end
    
    Fasten App->>Medical Record Source: 4. Authorization code request and code challenge to authorize.
    Medical Record Source->>User: 5. Redirect to login/authorization prompt.

	loop wait-for-code
    Fasten App->Lighthouse: 6. Check if authorization code available
    end

    User->>Medical Record Source: 7. Authenticate and consent
    Medical Record Source->>Lighthouse: 8. Authorization code stored.
    Fasten App->>Medical Record Source: 9. Authorization code and code verifier sent for OAuth token.
    
    loop validate
    Medical Record Source->Medical Record Source: 10. Validate code verifier and challenge.
    end
    
    Medical Record Source->>User: 11. ID token, access token and, optionally, refresh token
    User->>Fasten App: 12. Store access token and request patient medical records.
    Fasten App->>Medical Record Source: 13. Electronic medical records retrieved
    Fasten App->>User: 14. Response.

```
