# 15_JWT_Authentication – MCQs

## EASY MCQs

### Q1. What does JWT stand for?
A. Java Web Token
B. JSON Web Token
C. Javascript Web Text
D. Just Web Token

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
A standard for representing claims securely between two parties.
</details>

### Q2. Which attribute protects a controller, requiring the user to be logged in?
A. `[Protect]`
B. `[Authorize]`
C. `[Login]`
D. `[Secure]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The standard authorization attribute in ASP.NET Core.
</details>

### Q3. Where is the JWT typically sent in the HTTP request?
A. In the URL.
B. In the `Authorization` header, using the `Bearer` schema.
C. In a cookie only.
D. In the HTML body.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
`Authorization: Bearer <token>`
</details>

### Q4. What are the three parts of a JWT?
A. Header, Payload, Signature.
B. Start, Middle, End.
C. User, Pass, Role.
D. Key, Value, Pair.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Base64UrlEncoded segments separated by dots.
</details>

### Q5. If you want to allow anyone to access an action inside an `[Authorize]` controller, what attribute do you use?
A. `[Public]`
B. `[AllowAnonymous]`
C. `[Open]`
D. `[Free]`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Overrides the controller-level authorization requirement.
</details>

---

## MEDIUM MCQs

### Q6. The "Payload" part of JWT contains what?
A. The password.
B. Claims (User ID, Name, Role, Expiry).
C. The encryption algorithm.
D. The signature.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The actual data payload.
</details>

### Q7. Why is the "Signature" important?
A. It makes the token look pretty.
B. It allows the server to verify that the token has not been tampered with. If the client changes the payload, the signature won't match.
C. It encrypts the data so no one can read it.
D. It compresses the token.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
JWTs are typically signed, not encrypted. The data is readable (Base64), but trusted because of the signature.
</details>

### Q8. Which NuGet package is commonly used for JWT in ASP.NET Core?
A. `Microsoft.AspNetCore.Authentication.JwtBearer`
B. `System.IdentityModel`
C. `Newtonsoft.Json`
D. `EntityFramework`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Provides the middleware to parse and validate bearer tokens.
</details>

### Q9. In `Program.cs`, which order is correct?
A. `UseAuthorization` then `UseAuthentication`.
B. `UseAuthentication` then `UseAuthorization`.
C. Order doesn't matter.
D. Use neither.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
"Who are you?" (AuthN) must be answered before "Are you allowed here?" (AuthZ).
</details>

### Q10. What is a "Claim" in JWT context?
A. A complaint.
B. A key-value pair representing a fact about the user (e.g., `role: admin`, `sub: 123`).
C. A method.
D. A server.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
The unit of identity data.
</details>

---

## HARD MCQs

### Q11. Is the information in a JWT Payload encrypted (hidden)?
A. Yes, fully secret.
B. No, it is just Base64Url encoded. Anyone with the token can decode and read the payload. Do not store secrets (passwords) in JWTs.
C. Yes, by the private key.
D. Depends on browser.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Common misconception. Confidentiality is not inherent to standard JWTs (unless using JWE).
</details>

### Q12. How does the server validate the JWT without hitting the database?
A. It checks the signature using the Secret Key (stored on server). If Hash(Header + Payload + Secret) == Signature, the token is valid and trusted.
B. It calls Google.
C. It checks a CSV file.
D. It asks the Client.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
This is why JWT is "Stateless". No session store lookup needed.
</details>

### Q13. `[Authorize(Roles = "Admin")]` checks which claim?
A. `ClaimTypes.Name`
B. `ClaimTypes.Role` (or simply `role` in JSON).
C. `ClaimTypes.Id`
D. `ClaimTypes.Group`

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Maps to the IPrincipal.IsInRole check.
</details>

### Q14. What happens when a JWT expires (`exp` claim)?
A. The server refreshes it automatically.
B. The `JwtBearer` middleware rejects it with a 401 Unauthorized (`SecurityTokenExpiredException`).
C. It works for 5 more minutes.
D. The user is deleted.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** B
**Explanation:**
Time-bound security is strict.
</details>

### Q15. Symmetric vs Asymmetric signing. Which one uses a single shared secret key?
A. Symmetric (HMAC-SHA256).
B. Asymmetric (RSA).
C. Neither.
D. Both.

<details>
<summary><strong>Answer</strong></summary>
**Correct Answer:** A
**Explanation:**
Symmetric = Shared Secret (fast, simple). Asymmetric = Private/Public Key pair (good for distributed auth servers).
</details>
