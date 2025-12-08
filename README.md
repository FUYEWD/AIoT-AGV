# AIoT-AGV — 戰術控制台

**工業級多AGV協同調度系統**

> 一個用於模擬真實工業環境中多台自動導引車（AGV）協同工作的網頁應用。展示戰術地圖、實時監控、任務調度以及障礙物編輯等功能，便於演示調度算法與路徑規劃能力。

---

## 🚀 核心概念

* **多AGV協同**：同時模擬物流型與巡檢型 AGV，支援獨立狀態及任務隊列。
* **真實物理模擬**：電量/溫度/載重/速度等物理屬性模擬，並支援故障與感測器雜訊模擬。
* **可編輯工廠佈局**：在戰術地圖上增刪障礙物，並載入預設佈局。
* **任務調度與路徑優化**：手動或自動生成任務、隊列管理、智能路線優化。
* **視覺化監控**：Canvas 實時渲染、數據面板、日誌系統與事件追蹤。

---

## ✨ 主要功能

1. **多AGV控制系統**

   * 支援多台 AGV（例：物流型、巡檢型）
   * 每台車獨立狀態：`IDLE, MOVING, PAUSED, ESTOP, CHARGING, ERROR`
   * 獨立任務隊列與參數配置

2. **真實模擬系統**

   * 電量管理（耗電、充電、低電量保護）
   * 物理模擬（速度、轉向、避障）
   * 故障模擬（感測器雜訊、網路延遲、馬達過熱）
   * 環境互動（載重影響、溫度、路徑阻塞）

3. **障礙物編輯系統**

   * 右鍵地圖新增障礙物；點選刪除（`Delete`）
   * 支援多種類型：`RACK`, `WORKSTATION`, `PILLAR`, `MACHINE`
   * 一鍵載入工廠佈局

4. **任務調度系統**

   * 任務隊列（上限 20 個）
   * 連續任務 / 巡邏路徑生成
   * 智能路徑優化（可切換手動 / 自動生成）

5. **視覺化與監控**

   * HTML5 Canvas 實時渲染（動態網格、縮放）
   * 側欄實時數據面板、事件日誌

---

## 🛠️ 技術棧

* **前端**：原生 HTML5 / CSS3 / JavaScript
* **渲染**：HTML5 Canvas 2D API（Canvas 分層）
* **狀態管理**：自定義狀態機與事件系統
* **物理**：自實作 AGV 物理計算模型（速度、角速度、碰撞）
* **UI**：CSS Grid / Flexbox、動畫與漸層

---

## 📁 專案結構（建議）

```
AGV-Control-Console/
├── index.html
├── README.md
├── LICENSE
├── .gitignore
├── src/
│   ├── app.js
│   ├── renderer.js
│   ├── physics.js
│   ├── taskScheduler.js
│   └── obstacles.js
└── assets/
    ├── images/
    └── docs/
```

---

## 🎮 快速開始

**1. 克隆專案**

```bash
git clone https://github.com/yourusername/agv-control-console.git
cd agv-control-console
```

**2. 本地啟動（任一方式）**

```bash
# Python 內建簡易伺服器
python -m http.server 8000
# 或使用 Node.js 的 serve
npx serve .
```

**3. 操作說明（UI）**

* 選擇 AGV：點擊左側 AGV 卡片
* 設定目標：

  * 左鍵點擊地圖 → 直接導航
  * Ctrl + 左鍵 → 加入任務隊列
  * 右鍵 → 添加障礙物
* 任務管理：使用任務分頁管理任務隊列；可啟動連續任務模式
* 障礙物編輯：切換到障礙物分頁、右鍵新增、點擊選擇、`Delete` 刪除
* 監控：右側面板查看電量、溫度、任務狀態與日誌

---

## 🧭 架構設計（高階）

* UI 渲染層（View） — Canvas 與面板
* 控制層（Controller） — 事件處理、使用者互動
* 模型層（Model） — AGV 狀態、任務、障礙物
* 物理層（Physics） — 運動學、碰撞偵測、感測器模擬

---

## ⚙️ 主要模組說明

* **updateAGVPhysics**：速度計算、轉向、避障、電量/溫度更新
* **taskQueues**：任務入隊、出隊、優先權管理、自動生成任務
* **obstacles**：障礙物 CRUD、碰撞檢測
* **eventLog**：事件記錄、日誌與警示
* **faultSim**：模擬故障（sensor noise, network delay, motor overheating）

---

## 🔧 系統配置（範例）

```javascript
const CONFIG = {
  TARGET_THRESHOLD: 3.0,        // 目標到達閾值 (px)
  MIN_SPEED: 0.5,               // 最小移動速度
  MAX_SPEED: 10.0,              // 最大移動速度
  BATTERY_DRAIN_RATE: 0.002,    // 電量消耗率 (每幀)
  COLLISION_RADIUS: 30,         // 碰撞檢測半徑 (px)
  CHARGING_RATE: 0.5,           // 充電速度 (單位/秒)
  REALISM_MODE: true,           // 真實模擬模式開關
  TASK_QUEUE_LIMIT: 20          // 任務隊列限制
};
```

**AGV 設定（範例）**

```javascript
const AGV_TEMPLATE = {
  id: 'AGV-001',
  type: 'logistics',
  maxSpeed: 8.0,
  battery: 100.0,
  loadCapacity: 50, // kg
  sensors: { temp: 25, current: 0.5 }
};
```

---

## 🧪 測試與工具

* 故障模擬：`simulateRealFault()`, `simulateNetworkDelay()`, `simulateSensorNoise()`
* 系統診斷：`runDiagnostics()`
* 路線優化：`optimizeFleetRoutes()`
* 環境測試：`generateRandomObstacles()`, `loadFactoryLayout()`

---

## 🔍 效能優化建議

1. 渲染：`requestAnimationFrame`、Canvas 分層、限制軌跡點
2. 計算：增量式物理計算、四叉樹碰撞檢測、事件節流
3. 記憶體：物件池、定期清理歷史訊息、移除不必要監聽器

---

## 🔮 未來擴展（Roadmap）

* 多AGV編隊行駛與任務分配算法
* A* 與動態重規劃、預測性避障
* WebSocket / MQTT 實時通訊、REST API
* 後端儲存（IndexedDB）、分析報表與預測性維護
* 3D 可視化（WebGL）與 VR/AR 支援
* 移植至 Vue/React 與 TypeScript 重構

---

## 🤝 貢獻指南

1. Fork 專案並建立功能分支：`git checkout -b feature/your-feature`
2. 使用明確 commit 訊息並 push 到遠端
3. 開 PR 並附上變更說明與測試方式

**程式風格（建議）**

* 變數：`camelCase`
* 函數：`camelCase`
* 常數：`UPPER_SNAKE_CASE`
* 類別：`PascalCase`

請使用 JSDoc 註解複雜函式，且在邏輯複雜處加入說明註釋。

---

## 📝 版本歷史

* **v1.0.0** — 基本 AGV 移動、單一任務系統、基礎 UI
* **v2.0.0** — 多AGV 支援、任務隊列、障礙物功能
* **v3.0.0** — 真實物理模擬、障礙物編輯、高級故障模擬

---

## 📄 授權

本專案採用 **MIT License**。詳見 LICENSE 檔案。

---

## 聯絡

如有問題或想討論功能設計，歡迎開 issue 或 PR。

---

> 若希望我幫你把此 README 轉成 `index.html` 的專案首頁（含樣式與互動按鈕範例）、或改寫為英文版 README，我可以直接替你生成範本檔案。
