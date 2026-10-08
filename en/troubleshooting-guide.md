<!-- pre-align:aligned sig=aa4052351c5f -->

<a id="management-certificate-manager-troubleshooting-guide"></a>
## Management > Certificate Manager > Troubleshooting Guide { #management-certificate-manager-troubleshooting-guide }

<a id="converting-certificate-file-formats"></a>
## Converting Certificate File Formats { #converting-certificate-file-formats }

Certificate Manager currently supports only the pem-format certificate files.

  * More formats are to be supported in the near future.

Following are the available certificate file formats for Certificate Manager.

<a id="format-of-certificate-file-pem"></a>
### Format of Certificate File (.pem) { #format-of-certificate-file-pem }

The filename extension is **.pem**.

Each file includes certificate (chain) information and private key information.

``` text
-----BEGIN CERTIFICATE-----
...
-----END CERTIFICATE-----
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
```

<a id="how-to-create-pem-files"></a>
### How to Create PEM Files { #how-to-create-pem-files }

You can create pem files like follows:
1. Convert certificate information into pem.
2. Create a single pem file which includes certificate chain and a private key.

<a id="how-to-create-pem-files-convert-certificate-information-into-pem"></a>
#### Convert Certificate Information into PEM

1. In case of a Java JKS or JCEKS certificate, use `keytool` to convert certificate into the `.p12` or `.pks` format.
2. For the `.p12` or  `.pks` type, execute the command as follows and convert it into  `.pem` .

```sh
openssl pkcs12 -in my_certificate_input_file.pfx -nokeys -out my_cert_converting_result_file.pem
openssl pkcs12 -in my_certificate_input_file.pfx -nodes -nocerts -out my_cert_converting_result_file.pem
```

* See the link below for the **openssl** command which is applied to convert certificate formats.
    * openssl command guide : [https://www.openssl.org/docs/manmaster/man1/openssl.html](https://www.openssl.org/docs/manmaster/man1/openssl.html)
* See the link as below on how to use keytool.
    * java-1.6.0 keytool : [https://linux.die.net/man/1/keytool-java-1.6.0-openjdk](https://linux.die.net/man/1/keytool-java-1.6.0-openjdk)
    * java-1.7.0 keytool : [https://linux.die.net/man/1/keytool-java-1.7.0-openjdk](https://linux.die.net/man/1/keytool-java-1.7.0-openjdk)

<a id="how-to-create-pem-files-optional-convert-into-rsa-private-key-type"></a>
#### (Optional) Convert into RSA Private Key Type

If a private key is not in the RSA format, encode it into an RSA private key format.

* When a private key file is open and if it starts with **-----BEGIN PRIVATE KEY-----**, it is not an RSA private key file.

To convert a private key into an RSA private key, execute the following command:

``` bash
openssl rsa -in my_key_not_rsa_input_file.pem -check -out my_key_rsa_converting_result_file.pem

> writing RSA key
> Enter PEM pass phrase: (enter passphrase encoded with RSA private key)
> Verifying - Enter PEM pass phrase:
```

<a id="how-to-create-pem-files-create-single-pem-files-including-certificate-chain-and-private-key"></a>
#### Create Single PEM Files including Certificate Chain and Private Key

Combine PEM file information of certificate and private key, to create a single PEM file.

``` bash
cat my_cert_converting_result_file.pem my_key_rsa_converting_result_file.pem > final_result_pem_file.pem
```
The format of a newly-made PEM file (which is "final\_result\_pem\_file.pem" in the above example) is like below.

``` text
-----BEGIN CERTIFICATE-----
.... (your primary SSL certificate)
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
.... (the intermediate CA certificate)
.... (unavailable if certificate chain information does not exist.)
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
.... (the trusted root certificate)
.... (unavailable if certificate chain information does not exist.)
-----END CERTIFICATE-----
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
```
