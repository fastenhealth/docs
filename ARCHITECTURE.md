
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
    Fasten App->>Medical Record Source: 9. Authorization code and code verified to OAuth token.
    
    loop validate
    Medical Record Source->Medical Record Source: 10. Validate code verifier and challenge.
    end
    
    Medical Record Source->>User: 11. ID token and access token.
    User->>Fasten App: 12. Store access token and request patient medical records.
    Fasten App->>Medical Record Source: 13. Electronic medical records retrieved
    Fasten App->>User: 14. Response.

```

> The PKCE authorization code flow adds a secret (a `code_verifier` generated using SHA-256) created by the client application that is verified by the authorization server. The client application creates a transform value (hash string) of the `code_verifier` called the `code_challenge` which is sent using HTTPS to retrieve an authorization code. A malicious attacker can intercept this code, but cannot exchange it for a token without the `code_verifier`.
> 
> https://andrewowen.net/blog/creating-diagrams-with-mermaid/

The Fasten Lighthouse acts like a man-in-the-middle, however it only temporarily stores the code 