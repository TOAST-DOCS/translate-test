<!-- pre-align:aligned sig=dbef1ffc99ce -->

<a id="ai-service-ocr-document-ai-console-user-guide"></a>
## AI Service > OCR > Document AI > 콘솔 사용 가이드 { #ai-service-ocr-document-ai-console-user-guide }

콘솔에 이미지 파일을 업로드하고 문서 유형과 질문을 입력하여 답변을 얻을 수 있습니다.

<a id="document-ai-analysis"></a>
## Document AI 분석 { #document-ai-analysis }

<a id="select-document-types-for-analysis"></a>
### 분석을 위한 문서 유형 선택 { #select-document-types-for-analysis }

분석할 이미지의 문서 유형을 선택합니다.

* 선택 안 함(일반)
* 사업자등록증
* 명함

<a id="upload-an-image-for-analysis"></a>
### 분석을 위한 이미지 업로드 { #upload-an-image-for-analysis }

분석할 이미지를 업로드합니다.<br>
이미지는 다음 2가지 방법으로 업로드할 수 있습니다.
1. **이미지 업로드** 클릭
2. 이미지 드래그 앤드 드롭

<a id="enter-a-question"></a>
### 질문 입력 { #enter-a-question }

질문을 입력합니다.

<a id="analysis"></a>
### 분석 { #analysis }

**분석**을 클릭하면 분석 결과가 화면 오른쪽에 나타납니다.

![General OCR Image](http://static.toastoven.net/prod_ocr/DocumentAI_console_ko.png)

* **텍스트**: 분석 결과를 표시합니다.
* **JSON**: 분석 결과를 JSON 코드 형식으로 표시합니다.
    * **llmResponse**: LLM 분석 답변
* **복사**, **다운로드**: 분석 결과 복사 및 다운로드(Text, JSON) 기능을 제공합니다. 
* JSON 분석 결과 예시
```json
{
  "llmResponse": "본 문서는 의미가 없는 텍스트인 '로렌 ipsum'을 사용하여 글자가 있는 그러나 읽기 어렵고 가독성이 떨어지는 문장을 작성한 것 같습니다."
}
```

<a id="initialize"></a>
### 초기화 { #initialize }

**초기화**를 클릭하면 입력하신 이미지, 질문 및 답변 결과가 모두 초기화됩니다.
