<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Rennova — Fluxo de Lançamento de Produtos v3</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Space+Grotesk:wght@400;500;700&display=swap');
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#0f1117;--surface:#1a1d27;--surface2:#222535;--border:#2e3248;
  --accent:#4f7fff;--green:#22c97a;--orange:#f5a623;--red:#e05c5c;
  --text:#e8eaf0;--text2:#8b90a8;--text3:#555a74;--white:#fff;
}
body{background:var(--bg);color:var(--text);font-family:'Inter',sans-serif;min-height:100vh}

/* HEADER */
header{background:var(--surface);border-bottom:1px solid var(--border);padding:14px 28px;display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;z-index:100}
.logo{font-family:'Space Grotesk',sans-serif;font-size:17px;font-weight:700;color:var(--white)}
.logo span{color:var(--accent)}
.hbadge{background:#1e2640;border:1px solid var(--border);border-radius:20px;padding:3px 11px;font-size:10px;color:var(--text2);font-weight:500}
.hbadge.v{border-color:#22c97a44;color:var(--green)}
.header-meta{display:flex;gap:10px;align-items:center}

/* CANVAS */
.canvas-wrapper{overflow-x:auto;padding:28px 14px 80px}
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
</style>
</head>
<body>

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
</body>
</html>
