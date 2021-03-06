# JWT
JSON Web Tokens

### 1.	Overview

An abstract definition tells that a JSON Web Token (JWT) is a JSON object that is defined in RFC 7519 (open standard) as a safe way to represent a set of information between two parties.
There is no need to contact a third-party service or keep JWTs in-memory between requests to confirm that the claim they carry is valid - this is because they carry a Message Authentication Code (MAC).
Here is an example of encoded JSON Web Token:
`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ`

### 2.	The Structure

A JWT consists of the following three parts: the header, the payload, and the signature.
Simply, a JWT is a string consisting of three components, each component delimited by a “.” (period) character.
The overall scheme is the following: header.payload.signature

<b>a.	Header:</b> Algorithm & Token Type. A JSON (Base64 encoded) that has information about algorithm used (like HS256, RSA) and so on.
  
<b>b.	Payload:</b> Data. A JSON (Base64 encoded) that has information about the user.

<b>c.	Signature:</b> A string that was generated using #a + #b + secret key (a secret that only the server knows), using the algorithm mentioned in #a.

<b>JWT Header:</b>
`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`

<b>JWT Payload:</b>
`eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9`

<b>JWT Signature:</b>
`TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ`

If the signature is valid and can be verified using the secret key, we can simply decode the payload and get the user information without going to database.
There is an example below that shows the JWT token used in both encoded and decoded manners.

![alt-Example](https://res.cloudinary.com/dyyck73ly/image/upload/v1458077225/shoskufayqrg0ffwqqau.jpg "Example")

### 3.	General scheme of work

<b>Access-token</b> contains the security credentials for a login session and identifies the user, the user's groups, the user's privileges, and, in some cases, a particular application.

<b>Refresh-token</b> allows customers to request new access-tokens after their lifetime. These tokens are usually issued for a long time.

![alt-Scheme example](https://github.com/AntonOrel/jwt/blob/master/JWT.jpg "Scheme example")

Usually the following scheme is implemented when using JSON tokens in client-server applications:
1.	The client is authenticated in the application (for example, using a login and password).
2.	In case of successful authentication, the server sends access- and refresh-tokens to the client.
3.	Upon further access to the server, the client uses the access-token. The server checks the token for validity and gives an access to resources for the client.
4.	If the access token is not valid, the client sends a refresh-token. The server provides two updated tokens.
5.	The client must go through the authentication process again in case the refresh-token becomes not valid.
