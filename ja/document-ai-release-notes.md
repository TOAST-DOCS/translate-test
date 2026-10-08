<!-- pre-align:aligned sig=c2c525b018f2 -->

<a id="ai-service-ocr-document-ai-release-notes"></a>
## AI Service > OCR > Document AI > リリースノート { #ai-service-ocr-document-ai-release-notes }

<a id="august-11-2026"></a>
### 2026. 08. 11. { #august-11-2026 }

- APIエンドポイントドメインの変更
  - 新規エンドポイント `https://api-ocr.nhncloudservice.com` が追加されました。
  - 既存のエンドポイント `https://ocr.api.nhncloudservice.com` は、2027年7月31日まで維持された後、サポートが終了します。
  - 新規エンドポイントへ切り替えてください。詳細については、[APIガイド](./document-ai-api-guide-v1.1.md)を参照してください。
- リクエストファイルの最大容量拡大
  - リクエストファイルの最大容量が5MBから20MBに拡大されました。

<a id="march-10-2026"></a>
### 2026. 03. 10. { #march-10-2026 }

- API v1.1リリース
  - User Access Keyトークン認証を使用するAPIが追加されました。
  - User Access Keyトークンの発行及び使用に関する詳細は、[User Access Keyトークン](/nhncloud/ja/public-api/user-access-key-token)を参照してください。

<a id="november-12-2024"></a>
### 2024. 11. 12. { #november-12-2024 }

* Document AIサービスリリース
    * OCRを通じて画像から文字を抽出し、抽出した情報を基にLLMモデルと連動して内容の要約、情報抽出などの質疑応答を提供するサービスです。
