<!DOCTYPE html>
<html lang="zh-Hant">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>GWall 4.0 網路安全解決方案｜互動式單頁</title>
<style>
  :root{
    --bg:#0b0f17;          /* 深色背景 */
    --panel:#0f1522;       /* 卡片底色 */
    --muted:#8b98a5;       /* 次文字 */
    --line:#243148;        /* 邊線 */
    --primary:#58a6ff;     /* 主色 */
    --primary-2:#1f6feb;   /* 主色深 */
    --accent:#2ea043;      /* 強調色 */
    --warn:#ffb86b;
  }
  *{box-sizing:border-box}
  html,body{height:100%}
  body{
    margin:0;font-family:Segoe UI, Roboto, Noto Sans TC, "Microsoft JhengHei", system-ui, -apple-system, sans-serif;
    background:radial-gradient(1000px 600px at 20% -10%, rgba(47,88,160,.25), transparent 60%),
               radial-gradient(1200px 900px at 120% 10%, rgba(50,205,140,.12), transparent 50%),
               var(--bg);
    color:#c9d1d9; overflow-x:hidden;
  }
  /* 背景動態網格 */
  .grid-bg::before{
    content:"";position:fixed;inset:0;pointer-events:none;opacity:.35;
    background-image: linear-gradient(to right, rgba(255,255,255,.04) 1px, transparent 1px),
                      linear-gradient(to bottom, rgba(255,255,255,.04) 1px, transparent 1px);
    background-size: 40px 40px; transform:translateZ(0);
  }
  header{
    position:sticky;top:0;z-index:10;
    background:linear-gradient(90deg, var(--primary-2), var(--primary));
    color:#fff;padding:14px 18px;display:flex;align-items:center;gap:12px;justify-content:space-between;
    box-shadow:0 10px 24px rgba(0,0,0,.35);
  }
  .brand{display:flex;align-items:center;gap:10px;font-weight:700;letter-spacing:.5px}
  .brand .dot{width:10px;height:10px;border-radius:50%;background:conic-gradient(from 90deg, #97d0ff, #2ea043, #97d0ff)}
  .search{max-width:520px;flex:1;display:flex;gap:8px}
  .search input{flex:1;background:#0d1320;border:1px solid #234; color:#c9d1d9;padding:10px 12px;border-radius:10px;outline:none}
  .btn{position:relative; border:1px solid #3a5b9a;background:#0d1320;color:#cfe6ff;padding:10px 14px;border-radius:12px;cursor:pointer;transition:.25s;overflow:hidden}
  .btn:hover{transform:translateY(-1px);box-shadow:0 8px 24px rgba(42,125,255,.25)}
  .btn:active{transform:translateY(0)}
  /* ripple */
  .btn span.ripple{position:absolute;border-radius:50%;transform:translate(-50%,-50%);animation:ripple .6s linear; background:rgba(88,166,255,.35)}
  @keyframes ripple{from{width:0;height:0;opacity:.6} to{width:420px;height:420px;opacity:0}}

  .layout{display:grid;grid-template-columns:280px 1fr;gap:20px;max-width:1400px;margin:0 auto;padding:20px}
  @media (max-width: 980px){.layout{grid-template-columns:1fr}.sidebar{position:static;height:auto}}

  .sidebar{position:sticky;top:72px;height:calc(100dvh - 86px);overflow:auto;background:#0e1421;border:1px solid var(--line);border-radius:16px;padding:14px}
  .toc h3{margin:6px 10px 12px;font-size:14px;color:var(--muted);font-weight:600}
  .toc a{display:flex;align-items:center;gap:8px;text-decoration:none;color:#bcd6ff;padding:10px 12px;border-radius:10px;border:1px solid transparent;transition:.2s}
  .toc a:hover{background:#0a1222;border-color:#21324f}
  .toc a.active{background:linear-gradient(90deg, rgba(31,111,235,.25), rgba(88,166,255,.1));border-color:#2a4e8b}

  main{min-height:70vh}
  section{background:var(--panel);border:1px solid var(--line);border-radius:16px;padding:22px;margin-bottom:20px;position:relative;overflow:hidden}
  section .title{display:flex;align-items:center;gap:10px;justify-content:space-between}
  h2{margin:.2rem 0 1rem;font-size:1.35rem;color:#d7e9ff}
  .meta{color:var(--muted);font-size:.9rem}
  .chip{font-size:.75rem;padding:4px 8px;border-radius:999px;background:#0c162d;border:1px solid #1f3b6b;color:#96b9ff}

  /* 可收合區域 */
  details{border:1px dashed #294067;border-radius:12px;padding:12px;margin:10px 0;background:#0c1322}
  details summary{cursor:pointer;list-style:none}
  details[open]{animation:open .25s ease}
  @keyframes open{from{opacity:.5;transform:translateY(-2px)}to{opacity:1;transform:none}}

  .grid{display:grid;gap:12px}
  .grid.cols-3{grid-template-columns:repeat(3,1fr)}
  .grid.cols-2{grid-template-columns:repeat(2,1fr)}
  @media (max-width: 960px){.grid.cols-3{grid-template-columns:1fr}.grid.cols-2{grid-template-columns:1fr}}

  .card{background:#0e1627;border:1px solid #243453;border-radius:14px;padding:14px;transition:.25s}
  .card:hover{transform:translateY(-2px);box-shadow:0 12px 28px rgba(0,0,0,.35)}

  .feature{display:flex;gap:12px}
  .feature .icon{width:38px;height:38px;border-radius:10px;background:linear-gradient(135deg,#1f6feb33,#58a6ff22);display:grid;place-items:center;border:1px solid #2a4e8b;color:#9fd1ff}

  .tag{display:inline-block;margin-right:8px;margin-bottom:6px}
  .kbd{padding:2px 6px;border:1px solid #3a4b63;border-bottom-width:2px;border-radius:6px;background:#0a1221;color:#cfe2ff;font-family:ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas}

  /* 回頂 */
  #topBtn{position:fixed;right:22px;bottom:22px;z-index:9;border:none;border-radius:50%;width:44px;height:44px;display:grid;place-items:center;cursor:pointer;background:linear-gradient(135deg,var(--primary-2),var(--primary));color:#fff;box-shadow:0 10px 26px rgba(0,0,0,.45);opacity:0;pointer-events:none;transition:.25s}
  #topBtn.show{opacity:1;pointer-events:auto}

  /* 區塊內工具列 */
  .toolbar{display:flex;gap:8px;align-items:center}
  .icon-btn{background:#0a1221;border:1px solid #20324f;border-radius:10px;padding:8px;cursor:pointer;color:#a8c9ff}
  .icon-btn:hover{filter:brightness(1.15)}

  /* Tabs */
  .tabs{display:flex;gap:6px;margin:8px 0 14px}
  .tab{padding:8px 12px;border-radius:10px;border:1px solid #253a62;background:#0a1322;color:#b9d0ff;cursor:pointer}
  .tab.active{background:linear-gradient(90deg, rgba(31,111,235,.35), rgba(88,166,255,.2));border-color:#2a4e8b}
  .tab-panel{display:none}
  .tab-panel.active{display:block}

  /* 小動畫 */
  .pulse{box-shadow:0 0 0 0 rgba(46,160,67,.45);animation:pulse 2s infinite}
  @keyframes pulse{0%{box-shadow:0 0 0 0 rgba(46,160,67,.45)}70%{box-shadow:0 0 0 12px rgba(46,160,67,0)}100%{box-shadow:0 0 0 0 rgba(46,160,67,0)}}
</style>
</head>
<body class="grid-bg">
  <header>
    <div class="brand"><span class="dot"></span> GWall 4.0 網路安全解決方案</div>
    <div class="search">
      <input id="searchInput" placeholder="搜尋章節 / 關鍵字（例如：VPN、IPS、規格）"/>
      <button class="btn" id="clearSearch">清除</button>
    </div>
    <button class="btn" id="expandAll">展開/收合全部</button>
  </header>

  <div class="layout">
    <aside class="sidebar">
      <nav class="toc" id="toc">
        <h3>目錄</h3>
        <div id="tocLinks"></div>
      </nav>
    </aside>

    <main id="content">
      <!-- 1 產品概述 -->
      <section id="intro" data-title="產品概述">
        <div class="title">
          <h2>產品概述</h2>
          <div class="toolbar">
            <button class="icon-btn" data-copy="#intro">🔗</button>
            <button class="icon-btn" data-collapse>－</button>
          </div>
        </div>
        <p class="meta">請將 PDF「GWall 4.0 網路安全解決方案」的前言與整體定位貼到此處。</p>
        <details open>
          <summary>重點摘要</summary>
          <div class="grid cols-3">
            <div class="card feature"><div class="icon">⚡</div><div><b>高效能安全閘道</b><br><small>整合防火牆、VPN、IPS/IDS 等核心能力。</small></div></div>
            <div class="card feature"><div class="icon">🧭</div><div><b>彈性部署</b><br><small>多種網路拓撲與模式，因應企業規模擴張。</small></div></div>
            <div class="card feature"><div class="icon">📊</div><div><b>可視化管理</b><br><small>儀表板、告警、報表與日誌分析。</small></div></div>
          </div>
        </details>
      </section>

      <!-- 2 解決方案架構 -->
      <section id="architecture" data-title="解決方案架構">
        <div class="title"><h2>解決方案架構</h2><div class="toolbar"><button class="icon-btn" data-copy="#architecture">🔗</button><button class="icon-btn" data-collapse>－</button></div></div>
        <p class="meta">放置 PDF 中的整體架構圖解與說明（核心模組、資料流、邊緣/核心/雲端整合）。</p>
        <details open>
          <summary>架構重點</summary>
          <ul>
            <li>北向/南向流量控管、東西向流量微分段。</li>
            <li>威脅情報同步、政策集中管理。</li>
            <li>高可用性（HA）與故障切換設計。</li>
          </ul>
        </details>
      </section>

      <!-- 3 核心功能 -->
      <section id="features" data-title="核心功能">
        <div class="title"><h2>核心功能</h2><div class="toolbar"><button class="icon-btn" data-copy="#features">🔗</button><button class="icon-btn" data-collapse>－</button></div></div>
        <div class="tabs" data-tabs>
          <button class="tab active" data-tab="f1">防火牆 / NAT</button>
          <button class="tab" data-tab="f2">VPN（IPsec / SSL）</button>
          <button class="tab" data-tab="f3">入侵偵測/防禦（IDS/IPS）</button>
          <button class="tab" data-tab="f4">應用控制 / URL 過濾</button>
          <button class="tab" data-tab="f5">日誌 / 報表 / 告警</button>
        </div>
        <div class="tab-panel active" id="f1">
          <div class="grid cols-2">
            <div class="card"><b>狀態檢查</b><br><small>基於連線狀態的策略判斷；支援 Zone/Address 物件化管理。</small></div>
            <div class="card"><b>進階 NAT</b><br><small>SNAT/DNAT/Port-Forward；雙線路/多 WAN 規則。</small></div>
          </div>
        </div>
        <div class="tab-panel" id="f2">
          <div class="grid cols-2">
            <div class="card"><b>站點到站點</b><br><small>相容主流設備；策略式與路由式 VPN。</small></div>
            <div class="card"><b>遠端存取</b><br><small>SSL VPN 入口、雙因子驗證、端點檢查。</small></div>
          </div>
        </div>
        <div class="tab-panel" id="f3">
          <div class="grid cols-2">
            <div class="card"><b>威脅特徵</b><br><small>定期更新簽章；自訂例外。</small></div>
            <div class="card"><b>阻斷/告警</b><br><small>自動封鎖、速率限制與事件聯防。</small></div>
          </div>
        </div>
        <div class="tab-panel" id="f4">
          <div class="grid cols-2">
            <div class="card"><b>L7 辨識</b><br><small>常見應用與自訂分類。</small></div>
            <div class="card"><b>政策控管</b><br><small>工作時段限制、黑白名單、風險分級。</small></div>
          </div>
        </div>
        <div class="tab-panel" id="f5">
          <div class="grid cols-2">
            <div class="card"><b>集中日誌</b><br><small>支援 Syslog/CEF；匯出 CSV / PDF 報表。</small></div>
            <div class="card"><b>即時告警</b><br><small>Email / Webhook；閾值/事件觸發。</small></div>
          </div>
        </div>
      </section>

      <!-- 4 進階安全 -->
      <section id="advanced" data-title="進階安全">
        <div class="title"><h2>進階安全</h2><div class="toolbar"><button class="icon-btn" data-copy="#advanced">🔗</button><button class="icon-btn" data-collapse>－</button></div></div>
        <details open>
          <summary>零信任與微分段</summary>
          <ul>
            <li>以身分與裝置狀態為核心之存取控管。</li>
            <li>東西向流量政策化，降低橫向移動風險。</li>
          </ul>
        </details>
        <details>
          <summary>防護與資安整合</summary>
          <ul>
            <li>與端點 EDR/AV、SIEM/SOAR 整合（請依 PDF 內容補全）。</li>
            <li>威脅情資（TIP）同步。</li>
          </ul>
        </details>
      </section>

      <!-- 5 部署情境 -->
      <section id="scenarios" data-title="部署情境">
        <div class="title"><h2>部署情境</h2><div class="toolbar"><button class="icon-btn" data-copy="#scenarios">🔗</button><button class="icon-btn" data-collapse>－</button></div></div>
        <div class="grid cols-3">
          <div class="card"><b>單一據點</b><br><small>邊界防護、上網管理與基本 VPN。</small></div>
          <div class="card"><b>多據點/分公司</b><br><small>Hub-and-Spoke、MPLS/SD-WAN 並行策略。</small></div>
          <div class="card"><b>資料中心/雲</b><br><small>混合雲、跨區冗餘與專線互連。</small></div>
        </div>
      </section>

      <!-- 6 硬體規格 -->
      <section id="specs" data-title="硬體規格">
        <div class="title"><h2>硬體規格</h2><div class="toolbar"><button class="icon-btn" data-copy="#specs">🔗</button><button class="icon-btn" data-collapse>－</button></div></div>
        <p class="meta">請將 PDF 的規格表逐列貼入下方（型號、介面、吞吐量、同時連線、尺寸、功耗等）。</p>
        <details open>
          <summary>規格表（範例結構）</summary>
          <div class="grid cols-2">
            <div class="card"><b>介面</b><br><small>例如：5× RJ45、1× SFP（依 PDF 調整）。</small></div>
            <div class="card"><b>防火牆效能</b><br><small>例如：2.5 Gbps（依 PDF 調整）。</small></div>
            <div class="card"><b>最大連線/每秒新連線</b><br><small>請填入 PDF 數值。</small></div>
            <div class="card"><b>作業溫濕度 / 尺寸 / 重量</b><br><small>請填入 PDF 數值。</small></div>
          </div>
        </details>
      </section>

      <!-- 7 授權與維護 -->
      <section id="licensing" data-title="授權與維護">
        <div class="title"><h2>授權與維護</h2><div class="toolbar"><button class="icon-btn" data-copy="#licensing">🔗</button><button class="icon-btn" data-collapse>－</button></div></div>
        <ul>
          <li>授權方案與到期續約（依 PDF 條列）。</li>
          <li>維護與技術支援 SLA。</li>
          <li>韌體/特徵庫更新頻率。</li>
        </ul>
      </section>

      <!-- 8 成功案例 -->
      <section id="cases" data-title="成功案例">
        <div class="title"><h2>成功案例</h2><div class="toolbar"><button class="icon-btn" data-copy="#cases">🔗</button><button class="icon-btn" data-collapse>－</button></div></div>
        <details open>
          <summary>業界案例（請依 PDF 補充）</summary>
          <div class="grid cols-3">
            <div class="card"><b>製造業</b><br><small>工廠據點互聯、零停機維運。</small></div>
            <div class="card"><b>教育業</b><br><small>校園網路分區與上網行為管理。</small></div>
            <div class="card"><b>醫療業</b><br><small>法規遵循與病歷系統保護。</small></div>
          </div>
        </details>
      </section>

      <!-- 9 常見問題 -->
      <section id="faq" data-title="常見問題">
        <div class="title"><h2>常見問題（FAQ）</h2><div class="toolbar"><button class="icon-btn" data-copy="#faq">🔗</button><button class="icon-btn" data-collapse>－</button></div></div>
        <details open>
          <summary>是否支援高可用性（HA）？</summary>
          <p>支援（依 PDF 實際功能補充：Active-Standby / Active-Active、心跳埠、虛擬 IP 之類）。</p>
        </details>
        <details>
          <summary>是否支援 AD 整合與 2FA？</summary>
          <p>支援（依 PDF 補充：LDAP/AD、RADIUS、OTP、硬體金鑰等）。</p>
        </details>
      </section>

      <!-- 10 下載資源 -->
      <section id="downloads" data-title="下載資源">
        <div class="title"><h2>下載資源</h2><div class="toolbar"><button class="icon-btn" data-copy="#downloads">🔗</button><button class="icon-btn" data-collapse>－</button></div></div>
        <ul>
          <li>型錄 / 規格書（連結到公司網站或檔案伺服器）。</li>
          <li>韌體 / 管理解決方案工具。</li>
        </ul>
      </section>

      <!-- 11 聯絡我們 -->
      <section id="contact" data-title="聯絡我們">
        <div class="title"><h2>聯絡我們</h2><div class="toolbar"><button class="icon-btn" data-copy="#contact">🔗</button><button class="icon-btn" data-collapse>－</button></div></div>
        <form id="contactForm" class="grid cols-2">
          <input class="card" name="name" placeholder="您的姓名" required />
          <input class="card" name="email" placeholder="Email" required type="email"/>
          <input class="card" name="company" placeholder="公司/單位" />
          <input class="card" name="phone" placeholder="聯絡電話" />
          <textarea class="card" name="message" placeholder="您的需求 / 想法" rows="4"></textarea>
          <button type="submit" class="btn pulse">送出需求</button>
        </form>
        <p class="meta">送出後僅在本機顯示成功訊息（可改寫為實際 API）。</p>
      </section>
    </main>
  </div>

  <button id="topBtn" title="回頂">▲</button>

<script>
// -------- 互動工具：ripple --------
function addRipple(e){
  const rect = e.currentTarget.getBoundingClientRect();
  const s = document.createElement('span');
  s.className='ripple';
  s.style.left = (e.clientX - rect.left) + 'px';
  s.style.top  = (e.clientY - rect.top)  + 'px';
  e.currentTarget.appendChild(s);
  setTimeout(()=>s.remove(), 650);
}
Array.from(document.querySelectorAll('.btn')).forEach(b=>b.addEventListener('click',addRipple));

// -------- 目錄自動生成 / ScrollSpy --------
const tocLinks = document.getElementById('tocLinks');
const sections = Array.from(document.querySelectorAll('main section'));
function buildTOC(){
  tocLinks.innerHTML = sections.map(s=>`<a href="#${s.id}">📄 ${s.dataset.title||s.querySelector('h2').textContent}</a>`).join('');
}
buildTOC();
const tocAnchors = Array.from(tocLinks.querySelectorAll('a'));

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
  if(el){ e.preventDefault(); el.scrollIntoView({behavior:'smooth', block:'start'}); }
});

// 回頂按鈕
const topBtn = document.getElementById('topBtn');
window.addEventListener('scroll',()=>{
  const y = window.scrollY;
  topBtn.classList.toggle('show', y>400);
});
topBtn.addEventListener('click', ()=>window.scrollTo({top:0,behavior:'smooth'}));

// 摺疊/展開工具列
Array.from(document.querySelectorAll('[data-collapse]')).forEach(b=>{
  b.addEventListener('click',()=>{
    const section = b.closest('section');
    const d = section.querySelector('details');
    if(!d){ section.classList.toggle('collapsed'); Array.from(section.children).forEach((c,i)=>{if(i>0)c.toggleAttribute('hidden');}); return; }
    d.open = !d.open;
  });
});

// 複製章節連結
Array.from(document.querySelectorAll('[data-copy]')).forEach(b=>{
  b.addEventListener('click',()=>{
    const id = b.getAttribute('data-copy');
    const url = location.origin + location.pathname + id;
    navigator.clipboard.writeText(url).then(()=>{
      b.textContent='✅'; setTimeout(()=>b.textContent='🔗',1200);
    });
  });
});

// Tabs 切換
Array.from(document.querySelectorAll('[data-tabs]')).forEach(group=>{
  const tabs = group.querySelectorAll('.tab');
  const panels = group.parentElement.querySelectorAll('.tab-panel');
  group.addEventListener('click',e=>{
    const t = e.target.closest('.tab'); if(!t) return;
    tabs.forEach(x=>x.classList.toggle('active', x===t));
    panels.forEach(p=>p.classList.toggle('active', p.id===t.dataset.tab));
  });
});

// 全展開/收合
document.getElementById('expandAll').addEventListener('click', e=>{
  const openCount = Array.from(document.querySelectorAll('details')).filter(d=>d.open).length;
  const toOpen = openCount===0;
  document.querySelectorAll('details').forEach(d=>d.open = toOpen);
});

// 搜尋（即時篩選章節內容）
const searchInput=document.getElementById('searchInput');
const clearSearch=document.getElementById('clearSearch');
function highlight(text, q){
  if(!q) return text;
  return text.replace(new RegExp(q.replace(/[.*+?^${}()|[\]\\]/g,'\\$&'),'gi'), m=>`<mark style="background:rgba(88,166,255,.35);padding:0 .2em;border-radius:4px">${m}</mark>`);
}
let lastQ="";
searchInput.addEventListener('input',()=>{
  const q = searchInput.value.trim();
  if(q===lastQ) return; lastQ=q;
  sections.forEach(sec=>{
    const raw = sec.innerText.toLowerCase();
    const show = raw.includes(q.toLowerCase());
    sec.style.display = show?'' : 'none';
  });
});
clearSearch.addEventListener('click',()=>{searchInput.value='';searchInput.dispatchEvent(new Event('input'));});

// 表單提交（示範）
document.getElementById('contactForm').addEventListener('submit', e=>{
  e.preventDefault();
  alert('✅ 已收到您的需求（示範）。可將此區改為實際送出 API。');
  e.target.reset();
});
</script>
</body>
</html>
