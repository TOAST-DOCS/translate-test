# Console Guide
**Management > Private CA > Console Guide**

The Private CA console is organized around certificate authorities (CAs), and all resources (certificate templates, issuers, certificates, ACME tokens) belong to a specific store. The console screen has a tab structure with a list of stores on the left and detailed information of the selected store on the right.

## Private CA Usage Flow

The process for issuing certificates in Private CA is as follows:

1. **Create Store**: Create a space to manage certificates.
2. **Create Issuer**: Create a certificate authority (CA) to sign certificates.
    - Root CA: Top-level certificate authority
    - Intermediate CA: Intermediate certificate authority under the Root CA
3. **Create Certificate Template**: Used when issuing multiple certificates with the same settings.
4. **Issue Certificate**: Issue certificates for actual use through certificate templates.

!!! tip "Note"
    - **CA (certificate authority)**: The entity that issues and signs certificates.
    - **Root CA**: A self-signed top-level certificate. It is the starting point of all trust.
    - **Intermediate CA**: An intermediate certificate signed by the Root CA. Used for issuing actual server certificates.

![Private CA Console Screen](https://static.toastoven.net/prod2_translate-test/en/privateca.png)

## Additional Images

![Pre-existing Image (Not included in PR)](../images/preexisting.png)

![External Screenshot (Not included in PR)](http://static.toastoven.net/prod_ai_easymaker/console-guide_appendix_hyperparameter_ko.png)