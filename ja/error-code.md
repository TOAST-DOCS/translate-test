<!-- machine_translated: true -->

<!-- pre-align:aligned sig=172b01aa78b5 -->

<a id="notification-sms-result-code"></a>
## Notification > SMS > 結果コード { #notification-sms-result-code }

<a id="api-result-code"></a>
## API結果コード { #api-result-code }

| カテゴリー | 成功可否 | 結果コード | 結果コードメッセージ | API応答メッセージ | 
| - | - |-------| - | - |
| 共通 | true | 0     | 成功 | SUCCESS |
| 共通 | false | 4     | パラメータの有効性検証失敗 | | 
| 共通 | false | -1000 | 無効なアプリキー | Invalid appKey. |
| 共通 | false | -1001 | 存在しないアプリキー | Service is not exist. |
| 共通 | false | -1002 | 使用終了したアプリキー | Service is disabled. |
| 共通 | false | -1003 | プロジェクトに含まれないメンバー | Not project member id. |
| 共通 | false | -1004 | 許可されていないIP | Not allow ip. |
| 共通 | false | -1007 | 無効なメンバー | MemberType is invalid. |
| 共通 | false | -1008 | ブロックされたプロジェクト | Service is blocked. |
| 共通 | false | -9995 | 無効なAPIバージョン | Invalid api version. |
| 共通 | false | -9996 | 無効なcontentType。Only application/JSON | Only application/json Content-type is supported. |
| 共通 | false | -9997 | 無効なJSON形式 | Invalid API parameters. |
| 共通 | false | -9998 | 存在しないAPI | Not exist API. |
| 共通 | false | -9999 | システムエラー(予期しないエラー) | System error. Please inquire at support@toast.com. |
| 送信/照会 | false | -1005 | 無効な検索条件 | Service parameter is invalid. | 
| 送信/照会 | false | -1006 | 無効な送信メッセージ(messageType)タイプ | MessageType is invalid. |
| 送信/照会 | false | -2000 | 無効な日付形式 | Date format error. |
| 送信/照会 | false | -2001 | 受信者が空の場合 | RecipientList can not be null. |
| 送信/照会 | false | -2002 | 添付ファイル名が無効な場合 | Invalid attach file name. |
| 送信/照会 | false | -2003 | 添付ファイルの拡張子がjpg、jpegではない場合 | Attach file required jpg or jpeg. |
| 送信/照会 | false | -2004 | 添付ファイルが期限切れまたは存在しない場合 | File is expired or does not exist. | 
| 送信/照会 | false | -2005 | 添付ファイルのサイズが300KBを超える場合 | The file size must be greater than 0 and less than 300KB. |
| 送信/照会 | false | -2006 | テンプレートに設定された送信タイプとリクエストされた送信タイプが一致しない場合 | Invalid template type. |
| 送信/照会 | false | -2007 | リクエストされたデータが存在しない場合 | Not exist data. |
| 送信/照会 | false | -2008 | リクエストID(requestId)が無効な場合 | Invalid requestId. |
| 送信/照会 | false | -2009 | 添付ファイルのアップロード中にサーバーエラーが発生し、正常にアップロードされなかった場合 | Upload attach file error. | 
| 送信/照会 | false | -2010 | 添付ファイルのアップロードタイプが無効な場合(サーバーエラー) | Upload attach file type can not be empty. |
| 送信/照会 | false | -2011 | 必須照会パラメータが空の場合(requestIdまたはstartRequestDate、endRequestDate) | RequestId or start/endRequestDate or start/endCreateDate is required. | 
| 送信/照会 | false | -2012 | 詳細照会パラメータが無効な場合(requestIdまたはmtPr) | Search parameter is invalid.(requestId and mtPr). |
| 送信/照会 | false | -2014 | タイトルまたは本文が空の場合 | The recipient can not be empty. |
| 送信/照会 | false | -2015 | タイトルまたは本文が超過した場合 | Title or Body exceed maximum byte. |
| 送信/照会 | false | -2016 | 受信者が1,000人を超えた場合 | The max recipient size is 1000. |
| 送信/照会 | false | -2017 | Excelの作成が失敗した場合 | Making Excel file is failed. |
| 送信/照会 | false | -2018 | 受信者番号が空の場合 | RecipientNo can not be empty. |
| 送信/照会 | false | -2019 | 受信者番号が無効な場合 | RecipientNo is invalid. |
| 送信/照会 | false | -2021 | システムエラー(キュー保存失敗) | System error. Failed insert queue. |
| 送信/照会 | false | -2022 | リクエスト日時を現在時刻より以前に設定した場合 | RequestDate is not before currentDate. |
| 送信/照会 | false | -2023 | タイトルまたは本文に許可されていない文字(Emojiなど)が含まれている場合 | Unacceptable characters in title and body. |
| 送信/照会 | false | -2024 | LMS/MMSで国際送信を行う場合 | LMS/MMS Type is not sent to outside of Korea. |
| 送信/照会 | false | -2044 | 送信不可能な国へリクエストを送った場合 | Invalid countryCode for sending. |
| 送信/照会 | false | -2045 | 国際送信をブロックした場合 | International sending blocked by service. |
| 送信/照会 | false | -2046 | ブロックした国に送信した場合 | Blocked country by service. |
| 送信/照会 | false | -2047 | ブロック制限件数を超えた場合 | Blocked by total indicator. |
| 送信/照会 | false | -2048 | 国際送信の本文が最大長を超えた場合 | International message body exceed maximum length. |
| 送信/照会 | false | -2050 | 国際送信への変換に失敗した場合(変換可能な状態ではない) | Conversion status is not ready. |
| 送信/照会 | false | -2051 | コンバージョン率ベースのブロックにより送信に失敗した場合 | Conversion rate is lower than threshold. |
| 送信/照会 | false | -2052 | 組織あたりの月別送信数超過により送信に失敗した場合 | Blocked by organization message sending count exceed. |
| 送信/照会 | false | -2053 | 国別1日送信上限の制限により国際送信に失敗した場合 | Blocked by daily country send limit. |
| 送信/照会 | false | -4000 | 照会範囲が1か月を超えた場合 | Search is possible within one month. |
| 送信/照会 | false | -8000 | 認証送信に認証フレーズが含まれていない場合 | The body must contain auth guide ment. |
| テンプレート | false | -2100 | テンプレートIDが空の場合 | The templateId can not be empty. |
| テンプレート | false | -2101 | 既に登録済みのテンプレートID | Already used templateId. |
| テンプレート | false | -2102 | テンプレート名が空の場合 | The template name can not be empty. |
| テンプレート | false | -2103 | 発信番号が空の場合 | The sendNo can not be empty. |
| テンプレート | false | -2104 | 送信タイプが空の場合(0: sms, 1: mms) | The sendType can not be empty.(0-sms, 1-mms) |
| テンプレート | false | -2105 | 本文が空の場合 | The body can not be empty. |
| テンプレート | false | -2106 | 使用可否が無効な場合 | UseYn is invalid. |
| テンプレート | false | -2107 | 無効なテンプレートID(修正/削除時) | Invalid template. |
| テンプレート | false | -2108 | カテゴリーIDが空の場合 | The categoryId can not be empty. |
| テンプレート | false | -2109 | テンプレートIDが50文字を超える場合 | TemplateId length must be under 50. |
| テンプレート | false | -2110 | テンプレートが存在しない場合 | Template is not exist. |
| テンプレート | false | -2111 | 無効なテンプレートパラメータの場合 | Template add parameter is invalid. |
| テンプレート | false | -2112 | 登録可能なテンプレートの最大数を超えた場合(最大: 1,000) | The maximum number of registered templates. |
| テンプレート | false | -2114 | タイトルが空の場合 | The title can not be empty. |
| テンプレート | false | -2115 | タイトルが120文字を超える場合 | Title length must be under 120. |
| テンプレート | false | -2116 | 送信タイプがSMSで、本文の長さが255文字を超える場合 | SMS Body length must be under 255. |
| テンプレート | false | -2117 | 送信タイプがLMS/MMSで、本文の長さが4,000文字を超える場合 | LMS/MMS Body length must be under 4000. |
| テンプレート | false | -2043 | テンプレートに登録する添付ファイルがすでに他のテンプレートに登録されている場合 | Already used attachFileId |
| カテゴリー | false | -2200 | 無効なカテゴリーパラメータ(登録時) | Invalid add category parameter.(categoryName, useYn) |
| カテゴリー | false | -2201 | 無効なカテゴリーパラメータ(修正時) | Invalid modify category parameter.(categoryId, categoryName, useYn) |
| カテゴリー | false | -2202 | 無効なカテゴリー(カテゴリー照会失敗) | Invalid category. |
| カテゴリー | false | -2203 | 親カテゴリーが存在しない場合 | CategoryParentId is invalid. |
| カテゴリー | false | -2204 | 使用可否が無効な場合 | UseYn is invalid. |
| カテゴリー | false | -2205 | 最上位カテゴリーを削除しようとした場合 | Cannot delete the highest category. |
| カテゴリー | false | -2206 | 存在しないカテゴリーの場合 | Category is not exist. |
| 発信番号 | false | -2312 | 発信番号が空白または未登録の状態 | Not regist sendno. |
| 発信番号 | false | -2313 | ブロックされた発信番号 | This sendno is blocked. |
| 統計 | false | -2700 | 無効な統計範囲 | Invalid search period. |
| 統計 | false | -2701 | 無効な統計検索パラメータ | Invalid statistics search parameter. |
| 統計 | false | -2703 | 無効な統計詳細範囲 | Invalid duration time. |
| 統計 | false | -2704 | 無効な統計パラメータ | Invalid stats parameter. |
| 統計 | false | -2706 | 統計内部エラー(API呼び出し失敗) | Failed read stats. |
| 080受信拒否 | false | -6000 | 受信拒否機能を使用していない | Block service is not joined. |
| 080受信拒否 | false | -6001 | 受信拒否された番号 | Recipient Number is refused. |
| 080受信拒否 | false | -6003 | 本文に受信拒否案内メッセージがない | The body must contain block guide ment. |
| 080受信拒否 | false | -6004 | 受信拒否番号が空であるか未登録の番号 | This is not a joined unsubscribeNo. |
| タグ | false | -7000 | タグ内部エラー(API呼び出し失敗) | Fail to call Tag API. |
| タグ | false | -7001 | 無効なパラメータ | Invalid parameter. |
| タグ | false | -7002 | .csvの読み取り失敗 | Invalid csv read. |

<a id="result-code-of-receiving"></a>
## 受信結果コード { #result-code-of-receiving }

| 区分 | 結果コード | 分類 | 意味 |
| - | - | - | - |
| 移動体通信事業者 | 1000 | 成功 | 成功 |
| 移動体通信事業者 | 1001 | 失敗 | Server Busy |
| 移動体通信事業者 | 1002 | 失敗 | 受信番号フォーマットエラー |
| 移動体通信事業者 | 1003 | 失敗 | 発信番号フォーマットエラー |
| 移動体通信事業者 | 1019 | 失敗 | TTL超過 |
| 移動体通信事業者 | 2000 | 失敗 | 送信タイムアウト |
| 移動体通信事業者 | 2001 | 失敗 | 送信失敗(無線網側) |
| 移動体通信事業者 | 2002 | 失敗 | 送信失敗(無線網→端末側) |
| 移動体通信事業者 | 2003 | 失敗 | 端末の電源オフ |
| 移動体通信事業者 | 2004 | 失敗 | サービスプロバイダーと端末間のメッセージバッファが満杯のため配信不可 |
| 移動体通信事業者 | 2005 | 失敗 | 電波の届かない地域 |
| 移動体通信事業者 | 2006 | 失敗 | メッセージが削除されました |
| 移動体通信事業者 | 2007 | 失敗 | 一時的な端末の問題 |
| 移動体通信事業者 | 3000 | 失敗 | 送信できません |
| 移動体通信事業者 | 3001 | 失敗 | 加入者が存在しません |
| 移動体通信事業者 | 3002 | 失敗 | 成人認証失敗 |
| 移動体通信事業者 | 3003 | 失敗 | 受信番号の形式エラーまたは欠番(存在しない番号) |
| 移動体通信事業者 | 3004 | 失敗 | 端末サービス一時停止 |
| 移動体通信事業者 | 3005 | 失敗 | 端末の呼処理(Call processing)状態、端末に到達できません |
| 移動体通信事業者 | 3006 | 失敗 | 着信拒否 |
| 移動体通信事業者 | 3007 | 失敗 | コールバックURLを受信できない端末 |
| 移動体通信事業者 | 3008 | 失敗 | その他の端末の問題 |
| 移動体通信事業者 | 3009 | 失敗 | メッセージ形式エラー |
| 移動体通信事業者 | 3010 | 失敗 | MMS非対応端末 |
| 移動体通信事業者 | 3011 | 失敗 | サーバーエラー |
| 移動体通信事業者 | 3012 | 失敗 | スパム |
| 移動体通信事業者 | 3013 | 失敗 | サービス拒否 |
| 移動体通信事業者 | 3014 | 失敗 | その他 |
| 移動体通信事業者 | 3015 | 失敗 | 送信経路なし |
| 移動体通信事業者 | 3016 | 失敗 | 添付ファイルサイズ制限超過 |
| 移動体通信事業者 | 3017 | 失敗 | 発信番号偽装防止サービスに基づく番号形式エラー |
| 移動体通信事業者 | 3018 | 失敗 | 発信番号偽装防止サービスに登録された携帯電話個人加入者番号 |
| 移動体通信事業者 | 3019 | 失敗 | KISAまたは未来創造科学部がすべての顧客企業に対してブロック処理した発信番号 |
| 国際送信 | 4001 | 失敗 | 署名形式エラー |
| 国際送信 | 4002 | 失敗 | 発信番号エラー |
| 国際送信 | 4003 | 失敗 | 受信番号エラー |
| 国際送信 | 4004 | 失敗 | 一時的な端末の問題 |
| 国際送信 | 4005 | 失敗 | 加入者なし |
| 国際送信 | 4006 | 失敗 | 受信者エラーによる失敗 |
| 国際送信 | 4007 | 失敗 | サービスプロバイダーエラーまたはブロック |
| 国際送信 | 4008 | 失敗 | スパム |
| 国際送信 | 4009 | 失敗 | 一時的なネットワークエラー |
| 国際送信 | 4010 | 失敗 | 異常な送信パターンによる失敗 |
| ETC | E900 | 失敗 | その他の送信エラー |
| ETC | E911 | 失敗 | 添付ファイルの拡張子がない場合 |
| ETC | E913 | 失敗 | 添付ファイルのサイズが0の場合 |
| ETC | E915 | 失敗 | 重複メッセージ |
| ETC | E919 | 失敗 | 送信制限時間の場合、メッセージの再送信処理が禁止されている場合 |
| ETC | E999 | 失敗 | その他のエラー |

<a id="dlr-result-code"></a>
## DLR結果コード { #dlr-result-code }
<a id="dlr-status-code"></a>
### DLRステータスコード { #dlr-status-code }
| DLRステータスコード | 意味 |
| - | - |
| DELIVERED | メッセージが端末に送信された状態 |
| ACCEPTED | メッセージが受け付けられたが、まだ送信されていない状態 |
| BUFFERED | メッセージが受け付けられ、待機中の状態 |
| EXPIRED | サービスプロバイダーの再送信ポリシーにより、メッセージの有効期限内に送信失敗 |
| FAILED | メッセージ送信失敗 |
| REJECTED | サービスプロバイダーがメッセージ送信を拒否した状態 |
| UNKNOWN | 不明 |

<a id="dlr-error-code"></a>
### DLRエラーコード { #dlr-error-code }
| DLRエラーコード | 意味 | 説明 |
| - | - | - |
| 0 | 送信済み | メッセージが正常に送信されました。 |
| 1 | 不明 | メッセージが不明な理由で送信されませんでした。 |
| 2 | 受信者不在 - 一時的 | 一時的に端末が使用できない状態のためメッセージが送信されませんでした。再試行してください。 |
| 3 | 受信者不在 - 永続的 | 該当番号はすでにアクティブではないため、データベースから削除する必要があります。 |
| 4 | 受信者によってブロックされた番号 | 永続的なエラーのため、該当番号を必ずデータベースから削除し、サービスプロバイダーに問い合わせてブロックを解除する必要があります。 |
| 5 | 番号ポータビリティエラー | 番号ポータビリティに関する問題がある場合は、サービスプロバイダーに問い合わせて解決する必要があります。 |
| 6 | スパム防止フィルターによるブロック | メッセージがサービスプロバイダーのスパム防止フィルターによってブロックされました。 |
| 7 | 端末使用中 | メッセージ送信時に端末が使用できない状態です。再試行してください。 |
| 8 | ネットワークエラー | ネットワークエラーによりメッセージ送信に失敗しました。再試行してください。 |
| 9 | 無効な番号 | 受信者が特定のサービスからのメッセージの受信拒否を明示的に要求した場合。 |
| 11 | ルーティング不可 | NHN Cloudでメッセージ送信のための適切なルートが見つかりませんでした。カスタマーサポートにお問い合わせください。 |
| 12 | 接続不可能な宛先 | 該当番号への経路が見つかりません。受信者番号を確認してください。 |
| 13 | 受信者の年齢制限 | 受信者の年齢制限によりメッセージを受信できません。 |
| 14 | サービスプロバイダーによってブロックされた番号 | 受信者の料金プランでSMSサービスを利用できるよう、サービスプロバイダーに問い合わせる必要があります。 |
| 16 | ゲートウェイクォータ超過 | 期間あたりの許可されたリクエスト回数を超過したためメッセージ送信に失敗しました。このエラーは、米国とフランスに登録されたアカウントにのみ適用されます。 |
| 20 | 不正行為防止トラフィックルール | メッセージがトラフィックパンピングにより拒否されました。カスタマーサポートにお問い合わせください。 |
| 21 | 異常な連続発信の検出 | 高密度の受信番号範囲のしきい値を超過しました。 |
| 22 | 異常なトラフィック急増の検出 | 相対的な増加のしきい値を超過しました。 |
| 39 | 宛先が米国の無効な発信者アドレス | 発信番号の問題により、米国へのメッセージ送信に失敗しました。カスタマーサポートにお問い合わせください。 |
| 51 | ヘッダーフィルター | 発信番号の問題により、米国へのメッセージ送信に失敗しました。カスタマーサポートにお問い合わせください。 |
| 53 | 同意フィルター | 同意がないためメッセージ送信に失敗しました。 |
| 54 | 規制エラー | 予期しない規制関連のエラーが発生しました。カスタマーサポートにお問い合わせください。 |
| 99 | 一般エラー | 一般的にルートエラーを意味します。カスタマーサポートにお問い合わせください。 |
| 1000 | その他のエラー | その他のエラー |

<a id="query-delivery-codes"></a>
## 結果照会コード { #query-delivery-codes }
<a id="query-delivery-codes-result-code-of-receiving"></a>
### 受信結果照会コード { #query-delivery-codes-result-code-of-receiving }

| コード値 | 意味 | 
| - | - |
| MTR1 | 成功 | 
| MTR2 | 失敗 | 

<a id="detail-result-code-of-receiving"></a>
### 受信結果照会詳細コード { #detail-result-code-of-receiving }

| コード値 | 意味 | 
| - | - |
| MTR2_1 | バリデーション失敗 | 
| MTR2_2 | サービスプロバイダーの問題 | 
| MTR2_3 | 端末の問題 |