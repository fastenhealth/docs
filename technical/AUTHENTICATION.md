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



# Self-Hosted Redirect Based flow
This is a potential future authentication flow, primarily to make sure that mobile apps are able to work correctly. 


```mermaid
sequenceDiagram
    participant User
    participant Browser
    participant Fasten Server
    participant Fasten SPA
    participant Lighthouse
    participant Healthcare Provider
	

    User->>Browser: 1. Request Fasten App
    Browser->>Fasten Server: 2. Request Fasten App
    Fasten Server->>Browser: 3. Respond with Fasten SPA

	User->>Fasten SPA: 4. Click "Connect Healthcare Provider"
	Fasten SPA->>Browser: 5. Generate & Store State, Code Challenge & Validator 
	Browser->>Lighthouse: 6. Redirect to Lighthouse. 
	Lighthouse->>Browser: 7. Store Referrer URL (Fasten Server) in session storage. 
	Browser->>Healthcare Provider: 8. Redirect to Healthcare Provider & Login prompt 
	User->>Browser: 9. Enter Healthcare provider credentials & complete auth flow.
	Browser->>Lighthouse: 10. Redirect to Lighthouse service (callback url). Store Authorization Code in DB. Display "Connection Complete" URL, which reads Referrer URL from session storage.
	Browser->>Fasten SPA: 11. Redirect to Fasten SPA (from Cache)
	Fasten SPA->>Lighthouse: 12. Request Authorization Code via State parameter
	Lighthouse->>Fasten SPA: 13. Respond with Authorization Code
	Fasten SPA->>Healthcare Provider: 14. Request OAuth tokens using authorization code, code verifier & challenge
	Healthcare Provider->>Fasten SPA: 15 Validate code verifier & challenge, respond with id, access and refresh tokens. 
    Fasten SPA->>Fasten Server: 16. Store id, access & refresh token in database
    
    loop Async (Daily) Request Patient Data
    Fasten Server->>Healthcare Provider: 17. Update access token using refresh token, request Electonic medical records for patient.
    Healthcare Provider->>Fasten Server: 18. Store records in database. 
    end

```


# Cloud Redirect Based flow
This is a potential future authentication flow, primarily to ensure that patient data can be cloud accessible, with client-side encryption (Server cannot decrypt)


```mermaid
sequenceDiagram
	participant Hello IdP
    participant User
    participant Browser
    participant Fasten Cloud Server
    participant Fasten Storage
    participant Fasten SPA
    participant Lighthouse
    participant Healthcare Provider
	

    User->>Browser: 1. Request Fasten App
    Browser->>Fasten Cloud Server: 2. Request Fasten App
    Fasten Cloud Server->>Browser: 3. Respond with Fasten SPA
	User->>Fasten SPA: 4. Click "Login with Hello"
	Browser->>Hello IdP: 5. Redirect to Hello service
	User->>Hello IdP: 6. User authenticates
	Browser->>Fasten SPA: 7. Redirect to Fasten SPA (from Cache) with auth metadata & ID token.
	Fasten SPA->>Browser: 8. Store ID token in browser session/cookie
	
	User->>Fasten SPA: 9. Click "Connect Healthcare Provider"
	Fasten SPA->>Browser: 10. Generate & Store State, Code Challenge & Validator 
	Browser->>Lighthouse: 11. Redirect to Lighthouse. 
	Lighthouse->>Browser: 12. Store Referrer URL (Fasten Cloud Server) in session storage. 
	Browser->>Healthcare Provider: 13. Redirect to Healthcare Provider & Login prompt 
	User->>Browser: 14. Enter Healthcare provider credentials & complete auth flow.
	Browser->>Lighthouse: 15. Redirect to Lighthouse service (callback url). Store Authorization Code in DB. Display "Connection Complete" URL, which reads Referrer URL from session storage.
	Browser->>Fasten SPA: 16. Redirect to Fasten SPA (from Cache)
	Fasten SPA->>Lighthouse: 17. Request Authorization Code via State parameter
	Lighthouse->>Fasten SPA: 18. Respond with Authorization Code
	Fasten SPA->>Healthcare Provider: 19. Request OAuth tokens using authorization code, code verifier & challenge
	Healthcare Provider->>Fasten SPA: 20 Validate code verifier & challenge, respond with id, access and refresh tokens. 
    Fasten SPA->>Fasten Cloud Server: 21. SPA Encrypts the access & refresh token with Hello ID token, then transmits both with hashed ID token.
    Fasten Cloud Server->>Fasten Storage: 22. Fasten Cloud Server encrypts data (again) with hashed Hello ID + salt, then stores in Storage.
    
    loop Client-Side Encryption & Submit Medical Records
	Fasten SPA->>Healthcare Provider: 23. Update access token using refresh token, request Electonic medical records for patient.
	Fasten SPA->>Fasten Cloud Server: 24. SPA Encrypts the EMR records with Hello ID token, then transmits records with hashed ID token.
    Fasten Cloud Server->>Fasten Storage: 25. Fasten Cloud Server encrypts data (again) with hashed Hello ID + salt, then stores in Storage
    end

```
