# AIoT-AGV
AIoT AGV 戰術控制台 - 工業級多AGV協同調度系統
🚀 項目概述
這是一個用於模擬真實工業環境中多台自動導引車（AGV）協同工作的網頁應用。系統提供直觀的戰術地圖、實時監控、任務調度和障礙物編輯等功能，旨在展示AGV系統的調度算法和路徑規劃能力。

✨ 核心功能
1. 多AGV控制系統
同時控制兩台不同類型AGV（物流型、巡檢型）

獨立狀態管理：IDLE, MOVING, PAUSED, ESTOP, CHARGING, ERROR

獨立任務隊列和參數配置

2. 真實模擬系統
電量管理：電量消耗、自動充電、低電量保護

物理模擬：速度控制、轉向計算、障礙物避讓

故障模擬：感測器雜訊、網路延遲、馬達過熱

環境互動：載重影響、溫度監控、路徑阻塞

3. 障礙物編輯系統
右鍵點擊地圖添加障礙物

點擊選擇、Delete鍵刪除障礙物

多種障礙物類型：RACK, WORKSTATION, PILLAR, MACHINE

工廠佈局一鍵載入

4. 任務調度系統
任務隊列管理（最大20個任務）

連續任務模式、巡邏路徑生成

智能路線優化算法

手動/自動任務生成

5. 視覺化界面
HTML5 Canvas實時渲染

動態網格系統、縮放控制

實時數據監控面板

日誌系統和事件記錄

🛠️ 技術棧
前端框架：原生HTML5/CSS3/JavaScript

圖形渲染：HTML5 Canvas 2D API

狀態管理：自定義狀態機和事件系統

物理引擎：自實現AGV物理計算模型

UI/UX：CSS Grid/Flexbox、漸變效果、動畫

📁 項目結構
text
AGV-Control-Console/
├── index.html              # 主HTML文件（包含CSS和JS）
├── README.md               # 項目說明文件
├── LICENSE                 # 開源許可證
├── .gitignore              # Git忽略文件
└── assets/                 # 靜態資源（可選）
    ├── images/             # 圖片資源
    └── docs/               # 文檔資料
🎮 快速開始
1. 本地運行
bash
# 克隆項目
git clone https://github.com/yourusername/agv-control-console.git

# 進入項目目錄
cd agv-control-console

# 直接打開index.html或在本地服務器運行
# 使用Python簡單服務器
python -m http.server 8000
# 或使用Node.js
npx serve .
2. 使用說明
選擇AGV：點擊左側AGV卡片選擇要控制的車輛

設定目標：

左鍵點擊地圖：直接導航

Ctrl+左鍵：添加到任務隊列

右鍵：添加障礙物

任務管理：

使用任務分頁管理任務隊列

啟動連續任務模式自動運行

障礙物編輯：

切換到障礙物分頁

右鍵添加，點擊選擇，Delete鍵刪除

監控系統：

右側面板查看實時數據

事件日誌跟蹤系統活動

🔧 開發指南
架構設計
text
┌─────────────────────────────────────┐
│           UI 渲染層 (View)          │
├─────────────────────────────────────┤
│      控制層 (Controller)            │
│  ┌─────────────────────────────┐    │
│  │  事件處理  │ 用戶交互      │    │
│  └─────────────────────────────┘    │
├─────────────────────────────────────┤
│      模型層 (Model)                  │
│  ┌─────────────────────────────┐    │
│  │  AGV狀態  │ 任務隊列       │    │
│  │ 障礙物數據│ 系統配置       │    │
│  └─────────────────────────────┘    │
├─────────────────────────────────────┤
│      物理引擎層 (Physics)            │
│  ┌─────────────────────────────┐    │
│  │ 移動計算 │ 碰撞檢測        │    │
│  │ 感測器模擬│ 路徑規劃       │    │
│  └─────────────────────────────┘    │
└─────────────────────────────────────┘
主要模塊
AGV物理計算 (updateAGVPhysics)

速度計算、轉向控制

障礙物檢測和避讓

電量消耗和溫度計算

任務調度系統 (taskQueues)

隊列管理

任務執行順序

自動任務生成

障礙物管理 (obstacles)

障礙物添加/刪除

碰撞檢測

視覺化渲染

事件系統 (addEvent, addLog)

系統日誌記錄

實時事件通知

故障模擬和恢復

⚙️ 配置參數
系統配置 (CONFIG)
javascript
{
  TARGET_THRESHOLD: 3.0,        // 目標到達閾值
  MIN_SPEED: 0.5,               // 最小移動速度
  MAX_SPEED: 10.0,              // 最大移動速度
  BATTERY_DRAIN_RATE: 0.002,    // 電量消耗率
  COLLISION_RADIUS: 30,         // 碰撞檢測半徑
  CHARGING_RATE: 0.5,           // 充電速度
  REALISM_MODE: true,           // 真實模擬模式
  TASK_QUEUE_LIMIT: 20          // 任務隊列限制
}
AGV配置
每個AGV有獨立的配置，包括：

最大速度、電量、顏色

載重、效率值

感測器參數（溫度、電流等）

🧪 測試功能
真實模擬測試
故障模擬：

javascript
simulateRealFault()      // 模擬隨機故障
simulateNetworkDelay()   // 模擬網路延遲
simulateSensorNoise()    // 模擬感測器雜訊
系統診斷：

javascript
runDiagnostics()         // 執行系統診斷
optimizeFleetRoutes()    // 優化路線
環境測試：

javascript
generateRandomObstacles()  // 生成隨機障礙物
loadFactoryLayout()        // 載入工廠佈局
📊 數據流
text
用戶交互 → 事件處理 → 狀態更新 → 物理計算 → 視覺化渲染
    ↓          ↓          ↓          ↓           ↓
任務指令   控制命令    AGV狀態   位置更新    Canvas繪製
    ↓          ↓          ↓          ↓           ↓
任務隊列   系統配置   感測器數據 碰撞檢測    UI更新
🎯 性能優化
1. 渲染優化
使用requestAnimationFrame進行動畫渲染

Canvas分層渲染（網格、障礙物、AGV分開）

軌跡點數限制防止內存泄漏

2. 計算優化
增量式物理計算

四叉樹碰撞檢測（可擴展）

事件節流和防抖

3. 內存管理
定期清理歷史數據

對象池重用

事件監聽器正確移除

🔮 未來擴展
計劃功能
多AGV協同：

編隊行駛

任務分配算法

衝突解決協議

高級路徑規劃：

A*算法優化

動態路徑重規劃

預測性避障

遠程控制：

WebSocket實時通訊

REST API接口

MQTT協議支持

數據分析：

運行統計報表

性能分析工具

預測性維護

3D可視化：

WebGL三維渲染

虛擬現實(VR)支持

增強現實(AR)預覽

技術升級
移植到Vue.js/React框架

使用TypeScript重構

Web Workers後台計算

IndexedDB數據持久化

🤝 貢獻指南
代碼規範
命名約定：

變數：camelCase

函數：camelCase

常量：UPPER_SNAKE_CASE

類別：PascalCase

代碼結構：

javascript
// 模塊導入

// 常量定義

// 全局變數

// 函數定義（按功能分組）

// 事件監聽器

// 初始化代碼
文檔要求：

函數使用JSDoc註釋

複雜邏輯添加說明註釋

API接口文檔

開發流程
Fork項目

創建功能分支 (git checkout -b feature/AmazingFeature)

提交更改 (git commit -m 'Add some AmazingFeature')

推送到分支 (git push origin feature/AmazingFeature)

開啟Pull Request

📝 版本歷史
v1.0.0 (基礎版)
基礎AGV移動功能

簡單任務系統

基本UI界面

v2.0.0 (增強版)
多AGV支持

任務隊列系統

障礙物檢測

v3.0.0 (當前版本)
真實物理模擬

障礙物編輯系統

高級故障模擬

專業工業界面

📄 許可證
本項目採用 MIT 許可證 - 詳見 LICENSE 文件
