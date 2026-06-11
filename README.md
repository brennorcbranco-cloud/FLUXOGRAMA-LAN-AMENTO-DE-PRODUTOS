<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Rennova — Central de Projetos</title>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@2.44.0/tabler-icons.min.css">
<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Space+Grotesk:wght@400;500;700&display=swap');
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}

/* ── SHARED ── */
:root{
  --bg:#0f1117;--s1:#1a1d27;--s2:#222535;--s3:#2a2d3e;
  --border:#2e3248;--border2:#3a3f58;
  --accent:#4f7fff;--green:#22c97a;--orange:#f5a623;--red:#e05c5c;
  --text:#e8eaf0;--text2:#8b90a8;--text3:#555a74;--white:#fff;
}
html,body{height:100%;background:var(--bg);color:var(--text);font-family:'Inter',sans-serif;overflow:hidden}
.page{position:fixed;inset:0;display:none;flex-direction:column;background:var(--bg)}
.page.active{display:flex}

/* ── HOME ── */
#home{align-items:center;justify-content:center}
.home-inner{display:flex;flex-direction:column;align-items:center;gap:0;max-width:760px;width:100%;padding:40px 24px}
.home-logo{font-family:'Space Grotesk',sans-serif;font-size:13px;font-weight:700;letter-spacing:3px;text-transform:uppercase;color:var(--text3);margin-bottom:32px;display:flex;align-items:center;gap:10px}
.home-logo-dot{width:8px;height:8px;border-radius:50%;background:var(--accent)}
.home-title{font-family:'Space Grotesk',sans-serif;font-size:38px;font-weight:700;color:var(--white);text-align:center;line-height:1.18;letter-spacing:-1px;margin-bottom:12px}
.home-title span{color:var(--accent)}
.home-sub{font-size:15px;color:var(--text2);text-align:center;line-height:1.6;margin-bottom:48px;max-width:480px}
.home-cards{display:grid;grid-template-columns:1fr 1fr;gap:16px;width:100%}
.home-card{background:var(--s1);border:1px solid var(--border);border-radius:16px;padding:32px 28px;cursor:pointer;transition:all .2s;position:relative;overflow:hidden}
.home-card:hover{border-color:var(--border2);background:var(--s2);transform:translateY(-3px)}
.home-card:hover .hc-arrow{transform:translate(3px,-3px)}
.home-card.accent-flow{border-top:3px solid var(--accent)}
.home-card.accent-kanban{border-top:3px solid var(--green)}
.hc-icon{font-size:32px;margin-bottom:16px;display:block}
.hc-title{font-family:'Space Grotesk',sans-serif;font-size:20px;font-weight:700;color:var(--white);margin-bottom:8px}
.hc-desc{font-size:13px;color:var(--text2);line-height:1.6;margin-bottom:20px}
.hc-tags{display:flex;flex-wrap:wrap;gap:6px;margin-bottom:20px}
.hc-tag{font-size:10px;font-weight:600;padding:3px 9px;border-radius:20px;border:1px solid var(--border);color:var(--text3)}
.hc-cta{display:flex;align-items:center;gap:6px;font-size:13px;font-weight:600}
.hc-arrow{transition:transform .2s}
.home-footer{margin-top:36px;font-size:11px;color:var(--text3);text-align:center}

/* ── BACK BUTTON (shared between sub-pages) ── */
.back-btn{background:var(--s2);border:1px solid var(--border2);border-radius:8px;color:var(--text2);font-size:12px;font-weight:500;padding:6px 14px;cursor:pointer;display:flex;align-items:center;gap:6px;transition:all .15s;white-space:nowrap}
.back-btn:hover{background:var(--s3);color:var(--text);border-color:var(--accent)}

/* scrollbar */
::-webkit-scrollbar{width:4px;height:4px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:var(--border2);border-radius:2px}

</style>

<style>
#flow-page > .canvas-wrapper { flex: 1; overflow: auto; min-height: 0; }
#kanban-page > .main { flex: 1; min-height: 0; }
</style>

<!-- FLOW STYLES (scoped) -->
<style id="flow-styles">
#flow-page *{box-sizing:border-box}



:root{
  --bg:#0f1117;--surface:#1a1d27;--surface2:#222535;--border:#2e3248;
  --accent:#4f7fff;--green:#22c97a;--orange:#f5a623;--red:#e05c5c;
  --text:#e8eaf0;--text2:#8b90a8;--text3:#555a74;--white:#fff;
}
#flow-page{overflow-y:auto}

/* HEADER */
header{background:var(--surface);border-bottom:1px solid var(--border);padding:14px 28px;display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;z-index:100}
.logo{font-family:'Space Grotesk',sans-serif;font-size:17px;font-weight:700;color:var(--white)}
.logo span{color:var(--accent)}
.hbadge{background:#1e2640;border:1px solid var(--border);border-radius:20px;padding:3px 11px;font-size:10px;color:var(--text2);font-weight:500}
.hbadge.v{border-color:#22c97a44;color:var(--green)}
.header-meta{display:flex;gap:10px;align-items:center}

/* CANVAS */
.canvas-wrapper{overflow-x:auto;overflow-y:auto;flex:1;padding:28px 14px 80px}
.flow{min-width:1260px;max-width:1480px;margin:0 auto;display:flex;flex-direction:column}

/* PHASE */
.ph{font-family:'Space Grotesk',sans-serif;font-size:9px;font-weight:700;letter-spacing:2.5px;text-transform:uppercase;color:var(--text3);margin-bottom:7px;padding-left:2px;margin-top:4px}

/* ARROWS */
.ad{display:flex;justify-content:center;padding:3px 0}
.ad svg{display:block}
.ar{display:flex;align-items:center;padding:0 2px;flex-shrink:0}
.ar svg{display:block}

/* NODE */
.node{border:1.5px solid var(--border);border-radius:10px;padding:11px 13px;min-width:148px;max-width:192px;flex:1;cursor:pointer;transition:border-color .18s,box-shadow .18s,transform .13s;position:relative}
.node:hover{border-color:var(--accent);box-shadow:0 0 0 3px rgba(79,127,255,.13);transform:translateY(-2px);z-index:10}
.node.comex   {border-color:#3a4a6b;background:#141a2e}
.node.mkt     {border-color:#3a2f6b;background:#16142b}
.node.reg     {border-color:#2f5a3a;background:#121e16}
.node.jur     {border-color:#5a4a2f;background:#1e1a12}
.node.house   {border-color:#4a2f5a;background:#1a1220}
.node.fiscal  {border-color:#5a3a2f;background:#1e1210}
.node.cad     {border-color:#2f4a5a;background:#101e26}
.node.qual    {border-color:#3a5a3a;background:#121e12}
.node.go      {border-color:var(--green);background:#0e1f14}
.node.start   {border-color:var(--accent);background:#0f1524}
.node-icon{font-size:15px;margin-bottom:5px;display:block}
.node-owner{font-size:8px;font-weight:700;letter-spacing:1.4px;text-transform:uppercase;margin-bottom:4px;opacity:.85}
.node.comex  .node-owner{color:#7ea8ff}
.node.mkt    .node-owner{color:#a07eff}
.node.reg    .node-owner{color:#44cc88}
.node.jur    .node-owner{color:#ffcc55}
.node.house  .node-owner{color:#cc77ff}
.node.fiscal .node-owner{color:#ff9955}
.node.cad    .node-owner{color:#55aacc}
.node.qual   .node-owner{color:#88cc55}
.node.start  .node-owner{color:var(--accent)}
.node.go     .node-owner{color:var(--green)}
.node-title{font-family:'Space Grotesk',sans-serif;font-size:11.5px;font-weight:600;color:var(--white);line-height:1.3;margin-bottom:4px}
.node-desc{font-size:10px;color:var(--text2);line-height:1.42}
.lt{display:inline-flex;align-items:center;gap:3px;border-radius:20px;padding:2px 7px;font-size:8.5px;font-weight:600;margin-top:5px;border:1px solid}
.lt.f{border-color:#22c97a44;color:#22c97a;background:rgba(34,201,122,.07)}
.lt.m{border-color:#f5a62344;color:#f5a623;background:rgba(245,166,35,.07)}
.lt.s{border-color:#e05c5c44;color:#e05c5c;background:rgba(224,92,92,.07)}
.note{display:inline-block;font-size:8.5px;color:var(--text2);background:var(--surface2);border:1px solid var(--border);border-radius:5px;padding:2px 7px;margin-top:4px;line-height:1.4}
.note.ok{border-color:#22c97a33;color:#44cc88}
.note.warn{border-color:#f5a62333;color:#f5a623}

/* PARALLEL */
.para{border:1.5px dashed var(--border);border-radius:13px;padding:13px;position:relative}
.para-lbl{position:absolute;top:-9px;left:13px;background:var(--bg);padding:0 7px;font-size:7.5px;font-weight:700;letter-spacing:2px;text-transform:uppercase;color:var(--text3)}
.track-lbl{font-size:7.5px;font-weight:700;letter-spacing:1.4px;text-transform:uppercase;text-align:center;padding-bottom:5px;border-bottom:1px solid var(--border);margin-bottom:7px}

/* GATE */
.gate-wrap{display:flex;flex-direction:column;align-items:center;gap:4px}
.gate-d{width:72px;height:72px;border:2px solid var(--orange);background:#1e1608;transform:rotate(45deg);border-radius:7px;display:flex;align-items:center;justify-content:center;cursor:pointer;transition:box-shadow .18s;flex-shrink:0}
.gate-d:hover{box-shadow:0 0 0 4px rgba(245,166,35,.18)}
.gate-di{transform:rotate(-45deg);text-align:center}
.gate-di span{font-size:7.5px;font-weight:700;color:var(--orange);display:block;letter-spacing:.4px}
.branches{display:flex;gap:32px;align-items:flex-start}
.branch{display:flex;flex-direction:column;align-items:center;gap:3px}
.blbl{font-size:9px;font-weight:700}
.blbl.y{color:var(--green)}.blbl.n{color:var(--red)}

/* SYNC */
.sync{height:3px;background:linear-gradient(90deg,#7c5cfc,var(--accent));border-radius:2px;margin:8px 0;position:relative}
.sync::before{content:'SINCRONIZAÇÃO';position:absolute;top:-12px;left:50%;transform:translateX(-50%);font-size:7px;font-weight:700;letter-spacing:2px;color:var(--text3);white-space:nowrap}

/* CADASTRO SUB-FLOW */
.cad-box{background:#0a1520;border:1.5px solid #2f4a5a;border-radius:13px;padding:14px;position:relative}
.cad-box-lbl{position:absolute;top:-9px;left:13px;background:var(--bg);padding:0 7px;font-size:7.5px;font-weight:700;letter-spacing:2px;text-transform:uppercase;color:#55aacc}

/* DIVIDER */
.div-line{width:100%;height:1px;background:var(--border);margin:10px 0;opacity:.4}

/* LEGEND */
.legend{display:flex;flex-wrap:wrap;gap:9px;padding:12px 28px;border-top:1px solid var(--border);background:var(--surface)}
.li{display:flex;align-items:center;gap:6px;font-size:10px;color:var(--text2)}
.ld{width:8px;height:8px;border-radius:50%;flex-shrink:0}

/* PANEL */
#panel{position:fixed;right:-400px;top:0;bottom:0;width:375px;background:var(--surface);border-left:1px solid var(--border);z-index:200;padding:24px 20px;overflow-y:auto;transition:right .28s ease}
#panel.open{right:0}
.pcls{position:absolute;top:12px;right:12px;background:var(--surface2);border:1px solid var(--border);border-radius:5px;color:var(--text2);font-size:13px;width:28px;height:28px;display:flex;align-items:center;justify-content:center;cursor:pointer}
.pbadge{font-size:8.5px;font-weight:700;letter-spacing:1.4px;text-transform:uppercase;padding:3px 9px;border-radius:20px;display:inline-block;margin-bottom:9px}
.ptitle{font-family:'Space Grotesk',sans-serif;font-size:17px;font-weight:700;color:var(--white);margin-bottom:8px;line-height:1.3}
.plt{display:inline-flex;align-items:center;gap:5px;padding:3px 11px;border-radius:20px;font-size:10px;font-weight:600;margin-bottom:11px;border:1px solid}
.plt.f{background:rgba(34,201,122,.09);color:#22c97a;border-color:rgba(34,201,122,.3)}
.plt.m{background:rgba(245,166,35,.09);color:#f5a623;border-color:rgba(245,166,35,.3)}
.plt.s{background:rgba(224,92,92,.09);color:#e05c5c;border-color:rgba(224,92,92,.3)}
.pdesc{font-size:11.5px;color:var(--text2);line-height:1.58;margin-bottom:14px}
.psec{margin-bottom:14px}
.psec-t{font-size:8.5px;font-weight:700;letter-spacing:1.4px;text-transform:uppercase;color:var(--text3);margin-bottom:6px}
.plist{list-style:none;display:flex;flex-direction:column;gap:4px}
.plist li{font-size:11px;color:var(--text2);padding-left:13px;position:relative;line-height:1.48}
.plist li::before{content:'→';position:absolute;left:0;color:var(--accent);font-size:10px}
.pbox{background:var(--surface2);border-radius:7px;padding:9px}
.pflag{display:flex;align-items:flex-start;gap:5px;background:rgba(224,92,92,.09);border:1px solid rgba(224,92,92,.22);border-radius:6px;padding:6px 9px;font-size:10.5px;color:var(--red);margin-bottom:5px;line-height:1.44}
.pok{display:flex;align-items:flex-start;gap:5px;background:rgba(34,201,122,.07);border:1px solid rgba(34,201,122,.2);border-radius:6px;padding:6px 9px;font-size:10.5px;color:#44cc88;margin-bottom:5px;line-height:1.44}
.raci-t{width:100%;border-collapse:collapse;font-size:9.5px;margin-top:5px}
.raci-t th{background:var(--surface2);color:var(--text3);font-weight:700;letter-spacing:.8px;text-transform:uppercase;padding:4px 7px;text-align:left;font-size:8px}
.raci-t td{padding:4px 7px;color:var(--text2);border-bottom:1px solid var(--border)}
.rR{color:#e05c5c;font-weight:700}.rA{color:#f5a623;font-weight:700}.rC{color:#7ea8ff}.rI{color:var(--text3)}

.flex{display:flex}.col{flex-direction:column}.ctr{align-items:center;justify-content:center}
.g4{gap:4px}.g6{gap:6px}.g8{gap:8px}.g10{gap:10px}.g12{gap:12px}.g16{gap:16px}
.mt4{margin-top:4px}.mt6{margin-top:6px}.mt8{margin-top:8px}.mt10{margin-top:10px}.mt12{margin-top:12px}.mt16{margin-top:16px}

#flow-page header{z-index:100;flex-shrink:0}
#flow-page #detail-panel{z-index:200;position:fixed}
</style>

<!-- KANBAN STYLES (scoped) -->
<style id="kanban-styles">
#kanban-page *{box-sizing:border-box}


@import url('https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@2.44.0/tabler-icons.min.css');


body{background:var(--bg);color:var(--text);font-family:'Inter',sans-serif;min-height:100vh;overflow-x:hidden}

/* ── HEADER ── */
header{background:var(--s1);border-bottom:1px solid var(--border);padding:0 20px;height:52px;display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;z-index:200}
.logo{font-family:'Space Grotesk',sans-serif;font-size:15px;font-weight:700;color:var(--white);display:flex;align-items:center;gap:8px}
.logo-dot{width:8px;height:8px;border-radius:50%;background:var(--accent)}
.hactions{display:flex;gap:8px;align-items:center}
.btn{background:var(--s2);border:1px solid var(--border2);border-radius:7px;color:var(--text2);font-size:12px;font-weight:500;padding:5px 12px;cursor:pointer;display:flex;align-items:center;gap:5px;transition:all .15s}
.btn:hover{background:var(--s3);color:var(--text);border-color:var(--accent)}
.btn.primary{background:var(--accent);border-color:var(--accent);color:#fff}
.btn.primary:hover{background:#3a6ee0}
.btn.danger{background:rgba(224,92,92,.12);border-color:rgba(224,92,92,.3);color:var(--red)}
.btn.danger:hover{background:rgba(224,92,92,.2)}

/* ── TABS ── */
.tabs{background:var(--s1);border-bottom:1px solid var(--border);padding:0 20px;display:flex;gap:2px;overflow-x:auto}
.tab{padding:10px 16px;font-size:12px;font-weight:500;color:var(--text3);cursor:pointer;border-bottom:2px solid transparent;white-space:nowrap;transition:all .15s;display:flex;align-items:center;gap:6px}
.tab:hover{color:var(--text2)}
.tab.active{color:var(--accent);border-bottom-color:var(--accent)}
.tab .tab-count{background:var(--s3);border-radius:10px;padding:1px 6px;font-size:10px;color:var(--text3)}
.tab.active .tab-count{background:rgba(79,127,255,.2);color:var(--accent)}

/* ── LAYOUT ── */
.main{display:flex;height:calc(100vh - 104px);min-height:0}

/* ── SIDEBAR ── */
.sidebar{width:260px;min-width:260px;background:var(--s1);border-right:1px solid var(--border);display:flex;flex-direction:column;overflow:hidden}
.sidebar-header{padding:14px 16px;border-bottom:1px solid var(--border);font-size:11px;font-weight:600;letter-spacing:1.5px;text-transform:uppercase;color:var(--text3);display:flex;justify-content:space-between;align-items:center}
.project-list{overflow-y:auto;flex:1;padding:8px}
.project-item{padding:10px 12px;border-radius:8px;cursor:pointer;border:1px solid transparent;margin-bottom:3px;transition:all .15s}
.project-item:hover{background:var(--s2)}
.project-item.active{background:var(--s2);border-color:var(--border2)}
.project-item.active .pi-name{color:var(--white)}
.pi-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:4px}
.pi-name{font-size:12px;font-weight:500;color:var(--text2);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;max-width:140px}
.pi-phase{font-size:9px;font-weight:600;letter-spacing:.5px;padding:2px 6px;border-radius:10px;white-space:nowrap}
.pi-meta{font-size:10px;color:var(--text3);display:flex;align-items:center;gap:6px}
.pi-progress{height:2px;background:var(--border);border-radius:1px;margin-top:6px;overflow:hidden}
.pi-progress-bar{height:100%;border-radius:1px;background:var(--accent);transition:width .3s}

/* ── KANBAN ── */
.kanban-wrap{flex:1;overflow-x:auto;overflow-y:auto;padding:16px}
.kanban{display:flex;gap:12px;min-width:max-content;align-items:flex-start}
.col-wrap{width:220px;flex-shrink:0}
.col-header{padding:8px 10px;margin-bottom:8px;display:flex;justify-content:space-between;align-items:center}
.col-title{font-size:10px;font-weight:700;letter-spacing:1.5px;text-transform:uppercase;color:var(--text3);display:flex;align-items:center;gap:6px}
.col-count{background:var(--s2);border-radius:10px;padding:1px 7px;font-size:10px;color:var(--text3);font-weight:600}
.col-cards{display:flex;flex-direction:column;gap:6px;min-height:40px}

/* ── TASK CARD ── */
.card{background:var(--s1);border:1px solid var(--border);border-radius:9px;padding:11px 12px;cursor:pointer;transition:all .15s;position:relative}
.card:hover{border-color:var(--border2);background:var(--s2);transform:translateY(-1px)}
.card.done{opacity:.55}
.card.blocked{border-color:rgba(224,92,92,.35)}
.card-phase-bar{height:2px;border-radius:1px;margin-bottom:8px}
.card-owner-row{display:flex;justify-content:space-between;align-items:center;margin-bottom:5px}
.card-owner{font-size:8.5px;font-weight:700;letter-spacing:1px;text-transform:uppercase}
.card-status{width:7px;height:7px;border-radius:50%;flex-shrink:0}
.card-title{font-size:11.5px;font-weight:500;color:var(--white);line-height:1.35;margin-bottom:7px}
.card-meta{display:flex;flex-wrap:wrap;gap:4px;margin-top:5px}
.pill{font-size:9px;font-weight:600;padding:2px 7px;border-radius:10px;border:1px solid;white-space:nowrap}
.lt-f{border-color:#22c97a33;color:#22c97a;background:rgba(34,201,122,.07)}
.lt-m{border-color:#f5a62333;color:#f5a623;background:rgba(245,166,35,.07)}
.lt-s{border-color:#e05c5c33;color:#e05c5c;background:rgba(224,92,92,.07)}
.pill-blocked{border-color:#e05c5c55;color:#e05c5c;background:rgba(224,92,92,.1)}
.pill-dep{border-color:#4f7fff33;color:#4f7fff;background:rgba(79,127,255,.07)}
.card-date{font-size:9px;color:var(--text3);margin-top:5px;display:flex;align-items:center;gap:3px}

/* ── GATE CARD ── */
.gate-card{border:1.5px solid var(--orange);background:#1e1608;border-radius:9px;padding:10px 12px;cursor:pointer;transition:all .15s;margin-bottom:6px}
.gate-card:hover{border-color:#f5c04a;background:#211a09}
.gate-label{font-size:8.5px;font-weight:700;letter-spacing:1px;text-transform:uppercase;color:var(--orange);margin-bottom:4px}
.gate-title{font-size:11.5px;font-weight:500;color:var(--white);margin-bottom:4px}
.gate-status{font-size:9px;color:var(--text3)}

/* ── SYNC BAR ── */
.sync-bar-col{background:rgba(79,127,255,.08);border:1px dashed rgba(79,127,255,.2);border-radius:7px;padding:6px 10px;text-align:center;font-size:9px;font-weight:600;letter-spacing:1px;text-transform:uppercase;color:#4f7fff;margin-bottom:6px}

/* ── DETAIL PANEL ── */
#detail{position:fixed;right:-420px;top:0;bottom:0;width:400px;background:var(--s1);border-left:1px solid var(--border);z-index:300;overflow-y:auto;transition:right .25s ease}
#detail.open{right:0}
.det-header{padding:18px 20px;border-bottom:1px solid var(--border);display:flex;justify-content:space-between;align-items:flex-start}
.det-close{background:var(--s2);border:1px solid var(--border);border-radius:6px;color:var(--text2);font-size:13px;width:28px;height:28px;display:flex;align-items:center;justify-content:center;cursor:pointer;flex-shrink:0}
.det-body{padding:18px 20px;display:flex;flex-direction:column;gap:14px}
.det-section{display:flex;flex-direction:column;gap:6px}
.det-label{font-size:9px;font-weight:700;letter-spacing:1.5px;text-transform:uppercase;color:var(--text3)}
.det-val{font-size:13px;color:var(--text2);line-height:1.55}
.det-input{background:var(--s2);border:1px solid var(--border);border-radius:7px;color:var(--text);font-size:12px;padding:7px 10px;width:100%;outline:none;font-family:inherit}
.det-input:focus{border-color:var(--accent)}
.det-input::placeholder{color:var(--text3)}
.det-select{background:var(--s2);border:1px solid var(--border);border-radius:7px;color:var(--text);font-size:12px;padding:7px 10px;width:100%;outline:none;font-family:inherit;cursor:pointer}
.det-select:focus{border-color:var(--accent)}
.det-textarea{background:var(--s2);border:1px solid var(--border);border-radius:7px;color:var(--text);font-size:12px;padding:7px 10px;width:100%;outline:none;font-family:inherit;min-height:70px;resize:vertical;line-height:1.5}
.det-textarea:focus{border-color:var(--accent)}
.det-row{display:flex;gap:8px}
.det-row > *{flex:1}
.raci-mini{display:flex;flex-wrap:wrap;gap:4px}
.raci-tag{font-size:9px;font-weight:600;padding:2px 7px;border-radius:10px;border:1px solid}

/* ── NEW PROJECT MODAL (faux viewport) ── */
#modal-bg{display:none;position:fixed;inset:0;background:rgba(0,0,0,.6);z-index:400;align-items:center;justify-content:center}
#modal-bg.open{display:flex}
.modal{background:var(--s1);border:1px solid var(--border2);border-radius:13px;width:460px;max-height:80vh;overflow-y:auto}
.modal-header{padding:18px 20px;border-bottom:1px solid var(--border);display:flex;justify-content:space-between;align-items:center}
.modal-title{font-family:'Space Grotesk',sans-serif;font-size:15px;font-weight:600;color:var(--white)}
.modal-body{padding:18px 20px;display:flex;flex-direction:column;gap:12px}
.modal-footer{padding:14px 20px;border-top:1px solid var(--border);display:flex;justify-content:flex-end;gap:8px}
.form-label{font-size:10px;font-weight:600;letter-spacing:1px;text-transform:uppercase;color:var(--text3);margin-bottom:4px;display:block}
.form-input{background:var(--s2);border:1px solid var(--border);border-radius:7px;color:var(--text);font-size:12px;padding:8px 11px;width:100%;outline:none;font-family:inherit}
.form-input:focus{border-color:var(--accent)}
.form-select{background:var(--s2);border:1px solid var(--border);border-radius:7px;color:var(--text);font-size:12px;padding:8px 11px;width:100%;outline:none;font-family:inherit;cursor:pointer}
.form-select:focus{border-color:var(--accent)}
.form-row{display:flex;gap:10px}
.form-row>div{flex:1}

/* ── EMPTY STATE ── */
.empty{display:flex;flex-direction:column;align-items:center;justify-content:center;height:100%;color:var(--text3);text-align:center;gap:10px}
.empty i{font-size:36px;opacity:.3}
.empty p{font-size:13px}

/* ── PORTFOLIO VIEW ── */
.portfolio-grid{padding:16px;display:flex;flex-direction:column;gap:10px}
.pf-card{background:var(--s1);border:1px solid var(--border);border-radius:10px;padding:14px 16px;cursor:pointer;transition:all .15s}
.pf-card:hover{border-color:var(--border2);background:var(--s2)}
.pf-top{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:10px}
.pf-name{font-size:13px;font-weight:500;color:var(--white)}
.pf-meta{display:flex;gap:8px;align-items:center;flex-wrap:wrap}
.pf-phase-badge{font-size:9px;font-weight:700;letter-spacing:.5px;padding:3px 8px;border-radius:10px}
.pf-lanes{display:grid;grid-template-columns:repeat(4,1fr);gap:6px;margin-top:10px}
.pf-lane{background:var(--s2);border-radius:6px;padding:6px 8px;font-size:9px}
.pf-lane-name{color:var(--text3);font-weight:600;letter-spacing:.5px;text-transform:uppercase;margin-bottom:3px}
.pf-lane-status{display:flex;align-items:center;gap:4px;font-size:10px;color:var(--text2)}
.status-dot{width:6px;height:6px;border-radius:50%;flex-shrink:0}
.pf-progress-row{display:flex;align-items:center;gap:8px;margin-top:8px}
.pf-progress-bg{flex:1;height:3px;background:var(--border);border-radius:2px;overflow:hidden}
.pf-progress-fill{height:100%;border-radius:2px;background:var(--accent)}
.pf-pct{font-size:10px;color:var(--text3);min-width:28px;text-align:right}

/* ── SCROLLBAR ── */
::-webkit-scrollbar{width:4px;height:4px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:var(--border2);border-radius:2px}

/* ── UTILS ── */
.flex{display:flex}.gap4{gap:4px}.gap6{gap:6px}.gap8{gap:8px}.gap12{gap:12px}
.ai-c{align-items:center}.jc-sb{justify-content:space-between}
.mt4{margin-top:4px}.mt8{margin-top:8px}.mt12{margin-top:12px}
.fw5{font-weight:500}.fs10{font-size:10px}.fs11{font-size:11px}.fs12{font-size:12px}.fs13{font-size:13px}
.col-text{color:var(--text2)}.col-muted{color:var(--text3)}

#kanban-page header{z-index:100}
#kanban-page #detail{z-index:300}
#kanban-page #modal-bg{z-index:400}
</style>
</head>
<body>

<!-- ══════════════ HOME ══════════════ -->
<div id="home" class="page active">
  <div class="home-inner">
    <div class="home-logo"><div class="home-logo-dot"></div> Rennova · Gestão de Lançamentos</div>
    <h1 class="home-title">Central de <span>Projetos</span><br>de Novos Produtos</h1>
    <p class="home-sub">Acesse o fluxograma completo do processo de lançamento ou gerencie os projetos ativos no Kanban.</p>
    <div class="home-cards">

      <div class="home-card accent-flow" onclick="goTo('flow-page')">
        <span class="hc-icon">🗺️</span>
        <div class="hc-title">Fluxograma do Processo</div>
        <div class="hc-desc">Visualize todas as fases, trilhas paralelas, gates de decisão e responsáveis do processo de lançamento.</div>
        <div class="hc-tags">
          <span class="hc-tag">10 Fases</span>
          <span class="hc-tag">4 Trilhas Paralelas</span>
          <span class="hc-tag">2 Gates ANVISA</span>
          <span class="hc-tag">RACI por etapa</span>
          <span class="hc-tag">Lead Times</span>
        </div>
        <div class="hc-cta" style="color:var(--accent)">
          Abrir Fluxograma
          <i class="ti ti-arrow-up-right hc-arrow" style="font-size:16px"></i>
        </div>
      </div>

      <div class="home-card accent-kanban" onclick="goTo('kanban-page')">
        <span class="hc-icon">📋</span>
        <div class="hc-title">Kanban de Projetos</div>
        <div class="hc-desc">Gerencie projetos simultâneos, acompanhe status por fase, defina responsáveis e prazos por tarefa.</div>
        <div class="hc-tags">
          <span class="hc-tag">Multi-projeto</span>
          <span class="hc-tag">Tarefas pré-carregadas</span>
          <span class="hc-tag">Visão de Portfólio</span>
          <span class="hc-tag">Progresso automático</span>
          <span class="hc-tag">Dados salvos</span>
        </div>
        <div class="hc-cta" style="color:var(--green)">
          Abrir Kanban
          <i class="ti ti-arrow-up-right hc-arrow" style="font-size:16px"></i>
        </div>
      </div>

    </div>
    <div class="home-footer">v3.0 · Stage-Gate + Kanban · Processo de Lançamento de Produtos Rennova</div>
  </div>
</div>

<!-- ══════════════ FLOW PAGE ══════════════ -->
<div id="flow-page" class="page">


<header>
  <div class="logo">Rennova <span>·</span> Product Launch <span style="font-size:12px;color:var(--text3);margin-left:6px">v3.0</span></div>
  <div class="header-meta">
    <span class="hbadge v">● v3 — Sequência corrigida</span>
    <span class="hbadge">⏱ Lead times</span>
    <span class="hbadge" style="border-color:#22c97a44;color:#44cc88">✓ Gaps respondidos</span>
    <span class="hbadge">Clique nos blocos para detalhes + RACI</span>
  </div>
</header>

<div class="canvas-wrapper">
<div class="flow" id="flow">

<!-- ═══ FASE 1 ═══ -->
<div class="ph">Fase 1 — Origem e Proposta</div>
<div class="flex ctr">
  <div class="node start" onclick="op('origem')" style="max-width:260px">
    <span class="node-icon">🔍</span>
    <div class="node-owner">Iniciador · Comex ou BD</div>
    <div class="node-title">Identificação de Oportunidade</div>
    <div class="node-desc">Traz proposta com custos do produto, contrato com fabricante e fornecedor já negociado</div>
    <div class="lt f">⏱ 1–5 dias</div>
    <div class="note ok">✓ Viabilidade financeira já vem com a proposta</div>
    <div class="note ok">✓ Fornecedor homologado antes deste passo</div>
  </div>
</div>

<div class="ad mt4"><svg width="2" height="26"><line x1="1" y1="0" x2="1" y2="18" stroke="#2e3248" stroke-width="2"/><polygon points="1,26 -4,16 6,16" fill="#2e3248"/></svg></div>

<!-- ═══ FASE 2 ═══ -->
<div class="ph">Fase 2 — Triagem de Portfólio</div>
<div class="flex col" style="align-items:center;gap:7px">
  <div class="node mkt" onclick="op('triagem')" style="max-width:290px">
    <span class="node-icon">📋</span>
    <div class="node-owner">Mkt Produtos · Projetos · Regulatório</div>
    <div class="node-title">Reunião de Apresentação da Proposta</div>
    <div class="node-desc">Mkt Produtos avalia canibalização, fit de portfólio e viabilidade técnica/financeira. Regulatório mapeia requisitos ANVISA.</div>
    <div class="lt m">⏱ 3–7 dias</div>
    <div class="note ok">✓ Mkt Produtos é quem aprova ou reprova — decisão técnica e estratégica</div>
  </div>
  <div class="ad"><svg width="2" height="18"><line x1="1" y1="0" x2="1" y2="10" stroke="#2e3248" stroke-width="2"/><polygon points="1,18 -4,8 6,8" fill="#2e3248"/></svg></div>
  <div class="gate-wrap">
    <div class="gate-d" onclick="op('gate1')"><div class="gate-di"><span>CABE NO</span><span>PORTFÓLIO?</span></div></div>
    <div class="branches">
      <div class="branch"><div class="blbl y">✓ SIM</div><svg width="2" height="18"><line x1="1" y1="0" x2="1" y2="18" stroke="#22c97a" stroke-width="2"/></svg><div style="font-size:8px;color:var(--text3)">continua ↓</div></div>
      <div class="branch"><div class="blbl n">✗ NÃO</div><svg width="2" height="18"><line x1="1" y1="0" x2="1" y2="18" stroke="#e05c5c" stroke-width="2"/></svg><div style="font-size:8px;color:var(--red)">encerra</div></div>
    </div>
  </div>
</div>

<div class="ad mt8"><svg width="2" height="26"><line x1="1" y1="0" x2="1" y2="18" stroke="#2e3248" stroke-width="2"/><polygon points="1,26 -4,16 6,16" fill="#2e3248"/></svg></div>

<!-- ═══ FASE 3 ═══ -->
<div class="ph">Fase 3 — Kick-off do Projeto</div>
<div class="flex col" style="align-items:center;gap:7px">
  <div class="node comex" onclick="op('cc-abertura')" style="max-width:290px">
    <span class="node-icon">📂</span>
    <div class="node-owner">Comex ou BD (quem startou)</div>
    <div class="node-title">Abertura do Change Control no Sistema</div>
    <div class="node-desc">Equipe que startou o projeto abre o controle de mudança no sistema com as informações do produto</div>
    <div class="lt f">⏱ 1 dia</div>
    <div class="note ok">✓ Responsabilidade clara: quem abre é quem startou</div>
  </div>
  <div class="ad"><svg width="2" height="16"><line x1="1" y1="0" x2="1" y2="16" stroke="#2e3248" stroke-width="2"/></svg></div>
  <div class="node qual" onclick="op('kickoff')" style="max-width:290px">
    <span class="node-icon">🚀</span>
    <div class="node-owner">Controle de Qualidade (GQ) · PM</div>
    <div class="node-title">GQ + PM Conduzem o Kick-off</div>
    <div class="node-desc">GQ e PM convocam e conduzem a reunião de kick-off com todas as áreas. PM (pessoa fixa) assume formalmente o projeto e define cronograma e RACI.</div>
    <div class="lt f">⏱ 1–2 dias</div>
    <div class="note ok">✓ PM já definida — mesma pessoa em todos os projetos</div>
    <div class="note ok">✓ GQ co-lidera junto com a PM</div>
  </div>
</div>

<div class="ad mt8"><svg width="2" height="26"><line x1="1" y1="0" x2="1" y2="18" stroke="#2e3248" stroke-width="2"/><polygon points="1,26 -4,16 6,16" fill="#2e3248"/></svg></div>

<!-- ═══ FASE 4 ═══ -->
<div class="ph">Fase 4 — Pré-ANVISA: Documentação + Arte Aberta (Paralelo)</div>
<div class="para">
  <div class="para-lbl">⟵ ATIVIDADES SIMULTÂNEAS PÓS KICK-OFF ⟶</div>
  <div class="flex g8 mt10" style="align-items:flex-start">

    <!-- TRILHA A: REGULATÓRIO → DOCUMENTAÇÃO -->
    <div class="flex col g6" style="flex:1;min-width:148px">
      <div class="track-lbl" style="color:#44cc88;border-color:#2f5a3a">TRILHA A · REGULATÓRIO</div>
      <div class="node reg" onclick="op('reg-checklist')">
        <span class="node-icon">📋</span>
        <div class="node-owner">Regulatório</div>
        <div class="node-title">Checklist de Documentos ao Comex/BD</div>
        <div class="node-desc">Reg envia lista padronizada de docs necessários para o processo ANVISA</div>
        <div class="lt f">⏱ 1–2 dias</div>
        <div class="note ok">✓ Checklist já existe no Regulatório</div>
      </div>
      <div class="ad"><svg width="2" height="14"><line x1="1" y1="0" x2="1" y2="14" stroke="#2e3248" stroke-width="2"/></svg></div>
      <div class="node comex" onclick="op('docs-coleta')">
        <span class="node-icon">📦</span>
        <div class="node-owner">Comex / BD</div>
        <div class="node-title">Coleta e Envio de Docs ao Regulatório</div>
        <div class="node-desc">Comex/BD reúne documentação técnica do fabricante conforme checklist</div>
        <div class="lt m">⏱ 5–15 dias</div>
      </div>
      <div class="ad"><svg width="2" height="14"><line x1="1" y1="0" x2="1" y2="14" stroke="#2e3248" stroke-width="2"/></svg></div>
      <div class="node reg" onclick="op('anvisa-sub')">
        <span class="node-icon">🏛️</span>
        <div class="node-owner">Regulatório</div>
        <div class="node-title">Submissão para Registro na ANVISA</div>
        <div class="node-desc">Regulatório protocola o processo de registro com toda a documentação</div>
        <div class="lt s">⏱ 30 dias a 1+ ano ⚠</div>
        <div class="note warn">⚠ Principal risco de prazo do projeto</div>
      </div>
    </div>

    <div class="ar"><svg width="14" height="2"><line x1="0" y1="1" x2="14" y2="1" stroke="#2e3248" stroke-width="2"/></svg></div>

    <!-- TRILHA B: MARKETING → ARTE ABERTA -->
    <div class="flex col g6" style="flex:1;min-width:148px">
      <div class="track-lbl" style="color:#a07eff;border-color:#3a2f6b">TRILHA B · MKT + HOUSE</div>
      <div class="node mkt" onclick="op('estrategia-inicial')">
        <span class="node-icon">🎯</span>
        <div class="node-owner">Mkt de Novos Produtos</div>
        <div class="node-title">Estratégia de Posicionamento</div>
        <div class="node-desc">Posicionamento, pricing, canal, diferenciais vs concorrentes</div>
        <div class="lt m">⏱ 7–15 dias</div>
      </div>
      <div class="ad"><svg width="2" height="14"><line x1="1" y1="0" x2="1" y2="14" stroke="#2e3248" stroke-width="2"/></svg></div>
      <div class="node house" onclick="op('kv-arte-aberta')">
        <span class="node-icon">🖼️</span>
        <div class="node-owner">Mkt Produtos → House</div>
        <div class="node-title">Briefing → KV + Arte Aberta p/ ANVISA</div>
        <div class="node-desc">House produz KV. Arte aprovada pelo CEO. Arte aberta (sem nº registro) preparada para ANVISA.</div>
        <div class="lt m">⏱ 10–20 dias</div>
        <div class="note warn">⚠ Arte aberta ≠ arte de embalagem final</div>
        <div class="note ok">✓ Aprovação: CEO</div>
      </div>
    </div>

    <div class="ar"><svg width="14" height="2"><line x1="0" y1="1" x2="14" y2="1" stroke="#2e3248" stroke-width="2"/></svg></div>

    <!-- TRILHA C: JURÍDICO → INPI (só inicia após CEO aprovar KV) -->
    <div class="flex col g6" style="flex:1;min-width:148px">
      <div class="track-lbl" style="color:#ffcc55;border-color:#5a4a2f">TRILHA C · JURÍDICO</div>
      <div style="background:rgba(79,127,255,.07);border:1px solid rgba(79,127,255,.2);border-radius:7px;padding:6px 9px;font-size:8.5px;color:var(--accent);line-height:1.4;margin-bottom:4px">
        🔗 <strong>Depende:</strong> só inicia após CEO aprovar o KV (Trilha B)
      </div>
      <div class="node jur" onclick="op('inpi')">
        <span class="node-icon">⚖️</span>
        <div class="node-owner">Jurídico</div>
        <div class="node-title">Análise do Nome no INPI</div>
        <div class="node-desc">Busca disponibilidade de marca. Inicia somente após CEO aprovar o KV com o nome do produto.</div>
        <div class="lt m">⏱ 5–10 dias</div>
      </div>
      <div class="ad"><svg width="2" height="14"><line x1="1" y1="0" x2="1" y2="14" stroke="#2e3248" stroke-width="2"/></svg></div>
      <div class="node jur" onclick="op('liminar')">
        <span class="node-icon">🔏</span>
        <div class="node-owner">Jurídico</div>
        <div class="node-title">Depósito de Marca / Liminar</div>
        <div class="node-desc">Protege o nome enquanto INPI analisa o registro completo</div>
        <div class="lt s">⏱ Depósito: 1–2 dias / INPI: 18–24 meses</div>
      </div>
    </div>

  </div>
</div>

<div class="ad mt8"><svg width="2" height="26"><line x1="1" y1="0" x2="1" y2="18" stroke="#2e3248" stroke-width="2"/><polygon points="1,26 -4,16 6,16" fill="#2e3248"/></svg></div>

<!-- ═══ FASE 5 — AGUARDA ANVISA ═══ -->
<div class="ph">Fase 5 — Aguarda Deferimento ANVISA</div>
<div class="flex col" style="align-items:center;gap:7px">
  <div class="node reg" onclick="op('aguarda-anvisa')" style="max-width:290px">
    <span class="node-icon">⏳</span>
    <div class="node-owner">Regulatório · PM monitora</div>
    <div class="node-title">Aguardando Deferimento ANVISA</div>
    <div class="node-desc">PM acompanha andamento. Projeto suspenso até resposta. Tudo que vem depois depende deste deferimento.</div>
    <div class="lt s">⏱ Variável — risco crítico de cronograma</div>
    <div class="note warn">⚠ Nenhuma etapa de cadastro ou arte de embalagem começa antes daqui</div>
  </div>
  <div class="ad"><svg width="2" height="18"><line x1="1" y1="0" x2="1" y2="10" stroke="#2e3248" stroke-width="2"/><polygon points="1,18 -4,8 6,8" fill="#2e3248"/></svg></div>
  <div class="gate-wrap">
    <div class="gate-d" onclick="op('gate2')"><div class="gate-di"><span>DEFERIDO</span><span>ANVISA?</span></div></div>
    <div class="branches">
      <div class="branch"><div class="blbl y">✓ SIM</div><svg width="2" height="18"><line x1="1" y1="0" x2="1" y2="18" stroke="#22c97a" stroke-width="2"/></svg><div style="font-size:8px;color:var(--text3)">dispara fase 6 ↓</div></div>
      <div class="branch"><div class="blbl n">✗ NÃO</div><svg width="2" height="18"><line x1="1" y1="0" x2="1" y2="18" stroke="#e05c5c" stroke-width="2"/></svg><div style="font-size:8px;color:var(--red)">recurso / encerra</div></div>
    </div>
  </div>
</div>

<div class="ad mt8"><svg width="2" height="26"><line x1="1" y1="0" x2="1" y2="18" stroke="#2e3248" stroke-width="2"/><polygon points="1,26 -4,16 6,16" fill="#2e3248"/></svg></div>

<!-- ═══ FASE 6 — PÓS DEFERIMENTO (PARALELO GRANDE) ═══ -->
<div class="ph">Fase 6 — Pós-Deferimento ANVISA: 4 Trilhas Simultâneas</div>
<div class="para">
  <div class="para-lbl">⟵ TODAS COMEÇAM AO MESMO TEMPO — PM monitora convergência ⟶</div>
  <div class="flex g6 mt10" style="align-items:flex-start">

    <!-- TRILHA 1: CADASTRO (sub-fluxo) -->
    <div class="flex col g6" style="flex:1.4;min-width:200px">
      <div class="track-lbl" style="color:#55aacc;border-color:#2f4a5a">TRILHA 1 · CADASTRO</div>
      <!-- ABERTURA pelo BD/Comex -->
      <div class="node comex" onclick="op('cad-abertura')">
        <span class="node-icon">📂</span>
        <div class="node-owner">BD ou Comex (quem startou)</div>
        <div class="node-title">Abre o Cadastro no Sistema</div>
        <div class="node-desc">Equipe que startou o projeto inicia o processo de cadastro no sistema com os dados básicos do produto</div>
        <div class="lt f">⏱ 1 dia</div>
        <div class="note ok">✓ BD ou Comex que startou é quem abre</div>
      </div>
      <div class="ad"><svg width="2" height="12"><line x1="1" y1="0" x2="1" y2="8" stroke="#2e3248" stroke-width="2"/><polygon points="1,12 -3,5 5,5" fill="#2e3248"/></svg></div>
      <div class="cad-box">
        <div class="cad-box-lbl">📦 SUB-FLUXO CADASTRO</div>
        <div class="flex col g4 mt10">
          <div class="node cad" onclick="op('cad-verifica')">
            <span class="node-icon">🔎</span>
            <div class="node-owner">Equipe de Cadastro</div>
            <div class="node-title">Verifica se Produto já tem Cadastro</div>
            <div class="node-desc">Busca no sistema. Se já existe → atualiza e finaliza.</div>
            <div class="lt f">⏱ 1 dia</div>
          </div>
          <div class="ad"><svg width="2" height="14"><line x1="1" y1="0" x2="1" y2="10" stroke="#2e3248" stroke-width="2"/><polygon points="1,14 -3,6 5,6" fill="#2e3248"/></svg></div>
          <div class="gate-wrap" style="transform:scale(.82);transform-origin:top center">
            <div class="gate-d" onclick="op('gate-cad')"><div class="gate-di"><span>JÁ TEM</span><span>CADASTRO?</span></div></div>
            <div class="branches" style="gap:16px">
              <div class="branch"><div class="blbl y" style="font-size:8px">✓ SIM</div><svg width="2" height="14"><line x1="1" y1="0" x2="1" y2="14" stroke="#22c97a" stroke-width="2"/></svg><div style="font-size:7px;color:var(--green)">atualiza → fim</div></div>
              <div class="branch"><div class="blbl n" style="font-size:8px">✗ NÃO</div><svg width="2" height="14"><line x1="1" y1="0" x2="1" y2="14" stroke="#e05c5c" stroke-width="2"/></svg><div style="font-size:7px;color:var(--text3)">segue ↓</div></div>
            </div>
          </div>
          <div class="ad"><svg width="2" height="10"><line x1="1" y1="0" x2="1" y2="10" stroke="#2e3248" stroke-width="2"/></svg></div>
          <!-- Paralelo interno: Fiscal + Reg + Comex -->
          <div style="background:#0d1a24;border:1px dashed #2f4a5a;border-radius:9px;padding:9px;position:relative">
            <div style="position:absolute;top:-8px;left:10px;background:#0a1520;padding:0 6px;font-size:7px;font-weight:700;letter-spacing:1.5px;text-transform:uppercase;color:#2f4a5a">VALIDAÇÃO SIMULTÂNEA</div>
            <div class="flex g4 mt6" style="align-items:flex-start">
              <div class="node fiscal" onclick="op('fiscal-ncm')" style="min-width:0;padding:8px 9px">
                <span class="node-icon" style="font-size:13px">🧾</span>
                <div class="node-owner" style="font-size:7px">Fiscal</div>
                <div class="node-title" style="font-size:10px">Valida NCM (tributos)</div>
                <div class="node-desc" style="font-size:9px">ICMS, PIS/COFINS, ST, benefícios fiscais</div>
                <div class="lt m" style="font-size:7.5px">⏱ 2–5 dias</div>
              </div>
              <div class="node reg" onclick="op('reg-cadastro')" style="min-width:0;padding:8px 9px">
                <span class="node-icon" style="font-size:13px">🏛️</span>
                <div class="node-owner" style="font-size:7px">Regulatório</div>
                <div class="node-title" style="font-size:10px">Dados Reg. p/ Cadastro</div>
                <div class="node-desc" style="font-size:9px">Descrição técnica · Nº registro ANVISA · Validade reg. · Shelf life</div>
                <div class="lt f" style="font-size:7.5px">⏱ 1–2 dias*</div>
                <div class="note ok" style="font-size:7.5px">✓ Nº ANVISA já disponível</div>
              </div>
              <div class="node comex" onclick="op('comex-val')" style="min-width:0;padding:8px 9px">
                <span class="node-icon" style="font-size:13px">🚢</span>
                <div class="node-owner" style="font-size:7px">Comex</div>
                <div class="node-title" style="font-size:10px">Valida NCM (importação)</div>
                <div class="node-desc" style="font-size:9px">II, IPI, lead time, Incoterm. Fornecedor já homologado.</div>
                <div class="lt m" style="font-size:7.5px">⏱ 2–5 dias</div>
              </div>
            </div>
          </div>
          <div class="sync mt4"></div>
          <div class="node cad" onclick="op('cad-finaliza')">
            <span class="node-icon">✅</span>
            <div class="node-owner">Equipe de Cadastro</div>
            <div class="node-title">Finaliza Cadastro + Gera Códigos</div>
            <div class="node-desc">Consolida tudo. Gera Código do Item. Gera EAN/GTIN se produto não tiver cód. de barras.</div>
            <div class="lt f">⏱ 1–2 dias</div>
            <div class="note ok">✓ Cadastro valida internamente antes de ativar</div>
          </div>
        </div>
      </div>
    </div>

    <div class="ar"><svg width="12" height="2"><line x1="0" y1="1" x2="12" y2="1" stroke="#2e3248" stroke-width="2"/></svg></div>

    <!-- TRILHA 2: GESTÃO DE ARTE DE EMBALAGEM -->
    <div class="flex col g6" style="flex:1.3;min-width:175px">
      <div class="track-lbl" style="color:#cc77ff;border-color:#4a2f5a">TRILHA 2 · ARTE EMBALAGEM</div>
      <div class="node reg" onclick="op('dizeres')">
        <span class="node-icon">📝</span>
        <div class="node-owner">Regulatório</div>
        <div class="node-title">Elabora Dizeres Técnicos</div>
        <div class="node-desc">Texto regulatório oficial com nº de registro, indicações, composição, modo de uso</div>
        <div class="lt m">⏱ 5–10 dias</div>
      </div>
      <div class="ad"><svg width="2" height="12"><line x1="1" y1="0" x2="1" y2="12" stroke="#2e3248" stroke-width="2"/></svg></div>
      <div class="node house" onclick="op('arte-emb')">
        <span class="node-icon">🎨</span>
        <div class="node-owner">Mkt Produtos → House</div>
        <div class="node-title">Abertura de Gestão de Arte de Embalagem</div>
        <div class="node-desc">Mkt abre no sistema. House produz arte com dizeres técnicos + KV aprovado.</div>
        <div class="lt m">⏱ 5–10 dias</div>
        <div class="note warn">⚠ Arte de embalagem ≠ arte aberta da Fase 4</div>
      </div>
      <div class="ad"><svg width="2" height="12"><line x1="1" y1="0" x2="1" y2="12" stroke="#2e3248" stroke-width="2"/></svg></div>
      <div class="node reg" onclick="op('revisao-arte')">
        <span class="node-icon">🔄</span>
        <div class="node-owner">House · Mkt Produtos · Regulatório</div>
        <div class="node-title">Roda de Revisão de Arte</div>
        <div class="node-desc">Ciclos iterativos. Recomendado: máx. 3 rodadas com SLA de 2 dias por área.</div>
        <div class="lt m">⏱ 10–20 dias</div>
      </div>
      <div class="ad"><svg width="2" height="12"><line x1="1" y1="0" x2="1" y2="12" stroke="#2e3248" stroke-width="2"/></svg></div>
      <div class="node reg" onclick="op('homologacao')">
        <span class="node-icon">✅</span>
        <div class="node-owner">Regulatório</div>
        <div class="node-title">Homologa Arte + Envia ao Fabricante</div>
        <div class="node-desc">Reg homologa no sistema e envia arquivos finais ao fabricante</div>
        <div class="lt f">⏱ 2–3 dias</div>
      </div>
    </div>

    <div class="ar"><svg width="12" height="2"><line x1="0" y1="1" x2="12" y2="1" stroke="#2e3248" stroke-width="2"/></svg></div>

    <!-- TRILHA 3: ESTRATÉGIA PÓS-DEFERIMENTO -->
    <div class="flex col g6" style="flex:1;min-width:148px">
      <div class="track-lbl" style="color:#a07eff;border-color:#3a2f6b">TRILHA 3 · ESTRATÉGIA</div>
      <div class="node mkt" onclick="op('estrategia-final')">
        <span class="node-icon">🎯</span>
        <div class="node-owner">Mkt Produtos</div>
        <div class="node-title">Aprovação da Estratégia de Lançamento</div>
        <div class="node-desc">Estratégia final de lançamento aprovada em paralelo à arte de embalagem</div>
        <div class="lt m">⏱ 5–10 dias</div>
        <div class="note ok">✓ Em paralelo à gestão de arte — não sequencial</div>
      </div>
      <div class="ad"><svg width="2" height="12"><line x1="1" y1="0" x2="1" y2="12" stroke="#2e3248" stroke-width="2"/></svg></div>
      <div class="node mkt" onclick="op('racional')">
        <span class="node-icon">📊</span>
        <div class="node-owner">Mkt Produtos → Gerente do Produto</div>
        <div class="node-title">Entrega do Racional Estratégico</div>
        <div class="node-desc">Posicionamento, pricing, metas e plano de comunicação entregues ao gerente responsável</div>
        <div class="lt f">⏱ 2–3 dias</div>
      </div>
    </div>

    <div class="ar"><svg width="12" height="2"><line x1="0" y1="1" x2="12" y2="1" stroke="#2e3248" stroke-width="2"/></svg></div>

    <!-- TRILHA 4: FORECAST -->
    <div class="flex col g6" style="flex:1;min-width:148px">
      <div class="track-lbl" style="color:#7ea8ff;border-color:#3a4a6b">TRILHA 4 · FORECAST</div>
      <div class="node comex" onclick="op('forecast')">
        <span class="node-icon">📦</span>
        <div class="node-owner">Comex / BD + CEO</div>
        <div class="node-title">Planejamento do Forecast de Compra</div>
        <div class="node-desc">Volumes, lead time, incoterm e 1ª ordem de compra. Feito entre a equipe que startou e o CEO.</div>
        <div class="lt m">⏱ 7–14 dias</div>
        <div class="note ok">✓ Em paralelo com arte — não sequencial</div>
        <div class="note ok">✓ CEO envolvido nesta etapa</div>
      </div>
    </div>

  </div>
</div>

<div class="sync mt16"></div>

<div class="ad mt8"><svg width="2" height="26"><line x1="1" y1="0" x2="1" y2="18" stroke="#2e3248" stroke-width="2"/><polygon points="1,26 -4,16 6,16" fill="#2e3248"/></svg></div>

<!-- ═══ FASE 7 ═══ -->
<div class="ph">Fase 7 — Encerramento do Projeto de Lançamento</div>
<div class="flex ctr">
  <div class="node go" onclick="op('encerramento')" style="max-width:320px">
    <span class="node-icon">🏁</span>
    <div class="node-owner">PM · Todas as Áreas</div>
    <div class="node-title">Checklist de Encerramento — Produto Pronto para Lançar</div>
    <div class="node-desc">Cadastro ativo ✓ · Arte homologada ✓ · Forecast/PO emitida ✓ · Estratégia aprovada ✓ · Marca protegida ✓</div>
    <div class="lt f">⏱ 1–2 dias</div>
  </div>
</div>

<div style="height:44px"></div>
</div><!-- /flow -->
</div><!-- /canvas-wrapper -->

<div class="legend">
  <div class="li"><div class="ld" style="background:#55aacc"></div> Cadastro</div>
  <div class="li"><div class="ld" style="background:#7ea8ff"></div> Comex / BD</div>
  <div class="li"><div class="ld" style="background:#a07eff"></div> Mkt Produtos</div>
  <div class="li"><div class="ld" style="background:#44cc88"></div> Regulatório</div>
  <div class="li"><div class="ld" style="background:#ffcc55"></div> Jurídico</div>
  <div class="li"><div class="ld" style="background:#ff9955"></div> Fiscal</div>
  <div class="li"><div class="ld" style="background:#88cc55"></div> Qualidade / GQ</div>
  <div class="li"><div class="ld" style="background:#cc77ff"></div> House (Agência)</div>
  <div class="li"><div class="ld" style="background:var(--orange)"></div> Gate de Decisão</div>
  <div class="li"><div class="ld" style="background:var(--green)"></div> Marco / Encerramento</div>
  <div style="margin-left:auto;font-size:9.5px;color:var(--text3)">
    ⏱ <span style="color:#22c97a">verde = &lt;5 dias</span> · 
    <span style="color:#f5a623">laranja = 5–30 dias</span> · 
    <span style="color:#e05c5c">vermelho = crítico / variável</span>
  </div>
</div>

<div id="panel">
  <div class="pcls" onclick="cp()">✕</div>
  <div id="pc"></div>
</div>

<script>
const D={
  origem:{
    owner:'Comex / BD',color:'#7ea8ff',bg:'#1a2040',lt:{l:'1–5 dias úteis',c:'f'},
    title:'Identificação de Oportunidade',
    desc:'A equipe de Comex ou BD identifica a oportunidade e traz a proposta já estruturada, incluindo os custos do produto e as condições contratuais com o fabricante. O fornecedor já foi negociado e homologado nesta fase.',
    raci:[['Comex / BD','R','A','',''],['Mkt Produtos','','','C','I']],rc:['Área','R','A','C','I'],
    inputs:['Oportunidade de mercado identificada','Custos do produto levantados','Contrato/proposta do fabricante','Fornecedor negociado e homologado'],
    outputs:['Proposta formalizada com viabilidade financeira'],
    ok:['Viabilidade financeira já vem com a proposta — não é um gap','Fornecedor homologado antes de iniciar o processo'],flags:[]
  },
  triagem:{
    owner:'Mkt Produtos · Projetos · Reg',color:'#a07eff',bg:'#1a1430',lt:{l:'3–7 dias úteis',c:'m'},
    title:'Reunião de Apresentação da Proposta',
    desc:'Marketing de Produtos avalia se o produto pode gerar canibalização no portfólio atual, se há algo parecido que impacta na estratégia e a viabilidade técnica e financeira. É esta equipe que aprova ou reprova o avanço.',
    raci:[['Mkt Produtos','R','A','',''],['Projetos / PM','C','','','I'],['Regulatório','C','','','I'],['Comex/BD apresenta','','','','I']],rc:['Área','R','A','C','I'],
    inputs:['Proposta com custos e contrato','Portfólio atual','Roadmap estratégico'],
    outputs:['Decisão documentada em ata','Mapa inicial de requisitos ANVISA'],
    ok:['Mkt Produtos tem autoridade para aprovar ou reprovar','Análise de canibalização e fit estratégico é a responsabilidade desta equipe'],flags:[]
  },
  gate1:{
    owner:'Gate de Decisão',color:'#f5a623',bg:'#1e1608',lt:{l:'Na reunião',c:'f'},
    title:'Gate 1 — Cabe no Portfólio?',
    desc:'Decisão de Mkt Produtos: o produto avança ou é encerrado. Critérios: risco de canibalização, fit estratégico, viabilidade financeira confirmada.',
    raci:[],rc:[],
    inputs:['Análise de portfólio de Mkt Produtos','Viabilidade financeira da proposta'],
    outputs:['SIM → kick-off','NÃO → encerrado com justificativa documentada'],
    ok:[],flags:[]
  },
  'cc-abertura':{
    owner:'Comex ou BD',color:'#7ea8ff',bg:'#1a2040',lt:{l:'1 dia útil',c:'f'},
    title:'Abertura do Change Control no Sistema',
    desc:'A equipe que startou o projeto (Comex ou BD) é responsável por abrir o controle de mudança no sistema com as informações iniciais do produto. Isso formaliza o projeto.',
    raci:[['Comex / BD (quem startou)','R','A','',''],['PM','','','','I'],['Regulatório','','','','I']],rc:['Área','R','A','C','I'],
    inputs:['Aprovação do Gate 1','Dados iniciais do produto'],
    outputs:['Change control aberto no sistema','Número do projeto gerado'],
    ok:['Responsabilidade clara: quem abre é quem startou o projeto'],flags:[]
  },
  kickoff:{
    owner:'Controle de Qualidade (GQ) · PM',color:'#88cc55',bg:'#121e12',lt:{l:'1–2 dias úteis',c:'f'},
    title:'GQ + PM Conduzem o Kick-off',
    desc:'Com o change control aberto, GQ e PM convocam e conduzem a reunião de kick-off com todas as áreas envolvidas. A PM (pessoa fixa, responsável por todos os projetos) assume formalmente o projeto e define cronograma e RACI.',
    raci:[['GQ (Controle de Qualidade)','R','','',''],['PM','R','A','',''],['Todas as áreas','','','C','I']],rc:['Área','R','A','C','I'],
    inputs:['Change control aberto','Dados iniciais do produto'],
    outputs:['Reunião de kick-off realizada','Cronograma macro definido','Responsáveis por trilha confirmados'],
    ok:['PM já está definida — mesma pessoa em todos os projetos','GQ co-lidera junto com a PM — não é o Regulatório'],flags:[]
  },
  'reg-checklist':{
    owner:'Regulatório',color:'#44cc88',bg:'#0e1a12',lt:{l:'1–2 dias úteis',c:'f'},
    title:'Checklist de Documentos ao Comex/BD',
    desc:'Regulatório envia para Comex/BD a lista padronizada de documentos técnicos necessários para o processo de registro na ANVISA. Este checklist já existe internamente no Regulatório.',
    raci:[['Regulatório','R','A','',''],['Comex/BD','','','','I']],rc:['Área','R','A','C','I'],
    inputs:['Kick-off realizado','Categoria do produto definida'],
    outputs:['Checklist de documentação enviado ao Comex/BD'],
    ok:['Checklist padronizado já existe no Regulatório'],flags:[]
  },
  'docs-coleta':{
    owner:'Comex / BD',color:'#7ea8ff',bg:'#1a2040',lt:{l:'5–15 dias úteis',c:'m'},
    title:'Coleta e Envio de Documentos ao Regulatório',
    desc:'Comex/BD coleta toda a documentação técnica do fabricante conforme o checklist enviado pelo Regulatório e entrega o pacote completo.',
    raci:[['Comex/BD','R','A','',''],['Regulatório recebe','','','','I']],rc:['Área','R','A','C','I'],
    inputs:['Checklist do Regulatório','Documentação técnica do fabricante'],
    outputs:['Pacote documental completo entregue ao Regulatório'],
    ok:[],flags:[]
  },
  'anvisa-sub':{
    owner:'Regulatório',color:'#44cc88',bg:'#0e1a12',lt:{l:'30 dias a 1+ ano',c:'s'},
    title:'Submissão para Registro na ANVISA',
    desc:'Com toda a documentação reunida e a arte aberta em mãos, o Regulatório protocola o pedido de registro do produto na ANVISA. Este é o principal risco de prazo do projeto — o prazo de resposta da ANVISA é externo e não controlável.',
    raci:[['Regulatório','R','A','',''],['PM monitora','','','','I']],rc:['Área','R','A','C','I'],
    inputs:['Documentação técnica completa (Comex/BD)','Arte aberta do produto (para ANVISA)'],
    outputs:['Número de protocolo ANVISA','Data estimada de análise'],
    ok:[],flags:['RISCO CRÍTICO: prazo de análise da ANVISA é o maior risco do cronograma do projeto. Varia de 30 dias a mais de 1 ano por categoria. PM deve registrar isso no plano de risco.']
  },
  'estrategia-inicial':{
    owner:'Mkt de Novos Produtos',color:'#a07eff',bg:'#1a1430',lt:{l:'7–15 dias úteis',c:'m'},
    title:'Estratégia de Posicionamento',
    desc:'Em paralelo à trilha regulatória, Mkt de Novos Produtos elabora o posicionamento estratégico: público-alvo, diferenciais, pricing e canal de distribuição.',
    raci:[['Mkt Novos Produtos','R','A','',''],['Mkt Produtos','','','C',''],['Diretoria Comercial','','','C','I']],rc:['Área','R','A','C','I'],
    inputs:['Briefing do produto','Análise de concorrentes','Dados de mercado'],
    outputs:['Documento de posicionamento','Proposta de pricing','Estratégia de canal'],
    ok:[],flags:[]
  },
  'kv-arte-aberta':{
    owner:'Mkt Produtos → House',color:'#cc77ff',bg:'#1a1220',lt:{l:'10–20 dias úteis',c:'m'},
    title:'Briefing → KV + Arte Aberta para ANVISA',
    desc:'Marketing prepara o briefing criativo. A House produz o Key Visual (KV) do produto. Arte aprovada pelo CEO. Em seguida, é preparada a arte aberta (sem número de registro ANVISA) para protocolo no órgão.\n\nIMPORTANTE: esta é a arte aberta para ANVISA — não a arte de embalagem final. A arte de embalagem com dizeres técnicos e número de registro só é feita APÓS o deferimento.',
    raci:[['Mkt Produtos','R','','',''],['House','R','','',''],['CEO','','A','',''],['Regulatório','','','C','I']],rc:['Área','R','A','C','I'],
    inputs:['Estratégia de posicionamento','Guia de marca Rennova'],
    outputs:['KV aprovado pelo CEO','Arte aberta para protocolo ANVISA'],
    ok:['Arte aberta ≠ arte de embalagem final. São dois artefatos distintos.'],
    flags:['Não há SLA formal para aprovação do CEO. Definir prazo máximo para evitar gargalo nesta trilha.']
  },
  inpi:{
    owner:'Jurídico',color:'#ffcc55',bg:'#1e1808',lt:{l:'5–10 dias úteis',c:'m'},
    title:'Análise do Nome no INPI',
    desc:'Jurídico realiza busca de disponibilidade do nome/marca no banco do INPI. IMPORTANTE: esta tarefa só inicia após o CEO aprovar o KV do produto apresentado pelo Marketing — pois é no KV que o nome comercial do produto é definido e confirmado. Se o nome estiver indisponível, retorna ao Mkt Produtos para decisão de novo nome.',
    raci:[['Jurídico','R','A','',''],['Mkt Produtos','','','C','I']],rc:['Área','R','A','C','I'],
    inputs:['KV aprovado pelo CEO (com nome do produto confirmado)','Classe NICE aplicável'],
    outputs:['Relatório de disponibilidade','Nome disponível → segue / Indisponível → Mkt decide novo nome'],
    ok:['Só inicia após CEO aprovar o KV — nome precisa estar confirmado antes da busca no INPI'],
    flags:['Se o nome estiver indisponível, pode gerar retrabalho em briefing e arte. Ideal resolver o mais cedo possível.']
  },
  liminar:{
    owner:'Jurídico',color:'#ffcc55',bg:'#1e1808',lt:{l:'Depósito: 1–2 dias / INPI: 18–24 meses',c:'s'},
    title:'Depósito de Marca / Liminar de Proteção',
    desc:'Com disponibilidade confirmada, Jurídico realiza o depósito da marca no INPI e, se necessário, obtém liminar para proteção imediata enquanto o INPI processa o registro completo.',
    raci:[['Jurídico','R','A','',''],['Diretoria','','A','','']],rc:['Área','R','A','C','I'],
    inputs:['Nome disponível confirmado pelo INPI'],
    outputs:['Protocolo de depósito de marca','Liminar de proteção (se aplicável)'],
    ok:[],flags:[]
  },
  'aguarda-anvisa':{
    owner:'Regulatório · PM',color:'#44cc88',bg:'#0e1a12',lt:{l:'Variável — externo',c:'s'},
    title:'Aguardando Deferimento ANVISA',
    desc:'O projeto aguarda a resposta da ANVISA. A PM monitora o andamento e comunica as áreas sobre atualizações. NENHUMA etapa de cadastro ou arte de embalagem começa antes do deferimento ser obtido.',
    raci:[['Regulatório','R','A','',''],['PM','R','','',''],['Todas as áreas','','','','I']],rc:['Área','R','A','C','I'],
    inputs:['Protocolo ANVISA ativo'],
    outputs:['Deferimento publicado no DOU','Ou: indeferimento / exigências'],
    ok:['Cadastro do produto no sistema NÃO começa antes do deferimento','Arte de embalagem NÃO começa antes do deferimento'],
    flags:['Este é o maior risco de prazo do projeto. Deve haver plano de contingência documentado para cenários de indeferimento.']
  },
  gate2:{
    owner:'Gate de Decisão',color:'#f5a623',bg:'#1e1608',lt:{l:'Decisão da ANVISA',c:'s'},
    title:'Gate 2 — Deferimento ANVISA?',
    desc:'A ANVISA pode: deferir, deferir com exigências (que precisam ser respondidas) ou indeferir. Cada cenário exige resposta diferente.',
    raci:[],rc:[],
    inputs:['Publicação oficial da ANVISA / DOU'],
    outputs:['Deferido → dispara Fase 6 integralmente','Exigências → Reg responde (30–60 dias)','Indeferido → análise de recurso ou encerramento do projeto'],
    ok:[],flags:['Indeferimento: quem decide se recorre? Em quanto tempo? Qual o critério para encerrar o projeto? Isso precisa ser definido na política interna.']
  },
  'cad-abertura':{
    owner:'BD ou Comex (quem startou)',color:'#7ea8ff',bg:'#1a2040',lt:{l:'1 dia útil',c:'f'},
    title:'Abre o Cadastro no Sistema',
    desc:'A equipe que startou o projeto (BD ou Comex) é responsável por iniciar o processo de cadastro no sistema com os dados básicos do produto. A partir daqui o fluxo segue dentro do sistema com as validações das áreas de Cadastro, Fiscal, Regulatório e Comex.',
    raci:[['BD / Comex (quem startou)','R','A','',''],['Cadastro','','','','I']],rc:['Área','R','A','C','I'],
    inputs:['Deferimento ANVISA obtido','Dados básicos do produto (nome, fornecedor, descrição inicial)'],
    outputs:['Processo de cadastro aberto no sistema','Fluxo interno de cadastro iniciado'],
    ok:['BD ou Comex que startou o projeto é quem abre — responsabilidade clara','A partir daqui o processo segue no sistema conforme o sub-fluxo de cadastro'],flags:[]
  },
  'cad-verifica':{
    owner:'Equipe de Cadastro',color:'#55aacc',bg:'#101e26',lt:{l:'1 dia útil',c:'f'},
    title:'Verifica se Produto já tem Cadastro',
    desc:'A equipe de Cadastro busca no sistema se o produto (ou variação dele) já existe. Esta etapa só começa após o deferimento da ANVISA — pois o número de registro é obrigatório para o cadastro.',
    raci:[['Cadastro','R','A','',''],['Comex/BD','','','C','']],rc:['Área','R','A','C','I'],
    inputs:['Deferimento ANVISA obtido','Dados básicos do produto'],
    outputs:['Produto existe no sistema → atualiza e finaliza','Produto não existe → segue sub-fluxo completo'],
    ok:['Cadastro só começa após deferimento ANVISA — número de registro obrigatório'],flags:[]
  },
  'gate-cad':{
    owner:'Gate de Cadastro',color:'#f5a623',bg:'#1e1608',lt:{l:'Imediato',c:'f'},
    title:'Gate — Produto já tem Cadastro?',
    desc:'Se o produto já existe no sistema, o processo é acelerado: atualiza os dados faltantes e segue. Se não existe, percorre o sub-fluxo completo de validação.',
    raci:[],rc:[],
    inputs:['Resultado da busca no sistema'],
    outputs:['SIM → atualização e finalização do cadastro','NÃO → sub-fluxo completo (Fiscal + Reg + Comex)'],
    ok:[],flags:[]
  },
  'fiscal-ncm':{
    owner:'Equipe Fiscal',color:'#ff9955',bg:'#1e1210',lt:{l:'2–5 dias úteis',c:'m'},
    title:'Validação do NCM — Fiscal',
    desc:'Equipe fiscal confirma o NCM correto para fins tributários internos: ICMS, PIS/COFINS, Substituição Tributária, benefícios fiscais estaduais aplicáveis.',
    raci:[['Fiscal','R','A','',''],['Comex','','','C',''],['Cadastro','','','','I']],rc:['Área','R','A','C','I'],
    inputs:['NCM proposto','Descrição técnica do produto','Estado principal de destino'],
    outputs:['NCM validado (tributário)','Carga tributária calculada','Alertas de benefícios ou riscos fiscais'],
    ok:['Checklist de validação fiscal já existe internamente na equipe Fiscal'],flags:[]
  },
  'reg-cadastro':{
    owner:'Regulatório',color:'#44cc88',bg:'#0e1a12',lt:{l:'1–2 dias úteis',c:'f'},
    title:'Dados Regulatórios para Cadastro',
    desc:'Regulatório insere as informações que só ele possui: número de registro ANVISA (obtido no deferimento), descrição técnica normalizada, validade do registro e shelf life do produto.',
    raci:[['Regulatório','R','A','',''],['Cadastro','','','','I']],rc:['Área','R','A','C','I'],
    inputs:['Número de registro ANVISA (deferimento em mãos)','Dossier técnico do produto'],
    outputs:['Descrição técnica normalizada do item','Número de registro ANVISA','Data de validade do registro ANVISA','Shelf life (prazo de validade em meses)'],
    ok:['O número ANVISA já está disponível porque o cadastro só começa após deferimento — sem limbo de dado faltante'],flags:[]
  },
  'comex-val':{
    owner:'Comex',color:'#7ea8ff',bg:'#1a2040',lt:{l:'2–5 dias úteis',c:'m'},
    title:'Validação NCM + Fornecedor — Comex',
    desc:'Comex valida o NCM sob a ótica de importação (II, IPI, PIS/COFINS importação, antidumping, licença de importação). Confirma fornecedor e valida Incoterm e lead time de entrega.',
    raci:[['Comex','R','A','',''],['Fiscal','','','C',''],['Cadastro','','','','I']],rc:['Área','R','A','C','I'],
    inputs:['NCM proposto','País de origem','Fornecedor negociado'],
    outputs:['NCM validado para importação','Fornecedor confirmado','Lead time e Incoterm validados'],
    ok:['Fornecedor já foi homologado na Fase 1 — não há retrabalho aqui'],flags:[]
  },
  'cad-finaliza':{
    owner:'Equipe de Cadastro',color:'#55aacc',bg:'#101e26',lt:{l:'1–2 dias úteis',c:'f'},
    title:'Finaliza Cadastro + Gera Código do Item e EAN',
    desc:'Cadastro consolida todas as informações validadas pelas três áreas. Gera o Código do Item no sistema. Verifica se o produto possui código de barras: se NÃO tiver, gera novo EAN-13 ou GTIN. A própria equipe de Cadastro valida internamente antes de ativar o SKU.',
    raci:[['Cadastro','R','A','','']],rc:['Área','R','A','C','I'],
    inputs:['NCM validado (Fiscal + Comex)','Dados regulatórios completos (Reg)','Dados técnicos e comerciais do produto'],
    outputs:['Código do Item gerado e ativo','EAN-13 / GTIN gerado (se produto não tinha)','SKU ativo no sistema'],
    ok:['A equipe de Cadastro valida internamente antes de ativar — não há dependência externa nesta etapa'],flags:[]
  },
  dizeres:{
    owner:'Regulatório',color:'#44cc88',bg:'#0e1a12',lt:{l:'5–10 dias úteis',c:'m'},
    title:'Elaboração dos Dizeres Técnicos',
    desc:'Com o deferimento em mãos, Regulatório elabora o texto oficial que constará na embalagem: indicações, composição, modo de uso, advertências e número de registro ANVISA.',
    raci:[['Regulatório','R','A','',''],['Mkt Produtos','','','C','I']],rc:['Área','R','A','C','I'],
    inputs:['Deferimento ANVISA com número de registro','Especificações técnicas do produto'],
    outputs:['Dizeres técnicos finalizados e aprovados','Instrução de uso do produto'],
    ok:[],flags:[]
  },
  'arte-emb':{
    owner:'Mkt Produtos → House',color:'#cc77ff',bg:'#1a1220',lt:{l:'5–10 dias úteis',c:'m'},
    title:'Abertura de Gestão de Arte de Embalagem',
    desc:'Esta é a arte de embalagem FINAL — diferente da arte aberta feita na Fase 4. Mkt abre o processo no sistema. House produz a arte com dizeres técnicos aprovados + KV + número de registro ANVISA.',
    raci:[['Mkt Produtos','R','','',''],['House','R','','',''],['Regulatório','','','C','']],rc:['Área','R','A','C','I'],
    inputs:['Dizeres técnicos aprovados pelo Regulatório','KV aprovado (da Fase 4)','Número de registro ANVISA'],
    outputs:['Arte de embalagem v1 (rascunho)'],
    ok:['Arte de embalagem ≠ arte aberta da Fase 4. A embalagem final só é feita aqui, pós-deferimento.'],flags:[]
  },
  'revisao-arte':{
    owner:'House · Mkt Produtos · Regulatório',color:'#cc77ff',bg:'#1a1220',lt:{l:'10–20 dias úteis',c:'m'},
    title:'Roda de Revisão de Arte',
    desc:'Ciclos iterativos de revisão entre House, Mkt Produtos e Regulatório. Recomendação: máximo 3 rodadas com SLA de 2 dias úteis por área para retorno de comentários.',
    raci:[['House','R','','',''],['Mkt Produtos','','A','C',''],['Regulatório','','A','C',''],['Qualidade','','','C','I']],rc:['Área','R','A','C','I'],
    inputs:['Arte de embalagem v1','Dizeres técnicos de referência'],
    outputs:['Arte de embalagem final aprovada por todas as áreas'],
    ok:[],flags:['Sem limite de rodadas e SLA por área, esse ciclo pode se arrastar. Recomendação: formalizar máx. 3 rodadas + 2 dias úteis de retorno por área.']
  },
  homologacao:{
    owner:'Regulatório',color:'#44cc88',bg:'#0e1a12',lt:{l:'2–3 dias úteis',c:'f'},
    title:'Homologa Arte + Envia ao Fabricante',
    desc:'Após aprovação de todas as áreas, Regulatório homologa oficialmente a arte no sistema e envia os arquivos finais ao fabricante para início da produção das embalagens.',
    raci:[['Regulatório','R','A','',''],['Comex/BD','','','C','I']],rc:['Área','R','A','C','I'],
    inputs:['Arte aprovada por todas as áreas'],
    outputs:['Arte homologada no sistema','Arquivos enviados ao fabricante','Autorização para produção'],
    ok:[],flags:[]
  },
  'estrategia-final':{
    owner:'Mkt Produtos',color:'#a07eff',bg:'#1a1430',lt:{l:'5–10 dias úteis',c:'m'},
    title:'Aprovação da Estratégia de Lançamento',
    desc:'Em paralelo à gestão de arte de embalagem, a estratégia final de lançamento é aprovada. Não é um passo sequencial — deve correr ao mesmo tempo para não atrasar o go-to-market.',
    raci:[['Mkt Produtos','R','A','',''],['Diretoria','','A','',''],['Comex/BD','','','C','I']],rc:['Área','R','A','C','I'],
    inputs:['Estratégia elaborada na Fase 4','Confirmações pós-deferimento'],
    outputs:['Estratégia de lançamento aprovada formalmente'],
    ok:['Em paralelo com arte de embalagem — não sequencial. Corrige perda de tempo do fluxo anterior.'],flags:[]
  },
  racional:{
    owner:'Mkt Produtos → Gerente do Produto',color:'#a07eff',bg:'#1a1430',lt:{l:'2–3 dias úteis',c:'f'},
    title:'Entrega do Racional Estratégico',
    desc:'Marketing entrega ao gerente responsável pelo produto o documento completo: posicionamento, pricing, estratégia de comunicação e metas de lançamento. Transferência formal de gestão do produto.',
    raci:[['Mkt Produtos','R','A','',''],['Gerente do Produto','','','','I']],rc:['Área','R','A','C','I'],
    inputs:['Estratégia aprovada','Dados finais do produto'],
    outputs:['Racional estratégico completo','Handoff formal para o gerente do produto'],
    ok:[],flags:[]
  },
  forecast:{
    owner:'Comex / BD + CEO',color:'#7ea8ff',bg:'#1a2040',lt:{l:'7–14 dias úteis',c:'m'},
    title:'Planejamento do Forecast de Compra',
    desc:'Comex/BD e CEO planejam o forecast de compra em paralelo com a gestão de arte. Não aguarda a arte finalizar — o lead time de importação é longo e qualquer atraso posterga o lançamento. Define volumes, Incoterm, cronograma de entrega e emite a 1ª PO.',
    raci:[['Comex/BD','R','','',''],['CEO','','A','',''],['Financeiro','','','C','I']],rc:['Área','R','A','C','I'],
    inputs:['Deferimento ANVISA','Estimativa de demanda (da estratégia)'],
    outputs:['Purchase Order inicial emitida','Forecast de 6 meses','Data estimada de chegada do estoque'],
    ok:['Em paralelo com arte — não sequencial. Evita perda de semanas de lead time.','CEO é aprovador desta etapa — alinhado com o que foi informado.'],flags:[]
  },
  encerramento:{
    owner:'PM · Todas as Áreas',color:'#22c97a',bg:'#0a1a0e',lt:{l:'1–2 dias úteis',c:'f'},
    title:'Encerramento — Produto Pronto para Lançar',
    desc:'PM valida o checklist de encerramento com todas as áreas. Com tudo aprovado, o produto está pronto para o processo de lançamento (que é um fluxo separado).',
    raci:[['PM','R','A','',''],['Todas as áreas','','','C','I']],rc:['Área','R','A','C','I'],
    inputs:['Cadastro ativo no sistema','Arte de embalagem homologada','Forecast / PO emitida','Estratégia de lançamento aprovada','Marca protegida (depósito INPI)'],
    outputs:['Checklist de encerramento aprovado','Produto liberado para processo de lançamento'],
    ok:['Lançamento é outro fluxo — este processo termina aqui com o produto pronto'],flags:[]
  }
};

function op(k){
  const d=D[k]; if(!d) return;
  const panel=document.getElementById('panel');
  const pc=document.getElementById('pc');
  const lc=d.lt?d.lt.c:'f';
  const ll=d.lt?d.lt.l:'';
  let raciHtml='';
  if(d.raci&&d.raci.length){
    raciHtml=`<div class="psec"><div class="psec-t">Matriz RACI</div>
    <table class="raci-t"><thead><tr>${d.rc.map(c=>`<th>${c}</th>`).join('')}</tr></thead><tbody>
    ${d.raci.map(r=>`<tr>${r.map((c,i)=>{let cl='';if(c==='R')cl='rR';if(c==='A')cl='rA';if(c==='C')cl='rC';if(c==='I')cl='rI';return`<td class="${cl}">${c||'—'}</td>`}).join('')}</tr>`).join('')}
    </tbody></table></div>`;
  }
  const flagsH=d.flags.map(f=>`<div class="pflag">⚠ ${f}</div>`).join('');
  const okH=d.ok.map(o=>`<div class="pok">✓ ${o}</div>`).join('');
  pc.innerHTML=`
    <div class="pbadge" style="background:${d.bg};color:${d.color};border:1px solid ${d.color}33">${d.owner}</div>
    <div class="ptitle">${d.title}</div>
    ${ll?`<div class="plt ${lc}">⏱ Lead Time: ${ll}</div>`:''}
    <div class="pdesc">${d.desc}</div>
    ${(d.flags&&d.flags.length)||(d.ok&&d.ok.length)?`<div class="psec"><div class="psec-t">Pontos de Atenção + Confirmações</div>${flagsH}${okH}</div>`:''}
    ${raciHtml}
    <div class="psec"><div class="psec-t">Entradas (Inputs)</div><div class="pbox"><ul class="plist">${d.inputs.map(i=>`<li>${i}</li>`).join('')}</ul></div></div>
    <div class="psec"><div class="psec-t">Saídas (Outputs)</div><div class="pbox"><ul class="plist">${d.outputs.map(o=>`<li>${o}</li>`).join('')}</ul></div></div>
  `;
  panel.classList.add('open');
}
function cp(){document.getElementById('panel').classList.remove('open')}
document.addEventListener('keydown',e=>{if(e.key==='Escape')cp()});
</script>

</div>

<!-- ══════════════ KANBAN PAGE ══════════════ -->
<div id="kanban-page" class="page">


<header>
  <div class="logo">
    <div class="logo-dot"></div>
    Rennova <span style="color:var(--text3);margin:0 4px">·</span> Kanban de Projetos
  </div>
  <div class="hactions">
    <button class="btn" onclick="switchView('portfolio')"><i class="ti ti-layout-grid"></i> Portfólio</button>
    <button class="btn" onclick="switchView('kanban')"><i class="ti ti-columns"></i> Kanban</button>
    <button class="btn primary" onclick="openNewProject()"><i class="ti ti-plus"></i> Novo Projeto</button>
  </div>
</header>

<div class="tabs" id="tabs"></div>

<div class="main">
  <div class="sidebar">
    <div class="sidebar-header">
      Projetos <span id="proj-count" style="background:var(--s3);border-radius:10px;padding:1px 7px;font-size:10px;color:var(--text3)">0</span>
    </div>
    <div class="project-list" id="project-list"></div>
  </div>
  <div id="view-container" style="flex:1;overflow:hidden;display:flex;flex-direction:column">
    <div id="kanban-view" style="flex:1;overflow:auto;display:none">
      <div class="kanban-wrap"><div class="kanban" id="kanban-board"></div></div>
    </div>
    <div id="portfolio-view" style="flex:1;overflow:auto;display:none">
      <div class="portfolio-grid" id="portfolio-grid"></div>
    </div>
    <div id="empty-view" style="flex:1;display:flex">
      <div class="empty">
        <i class="ti ti-rocket"></i>
        <p style="font-size:15px;font-weight:500;color:var(--text2)">Nenhum projeto ainda</p>
        <p>Clique em "Novo Projeto" para começar</p>
        <button class="btn primary" style="margin-top:8px" onclick="openNewProject()"><i class="ti ti-plus"></i> Criar primeiro projeto</button>
      </div>
    </div>
  </div>
</div>

<!-- DETAIL PANEL -->
<div id="detail">
  <div id="det-content"></div>
</div>

<!-- NEW PROJECT MODAL -->
<div id="modal-bg">
  <div class="modal">
    <div class="modal-header">
      <div class="modal-title">Novo Projeto de Lançamento</div>
      <button class="btn" onclick="closeModal()"><i class="ti ti-x"></i></button>
    </div>
    <div class="modal-body">
      <div>
        <label class="form-label">Nome do Produto *</label>
        <input class="form-input" id="np-name" placeholder="Ex: Hidratante Facial FPS 50">
      </div>
      <div class="form-row">
        <div>
          <label class="form-label">Área Iniciadora *</label>
          <select class="form-select" id="np-area">
            <option value="Comex">Comex</option>
            <option value="BD">BD (Business Development)</option>
          </select>
        </div>
        <div>
          <label class="form-label">Responsável (PM)</label>
          <input class="form-input" id="np-pm" placeholder="Nome da PM">
        </div>
      </div>
      <div class="form-row">
        <div>
          <label class="form-label">Categoria ANVISA</label>
          <select class="form-select" id="np-cat">
            <option value="Cosmético">Cosmético</option>
            <option value="Dispositivo Médico">Dispositivo Médico</option>
            <option value="Suplemento">Suplemento</option>
            <option value="Medicamento">Medicamento</option>
            <option value="Outro">Outro</option>
          </select>
        </div>
        <div>
          <label class="form-label">Data de Início</label>
          <input class="form-input" type="date" id="np-start">
        </div>
      </div>
      <div>
        <label class="form-label">Fornecedor</label>
        <input class="form-input" id="np-supplier" placeholder="Nome do fornecedor">
      </div>
      <div>
        <label class="form-label">Observações iniciais</label>
        <textarea class="form-input" id="np-notes" style="min-height:60px;resize:vertical" placeholder="Contexto, oportunidade, observações..."></textarea>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn" onclick="closeModal()">Cancelar</button>
      <button class="btn primary" onclick="createProject()"><i class="ti ti-rocket"></i> Criar Projeto</button>
    </div>
  </div>
</div>

<script>
const PHASES = [
  {id:'fase1', label:'Fase 1', title:'Origem', color:'#4f7fff'},
  {id:'fase2', label:'Fase 2', title:'Triagem', color:'#a07eff'},
  {id:'fase3', label:'Fase 3', title:'Kick-off', color:'#88cc55'},
  {id:'fase4', label:'Fase 4', title:'Pré-ANVISA', color:'#44cc88'},
  {id:'gate2', label:'Gate', title:'Aguarda ANVISA', color:'#f5a623', isGate:true},
  {id:'fase6a', label:'Fase 6A', title:'Cadastro', color:'#55aacc'},
  {id:'fase6b', label:'Fase 6B', title:'Arte Embalagem', color:'#cc77ff'},
  {id:'fase6c', label:'Fase 6C', title:'Estratégia', color:'#a07eff'},
  {id:'fase6d', label:'Fase 6D', title:'Forecast', color:'#7ea8ff'},
  {id:'encerramento', label:'Encerramento', title:'Pronto p/ Lançar', color:'#22c97a'}
];

const TASK_TEMPLATES = {
  fase1:[
    {id:'t1_1',title:'Identificação de Oportunidade',owner:'Comex / BD',ownerColor:'#7ea8ff',lt:'f',ltLabel:'1–5 dias',raci:{R:'Comex/BD',A:'Comex/BD',C:'Mkt Produtos',I:'—'},desc:'Proposta trazida com custos, contrato e fornecedor já negociado.',inputs:['Oportunidade de mercado','Custos do produto','Proposta do fabricante'],outputs:['Proposta formalizada com viabilidade']},
  ],
  fase2:[
    {id:'t2_1',title:'Reunião de Apresentação da Proposta',owner:'Mkt Produtos + Projetos + Reg',ownerColor:'#a07eff',lt:'m',ltLabel:'3–7 dias',raci:{R:'Mkt Produtos',A:'Mkt Produtos',C:'Regulatório / Projetos',I:'Comex/BD'},desc:'Marketing avalia canibalização e fit estratégico. Regulatório mapeia requisitos ANVISA.',inputs:['Proposta com viabilidade','Portfólio atual'],outputs:['Decisão documentada em ata','Mapa de requisitos ANVISA']},
    {id:'t2_gate',title:'Gate 1 — Cabe no Portfólio?',owner:'Gate de Decisão',ownerColor:'#f5a623',lt:'f',ltLabel:'Na reunião',isGate:true,raci:{R:'Mkt Produtos',A:'Mkt Produtos',C:'—',I:'—'},desc:'SIM → kick-off | NÃO → encerrado com justificativa.',inputs:['Análise de portfólio'],outputs:['Aprovado ou encerrado com justificativa']},
  ],
  fase3:[
    {id:'t3_1',title:'Abertura do Change Control no Sistema',owner:'Comex ou BD (quem startou)',ownerColor:'#7ea8ff',lt:'f',ltLabel:'1 dia',raci:{R:'Comex/BD',A:'Comex/BD',C:'—',I:'PM / Reg'},desc:'Quem startou o projeto abre o CC com dados iniciais do produto.',inputs:['Aprovação Gate 1','Dados iniciais'],outputs:['Change control aberto','Nº do projeto gerado']},
    {id:'t3_2',title:'GQ + PM Conduzem o Kick-off',owner:'Controle de Qualidade + PM',ownerColor:'#88cc55',lt:'f',ltLabel:'1–2 dias',raci:{R:'GQ / PM',A:'PM',C:'Todas as áreas',I:'—'},desc:'GQ e PM convocam e conduzem o kick-off. Define cronograma e RACI por trilha.',inputs:['Change control aberto'],outputs:['Kick-off realizado','Cronograma macro','RACI por trilha']},
  ],
  fase4:[
    {id:'t4_1',title:'Reg envia Checklist de Docs ao Comex/BD',owner:'Regulatório',ownerColor:'#44cc88',lt:'f',ltLabel:'1–2 dias',raci:{R:'Regulatório',A:'Regulatório',C:'—',I:'Comex/BD'},desc:'Lista padronizada de documentos necessários para a ANVISA. Checklist já existe internamente.',inputs:['Kick-off realizado','Categoria do produto'],outputs:['Checklist enviado ao Comex/BD']},
    {id:'t4_2',title:'Estratégia de Posicionamento',owner:'Mkt de Novos Produtos',ownerColor:'#a07eff',lt:'m',ltLabel:'7–15 dias',raci:{R:'Mkt Novos Produtos',A:'Mkt Novos Produtos',C:'Diretoria',I:'—'},desc:'Posicionamento, pricing, canal, diferenciais vs. concorrentes.',inputs:['Briefing do produto','Análise de mercado'],outputs:['Documento de posicionamento','Proposta de pricing']},
    {id:'t4_3',title:'Briefing → KV + Arte Aberta (ANVISA)',owner:'Mkt Produtos → House',ownerColor:'#cc77ff',lt:'m',ltLabel:'10–20 dias',raci:{R:'House / Mkt',A:'CEO',C:'Regulatório',I:'—'},desc:'KV aprovado pelo CEO. Arte aberta (sem nº registro) preparada para ANVISA. Arte aberta ≠ arte de embalagem final.',inputs:['Estratégia aprovada','Guia de marca'],outputs:['KV aprovado pelo CEO','Arte aberta para ANVISA']},
    {id:'t4_4',title:'Coleta e Envio de Docs ao Regulatório',owner:'Comex / BD',ownerColor:'#7ea8ff',lt:'m',ltLabel:'5–15 dias',raci:{R:'Comex/BD',A:'Comex/BD',C:'—',I:'Regulatório'},desc:'Comex/BD reúne documentação técnica do fabricante conforme checklist do Regulatório.',inputs:['Checklist do Regulatório','Docs técnicos do fabricante'],outputs:['Pacote documental entregue ao Reg']},
    {id:'t4_5',title:'Análise do Nome no INPI',owner:'Jurídico',ownerColor:'#ffcc55',lt:'m',ltLabel:'5–10 dias',dep:'Após CEO aprovar KV (t4_3)',raci:{R:'Jurídico',A:'Jurídico',C:'Mkt Produtos',I:'—'},desc:'Só inicia após CEO aprovar o KV. Busca disponibilidade de marca. Se indisponível → Mkt decide novo nome.',inputs:['KV aprovado pelo CEO (nome confirmado)','Classe NICE'],outputs:['Relatório de disponibilidade de marca']},
    {id:'t4_6',title:'Depósito de Marca / Liminar INPI',owner:'Jurídico',ownerColor:'#ffcc55',lt:'s',ltLabel:'Depósito: 1–2 dias / Registro: 18–24 meses',raci:{R:'Jurídico',A:'Diretoria',C:'—',I:'—'},desc:'Depósito após disponibilidade confirmada. Liminar protege o nome enquanto o INPI processa.',inputs:['Nome disponível confirmado'],outputs:['Protocolo de depósito de marca','Liminar (se necessário)']},
    {id:'t4_7',title:'Submissão para Registro na ANVISA',owner:'Regulatório',ownerColor:'#44cc88',lt:'s',ltLabel:'30 dias a 1+ ano ⚠',raci:{R:'Regulatório',A:'Regulatório',C:'—',I:'PM'},desc:'Protocola o registro com toda a documentação. Principal risco de prazo do projeto.',inputs:['Docs completos do Comex/BD','Arte aberta para ANVISA'],outputs:['Nº de protocolo ANVISA','Estimativa de prazo']},
  ],
  gate2:[
    {id:'tg2_1',title:'Gate 2 — Aguardando Deferimento ANVISA',owner:'Regulatório · PM monitora',ownerColor:'#f5a623',isGate:true,lt:'s',ltLabel:'Variável — risco crítico',raci:{R:'Regulatório',A:'Regulatório',C:'—',I:'PM / Todas'},desc:'Nenhuma etapa de cadastro ou arte de embalagem começa antes do deferimento. PM monitora e comunica.',inputs:['Protocolo ANVISA ativo'],outputs:['Deferimento publicado no DOU']},
  ],
  fase6a:[
    {id:'t6a_0',title:'BD/Comex Abre Cadastro no Sistema',owner:'BD ou Comex (quem startou)',ownerColor:'#7ea8ff',lt:'f',ltLabel:'1 dia',raci:{R:'Comex/BD',A:'Comex/BD',C:'—',I:'Cadastro'},desc:'Quem startou o projeto inicia o processo de cadastro no sistema com os dados básicos.',inputs:['Deferimento ANVISA obtido','Dados básicos do produto'],outputs:['Cadastro aberto no sistema']},
    {id:'t6a_1',title:'Verificação: Produto já tem Cadastro?',owner:'Equipe de Cadastro',ownerColor:'#55aacc',lt:'f',ltLabel:'1 dia',isGate:true,raci:{R:'Cadastro',A:'Cadastro',C:'Comex/BD',I:'—'},desc:'SIM → atualiza dados e finaliza | NÃO → sub-fluxo completo de validação.',inputs:['Dados básicos do produto'],outputs:['Existe: atualiza → fim | Não existe: segue validação']},
    {id:'t6a_2',title:'Fiscal: Valida NCM (tributos)',owner:'Equipe Fiscal',ownerColor:'#ff9955',lt:'m',ltLabel:'2–5 dias',raci:{R:'Fiscal',A:'Fiscal',C:'Comex',I:'Cadastro'},desc:'ICMS, PIS/COFINS, ST, benefícios fiscais. Checklist padronizado já existe no Fiscal.',inputs:['NCM proposto','Descrição do produto','Estado de destino'],outputs:['NCM validado (tributário)','Carga tributária calculada']},
    {id:'t6a_3',title:'Reg: Dados Regulatórios p/ Cadastro',owner:'Regulatório',ownerColor:'#44cc88',lt:'f',ltLabel:'1–2 dias',raci:{R:'Regulatório',A:'Regulatório',C:'—',I:'Cadastro'},desc:'Insere: nº de registro ANVISA, descrição técnica, validade do registro e shelf life. Disponível pois o cadastro só começa após deferimento.',inputs:['Nº de registro ANVISA (deferimento em mãos)'],outputs:['Nº registro ANVISA','Descrição técnica','Validade do registro','Shelf life']},
    {id:'t6a_4',title:'Comex: Valida NCM + Fornecedor',owner:'Comex',ownerColor:'#7ea8ff',lt:'m',ltLabel:'2–5 dias',raci:{R:'Comex',A:'Comex',C:'Fiscal',I:'Cadastro'},desc:'Valida NCM para importação (II, IPI, antidumping, LI). Confirma fornecedor (já homologado desde Fase 1), Incoterm e lead time.',inputs:['NCM proposto','País de origem','Fornecedor'],outputs:['NCM validado (importação)','Fornecedor e Incoterm confirmados']},
    {id:'t6a_5',title:'Cadastro Finaliza + Gera Códigos',owner:'Equipe de Cadastro',ownerColor:'#55aacc',lt:'f',ltLabel:'1–2 dias',raci:{R:'Cadastro',A:'Cadastro',C:'—',I:'—'},desc:'Consolida todas as validações. Gera Código do Item. Gera EAN-13/GTIN se produto não tem código de barras. Cadastro valida internamente antes de ativar.',inputs:['Validações de Fiscal + Reg + Comex'],outputs:['Código do Item ativo','EAN/GTIN gerado (se necessário)','SKU ativo no sistema']},
  ],
  fase6b:[
    {id:'t6b_1',title:'Reg: Elabora Dizeres Técnicos',owner:'Regulatório',ownerColor:'#44cc88',lt:'m',ltLabel:'5–10 dias',raci:{R:'Regulatório',A:'Regulatório',C:'Mkt Produtos',I:'—'},desc:'Texto regulatório oficial da embalagem: indicações, composição, modo de uso, advertências, nº de registro.',inputs:['Deferimento ANVISA','Specs técnicas'],outputs:['Dizeres técnicos aprovados','Instrução de uso']},
    {id:'t6b_2',title:'Abertura de Gestão de Arte de Embalagem',owner:'Mkt Produtos → House',ownerColor:'#cc77ff',lt:'m',ltLabel:'5–10 dias',raci:{R:'House / Mkt',A:'Mkt Produtos',C:'Regulatório',I:'—'},desc:'Arte de embalagem FINAL — diferente da arte aberta da Fase 4. Usa dizeres técnicos + KV + nº registro ANVISA.',inputs:['Dizeres técnicos aprovados','KV aprovado','Nº registro ANVISA'],outputs:['Arte de embalagem v1']},
    {id:'t6b_3',title:'Roda de Revisão de Arte',owner:'House · Mkt Produtos · Regulatório',ownerColor:'#cc77ff',lt:'m',ltLabel:'10–20 dias',raci:{R:'House',A:'Mkt / Reg',C:'GQ',I:'—'},desc:'Máx. 3 rodadas. SLA: 2 dias úteis por área para retorno de comentários.',inputs:['Arte de embalagem v1'],outputs:['Arte final aprovada por todas as áreas']},
    {id:'t6b_4',title:'Homologação + Envio ao Fabricante',owner:'Regulatório',ownerColor:'#44cc88',lt:'f',ltLabel:'2–3 dias',raci:{R:'Regulatório',A:'Regulatório',C:'Comex/BD',I:'—'},desc:'Reg homologa no sistema e envia arquivos finais ao fabricante para produção.',inputs:['Arte aprovada por todas as áreas'],outputs:['Arte homologada no sistema','Arquivos enviados ao fabricante']},
  ],
  fase6c:[
    {id:'t6c_1',title:'Aprovação da Estratégia de Lançamento',owner:'Mkt Produtos',ownerColor:'#a07eff',lt:'m',ltLabel:'5–10 dias',raci:{R:'Mkt Produtos',A:'Diretoria',C:'Comex/BD',I:'—'},desc:'Em paralelo com arte de embalagem. Estratégia final aprovada formalmente.',inputs:['Estratégia elaborada Fase 4','Confirmações pós-deferimento'],outputs:['Estratégia de lançamento aprovada']},
    {id:'t6c_2',title:'Entrega do Racional Estratégico',owner:'Mkt Produtos → Gerente do Produto',ownerColor:'#a07eff',lt:'f',ltLabel:'2–3 dias',raci:{R:'Mkt Produtos',A:'Mkt Produtos',C:'—',I:'Gerente do Produto'},desc:'Documento completo: posicionamento, pricing, estratégia de comunicação, metas. Handoff formal.',inputs:['Estratégia aprovada','Dados finais do produto'],outputs:['Racional estratégico completo','Handoff formal ao gerente']},
  ],
  fase6d:[
    {id:'t6d_1',title:'Planejamento do Forecast de Compra',owner:'Comex / BD + CEO',ownerColor:'#7ea8ff',lt:'m',ltLabel:'7–14 dias',raci:{R:'Comex/BD',A:'CEO',C:'Financeiro',I:'—'},desc:'Em paralelo com arte — não aguarda a arte finalizar. CEO é aprovador. Define volumes, lead time, Incoterm e emite 1ª PO.',inputs:['Deferimento ANVISA','Estimativa de demanda'],outputs:['PO inicial emitida','Forecast 6 meses','Data estimada de chegada do estoque']},
  ],
  encerramento:[
    {id:'tenc_1',title:'Checklist de Encerramento',owner:'PM · Todas as Áreas',ownerColor:'#22c97a',lt:'f',ltLabel:'1–2 dias',raci:{R:'PM',A:'PM',C:'Todas as áreas',I:'—'},desc:'PM valida: Cadastro ativo ✓ Arte homologada ✓ PO emitida ✓ Estratégia aprovada ✓ Marca protegida ✓',inputs:['Todos os entregáveis das fases anteriores'],outputs:['Produto liberado para processo de lançamento']},
  ]
};

const STATUS_OPTS = ['Pendente','Em andamento','Concluído','Bloqueado'];
const STATUS_COLORS = {'Pendente':'#555a74','Em andamento':'#f5a623','Concluído':'#22c97a','Bloqueado':'#e05c5c'};

let projects = [];
let activeProject = null;
let activeView = 'kanban';

async function save(){
  try{ await window.storage.set('rennova_projects', JSON.stringify(projects)); }catch(e){}
}
async function load(){
  try{
    const r = await window.storage.get('rennova_projects');
    if(r && r.value){ projects = JSON.parse(r.value); }
  }catch(e){}
}

function buildProjectTasks(){
  const tasks = {};
  Object.keys(TASK_TEMPLATES).forEach(phase => {
    tasks[phase] = TASK_TEMPLATES[phase].map(t => ({
      ...t,
      status: 'Pendente',
      startDate: '',
      endDate: '',
      notes: '',
      responsible: ''
    }));
  });
  return tasks;
}

function createProject(){
  const name = document.getElementById('np-name').value.trim();
  if(!name){ alert('Informe o nome do produto.'); return; }
  const proj = {
    id: 'p_' + Date.now(),
    name,
    area: document.getElementById('np-area').value,
    pm: document.getElementById('np-pm').value,
    category: document.getElementById('np-cat').value,
    startDate: document.getElementById('np-start').value,
    supplier: document.getElementById('np-supplier').value,
    notes: document.getElementById('np-notes').value,
    phase: 'fase1',
    createdAt: new Date().toISOString(),
    tasks: buildProjectTasks()
  };
  projects.push(proj);
  save();
  closeModal();
  renderAll();
  selectProject(proj.id);
}

function selectProject(id){
  activeProject = projects.find(p => p.id === id);
  renderSidebar();
  if(activeView === 'kanban') renderKanban();
  closeDetail();
}

function deleteProject(id, e){
  e && e.stopPropagation();
  if(!confirm('Remover este projeto?')) return;
  projects = projects.filter(p => p.id !== id);
  if(activeProject && activeProject.id === id){
    activeProject = projects[0] || null;
  }
  save();
  renderAll();
}

function switchView(v){
  activeView = v;
  document.getElementById('kanban-view').style.display = v === 'kanban' ? 'block' : 'none';
  document.getElementById('portfolio-view').style.display = v === 'portfolio' ? 'flex' : 'none';
  document.getElementById('empty-view').style.display = 'none';
  if(v === 'kanban' && activeProject) renderKanban();
  if(v === 'portfolio') renderPortfolio();
}

function getPhaseProgress(proj){
  let total = 0, done = 0;
  Object.values(proj.tasks).forEach(arr => arr.forEach(t => {
    total++;
    if(t.status === 'Concluído') done++;
  }));
  return total ? Math.round(done/total*100) : 0;
}

function getPhaseColor(phaseId){
  const p = PHASES.find(x => x.id === phaseId);
  return p ? p.color : '#555a74';
}

function getCurrentPhaseLabel(proj){
  const ph = PHASES.find(p => p.id === proj.phase);
  return ph ? ph.label + ' — ' + ph.title : '—';
}

function renderAll(){
  renderSidebar();
  renderTabs();
  const hasProjets = projects.length > 0;
  document.getElementById('empty-view').style.display = hasProjets ? 'none' : 'flex';
  if(!hasProjets){
    document.getElementById('kanban-view').style.display = 'none';
    document.getElementById('portfolio-view').style.display = 'none';
    return;
  }
  if(activeView === 'kanban'){
    document.getElementById('kanban-view').style.display = 'block';
    if(activeProject) renderKanban();
  } else {
    document.getElementById('portfolio-view').style.display = 'flex';
    renderPortfolio();
  }
}

function renderTabs(){
  const el = document.getElementById('tabs');
  if(!projects.length){ el.innerHTML=''; return; }
  el.innerHTML = projects.map(p => {
    const pct = getPhaseProgress(p);
    const active = activeProject && activeProject.id === p.id;
    return `<div class="tab ${active?'active':''}" onclick="selectProject('${p.id}')">
      <span>${p.name}</span>
      <span class="tab-count">${pct}%</span>
    </div>`;
  }).join('');
}

function renderSidebar(){
  document.getElementById('proj-count').textContent = projects.length;
  const el = document.getElementById('project-list');
  if(!projects.length){
    el.innerHTML = '<div style="padding:16px;text-align:center;font-size:11px;color:var(--text3)">Nenhum projeto</div>';
    return;
  }
  el.innerHTML = projects.map(p => {
    const pct = getPhaseProgress(p);
    const active = activeProject && activeProject.id === p.id;
    const ph = PHASES.find(x => x.id === p.phase);
    return `<div class="project-item ${active?'active':''}" onclick="selectProject('${p.id}')">
      <div class="pi-header">
        <div class="pi-name">${p.name}</div>
        <div class="pi-phase" style="background:${ph?ph.color+'18':'#2e324888'};color:${ph?ph.color:'#555a74'}">${ph?ph.label:'—'}</div>
      </div>
      <div class="pi-meta">
        <span>${p.category}</span>
        <span>·</span>
        <span>${p.area}</span>
      </div>
      <div class="pi-progress"><div class="pi-progress-bar" style="width:${pct}%"></div></div>
    </div>`;
  }).join('');
}

function renderKanban(){
  const board = document.getElementById('kanban-board');
  if(!activeProject){ board.innerHTML=''; return; }
  const proj = activeProject;

  board.innerHTML = PHASES.map(phase => {
    const tasks = proj.tasks[phase.id] || [];
    const doneCount = tasks.filter(t => t.status === 'Concluído').length;

    const cardsHtml = tasks.map(t => {
      const sc = STATUS_COLORS[t.status] || '#555a74';
      const isDone = t.status === 'Concluído';
      const isBlocked = t.status === 'Bloqueado';
      let pills = `<span class="pill lt-${t.lt}">${t.ltLabel}</span>`;
      if(t.dep) pills += `<span class="pill pill-dep">Dep: ${t.dep.split(' ')[0]}...</span>`;
      if(isBlocked) pills += `<span class="pill pill-blocked">Bloqueado</span>`;

      if(t.isGate){
        return `<div class="gate-card ${isDone?'done':''}" onclick="openDetail('${t.id}')">
          <div class="gate-label"><i class="ti ti-diamond" style="font-size:9px"></i> ${phase.isGate?'Gate ANVISA':'Gate de Decisão'}</div>
          <div class="gate-title">${t.title}</div>
          <div class="gate-status" style="color:${sc}">${t.status}</div>
        </div>`;
      }

      return `<div class="card ${isDone?'done':''} ${isBlocked?'blocked':''}" onclick="openDetail('${t.id}')">
        <div class="card-phase-bar" style="background:${phase.color}"></div>
        <div class="card-owner-row">
          <div class="card-owner" style="color:${t.ownerColor}">${t.owner.split(' ')[0]}</div>
          <div class="card-status" style="background:${sc}" title="${t.status}"></div>
        </div>
        <div class="card-title">${t.title}</div>
        <div class="card-meta">${pills}</div>
        ${t.responsible ? `<div class="card-date"><i class="ti ti-user" style="font-size:9px"></i> ${t.responsible}</div>` : ''}
        ${t.endDate ? `<div class="card-date"><i class="ti ti-calendar" style="font-size:9px"></i> Prazo: ${formatDate(t.endDate)}</div>` : ''}
        ${t.notes ? `<div class="card-date" style="color:var(--text3);font-style:italic;font-size:9px">${t.notes.substring(0,40)}${t.notes.length>40?'…':''}</div>` : ''}
      </div>`;
    }).join('');

    return `<div class="col-wrap">
      <div class="col-header">
        <div class="col-title">
          <span style="width:7px;height:7px;border-radius:50%;background:${phase.color};display:inline-block;flex-shrink:0"></span>
          ${phase.label} · ${phase.title}
        </div>
        <span class="col-count">${doneCount}/${tasks.length}</span>
      </div>
      <div class="col-cards">${cardsHtml || '<div style="font-size:10px;color:var(--text3);text-align:center;padding:8px">—</div>'}</div>
    </div>`;
  }).join('');
}

function renderPortfolio(){
  const el = document.getElementById('portfolio-grid');
  if(!projects.length){ el.innerHTML='<div class="empty"><p>Nenhum projeto</p></div>'; return; }
  const lanes = [
    {key:'fase4',label:'Reg/Docs',color:'#44cc88'},
    {key:'gate2',label:'ANVISA',color:'#f5a623'},
    {key:'fase6b',label:'Arte',color:'#cc77ff'},
    {key:'fase6a',label:'Cadastro',color:'#55aacc'},
  ];
  el.innerHTML = projects.map(p => {
    const pct = getPhaseProgress(p);
    const ph = PHASES.find(x => x.id === p.phase);
    const lanesHtml = lanes.map(l => {
      const tasks = p.tasks[l.key] || [];
      const hasBlocked = tasks.some(t => t.status === 'Bloqueado');
      const allDone = tasks.length && tasks.every(t => t.status === 'Concluído');
      const anyInProgress = tasks.some(t => t.status === 'Em andamento');
      const sc = hasBlocked ? '#e05c5c' : allDone ? '#22c97a' : anyInProgress ? '#f5a623' : '#555a74';
      const sl = hasBlocked ? 'Bloqueado' : allDone ? 'Concluído' : anyInProgress ? 'Em andamento' : 'Pendente';
      return `<div class="pf-lane">
        <div class="pf-lane-name" style="color:${l.color}">${l.label}</div>
        <div class="pf-lane-status"><div class="status-dot" style="background:${sc}"></div>${sl}</div>
      </div>`;
    }).join('');
    return `<div class="pf-card" onclick="selectProject('${p.id}');switchView('kanban')">
      <div class="pf-top">
        <div>
          <div class="pf-name">${p.name}</div>
          <div class="pf-meta" style="margin-top:4px">
            <span class="pf-phase-badge" style="background:${ph?ph.color+'18':'#2e3248'};color:${ph?ph.color:'#555a74'}">${ph?ph.label+' — '+ph.title:'—'}</span>
            <span style="font-size:10px;color:var(--text3)">${p.category}</span>
            <span style="font-size:10px;color:var(--text3)">${p.area}</span>
            ${p.pm?`<span style="font-size:10px;color:var(--text3)">PM: ${p.pm}</span>`:''}
          </div>
        </div>
        <button class="btn danger" style="font-size:10px;padding:3px 8px" onclick="deleteProject('${p.id}',event)"><i class="ti ti-trash"></i></button>
      </div>
      <div class="pf-lanes">${lanesHtml}</div>
      <div class="pf-progress-row">
        <div class="pf-progress-bg"><div class="pf-progress-fill" style="width:${pct}%"></div></div>
        <div class="pf-pct">${pct}%</div>
      </div>
    </div>`;
  }).join('');
}

function findTask(taskId){
  if(!activeProject) return null;
  for(const phase of Object.values(activeProject.tasks)){
    const t = phase.find(x => x.id === taskId);
    if(t) return t;
  }
  return null;
}

function openDetail(taskId){
  const t = findTask(taskId);
  if(!t) return;
  const det = document.getElementById('detail');
  const ct = document.getElementById('det-content');
  const ph = PHASES.find(p => (activeProject.tasks[p.id]||[]).find(x=>x.id===taskId));

  const statusOpts = STATUS_OPTS.map(s => `<option value="${s}" ${t.status===s?'selected':''}>${s}</option>`).join('');
  const raciHtml = t.raci ? Object.entries(t.raci).map(([role,val])=>
    `<div class="raci-tag" style="border-color:${role==='R'?'#e05c5c44':role==='A'?'#f5a62344':role==='C'?'#4f7fff44':'#2e3248'};color:${role==='R'?'#e05c5c':role==='A'?'#f5a623':role==='C'?'#4f7fff':'#555a74'};background:${role==='R'?'rgba(224,92,92,.08)':role==='A'?'rgba(245,166,35,.08)':role==='C'?'rgba(79,127,255,.08)':'transparent'}"><b>${role}</b>: ${val}</div>`
  ).join('') : '';

  ct.innerHTML = `
    <div class="det-header">
      <div>
        <div style="font-size:9px;font-weight:700;letter-spacing:1.2px;text-transform:uppercase;color:${t.ownerColor};margin-bottom:6px">${t.owner}</div>
        <div style="font-family:'Space Grotesk',sans-serif;font-size:15px;font-weight:600;color:var(--white);line-height:1.3">${t.title}</div>
        ${ph ? `<div style="font-size:10px;color:var(--text3);margin-top:4px">${ph.label} · ${ph.title}</div>` : ''}
      </div>
      <div class="det-close" onclick="closeDetail()"><i class="ti ti-x"></i></div>
    </div>
    <div class="det-body">
      <div class="det-section">
        <div class="det-label">Descrição</div>
        <div class="det-val" style="font-size:12px">${t.desc}</div>
      </div>
      ${t.dep?`<div style="background:rgba(79,127,255,.08);border:1px solid rgba(79,127,255,.2);border-radius:7px;padding:7px 10px;font-size:11px;color:#7ea8ff"><i class="ti ti-link" style="font-size:11px"></i> <b>Dependência:</b> ${t.dep}</div>`:''}
      <div class="det-section">
        <div class="det-label">Status</div>
        <select class="det-select" onchange="updateTask('${t.id}','status',this.value)">${statusOpts}</select>
      </div>
      <div class="det-section">
        <div class="det-label">Responsável</div>
        <input class="det-input" placeholder="Nome do responsável" value="${t.responsible||''}" onchange="updateTask('${t.id}','responsible',this.value)">
      </div>
      <div class="det-row">
        <div class="det-section">
          <div class="det-label">Data início</div>
          <input class="det-input" type="date" value="${t.startDate||''}" onchange="updateTask('${t.id}','startDate',this.value)">
        </div>
        <div class="det-section">
          <div class="det-label">Prazo / Data fim</div>
          <input class="det-input" type="date" value="${t.endDate||''}" onchange="updateTask('${t.id}','endDate',this.value)">
        </div>
      </div>
      <div class="det-section">
        <div class="det-label">Lead time previsto</div>
        <div><span class="pill lt-${t.lt}" style="font-size:10px">${t.ltLabel}</span></div>
      </div>
      <div class="det-section">
        <div class="det-label">Matriz RACI</div>
        <div class="raci-mini">${raciHtml}</div>
      </div>
      <div class="det-section">
        <div class="det-label">Inputs necessários</div>
        <div style="background:var(--s2);border-radius:7px;padding:9px">
          ${t.inputs.map(i=>`<div style="font-size:11px;color:var(--text2);padding:2px 0;padding-left:12px;position:relative"><span style="position:absolute;left:0;color:var(--accent);font-size:10px">→</span>${i}</div>`).join('')}
        </div>
      </div>
      <div class="det-section">
        <div class="det-label">Outputs / Entregáveis</div>
        <div style="background:var(--s2);border-radius:7px;padding:9px">
          ${t.outputs.map(o=>`<div style="font-size:11px;color:var(--text2);padding:2px 0;padding-left:12px;position:relative"><span style="position:absolute;left:0;color:var(--green);font-size:10px">✓</span>${o}</div>`).join('')}
        </div>
      </div>
      <div class="det-section">
        <div class="det-label">Anotações</div>
        <textarea class="det-textarea" placeholder="Observações, bloqueios, contexto..." onchange="updateTask('${t.id}','notes',this.value)">${t.notes||''}</textarea>
      </div>
      <div style="display:flex;gap:8px;padding-top:4px">
        <button class="btn" style="flex:1;justify-content:center" onclick="setStatus('${t.id}','Concluído')"><i class="ti ti-check"></i> Marcar Concluído</button>
        <button class="btn" style="flex:1;justify-content:center" onclick="setStatus('${t.id}','Bloqueado')"><i class="ti ti-alert-triangle"></i> Bloqueado</button>
      </div>
      <button class="btn" style="width:100%;justify-content:center" onclick="advancePhase()"><i class="ti ti-arrow-right"></i> Avançar Fase do Projeto</button>
    </div>
  `;
  det.classList.add('open');
}

function closeDetail(){
  document.getElementById('detail').classList.remove('open');
}

function updateTask(taskId, field, value){
  if(!activeProject) return;
  for(const phase of Object.values(activeProject.tasks)){
    const t = phase.find(x => x.id === taskId);
    if(t){ t[field] = value; break; }
  }
  save();
  renderKanban();
  renderSidebar();
  renderTabs();
}

function setStatus(taskId, status){
  updateTask(taskId, 'status', status);
  openDetail(taskId);
}

function advancePhase(){
  if(!activeProject) return;
  const idx = PHASES.findIndex(p => p.id === activeProject.phase);
  if(idx < PHASES.length - 1){
    activeProject.phase = PHASES[idx+1].id;
    save();
    renderAll();
    closeDetail();
  } else {
    alert('Projeto já está na fase final.');
  }
}

function formatDate(d){
  if(!d) return '';
  const [y,m,dd] = d.split('-');
  return `${dd}/${m}/${y}`;
}

function openNewProject(){
  document.getElementById('np-name').value='';
  document.getElementById('np-pm').value='';
  document.getElementById('np-supplier').value='';
  document.getElementById('np-notes').value='';
  document.getElementById('np-start').value=new Date().toISOString().split('T')[0];
  document.getElementById('modal-bg').classList.add('open');
}
function closeModal(){
  document.getElementById('modal-bg').classList.remove('open');
}
document.getElementById('modal-bg').addEventListener('click', e => {
  if(e.target === document.getElementById('modal-bg')) closeModal();
});
document.addEventListener('keydown', e => {
  if(e.key === 'Escape'){ closeModal(); closeDetail(); }
});

(async()=>{
  await load();
  if(projects.length){ activeProject = projects[0]; activeView = 'kanban'; }
  renderAll();
})();
</script>

</div>

<script>
function goTo(pageId){
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById(pageId).classList.add('active');
  if(pageId === 'kanban-page') initKanban();
}
function goHome(){
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById('home').classList.add('active');
}

// Inject back buttons into sub-page headers
function injectBackButtons(){
  // Flow header
  const fh = document.querySelector('#flow-page header');
  if(fh){
    const bb = document.createElement('button');
    bb.className = 'back-btn';
    bb.innerHTML = '<i class="ti ti-arrow-left" style="font-size:13px"></i> Início';
    bb.onclick = goHome;
    fh.insertBefore(bb, fh.firstChild);
    fh.style.gap = '12px';
  }
  // Kanban header
  const kh = document.querySelector('#kanban-page header');
  if(kh){
    const bb = document.createElement('button');
    bb.className = 'back-btn';
    bb.innerHTML = '<i class="ti ti-arrow-left" style="font-size:13px"></i> Início';
    bb.onclick = goHome;
    kh.insertBefore(bb, kh.firstChild);
    kh.style.gap = '12px';
  }
}

let kanbanInited = false;
function initKanban(){
  if(kanbanInited) return;
  kanbanInited = true;
  // trigger async init
  if(typeof window._kanbanInit === 'function') window._kanbanInit();
}

injectBackButtons();

// Keyboard nav
document.addEventListener('keydown', e => {
  if(e.key === 'Escape'){
    const active = document.querySelector('.page.active');
    if(active && active.id !== 'home') goHome();
  }
});
</script>

</body>
</html>
