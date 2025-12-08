🌐 AIoT-AGV — 戰術控制台
🎮 工業級多 AGV 協同調度系統 一個用於模擬真實工業環境中多台自動導引車（AGV）協同工作的網頁應用。 展示戰術地圖、即時監控、任務調度與障礙物編輯，演示調度算法與路徑規劃能力。

🔗 官方網站入口

🚀 核心概念
✨ 多AGV協同 — 同時模擬物流型與巡檢型 AGV ⚡ 真實物理模擬 — 電量 / 溫度 / 載重 / 速度 / 故障 🏭 可編輯工廠佈局 — 戰術地圖增刪障礙物 🧭 任務調度與路徑優化 — 手動 / 自動生成路線 📊 視覺化監控 — Canvas 即時渲染 + 數據面板 + 日誌系統

✨ 功能亮點
🔹 多AGV控制系統
支援多台 AGV（物流型、巡檢型）

獨立狀態：IDLE | MOVING | PAUSED | ESTOP | CHARGING | ERROR

每台車獨立任務隊列與參數配置

🔹 真實模擬系統
電量管理（耗電、充電、低電量保護）

物理模擬（速度、轉向、避障）

故障模擬（感測器雜訊、網路延遲、馬達過熱）

環境互動（載重影響、溫度、路徑阻塞）

🔹 障礙物編輯系統
右鍵地圖新增障礙物，點擊刪除（Delete）

類型：RACK | WORKSTATION | PILLAR | MACHINE

一鍵載入工廠佈局

🔹 任務調度系統
任務隊列（上限 20 個）

巡邏路徑生成

智能路徑優化（手動 / 自動）

🔹 視覺化與監控
HTML5 Canvas 即時渲染（動態網格、縮放）

側欄數據面板 + 事件日誌

🛠 技術棧
💻 前端：HTML5 / CSS3 / JavaScript 🎨 渲染：Canvas 2D API ⚙️ 狀態管理：自定義狀態機 + 事件系統 🧮 物理模擬：速度、角速度、碰撞 🖼 UI：CSS Grid / Flexbox + 漸層動畫

🎮 快速開始
bash
# 克隆專案
git clone https://github.com/yourusername/agv-control-console.git
cd agv-control-console

# 啟動伺服器
python -m http.server 8000
# 或
npx serve .
👉 打開瀏覽器，進入 AIoT-AGV 戰術控制台

🧭 操作指南
🟢 選擇 AGV：點擊左側 AGV 卡片 🟡 設定目標：

左鍵 → 直接導航

Ctrl + 左鍵 → 加入任務隊列

右鍵 → 添加障礙物

🔵 任務管理：在任務分頁管理隊列，可啟動連續任務模式 🔴 障礙物編輯：右鍵新增、點擊選取、Delete 刪除 🟣 監控面板：查看電量、溫度、任務狀態與日誌

🔮 未來 Roadmap
🚗 多AGV編隊行駛與任務分配

🧠 A* 與動態重規劃、預測性避障

🌐 WebSocket / MQTT 即時通訊

📦 IndexedDB 儲存、報表與預測性維護

🕶 WebGL 3D 與 VR/AR 支援

⚛️ Vue/React + TypeScript 重構

📄 授權
📜 本專案採用 MIT License
