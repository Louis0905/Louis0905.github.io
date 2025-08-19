<!DOCTYPE html>
<html lang="zh-Hant">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>GWall 4.0 網路安全解決方案｜企業級整合式防護平台</title>
<style>
  :root{
    --bg: linear-gradient(135deg, #0a0b1e 0%, #1a0b2e 35%, #16213e 100%);
    --panel: linear-gradient(145deg, rgba(15,25,45,0.9), rgba(25,35,55,0.8));
    --panel-border: linear-gradient(45deg, #00d4ff, #7c3aed, #00d4ff);
    --muted: #64748b;
    --text: #e2e8f0;
    --primary: #00d4ff;
    --primary-2: #0ea5e9;
    --accent: #10b981;
    --warn: #f59e0b;
    --critical: #ef4444;
    --glass: rgba(255,255,255,0.03);
    --glow: 0 0 20px rgba(0,212,255,0.3);
    --neon-blue: #00d4ff;
    --neon-purple: #7c3aed;
    --neon-green: #10b981;
  }
  
  * { box-sizing: border-box; }
  
  html, body { height: 100%; }
  
  body {
    margin: 0;
    font-family: 'JetBrains Mono', 'Cascadia Code', 'Fira Code', monospace, 'Noto Sans TC', system-ui;
    background: var(--bg);
    color: var(--text);
    overflow-x: hidden;
    position: relative;
    line-height: 1.6;
  }
  
  /* 背景科技網格 */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background: 
      radial-gradient(circle at 25% 25%, rgba(0,212,255,0.1) 0%, transparent 50%),
      radial-gradient(circle at 75% 75%, rgba(124,58,237,0.08) 0%, transparent 50%),
      linear-gradient(90deg, transparent 49%, rgba(0,212,255,0.03) 50%, transparent 51%),
      linear-gradient(0deg, transparent 49%, rgba(0,212,255,0.03) 50%, transparent 51%);
    background-size: 100% 100%, 100% 100%, 40px 40px, 40px 40px;
    pointer-events: none;
    animation: grid-pulse 4s ease-in-out infinite alternate;
  }
  
  @keyframes grid-pulse {
    0% { opacity: 0.3; }
    100% { opacity: 0.6; }
  }
  
  /* 浮動粒子效果 */
  .particles {
    position: fixed;
    inset: 0;
    pointer-events: none;
    z-index: 0;
  }
  
  .particle {
    position: absolute;
    width: 2px;
    height: 2px;
    background: var(--neon-blue);
    border-radius: 50%;
    animation: float 6s ease-in-out infinite;
    box-shadow: 0 0 10px var(--neon-blue);
  }
  
  @keyframes float {
    0%, 100% { transform: translateY(0px) rotate(0deg); opacity: 0; }
    50% { transform: translateY(-100px) rotate(180deg); opacity: 1; }
  }
  
  /* Header 科技感 */
  header {
    position: sticky;
    top: 0;
    z-index: 100;
    background: linear-gradient(135deg, 
      rgba(15,25,45,0.95) 0%, 
      rgba(25,35,55,0.9) 50%, 
      rgba(15,25,45,0.95) 100%);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid rgba(0,212,255,0.2);
    padding: 16px 20px;
    display: flex;
    align-items: center;
    gap: 20px;
    justify-content: space-between;
    box-shadow: 
      0 8px 32px rgba(0,0,0,0.3),
      inset 0 1px 0 rgba(255,255,255,0.1);
  }
  
  .brand {
    display: flex;
    align-items: center;
    gap: 12px;
    font-weight: 700;
    font-size: 1.1rem;
    color: var(--neon-blue);
    text-shadow: 0 0 10px var(--neon-blue);
  }
  
  .brand .logo {
    width: 32px;
    height: 32px;
    border-radius: 8px;
    background: linear-gradient(45deg, var(--neon-blue), var(--neon-purple));
    display: grid;
    place-items: center;
    font-size: 16px;
    animation: logo-pulse 2s ease-in-out infinite alternate;
    box-shadow: var(--glow);
  }
  
  @keyframes logo-pulse {
    0% { box-shadow: 0 0 20px rgba(0,212,255,0.3); }
    100% { box-shadow: 0 0 30px rgba(0,212,255,0.6), 0 0 40px rgba(124,58,237,0.3); }
  }
  
  .search {
    max-width: 600px;
    flex: 1;
    position: relative;
  }
  
  .search input {
    width: 100%;
    background: rgba(15,25,45,0.8);
    border: 1px solid rgba(0,212,255,0.3);
    color: var(--text);
    padding: 12px 16px;
    border-radius: 12px;
    outline: none;
    font-family: inherit;
    backdrop-filter: blur(10px);
    transition: all 0.3s ease;
  }
  
  .search input:focus {
    border-color: var(--neon-blue);
    box-shadow: 0 0 20px rgba(0,212,255,0.2);
    background: rgba(15,25,45,0.9);
  }
  
  .btn {
    position: relative;
    background: linear-gradient(135deg, rgba(15,25,45,0.8), rgba(25,35,55,0.6));
    border: 1px solid rgba(0,212,255,0.4);
    color: var(--neon-blue);
    padding: 12px 18px;
    border-radius: 12px;
    cursor: pointer;
    font-family: inherit;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    transition: all 0.3s ease;
    backdrop-filter: blur(10px);
    overflow: hidden;
  }
  
  .btn::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(45deg, transparent, rgba(0,212,255,0.1), transparent);
    transform: translateX(-100%);
    transition: transform 0.6s ease;
  }
  
  .btn:hover::before {
    transform: translateX(100%);
  }
  
  .btn:hover {
    transform: translateY(-2px);
    box-shadow: 
      0 0 25px rgba(0,212,255,0.4),
      0 8px 25px rgba(0,0,0,0.3);
    border-color: var(--neon-blue);
  }
  
  /* Layout */
  .layout {
    display: grid;
    grid-template-columns: 300px 1fr;
    gap: 24px;
    max-width: 1400px;
    margin: 0 auto;
    padding: 24px;
    position: relative;
    z-index: 1;
  }
  
  @media (max-width: 980px) {
    .layout { grid-template-columns: 1fr; }
    .sidebar { position: static; height: auto; }
  }
  
  /* Sidebar 科技感 */
  .sidebar {
    position: sticky;
    top: 100px;
    height: calc(100vh - 120px);
    overflow: auto;
    background: linear-gradient(145deg, rgba(15,25,45,0.7), rgba(25,35,55,0.5));
    border: 1px solid rgba(0,212,255,0.2);
    border-radius: 16px;
    padding: 20px;
    backdrop-filter: blur(15px);
    box-shadow: 
      0 8px 32px rgba(0,0,0,0.3),
      inset 0 1px 0 rgba(255,255,255,0.1);
  }
  
  .toc h3 {
    margin: 8px 0 16px;
    font-size: 14px;
    color: var(--neon-blue);
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 1px;
    text-shadow: 0 0 10px var(--neon-blue);
  }
  
  .toc a {
    display: flex;
    align-items: center;
    gap: 12px;
    text-decoration: none;
    color: var(--text);
    padding: 12px 16px;
    border-radius: 10px;
    border: 1px solid transparent;
    margin-bottom: 4px;
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }
  
  .toc a::before {
    content: '';
    position: absolute;
    left: 0;
    top: 0;
    height: 100%;
    width: 0;
    background: linear-gradient(90deg, var(--neon-blue), transparent);
    transition: width 0.3s ease;
  }
  
  .toc a:hover {
    background: rgba(0,212,255,0.1);
    border-color: rgba(0,212,255,0.3);
    transform: translateX(4px);
  }
  
  .toc a:hover::before {
    width: 4px;
  }
  
  .toc a.active {
    background: linear-gradient(135deg, rgba(0,212,255,0.2), rgba(124,58,237,0.1));
    border-color: var(--neon-blue);
    color: var(--neon-blue);
    box-shadow: 0 0 15px rgba(0,212,255,0.3);
  }
  
  .toc a.active::before {
    width: 4px;
  }
  
  /* Main Content */
  main { min-height: 70vh; }
  
  section {
    background: var(--panel);
    border: 1px solid rgba(0,212,255,0.2);
    border-radius: 16px;
    padding: 28px;
    margin-bottom: 24px;
    position: relative;
    overflow: hidden;
    backdrop-filter: blur(15px);
    box-shadow: 
      0 8px 32px rgba(0,0,0,0.3),
      inset 0 1px 0 rgba(255,255,255,0.1);
  }
  
  section::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--neon-blue), var(--neon-purple), var(--neon-green));
    animation: border-flow 3s ease-in-out infinite;
  }
  
  @keyframes border-flow {
    0%, 100% { opacity: 0.5; }
    50% { opacity: 1; }
  }
  
  .title {
    display: flex;
    align-items: center;
    gap: 16px;
    justify-content: space-between;
    margin-bottom: 20px;
  }
  
  h2 {
    margin: 0;
    font-size: 1.6rem;
    color: var(--neon-blue);
    font-weight: 700;
    text-shadow: 0 0 15px var(--neon-blue);
  }
  
  .meta {
    color: var(--muted);
    font-size: 0.9rem;
    font-style: italic;
    margin-bottom: 16px;
  }
  
  /* Cards */
  .card {
    background: linear-gradient(145deg, rgba(15,25,45,0.6), rgba(25,35,55,0.4));
    border: 1px solid rgba(0,212,255,0.2);
    border-radius: 12px;
    padding: 18px;
    transition: all 0.3s ease;
    backdrop-filter: blur(10px);
    position: relative;
    overflow: hidden;
  }
  
  .card::before {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(0,212,255,0.1), transparent);
    transition: left 0.6s ease;
  }
  
  .card:hover {
    transform: translateY(-4px);
    box-shadow: 
      0 0 25px rgba(0,212,255,0.3),
      0 12px 35px rgba(0,0,0,0.3);
    border-color: var(--neon-blue);
  }
  
  .card:hover::before {
    left: 100%;
  }
  
  /* Feature Cards */
  .feature {
    display: flex;
    gap: 16px;
    align-items: flex-start;
  }
  
  .feature .icon {
    width: 48px;
    height: 48px;
    border-radius: 12px;
    background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple));
    display: grid;
    place-items: center;
    font-size: 24px;
    box-shadow: 0 0 20px rgba(0,212,255,0.4);
    animation: icon-glow 2s ease-in-out infinite alternate;
    flex-shrink: 0;
  }
  
  @keyframes icon-glow {
    0% { box-shadow: 0 0 20px rgba(0,212,255,0.4); }
    100% { box-shadow: 0 0 30px rgba(0,212,255,0.6), 0 0 40px rgba(124,58,237,0.2); }
  }
  
  /* Stats Card */
  .stat-card {
    text-align: center;
    background: linear-gradient(145deg, rgba(16,185,129,0.2), rgba(15,25,45,0.8));
    border: 1px solid var(--neon-green);
    border-radius: 12px;
    padding: 20px;
    position: relative;
    overflow: hidden;
  }
  
  .stat-card .number {
    font-size: 2.2rem;
    font-weight: 900;
    color: var(--neon-green);
    text-shadow: 0 0 15px var(--neon-green);
    display: block;
    margin-bottom: 8px;
  }
  
  .stat-card .label {
    font-size: 0.9rem;
    color: var(--text);
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }
  
  /* Grid */
  .grid { display: grid; gap: 16px; }
  .grid.cols-3 { grid-template-columns: repeat(3, 1fr); }
  .grid.cols-2 { grid-template-columns: repeat(2, 1fr); }
  .grid.cols-4 { grid-template-columns: repeat(4, 1fr); }
  
  @media (max-width: 960px) {
    .grid.cols-3, .grid.cols-2, .grid.cols-4 { grid-template-columns: 1fr; }
  }
  
  /* Tabs */
  .tabs {
    display: flex;
    gap: 8px;
    margin: 12px 0 20px;
    flex-wrap: wrap;
  }
  
  .tab {
    padding: 12px 18px;
    border-radius: 10px;
    border: 1px solid rgba(0,212,255,0.3);
    background: rgba(15,25,45,0.6);
    color: var(--text);
    cursor: pointer;
    font-family: inherit;
    font-weight: 600;
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }
  
  .tab::before {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 0;
    height: 2px;
    background: var(--neon-blue);
    transition: width 0.3s ease;
  }
  
  .tab:hover {
    background: rgba(0,212,255,0.1);
    border-color: var(--neon-blue);
  }
  
  .tab:hover::before {
    width: 100%;
  }
  
  .tab.active {
    background: linear-gradient(135deg, rgba(0,212,255,0.2), rgba(124,58,237,0.1));
    border-color: var(--neon-blue);
    color: var(--neon-blue);
    box-shadow: 0 0 15px rgba(0,212,255,0.3);
  }
  
  .tab.active::before {
    width: 100%;
  }
  
  .tab-panel { display: none; }
  .tab-panel.active { display: block; }
  
  /* Details */
  details {
    border: 1px solid rgba(0,212,255,0.2);
    border-radius: 12px;
    padding: 16px;
    margin: 12px 0;
    background: rgba(15,25,45,0.4);
    backdrop-filter: blur(10px);
  }
  
  details summary {
    cursor: pointer;
    font-weight: 600;
    color: var(--neon-blue);
    margin-bottom: 12px;
    position: relative;
    list-style: none;
  }
  
  details summary::before {
    content: '▶';
    position: absolute;
    left: -20px;
    transition: transform 0.3s ease;
  }
  
  details[open] summary::before {
    transform: rotate(90deg);
  }
  
  details[open] {
    animation: details-open 0.3s ease;
  }
  
  @keyframes details-open {
    0% { opacity: 0.5; transform: translateY(-4px); }
    100% { opacity: 1; transform: translateY(0); }
  }
  
  /* Progress bars */
  .progress-bar {
    background: rgba(15,25,45,0.8);
    border-radius: 8px;
    height: 8px;
    overflow: hidden;
    margin: 8px 0;
  }
  
  .progress-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--neon-blue), var(--neon-green));
    border-radius: 8px;
    transition: width 1s ease;
    box-shadow: 0 0 10px rgba(0,212,255,0.5);
  }
  
  /* Toolbar */
  .toolbar {
    display: flex;
    gap: 8px;
    align-items: center;
  }
  
  .icon-btn {
    background: rgba(15,25,45,0.8);
    border: 1px solid rgba(0,212,255,0.3);
    border-radius: 8px;
    padding: 8px;
    cursor: pointer;
    color: var(--neon-blue);
    font-size: 14px;
    transition: all 0.3s ease;
  }
  
  .icon-btn:hover {
    background: rgba(0,212,255,0.1);
    box-shadow: 0 0 12px rgba(0,212,255,0.4);
    transform: translateY(-1px);
  }
  
  /* Form */
  form.grid input, form.grid textarea, form.grid select {
    background: rgba(15,25,45,0.6);
    border: 1px solid rgba(0,212,255,0.3);
    color: var(--text);
    padding: 14px;
    border-radius: 10px;
    outline: none;
    font-family: inherit;
    transition: all 0.3s ease;
  }
  
  form.grid input:focus, form.grid textarea:focus, form.grid select:focus {
    border-color: var(--neon-blue);
    box-shadow: 0 0 15px rgba(0,212,255,0.2);
    background: rgba(15,25,45,0.8);
  }
  
  /* Tables */
  .spec-table {
    width: 100%;
    border-collapse: collapse;
    margin: 16px 0;
    background: rgba(15,25,45,0.4);
    border-radius: 12px;
    overflow: hidden;
  }
  
  .spec-table th {
    background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple));
    color: white;
    padding: 16px;
    text-align: left;
    font-weight: 700;
  }
  
  .spec-table td {
    padding: 12px 16px;
    border-bottom: 1px solid rgba(0,212,255,0.1);
  }
  
  .spec-table tr:hover {
    background: rgba(0,212,255,0.05);
  }
  
  /* Pulse Animation */
  .pulse {
    animation: pulse-glow 2s ease-in-out infinite;
  }
  
  @keyframes pulse-glow {
    0%, 100% { 
      box-shadow: 0 0 20px rgba(16,185,129,0.4);
    }
    50% { 
      box-shadow: 0 0 35px rgba(16,185,129,0.7), 0 0 50px rgba(16,185,129,0.3);
    }
  }
  
  /* Status indicators */
  .status {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 4px 8px;
    border-radius: 6px;
    font-size: 0.8rem;
    font-weight: 600;
  }
  
  .status.active {
    background: rgba(16,185,129,0.2);
    color: var(--neon-green);
  }
  
  .status.warning {
    background: rgba(245,158,11,0.2);
    color: var(--warn);
  }
  
  .status.critical {
    background: rgba(239,68,68,0.2);
    color: var(--critical);
  }
  
  /* Back to top */
  #topBtn {
    position: fixed;
    right: 24px;
    bottom: 24px;
    z-index: 1000;
    border: none;
    border-radius: 50%;
    width: 52px;
    height: 52px;
    display: grid;
    place-items: center;
    cursor: pointer;
    background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple));
    color: #fff;
    font-size: 18px;
    font-weight: bold;
    opacity: 0;
    pointer-events: none;
    transition: all 0.3s ease;
    box-shadow: 0 0 25px rgba(0,212,255,0.4);
  }
  
  #topBtn.show {
    opacity: 1;
    pointer-events: auto;
  }
  
  #topBtn:hover {
    transform: translateY(-4px);
    box-shadow: 0 0 35px rgba(0,212,255,0.6), 0 8px 25px rgba(0,0,0,0.3);
  }
  
  /* Alert boxes */
  .alert {
    padding: 16px;
    border-radius: 12px;
    margin: 16px 0;
    border-left: 4px solid;
    position: relative;
    backdrop-filter: blur(10px);
  }
  
  .alert.info {
    background: rgba(0,212,255,0.1);
    border-color: var(--neon-blue);
    color: var(--text);
  }
  
  .alert.success {
    background: rgba(16,185,129,0.1);
    border-color: var(--neon-green);
    color: var(--text);
  }
  
  .alert.warning {
    background: rgba(245,158,11,0.1);
    border-color: var(--warn);
    color: var(--text);
  }
  
  /* Scrollbar */
  ::-webkit-scrollbar {
    width: 8px;
  }
  
  ::-webkit-scrollbar-track {
    background: rgba(15,25,45,0.3);
  }
  
  ::-webkit-scrollbar-thumb {
    background: linear-gradient(180deg, var(--neon-blue), var(--neon-purple));
    border-radius: 4px;
  }
  
  ::-webkit-scrollbar-thumb:hover {
    background: linear-gradient(180deg, var(--neon-purple), var(--neon-blue));
  }
  
  /* Responsive text */
  @media (max-width: 768px) {
    h2 { font-size: 1.4rem; }
    .feature { flex-direction: column; text-align: center; }
    .feature .icon { width: 40px; height: 40px; font-size: 20px; }
  }
</style>
</head>
<body>
  <!-- 粒子背景 -->
  <div class="particles" id="particles"></div>

  <header>
    <div class="brand">
      <div class="logo">🛡️</div>
      GWall 4.0 網路安全解決方案
    </div>
    <div class="search">
      <input id="searchInput" placeholder="搜尋章節 / 關鍵字（例如：VPN、IPS、零信任、高可用性）"/>
    </div>
    <div style="display: flex; gap: 12px;">
      <button class="btn" id="clearSearch">清除</button>
      <button class="btn" id="expandAll">展開全部</button>
    </div>
  </header>

  <div class="layout">
    <aside class="sidebar">
      <nav class="toc" id="toc">
        <h3>產品導覽</h3>
        <div id="tocLinks"></div>
        
        <div style="margin-top: 24px; padding: 16px; background: rgba(16,185,129,0.1); border: 1px solid var(--neon-green); border-radius: 12px;">
          <h4 style="color: var(--neon-green); margin: 0 0 8px; font-size: 0.9rem;">即時狀態</h4>
          <div class="status active">🟢 系統正常</div>
          <div style="margin-top: 8px; font-size: 0.8rem; color: var(--muted);">威脅特徵庫已更新</div>
        </div>
      </nav>
    </aside>

    <main id="content">
      <!-- 1 產品概述 -->
      <section id="intro" data-title="產品概述">
        <div class="title">
          <h2>GWall 4.0 企業級網路安全解決方案</h2>
          <div class="toolbar">
            <button class="icon-btn" data-copy="#intro">🔗</button>
            <button class="icon-btn" data-collapse>－</button>
          </div>
        </div>
        <p class="meta">Angroup GWall 4.0 - 次世代整合式網路安全平台，結合防火牆、VPN、IDS/IPS、應用控制於單一設備，提供企業級零信任架構與威脅防護。</p>
        
        <div class="grid cols-4" style="margin-bottom: 24px;">
          <div class="stat-card">
            <span class="number">5Gbps</span>
            <span class="label">防火牆吞吐量</span>
          </div>
          <div class="stat-card">
            <span class="number">800Mbps</span>
            <span class="label">VPN 效能</span>
          </div>
          <div class="stat-card">
            <span class="number">50K</span>
            <span class="label">並發連線</span>
          </div>
          <div class="stat-card">
            <span class="number">99.9%</span>
            <span class="label">可用性保證</span>
          </div>
        </div>
        
        <details open>
          <summary>核心優勢</summary>
          <div class="grid cols-3">
            <div class="card feature">
              <div class="icon">🔐</div>
              <div>
                <b>多重 VPN 技術</b><br>
                <small>支援 OpenVPN、WireGuard、IPSec VPN，提供最高 800Mbps 加密傳輸效能</small>
              </div>
            </div>
            <div class="card feature">
              <div class="icon">🛡️</div>
              <div>
                <b>AI 驅動防護</b><br>
                <small>機器學習引擎結合傳統特徵比對，提供零日威脅檢測與自動化回應</small>
              </div>
            </div>
            <div class="card feature">
              <div class="icon">⚡</div>
              <div>
                <b>極致效能</b><br>
                <small>防火牆吞吐量達 5Gbps，支援 50,000 併發連線與每秒 5,000 新連線</small>
              </div>
            </div>
            <div class="card feature">
              <div class="icon">🌐</div>
              <div>
                <b>零信任架構</b><br>
                <small>以身份為核心的存取控制，微分段技術防範橫向移動攻擊</small>
              </div>
            </div>
            <div class="card feature">
              <div class="icon">📊</div>
              <div>
                <b>智慧分析</b><br>
                <small>即時流量視覺化、威脅情報整合、預測性風險評估</small>
              </div>
            </div>
            <div class="card feature">
              <div class="icon">🔧</div>
              <div>
                <b>統一管理</b><br>
                <small>Web-based 集中控台，支援 API 自動化與第三方 SIEM 整合</small>
              </div>
            </div>
          </div>
        </details>
        
        <details>
          <summary>產業認證與合規</summary>
          <div class="grid cols-2">
            <div class="card">
              <b>🏆 國際認證</b><br>
              <small>Common Criteria EAL4+、FIPS 140-2 Level 2、IPv6 Ready Logo</small>
            </div>
            <div class="card">
              <b>📋 法規遵循</b><br>
              <small>支援 GDPR、HIPAA、SOX、PCI-DSS 等合規要求</small>
            </div>
          </div>
        </details>
      </section>

      <!-- 2 解決方案架構 -->
      <section id="architecture" data-title="解決方案架構">
        <div class="title">
          <h2>解決方案架構</h2>
          <div class="toolbar">
            <button class="icon-btn" data-copy="#architecture">🔗</button>
            <button class="icon-btn" data-collapse>－</button>
          </div>
        </div>
        <p class="meta">現代化網路安全架構設計，整合邊緣防護、核心控制與雲端威脅情報，實現全方位安全防護。</p>
        
        <details open>
          <summary>架構核心元件</summary>
          <div class="grid cols-2">
            <div class="card">
              <b>🌊 流量控制層</b><br>
              <small><strong>北向/南向：</strong>外網存取控制與威脅阻斷<br>
              <strong>東西向：</strong>內網微分段與橫向移動防護</small>
            </div>
            <div class="card">
              <b>🧠 威脅情報中心</b><br>
              <small><strong>即時同步：</strong>全球威脅情報與 IOC 指標<br>
              <strong>機器學習：</strong>行為基線學習與異常檢測</small>
            </div>
            <div class="card">
              <b>🎯 政策引擎</b><br>
              <small><strong>集中管理：</strong>統一政策配發與版本控制<br>
              <strong>動態調整：</strong>基於風險等級的自動政策更新</small>
            </div>
            <div class="card">
              <b>⚡ 高可用性設計</b><br>
              <small><strong>Active-Active：</strong>雙機負載平衡與故障切換<br>
              <strong>狀態同步：</strong>連線表與政策即時同步</small>
            </div>
          </div>
        </details>
        
        <details>
          <summary>部署拓撲範例</summary>
          <div class="alert info">
            <strong>💡 建議架構：</strong>採用 DMZ 三層架構設計，外網區 → DMZ 區 → 內網區，每層間部署 GWall 4.0 進行流量檢查與控制。
          </div>
          <ul>
            <li><strong>邊界部署：</strong>作為主要防火牆，處理所有外網流量</li>
            <li><strong>核心交換：</strong>內網分段控制，東西向流量監控</li>
            <li><strong>雲端整合：</strong>混合雲環境的統一安全政策</li>
            <li><strong>分支連接：</strong>SD-WAN 與傳統 MPLS 的安全閘道</li>
          </ul>
        </details>
      </section>

      <!-- 3 核心功能 -->
      <section id="features" data-title="核心功能">
        <div class="title">
          <h2>核心功能模組</h2>
          <div class="toolbar">
            <button class="icon-btn" data-copy="#features">🔗</button>
            <button class="icon-btn" data-collapse>－</button>
          </div>
        </div>
        
        <div class="tabs" data-tabs>
          <button class="tab active" data-tab="f1">防火牆 & NAT</button>
          <button class="tab" data-tab="f2">VPN 解決方案</button>
          <button class="tab" data-tab="f3">IDS/IPS 防護</button>
          <button class="tab" data-tab="f4">應用控制</button>
          <button class="tab" data-tab="f5">監控告警</button>
          <button class="tab" data-tab="f6">零信任</button>
        </div>
        
        <div class="tab-panel active" id="f1">
          <div class="grid cols-2">
            <div class="card">
              <b>🔥 狀態防火牆</b><br>
              <small>基於連線狀態的深度包檢測，支援 TCP/UDP 狀態追蹤與應用層檢查</small>
              <div class="progress-bar"><div class="progress-fill" style="width: 95%"></div></div>
            </div>
            <div class="card">
              <b>🔄 進階 NAT</b><br>
              <small>支援 SNAT/DNAT/Port Forwarding，多 WAN 負載平衡與故障切換</small>
              <div class="progress-bar"><div class="progress-fill" style="width: 88%"></div></div>
            </div>
            <div class="card">
              <b>🏷️ Zone 管理</b><br>
              <small>邏輯區域劃分，支援 VLAN、物理介面與虛擬介面混合配置</small>
              <div class="progress-bar"><div class="progress-fill" style="width: 92%"></div></div>
            </div>
            <div class="card">
              <b>📐 政策物件</b><br>
              <small>地址群組、服務群組、時間排程，可重複使用的政策元件</small>
              <div class="progress-bar"><div class="progress-fill" style="width: 90%"></div></div>
            </div>
          </div>
        </div>
        
        <div class="tab-panel" id="f2">
          <div class="alert success">
            <strong>🚀 業界領先 VPN 效能：</strong>採用硬體加速引擎，AES-256 加密下仍可達到 800Mbps 吞吐量。
          </div>
          <div class="grid cols-2">
            <div class="card">
              <b>🏢 Site-to-Site VPN</b><br>
              <small><strong>IPSec：</strong>IKEv1/v2、ESP/AH、PFS 支援<br>
              <strong>相容性：</strong>Cisco、Fortinet、Palo Alto 等主流設備</small>
            </div>
            <div class="card">
              <b>👥 Remote Access VPN</b><br>
              <small><strong>SSL VPN：</strong>無客戶端 Web 存取<br>
              <strong>OpenVPN：</strong>跨平台客戶端支援</small>
            </div>
            <div class="card">
              <b>🆕 WireGuard 支援</b><br>
              <small><strong>新世代協定：</strong>更快速、更安全的 VPN 體驗<br>
              <strong>行動優化：</strong>適合行動裝置與不穩定網路</small>
            </div>
            <div class="card">
              <b>🔐 進階認證</b><br>
              <small><strong>雙因子驗證：</strong>OTP、硬體金鑰、行動 App<br>
              <strong>AD 整合：</strong>LDAP/RADIUS 單一登入</small>
            </div>
          </div>
        </div>
        
        <div class="tab-panel" id="f3">
          <div class="grid cols-2">
            <div class="card">
              <b>🎯 威脅檢測引擎</b><br>
              <small><strong>特徵比對：</strong>40,000+ 威脅特徵，每日更新<br>
              <strong>異常偵測：</strong>基於 ML 的行為分析與零日威脅檢測</small>
            </div>
            <div class="card">
              <b>⚡ 即時防禦</b><br>
              <small><strong>自動阻斷：</strong>惡意 IP/域名即時封鎖<br>
              <strong>速率限制：</strong>DDoS 攻擊緩解與頻寬控制</small>
            </div>
            <div class="card">
              <b>🔬 深度檢測</b><br>
              <small><strong>協定分析：</strong>HTTP/HTTPS、FTP、SMTP 等應用層檢查<br>
              <strong>惡意軟體：</strong>檔案沙箱分析與病毒掃描</small>
            </div>
            <div class="card">
              <b>🚨 事件回應</b><br>
              <small><strong>自動化：</strong>SOAR 整合，事件自動分類與處理<br>
              <strong>取證支援：</strong>完整攻擊鏈重建與證據保全</small>
            </div>
          </div>
        </div>
        
        <div class="tab-panel" id="f4">
          <div class="grid cols-2">
            <div class="card">
              <b>🕵️ Layer 7 應用辨識</b><br>
              <small><strong>深度檢測：</strong>超過 3,000 種應用程式辨識<br>
              <strong>自訂分類：</strong>企業專屬應用與雲端服務控制</small>
            </div>
            <div class="card">
              <b>🌐 URL 過濾</b><br>
              <small><strong>即時分類：</strong>80+ 類別，惡意網站即時攔截<br>
              <strong>自訂清單：</strong>黑白名單與例外規則設定</small>
            </div>
            <div class="card">
              <b>⏰ 時間政策</b><br>
              <small><strong>工作時段：</strong>基於時間的存取控制<br>
              <strong>頻寬配置：</strong>動態 QoS 與流量優先權</small>
            </div>
            <div class="card">
              <b>☁️ 雲端應用控制</b><br>
              <small><strong>SaaS 管控：</strong>Office 365、Google Workspace 精細控制<br>
              <strong>影子 IT：</strong>未授權雲端服務檢測與阻斷</small>
            </div>
          </div>
        </div>
        
        <div class="tab-panel" id="f5">
          <div class="grid cols-2">
            <div class="card">
              <b>📊 即時監控儀表板</b><br>
              <small><strong>視覺化：</strong>流量圖表、威脅地圖、連線狀態<br>
              <strong>效能監控：</strong>CPU、記憶體、網路介面使用率</small>
            </div>
            <div class="card">
              <b>📧 智慧告警系統</b><br>
              <small><strong>多通道：</strong>Email、SMS、Webhook、SNMP Trap<br>
              <strong>智慧過濾：</strong>告警聚合與重複抑制</small>
            </div>
            <div class="card">
              <b>📋 合規報表</b><br>
              <small><strong>自動生成：</strong>法規遵循、稽核、管理報表<br>
              <strong>客製化：</strong>排程報表與 CSV/PDF 匯出</small>
            </div>
            <div class="card">
              <b>🔍 日誌分析</b><br>
              <small><strong>集中收集：</strong>Syslog、CEF、LEEF 格式支援<br>
              <strong>長期保存：</strong>法規要求的日誌保留與檢索</small>
            </div>
          </div>
        </div>
        
        <div class="tab-panel" id="f6">
          <div class="alert info">
            <strong>🎯 零信任核心原則：</strong>永不信任，持續驗證 - 每個存取請求都需通過身份驗證、裝置檢查與風險評估。
          </div>
          <div class="grid cols-2">
            <div class="card">
              <b>🆔 身份驗證</b><br>
              <small><strong>多因子認證：</strong>密碼 + OTP + 生物特徵<br>
              <strong>單一登入：</strong>SAML、OAuth 2.0、OpenID Connect</small>
            </div>
            <div class="card">
              <b>📱 裝置信任</b><br>
              <small><strong>端點檢查：</strong>防毒狀態、修補程式、合規性<br>
              <strong>憑證管理：</strong>PKI 整合與裝置憑證驗證</small>
            </div>
            <div class="card">
              <b>🎲 風險評估</b><br>
              <small><strong>動態評分：</strong>使用者、裝置、位置風險計算<br>
              <strong>適應性存取：</strong>基於風險的存取權限調整</small>
            </div>
            <div class="card">
              <b>🔍 持續監控</b><br>
              <small><strong>行為分析：</strong>異常行為即時檢測<br>
              <strong>會話管理：</strong>動態會話驗證與終止</small>
            </div>
          </div>
        </div>
      </section>

      <!-- 4 進階安全功能 -->
      <section id="advanced" data-title="進階安全">
        <div class="title">
          <h2>進階安全功能</h2>
          <div class="toolbar">
            <button class="icon-btn" data-copy="#advanced">🔗</button>
            <button class="icon-btn" data-collapse>－</button>
          </div>
        </div>
        
        <details open>
          <summary>AI 威脅防護</summary>
          <div class="grid cols-3">
            <div class="card">
              <b>🤖 機器學習引擎</b><br>
              <small>深度學習模型分析網路流量模式，檢測未知威脅與進階持續威脅（APT）</small>
            </div>
            <div class="card">
              <b>🔮 預測性分析</b><br>
              <small>基於歷史攻擊模式預測潛在威脅，提前部署防護策略</small>
            </div>
            <div class="card">
              <b>🎯 精準阻斷</b><br>
              <small>智慧判斷減少誤報，確保業務連續性同時維持高安全性</small>
            </div>
          </div>
        </details>
        
        <details>
          <summary>企業整合能力</summary>
          <div class="grid cols-2">
            <div class="card">
              <b>🔌 SIEM/SOAR 整合</b><br>
              <small><strong>支援平台：</strong>Splunk、IBM QRadar、Microsoft Sentinel<br>
              <strong>API 介接：</strong>RESTful API 與 Webhook 事件推送</small>
            </div>
            <div class="card">
              <b>🛡️ EDR/XDR 聯防</b><br>
              <small><strong>端點協作：</strong>與 CrowdStrike、SentinelOne 等 EDR 整合<br>
              <strong>威脅獵捕：</strong>網路與端點的關聯分析</small>
            </div>
            <div class="card">
              <b>☁️ 雲端安全</b><br>
              <small><strong>CASB 功能：</strong>雲端應用存取控制與資料外洩防護<br>
              <strong>混合雲：</strong>統一管理地端與雲端安全政策</small>
            </div>
            <div class="card">
              <b>🔗 IT 生態整合</b><br>
              <small><strong>身份管理：</strong>Active Directory、LDAP、Azure AD<br>
              <strong>票務系統：</strong>ServiceNow、Jira 事件自動建立</small>
            </div>
          </div>
        </details>
        
        <details>
          <summary>法規遵循與稽核</summary>
          <div class="alert warning">
            <strong>⚖️ 法規要求：</strong>符合個資法、資通安全管理法等台灣法規，以及國際 GDPR、HIPAA、SOX 等合規標準。
          </div>
          <ul>
            <li><strong>稽核軌跡：</strong>完整的管理員操作記錄與政策變更歷程</li>
            <li><strong>資料保護：</strong>敏感資料識別、DLP 功能與加密傳輸</li>
            <li><strong>存取控制：</strong>最小權限原則與職責分離設計</li>
            <li><strong>定期檢核：</strong>自動合規性檢查與報告生成</li>
          </ul>
        </details>
      </section>

      <!-- 5 部署情境 -->
      <section id="scenarios" data-title="部署情境">
        <div class="title">
          <h2>部署情境與最佳實務</h2>
          <div class="toolbar">
            <button class="icon-btn" data-copy="#scenarios">🔗</button>
            <button class="icon-btn" data-collapse>－</button>
          </div>
        </div>
        
        <div class="tabs" data-tabs>
          <button class="tab active" data-tab="s1">中小企業</button>
          <button class="tab" data-tab="s2">大型企業</button>
          <button class="tab" data-tab="s3">金融業</button>
          <button class="tab" data-tab="s4">製造業</button>
          <button class="tab" data-tab="s5">教育業</button>
        </div>
        
        <div class="tab-panel active" id="s1">
          <div class="card feature">
            <div class="icon">🏢</div>
            <div>
              <b>單點部署方案</b><br>
              <small><strong>適用規模：</strong>50-200 人企業，單一據點或總部<br>
              <strong>主要功能：</strong>邊界防護、員工上網管理、基本 VPN 存取<br>
              <strong>建議配置：</strong>GWall-2000 系列，雙 WAN 備援</small>
            </div>
          </div>
          <div class="grid cols-2">
            <div class="card">
              <b>💰 投資回報</b><br>
              <small>整合多功能設備，減少 60% 硬體成本與維護費用</small>
            </div>
            <div class="card">
              <b>⚡ 快速部署</b><br>
              <small>預設政策模板，24 小時內完成基本配置</small>
            </div>
          </div>
        </div>
        
        <div class="tab-panel" id="s2">
          <div class="card feature">
            <div class="icon">🏭</div>
            <div>
              <b>企業級高可用性方案</b><br>
              <small><strong>適用規模：</strong>500+ 人企業，多據點分布<br>
              <strong>架構特色：</strong>Active-Active HA、集中管理、分層防護<br>
              <strong>建議配置：</strong>GWall-5000 系列 HA 叢集</small>
            </div>
          </div>
          <div class="grid cols-3">
            <div class="card">
              <b>🔄 高可用性</b><br>
              <small>99.99% 運行時間保證，故障切換 < 3 秒</small>
            </div>
            <div class="card">
              <b>📈 可擴展性</b><br>
              <small>模組化架構，支援水平與垂直擴展</small>
            </div>
            <div class="card">
              <b>🎛️ 集中管理</b><br>
              <small>統一控制台管理所有據點設備</small>
            </div>
          </div>
        </div>
        
        <div class="tab-panel" id="s3">
          <div class="card feature">
            <div class="icon">🏦</div>
            <div>
              <b>金融業專用解決方案</b><br>
              <small><strong>法規遵循：</strong>符合金管會資安規範、個資法要求<br>
              <strong>高安全性：</strong>多層防護、加密傳輸、存取控制<br>
              <strong>稽核需求：</strong>完整日誌記錄與合規報表</small>
            </div>
          </div>
          <div class="grid cols-2">
            <div class="card">
              <b>🔒 資料保護</b><br>
              <small>端到端加密、DLP 防護、敏感資料遮罩</small>
            </div>
            <div class="card">
              <b>📋 法規合規</b><br>
              <small>自動化合規檢查、稽核報表、政策基線</small>
            </div>
          </div>
        </div>
        
        <div class="tab-panel" id="s4">
          <div class="card feature">
            <div class="icon">⚙️</div>
            <div>
              <b>智慧製造安全方案</b><br>
              <small><strong>OT/IT 整合：</strong>工業控制系統與企業網路安全隔離<br>
              <strong>零停機：</strong>不影響生產線的安全更新與維護<br>
              <strong>物聯網防護：</strong>工業物聯網設備存取控制</small>
            </div>
          </div>
          <div class="grid cols-2">
            <div class="card">
              <b>🏭 生產網路隔離</b><br>
              <small>OT/IT 網路分段，保護關鍵生產系統</small>
            </div>
            <div class="card">
              <b>📡 IoT 設備管理</b><br>
              <small>工業物聯網設備識別與存取控制</small>
            </div>
          </div>
        </div>
        
        <div class="tab-panel" id="s5">
          <div class="card feature">
            <div class="icon">🎓</div>
            <div>
              <b>校園網路安全方案</b><br>
              <small><strong>多用戶管理：</strong>學生、教職員、訪客分層存取控制<br>
              <strong>內容過濾：</strong>不當內容攔截與學習資源保護<br>
              <strong>頻寬管理：</strong>公平使用與學術優先的流量分配</small>
            </div>
          </div>
          <div class="grid cols-2">
            <div class="card">
              <b>👥 多角色管理</b><br>
              <small>學生、教師、行政、訪客不同權限控制</small>
            </div>
            <div class="card">
              <b>📚 學習環境保護</b><br>
              <small>不當內容過濾、網路霸凌防護</small>
            </div>
          </div>
        </div>
      </section>

      <!-- 6 硬體規格 -->
      <section id="specs" data-title="硬體規格">
        <div class="title">
          <h2>產品規格與效能</h2>
          <div class="toolbar">
            <button class="icon-btn" data-copy="#specs">🔗</button>
            <button class="icon-btn" data-collapse>－</button>
          </div>
        </div>
        <p class="meta">高效能硬體平台，採用多核心處理器與硬體加速技術，提供企業級可靠性與擴展性。</p>
        
        <details open>
          <summary>GWall-2000 系列（中小企業）</summary>
          <table class="spec-table">
            <thead>
              <tr>
                <th>規格項目</th>
                <th>GWall-2500</th>
                <th>GWall-2800</th>
              </tr>
            </thead>
            <tbody>
              <tr><td><b>防火牆吞吐量</b></td><td>2.5 Gbps</td><td>5 Gbps</td></tr>
              <tr><td><b>VPN 吞吐量</b></td><td>400 Mbps</td><td>800 Mbps</td></tr>
              <tr><td><b>最大併發連線</b></td><td>25,000</td><td>50,000</td></tr>
              <tr><td><b>新連線/秒</b></td><td>2,500</td><td>5,000</td></tr>
              <tr><td><b>網路介面</b></td><td>6× GbE + 2× SFP+</td><td>8× GbE + 4× SFP+</td></tr>
              <tr><td><b>處理器</b></td><td>4 核心 2.0GHz</td><td>8 核心 2.4GHz</td></tr>
              <tr><td><b>記憶體</b></td><td>8GB DDR4</td><td>16GB DDR4</td></tr>
              <tr><td><b>儲存空間</b></td><td>256GB SSD</td><td>512GB SSD</td></tr>
              <tr><td><b>電源供應</b></td><td>150W (含備援)</td><td>250W (含備援)</td></tr>
              <tr><td><b>作業溫度</b></td><td colspan="2">0°C ~ 40°C</td></tr>
              <tr><td><b>尺寸 (W×D×H)</b></td><td colspan="2">440 × 350 × 44 mm (1U)</td></tr>
            </tbody>
          </table>
        </details>
        
        <details>
          <summary>GWall-5000 系列（企業級）</summary>
          <table class="spec-table">
            <thead>
              <tr>
                <th>規格項目</th>
                <th>GWall-5200</th>
                <th>GWall-5500</th>
                <th>GWall-5800</th>
              </tr>
            </thead>
            <tbody>
              <tr><td><b>防火牆吞吐量</b></td><td>10 Gbps</td><td>20 Gbps</td><td>40 Gbps</td></tr>
              <tr><td><b>VPN 吞吐量</b></td><td>2 Gbps</td><td>5 Gbps</td><td>10 Gbps</td></tr>
              <tr><td><b>最大併發連線</b></td><td>500,000</td><td>2,000,000</td><td>10,000,000</td></tr>
              <tr><td><b>新連線/秒</b></td><td>50,000</td><td>200,000</td><td>500,000</td></tr>
              <tr><td><b>網路介面</b></td><td>12× GbE + 8× SFP+</td><td>16× GbE + 8× SFP+</td><td>24× GbE + 16× SFP+</td></tr>
              <tr><td><b>處理器</b></td><td>12 核心 3.0GHz</td><td>16 核心 3.2GHz</td><td>24 核心 3.5GHz</td></tr>
              <tr><td><b>記憶體</b></td><td>32GB DDR4</td><td>64GB DDR4</td><td>128GB DDR4</td></tr>
              <tr><td><b>儲存空間</b></td><td>1TB SSD</td><td>2TB SSD</td><td>4TB SSD</td></tr>
              <tr><td><b>電源供應</b></td><td>400W (雙備援)</td><td>600W (雙備援)</td><td>800W (雙備援)</td></tr>
              <tr><td><b>作業溫度</b></td><td colspan="3">0°C ~ 40°C (工業級 -10°C ~ 60°C 可選)</td></tr>
              <tr><td><b>尺寸 (W×D×H)</b></td><td>440 × 450 × 88 mm (2U)</td><td colspan="2">440 × 650 × 132 mm (3U)</td></tr>
            </tbody>
          </table>
        </details>
        
        <details>
          <summary>效能基準測試</summary>
          <div class="grid cols-3">
            <div class="card">
              <b>🔥 防火牆測試</b><br>
              <small><strong>測試條件：</strong>64 byte 封包，雙向流量<br>
              <strong>效能保證：</strong>規格值的 95% 以上穩定輸出</small>
            </div>
            <div class="card">
              <b>🔐 VPN 加密測試</b><br>
              <small><strong>加密標準：</strong>AES-256-GCM<br>
              <strong>硬體加速：</strong>專用加密處理器，CPU 占用 < 30%</small>
            </div>
            <div class="card">
              <b>🎯 IPS 檢測測試</b></td>
              <small><strong>威脅檢測：</strong>啟用全部特徵庫<br>
              <strong>延遲影響：</strong>< 100μs 額外延遲</small>
            </div>
          </div>
        </details>
        
        <details>
          <summary>環境規格與認證</summary>
          <div class="grid cols-2">
            <div class="card">
              <b>🌡️ 環境適應性</b><br>
              <small><strong>溫度範圍：</strong>0°C ~ 40°C (標準) / -10°C ~ 60°C (工業級)<br>
              <strong>濕度範圍：</strong>5% ~ 95% (無凝結)<br>
              <strong>海拔高度：</strong>3,000 公尺以下正常運行</small>
            </div>
            <div class="card">
              <b>🏆 安全認證</b><br>
              <small><strong>國際標準：</strong>Common Criteria EAL4+、FIPS 140-2<br>
              <strong>電氣安全：</strong>UL、CE、FCC Class A<br>
              <strong>環保標準：</strong>RoHS、WEEE 符合</small>
            </div>
          </div>
        </details>
      </section>

      <!-- 7 授權與維護 -->
      <section id="licensing" data-title="授權與維護">
        <div class="title">
          <h2>授權方案與技術支援</h2>
          <div class="toolbar">
            <button class="icon-btn" data-copy="#licensing">🔗</button>
            <button class="icon-btn" data-collapse>－</button>
          </div>
        </div>
        
        <details open>
          <summary>授權方案比較</summary>
          <table class="spec-table">
            <thead>
              <tr>
                <th>功能模組</th>
                <th>基礎版</th>
                <th>專業版</th>
                <th>企業版</th>
              </tr>
            </thead>
            <tbody>
              <tr><td><b>防火牆 & NAT</b></td><td class="status active">✓ 包含</td><td class="status active">✓ 包含</td><td class="status active">✓ 包含</td></tr>
              <tr><td><b>VPN (IPSec/SSL)</b></td><td>5 條通道</td><td>50 條通道</td><td>無限制</td></tr>
              <tr><td><b>IDS/IPS 防護</b></td><td class="status warning">基礎特徵</td><td class="status active">✓ 完整</td><td class="status active">✓ 完整</td></tr>
              <tr><td><b>應用控制</b></td><td class="status warning">500 種應用</td><td class="status active">✓ 完整</td><td class="status active">✓ 完整</td></tr>
              <tr><td><b>URL 過濾</b></td><td>-</td><td class="status active">✓ 包含</td><td class="status active">✓ 包含</td></tr>
              <tr><td><b>反病毒掃描</b></td><td>-</td><td class="status active">✓ 包含</td><td class="status active">✓ 包含</td></tr>
              <tr><td><b>零信任功能</b></td><td>-</td><td>-</td><td class="status active">✓ 包含</td></tr>
              <tr><td><b>高可用性 (HA)</b></td><td>-</td><td class="status active">✓ 包含</td><td class="status active">✓ 包含</td></tr>
              <tr><td><b>集中管理</b></td><td>-</td><td>5 台設備</td><td>無限制</td></tr>
              <tr><td><b>技術支援</b></td><td>工作時間</td><td>24×5</td><td>24×7</td></tr>
            </tbody>
          </table>
        </details>
        
        <details>
          <summary>維護服務等級協定 (SLA)</summary>
          <div class="grid cols-3">
            <div class="card">
              <b>🎯 基礎支援</b><br>
              <small><strong>回應時間：</strong>4 小時 (工作時間)<br>
              <strong>解決時間：</strong>2 個工作天<br>
              <strong>支援方式：</strong>Email、線上工單</small>
            </div>
            <div class="card">
              <b>⚡ 專業支援</b><br>
              <small><strong>回應時間：</strong>2 小時 (24×5)<br>
              <strong>解決時間：</strong>4 小時 (重大問題)<br>
              <strong>支援方式：</strong>電話、遠端協助</small>
            </div>
            <div class="card">
              <b>🚀 企業支援</b><br>
              <small><strong>回應時間：</strong>1 小時 (24×7)<br>
              <strong>解決時間：</strong>2 小時 (緊急問題)<br>
              <strong>支援方式：</strong>專屬技術顧問</small>
            </div>
          </div>
        </details>
        
        <details>
          <summary>更新與升級服務</summary>
          <div class="grid cols-2">
            <div class="card">
              <b>🔄 自動更新機制</b><br>
              <small><strong>威脅特徵：</strong>每日自動更新，緊急威脅即時推送<br>
              <strong>韌體更新：</strong>季度定期更新，安全修補即時發布<br>
              <strong>應用特徵：</strong>月度更新，新興應用快速支援</small>
            </div>
            <div class="card">
              <b>📈 版本升級政策</b><br>
              <small><strong>小版本：</strong>免費升級，向下相容<br>
              <strong>大版本：</strong>優惠升級價格，功能增強<br>
              <strong>硬體升級：</strong>以舊換新優惠方案</small>
            </div>
          </div>
        </details>
        
        <details>
          <summary>專業服務項目</summary>
          <ul>
            <li><strong>🏗️ 部署規劃服務：</strong>網路架構評估、安全政策設計、實施計畫制定</li>
            <li><strong>⚙️ 安裝配置服務：</strong>現場安裝、基礎配置、功能測試驗收</li>
            <li><strong>🎓 教育訓練服務：</strong>管理員培訓、操作手冊、認證考試</li>
            <li><strong>🔍 健康檢查服務：</strong>定期系統檢查、效能優化建議、安全評估報告</li>
            <li><strong>🚨 事件回應服務：</strong>7×24 緊急支援、資安事件協處、鑑識分析服務</li>
          </ul>
        </details>
      </section>

      <!-- 8 成功案例 -->
      <section id="cases" data-title="成功案例">
        <div class="title">
          <h2>客戶成功案例</h2>
          <div class="toolbar">
            <button class="icon-btn" data-copy="#cases">🔗</button>
            <button class="icon-btn" data-collapse>－</button>
          </div>
        </div>
        
        <details open>
          <summary>產業應用實例</summary>
          <div class="grid cols-3">
            <div class="card feature">
              <div class="icon">🏭</div>
              <div>
                <b>某大型製造集團</b><br>
                <small><strong>挑戰：</strong>全球 50+ 工廠網路安全統一管理<br>
                <strong>解決：</strong>部署 GWall 5000 系列 HA 叢集<br>
                <strong>效益：</strong>資安事件減少 85%，管理效率提升 300%</small>
              </div>
            </div>
            <div class="card feature">
              <div class="icon">🏦</div>
              <div>
                <b>區域性銀行</b><br>
                <small><strong>挑戰：</strong>金融法規遵循與零信任架構建置<br>
                <strong>解決：</strong>企業版授權 + 零信任功能模組<br>
                <strong>效益：</strong>100% 法規合規，內部威脅檢測率 95%</small>
              </div>
            </div>
            <div class="card feature">
              <div class="icon">🎓</div>
              <div>
                <b>國立大學</b><br>
                <small><strong>挑戰：</strong>校園網路 15,000 用戶存取管理<br>
                <strong>解決：</strong>多台 GWall 2800 叢集部署<br>
                <strong>效益：</strong>網路安全事件降低 70%，頻寬使用最佳化</small>
              </div>
            </div>
          </div>
        </details>
        
        <details>
          <summary>量化效益分析</summary>
          <div class="grid cols-2">
            <div class="card">
              <b>💰 總擁有成本 (TCO) 降低</b><br>
              <small><strong>硬體整合：</strong>單一設備取代多套設備，減少 60% 硬體成本<br>
              <strong>管理效率：</strong>統一介面管理，IT 人力成本節省 40%<br>
              <strong>維護簡化：</strong>單一廠商支援，維護成本降低 50%</small>
            </div>
            <div class="card">
              <b>📊 安全效益提升</b><br>
              <small><strong>威脅阻斷：</strong>惡意攻擊阻斷率達 99.9%<br>
              <strong>誤報率：</strong>AI 輔助判斷，誤報率 < 0.1%<br>
              <strong>回應時間：</strong>安全事件平均回應時間 < 5 分鐘</small>
            </div>
          </div>
        </details>
        
        <details>
          <summary>客戶推薦</summary>
          <div class="alert success">
            <strong>💬 台灣某科技製造業 CTO：</strong><br>
            "GWall 4.0 不僅提供了強大的安全防護能力，更重要的是整合了我們所需的各種功能。AI 威脅檢測準確率很高，大幅減少了我們 SOC 團隊的工作負擔，真正做到了智慧化安全管理。"
          </div>
          <div class="alert info">
            <strong>💬 某金融機構資安長：</strong><br>
            "在法規遵循方面，GWall 4.0 提供的自動化合規檢查和報告功能，讓我們順利通過了金管會的資安檢查。零信任架構的建置也為我們的數位轉型提供了堅實的安全基礎。"
          </div>
        </details>
      </section>

      <!-- 9 常見問題 -->
      <section id="faq" data-title="常見問題">
        <div class="title">
          <h2>常見問題 (FAQ)</h2>
          <div class="toolbar">
            <button class="icon-btn" data-copy="#faq">🔗</button>
            <button class="icon-btn" data-collapse>－</button>
          </div>
        </div>
        
        <details open>
          <summary>🏗️ GWall 4.0 支援哪些高可用性 (HA) 模式？</summary>
          <p>支援 Active-Standby 與 Active-Active 兩種 HA 模式：</p>
          <ul>
            <li><strong>Active-Standby：</strong>主備機制，故障切換時間 < 3 秒，適合一般企業應用</li>
            <li><strong>Active-Active：</strong>雙機負載平衡，提供更高效能與可用性，適合高流量環境</li>
            <li><strong>狀態同步：</strong>連線表、政策、日誌即時同步，確保無縫切換</li>
            <li><strong>健康檢查：</strong>多種檢測機制包含網路、應用、硬體狀態監控</li>
          </ul>
        </details>
        
        <details>
          <summary>🔐 是否支援 Active Directory 整合與雙因子驗證？</summary>
          <p>完整支援企業身份認證系統：</p>
          <ul>
            <li><strong>AD/LDAP 整合：</strong>支援 Windows AD、OpenLDAP、Azure AD</li>
            <li><strong>單一登入 (SSO)：</strong>SAML 2.0、OAuth 2.0、OpenID Connect</li>
            <li><strong>雙因子驗證：</strong>TOTP (Google Authenticator)、SMS、Email、硬體 Token</li>
            <li><strong>RADIUS 支援：</strong>與既有 AAA 系統整合，支援 802.1X 認證</li>
          </ul>
        </details>
        
        <details>
          <summary>⚡ 在啟用所有安全功能下，實際效能表現如何？</summary>
          <p>GWall 4.0 採用硬體加速與效能最佳化設計：</p>
          <ul>
            <li><strong>防火牆 + IPS：</strong>效能影響 < 15%，延遲增加 < 100μs</li>
            <li><strong>防毒掃描：</strong>非同步處理，對即時流量影響最小</li>
            <li><strong>VPN 加密：</strong>硬體加速 AES-256，CPU 使用率 < 30%</li>
            <li><strong>流量控制：</strong>支援線速 QoS 與頻寬管理</li>
          </ul>
        </details>
        
        <details>
          <summary>🌐 如何與現有的 SIEM/SOAR 系統整合？</summary>
          <p>提供多種整合方式與標準化介面：</p>
          <ul>
            <li><strong>Syslog 輸出：</strong>支援 CEF、LEEF、JSON 格式</li>
            <li><strong>RESTful API：</strong>完整的管理與監控 API，支援自動化操作</li>
            <li><strong>Webhook：</strong>即時事件推送，觸發 SOAR 自動化流程</li>
            <li><strong>SNMP：</strong>標準 MIB 支援，整合網管系統</li>
            <li><strong>預設整合：</strong>Splunk、QRadar、ArcSight 等主流 SIEM 模板</li>
          </ul>
        </details>
        
        <details>
          <summary>🔄 威脅特徵更新機制與頻率？</summary>
          <p>採用多層次威脅情報更新機制：</p>
          <ul>
            <li><strong>自動更新：</strong>每日定期更新，無需人工干預</li>
            <li><strong>緊急推送：</strong>重大威脅 2 小時內推送更新</li>
            <li><strong>多源情報：</strong>整合商業威脅情報與開源 IOC</li>
            <li><strong>本地快取：</strong>更新失敗時使用本地快取，不影響防護能力</li>
            <li><strong>測試驗證：</strong>更新前經過實驗室驗證，確保穩定性</li>
          </ul>
        </details>
        
        <details>
          <summary>💾 日誌保存與合規性要求？</summary>
          <p>滿足各種法規的日誌保存要求：</p>
          <ul>
            <li><strong>本地儲存：</strong>可設定 3-36 個月本地保存期限</li>
            <li><strong>外部備份：</strong>支援 NFS、CIFS、S3 等外部儲存</li>
            <li><strong>加密保護：</strong>日誌檔案 AES-256 加密儲存</li>
            <li><strong>完整性驗證：</strong>數位簽章確保日誌未被竄改</li>
            <li><strong>法規模板：</strong>預設 GDPR、HIPAA、SOX 等合規報表</li>
          </ul>
        </details>
      </section>

      <!-- 10 下載資源 -->
      <section id="downloads" data-title="下載資源">
        <div class="title">
          <h2>技術文件與下載資源</h2>
          <div class="toolbar">
            <button class="icon-btn" data-copy="#downloads">🔗</button>
            <button class="icon-btn" data-collapse>－</button>
          </div>
        </div>
        
        <div class="grid cols-2">
          <div class="card">
            <b>📋 產品文件</b><br>
            <small>
              <a href="#" style="color: var(--neon-blue);">📄 產品型錄 (PDF, 8.5MB)</a><br>
              <a href="#" style="color: var(--neon-blue);">📊 技術規格表 (PDF, 2.1MB)</a><br>
              <a href="#" style="color: var(--neon-blue);">🏗️ 部署指南 (PDF, 15.2MB)</a><br>
              <a href="#" style="color: var(--neon-blue);">⚙️ 管理手冊 (PDF, 25.8MB)</a>
            </small>
          </div>
          <div class="card">
            <b>🛠️ 工具與韌體</b><br>
            <small>
              <a href="#" style="color: var(--neon-blue);">💿 最新韌體 v4.2.1 (ZIP, 156MB)</a><br>
              <a href="#" style="color: var(--neon-blue);">🖥️ 集中管理工具 (EXE, 89MB)</a><br>
              <a href="#" style="color: var(--neon-blue);">📱 行動管理 App (Android/iOS)</a><br>
              <a href="#" style="color: var(--neon-blue);">🔧 配置範本庫 (JSON, 5.2MB)</a>
            </small>
          </div>
          <div class="card">
            <b>🎓 教育資源</b><br>
            <small>
              <a href="#" style="color: var(--neon-blue);">🎬 產品介紹影片 (20分鐘)</a><br>
              <a href="#" style="color: var(--neon-blue);">👨‍🏫 線上培訓課程 (4小時)</a><br>
              <a href="#" style="color: var(--neon-blue);">📚 最佳實務白皮書</a><br>
              <a href="#" style="color: var(--neon-blue);">🏆 認證考試資訊</a>
            </small>
          </div>
          <div class="card">
            <b>🔍 技術支援</b><br>
            <small>
              <a href="#" style="color: var(--neon-blue);">❓ 知識庫 (800+ 文章)</a><br>
              <a href="#" style="color: var(--neon-blue);">🎫 線上工單系統</a><br>
              <a href="#" style="color: var(--neon-blue);">💬 社群論壇</a><br>
              <a href="#" style="color: var(--neon-blue);">📞 技術支援熱線</a>
            </small>
          </div>
        </div>
        
        <div class="alert info" style="margin-top: 20px;">
          <strong>🔒 存取權限：</strong>部分進階文件需要合作夥伴帳號或產品註冊後方可下載。如需協助請聯繫我們的技術支援團隊。
        </div>
      </section>

      <!-- 11 聯絡我們 -->
      <section id="contact" data-title="聯絡我們">
        <div class="title">
          <h2>聯絡我們</h2>
          <div class="toolbar">
            <button class="icon-btn" data-copy="#contact">🔗</button>
            <button class="icon-btn" data-collapse>－</button>
          </div>
        </div>
        
        <div class="grid cols-3" style="margin-bottom: 24px;">
          <div class="card feature">
            <div class="icon">📞</div>
            <div>
              <b>銷售諮詢</b><br>
              <small>電話：0800-123-456<br>
              Email: sales@angroup.com<br>
              服務時間：週一至五 9:00-18:00</small>
            </div>
          </div>
          <div class="card feature">
            <div class="icon">🛠️</div>
            <div>
              <b>技術支援</b><br>
              <small>電話：0800-789-012<br>
              Email: support@angroup.com<br>
              24x7 緊急支援熱線</small>
            </div>
          </div>
          <div class="card feature">
            <div class="icon">🏢</div>
            <div>
              <b>台灣總部</b><br>
              <small>台北市信義區信義路五段 7 號<br>
              台北 101 大樓 45 樓<br>
              郵遞區號：110</small>
            </div>
          </div>
        </div>
        
        <form id="contactForm" class="grid cols-2">
          <input class="card" name="name" placeholder="您的姓名 *" required />
          <input class="card" name="email" placeholder="Email 信箱 *" required type="email"/>
          <input class="card" name="company" placeholder="公司/機構名稱" />
          <input class="card" name="phone" placeholder="聯絡電話" />
          <select class="card" name="interest">
            <option value="">請選擇感興趣的產品</option>
            <option value="gwall-2000">GWall-2000 系列</option>
            <option value="gwall-5000">GWall-5000 系列</option>
            <option value="enterprise">企業級解決方案</option>
            <option value="consulting">顧問服務</option>
            <option value="training">教育訓練</option>
          </select>
          <select class="card" name="deployment">
            <option value="">預計部署時程</option>
            <option value="immediate">立即 (1個月內)</option>
            <option value="quarter">本季 (3個月內)</option>
            <option value="half-year">半年內</option>
            <option value="planning">規劃評估中</option>
          </select>
          <textarea class="card" name="message" placeholder="詳細需求說明，例如：&#10;• 現有網路環境與使用者規模&#10;• 特殊安全需求或合規要求&#10;• 預算考量與期望效益&#10;• 其他技術問題或整合需求" rows="4" style="grid-column: span 2;"></textarea>
          <div class="card" style="grid-column: span 2; display: flex; align-items: center; gap: 12px;">
            <input type="checkbox" id="privacy" name="privacy" required style="margin: 0;">
            <label for="privacy" style="font-size: 0.9rem; color: var(--muted);">
              我同意 <a href="#" style="color: var(--neon-blue);">隱私政策</a> 並願意接收產品相關資訊
            </label>
          </div>
          <button type="submit" class="btn pulse" style="grid-column: span 2;">🚀 立即索取產品資訊</button>
        </form>
        
        <div class="alert success" style="margin-top: 20px;">
          <strong>📧 快速回應承諾：</strong>我們將在收到您的詢問後 2 小時內回覆（工作時間），並安排專業技術顧問與您聯繫，提供客製化解決方案建議。
        </div>
        
        <details style="margin-top: 20px;">
          <summary>合作夥伴通路</summary>
          <div class="grid cols-2">
            <div class="card">
              <b>🤝 系統整合商夥伴</b><br>
              <small>尋找當地認證的系統整合商？我們在全台有 50+ 家合作夥伴，提供在地化服務支援。</small>
            </div>
            <div class="card">
              <b>🎓 教育訓練中心</b><br>
              <small>提供原廠認證課程、技術研習會以及客製化企業內訓服務。</small>
            </div>
          </div>
        </details>
        
        <details>
          <summary>展示中心與體驗</summary>
          <p>歡迎預約參觀我們的解決方案展示中心，現場體驗 GWall 4.0 的完整功能：</p>
          <ul>
            <li><strong>🏢 台北展示中心：</strong>台北市信義區 - 完整產品線展示與 PoC 測試環境</li>
            <li><strong>🏢 台中服務中心：</strong>台中市西屯區 - 中部地區技術支援與展示</li>
            <li><strong>🏢 高雄辦公室：</strong>高雄市前鎮區 - 南部地區客戶服務</li>
            <li><strong>☁️ 線上展示：</strong>透過 WebEx 提供遠端產品展示與技術諮詢</li>
          </ul>
        </details>
      </section>

      <!-- 12 附錄：技術詞彙 -->
      <section id="glossary" data-title="技術詞彙">
        <div class="title">
          <h2>技術詞彙表</h2>
          <div class="toolbar">
            <button class="icon-btn" data-copy="#glossary">🔗</button>
            <button class="icon-btn" data-collapse>－</button>
          </div>
        </div>
        <p class="meta">常見網路安全與 GWall 4.0 相關技術名詞解釋</p>
        
        <details open>
          <summary>核心技術縮寫</summary>
          <div class="grid cols-2">
            <div class="card">
              <b>IDS/IPS</b><br>
              <small><strong>Intrusion Detection/Prevention System</strong><br>入侵檢測/防護系統，監控並阻斷惡意網路活動</small>
            </div>
            <div class="card">
              <b>UTM</b><br>
              <small><strong>Unified Threat Management</strong><br>統一威脅管理，整合多種安全功能於單一平台</small>
            </div>
            <div class="card">
              <b>NGFW</b><br>
              <small><strong>Next-Generation Firewall</strong><br>次世代防火牆，具備應用感知與深度檢測能力</small>
            </div>
            <div class="card">
              <b>DPI</b><br>
              <small><strong>Deep Packet Inspection</strong><br>深度封包檢測，分析封包內容與應用行為</small>
            </div>
            <div class="card">
              <b>SASE</b><br>
              <small><strong>Secure Access Service Edge</strong><br>安全存取服務邊緣，雲端化網路安全架構</small>
            </div>
            <div class="card">
              <b>ZTNA</b><br>
              <small><strong>Zero Trust Network Access</strong><br>零信任網路存取，基於身份的精細化存取控制</small>
            </div>
          </div>
        </details>
        
        <details>
          <summary>VPN 技術名詞</summary>
          <div class="grid cols-2">
            <div class="card">
              <b>IPSec</b><br>
              <small><strong>Internet Protocol Security</strong><br>網路層 VPN 協定，提供端對端加密傳輸</small>
            </div>
            <div class="card">
              <b>IKE</b><br>
              <small><strong>Internet Key Exchange</strong><br>IPSec 金鑰交換協定，負責建立安全通道</small>
            </div>
            <div class="card">
              <b>SSL VPN</b><br>
              <small><strong>Secure Sockets Layer VPN</strong><br>應用層 VPN，透過 Web 瀏覽器建立安全連線</small>
            </div>
            <div class="card">
              <b>WireGuard</b><br>
              <small><strong>現代化 VPN 協定</strong><br>輕量級、高效能的新世代 VPN 解決方案</small>
            </div>
          </div>
        </details>
        
        <details>
          <summary>安全威脅類型</summary>
          <div class="grid cols-2">
            <div class="card">
              <b>APT</b><br>
              <small><strong>Advanced Persistent Threat</strong><br>進階持續威脅，長期潛伏的目標性攻擊</small>
            </div>
            <div class="card">
              <b>DDoS</b><br>
              <small><strong>Distributed Denial of Service</strong><br>分散式阻斷服務攻擊，癱瘓目標系統</small>
            </div>
            <div class="card">
              <b>Botnet</b><br>
              <small><strong>殭屍網路</strong><br>被惡意軟體控制的電腦網路，用於發動攻擊</small>
            </div>
            <div class="card">
              <b>Zero-day</b><br>
              <small><strong>零日漏洞</strong><br>尚未發布修補程式的安全漏洞</small>
            </div>
          </div>
        </details>
        
        <details>
          <summary>網路與效能指標</summary>
          <div class="grid cols-2">
            <div class="card">
              <b>Throughput</b><br>
              <small><strong>吞吐量</strong><br>單位時間內處理的資料量，通常以 Gbps 或 Mbps 表示</small>
            </div>
            <div class="card">
              <b>Latency</b><br>
              <small><strong>延遲</strong><br>封包從來源到目的地的傳輸時間</small>
            </div>
            <div class="card">
              <b>PPS</b><br>
              <small><strong>Packets Per Second</strong><br>每秒處理封包數，衡量設備處理能力</small>
            </div>
            <div class="card">
              <b>Concurrent Sessions</b><br>
              <small><strong>併發連線</strong><br>設備同時維護的網路連線數量</small>
            </div>
          </div>
        </details>
      </section>
    </main>
  </div>

  <button id="topBtn" title="回到頂部">▲</button>

<script>
// 創建粒子效果
function createParticles() {
  const container = document.getElementById('particles');
  const particleCount = 50;
  
  for (let i = 0; i < particleCount; i++) {
    const particle = document.createElement('div');
    particle.className = 'particle';
    particle.style.left = Math.random() * 100 + '%';
    particle.style.top = Math.random() * 100 + '%';
    particle.style.animationDelay = Math.random() * 6 + 's';
    particle.style.animationDuration = (Math.random() * 3 + 3) + 's';
    
    // 隨機顏色
    const colors = ['#00d4ff', '#7c3aed', '#10b981'];
    const color = colors[Math.floor(Math.random() * colors.length)];
    particle.style.background = color;
    particle.style.boxShadow = `0 0 10px ${color}`;
    
    container.appendChild(particle);
  }
}

// 初始化粒子
createParticles();

// 添加 CSS Keyframes
const style = document.createElement('style');
style.textContent = `
@keyframes ripple {
  from { width: 0; height: 0; opacity: 0.6; }
  to { width: 420px; height: 420px; opacity: 0; }
}
`;
document.head.appendChild(style);

// -------- 互動工具：ripple --------
function addRipple(e){
  const rect = e.currentTarget.getBoundingClientRect();
  const s = document.createElement('span');
  s.className='ripple';
  s.style.left = (e.clientX - rect.left) + 'px';
  s.style.top  = (e.clientY - rect.top)  + 'px';
  s.style.background = 'rgba(0,212,255,0.3)';
  s.style.position = 'absolute';
  s.style.borderRadius = '50%';
  s.style.transform = 'translate(-50%,-50%)';
  s.style.animation = 'ripple 0.6s linear';
  s.style.pointerEvents = 'none';
  e.currentTarget.style.position = 'relative';
  e.currentTarget.appendChild(s);
  setTimeout(()=>s.remove(), 650);
}

// 為所有按鈕添加ripple效果
document.addEventListener('DOMContentLoaded', function() {
  Array.from(document.querySelectorAll('.btn, .icon-btn')).forEach(b=>b.addEventListener('click',addRipple));
});

// -------- 目錄自動生成 / ScrollSpy --------
const tocLinks = document.getElementById('tocLinks');
const sections = Array.from(document.querySelectorAll('main section'));

function buildTOC(){
  tocLinks.innerHTML = sections.map(s=>`<a href="#${s.id}">🔹 ${s.dataset.title||s.querySelector('h2').textContent}</a>`).join('');
}

buildTOC();
const tocAnchors = Array.from(tocLinks.querySelectorAll('a'));

// Intersection Observer for scroll spy
const io = new IntersectionObserver(entries=>{
  entries.forEach(en=>{
    if(en.isIntersecting){
      tocAnchors.forEach(a=>a.classList.toggle('active', a.getAttribute('href')==='#'+en.target.id));
    }
  });
},{rootMargin:'-40% 0px -55% 0px',threshold:.01});

sections.forEach(s=>io.observe(s));

// 平滑捲動
document.addEventListener('click', e=>{
  const a = e.target.closest('a[href^="#"]');
  if(!a) return;
  const id = a.getAttribute('href');
  const el = document.querySelector(id);
  if(el){ 
    e.preventDefault(); 
    el.scrollIntoView({behavior:'smooth', block:'start'}); 
    
    // 添加點擊動畫
    el.style.transform = 'scale(1.02)';
    el.style.transition = 'transform 0.3s ease';
    setTimeout(() => {
      el.style.transform = 'scale(1)';
    }, 300);
  }
});

// 回頂按鈕
const topBtn = document.getElementById('topBtn');
window.addEventListener('scroll',()=>{
  const y = window.scrollY;
  topBtn.classList.toggle('show', y>400);
});

topBtn.addEventListener('click', ()=>{
  window.scrollTo({top:0,behavior:'smooth'});
  // 創建人工事件來觸發 ripple
  const rect = topBtn.getBoundingClientRect();
  const event = {
    currentTarget: topBtn,
    clientX: rect.left + rect.width/2,
    clientY: rect.top + rect.height/2
  };
  addRipple(event);
});

// 摺疊/展開工具列
Array.from(document.querySelectorAll('[data-collapse]')).forEach(b=>{
  b.addEventListener('click',()=>{
    const section = b.closest('section');
    const details = section.querySelectorAll('details');
    
    if(details.length > 0) {
      const allOpen = Array.from(details).every(d => d.open);
      details.forEach(d => d.open = !allOpen);
      b.textContent = allOpen ? '＋' : '－';
    } else {
      // 如果沒有 details，則隱藏/顯示其他內容
      section.classList.toggle('collapsed');
      const content = Array.from(section.children).slice(1);
      content.forEach(c => c.style.display = section.classList.contains('collapsed') ? 'none' : '');
      b.textContent = section.classList.contains('collapsed') ? '＋' : '－';
    }
  });
});

// 複製章節連結
Array.from(document.querySelectorAll('[data-copy]')).forEach(b=>{
  b.addEventListener('click',()=>{
    const id = b.getAttribute('data-copy');
    const url = location.origin + location.pathname + id;
    navigator.clipboard.writeText(url).then(()=>{
      const originalText = b.textContent;
      b.textContent='✅'; 
      b.style.color='#10b981';
      setTimeout(()=>{
        b.textContent = originalText;
        b.style.color='';
      },1200);
    }).catch(()=>{
      // Fallback for browsers that don't support clipboard API
      const textArea = document.createElement('textarea');
      textArea.value = url;
      document.body.appendChild(textArea);
      textArea.select();
      document.execCommand('copy');
      document.body.removeChild(textArea);
      
      const originalText = b.textContent;
      b.textContent='📋';
      b.style.color='#10b981';
      setTimeout(()=>{
        b.textContent = originalText;
        b.style.color='';
      },1200);
    });
  });
});

// Tabs 切換
Array.from(document.querySelectorAll('[data-tabs]')).forEach(group=>{
  const tabs = group.querySelectorAll('.tab');
  const panels = group.parentElement.querySelectorAll('.tab-panel');
  
  group.addEventListener('click',e=>{
    const t = e.target.closest('.tab'); 
    if(!t) return;
    
    tabs.forEach(x=>x.classList.toggle('active', x===t));
    panels.forEach(p=>p.classList.toggle('active', p.id===t.dataset.tab));
    
    // 添加切換動畫
    const activePanel = group.parentElement.querySelector('.tab-panel.active');
    if(activePanel) {
      activePanel.style.opacity = '0';
      activePanel.style.transform = 'translateY(10px)';
      setTimeout(() => {
        activePanel.style.opacity = '1';
        activePanel.style.transform = 'translateY(0)';
        activePanel.style.transition = 'opacity 0.3s ease, transform 0.3s ease';
      }, 50);
    }
  });
});

// 全展開/收合
document.getElementById('expandAll').addEventListener('click', e=>{
  const allDetails = document.querySelectorAll('details');
  const openCount = Array.from(allDetails).filter(d=>d.open).length;
  const toOpen = openCount < allDetails.length / 2; // 如果少於一半是開啟的就全部展開
  
  allDetails.forEach(d=>{
    d.open = toOpen;
    if(toOpen) {
      d.style.animation = 'details-open 0.3s ease';
    }
  });
  
  // 按鈕文字動態更新
  e.target.textContent = toOpen ? '收合全部' : '展開全部';
  setTimeout(() => {
    e.target.textContent = '展開全部';
  }, 3000);
});

// 搜尋功能
const searchInput = document.getElementById('searchInput');
const clearSearch = document.getElementById('clearSearch');

function performSearch() {
  const query = searchInput.value.trim().toLowerCase();
  let hasResults = false;
  
  sections.forEach(section => {
    const content = section.textContent.toLowerCase();
    const shouldShow = !query || content.includes(query);
    
    section.style.display = shouldShow ? '' : 'none';
    
    if(shouldShow && query) {
      hasResults = true;
      // 高亮搜尋結果
      section.style.borderColor = 'var(--neon-blue)';
      section.style.boxShadow = '0 0 20px rgba(0,212,255,0.3)';
      setTimeout(() => {
        section.style.borderColor = '';
        section.style.boxShadow = '';
      }, 2000);
    }
  });
  
  // 如果有搜尋但沒有結果，顯示提示
  const noResults = document.getElementById('noResults');
  if(noResults) noResults.remove();
  
  if(query && !hasResults) {
    const noResultsDiv = document.createElement('div');
    noResultsDiv.id = 'noResults';
    noResultsDiv.className = 'alert warning';
    noResultsDiv.innerHTML = `<strong>🔍 找不到相關內容</strong><br>請嘗試其他關鍵字，例如：防火牆、VPN、IPS、零信任等`;
    document.querySelector('main').appendChild(noResultsDiv);
  }
}

let searchTimeout;
searchInput.addEventListener('input', () => {
  clearTimeout(searchTimeout);
  searchTimeout = setTimeout(performSearch, 300); // 延遲搜尋避免過於頻繁
});

clearSearch.addEventListener('click', () => {
  searchInput.value = '';
  performSearch();
  searchInput.focus();
});

// 表單提交
document.getElementById('contactForm').addEventListener('submit', e => {
  e.preventDefault();
  
  const submitBtn = e.target.querySelector('button[type="submit"]');
  const formData = new FormData(e.target);
  
  // 檢查必填欄位
  const requiredFields = e.target.querySelectorAll('[required]');
  let isValid = true;
  
  requiredFields.forEach(field => {
    if(!field.value.trim()) {
      field.style.borderColor = '#ef4444';
      isValid = false;
    } else {
      field.style.borderColor = '';
    }
  });
  
  if(!isValid) {
    submitBtn.textContent = '❌ 請填寫必填欄位';
    submitBtn.style.background = 'linear-gradient(135deg, #ef4444, #dc2626)';
    setTimeout(() => {
      submitBtn.textContent = '🚀 立即索取產品資訊';
      submitBtn.style.background = '';
    }, 3000);
    return;
  }
  
  // 模擬送出過程
  submitBtn.textContent = '⏳ 處理中...';
  submitBtn.disabled = true;
  
  setTimeout(() => {
    submitBtn.textContent = '✅ 已送出';
    submitBtn.style.background = 'linear-gradient(135deg, #10b981, #059669)';
    
    setTimeout(() => {
      // 顯示成功訊息
      const successMsg = document.createElement('div');
      successMsg.className = 'alert success';
      successMsg.innerHTML = `
        <strong>🎉 感謝您的詢問！</strong><br>
        我們已收到您的需求，專業顧問將在 2 小時內與您聯繫。<br>
        同時，您也會收到一封包含產品資訊的 Email。
      `;
      e.target.parentNode.insertBefore(successMsg, e.target);
      
      // 重置表單
      e.target.reset();
      submitBtn.textContent = '🚀 立即索取產品資訊';
      submitBtn.style.background = '';
      submitBtn.disabled = false;
      
      // 3秒後移除成功訊息
      setTimeout(() => {
        successMsg.remove();
      }, 8000);
    }, 1000);
  }, 2000);
});

// 滾動視差效果
let ticking = false;
function updateScrollEffects() {
  const scrolled = window.pageYOffset;
  const rate = scrolled * -0.2;
  
  // 背景視差效果
  document.body.style.backgroundPosition = `center ${rate}px`;
  
  // 卡片浮起效果
  const cards = document.querySelectorAll('.card');
  cards.forEach((card, index) => {
    const rect = card.getBoundingClientRect();
    const isVisible = rect.top < window.innerHeight && rect.bottom > 0;
    
    if (isVisible) {
      const progress = Math.max(0, Math.min(1, (window.innerHeight - rect.top) / window.innerHeight));
      const transform = Math.max(0, (1 - progress) * 10);
      const opacity = Math.max(0.3, progress);
      
      card.style.transform = `translateY(${transform}px)`;
      card.style.opacity = opacity;
    }
  });
  
  ticking = false;
}

window.addEventListener('scroll', () => {
  if (!ticking) {
    requestAnimationFrame(updateScrollEffects);
    ticking = true;
  }
});

// 進度條動畫
const progressBars = document.querySelectorAll('.progress-fill');
const progressObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const width = entry.target.style.width;
      entry.target.style.width = '0%';
      setTimeout(() => {
        entry.target.style.width = width;
        entry.target.style.transition = 'width 2s ease-out';
      }, 100);
    }
  });
}, { threshold: 0.1 });

progressBars.forEach(bar => progressObserver.observe(bar));

// 統計數字動畫
function animateNumbers() {
  const statNumbers = document.querySelectorAll('.stat-card .number');
  statNumbers.forEach(element => {
    const finalNumber = element.textContent;
    const numericValue = parseFloat(finalNumber.replace(/[^\d.]/g, ''));
    const suffix = finalNumber.replace(/[\d.]/g, '');
    
    if(!isNaN(numericValue)) {
      let current = 0;
      const increment = numericValue / 30;
      const timer = setInterval(() => {
        current += increment;
        if(current >= numericValue) {
          element.textContent = finalNumber;
          clearInterval(timer);
        } else {
          element.textContent = Math.floor(current) + suffix;
        }
      }, 50);
    }
  });
}

// 當統計卡片進入視窗時觸發動畫
const statsObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      animateNumbers();
      statsObserver.unobserve(entry.target);
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.stat-card').forEach(card => {
  statsObserver.observe(card);
});

// 初始化完成後的設置
document.addEventListener('DOMContentLoaded', function() {
  // 初始化所有進度條為0
  progressBars.forEach(bar => {
    bar.style.width = '0%';
  });
  
  console.log('🛡️ GWall 4.0 網頁已載入完成');
});
</script>

<!-- 回到頂部按鈕 -->
<button id="topBtn">↑</button>

<script>
// 取得按鈕
const topBtn = document.getElementById("topBtn");

// 監聽滾動事件，超過 200px 才顯示
window.addEventListener("scroll", () => {
  if (window.scrollY > 200) {
    topBtn.classList.add("show");
  } else {
    topBtn.classList.remove("show");
  }
});

// 點擊回到頂部
topBtn.addEventListener("click", () => {
  window.scrollTo({
    top: 0,
    behavior: "smooth"
  });
});
</script>

<style>
/* 回到頂部樣式 */
#topBtn {
  position: fixed !important;
  right: 24px;
  bottom: 24px;
  z-index: 9999;
  border: none;
  border-radius: 50%;
  width: 52px;
  height: 52px;
  display: grid;
  place-items: center;
  cursor: pointer;
  background: linear-gradient(135deg, #00d4ff, #7c3aed);
  color: #fff;
  font-size: 18px;
  font-weight: bold;
  opacity: 0;
  pointer-events: none;
  transition: all 0.3s ease;
  box-shadow: 0 0 25px rgba(0,212,255,0.4);
}

/* 顯示狀態 */
#topBtn.show {
  opacity: 1;
  pointer-events: auto;
}

/* hover 效果 */
#topBtn:hover {
  transform: translateY(-4px);
  box-shadow: 0 0 35px rgba(0,212,255,0.6), 0 8px 25px rgba(0,0,0,0.3);
}
</style>


</body>
</html>
