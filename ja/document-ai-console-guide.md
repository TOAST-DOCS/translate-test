<!-- pre-align:aligned sig=dbef1ffc99ce -->

<a id="ai-service-ocr-document-ai-console-user-guide"></a>
## AI Service > OCR > Document AI > コンソール使用ガイド { #ai-service-ocr-document-ai-console-user-guide }

コンソールに画像ファイルをアップロードし、文書の種類と質問を入力して回答を得ることができます。

<a id="document-ai-analysis"></a>
## Document AI分析 { #document-ai-analysis }

<a id="select-document-types-for-analysis"></a>
### 分析のための文書タイプ選択 { #select-document-types-for-analysis }

分析する画像の文書タイプを選択します。

* 選択しない(一般)
* 事業者登録証
* 名刺

<a id="upload-an-image-for-analysis"></a>
### 分析のための画像アップロード { #upload-an-image-for-analysis }

分析する画像をアップロードします。
画像は次の2つの方法でアップロードできます。
1. **画像アップロード**クリック
2. 画像をドラッグ＆ドロップ

<a id="enter-a-question"></a>
### 質問の入力 { #enter-a-question }

質問を入力します。

<a id="analysis"></a>
### 分析 { #analysis }

**分析**をクリックすると、分析結果が画面右側に表示されます。

![General OCR Image](http://static.toastoven.net/prod_ocr/DocumentAI_console_ko.png)

* **テキスト**：分析結果を表示します。
* **JSON**：分析結果をJSONコード形式で表示します。
    * **llmResponse**: LLM分析の回答
* **コピー**、**ダウンロード**：分析結果のコピー及びダウンロード(Text, JSON)機能を提供します。 
* JSON分析結果例
```json
{
  "llmResponse": "この文書は、意味のないテキストである'ローレンipsum'を使用して、文字はあるが読みにくい、可読性が落ちる文章を作成したようです。"
}
```

<a id="initialize"></a>
### 初期化 { #initialize }

**初期化**をクリックすると、入力された画像、質問、回答結果がすべて初期化されます。
