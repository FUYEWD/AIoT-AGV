AIoT-AGV — 戰術控制台
工業級多 AGV 協同調度的單頁式 Web 應用。以戰術地圖可視化模擬物流型與巡檢型 AGV 的路徑、任務與物理狀態，支援障礙物編輯與事件監控，用於展示調度算法與路徑規劃能力。

官方網站
AIoT-AGV — 戰術控制台

核心概念
多AGV協同： 同時模擬物流型與巡檢型 AGV，支援獨立狀態與任務隊列。

真實物理模擬： 電量、溫度、載重、速度與故障/雜訊模型。

可編輯工廠佈局： 在戰術地圖上增刪障礙物並載入預設佈局。

任務調度與路徑優化： 手動/自動生成任務，隊列管理與智能路徑。

視覺化監控： Canvas 實時渲染、數據面板、日誌與事件追蹤。

主要功能
多AGV控制系統

支援車種： 物流型、巡檢型

車輛狀態：

IDLE, MOVING, PAUSED, ESTOP, CHARGING, ERROR

獨立配置： 每台車具獨立任務隊列與參數

真實模擬系統

電量管理： 耗電、充電、低電量保護

運動學： 速度、轉向、避障

故障模擬： 感測器雜訊、網路延遲、馬達過熱

環境互動： 載重影響、溫度、路徑阻塞

障礙物編輯系統

快速編輯： 右鍵地圖新增障礙物、選取後可 Delete 刪除

類型支援： RACK, WORKSTATION, PILLAR, MACHINE

預設佈局： 一鍵載入工廠佈局

任務調度系統

隊列限制： 最多 20 個任務

路徑生成： 連續任務與巡邏路徑

路徑策略： 手動/自動切換的智能路徑優化

視覺化與監控

Canvas 渲染： 動態網格、平移縮放

監控面板： 電量、溫度、任務與事件日誌

技術棧
前端： 原生 HTML5 / CSS3 / JavaScript（單一 HTML 檔案）

渲染： HTML5 Canvas 2D API（分層）

狀態管理： 自定義狀態機與事件系統

物理： 自實作運動學、角速度、碰撞與雜訊模型

UI： CSS Grid / Flexbox、動畫與漸層

專案結構
單檔設計： 本專案目前以一個 index.html 提供所有功能，無外部框架與拆分模組。

擴充友善： 後續可將邏輯拆分至 renderer.js, physics.js, taskScheduler.js 等，但現階段維持單檔運作。

快速開始
本地開啟： 直接以瀏覽器打開 index.html。

靜態伺服器（選用）： 可使用任意簡易伺服器加速本地開發。

Python： python -m http.server 8000

Node.js： npx serve .

線上演示： https://aiot-agv.yay.boo/

操作說明
選擇 AGV： 點擊左側 AGV 卡片切換控制目標。

設定目標：

左鍵地圖： 直接導航到點位

Ctrl + 左鍵： 加入任務隊列

右鍵： 添加障礙物

任務管理： 於任務分頁管理隊列並可啟動連續任務模式。

障礙物編輯： 右鍵新增、點擊選取、Delete 刪除。

監控： 右側面板查看電量、溫度、任務狀態與事件日誌。

架構設計
UI 渲染層（View）： Canvas 與監控面板。

控制層（Controller）： 事件處理與交互控制。

模型層（Model）： AGV 狀態、任務、障礙物資料結構。

物理層（Physics）： 運動學、碰撞偵測、感測器雜訊。

主要模組與方法（單檔內邏輯）
updateAGVPhysics： 速度、轉向、避障與電量/溫度更新。

taskQueues： 任務入隊/出隊、優先權管理與自動生成。

obstacles： 障礙物 CRUD 與碰撞檢測。

eventLog： 系統事件記錄與警示。

faultSim： 感測器雜訊、網路延遲、馬達過熱等故障模擬。

系統配置（範例）
javascript
const CONFIG = {
  TARGET_THRESHOLD: 3.0,        // 目標到達閾值 (px)
  MIN_SPEED: 0.5,               // 最小移動速度
  MAX_SPEED: 10.0,              // 最大移動速度
  BATTERY_DRAIN_RATE: 0.002,    // 電量消耗率 (每幀)
  COLLISION_RADIUS: 30,         // 碰撞檢測半徑 (px)
  CHARGING_RATE: 0.5,           // 充電速度 (單位/秒)
  REALISM_MODE: true,           // 真實模擬模式
  TASK_QUEUE_LIMIT: 20          // 任務隊列限制
};
javascript
const AGV_TEMPLATE = {
  id: 'AGV-001',
  type: 'logistics',
  maxSpeed: 8.0,
  battery: 100.0,
  loadCapacity: 50, // kg
  sensors: { temp: 25, current: 0.5 }
};
測試與工具（單檔介面）
故障模擬： simulateRealFault(), simulateNetworkDelay(), simulateSensorNoise()

系統診斷： runDiagnostics()

路線優化： optimizeFleetRoutes()

環境測試： generateRandomObstacles(), loadFactoryLayout()

效能優化建議
渲染： 使用 requestAnimationFrame、Canvas 分層、限制軌跡點數量。

計算： 增量式物理更新、四叉樹碰撞偵測、事件節流。

記憶體： 物件池、定期清理歷史日誌、移除不必要監聽器。

未來擴展（Roadmap）
協同編隊： 多 AGV 編隊行駛與任務分配算法。

路徑規劃： A*、動態重規劃與預測性避障。

通訊： WebSocket / MQTT 實時通訊與 REST API。

儲存： IndexedDB、分析報表與預測性維護。

視覺化： WebGL 3D 與 VR/AR 支援。

工程化： 移植至 Vue/React、TypeScript 重構（保留單檔相容）。

貢獻指南
建立分支： git checkout -b feature/your-feature

提交規範： 使用明確 commit 訊息並 push 到遠端

提出 PR： 附上變更說明與測試方式

程式風格：

變數： camelCase

函數： camelCase

常數： UPPER_SNAKE_CASE

類別： PascalCase

註釋： 請使用 JSDoc 註解複雜函式，邏輯複雜處加入說明註釋。

版本歷史
v1.0.0： 基本 AGV 移動、單一任務系統與基礎 UI

v2.0.0： 多 AGV 支援、任務隊列與障礙物功能

v3.0.0： 真實物理模擬、障礙物編輯與高級故障模擬

授權
MIT License： 詳見 LICENSE（單檔版可於頁尾註明授權）。
