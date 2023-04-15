In cryptography and computer security, self-signed certificates are public key certificates that are not issued by a certificate authority (CA). 
These self-signed certificates are easy to make and do not cost money. However, they do not provide any trust value.

For instance, if a website owner uses a self-signed certificate to provide HTTPS services, people who visit that website cannot be certain that they are connected to their intended destination.
For all they know, a malicious third-party could be redirecting the connection using another self-signed certificate bearing the same holder name. 
The connection is still encrypted, but does not necessarily lead to its intended target.
In comparison, a certificate signed by a trusted CA prevents this attack because the user's web browser separately validates the certificate against the issuing CA. 
The attacker's certificate fails this validation.

Self-signed certificates, however, have their own limited uses. 
They have full trust value when the issuer and the sole user are the same entity.
For example, the Encrypting File System on Microsoft Windows issues a self-signed certificate on behalf of the encrypting user and uses it to transparently decrypt data on the fly. 
Another example is the root certificate, which is a form of self-signed certificate.

## Benefits

Self-signed certificates can be created for free, using a wide variety of tools including OpenSSL, Java's keytool, Adobe Reader, wolfSSL and Apple's Keychain. 
They are easy to customize; e.g, they can have larger key sizes or hold additional metadata. 
Their use doesn't involve the problems of trusting third parties that may improperly sign certificates. 
Self-signed certificate transactions usually present a far smaller attack surface by eliminating both the complex certificate chain validation, and CA revocation checks like CRL and OCSP.

## Trust issues

In a CA-based PKI system, parties engaged in secure communication must trust a CA, i.e. place the CA certificates in a whitelist of trusted certificates. 
Developers of web browsers may use procedures specified by the CA/Browser Forum to whitelist well-known, public certificate authorities. 
Individual groups and companies may whitelist additional, private CA certificates. 
The trust issues of an entity accepting a new self-signed certificate are similar to the issues of an entity trusting the addition of a new CA certificate. 
The parties in a self-signed PKI must establish trust with each other (using procedures outside the PKI), and confirm the accurate transfer of public keys e.g. compare the certificate's cryptographic hash out of band.

There are many subtle differences between CA signed and self-signed certificates, especially in the amount of trust that can be placed in the security assertions of the certificate. 
Some CAs can verify the identity of the person to whom they issue a certificate; for example the US military issues their Common Access Cards in person, with multiple forms of other ID. 
The CA can attest identity values like these by including them in the signed certificate. 
The entity that validates the certificate can trust the information in that certificate, to the same extent that they trust the CA that signed it (and by implication, the security procedures the CA used to verify the attested information).

With a self-signed certificate by contrast, trust of the values in the certificate are more complicated because the entity possesses the signing key, and can always generate a new certificate with different values. 
For example, the validity dates of a self-signed certificate might not be trusted because the entity could always create and sign a new certificate that contained a valid date range.

The values in a self-signed certificate can only be trusted when the values were verified out-of-band during the acceptance of the certificate, and there is a method to verify the self-signed certificate has not changed after it was trusted. 
For example, the procedure of trusting a self-signed certificate includes a manual verification of validity dates, and a hash of the certificate is incorporated into the white list.
When the certificate is presented for an entity to validate, they first verify the hash of the certificate matches the reference hash in the white-list, and if they match (indicating the self-signed certificate is the same as the one that was formally trusted) then the certificate's validity dates can be trusted. 
Special treatment of X.509 certificate fields for self-signed certificate can be found in RFC 3280.

Revocation of self-signed certificates differs from CA-signed certificates. 
By nature, no entity (CA or others) can revoke a self-signed certificate. 
But one could invalidate a self-signed CA by removing it from the trust whitelist.

## Uses
Self-signed certificates have limited uses, e.g. in the cases where the issuer and the sole user are the same entity. 
For example, the Encrypting File System on Microsoft Windows issues a self-signed certificate on behalf of a user account to transparently encrypt and decrypt files on the fly. 
Another example is root certificate, which is a form of self-signed certificate.

## See also
[Certificate authority § Implementation weakness of the trusted third party scheme](https://en.wikipedia.org/wiki/Certificate_authority#Implementation_weakness_of_the_trusted_third_party_scheme)
[X.509](https://en.wikipedia.org/wiki/X.509), the standard describing the most widely used format for storing certificates
[Let's Encrypt](https://en.wikipedia.org/wiki/Let%27s_Encrypt), a certificate authority which provides free [domain-validated certificates](https://en.wikipedia.org/wiki/Domain-validated_certificate)