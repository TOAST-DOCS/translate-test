<!-- pre-align:aligned sig=c2c525b018f2 -->

<a id="ai-service-ocr-document-ai-release-notes"></a>
## AI Service > OCR > Document AI > Release Notes { #ai-service-ocr-document-ai-release-notes }

<a id="august-11-2026"></a>
### August 11, 2026 { #august-11-2026 }

- API endpoint domain change
  - Added the new endpoint `https://api-ocr.nhncloudservice.com`.
  - The existing endpoint `https://ocr.api.nhncloudservice.com` will be maintained until July 31, 2027, after which support will end.
  - Switch to the new endpoint. For more information, see the [API Guide](./document-ai-api-guide-v1.1.md).
- Increased the maximum request file size
  - Increased the maximum request file size from 5 MB to 20 MB.

<a id="march-10-2026"></a>
### March 10, 2026 { #march-10-2026 }

- API v1.1 released
  - Added API using User Access Key token authentication.
  - For more information on issuing and using User Access Key tokens, please refer to the [User Access Key Token](/nhncloud/en/public-api/user-access-key-token).

<a id="november-12-2024"></a>
### November 12, 2024 { #november-12-2024 }

- Release of Document AI
  - Document AI extracts characters from images through OCR and provides questions and answers such as summarizing the content and extracting information based on the extracted informati on in conjunction with the LLM model.