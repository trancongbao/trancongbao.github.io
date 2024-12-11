# SAML
## After successful response
Redirect Response

# Traditonal Session Cookie (Stateless)
# JWT (Stateful)
## JWT stored in the Location url in Redirect Response.
Including the JWT directly in the Location header of the HTTP redirect response after successful authentication.

### Example: Passing JWT in Redirect URL
When the SAML authentication flow completes successfully, the Service Provider (SP) would issue a `302` redirect response with a `Location` header like this:
```
HTTP/1.1 302 Found
Location: https://client.example.com/dashboard?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwi...
```
This URL includes the JWT (token query parameter) so that when the user's browser follows the redirect, the JWT is appended as a parameter in the URL.

### Security Implications of Passing JWT in the Redirect URL
Although this approach might seem convenient, it has some significant security concerns:

#### Token Exposure in Browser History:

When the JWT is included in the URL, it gets stored in the browser's history. If an attacker gains access to the user's device, they could potentially extract the JWT from the browser history.

### Referrer Leakage:

If the user clicks on a link to another domain from the redirected page, the JWT might be leaked as part of the Referer header. Some sites could log or capture this information, making it accessible to third parties.
Insecure Storage in Bookmark or Logs:

If users bookmark the URL or if your application logs incoming URLs, the JWT could be inadvertently stored in a place where it’s exposed to others.
Cross-Site Scripting (XSS):

If the JWT is passed as a query parameter, it’s more accessible to JavaScript running on the client-side, increasing the risk that a malicious script (via an XSS attack) could read and extract the token.
## Auth Code (short-lived) stored in cookies

# JWT in Cookie (Stateless)
