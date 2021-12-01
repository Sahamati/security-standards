# Layered Security

Layered security is an approach that uses several components to protect the API operations with multiple levels of security measure. The purpose of a layered security approach is to make sure that every individual defense component has a backup to counter any flaws or gaps in the security. AA ecosystem APIs follow various security measures corresponding to the security layer as follows:

![](<.gitbook/assets/image (2).png>)

|                   |                                                                                                                                                  |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Layer             | **Security Goals**                                                                                                                               |
| Business Layer    | <ul><li>Regulatory control</li><li>AA Data blind</li><li>Consent Artefact</li><li>Forward Secrecy</li><li>Anonymity</li><li>Revocation</li></ul> |
| Application Layer | <ul><li>Authentication</li><li>Integrity</li><li>Non-repudiation</li></ul>                                                                       |
| Protocol Layer    | <ul><li>Privacy</li><li>Identity authentication</li><li>Reliability</li></ul>                                                                    |

## Business layer

The Business layer leverages the security mechanism that facilitates the AA does not maintain any financial information about the customer itself; it only acts as a “pass-through” of information and ensures that no information passes through it without the customer’s consent. The business layer achieves the following security goals:

* AA Data Blind: To prevent the unauthorized access of FI, the FIP perform end-to-end encryption on the financial information (FI) in such a way that only FIU can decrypt the FI. The encrypted FI only passes through AA to FIU. This process enables AA data blind.
* Consent Artefact: A consent artefact is a machine-readable electronic document that specifies the parameters and scope of data sharing that a Customer consents to in any data sharing transaction. It is a data access control defined by the customer to manage the access of FI.
* Forward Secrecy: NBFC-AA ecosystem should protect guards against future compromises of past sessions, which could cause the loss of sensitive data such as passwords or additional secret keys. This means that even if any of the key materials stored at FIPs, FIUs (either long-term private keys or session keys) are compromised at a given point in time, data that was exchanged in the past (i.e., before that point in time) would not be possible to decipher. This is a strong guarantee of secrecy which is necessary to ensure for financial data.
* Anonymity: The AA should enable that FIP is not aware of the identity of FIU.
* Revocation: The user can dismiss the authorization on financial information by consent revocation through AA.

### AA Data Blind and Transient Storage

#### **AA Data Blind: FI type encryption using E2EE**

End-to-end encryption (E2EE) is a method of securing the communication by preventing any intermediate node from accessing data while it's transferred from one end system or device to another. In AA ecosystem, the financial information is encrypted in a such a way that the only authorized FIU can decrypt the data and provide a value-added service to the customer. In this process, AA cannot decrypt the data and it can only pass through the encrypted FI to the FIU by offering a transient storage for storing the encrypted FI in a defined period and also notifying the availability of FI to the FIU.

**Note:** To implement the E2EE for AA ecosystem, please refer Annexure A for the cryptographic primitives that can be used to implement it.

### Consent Artefact: Creation, Management, and Validation

Consent is a digitally signed artefact collected by AA through interaction with a User (account holder) for the purpose of using it for requesting financial information from a FIP. In this process, the customer defines the consent as per the defined structure of consent artifact in Figure 1(as per the Section 6 and Section 7 of Master Direction[\[8\]](layered-security.md)). The generated consent is only valid for linked accounts with a recorded purpose of usages. AA acts as consent collector who given an interface to the customer for queried, paused, and revoked the consent. Before a Customer or FIU can obtain financial information, the AA has to collect consent from the Customer. Then, the AA creates two different sets of Consent Artefacts. One of the Consent Artefact represents a contract between the FIU and the AA. This Consent Artefact is utilized in the data flow requests between FIU and AA. The other set of Consent Artefacts (one or more for each FIP) authorizes the AA to obtain information from FIPs for FI data aggregation.

It is responsibility of AA to maintain the mapping between FIU Consent artefact and its corresponding FIP consent artefact(s). The illustrative process of consent mapping by the AA as a mediator between FIU and FIP as depicted in Figure 2. FIP maintains the most recent status of Consent and verifies it before servicing FI requests. The complete journey of customer starting from the registration, then account discovery and linking, initiation of consent with the approval of linked account, and finally FIP shared FI with FIU via AA is shown in Figure 3.

![Figure 1: Consent artefact structure](<.gitbook/assets/6 (1).png>)

![Figure 2: Consent mapping process between FIU-AA and AA-FIP](<.gitbook/assets/7 (1).png>)

|                                                                                                                               |
| ----------------------------------------------------------------------------------------------------------------------------- |
| **Customer Onboarding Journey**                                                                                               |
| <p>Account Creation at AA</p><p>Customer wants to avail services from FIU</p><p>Redirection</p><p>Account creation at FIU</p> |

|                                                                                                                                                                                                                                                                                                                                     |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Customer Consent Authorization Journey**                                                                                                                                                                                                                                                                                          |
| <p>FIU requires <strong>Consents</strong> from Customer for providing services, FIU redirects Customer to AA</p><p>Customer Discovers and Link Accounts at AA</p><p>FIP stores a copy of <strong>Consent</strong> for later validation</p><p>Customer generates <strong>Consents</strong> at AA for one or more linked accounts</p> |

|                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Customer FI Service Journey**                                                                                                                                                                                                                                                                                                                                                            |
| <p>AA aggregates the <strong>FI data</strong> from FIPs and delivers to FIU</p><p>FIU uses <strong>Consent</strong> and requests <strong>FI data</strong> from AA</p><p>AA sends <strong>FI Data</strong> requests to one or more FIPs using mapped <strong>Consents</strong></p><p>FIP validates the <strong>Consent</strong>, generates the <strong>FI Data</strong> as per the rule</p> |

Table 3: Consent journey mapping of FI flow in AA ecosystem\
TODO: add table/figure 3 flow images

## Application layer

Application layer imposes the security to provide the authentication, integrity, and non-repudiation by generating the JSON Web Signature (JWS) on payload/end point URL. The application layer achieves the following security goals:

* Authentication: Authentication is the mechanism of associating an incoming request with a set of identifying credentials, such as the user the request came from, or the token that it was signed with. The permission and throttling policies can then use those credentials to determine if the request should be permitted.
* Integrity: Assurance that the data has not been modified by unauthorized parties
* Non-repudiation: The participating entities in NBFC-AA ecosystem cannot deny their actions after performing the operations.

### JSON Web Signature (JWS) for Payload/End Point URL

JWS represents content secured with digital signature or Message Authentication Codes (MACs) in order to provide integrity protection for the information of API request and response. In AA ecosystem, Json Web Signature (JWS) method is used to sign the content, as described in Appendix F of RFC7515[\[9\]](layered-security.md). This method is called 'Detached Content' signature method. In this method, the generated JWS signature does not contain the content part. Only the header and signature are returned.

**Note:** The detailed process of generating the JSON Web Signature and the preferred cryptographic algorithms are mentioned in Annex B.

**Note:** Please refer the introduction section of FAQ in NBFC-AA API website[\[10\]](layered-security.md) for the detailed process of generating the JWS signature for request and response of the API.

**JSON Web signature for URI Parameters**

The URI parameters of GET APIs are also signed using JWS so that receiver can validate that URI parameters are not altered during communication and to verify the identity of requester before processing the request.

For example: Detached JWS of the endpoint URI “/FI/fetch/{sessionId}” with {sessionId} substituted with value before generating the JWS.

**Risk and mitigation**

JSON Web Tokens, also known as JWTs, are URL-safe JSON-based security tokens that contain a set of claims that can be signed and/or encrypted. To implement the JWS process based on JWT, the Best Current Practices document[\[11\]](layered-security.md) provides actionable guidance to secure implementation and deployment of JWTs.

### API Key

API Keys should be used as the first line of defence against unauthorized API calls. API keys need to be set up before FIUs or FIPs can start making API requests to AAs. AA ecosystem uses API keys for authorization. An API key is a token that a FIU provides when making API calls of AA and AA provides when making API calls of FIP. The key can be sent in the request header. For example: the request header for a FIU to call AA API is Client\_api\_key (apiKey), for an AA to call FIU is AA\_api\_key (apiKey), for a FIP to call AA is FIP\_api\_key (apiKey), and an AA to call FIP is AA\_api\_key (apiKey).

**Note:** Please refer the Section “6.2.1 Authentication Techniques” of Handbook on Application Programming Interfaces (APIs)[\[12\]](layered-security.md) to follow the security guidelines for implementing the API Authentication.

### IP Whitelisting

The communication between FIU-AA and AA-FIP should be allowed through IP whitelisting. The IP whitelisting can be done at network firewall level of respective AA, FIP, FIU domain. The APIs exposed by AAs/FIPs/FIUs will be allowed to call only through the whitelisted IP addresses or IP range. This provides an extra layer of security against unauthorized API calls in AA ecosystem.

## Protocol Layer

The protocol layer security protects the data in transit. This protection is achieved by encrypting the data before transmission; authenticating the endpoints; and decrypting and verifying the data on arrival. The protocol layer achieves the following security goals:

* Privacy: Connection through encryption.
* Identity authentication: Identification through mutual certificates.
* Reliability: Dependable maintenance of a secure connection through message integrity checking.

### Payload Encryption by TLSv1.2

The primary benefit of transport layer security is the protection of web application data from unauthorized disclosure and modification when it is transmitted between client-server and server-server. TLS also provides two additional benefits that are commonly overlooked; **integrity guarantee** and **replay prevention**. A TLS stream of communication contains built-in controls to prevent tampering with any portion of the encrypted data. In addition, controls are also built-in to prevent a captured stream of TLS data from being replayed at a later time. It should be noted that TLS provides the above guarantee to data during transmission.

**Note:** To implement secure TLSv1.2 in AA ecosystem, the client and server only allowed recommended description of cipher suite and follow the implementation recommendation given by OWSAP.

**Note:** The detailed process of performing payload encryption using TLSv1.2 is mentioned in Annex C.
