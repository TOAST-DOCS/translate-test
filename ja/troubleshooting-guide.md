<!-- pre-align:aligned sig=aa4052351c5f -->

<a id="management-certificate-manager-troubleshooting-guide"></a>
## Management > Certificate Manager > 問題解決ガイド { #management-certificate-manager-troubleshooting-guide }

<a id="converting-certificate-file-formats"></a>
## 証明書ファイルの形式変換 { #converting-certificate-file-formats }

Certificate Managerでは.pem形式の証明書ファイルのみサポートします。

* 今後、サポートする証明書形式を追加する予定です。

Certificate Managerで使用する証明書ファイルの形式は下記の通りです。

<a id="format-of-certificate-file-pem"></a>
### 証明書ファイル(.pem)形式 { #format-of-certificate-file-pem }

証明書ファイルの拡張子は**.pem**です。

ファイルには証明書(チェーン)情報と秘密鍵情報が含まれています。

``` text
-----BEGIN CERTIFICATE-----
...
-----END CERTIFICATE-----
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
```

<a id="how-to-create-pem-files"></a>
### 証明書ファイル(.pem)の作成方法 { #how-to-create-pem-files }

証明書ファイル(.pem)ファイルの作成手順は次のとおりです。
1. 証明書情報をPEM形式に変換します。
2. 証明書チェーンと秘密鍵を含む単一PEMファイルを作成します。

<a id="how-to-create-pem-files-convert-certificate-information-into-pem"></a>
#### 証明書情報をPEM形式に変換

1. 証明書がJava JKSまたはJCEKS形式の場合は`keytool`を使用し、証明書を`.p12`または`.pks`形式に変換します。
2. 証明書が`.p12`形式または`.pks`の場合には次のコマンドを実行して`.pem`に変換できます。

```sh
openssl pkcs12 -in my_certificate_input_file.pfx -nokeys -out my_cert_converting_result_file.pem
openssl pkcs12 -in my_certificate_input_file.pfx -nodes -nocerts -out my_cert_converting_result_file.pem
```

* 証明書の形式変換に使用する**openssl**コマンドの説明は次のOpenSSLガイドを参照してください。
    * OpenSSLガイド：[https://www.openssl.org/docs/manmaster/man1/openssl.html](https://www.openssl.org/docs/manmaster/man1/openssl.html)
* keytoolの使用方法は次のLinux関連文書を参照してください。
    * java-1.6.0 keytool : [https://linux.die.net/man/1/keytool-java-1.6.0-openjdk](https://linux.die.net/man/1/keytool-java-1.6.0-openjdk)
    * java-1.7.0 keytool : [https://linux.die.net/man/1/keytool-java-1.7.0-openjdk](https://linux.die.net/man/1/keytool-java-1.7.0-openjdk)

<a id="how-to-create-pem-files-optional-convert-into-rsa-private-key-type"></a>
#### (任意) RSA秘密鍵形式に変換

秘密鍵がRSA形式ではない場合、RSA秘密鍵形式で暗号化します。

* 秘密鍵ファイルを開いた時、**-----BEGIN PRIVATE KEY-----**で始まる場合はRSA形式ではない秘密鍵ファイルです。

秘密鍵をRSA秘密鍵形式に変換する場合は次のコマンドを実行します。

``` bash
openssl rsa -in my_key_not_rsa_input_file.pem -check -out my_key_rsa_converting_result_file.pem

> writing RSA key
> Enter PEM pass phrase：(秘密鍵RSA暗号化適用パスフレーズ入力)
> Verifying - Enter PEM pass phrase:
```

<a id="how-to-create-pem-files-create-single-pem-files-including-certificate-chain-and-private-key"></a>
#### 証明書チェーンと秘密鍵を含む単一PEMファイルを作成

証明書PEMファイルおよび秘密鍵PEMファイルにある情報を結合し、単一PEMファイルを作成します。

``` bash
cat my_cert_converting_result_file.pem my_key_rsa_converting_result_file.pem > final_result_pem_file.pem
```
作成されたPEMファイル(上の例では'final\_result\_pem\_file.pem')の形式は下記の通りです。

``` text
-----BEGIN CERTIFICATE-----
.... (your primary SSL certificate)
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
.... (the intermediate CA certificate)
.... (証明書チェーン情報がない場合、この部分はありません。)
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
.... (the trusted root certificate)
.... (証明書チェーン情報がない場合、この部分はありません。)
-----END CERTIFICATE-----
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
```
