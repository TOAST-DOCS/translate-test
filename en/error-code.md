<!-- machine_translated: true -->

<!-- pre-align:aligned sig=172b01aa78b5 -->

<a id="notification-sms-result-code"></a>

## Notification > SMS > Result Code { #notification-sms-result-code }

<a id="api-result-code"></a>

## API Result Code { #api-result-code }

| category | isSuccess | Result code | Result code message | API response message |
| - | - |-------| - | - |
| Common | true | 0     | Successful | SUCCESS |
| Common | false | 4     | Parameter validation failed | |
| Common | false | -1000 | Invalid appkey | Invalid appKey. |
| Common | false | -1001 | appkey does not exist | Service is not exist. |
| Common | false | -1002 | appkey has been disabled | Service is disabled. |
| Common | false | -1003 | Member not included in project | Not project member id. |
| Common | false | -1004 | IP not allowed | Not allow ip. |
| Common | false | -1007 | Invalid member | MemberType is invalid. |
| Common | false | -1008 | Blocked project | Service is blocked. |
| Common | false | -9995 | Invalid API version | Invalid api version. |
| Common | false | -9996 | Invalid contentType. Only application/json | Only application/json Content-type is supported. |
| Common | false | -9997 | Invalid JSON format | Invalid API parameters. |
| Common | false | -9998 | Non-existent API | Not exist API. |
| Common | false | -9999 | System error (unexpected error) | System error. Please inquire at support@toast.com. |
| Send/Query | false | -1005 | Invalid search condition | Service parameter is invalid. | 
| Send/Query | false | -1006 | Invalid send message type (messageType) | MessageType is invalid. |
| Send/Query | false | -2000 | Invalid date format | Date format error. |
| Send/Query | false | -2001 | Recipient list is empty | RecipientList can not be null. |
| Send/Query | false | -2002 | Invalid attachment file name | Invalid attach file name. |
| Send/Query | false | -2003 | Attachment file extension is not jpg or jpeg | Attach file required jpg or jpeg. |
| Send/Query | false | -2004 | When the attached file is expired or does not exist. | File is expired or does not exist. | 
| Send/Query | false | -2005 | When the attached file size exceeds 300 KB. | The file size must be greater than 0 and less than 300KB. |
| Send/Query | false | -2006 | When the send type set in the template does not match the requested send type. | Invalid template type. |
| Send/Query | false | -2007 | When the requested data does not exist. | Not exist data. |
| Send/Query | false | -2008 | When the request ID (requestId) is invalid. | Invalid requestId. |
| Send/Query | false | -2009 | When the attached file is not uploaded normally due to a server error during upload. | Upload attach file error. | 
| Send/Query | false | -2010 | When the attached file upload type is invalid (server error). | Upload attach file type can not be empty. |
| Send/Query | false | -2011 | When the required query parameter is empty (requestId or startRequestDate, endRequestDate). | RequestId or start/endRequestDate or start/endCreateDate is required. | 
| Send/Query | false | -2012 | When the detailed query parameter is invalid (requestId or mtPr). | Search parameter is invalid.(requestId and mtPr). |
| Send/Query | false | -2014 | When the subject or body is empty. | The recipient can not be empty. |
| Send/Query | false | -2015 | Title or body exceeds the maximum byte. | Title or Body exceed maximum byte. |
| Send/Query | false | -2016 | Recipient count exceeds 1,000. | The max recipient size is 1000. |
| Send/Query | false | -2017 | Excel file creation failed. | Making Excel file is failed. |
| Send/Query | false | -2018 | Recipient number is empty. | RecipientNo can not be empty. |
| Send/Query | false | -2019 | Recipient number is invalid. | RecipientNo is invalid. |
| Send/Query | false | -2021 | System error (queue storage failed). | System error. Failed insert queue. |
| Send/Query | false | -2022 | Request date and time is set before the current time. | RequestDate is not before currentDate. |
| Send/Query | false | -2023 | Title or body includes characters that are not allowed (e.g. emojis). | Unacceptable characters in title and body. |
| Send/Query | false | -2024 | International delivery by LMS/MMS. | LMS/MMS Type is not sent to outside of Korea. |
| Send/Query | false | -2044 | Request sent to a country where sending is unavailable. | Invalid countryCode for sending. |
| Send/Query | false | -2045 | International delivery blocked by service | International sending blocked by service. |
| Send/Query | false | -2046 | Sent to a blocked country | Blocked country by service. |
| Send/Query | false | -2047 | Exceeded the total blocked limit | Blocked by total indicator. |
| Send/Query | false | -2048 | International message body exceeded maximum length | International message body exceed maximum length. |
| Send/Query | false | -2050 | International delivery conversion failed (not in a convertible status) | Conversion status is not ready. |
| Send/Query | false | -2051 | Sending failed due to conversion rate-based blocking | Conversion rate is lower than threshold. |
| Send/Query | false | -2052 | Sending failed due to exceeding the monthly message count per organization | Blocked by organization message sending count exceed. |
| Send/Query | false | -2053 | International delivery failed due to the per-country daily send limit | Blocked by daily country send limit. |
| Send/Query | false | -4000 | Query range exceeds one month | Search is possible within one month. |
| Send/Query | false | -8000 | Authentication phrase not included in authentication message | The body must contain auth guide ment. |
| Template | false | -2100 | Template ID is empty | The templateId can not be empty. |
| Template | false | -2101 | Already registered template ID | Already used templateId. |
| Template | false | -2102 | Template name is empty | The template name can not be empty. |
| Template | false | -2103 | Sender number is empty | The sendNo can not be empty. |
| Template | false | -2104 | Sending type is empty (0: sms, 1: mms) | The sendType can not be empty.(0-sms, 1-mms) |
| Template | false | -2105 | Body is empty | The body can not be empty. |
| Template | false | -2106 | Use status is invalid | UseYn is invalid. |
| Template | false | -2107 | Invalid template ID (when modifying/deleting) | Invalid template. |
| Template | false | -2108 | Category ID is empty | The categoryId can not be empty. |
| Template | false | -2109 | Template ID exceeds 50 characters | TemplateId length must be under 50. |
| Template | false | -2110 | Template does not exist | Template is not exist. |
| Template | false | -2111 | Invalid template parameter | Template add parameter is invalid. |
| Template | false | -2112 | The number of registered templates exceeds the maximum limit (maximum: 1,000) | The maximum number of registered templates. |
| Template | false | -2114 | The title is empty | The title can not be empty. |
| Template | false | -2115 | The title exceeds 120 characters | Title length must be under 120. |
| Template | false | -2116 | The body exceeds 255 characters when the send type is SMS | SMS Body length must be under 255. |
| Template | false | -2117 | The body exceeds 4,000 characters when the send type is LMS/MMS | LMS/MMS Body length must be under 4000. |
| Template | false | -2043 | The attachment file to be registered to the template is already registered to another template | Already used attachFileId |
| Category | false | -2200 | Invalid category parameter (when registering) | Invalid add category parameter.(categoryName, useYn) |
| Category | false | -2201 | Invalid category parameter (when modifying) | Invalid modify category parameter.(categoryId, categoryName, useYn) |
| Category | false | -2202 | Invalid category (category query failed) | Invalid category. |
| Category | false | -2203 | Parent category does not exist | CategoryParentId is invalid. |
| Category | false | -2204 | UseYn is invalid | UseYn is invalid. |
| Category | false | -2205 | Attempting to delete the highest-level category | Cannot delete the highest category. |
| Category | false | -2206 | Category does not exist | Category is not exist. |
| Sender number | false | -2312 | Sender number is empty or not registered | Not regist sendno. |
| Sender number | false | -2313 | Sender number is blocked | This sendno is blocked. |
| Statistics | false | -2700 | Invalid statistics search period | Invalid search period. |
| Statistics | false | -2701 | Invalid statistics search parameter | Invalid statistics search parameter. | 
| Statistics | false | -2703 | Invalid statistics detailed search period | Invalid duration time. |
| Statistics | false | -2704 | Invalid statistics parameter | Invalid stats parameter. |
| Statistics | false | -2706 | Internal statistics error (API call failure) | Failed read stats. |
| 080 unsubscribe | false | -6000 | Opt-out feature is not in use | Block service is not joined. |
| 080 unsubscribe | false | -6001 | Opted-out number | Recipient Number is refused. |
| 080 unsubscribe | false | -6003 | No opt-out guide message in the body | The body must contain block guide ment. |
| 080 unsubscribe | false | -6004 | Opt-out number is empty or not registered | This is not a joined unsubscribeNo. |
| Tag | false | -7000 | Internal tag error (API call failure) | Fail to call Tag API. |
| Tag | false | -7001 | Invalid parameter | Invalid parameter. |
| Tag | false | -7002 | Failed to read .csv | Invalid csv read. |

<a id="result-code-of-receiving"></a>

## Result code of receiving { #result-code-of-receiving }

| Category | Result code | Classification | Description |
| - | - | - | - |
| Telecom Provider | 1000 | Successful | Successful |
| Telecom Provider | 1001 | Failure | Server Busy |
| Telecom Provider | 1002 | Failure | Error in recipient number format |
| Telecom Provider | 1003 | Failure | Error in sender number format |
| Telecom Provider | 1019 | Failure | TTL exceeded |
| Telecom Provider | 2000 | Failure | Delivery time exceeded |
| Telecom Provider | 2001 | Failure | Delivery failed (mobile network) |
| Telecom Provider | 2002 | Failure | Delivery failed (mobile network -> device) |
| Telecom Provider | 2003 | Failure | Device power off |
| Telecom Provider | 2004 | Failure | Unable to deliver because the message buffer between the carrier and the device is full |
| Telecom Provider | 2005 | Failure | Shadow area |
| Telecom Provider | 2006 | Failure | Message deleted |
| Telecom Provider | 2007 | Failure | Temporary device issue |
| Telecom Provider | 3000 | Failure | Unable to send |
| Telecom Provider | 3001 | Failure | No subscriber |
| Telecom Provider | 3002 | Failure | Adult authentication failed |
| Telecom Provider | 3003 | Failure | Recipient number format error or missing number (unavailable number) |
| Telecom Provider | 3004 | Failure | Temporary service suspension on device |
| Telecom Provider | 3005 | Failure | Device call processing status, not delivered to device |
| Telecom Provider | 3006 | Failure | Call rejected |
| Telecom Provider | 3007 | Failure | Phone unavailable to receive callback URL |
| Telecom Provider | 3008 | Failure | Other device issues |
| Telecom Provider | 3009 | Failure | Message format error |
| Telecom Provider | 3010 | Failure | Device not supporting MMS |
| Telecom Provider | 3011 | Failure | Server error |
| Telecom Provider | 3012 | Failure | Spam |
| Telecom Provider | 3013 | Failure | Service denied |
| Telecom Provider | 3014 | Failure | Other |
| Telecom Provider | 3015 | Failure | No transfer route available |
| Telecom Provider | 3016 | Failure | Size restriction failed for attached file |
| Telecom provider | 3017 | Failure | Number format error based on sender number tampering prevention service |
| Telecom provider | 3018 | Failure | Individual subscriber phone number subscribed to the sender number tampering prevention service |
| Telecom provider | 3019 | Failure | Sender numbers that KISA or the Ministry of Science and ICT has blocked for all customers |
| International delivery | 4001 | Failure | Signature format error |
| International delivery | 4002 | Failure | Sender number error |
| International delivery | 4003 | Failure | Recipient number error |
| International delivery | 4004 | Failure | Temporary device issue |
| International delivery | 4005 | Failure | No subscriber |
| International delivery | 4006 | Failure | Failure due to recipient error |
| International delivery | 4007 | Failure | Telecom provider error or blocking |
| International delivery | 4008 | Failure | Spam |
| International delivery | 4009 | Failure | Temporary network error |
| International delivery | 4010 | Failure | Failure due to abnormal sending pattern |
| ETC | E900 | Failure | Other sending errors |
| ETC | E911 | Failure | No attached file extension available, in the case of MMS MT |
| ETC | E913 | Failure | If attached file is sized 0, in the case of MMS MT |
| ETC | E915 | Failure | Duplicate message |
| ETC | E919 | Failure | Resending message is prohibited during when delivery is restricted |
| ETC | E999 | Failure | Other errors |

<a id="dlr-result-code"></a>

## DLR Result Code { #dlr-result-code }
<a id="dlr-status-code"></a>
### DLR Status Code { #dlr-status-code }
| DLR Status Code | Description |
| - | - |
| DELIVERED | Message delivered to the handset |
| ACCEPTED | Message accepted but not yet delivered |
| BUFFERED | Message accepted and queued |
| EXPIRED | Message failed to be delivered within the expiry time due to the telecom provider's retry policy |
| FAILED | Message delivery failed |
| REJECTED | Message rejected by the telecom provider |
| UNKNOWN | Unknown |

<a id="dlr-error-code"></a>
### DLR Error Code { #dlr-error-code }
| DLR Error Code | Description | Details |
| - | - | - |
| 0 | Delivered | Message successfully delivered |
| 1 | Unknown | Message not delivered for an unknown reason |
| 2 | Absent subscriber — temporary | Message not delivered because the handset is temporarily unavailable — try again |
| 3 | Absent subscriber — permanent | The number is no longer active and must be removed from the database |
| 4 | Number blocked by recipient | This is a permanent error — you must delete the number from the database and contact the telecom provider to remove the block |
| 5 | Portability error | If there is an issue related to number portability, contact the telecom provider to resolve it |
| 6 | Anti-spam filter block | Message blocked by the telecom provider's anti-spam filter |
| 7 | Handset busy | The handset is unavailable when the message is sent — try again |
| 8 | Network error | Message delivery failed due to a network error — try again |
| 9 | Invalid number | The recipient has specifically opted out of receiving messages from a particular service |
| 11 | Unroutable | NHN Cloud could not find an appropriate route to send the message — contact customer support |
| 12 | Unreachable destination | No route to the number could be found — verify the recipient number |
| 13 | Recipient age restriction | Unable to receive the message due to the recipient's age restriction |
| 14 | Number blocked by telecom provider | Contact the telecom provider to enable SMS service on the recipient's plan |
| 16 | Gateway quota exceeded | Message delivery failed because the number of allowed requests per period was exceeded. This error applies only to accounts registered in the United States and France |
| 20 | Anti-fraud traffic rule | Message rejected due to traffic pumping — contact customer support |
| 21 | Abnormal consecutive sending detected | The threshold for the high-density recipient number range has been exceeded |
| 22 | Abnormal traffic spike detected | The relative increase threshold has been exceeded |
| 39 | Invalid sender address for US destination | Message delivery to the United States failed due to a sender number issue — contact customer support |
| 51 | Header filter | Message delivery to the United States failed due to a sender number issue — contact customer support |
| 53 | Consent filter | Message delivery failed because consent was not given |
| 54 | Regulatory error | An unexpected regulatory error occurred — contact customer support |
| 99 | General error | Generally indicates a routing error — contact customer support |
| 1000 | Other error | Any other error |

<a id="query-delivery-codes"></a>

## Query Delivery Codes { #query-delivery-codes }
<a id="query-delivery-codes-result-code-of-receiving"></a>
### Reception Result Query Codes { #query-delivery-codes-result-code-of-receiving }

| Code Value | Description | 
| - | - |
| MTR1 | Successful | 
| MTR2 | Failure | 

<a id="detail-result-code-of-receiving"></a>
### Reception Result Query Detail Codes { #detail-result-code-of-receiving }

| Code Value | Description | 
| - | - |
| MTR2_1 | Validation failure | 
| MTR2_2 | Telecom provider issue | 
| MTR2_3 | Handset issue |