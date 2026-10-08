<!-- pre-align:aligned sig=dbef1ffc99ce -->

<a id="ai-service-ocr-document-ai-console-user-guide"></a>
## AI Service > OCR > Document AI > Console User Guide { #ai-service-ocr-document-ai-console-user-guide }

You can upload an image file to the console, enter a document type and a question to get answers.

<a id="document-ai-analysis"></a>
## Document AI Analysis { #document-ai-analysis }

<a id="select-document-types-for-analysis"></a>
### Select document types for analysis { #select-document-types-for-analysis }

Select the document type of the image you want to analyze.

* Not selected (General)
* Business registration certificate
* Business card

<a id="upload-an-image-for-analysis"></a>
### Upload an Image for Analysis { #upload-an-image-for-analysis }

Upload an image to analyze.<br>
Images can be uploaded in the following two methods:
1. Click **Upload Image**
2. Drag and drop the image

<a id="enter-a-question"></a>
### Enter a Question { #enter-a-question }

Enter a question.

<a id="analysis"></a>
### Analysis { #analysis }

When you click **Analysis**, the results of your analysis appear on the right side of the screen.

![General OCR Image](http://static.toastoven.net/prod_ocr/DocumentAI_console_ko.png)

* **Text**: Displays the results of the analysis.
* **JSON**: Displays the results of your analysis in JSON code format.
    * **llmResponse**: LLM Analysis Response
* **Copy**, **Download**: Provides the feature to copy and download analytics results (Text, JSON). 
* JSON Analysis Results
```json
{
  "llmResponse": "It appears that this document uses 'loren ipsum', which is meaningless text, to create a sentence that has letters but is difficult and illegible to read."
}
```

<a id="initialize"></a>
### Initialize { #initialize }

Click **Reset** to reset any images, questions, and answers you entered.
