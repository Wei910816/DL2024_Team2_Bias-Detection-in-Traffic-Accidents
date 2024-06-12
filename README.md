# DL2024_Team2_Bias-Detection-in-Traffic-Accidents  
本專案主要在探討台北市的交通事故數據中是否存在偏見，例如針對某性別/車款特別詳細記錄事故資料，並識別出其中的偏見所在，目標是分析交通事故數據，確定是否存在任何形式的偏見。  
  
## 使用方法  
1. git clone這個專案  
  
 ` git clone https://github.com/ccudl2024/DL2024_Team2_Bias-Detection-in-Traffic-Accidents.git `  
  
2. 執行bias_detector.ipynb  
  
## 檔案說明：
1.data: 有105~109年台北市的交通事故數據，用於預測bias，還有外送員欄位代碼對照表、道路交通事故調查報告來理解數據中代號的意思  
  
2.bias_detector.ipynb: 用於偵測資料集中的bias  
  
## 專案說明  
我們將提取105年-109年的資料集中欄位為「性別」、「年齡」、「車種」、「15事故類型及型態」 、「 22受傷程度」、「 Delivery_Type」和「7速限」，並創建一個空的 DataFrame df_combined，用來存儲合併後的數據，接著進行清理和轉換數據。完成後將features定義成模型的特徵變數，包括性別、年齡、車種、速限、Delivery_type和事故類型及型態，而y是目標變數，即受傷程度。設定favorable_value為 'high'，表示"無受傷" 是有利的結果，最後執行bias_scan函數。  
通過 bias_scan 函數，對數據進行偏差檢測，分別識別出在預測過程中可能存在的特權子集和非特權子集。其中特權子集指的是在預測有利結果中可能被過度預測的群體，而非特權子集則是可能被低估的群體。  

## License  
This repository is under [MIT License](LICENSE).
