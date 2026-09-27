<!-- pre-align:aligned sig=f43b6cdf1fbf -->

<a id="nhn-cloud-sdk-user-guide-getting-started-windows-c"></a>
## NHN Cloud > SDK 사용 가이드 > 시작하기 > Windows C++ { #nhn-cloud-sdk-user-guide-getting-started-windows-c }

<a id="supported-environment"></a>
## 지원 환경 { #supported-environment }
* Windows 7
* Windows 8
* Windows 10
* Windows 11

<a id="structure-of-nhn-cloud-sdk"></a>
## NHN Cloud SDK의 구성 { #structure-of-nhn-cloud-sdk }

Windows C++ 용 NHN Cloud SDK의 구성은 다음과 같습니다.

| Directory | Description | 
|---|---|
| dump_syms.exe| PDB(*.pdb)파일에서 크래시 분석용 심볼(*.sym)을 추출 |
| include| C++ 헤더 파일 |
| x86| C++ Windows 32bit 라이브러리 |
| x64| C++ Windows 64bit 라이브러리 |
| nhncloudsdk_example | 샘플 프로젝트 |

<a id="apply-nhn-cloud-sdk-to-visual-studio-projects"></a>
## NHN Cloud SDK를 Visual Studio 프로젝트에 적용하기 { #apply-nhn-cloud-sdk-to-visual-studio-projects }

NHN Cloud의 [Downloads](../../Download/#nhn-cloud-sdk) 페이지에서 NHN Cloud Windows C++ SDK를 다운로드합니다.

<a id="include-libraries"></a>
### 라이브러리 포함 { #include-libraries }

1. 메뉴바의 **Project** 탭에서 **Properties**를 선택합니다.
2. **C/C++ > General > Additional Include Directories**에서 SDK의 헤더파일 경로를 설정합니다.
3. **Linker > General > Additional Library Directories**에서 빌드환경(Debug/Release)과 Target Machine(x86, x64)에 따라 라이브러리를 포함합니다.
4. **Linker > Input > Additional Dependencies**에서 빌드환경(Debug/Release)과 Target Machine(x86, x64)에 따라 추가할 lib를 입력합니다.
[참고] [https://msdn.microsoft.com/ko-kr/library/ms235636.aspx](https://msdn.microsoft.com/ko-kr/library/ms235636.aspx)

<a id="nhncloudsdkexmple"></a>
### nhncloudsdk_exmple { #nhncloudsdkexmple }
* Visual Studio 2019 기준으로 작성한 샘플 프로젝트입니다.

<a id="use-nhn-cloud-log-crash-search-service"></a>
## NHN Cloud Log & Crash Search Service 사용 { #use-nhn-cloud-log-crash-search-service }

* [Log & Crash](./log-collector-windows) 사용 가이드

