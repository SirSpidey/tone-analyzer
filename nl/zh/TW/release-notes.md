---

copyright:
  years: 2015, 2017
lastupdated: "2017-09-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 版本注意事項

下列各節記載了 {{site.data.keyword.toneanalyzershort}} 服務的每一個版本所包含的新增特性及變更。變更不會岔斷現有的程式碼。
{: shortdesc}

> **附註：**版本注意事項現在會記載每次更新的*服務版本* 及*介面版本*。請以 `version` 查詢參數指定*介面版本*，才能使用該更新所提供的新增特性及功能。服務會使用 `X-Service-Api-Version` 回應標頭來傳回這兩個版本。

## 2017 年 9 月 28
{: #September2017b}

**服務版本：**`3.4.1`<br/> **介面版本：**`2017-09-21`

-   個別 {{site.data.keyword.Bluemix_notm}} 使用者名稱可提交之要求數上限的節流控制限制已增加為每分鐘 1200 個要求。如果使用者超出限制，則服務會傳回 HTTP 回應碼 429 *要求太多*。

## 2017 年 9 月 25 日
{: #September2017a}

**服務版本：**`3.4.1`<br/> **介面版本：**`2017-09-21`

-   一般用途端點（`/v3/tone` 方法）變更如下：

    -   除了英文之外，還支援法文 (`fr`) 輸入內容。
    -   不再傳回社交語氣。
    -   不再與情緒語氣一起傳回 `disgust`。
    -   省略其評分小於 `0.5` 的任何語氣。此資格符合 `/v3/tone_chat` 方法的回應。
    - 不再傳回語氣種類（`tone_categories` 欄位）作為其輸出的一部分。其值符合限定臨界值的所有語氣都會傳回作為單一 `tones` 物件的一部分。與之前一樣，預設一律會針對完整文件及每個個別句子傳回語氣。
    - 不再接受 `tones` 查詢參數，無法將輸出限制為指定的語氣。系統會針對每個要求傳回所有限定語氣。在要求中包含參數並不會造成錯誤，但它對回應沒有影響。
    - 不再針對個別句子傳回 `input_from` 及 `input_to` 欄位。除了其分析結果之外，此方法現在只會傳回 ID 及每一個句子的文字。

-   現在，服務會在下列情況下針對部分正確的輸入傳回 HTTP 回應碼 200（而非 400）：

    -   若為 `/v3/tone` 方法，如果您提交超過 128 KB 或 1000 個句子的輸入內容，則服務會傳回 `warning` 欄位作為其回應的一部分。服務會針對文件層次的分析分析前 1000 個句子，就像它目前只會針對句子層次的分析分析前 100 個句子。如果您超出任一限制，舊版的服務會針對要求傳回回應碼 400。請注意，服務現在會分析少於三個單字的句子。
    -   若為 `/v3/tone_chat` 方法，如果您提交超過 50 個陳述，則服務會在回應的 `utterances_tone` 層次，針對整體內容傳回 `warning` 欄位；它只會分析前 50 個陳述。如果您提交包含超過 500 個字元的單一陳述，則服務會針對該陳述傳回 `error` 欄位，而不分析此陳述。如果您超出任一限制，舊版的服務會傳回回應碼 400。請注意，如果輸入的所有陳述都超過 500 個字元，則服務仍會針對要求傳回回應碼 400。

-   服務現在會對它從單一使用者接受的要求數進行節流控制。如果服務每分鐘從個別 {{site.data.keyword.Bluemix_notm}} 使用者名稱收到超過 600 個要求，則服務會傳回 HTTP 回應碼 429 *要求太多*。

-   下列變更同時適用於一般用途端點及客戶參與端點：

    -   以 `version` 參數指定的介面版本是 `2017-09-21`，才能使用最新版本的服務。
    -   已更新文件來指出服務可以使用各種語言產生本地化輸出。請使用 `Accept-Language` 要求標頭來指定所需的語言。

## 2017 年 7 月 6 日
{: #July2017b}

**服務版本：**`3.3.6`<br/> **介面版本：**`2016-05-19`

服務已針對客戶參與端點的小型問題報告修正程式進行更新。

## 較舊版本

-   [2017 年 7 月 1 日](#July2017a)
-   [2017 年 5 月 8 日](#May2017)
-   [2017 年 4 月 17 日](#April2017)
-   [2017 年 3 月 15 日](#March2017)
-   [2016 年 12 月 1 日](#December2016)
-   [2016 年 10 月 18 日](#October2016b)
-   [2016 年 10 月 3 日](#October2016a)
-   [2016 年 5 月 19 日](#May2016)

### 2017 年 7 月 1 日
{: #July2017a}

**服務版本：**`3.3.5`<br/> **介面版本：**`2016-05-19`

{{site.data.keyword.toneanalyzershort}} 服務的客戶參與端點現在已正式發行 (GA)。端點的所有呼叫目前都是以與一般用途端點呼叫相同的費率收費。

### 2017 年 5 月 8 日
{: #May2017}

**服務版本：**`3.3.4`<br/> **介面版本：**`2016-05-19`

IBM 已透過進一步擴充訓練資料集來更新情緒語氣及客戶關懷參與語氣的評分模型。現在，模型對基準性能測試資料集具有更高的精準度。

### 2017 年 4 月 17 日
{: #April2017}

-   現在提供一組客戶參與領域特有的語氣：*frustrated*、*satisfied*、*excited*、*polite*、*impolite*、*sad* 及 *sympathetic*。服務會從客戶與客服人員之間的交談文字中偵測這些語氣。語氣目前是測試版功能。
-   IBM 已發行情緒語氣評分模型的更新，以改善情緒結果。

### 2017 年 3 月 15 日
{: #March2017}

IBM 已更新情緒語氣評分模式。訓練資料集已擴充。因此，現在模型對基準性能測試資料集具有更高的精準度。

### 2016 年 12 月 1 日
{: #December2016}

IBM 已更新文件情緒語氣評分。新模型會考量句子的情緒側寫來彙總文件評分。

### 2016 年 10 月 18 日
{: #October2016b}

IBM 已加強社交語氣。服務現在使用一個稱為 [GloVe ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://nlp.stanford.edu/projects/glove/){: new_window} 的開放程式碼單字內嵌技術，來推斷社交語氣評分。此變更可讓服務在計算社交語氣時涵蓋更大量的單字詞彙。如需如何推斷社交語氣的相關資訊，請參閱 {{site.data.keyword.personalityinsightsshort}} 服務的[服務背後的科學](http://www.ibm.com/watson/developercloud/doc/personality-insights/science.html)。

### 2016 年 10 月 3 日
{: #October2016a}

IBM 已加強型句子層次的情緒偵測。服務會使用新的訓練資料、新的特性選擇處理程序，以及單字、表情符號及俚語的擴增辭彙。這些變更會在句子層次產生不同但顯著改善的情緒評分。服務的 API 尚未變更。

### 2016 年 5 月 19 日
{: #May2016}

{{site.data.keyword.toneanalyzershort}} 服務的正式發行 (GA) 版本包含下列新增特性：

-   服務的模型使用改良的上下文敏感度來解譯語氣。模型目前使用的項目不只是詞彙記號。現在，他們會考量其他特性，例如標點符號、表情符號、語言參數（例如句子結構）及句子複雜性。
-   撰寫語氣模型已重新命名為語言語氣。
-   語言和情緒語氣模型現在會處理否定。
-   對於少於三個單字的句子，服務不再傳回回應。
-   服務現在有一個簡化及改良的[示範 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://tone-analyzer-demo.mybluemix.net){: new_window}。
