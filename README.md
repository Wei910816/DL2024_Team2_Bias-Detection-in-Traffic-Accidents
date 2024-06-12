# DL2024_Team2_Bias-Detection-in-Traffic-Accidents  
本專案主要在探討台北市的交通事故數據中是否存在偏見，例如針對某性別/車款特別詳細記錄事故資料，並識別出其中的偏見所在，目標是分析交通事故數據，確定是否存在任何形式的偏見。  
  
## 使用方法  
1. git clone這個專案  
  
 ` git clone https://github.com/ccudl2024/DL2024_Team2_Bias-Detection-in-Traffic-Accidents.git `  
  
2. 執行bias_detector.ipynb  
  
## 檔案說明：
1.data: 有105~109年台北市的交通事故數據，用於預測bias，還有外送員欄位代碼對照表、道路交通事故調查報告來理解數據中代號的意思  
  
2.bias_detector.ipynb: 用於偵測資料集中的bias  

## 資料集  
本資料集為公開資料集，能於data資料夾中下載，又或是前往[台北市交通局](https://www.dot.gov.taipei/)進行查閱  

## 模型  
我們參考[AIF360](https://github.com/Trusted-AI/AIF360/tree/main)中的demo_mdss_detector.ipynb

## 專案說明  
我們將提取105年-109年的資料集中欄位為「性別」、「年齡」、「車種」、「15事故類型及型態」 、「 22受傷程度」、「 Delivery_Type」和「7速限」，並創建一個空的 DataFrame df_combined，用來存儲合併後的數據，接著進行清理和轉換數據，具體如下:  
  
1. 對"性別"欄位進行轉換，男性設為1，女性設為2，並移除空值  
2. 對"年齡"欄位進行分箱，將年齡劃分為三個區間：18歲以下、19至64歲和65歲以上，並移除空值  
3. 對"車種"欄位進行轉換，B03 設為1，C03 設為2，其他全部設為0，並移除空值  
4. 對"15事故類型及型態"欄位進行二值化處理，非空值設為1，空值設為0，並移除空值  
5. 對"22受傷程度"欄位進行轉換，設置不受傷為1，其餘為0  
6. 對"Delivery_Type"欄位進行轉換，將非外送員設為0，外送員設為1，並移除空白值  
7. 對"7速限"欄位進行轉換，設置0~30為0，40-50為1，其餘為2，並移除空值  
  
完成後將features定義成模型的特徵變數，包括性別、年齡、車種、速限、Delivery_type和事故類型及型態，而y是目標變數，即受傷程度。設定favorable_value為 'high'，表示"無受傷" 是有利的結果，最後執行bias_scan函數。  
通過 bias_scan 函數，對數據進行偏差檢測，分別識別出在預測過程中可能存在的特權子集和非特權子集。其中特權子集指的是在預測有利結果中可能被過度預測的群體，而非特權子集則是可能被低估的群體。  

## License  
This repository is under [MIT License](LICENSE).
