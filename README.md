# Power BI 與 MongoDB 整合

下載 Power BI Desktop

https://www.microsoft.com/zh-tw/power-platform/products/power-bi/desktop

下載 MongoDB BI Connector

https://www.mongodb.com/try/download/bi-connector

解壓後複製路徑

C:\Program Files\MongoDB\Connector for BI\2.14\bin 點空白的地方cmd

輸入 mongosqld 

<port-3307>

Microsoft Visual C++ 可轉散發套件的最新支援下載項目架構X64

https://learn.microsoft.com/zh-tw/cpp/windows/latest-supported-vc-redist?view=msvc-170

安裝 MySQL ODBC Driver（Mongo BI 使用 MySQL 協定) 安裝時選 64-bit 版本。

<port-3306>

https://dev.mysql.com/downloads/connector/odbc/

控制台\系統及安全性\Windows 工具\ODBC資料來源(64位元)\新增-ODBC-MySQL ODBC 9.3 Unicode Driver

BI-取得資料-其他-OBDC-MongoDBDSN

2. 啟動 MongoDB 服務（確保 MongoDB 正常執行）

MongoDB 預設 port 是 27017

打開 CMD 或 PowerShell，執行：

net start MongoDB

若使用手動方式啟動，請至 MongoDB 安裝資料夾執行：

mongod

3. 啟動 MongoDB BI Connector（SQL 轉譯器）
   
切換到 BI Connector bin 路徑，啟動服務：

cd "C:\Program Files\MongoDB\Connector for BI\2.14\bin"

mongosqld

--port=3307：MySQL 協定的 MongoDB 資料服務（Power BI 透過這連接）

4. 設定 ODBC 連線（讓 Power BI 看得到 MongoDB）
    
路徑：

控制台 → 系統及安全性 → Windows 工具 → ODBC 資料來源 (64 位元) → 點「新增」

選擇驅動程式：

選擇 MySQL ODBC 8.0 ANSI Driver（或 Unicode）

填入設定：

項目	設定值

Data Source Name	MongoDB_BI_ODBC

TCP/IP Server	localhost

Port	3307

User	無須填寫（可空）

Password	無須填寫（可空）

點擊「Test」→ 成功後按「OK」

5. Power BI 連接 MongoDB（透過 ODBC）

Power BI Desktop 操作：

開啟 Power BI Desktop

點選「取得資料」 → 「其他」 → 選「ODBC」

選擇剛剛建立的資料來源（MongoDB_BI_ODBC）

選擇你想要分析的 MongoDB 資料表（collections）

6. 儲存並建立視覺化報表

匯入資料後，你可以用：

資料檢視：進行資料欄位檢查、轉型（變數格式）

報表檢視：拖拉圖表元件、建立視覺化圖表

可使用「轉換資料」來清洗資料（Power Query）

完成後可儲存 .pbix 檔案作為專案

備註提醒

每次開 Power BI 前，必須先啟動 mongosqld

若資料來源變動，可在 Power BI 點「重新整理」

若需自動更新，建議用 Power BI Gateway + Power BI Service 部署
