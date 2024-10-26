# Security aspects in distributed systems

This chapter introduces security protocols and techniques used in distributed systems.

We dive into three parts of security

1. **Authentication**
   * SAML-based SSO (Single Sign On)
   * User Tokens
   * OAuth (Authorization abused for authentication!)
2. **Authorization**
   * Access Control Lists
   * Rule Engines
   * Secret Keys
3. **Attack Vectors**
   * Hackers
   * Developers
   * Malicious Code

Things we **do not** discuss here are

1. DRM Solutions
2. Verification methods
3. Rate Limiting

# **Authentication**

## 1. Token Based Auth

This is the most basic form of authentication. The user sends their username and password to the server, which checks if they match in its database. If successful, the server generates a token, which is a piece of text signed by the server. The token contains information about the user's permissions. The user can then use this token for future requests without sending their password again. Tokens are simple but not extremely secure.

The token represents the user's authorization and specifies the actions they are allowed to perform. The user can present this token to the server as proof of authentication and authorization without needing to provide their password again. The server can verify the token by using its private key to decrypt the signed text and confirm its authenticity.

The private key is a secret number known only to the server, while the public key is shared with others. The public key can be used to decrypt the signed text and retrieve the authorization details. The token, being a signed piece of text, prevents unauthorized modifications.

However, the token-based authentication method has some limitations. It does not protect against replay attacks or token theft. If someone intercepts the token, they can potentially use it to impersonate the user and perform actions on their behalf. Additionally, if the token is stored in an insecure location, it can be accessed by unauthorized individuals.

Despite these limitations, token-based authentication is widely used due to its simplicity and efficiency. The permissions associated with the token can be quickly checked, and logging out invalidates the token. By including a version number or timestamp in the token, its validity can be controlled, and logging out will render it unusable.

Overall, token-based authentication offers a practical solution for balancing security and convenience in many authentication scenarios.


## 2. Single Sign-On (SSO) Based Auth

In SSO, the authentication process is delegated to an external service, such as Google or Uber. The user's credentials are checked by the external service, which then sends a token to the server. The server can decrypt the token and verify the user's permissions. SSO is useful for companies that want to have control over their users within their system, even if external services handle authentication.


## 3. OAuth Based Auth

OAuth is primarily an authorization system but is commonly used for authentication as well. It involves integrating external services, such as Google or GitHub, with a server. The user is prompted to give permissions to the server, allowing it to access certain information from the external service, such as the user's name or profile photo. OAuth tokens are generated, and the server can use them for authentication purposes. OAuth is widely used for authentication, even though it is originally designed for authorization.


# Authorization

## Access Control Lists and Rule Engines

ACLs are lists that define the actions that can be performed on objects. They can be 

1. user-based (a specific user has certain permissions),
2. role-based (users with a particular role have certain permissions),
3. group-based (a group of users or resources have certain permissions).

ACLs are grouped together to form the access control matrix of the system.

## Rule Engines:

Rule engines involve using a set of rules, often implemented as if statements, to determine whether a user or resource has permission to perform an action. Rule engines are useful for handling complex authorization requirements and can handle multiple objects and rules efficiently. They are also helpful in centralizing common rules and allowing easy rule modifications without modifying ACLs.


## Secret Keys:

Secret keys or client keys are an additional layer of security for authentication and authorization. They involve authenticating using a key or token rather than a username and password. This mechanism provides an extra level of security but is not considered ideal on its own.

----------------

These authorization mechanisms differ in their approach and can be used depending on the specific requirements of the system. They help define and enforce permissions for users and resources, ensuring that only authorized actions are performed.


# **Attack Vectors**

The video discusses different types of attackers and how to protect resources from them:

1. Hackers: Hackers often launch Distributed Denial of Service (DDoS) attacks to flood the system with requests. To mitigate this, techniques like distributed rate limiting and web application firewalls can be used to verify the authenticity of users and prevent flooding.
2. Employees: Employees, either willingly or unwillingly, can pose a threat to the system. Access control lists are useful in preventing unauthorized actions by employees. Restricting resource access and minimizing attack surfaces, such as opening only necessary entry points and allowing database access only to relevant servers, helps reduce the scope of attack.
3. Malicious Code: It is challenging to completely prevent the execution of malicious code. However, access to resources should be restricted, and rules in a rule engine can be used to prevent illegal modifications of code. Integrity checks and thorough code reviews can also help in identifying potential vulnerabilities.

Additionally, the video briefly mentions the importance of virtual private networks (VPNs) or virtual private clouds for secure remote access and end-to-end encryption while communicating with the system. Taking regular backups of the database is recommended as a preventive measure against the impact of malicious code.


# How videos are protected inside CDNs


In the video by Gaurav Sen, he discusses a design pattern for protecting videos on a CDN (Content Delivery Network) server from unauthorized access. He presents three approaches: token-based authentication, domain-based authentication, and server-side authentication.

1. Token-based authentication: The CDN server sends each user request to the main server to authenticate whether the user can view the video. If authorized, the CDN serves the video. This method provides strong authentication but is slower and less secure since the CDN can access and misuse the user's token.
2. Domain-based authentication: The CDN server restricts video access based on the domain from which the request originates. If the request comes from an allowed domain, the CDN serves the video; otherwise, access is denied. This approach is simple and fast but vulnerable to domain spoofing and lacks user-specific authorization.
3. Server-side authentication: The user's request directly communicates with the server for authentication. The server generates a token signed by the user's private key, indicating permission to access the video. This token is then forwarded to the CDN, which verifies its authenticity using the public key and grants access accordingly. The token can have a refresh interval to mitigate unauthorized sharing. This method offers a mix of security and efficiency.

Gaurav Sen also mentions that for enhanced security, digital rights management (DRM) solutions can be used to prevent unauthorized copying or multiple IP addresses accessing the content. Additionally, access control lists and rule engines can provide resilience against attacks. The video concludes by emphasizing the importance of authentication, authorization, and security mechanisms tailored to the system's specific needs.
