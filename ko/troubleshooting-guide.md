<!-- pre-align:aligned sig=aa4052351c5f -->

<a id="management-certificate-manager-troubleshooting-guide"></a>
## Management > Certificate Manager > 문제 해결 가이드 { #management-certificate-manager-troubleshooting-guide }

<a id="converting-certificate-file-formats"></a>
## 인증서 파일 형식 변환 { #converting-certificate-file-formats }

Certificate Manager에서는 .pem 형식의 인증서 파일만 지원합니다.

* 차후 지원하는 인증서 형식을 추가할 예정입니다.

Certificate Manager에서 사용하는 인증서 파일 형식은 아래와 같습니다.

<a id="format-of-certificate-file-pem"></a>
### 인증서 파일(.pem) 형식 { #format-of-certificate-file-pem }

인증서 파일 확장자는 **.pem**입니다.

파일에는 인증서 (체인) 정보와 개인 키 정보가 포함되어 있습니다.

``` text
-----BEGIN CERTIFICATE-----
...
-----END CERTIFICATE-----
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
```

<a id="how-to-create-pem-files"></a>
### 인증서 파일(.pem) 생성 방법 { #how-to-create-pem-files }

인증서 파일(.pem) 파일 생성 단계는 다음과 같습니다.
1. 인증서 정보를 PEM 형식으로 변환합니다.
2. 인증서 체인과 개인 키를 포함하는 단일 PEM 파일을 생성합니다.

<a id="how-to-create-pem-files-convert-certificate-information-into-pem"></a>
#### 인증서 정보를 PEM 형식으로 변환

1. 인증서가 Java JKS 또는 JCEKS 형식일 때는 `keytool`을 사용하여 인증서를 `.p12` 또는 `.pks` 형식으로 변환합니다.
2. 인증서가 `.p12` 형식이거나 `.pks`인 경우에는 다음 명령을 수행하여 `.pem` 으로 변환할 수 있습니다.

```sh
openssl pkcs12 -in my_certificate_input_file.pfx -nokeys -out my_cert_converting_result_file.pem
openssl pkcs12 -in my_certificate_input_file.pfx -nodes -nocerts -out my_cert_converting_result_file.pem
```

* 인증서 형식 변환에 사용되는 **openssl** 명령어 설명은 다음 OpenSSL 가이드를 참고하십시오.
    * OpenSSL 가이드: [https://www.openssl.org/docs/manmaster/man1/openssl.html](https://www.openssl.org/docs/manmaster/man1/openssl.html)
* keytool 사용법은 다음 Linux 관련 문서를 참고하십시오.
    * java-1.6.0 keytool : [https://linux.die.net/man/1/keytool-java-1.6.0-openjdk](https://linux.die.net/man/1/keytool-java-1.6.0-openjdk)
    * java-1.7.0 keytool : [https://linux.die.net/man/1/keytool-java-1.7.0-openjdk](https://linux.die.net/man/1/keytool-java-1.7.0-openjdk)

<a id="how-to-create-pem-files-optional-convert-into-rsa-private-key-type"></a>
#### (선택) RSA 개인 키 형식으로 변환

개인 키가 RSA 형식이 아닌 경우 RSA 개인 키 형식으로 암호화합니다.

* 개인 키 파일을 열었을 때 **-----BEGIN PRIVATE KEY-----** 로 시작하면 RSA 형식이 아닌 개인 키 파일입니다.

개인 키를 RSA 개인 키 형식으로 변환하는 경우 다음 명령어를 실행합니다.

``` bash
openssl rsa -in my_key_not_rsa_input_file.pem -check -out my_key_rsa_converting_result_file.pem

> writing RSA key
> Enter PEM pass phrase: (개인키 RSA 암호화 적용 패스프레이즈 입력)
> Verifying - Enter PEM pass phrase:
```

<a id="how-to-create-pem-files-create-single-pem-files-including-certificate-chain-and-private-key"></a>
#### 인증서 체인과 개인 키를 포함하는 단일 PEM 파일 생성

인증서 PEM 파일 및 개인 키 PEM 파일에 있는 정보를 결합하여 단일 PEM 파일을 만듭니다.

``` bash
cat my_cert_converting_result_file.pem my_key_rsa_converting_result_file.pem > final_result_pem_file.pem
```
만들어진 PEM 파일(위의 예제에선 'final\_result\_pem\_file.pem')의 형식은 아래와 같습니다.

``` text
-----BEGIN CERTIFICATE-----
.... (your primary SSL certificate)
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
.... (the intermediate CA certificate)
.... (인증서 체인 정보가 없을 경우 이 부분이 없습니다.)
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
.... (the trusted root certificate)
.... (인증서 체인 정보가 없을 경우 이 부분이 없습니다.)
-----END CERTIFICATE-----
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
```
