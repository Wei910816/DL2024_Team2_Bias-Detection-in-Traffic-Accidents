# DL2024_Team2_Bias-Detection-in-Traffic-Accidents
目標：
本專案主要在探討台北市的交通事故數據中是否存在偏見，例如針對某性別/車款特別詳細記錄事故資料，並識別出其中的偏見所在，目標是分析交通事故數據，確定是否存在任何形式的偏見。

檔案說明：
data資料夾中有105~109年台北市的交通事故數據，還有外送員欄位代碼對照表來理解代碼代表哪間的外送員，跟道路交通事故調查報告表來理解其他欄位代碼分別代表甚麼。

使用方法：
我們將提取105年-109年的資料集中欄位為「性別」、「年齡」、「車種」、「15事故類型及型態」 、「 22受傷程度」、「 Delivery_Type」和「7速限」，並創建一個空的 DataFrame df_combined，用來存儲合併後的數據，接著進行清理和轉換數據，步驟如下：
1. 對"性別"欄位進行轉換，男性設為1，女性設為2，並移除空值。
2. 對"年齡"欄位進行分箱，將年齡劃分為三個區間：18歲以下、19至64歲和65歲以上，並移除空值。
3. 對"車種"欄位進行轉換，B03 設為1，C03 設為2，其他全部設為0，並移除空值。
4. 對"15事故類型及型態"欄位進行二值化處理，非空值設為1，空值設為0，並移除空值。
5. 對"22受傷程度"欄位進行轉換，設置不受傷為1，其餘為0。
6. 對"Delivery_Type"欄位進行轉換，將非外送員設為0，外送員設為1，並移除空白值。
7. 對"7速限"欄位進行轉換，設置0~30為0，40~50為1，其餘為2，並移除空值。

最後尋找bias時，我們將features定義成模型的特徵變數，包括性別、年齡、車種、速限、Delivery_type和事故類型及型態，而y是目標變數，即受傷程度。設定favorable_value為 'high'，表示"無受傷" 是有利的結果，最後執行bias_scan函數。
通過 bias_scan 函數，對數據進行偏差檢測，分別識別出在預測過程中可能存在的特權子集和非特權子集。其中特權子集指的是在預測有利結果中可能被過度預測的群體，而非特權子集則是可能被低估的群體。
