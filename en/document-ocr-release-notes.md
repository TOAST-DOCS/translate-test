<!-- machine_translated: true -->

<!-- pre-align:aligned sig=1dc1c0f63720 -->

<a id="ai-service-ocr-document-ocr-release-notes"></a>
## AI Service > OCR > Document OCR > Release Notes { #ai-service-ocr-document-ocr-release-notes }

<a id="september-8-2026"></a>
## September 8, 2026 { #september-8-2026 }

- Encrypted serial number now required for driver license authenticity verification
  - Starting September 7, 2026, the encrypted serial number must be included in driver license authenticity verification requests.
  - This change reflects the strengthened driver license authenticity verification procedures of the National Police Agency.
  - The encrypted serial number can be found in the driver license analysis results.
  - For more information, see the [API Guide](./document-ocr-api-guide-v2.1.md).

<a id="august-11-2026"></a>
## August 11, 2026 { #august-11-2026 }

- API endpoint domain change
  - Added the new endpoint `https://api-ocr.nhncloudservice.com`.
  - The existing endpoint `https://ocr.api.nhncloudservice.com` will be maintained until July 31, 2027, after which support will end.
  - Switch to the new endpoint. For more information, see the [API Guide](./document-ocr-api-guide-v2.1.md).
- Increased the maximum request file size
  - Increased the maximum request file size from 5 MB to 20 MB.

<a id="may-27-2026"></a>
## May 27, 2026 { #may-27-2026 }

- Deprecated the passport authenticity verification service.
  - ID authenticity verification has been limited to resident registration card and driver's license.
  - For more information, see the [API Guide](./document-ocr-api-guide-v2.1.md).

<a id="march-10-2026"></a>
## March 10, 2026 { #march-10-2026 }

- API v1.1, v2.1 released
  - Added API using User Access Key token authentication.
  - For more information on issuing and using User Access Key tokens, please refer to the [User Access Key Token](/nhncloud/en/public-api/user-access-key-token).

<a id="may-13-2025"></a>
## May 13, 2025 { #may-13-2025 }
- Added [error code](./document-ocr-error-code.md) for password-configured PDF files when requesting business license analysis

<a id="april-15-2025"></a>
## April 15, 2025 { #april-15-2025 }
- Improved the speed of credit card recognition

<a id="march-11-2025"></a>
## March 11, 2025 { #march-11-2025 }
- Improved the speed of credit card recognition
- Improved the speed of ID card recognition

<a id="august-13-2024"></a>
## August 13, 2024 { #august-13-2024 }
- Added [error code](./document-ocr-error-code.md) for cases where an error occurs more than 5 times in entering the resident registration card issuance date when requesting verification of ID authenticity

<a id="july-9-2024"></a>
## July 9, 2024 { #july-9-2024 }
- Improved ID card recognition performance

<a id="april-9-2024"></a>
## April 9, 2024 { #april-9-2024 }
- Changed the password sequence number to not be a required value for driver licenses when requesting ID authenticity verification
- Improved ID card recognition performance

<a id="march-12-2024"></a>
## March 12, 2024 { #march-12-2024 }
- Added information on recognition area coordiates of the analyzed key when ID card analysis is successful

<a id="september-26-2023"></a>
## September 26, 2023 { #september-26-2023 }
- Added a feature to retrieve stoppage/closure of business registration certificates
- Improved the performance of business registration certificate recognition

<a id="august-29-2023"></a>
## August 29, 2023 { #august-29-2023 }
- Added an ID card analysis option
    - Added a stand alone API
    - Added passport
- Added an option to ID card authenticity verification
    - Added passport
- Improved the performance of business registration certificate recognition

<a id="june-13-2023"></a>
## June 13, 2023 { #june-13-2023 }
- Improved ID card recognition performance

<a id="march-28-2023"></a>
## March 28, 2023 { #march-28-2023 }
- Changed the service name from Document Recognizer to OCR

<a id="february-28-2023"></a>
## February 28, 2023 { #february-28-2023 }
- Improved the performance of business registration certificate
- Improved the console UI
    - Removed guide message at the top

<a id="december-27-2022"></a>
## December 27, 2022 { #december-27-2022 }
- Improved the performance of ID card recognition

<a id="november-29-2022"></a>
## November 29, 2022 { #november-29-2022 }
- Added an ID card analysis feature

<a id="october-25-2022"></a>
## October 25, 2022 { #october-25-2022 }
- Improved the performance of credit card recognition

<a id="august-23-2022"></a>
## August 23, 2022 { #august-23-2022 }
- Credit Card Analysis API v2.0 released

<a id="july-26-2022"></a>
## July 26, 2022 { #july-26-2022 }
- Improved the performance of credit card recognition
- Improved the speed of credit card recognition

<a id="may-24-2022"></a>
## May 24, 2022 { #may-24-2022 }
- Improved the service so that it can recognize credit card images taken at an angle

<a id="march-29-2022"></a>
## March 29, 2022 { #march-29-2022 }
- Improved the performance of credit card recognition

<a id="december-28-2021"></a>
## December 28, 2021 { #december-28-2021 }
- Added a credit card analysis feature

<a id="october-26-2021"></a>
## October 26, 2021 { #october-26-2021 }
- Document Recognizer service released
