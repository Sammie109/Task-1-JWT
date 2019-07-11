# Task-1-JWT
JSON Web Token
---
**JSON Web token** is a secure and safe way of data (claims) transmitting between two parties. It is performed using the JSON ***object***. Technically it is a non-encrypted string with three parts, separated by dots.
JWT acts effectively as a temporary user credential that replaces the permanent credential which is the username and password combination.
JSON itself is a simple data transmitting format, convenient for reading and writing by both human and computer.

JSON is based on two main data structures:
1) Key:value structure (realized in a form of an ***object***); 
2) An ordered list of values (realized in a form of an array)

***Object*** is the set of key:value pairs (e.g. "alg": "HS256", where "alg" is a key and "HS256" is the value).
***
JWT consists of 3 parts: header, payload and signature
***
 ### Header 
 contains information on how to calculate JWT signature (type of the algorithm such as SHA 256 or RSA) and type of the token which is JWT. It is encoded by Base 64 algorithm to be transmitted. Header describes what algorithm (signing JWS or encryption JWE) is used to process the data contained in the JWT. A signature allows a JWT to be validated against modifications. Encryption, on the other hand, makes sure the content of the JWT is only readable by certain parties.

```Example: {"alg": "HS256", "typ": "JWT"}' ```
***
 ### Payload 
contains the information that should be transmitted and is stored inside the JWT. Usually it contains claims (statements) about the user. Payload is also formed using the key:value structure and you can put as many claims into payload as you need. 

There are three types of claims: 

1) Reserved (predefined recommended interoperable claims like iss (issuer), exp (expiration time), sub (subject); 
2) Public (Custom claims for public consumption which can be defined at a will by those who use JWT. Usually it is name or email);
3) Private (Custom claims created to share information specific to your application and between parties that agree on using them). 

Attention should be paid to the name of any custom claim: 1) You can use any name which is not listed in the IANA JSON Web Token Claims Registry; 2) To avoid collision, private claims should not have same names with reserved or public claims.

*Payload should not contain any restricted information because it is not encrypted, it is only encoded by Base 64 algorithm, so anyone can decode it.*

```Example: {"userId": "b08f86af-35da-48f2-8fab-cef3904660bd", "username": "Paul"} ```
***
 ### Signature 
is used to verify the sender of JWT and to ensure that no information has been deleted or added into JWT. It contains MAC (Message authentication code). Above mentioned Base 64 algorithm encodes header and payload, then they are separated by a dot `[base64urlEncode(header) + '.' + base64urlEncode(payload]`, then this part is hashed by a secret key using the algorithm specified in the header (e.g. "alg": "HS256"). This part can also be encoded by Base 64 algorithm.
  ***
  Now, when all parts are ready, they just need to be concatenated by separating them with a dot.
  
![JWT](https://user-images.githubusercontent.com/52605746/61045134-e6b3f300-a3e2-11e9-887e-dd3c3cc14f3e.jpg)

***Basic look of JWT***
```
{ alg: "HS256", typ: "JWT" }.

{ aud: "myservice.com", 

userName: "John Smith", 

userRole: "Admin" }.

wmhbD8_QA_w54HSPCwcdCBf4weh6yhZ1u_PwHlYHr9Y
```

***Base 64 encoded look of JWT***  
                 
                    eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJhdXRoLm15c2VydmljZS5jb20iLCJhdWQiOiJteXNlcnZpY2UuY29tIiwidXNlck5hbWUiOiJKb2huIFNtaXRoIiwidXNlclJvbGUiOiJBZG1pbiJ9.4rmwo6lIy7SPvRs1tOTqFYEtdRTCG1M_LAEZi13985Y
  
  
  
  
  
   In this way user obtains an access token which has an expiration time (e.g. 30 min) and after 30 min expire user has to re-authenticate. The main disadvantage of this approach is that in the case of a short expiration period, the user will often have to enter a login and password (which is inconvenient and insecure). In order to solve the described problems, it is often proposed, along with a short-term access token, to additionally use a second long-playing refresh token (e.g. with the 1 year expiration period).
