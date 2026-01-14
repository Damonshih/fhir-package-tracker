# 🏥 基於 Arduino UNO R4 WiFi 之醫療包裹 FHIR 追蹤系統
> **2025 大健康產業創新創業競賽 - 決賽作品**

本專案是一個結合 **IoT 物聯網** 與 **FHIR 醫療資訊標準** 的智慧物流追蹤系統。透過 Arduino UNO R4 WiFi 連接 QR Code 掃描器，將醫療包裹的運送狀態即時上傳至 FHIR 伺服器，並透過 GitHub Pages 前端網頁進行視覺化監控。解決了傳統醫療物流資訊不透明、缺乏標準化格式的問題。

## 🌟 專案特色 (Features)
- **標準化資料傳輸**：採用 HL7 FHIR (Fast Healthcare Interoperability Resources) 標準格式 (JSON)，確保與醫院 HIS 系統的相容性。
- **即時物聯網追蹤**：使用 Arduino UNO R4 WiFi 進行 HTTPS 加密連線，直接將掃描數據上傳至雲端。
- **直觀視覺回饋**：
  - **硬體端**：Arduino LED 矩陣顯示即時狀態（綠色勾勾 ✅ 代表上傳成功、紅色叉叉 ❌ 代表失敗）。
  - **網頁端**：前端網頁透過進度條 (Progress Bar) 即時顯示包裹目前位置（如：轉運站 A、轉運站 B、藥局）。
- **四階段物流模擬**：內建狀態機邏輯，模擬包裹從出貨到送達的完整歷程。

---

## 🛠️ 開發環境與硬體架構 (Environment & Hardware)

### 1. 硬體設備
- **微控制器**：Arduino UNO R4 WiFi (內建 ESP32 模組，支援 WiFi/Bluetooth)
- **掃描模組**：QR Code / Barcode Scanner (透過 UART Serial 通訊)
- **顯示介面**：Arduino R4 內建 12x8 LED Matrix

### 2. 軟體與服務
- **開發工具**：Arduino IDE (C++), Visual Studio Code
- **後端資料庫**：HAPI FHIR Public Test Server (R4版本)
- **前端託管**：GitHub Pages (HTML/CSS/JavaScript)
- **通訊協定**：HTTPS (SSL/TLS), RESTful API (POST/GET)

### 3. 資料格式 (Data Format)
本系統使用標準 **FHIR JSON** 格式進行傳輸，範例 payload 如下：
```json
{
  "resourceType": "Observation",
  "status": "final",
  "code": {
    "coding": [{
      "system": "http://loinc.org",
      "code": "PACK-TRACK",
      "display": "Medical Package Tracking"
    }]
  },
  "valueString": "Station A"
}
```

---

## 🚀 操作方式 (How to Use)

### 硬體端操作
1. **上電啟動**：接上電源，等待 Arduino 連線至預設 WiFi（LED 矩陣顯示連線動畫）。
2. **掃描包裹**：將 QR Code 對準掃描器。
3. **狀態循環**：系統設定為 4 階段循環，請依序掃描以觸發不同地點狀態：
   - **第 1 次掃描**：`Warehouse` (出貨倉庫)
   - **第 2 次掃描**：`Station A` (轉運站 A)
   - **第 3 次掃描**：`Station B` (轉運站 B)
   - **第 4 次掃描**：`Pharmacy` (抵達藥局 - 完成)
4. **確認回饋**：
   - 若上傳成功：LED 矩陣顯示 **綠色勾勾**。
   - 若連線失敗：LED 矩陣顯示 **紅色叉叉**，請檢查網路熱點。

### 網頁端監控
1. 開啟下方的 Demo 連結。
2. 網頁會自動每秒向 FHIR Server 發送 GET 請求。
3. 當硬體掃描成功後，網頁上的進度條會自動變色並更新當前位置文字。

---

## 🔗 Demo 連結與資源 
[![HackMD](https://img.shields.io/badge/HackMD-競賽專題文件-blue?logo=hackmd)](https://hackmd.io/@8SqntYZfROaRXjgqLSj8Dg/SJ5VZqLfWl)
[![HackMD](https://img.shields.io/badge/HackMD-競賽專題討論-blue?logo=hackmd)](https://hackmd.io/@8SqntYZfROaRXjgqLSj8Dg/BydT5c8zWx)
[![HackMD](https://img.shields.io/badge/HackMD-競賽專題開發日誌-blue?logo=hackmd)](https://hackmd.io/@8SqntYZfROaRXjgqLSj8Dg/SJS1oncZZx)

---

## 👨‍💻 作者 (Author)
**慈濟大學 醫學資訊學系 - 哈哈組**
- 負責項目：Arduino 韌體開發、FHIR 資料串接、硬體整合
- 聯絡方式：[114106107@gms.tcu.edu.tw]
