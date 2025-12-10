<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AIoT-AGV 戰術控制台</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', 'Microsoft JhengHei', sans-serif;
            background: linear-gradient(135deg, #0a1428 0%, #1a2332 50%, #0d2d4e 100%);
            color: #e0e0e0;
            line-height: 1.8;
            min-height: 100vh;
            overflow-x: hidden;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 60px 20px;
        }

        /* Header */
        .header {
            text-align: center;
            margin-bottom: 60px;
            animation: slideDown 0.8s ease-out;
        }

        @keyframes slideDown {
            from { opacity: 0; transform: translateY(-30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .header h1 {
            font-size: 3.5em;
            background: linear-gradient(135deg, #00d4ff, #0099ff, #6366f1);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 10px;
            font-weight: 800;
            letter-spacing: 2px;
        }

        .header .subtitle {
            font-size: 1.3em;
            color: #64b5f6;
            margin-bottom: 20px;
            font-weight: 500;
        }

        .header .description {
            font-size: 1.1em;
            color: #b0bec5;
            margin-bottom: 30px;
            max-width: 800px;
            margin-left: auto;
            margin-right: auto;
        }

        .link-button {
            display: inline-block;
            background: linear-gradient(135deg, #00d4ff, #0099ff);
            color: white;
            padding: 12px 30px;
            border-radius: 50px;
            text-decoration: none;
            font-weight: 600;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0, 212, 255, 0.3);
        }

        .link-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0, 212, 255, 0.5);
        }

        /* Section */
        .section {
            margin-bottom: 50px;
            animation: fadeIn 0.8s ease-out forwards;
            opacity: 0;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .section:nth-child(1) { animation-delay: 0.2s; }
        .section:nth-child(2) { animation-delay: 0.4s; }
        .section:nth-child(3) { animation-delay: 0.6s; }
        .section:nth-child(4) { animation-delay: 0.8s; }
        .section:nth-child(5) { animation-delay: 1s; }

        .section h2 {
            font-size: 2.2em;
            margin-bottom: 30px;
            padding-bottom: 15px;
            border-bottom: 3px solid;
            border-image: linear-gradient(90deg, #00d4ff, #6366f1) 1;
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .section h2 span {
            font-size: 1.2em;
        }

        /* Features Grid */
        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
        }

        .feature-card {
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(0, 212, 255, 0.3);
            border-radius: 15px;
            padding: 25px;
            transition: all 0.3s ease;
            backdrop-filter: blur(10px);
        }

        .feature-card:hover {
            transform: translateY(-5px);
            border-color: rgba(0, 212, 255, 0.8);
            background: rgba(0, 212, 255, 0.1);
            box-shadow: 0 10px 30px rgba(0, 212, 255, 0.2);
        }

        .feature-card h3 {
            font-size: 1.3em;
            color: #00d4ff;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .feature-card p {
            color: #b0bec5;
            font-size: 0.95em;
            line-height: 1.7;
        }

        /* Tech Stack */
        .tech-stack {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
        }

        .tech-item {
            background: linear-gradient(135deg, rgba(0, 212, 255, 0.15), rgba(99, 102, 241, 0.15));
            border-left: 4px solid #00d4ff;
            padding: 20px;
            border-radius: 10px;
            transition: all 0.3s ease;
        }

        .tech-item:hover {
            transform: translateX(5px);
            border-left-color: #6366f1;
        }

        .tech-item strong {
            color: #00d4ff;
        }

        .tech-item p {
            color: #b0bec5;
            margin-top: 8px;
        }

        /* Operation Guide */
        .operation-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.3);
        }

        .operation-table thead {
            background: linear-gradient(90deg, rgba(0, 212, 255, 0.2), rgba(99, 102, 241, 0.2));
        }

        .operation-table th {
            padding: 18px;
            text-align: left;
            color: #00d4ff;
            font-weight: 600;
            border-bottom: 2px solid rgba(0, 212, 255, 0.5);
        }

        .operation-table td {
            padding: 15px 18px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            color: #b0bec5;
        }

        .operation-table tr:hover {
            background: rgba(0, 212, 255, 0.08);
        }

        .operation-table tbody tr:last-child td {
            border-bottom: none;
        }

        /* Quick Start */
        .step-item {
            background: rgba(255, 255, 255, 0.05);
            border-left: 4px solid #6366f1;
            padding: 20px;
            margin-bottom: 15px;
            border-radius: 8px;
            transition: all 0.3s ease;
        }

        .step-item:hover {
            background: rgba(99, 102, 241, 0.15);
        }

        .step-item h4 {
            color: #6366f1;
            margin-bottom: 10px;
            font-size: 1.1em;
        }

        .code-block {
            background: #0a1428;
            border: 1px solid rgba(0, 212, 255, 0.3);
            border-radius: 8px;
            padding: 15px;
            overflow-x: auto;
            margin-top: 10px;
            font-family: 'Courier New', monospace;
            font-size: 0.9em;
            color: #00d4ff;
            line-height: 1.5;
        }

        /* Roadmap */
        .roadmap-item {
            padding-left: 40px;
            position: relative;
            margin-bottom: 25px;
            color: #b0bec5;
        }

        .roadmap-item:before {
            content: '▶';
            position: absolute;
            left: 0;
            color: #00d4ff;
            font-weight: bold;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { color: #00d4ff; }
            50% { color: #6366f1; }
        }

        .roadmap-item strong {
            color: #00d4ff;
        }

        /* Footer */
        .footer {
            text-align: center;
            margin-top: 80px;
            padding-top: 40px;
            border-top: 2px solid rgba(0, 212, 255, 0.3);
            color: #64b5f6;
        }

        .footer p {
            margin: 10px 0;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .header h1 {
                font-size: 2.5em;
            }

            .section h2 {
                font-size: 1.8em;
            }

            .features-grid {
                grid-template-columns: 1fr;
            }

            .tech-stack {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header -->
        <div class="header">
            <h1>🌐 AIoT-AGV<br>戰術控制台</h1>
            <p class="subtitle">🎮 工業級多 AGV 協同調度系統</p>
            <p class="description">
                一個用於模擬真實工業環境中多台自動導引車（AGV）協同工作的網頁應用。
                展示戰術地圖、即時監控、任務調度與障礙物編輯，演示調度算法與路徑規劃能力。
            </p>
            <a href="https://aiot-agv.yay.boo/" class="link-button" target="_blank">🚀 進入控制台</a>
        </div>

        <!-- Core Concepts -->
        <div class="section">
            <h2><span>🚀</span> 核心概念</h2>
            <div class="features-grid">
                <div class="feature-card">
                    <h3>🤝 多AGV協同</h3>
                    <p>同時模擬物流型與巡檢型 AGV，支援多機協作與任務分配</p>
                </div>
                <div class="feature-card">
                    <h3>⚡ 真實物理模擬</h3>
                    <p>電量、溫度、載重、速度、故障等多維度環境模擬</p>
                </div>
                <div class="feature-card">
                    <h3>🏭 可編輯工廠佈局</h3>
                    <p>戰術地圖動態增刪障礙物，靈活配置工廠環境</p>
                </div>
                <div class="feature-card">
                    <h3>🧭 任務調度優化</h3>
                    <p>支援手動與自動路線生成，智能路徑規劃</p>
                </div>
                <div class="feature-card">
                    <h3>📊 視覺化監控</h3>
                    <p>Canvas 即時渲染 + 數據面板 + 日誌系統</p>
                </div>
            </div>
        </div>

        <!-- Features -->
        <div class="section">
            <h2><span>✨</span> 功能亮點</h2>
            <div class="features-grid">
                <div class="feature-card">
                    <h3>🔹 多AGV控制系統</h3>
                    <p>
                        支援多台 AGV（物流型、巡檢型）<br>
                        <strong>獨立狀態：</strong> IDLE | MOVING | PAUSED | ESTOP | CHARGING | ERROR<br>
                        每台車獨立任務隊列與參數配置
                    </p>
                </div>
                <div class="feature-card">
                    <h3>🔹 真實模擬系統</h3>
                    <p>
                        ✓ 電量管理（耗電、充電、低電量保護）<br>
                        ✓ 物理模擬（速度、轉向、避障）<br>
                        ✓ 故障模擬（感測器雜訊、網路延遲、馬達過熱）<br>
                        ✓ 環境互動（載重影響、溫度、路徑阻塞）
                    </p>
                </div>
                <div class="feature-card">
                    <h3>🔹 障礙物編輯系統</h3>
                    <p>
                        右鍵地圖新增障礙物，點擊刪除<br>
                        <strong>類型：</strong> RACK | WORKSTATION | PILLAR | MACHINE<br>
                        一鍵載入工廠佈局
                    </p>
                </div>
                <div class="feature-card">
                    <h3>🔹 任務調度系統</h3>
                    <p>
                        ✓ 任務隊列（上限 20 個）<br>
                        ✓ 巡邏路徑生成<br>
                        ✓ 智能路徑優化（手動 / 自動）
                    </p>
                </div>
                <div class="feature-card">
                    <h3>🔹 視覺化與監控</h3>
                    <p>
                        ✓ HTML5 Canvas 即時渲染（動態網格、縮放）<br>
                        ✓ 側欄數據面板<br>
                        ✓ 事件日誌系統
                    </p>
                </div>
            </div>
        </div>

        <!-- Tech Stack -->
        <div class="section">
            <h2><span>🛠</span> 技術棧</h2>
            <div class="tech-stack">
                <div class="tech-item">
                    <strong>💻 前端</strong>
                    <p>HTML5 / CSS3 / JavaScript</p>
                </div>
                <div class="tech-item">
                    <strong>🎨 渲染</strong>
                    <p>Canvas 2D API</p>
                </div>
                <div class="tech-item">
                    <strong>⚙️ 狀態管理</strong>
                    <p>自定義狀態機 + 事件系統</p>
                </div>
                <div class="tech-item">
                    <strong>🧮 物理模擬</strong>
                    <p>速度、角速度、碰撞</p>
                </div>
                <div class="tech-item">
                    <strong>🖼 UI 框架</strong>
                    <p>CSS Grid / Flexbox + 漸層動畫</p>
                </div>
            </div>
        </div>

        <!-- Quick Start -->
        <div class="section">
            <h2><span>🎮</span> 快速開始</h2>
            
            <div class="step-item">
                <h4>1️⃣ 克隆專案</h4>
                <div class="code-block">
git clone https://github.com/yourusername/agv-control-console.git<br>
cd agv-control-console
                </div>
            </div>

            <div class="step-item">
                <h4>2️⃣ 啟動伺服器</h4>
                <div class="code-block">
# Python 方案<br>
python -m http.server 8000<br>
<br>
# 或 Node.js 方案<br>
npx serve .
                </div>
            </div>

            <div class="step-item">
                <h4>3️⃣ 打開瀏覽器</h4>
                <div class="code-block">
http://localhost:8000
                </div>
            </div>
        </div>

        <!-- Operation Guide -->
        <div class="section">
            <h2><span>🧭</span> 操作指南</h2>
            <table class="operation-table">
                <thead>
                    <tr>
                        <th>操作</th>
                        <th>描述</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>🟢 <strong>選擇 AGV</strong></td>
                        <td>點擊左側 AGV 卡片</td>
                    </tr>
                    <tr>
                        <td>🟡 <strong>直接導航</strong></td>
                        <td>左鍵點擊地圖目標位置</td>
                    </tr>
                    <tr>
                        <td>🟡 <strong>加入任務隊列</strong></td>
                        <td>Ctrl + 左鍵點擊目標位置</td>
                    </tr>
                    <tr>
                        <td>🔴 <strong>添加障礙物</strong></td>
                        <td>右鍵點擊地圖</td>
                    </tr>
                    <tr>
                        <td>🟠 <strong>刪除障礙物</strong></td>
                        <td>點擊選取後按 Delete</td>
                    </tr>
                    <tr>
                        <td>🔵 <strong>任務管理</strong></td>
                        <td>在任務分頁管理隊列、啟動連續任務模式</td>
                    </tr>
                    <tr>
                        <td>🟣 <strong>監控面板</strong></td>
                        <td>查看電量、溫度、任務狀態與日誌</td>
                    </tr>
                </tbody>
            </table>
        </div>

        <!-- Roadmap -->
        <div class="section">
            <h2><span>🔮</span> 未來 Roadmap</h2>
            <div class="roadmap-item">
                <strong>🚗 多AGV編隊</strong> — 編隊行駛與任務分配
            </div>
            <div class="roadmap-item">
                <strong>🧠 進階路徑規劃</strong> — A* 與動態重規劃、預測性避障
            </div>
            <div class="roadmap-item">
                <strong>🌐 即時通訊</strong> — WebSocket / MQTT 即時通訊
            </div>
            <div class="roadmap-item">
                <strong>📦 數據持久化</strong> — IndexedDB 儲存、報表與預測性維護
            </div>
            <div class="roadmap-item">
                <strong>🕶 3D 與 XR</strong> — WebGL 3D 與 VR/AR 支援
            </div>
            <div class="roadmap-item">
                <strong>⚛️ 現代化重構</strong> — Vue/React + TypeScript 重構
            </div>
        </div>

        <!-- Footer -->
        <div class="footer">
            <p>📄 本專案採用 <strong>MIT License</strong></p>
            <p style="font-size: 0.9em; margin-top: 20px; color: #505050;">
                © 2024 AIoT-AGV Project | 工業級多AGV協同調度系統
            </p>
        </div>
    </div>
</body>
</html>
