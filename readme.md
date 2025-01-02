這段程式碼會從連結中下載food-11的壓縮檔 並將food-11.zip檔解壓縮至work檔中 解壓縮完成後再將壓縮檔刪除
![image](https://github.com/user-attachments/assets/c6b1ca48-e3f2-4a61-b1f3-b2f4c3baa2e8)
在影像預處理中，我們定義了一個名為 `preprocess` 的函數，
進行以下處理：統一將影像縮放至 128×128 像素，確保尺寸一致；對訓練資料隨機翻轉，以增強數據多樣性；將影像轉為 numpy 陣列並進行歸一化處理；最後調整數據形狀以適配 CNN 的輸入格式。
![image](https://github.com/user-attachments/assets/09d89333-f177-4bfc-81fd-184e4f83a293)
我們定義了一個名為 FoodDataSet 的自訂資料集類別，用於處理食物分類任務，並利用該類別建立了訓練和驗證（評估）用的資料載入器（DataLoader），以實現資料的高效讀取。
註：FoodDataSet 類別繼承自 paddle.io.Dataset，這是官方推薦的資料集類型，能夠直接與官方的訓練方法 fit() 結合使用。相關 API 文件可參考：Dataset。DataLoader 支援返回迭代器，並提供單進程與多進程的資料載入方式，特別適合大規模資料的高效處理。
![image](https://github.com/user-attachments/assets/508a54fe-8491-4f67-8505-4945c9413170)
我們構建了一個基於 LeNet() 的模型。LeNet 是由 Yann LeCun 等人在 1990 年代設計的經典捲積神經網路（CNN），最初用於手寫數字的識別（例如 MNIST 資料集）。在本範例中，LeNet 的結構經過修改，使其能夠適應包含 11 個類別的影像分類任務。本模型基於 PaddlePaddle 深度學習框架實現。

LeNet 模型包含以下部分：
卷積層（Convolutional Layers）

Conv0：第一層卷積，接收 3 通道（RGB 影像）輸入，輸出 10 通道，使用 5×5 的卷積核，步長為 1，並採用 SAME 填充保持特徵圖尺寸不變。
Conv1：第二層卷積，輸入 10 通道，輸出 20 通道，卷積核大小和步長與 Conv0 相同，使用 SAME 填充。
Conv2：第三層卷積，輸入 20 通道，輸出 50 通道，同樣使用 5×5 的卷積核和 SAME 填充。
池化層（Pooling Layers）
每個卷積層後緊接一個最大池化層（MaxPool2D），使用 2×2 的池化核和步長 2，縮小特徵圖尺寸，減少計算量，並提高模型的泛化能力。

全連接層（Fully Connected Layers）

FC1：將卷積層的輸出展平後，輸出特徵維度為 256。
FC2：輸入 256 維特徵，輸出 64 維特徵。
FC3：作為輸出層，輸入 64 維特徵，輸出對應 11 類的分類結果。
激活函數（Activation Functions）

在每個卷積層和前兩個全連接層後，應用 Leaky ReLU 激活函數引入非線性，提升模型表達能力。
在輸出層使用 Softmax 激活函數，將輸出轉換為機率分佈，用於多分類任務。
![image](https://github.com/user-attachments/assets/f0dec480-952c-4d18-a7ba-3936bf59a47b)
查看模型结构
![image](https://github.com/user-attachments/assets/b5319b55-69b4-4cfe-b390-9f7a8f64abf6)
模型訓練 如果發現運行時間較長，可以將epoch（訓練總輪次）降低，但這會導致訓練結果變差。
![image](https://github.com/user-attachments/assets/b14ccecf-f119-4388-97e4-c38d8cc32684)
在 work/food-11 目錄中新增一個 testing 資料夾，並隨機生成一些圖像，為後續的預測步驟提供測試資料。
![image](https://github.com/user-attachments/assets/0f7eed84-3626-4598-bac8-f4521d6084a4)
簡單地匯入一張圖，然後進行直覺測試
![image](https://github.com/user-attachments/assets/8d4101cc-00f4-43ee-a6cf-e23a5c0a9233)
以下為預測完的結果
![image](https://github.com/user-attachments/assets/e90164e9-03fc-46fc-9988-d572d959a9a2)










