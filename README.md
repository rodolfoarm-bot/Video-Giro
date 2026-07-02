# Video-Giro
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Giro — Demo para gravação (9:16)</title>
<style>
/* ===== TOKENS REAIS DO APP GIRO ===== */
:root{
  --accent:#7C3AED;--accent2:#6D28D9;--accent-l:#EDE9FE;--accent-ll:#F5F3FF;
  --success:#059669;--success-l:#D1FAE5;--danger:#DC2626;--danger-l:#FEE2E2;
  --warning:#D97706;--warning-l:#FEF3C7;--info:#2563EB;--info-l:#DBEAFE;
  --bg:#F8F7FF;--surface:#FFFFFF;--surface2:#F1F0F9;--border:#E5E3F0;--border2:#D1CEE8;
  --text1:#1E1B4B;--text2:#6B6894;--text3:#A8A5C5;
  --shadow:0 1px 3px rgba(124,58,237,.08),0 1px 2px rgba(124,58,237,.06);
  --shadow-md:0 4px 6px rgba(124,58,237,.07),0 2px 4px rgba(124,58,237,.06);
  --topbar-bg:linear-gradient(135deg,#7C3AED 0%,#5B21B6 100%);
  --card-radius:16px;--radius:10px;
  --wa-bg:#E5DDD5;--wa-verde:#DCF8C6;--wa-top:#075E54;
}
*{margin:0;padding:0;box-sizing:border-box}
html,body{height:100%;background:#0E0B1F;font-family:-apple-system,BlinkMacSystemFont,'Inter','Segoe UI',sans-serif;overflow:hidden}
#wrap{position:fixed;inset:0;display:flex;align-items:center;justify-content:center}
#stage{position:relative;width:405px;height:720px;background:var(--bg);overflow:hidden;border-radius:14px;box-shadow:0 30px 80px rgba(0,0,0,.5)}
.scene{position:absolute;inset:0;opacity:0;pointer-events:none;transition:opacity .5s ease}
.scene.on{opacity:1;pointer-events:auto}
/* legenda */
#cap{position:absolute;left:14px;right:14px;bottom:14px;z-index:60;display:flex;justify-content:center;pointer-events:none}
#cap span{background:rgba(14,11,31,.9);color:#fff;font-weight:700;font-size:15px;line-height:1.4;padding:9px 15px;border-radius:13px;text-align:center;opacity:0;transform:translateY(8px);transition:all .35s ease;max-width:100%}
#cap span.on{opacity:1;transform:none}
#prog{position:absolute;top:0;left:0;height:4px;background:linear-gradient(90deg,#7C3AED,#F9A8D4);width:0%;z-index:70}
/* play overlay */
#play-ov{position:absolute;inset:0;z-index:100;background:var(--topbar-bg);display:flex;flex-direction:column;align-items:center;justify-content:center;gap:16px;cursor:pointer}
#play-ov .g{width:104px;height:104px;border-radius:28px;background:#fff;display:flex;align-items:center;justify-content:center;font-size:62px;font-weight:800;color:var(--accent);box-shadow:0 16px 40px rgba(0,0,0,.3)}
#play-ov h1{color:#fff;font-size:36px;font-weight:800;letter-spacing:-.5px}
#play-ov p{color:rgba(255,255,255,.85);font-size:13.5px;text-align:center;max-width:270px;line-height:1.5}
#play-ov .btn{margin-top:6px;background:#fff;color:var(--accent);font-weight:800;font-size:17px;padding:13px 38px;border-radius:999px;box-shadow:0 10px 26px rgba(0,0,0,.25)}
#ctrl{position:absolute;top:10px;right:10px;z-index:80;display:none}
#ctrl button{background:rgba(14,11,31,.55);color:#fff;border:none;border-radius:8px;font-size:11px;font-weight:800;padding:6px 10px;cursor:pointer}

/* ===== moldura de celular ===== */
.phone{position:absolute;top:34px;left:50%;transform:translateX(-50%);width:320px;height:626px;background:var(--bg);border-radius:36px;border:8px solid #1E1B4B;overflow:hidden;box-shadow:0 26px 60px rgba(30,27,75,.3);display:flex;flex-direction:column}
.phone .notch{position:absolute;top:0;left:50%;transform:translateX(-50%);width:108px;height:19px;background:#1E1B4B;border-radius:0 0 12px 12px;z-index:9}

/* ===== COMPONENTES REAIS DO APP ===== */
.tb{background:var(--topbar-bg);padding:26px 14px 12px;flex-shrink:0}
.tb-row{display:flex;align-items:center;justify-content:space-between;margin-bottom:10px}
.tb-title{font-size:19px;font-weight:700;color:#fff;letter-spacing:-.4px}
.tb-count{font-size:12px;color:rgba(255,255,255,.85);font-weight:600;margin-left:8px}
.tb-user{font-size:10px;color:rgba(255,255,255,.7)}
.srch{position:relative}
.srch input{width:100%;background:rgba(255,255,255,.15);border:1px solid rgba(255,255,255,.2);border-radius:12px;padding:9px 12px 9px 34px;color:#fff;font-size:12.5px;outline:none}
.srch input::placeholder{color:rgba(255,255,255,.6)}
.srch svg{position:absolute;left:10px;top:50%;transform:translateY(-50%);width:15px;height:15px;opacity:.7}
.estq-tabs{display:flex;gap:6px;margin-top:9px;background:rgba(0,0,0,.18);padding:3px;border-radius:10px}
.estq-tab{flex:1;padding:7px;border-radius:8px;border:none;background:transparent;color:rgba(255,255,255,.65);font-size:11.5px;font-weight:700;letter-spacing:-.1px;text-align:center}
.estq-tab.on{background:#fff;color:var(--accent)}
.appbody{padding:12px;background:var(--bg);flex:1;overflow:hidden;position:relative}
.bnav{background:var(--surface);border-top:1px solid var(--border);display:flex;padding:7px 12px 10px;flex-shrink:0;gap:4px}
.bnav-item{flex:1;display:flex;flex-direction:column;align-items:center;gap:3px;padding:3px 0;background:none;border:none}
.bnav-ic{width:20px;height:20px;stroke:var(--text3);fill:none;stroke-width:1.8}
.bnav-lb{font-size:9px;color:var(--text3);font-weight:500}
.bnav-item.on .bnav-ic{stroke:var(--accent)}
.bnav-item.on .bnav-lb{color:var(--accent);font-weight:700}
.fbtn{width:100%;padding:12px;background:var(--accent);color:#fff;border:none;border-radius:var(--radius);font-size:13.5px;font-weight:700;letter-spacing:-.2px;box-shadow:0 4px 12px rgba(124,58,237,.3);text-align:center}
.fbtn-success{background:var(--success);box-shadow:0 4px 12px rgba(5,150,105,.3)}
.fbtn-outline{background:var(--surface);color:var(--accent);border:1.5px solid var(--accent);box-shadow:none}
/* pcard real */
.grid2{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.pcard{background:var(--surface);border-radius:var(--card-radius);border:1px solid var(--border);overflow:hidden;box-shadow:var(--shadow)}
.pcard-img{width:100%;aspect-ratio:3/4;display:flex;align-items:center;justify-content:center;position:relative;overflow:hidden;background:var(--surface2)}
.stk-badge{position:absolute;top:7px;right:7px;border-radius:8px;font-size:9px;font-weight:700;padding:2px 7px}
.sok{background:var(--success-l);color:var(--success)}.slow{background:var(--warning-l);color:var(--warning)}
.pcard-body{padding:8px 10px 10px}
.pcard-nome{font-size:11.5px;font-weight:700;color:var(--text1);margin-bottom:2px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.pcard-sub{font-size:9.5px;color:var(--text2);margin-bottom:6px;display:flex;align-items:center;gap:4px}
.cdot{display:inline-block;width:6px;height:6px;border-radius:50%}
.tam-chips{display:flex;gap:3px;margin-bottom:6px;flex-wrap:wrap}
.tam-chip{font-size:8.5px;font-weight:600;padding:1.5px 6px;border-radius:6px;border:1px solid var(--border);color:var(--text2);background:var(--surface2)}
.pcard-preco{font-size:12.5px;font-weight:700;color:var(--accent)}
.pfoto{width:100%;height:100%;display:flex;align-items:center;justify-content:center}

/* ===== CENA 1: abertura ===== */
#s1{background:var(--topbar-bg);display:flex;flex-direction:column;align-items:center;justify-content:center;gap:14px}
#s1 .logo{width:118px;height:118px;border-radius:32px;background:#fff;display:flex;align-items:center;justify-content:center;font-size:72px;font-weight:800;color:var(--accent);box-shadow:0 20px 50px rgba(0,0,0,.3);transform:scale(.6);opacity:0;transition:all .7s cubic-bezier(.2,1.4,.4,1)}
#s1.on .logo{transform:scale(1);opacity:1}
#s1 .nome{font-size:50px;font-weight:800;color:#fff;letter-spacing:-1px;opacity:0;transform:translateY(14px);transition:all .6s ease .35s}
#s1.on .nome{opacity:1;transform:none}
#s1 .tag{color:rgba(255,255,255,.9);font-size:16px;font-weight:600;opacity:0;transition:opacity .6s ease .7s}
#s1.on .tag{opacity:1}
#s1 .fig{position:absolute;font-size:32px;opacity:0;transition:all 1s ease}
#s1.on .fig{opacity:.9}
#s1 .f1{top:16%;left:14%;transition-delay:.9s}#s1 .f2{top:22%;right:14%;transition-delay:1.1s}
#s1 .f3{bottom:20%;left:18%;transition-delay:1.3s}#s1 .f4{bottom:16%;right:16%;transition-delay:1.5s}
/* ===== CENA 2: problema ===== */
#s2{background:var(--bg);display:flex;flex-direction:column;align-items:center;justify-content:center;padding:32px;gap:20px}
#s2 h2{font-size:28px;line-height:1.24;color:var(--text1);text-align:center;font-weight:800;letter-spacing:-.5px}
#s2 h2 em{font-style:normal;color:var(--accent)}
#s2 .dor{background:var(--surface);border:1px solid var(--border);border-radius:14px;padding:13px 15px;display:flex;gap:11px;align-items:center;font-size:14px;font-weight:700;color:var(--text1);opacity:0;transform:translateX(-16px);transition:all .5s ease;box-shadow:var(--shadow);width:100%}
#s2.on .dor{opacity:1;transform:none}
#s2.on .d1{transition-delay:.7s}#s2.on .d2{transition-delay:1.5s}#s2.on .d3{transition-delay:2.3s}
#s2 .dores{display:flex;flex-direction:column;gap:11px;width:100%}
/* ===== CENA 3: cadastrar ===== */
#s3 .fcard{background:var(--surface);border-radius:var(--card-radius);border:1px solid var(--border);padding:14px;box-shadow:var(--shadow)}
#s3 .flabel{font-size:10px;font-weight:700;color:var(--text2);text-transform:uppercase;letter-spacing:.4px;margin-bottom:6px}
#s3 .fotobox{height:186px;border-radius:12px;border:2px dashed var(--border2);display:flex;align-items:center;justify-content:center;position:relative;overflow:hidden;background:var(--accent-ll)}
#s3 .fotobox .hint{color:var(--text2);font-weight:700;font-size:13px;text-align:center;transition:opacity .4s}
#s3 .prod-foto{position:absolute;inset:0;opacity:0;transform:scale(1.12);transition:all .6s ease}
#s3.foto .prod-foto{opacity:1;transform:scale(1)}
#s3.foto .fotobox .hint{opacity:0}
#s3 .campos{margin-top:11px;display:flex;gap:8px}
#s3 .campo{flex:1;background:var(--surface2);border:1px solid var(--border);border-radius:var(--radius);padding:8px 10px;font-size:11px;color:var(--text1);font-weight:600}
#s3 .campo small{display:block;font-size:8.5px;color:var(--text3);font-weight:700;text-transform:uppercase}
#s3 .ia{margin-top:11px;background:var(--accent-l);border-radius:var(--radius);padding:9px 12px;display:flex;align-items:center;gap:8px;font-size:12px;font-weight:800;color:var(--accent);opacity:0;transition:opacity .4s}
#s3.ia .ia{opacity:1}
#s3 .dot{width:7px;height:7px;border-radius:50%;background:var(--accent);animation:pulse 1s infinite}
@keyframes pulse{0%,100%{opacity:.3}50%{opacity:1}}
#s3 .tags{margin-top:11px;display:flex;flex-wrap:wrap;gap:6px}
#s3 .tg{background:var(--surface2);border:1px solid var(--border);color:var(--text1);border-radius:999px;padding:4px 11px;font-size:10.5px;font-weight:700;opacity:0;transform:scale(.7);transition:all .4s cubic-bezier(.2,1.4,.4,1)}
#s3.tags .tg{opacity:1;transform:scale(1)}
#s3.tags .t1{transition-delay:.05s}#s3.tags .t2{transition-delay:.2s}#s3.tags .t3{transition-delay:.35s}#s3.tags .t4{transition-delay:.5s}#s3.tags .t5{transition-delay:.65s}
#s3 .ok{margin-top:11px;background:var(--success-l);color:var(--success);border-radius:var(--radius);padding:10px;text-align:center;font-weight:800;font-size:12.5px;opacity:0;transform:translateY(8px);transition:all .45s ease}
#s3.ok .ok{opacity:1;transform:none}
/* ===== CENA 4: estoque ===== */
#s4 .kpis{display:flex;gap:8px;margin-bottom:10px}
#s4 .kpi{flex:1;background:var(--surface);border:1px solid var(--border);border-radius:12px;padding:9px 10px;box-shadow:var(--shadow)}
#s4 .kpi .v{font-weight:800;font-size:16px;color:var(--text1);letter-spacing:-.3px}
#s4 .kpi .l{font-size:8.5px;font-weight:700;color:var(--text3);text-transform:uppercase;letter-spacing:.3px}
#s4 .pcard{opacity:0;transform:translateY(12px);transition:all .5s ease}
#s4.grid .pcard{opacity:1;transform:none}
#s4.grid .p2{transition-delay:.12s}#s4.grid .p3{transition-delay:.24s}#s4.grid .p4{transition-delay:.36s}
#s4 .alerta{position:absolute;left:12px;right:12px;bottom:8px;background:var(--danger-l);border:1px solid #FECACA;border-radius:12px;padding:10px 13px;display:flex;gap:10px;align-items:center;opacity:0;transform:translateY(14px);transition:all .5s ease;z-index:4;box-shadow:var(--shadow-md)}
#s4.alerta .alerta{opacity:1;transform:none}
#s4 .alerta .tx{font-size:11.5px;font-weight:800;color:#B91C1C;line-height:1.35}
#s4 .alerta .tx small{display:block;font-size:10px;font-weight:700;color:var(--danger)}
/* ===== CENA 5: WhatsApp ===== */
#s5{background:#111}
#s5 .phone{border-color:#111;background:var(--wa-bg)}
#s5 .wa-top{background:var(--wa-top);color:#fff;padding:26px 12px 9px;display:flex;align-items:center;gap:9px;flex-shrink:0}
#s5 .wa-av{width:30px;height:30px;border-radius:50%;background:linear-gradient(120deg,#7C3AED,#F9A8D4);display:flex;align-items:center;justify-content:center;font-size:14px}
#s5 .wa-nm{font-weight:800;font-size:13.5px}
#s5 .wa-nm small{display:block;font-weight:600;font-size:9px;opacity:.8}
#s5 .wa-body{flex:1;padding:10px 8px;display:flex;flex-direction:column;gap:6px;overflow-y:auto;scroll-behavior:smooth}
#s5 .wa-body::-webkit-scrollbar{display:none}
.bl{max-width:83%;border-radius:9px;padding:6px 9px;font-size:12px;line-height:1.4;color:#111;box-shadow:0 1px 1px rgba(0,0,0,.12);display:none;font-weight:600;flex-shrink:0}
.bl.show{display:block;animation:blin .35s ease}
@keyframes blin{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:none}}
.bl.in{background:#fff;align-self:flex-start;border-top-left-radius:2px}
.bl.out{background:var(--wa-verde);align-self:flex-end;border-top-right-radius:2px}
.bl .hr{font-size:8px;color:#7B8794;text-align:right;margin-top:2px;font-weight:700}
.bl.prod{padding:4px}
.bl.prod .bimg{width:150px;height:104px;border-radius:7px;overflow:hidden}
.bl.prod .bcap{font-size:10.5px;padding:5px 5px 2px;font-weight:700;line-height:1.4}
.bl.prod .bcap b{color:#5B21B6}
.digitando{align-self:flex-start;background:#fff;border-radius:9px;padding:8px 12px;box-shadow:0 1px 1px rgba(0,0,0,.12);display:none;flex-shrink:0}
.digitando.show{display:block}
.digitando i{display:inline-block;width:5.5px;height:5.5px;border-radius:50%;background:#98A1AB;margin:0 1.5px;animation:dg 1.1s infinite}
.digitando i:nth-child(2){animation-delay:.18s}.digitando i:nth-child(3){animation-delay:.36s}
@keyframes dg{0%,100%{transform:translateY(0)}50%{transform:translateY(-4px)}}
/* ===== CENA 6: pedido no app ===== */
#s6 .ped{background:var(--surface);border-radius:var(--card-radius);border:1px solid var(--border);padding:13px;box-shadow:var(--shadow-md);opacity:0;transform:translateY(14px);transition:all .5s ease}
#s6.ped .ped{opacity:1;transform:none}
#s6 .subtabs{display:flex;gap:6px;margin-bottom:10px}
#s6 .stab{flex:1;text-align:center;padding:8px;border-radius:10px;font-size:11.5px;font-weight:700;background:var(--surface);border:1px solid var(--border);color:var(--text2)}
#s6 .stab.on{background:var(--accent);color:#fff;border-color:var(--accent)}
#s6 .ped-top{display:flex;justify-content:space-between;align-items:center;margin-bottom:8px}
#s6 .pednum{font-weight:800;font-size:15px;color:var(--text1);letter-spacing:-.3px}
#s6 .selo{background:var(--success-l);color:var(--success);font-size:9px;font-weight:800;padding:3px 8px;border-radius:999px}
#s6 .it{display:flex;gap:9px;align-items:center;padding:7px 0;border-bottom:1px solid var(--border)}
#s6 .it .im{width:40px;height:40px;border-radius:8px;overflow:hidden;flex-shrink:0;background:var(--surface2)}
#s6 .it .nm{font-size:11.5px;font-weight:700;color:var(--text1)}
#s6 .it .dt{font-size:10px;font-weight:600;color:var(--text2)}
#s6 .cli{font-size:10.5px;font-weight:700;color:var(--text2);padding:7px 0;border-bottom:1px solid var(--border)}
#s6 .tot{display:flex;justify-content:space-between;font-weight:800;color:var(--text1);font-size:13.5px;padding:8px 0 2px}
#s6 .btnass{margin-top:8px;transition:transform .15s}
#s6.press .btnass{transform:scale(.94)}
#s6 .status{margin-top:8px;background:var(--warning-l);color:var(--warning);border:1px solid #FDE68A;text-align:center;border-radius:var(--radius);padding:9px;font-weight:800;font-size:11.5px;display:none}
#s6.atend .status{display:block;animation:blin .4s ease}
#s6 .btnconc{margin-top:8px;display:none}
#s6.atend .btnconc{display:block;animation:blin .4s ease .15s backwards}
#s6.atend .btnass{display:none}
#s6 .toast{position:absolute;left:50%;transform:translateX(-50%) translateY(16px);bottom:70px;background:var(--text1);color:#fff;font-weight:800;font-size:12px;padding:10px 17px;border-radius:999px;opacity:0;transition:all .45s;z-index:8;white-space:nowrap}
#s6.toast .toast{opacity:1;transform:translateX(-50%) translateY(0)}
/* ===== CENA 7: fechamento ===== */
#s7{background:var(--topbar-bg);display:flex;flex-direction:column;align-items:center;justify-content:center;gap:13px;padding:30px}
#s7 .logo{width:86px;height:86px;border-radius:24px;background:#fff;display:flex;align-items:center;justify-content:center;font-size:52px;font-weight:800;color:var(--accent);opacity:0;transform:scale(.7);transition:all .6s cubic-bezier(.2,1.4,.4,1)}
#s7.on .logo{opacity:1;transform:scale(1)}
#s7 h2{color:#fff;font-size:31px;font-weight:800;text-align:center;line-height:1.15;letter-spacing:-.5px;opacity:0;transform:translateY(12px);transition:all .55s ease .3s}
#s7.on h2{opacity:1;transform:none}
#s7 .li{color:#fff;font-size:14.5px;font-weight:700;display:flex;align-items:center;gap:9px;opacity:0;transform:translateX(-12px);transition:all .5s ease}
#s7.on .li{opacity:1;transform:none}
#s7.on .l1{transition-delay:.7s}#s7.on .l2{transition-delay:1s}#s7.on .l3{transition-delay:1.3s}
#s7 .cta{margin-top:8px;background:#fff;color:var(--accent);font-weight:800;font-size:16px;padding:13px 28px;border-radius:999px;opacity:0;transform:scale(.85);transition:all .5s cubic-bezier(.2,1.4,.4,1) 1.7s;box-shadow:0 12px 30px rgba(0,0,0,.25)}
#s7.on .cta{opacity:1;transform:scale(1)}
</style>
</head>
<body>
<div id="wrap">
  <div id="stage">
    <div id="prog"></div>
    <div id="ctrl"><button onclick="reiniciar()">↺ Reiniciar</button></div>

    <!-- CENA 1 -->
    <div class="scene" id="s1">
      <span class="fig f1">🧸</span><span class="fig f2">👶</span><span class="fig f3">👗</span><span class="fig f4">🧦</span>
      <div class="logo">G</div><div class="nome">Giro</div>
      <div class="tag">A loja infantil que gira sozinha</div>
    </div>

    <!-- CENA 2 -->
    <div class="scene" id="s2">
      <h2>Sua loja vende pelo WhatsApp…<br><em>mas o estoque vive na sua cabeça?</em></h2>
      <div class="dores">
        <div class="dor d1"><span style="font-size:22px">😵</span> Cliente pergunta, você corre pra conferir a prateleira</div>
        <div class="dor d2"><span style="font-size:22px">📵</span> Demora pra responder e a venda esfria</div>
        <div class="dor d3"><span style="font-size:22px">🗒️</span> Caderninho e memória não dão conta</div>
      </div>
    </div>

    <!-- CENA 3 · Cadastrar (layout real) -->
    <div class="scene" id="s3" style="background:var(--bg)">
      <div class="phone"><div class="notch"></div>
        <div class="tb">
          <div class="tb-row"><span class="tb-title">Cadastrar</span><span class="tb-user">Taturi Baby · Rodolfo</span></div>
        </div>
        <div class="appbody">
          <div class="fcard">
            <div class="flabel">Foto do produto</div>
            <div class="fotobox">
              <div class="hint">📸 Toque para tirar a foto da peça</div>
              <div class="prod-foto"><div class="pfoto" style="background:#FDF2F8">
                <svg width="160" height="160" viewBox="0 0 120 120"><path d="M38 28 L52 20 Q60 26 68 20 L82 28 L90 44 L78 50 L78 92 Q60 100 42 92 L42 50 L30 44 Z" fill="#F9A8D4" stroke="#DB7FB4" stroke-width="2"/><circle cx="60" cy="56" r="10" fill="#fff" opacity=".8"/><path d="M55 56 q5 6 10 0" stroke="#DB2777" stroke-width="2" fill="none" stroke-linecap="round"/><circle cx="56" cy="53" r="1.6" fill="#DB2777"/><circle cx="64" cy="53" r="1.6" fill="#DB2777"/><path d="M46 78 h28" stroke="#fff" stroke-width="3" stroke-linecap="round" opacity=".7"/></svg>
              </div></div>
            </div>
            <div class="campos">
              <div class="campo"><small>Tamanho</small>P</div>
              <div class="campo"><small>Preço</small>R$ 39,90</div>
              <div class="campo"><small>Qtd</small>4</div>
            </div>
            <div class="ia"><span class="dot"></span> IA analisando a foto…</div>
            <div class="tags">
              <span class="tg t1">Body bebê</span><span class="tg t2">Rosa</span><span class="tg t3">Menina</span><span class="tg t4">Algodão</span><span class="tg t5">1–3 meses</span>
            </div>
            <div class="ok">✔ Produto catalogado automaticamente!</div>
          </div>
        </div>
        <nav class="bnav">
          <button class="bnav-item"><svg class="bnav-ic" viewBox="0 0 24 24"><path d="M6 2 3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z"/><path d="M3 6h18"/><path d="M16 10a4 4 0 0 1-8 0"/></svg><span class="bnav-lb">Vendas</span></button>
          <button class="bnav-item on"><svg class="bnav-ic" viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><path d="M12 8v8M8 12h8"/></svg><span class="bnav-lb">Cadastrar</span></button>
          <button class="bnav-item"><svg class="bnav-ic" viewBox="0 0 24 24"><path d="M21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16z"/><polyline points="3.27 6.96 12 12.01 20.73 6.96"/><line x1="12" y1="22.08" x2="12" y2="12"/></svg><span class="bnav-lb">Estoque</span></button>
          <button class="bnav-item"><svg class="bnav-ic" viewBox="0 0 24 24"><line x1="18" y1="20" x2="18" y2="10"/><line x1="12" y1="20" x2="12" y2="4"/><line x1="6" y1="20" x2="6" y2="14"/></svg><span class="bnav-lb">Relatórios</span></button>
          <button class="bnav-item"><svg class="bnav-ic" viewBox="0 0 24 24"><circle cx="12" cy="8" r="4"/><path d="M4 20c0-4 3.6-7 8-7s8 3 8 7"/></svg><span class="bnav-lb">Perfil</span></button>
        </nav>
      </div>
    </div>

    <!-- CENA 4 · Estoque (layout real) -->
    <div class="scene" id="s4" style="background:var(--bg)">
      <div class="phone"><div class="notch"></div>
        <div class="tb">
          <div class="tb-row"><span><span class="tb-title">Estoque</span><span class="tb-count">128 peças</span></span><span class="tb-user">Taturi Baby</span></div>
          <div class="srch"><svg viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2.2"><circle cx="11" cy="11" r="7"/><path d="M16.5 16.5L21 21"/></svg><input placeholder="Buscar por código, cor, tipo, ocasião..." readonly></div>
          <div class="estq-tabs">
            <button class="estq-tab on">Produtos</button>
            <button class="estq-tab">Visão Geral</button>
            <button class="estq-tab">Alertas <span style="background:var(--danger);color:#fff;border-radius:8px;padding:0 6px;font-size:9px">3</span></button>
          </div>
        </div>
        <div class="appbody">
          <div class="kpis">
            <div class="kpi"><div class="v">R$ 6.4k</div><div class="l">Valor em estoque</div></div>
            <div class="kpi"><div class="v">128</div><div class="l">Peças</div></div>
            <div class="kpi"><div class="v" style="color:var(--danger)">3</div><div class="l">Alertas</div></div>
          </div>
          <div class="grid2">
            <div class="pcard p1"><div class="pcard-img"><span class="stk-badge sok">8 un</span><div class="pfoto" style="background:#FDF2F8">
              <svg width="86" height="86" viewBox="0 0 120 120"><path d="M45 22 L60 30 L75 22 L86 40 L74 46 L80 92 Q60 102 40 92 L46 46 L34 40 Z" fill="#F472B6" stroke="#DB2777" stroke-width="2"/><path d="M45 60 Q60 68 75 60 M43 74 Q60 83 77 74" stroke="#fff" stroke-width="2.5" fill="none" opacity=".75"/><circle cx="52" cy="50" r="3" fill="#FDE68A"/><circle cx="66" cy="54" r="3" fill="#FDE68A"/></svg>
            </div></div><div class="pcard-body"><div class="pcard-nome">Vestido floral</div><div class="pcard-sub"><span class="cdot" style="background:#F472B6"></span>Menina · #014</div><div class="tam-chips"><span class="tam-chip">1</span><span class="tam-chip">2</span><span class="tam-chip">3</span></div><div class="pcard-preco">R$ 49,90</div></div></div>
            <div class="pcard p2"><div class="pcard-img"><span class="stk-badge sok">6 un</span><div class="pfoto" style="background:#EFF6FF">
              <svg width="86" height="86" viewBox="0 0 120 120"><path d="M40 30 L55 22 Q60 27 65 22 L80 30 L87 45 L76 50 L76 74 L44 74 L44 50 L33 45 Z" fill="#93C5FD" stroke="#3B82F6" stroke-width="2"/><rect x="44" y="74" width="14" height="22" rx="5" fill="#93C5FD" stroke="#3B82F6" stroke-width="2"/><rect x="62" y="74" width="14" height="22" rx="5" fill="#93C5FD" stroke="#3B82F6" stroke-width="2"/><circle cx="60" cy="48" r="7" fill="#fff" opacity=".85"/></svg>
            </div></div><div class="pcard-body"><div class="pcard-nome">Macacão menino</div><div class="pcard-sub"><span class="cdot" style="background:#3B82F6"></span>Menino · #017</div><div class="tam-chips"><span class="tam-chip">M</span><span class="tam-chip">G</span></div><div class="pcard-preco">R$ 59,90</div></div></div>
            <div class="pcard p3"><div class="pcard-img"><span class="stk-badge slow">3 un</span><div class="pfoto" style="background:#FEFCE8">
              <svg width="86" height="86" viewBox="0 0 120 120"><path d="M35 40 Q42 30 55 32 L58 40 L62 40 L65 32 Q78 30 85 40 L80 56 L72 52 L74 88 L46 88 L48 52 L40 56 Z" fill="#FDE047" stroke="#CA8A04" stroke-width="2"/><circle cx="60" cy="60" r="9" fill="#fff" opacity=".9"/></svg>
            </div></div><div class="pcard-body"><div class="pcard-nome">Camiseta sol</div><div class="pcard-sub"><span class="cdot" style="background:#FDE047"></span>Unissex · #009</div><div class="tam-chips"><span class="tam-chip">4</span><span class="tam-chip">6</span></div><div class="pcard-preco">R$ 29,90</div></div></div>
            <div class="pcard p4"><div class="pcard-img"><span class="stk-badge sok">12 un</span><div class="pfoto" style="background:#ECFDF5">
              <svg width="86" height="86" viewBox="0 0 120 120"><path d="M44 26 h32 v34 q0 8 -7 10 l0 18 q0 8 -9 8 t-9 -8 l0 -18 q-7 -2 -7 -10 Z" fill="#6EE7B7" stroke="#059669" stroke-width="2" transform="rotate(18 60 60)"/></svg>
            </div></div><div class="pcard-body"><div class="pcard-nome">Meia kit 3 pares</div><div class="pcard-sub"><span class="cdot" style="background:#6EE7B7"></span>Unissex · #022</div><div class="tam-chips"><span class="tam-chip">0</span><span class="tam-chip">1</span></div><div class="pcard-preco">R$ 19,90</div></div></div>
          </div>
          <div class="alerta"><span style="font-size:20px">⚠️</span><div class="tx">Body branco RN: restam 2 unidades<small>Toque para repor o estoque</small></div></div>
        </div>
        <nav class="bnav">
          <button class="bnav-item"><svg class="bnav-ic" viewBox="0 0 24 24"><path d="M6 2 3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z"/><path d="M3 6h18"/><path d="M16 10a4 4 0 0 1-8 0"/></svg><span class="bnav-lb">Vendas</span></button>
          <button class="bnav-item"><svg class="bnav-ic" viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><path d="M12 8v8M8 12h8"/></svg><span class="bnav-lb">Cadastrar</span></button>
          <button class="bnav-item on"><svg class="bnav-ic" viewBox="0 0 24 24"><path d="M21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16z"/><polyline points="3.27 6.96 12 12.01 20.73 6.96"/><line x1="12" y1="22.08" x2="12" y2="12"/></svg><span class="bnav-lb">Estoque</span></button>
          <button class="bnav-item"><svg class="bnav-ic" viewBox="0 0 24 24"><line x1="18" y1="20" x2="18" y2="10"/><line x1="12" y1="20" x2="12" y2="4"/><line x1="6" y1="20" x2="6" y2="14"/></svg><span class="bnav-lb">Relatórios</span></button>
          <button class="bnav-item"><svg class="bnav-ic" viewBox="0 0 24 24"><circle cx="12" cy="8" r="4"/><path d="M4 20c0-4 3.6-7 8-7s8 3 8 7"/></svg><span class="bnav-lb">Perfil</span></button>
        </nav>
      </div>
    </div>

    <!-- CENA 5 · WhatsApp -->
    <div class="scene" id="s5">
      <div class="phone"><div class="notch"></div>
        <div class="wa-top"><div class="wa-av">👶</div><div class="wa-nm">Taturi Baby <small>online</small></div></div>
        <div class="wa-body" id="wa-body">
          <div class="bl in" id="b1">Oi! Procuro um vestido pra minha filha de 2 anos 🎀<div class="hr">14:02</div></div>
          <div class="digitando" id="dg"><i></i><i></i><i></i></div>
          <div class="bl out" id="b2">Oi! Aqui é a Sofia, assistente da Taturi Baby 😊 Achei essas opções no tamanho 2:<div class="hr">14:02</div></div>
          <div class="bl out prod" id="b3">
            <div class="bimg"><div class="pfoto" style="background:#FDF2F8">
              <svg width="92" height="92" viewBox="0 0 120 120"><path d="M45 22 L60 30 L75 22 L86 40 L74 46 L80 92 Q60 102 40 92 L46 46 L34 40 Z" fill="#F472B6" stroke="#DB2777" stroke-width="2"/><path d="M45 60 Q60 68 75 60 M43 74 Q60 83 77 74" stroke="#fff" stroke-width="2.5" fill="none" opacity=".75"/><circle cx="52" cy="50" r="3" fill="#FDE68A"/><circle cx="66" cy="54" r="3" fill="#FDE68A"/></svg>
            </div></div>
            <div class="bcap">Vestido floral rosa · Tam 2<br><b>R$ 49,90</b> · Código #014</div>
          </div>
          <div class="bl out prod" id="b4">
            <div class="bimg"><div class="pfoto" style="background:#FEF3E8">
              <svg width="92" height="92" viewBox="0 0 120 120"><path d="M47 24 L60 31 L73 24 L83 40 L72 45 L79 90 Q60 99 41 90 L48 45 L37 40 Z" fill="#FDBA74" stroke="#EA580C" stroke-width="2"/><path d="M52 58 l5 6 l-5 6 M68 58 l-5 6 l5 6" stroke="#fff" stroke-width="2.5" fill="none" stroke-linecap="round"/></svg>
            </div></div>
            <div class="bcap">Vestido laranjinha · Tam 2<br><b>R$ 44,90</b> · Código #021</div>
          </div>
          <div class="bl in" id="b5">Amei o floral! 😍 Pode fechar<div class="hr">14:03</div></div>
          <div class="bl out" id="b6">Perfeito! Pedido <b>#012</b> fechado ✨ Já aviso a equipe da loja!<div class="hr">14:03</div></div>
        </div>
      </div>
    </div>

    <!-- CENA 6 · Vendas (layout real) -->
    <div class="scene" id="s6" style="background:var(--bg)">
      <div class="phone"><div class="notch"></div>
        <div class="tb">
          <div class="tb-row"><span class="tb-title">Vendas</span><span class="tb-user">Taturi Baby · Rodolfo</span></div>
        </div>
        <div class="appbody">
          <div class="subtabs"><div class="stab on">Em aberto</div><div class="stab">Concluídas</div></div>
          <div class="ped">
            <div class="ped-top"><div class="pednum">Pedido #012</div><div class="selo">🟢 WhatsApp</div></div>
            <div class="it">
              <div class="im"><div class="pfoto" style="background:#FDF2F8">
                <svg width="32" height="32" viewBox="0 0 120 120"><path d="M45 22 L60 30 L75 22 L86 40 L74 46 L80 92 Q60 102 40 92 L46 46 L34 40 Z" fill="#F472B6" stroke="#DB2777" stroke-width="3"/></svg>
              </div></div>
              <div><div class="nm">Vestido floral rosa · Tam 2</div><div class="dt">1 un · R$ 49,90</div></div>
            </div>
            <div class="cli">👩 Mariana · (31) 9 9999-0000 · 🛵 Entrega</div>
            <div class="tot"><span>Total</span><span>R$ 49,90</span></div>
            <div class="fbtn btnass" id="btnass">Assumir pedido</div>
            <div class="status">🤝 Em atendimento por você — Sofia em pausa</div>
            <div class="fbtn fbtn-success btnconc">✔ Concluir venda</div>
          </div>
        </div>
        <div class="toast">Venda registrada! Estoque atualizado 🎉</div>
        <nav class="bnav">
          <button class="bnav-item on"><svg class="bnav-ic" viewBox="0 0 24 24"><path d="M6 2 3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z"/><path d="M3 6h18"/><path d="M16 10a4 4 0 0 1-8 0"/></svg><span class="bnav-lb">Vendas</span></button>
          <button class="bnav-item"><svg class="bnav-ic" viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><path d="M12 8v8M8 12h8"/></svg><span class="bnav-lb">Cadastrar</span></button>
          <button class="bnav-item"><svg class="bnav-ic" viewBox="0 0 24 24"><path d="M21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16z"/><polyline points="3.27 6.96 12 12.01 20.73 6.96"/><line x1="12" y1="22.08" x2="12" y2="12"/></svg><span class="bnav-lb">Estoque</span></button>
          <button class="bnav-item"><svg class="bnav-ic" viewBox="0 0 24 24"><line x1="18" y1="20" x2="18" y2="10"/><line x1="12" y1="20" x2="12" y2="4"/><line x1="6" y1="20" x2="6" y2="14"/></svg><span class="bnav-lb">Relatórios</span></button>
          <button class="bnav-item"><svg class="bnav-ic" viewBox="0 0 24 24"><circle cx="12" cy="8" r="4"/><path d="M4 20c0-4 3.6-7 8-7s8 3 8 7"/></svg><span class="bnav-lb">Perfil</span></button>
        </nav>
      </div>
    </div>

    <!-- CENA 7 -->
    <div class="scene" id="s7">
      <div class="logo">G</div>
      <h2>Sua loja girando<br>sozinha.</h2>
      <div class="li l1">📸 Cadastro com inteligência artificial</div>
      <div class="li l2">💬 Atendimento automático no WhatsApp</div>
      <div class="li l3">📦 Estoque e vendas sob controle</div>
      <div class="cta">Chame no WhatsApp e experimente</div>
    </div>

    <div id="cap"><span id="cap-tx"></span></div>

    <div id="play-ov" onclick="iniciar()">
      <div class="g">G</div>
      <h1>Giro</h1>
      <p>Demo para gravação de tela<br>Formato vertical 9:16 · ~72 segundos</p>
      <div class="btn">▶ Começar</div>
    </div>
  </div>
</div>

<script>
function fit(){
  const st=document.getElementById('stage');
  const s=Math.min(innerWidth/405,innerHeight/720)*0.99;
  st.style.transform='scale('+s+')';
}
addEventListener('resize',fit);fit();

const T=[];
function at(ms,fn){T.push([ms,fn]);}
function cena(id){document.querySelectorAll('.scene').forEach(s=>s.classList.remove('on'));document.getElementById(id).classList.add('on');}
function leg(txt){
  const el=document.getElementById('cap-tx');
  el.classList.remove('on');
  setTimeout(()=>{if(txt){el.textContent=txt;el.classList.add('on');}},300);
}
function fase(id,cls){document.getElementById(id).classList.add(cls);}
function bolha(id){
  const b=document.getElementById(id);if(b)b.classList.add('show');
  const w=document.getElementById('wa-body');
  if(w)setTimeout(()=>{w.scrollTo({top:w.scrollHeight,behavior:'smooth'});},60);
}

const DUR=72000;
/* CENA 1 · 0–6s */
at(0,   ()=>{cena('s1');leg('Conheça o Giro 💜');});
at(3200,()=>leg('O sistema completo para a sua loja infantil'));
/* CENA 2 · 6–14s */
at(6000,()=>{cena('s2');leg('Vender pelo WhatsApp é ótimo…');});
at(9500,()=>leg('…mas controlar tudo na mão cansa 😮‍💨'));
/* CENA 3 · 14–26s */
at(14000,()=>{cena('s3');leg('Cadastrar produto? Só tirar a foto 📸');});
at(16200,()=>fase('s3','foto'));
at(17400,()=>{fase('s3','ia');leg('A inteligência artificial analisa a peça…');});
at(20200,()=>{fase('s3','tags');leg('…e cataloga tudo sozinha: tipo, cor, tamanho, tecido');});
at(23600,()=>{fase('s3','ok');leg('Pronto! Produto no estoque em segundos ✔');});
/* CENA 4 · 26–36s */
at(26000,()=>{cena('s4');leg('Seu estoque inteiro na palma da mão 📦');fase('s4','grid');});
at(30500,()=>{fase('s4','alerta');leg('E o Giro avisa quando algo está acabando ⚠️');});
/* CENA 5 · 36–57s */
at(36000,()=>{cena('s5');leg('E no WhatsApp? A Sofia atende por você 💬');bolha('b1');});
at(38800,()=>document.getElementById('dg').classList.add('show'));
at(40300,()=>{document.getElementById('dg').classList.remove('show');bolha('b2');leg('Ela entende o que o cliente procura…');});
at(43000,()=>{bolha('b3');leg('…e mostra os produtos certos, com foto e preço 🛍️');});
at(46000,()=>bolha('b4'));
at(49500,()=>{bolha('b5');leg('O cliente escolhe…');});
at(52500,()=>{bolha('b6');leg('…e a Sofia fecha o pedido sozinha ✨');});
/* CENA 6 · 57–67s */
at(57000,()=>{cena('s6');leg('O pedido cai direto no app 🛍️');fase('s6','ped');});
at(60000,()=>{leg('Sua equipe assume com um toque…');fase('s6','press');});
at(60400,()=>{document.getElementById('s6').classList.remove('press');fase('s6','atend');});
at(63400,()=>{leg('…conclui a venda e o estoque baixa sozinho 🎉');fase('s6','toast');});
/* CENA 7 · 67–72s */
at(67000,()=>{cena('s7');leg('');});

let timers=[],t0=0,rafId=null;
function iniciar(){
  document.getElementById('play-ov').style.display='none';
  document.getElementById('ctrl').style.display='block';
  rodar();
}
function rodar(){
  limpar();
  t0=performance.now();
  T.forEach(([ms,fn])=>timers.push(setTimeout(fn,ms)));
  (function tick(){
    const p=Math.min((performance.now()-t0)/DUR,1);
    document.getElementById('prog').style.width=(p*100)+'%';
    if(p<1)rafId=requestAnimationFrame(tick);
  })();
}
function limpar(){
  timers.forEach(clearTimeout);timers=[];
  if(rafId)cancelAnimationFrame(rafId);
  document.querySelectorAll('.scene').forEach(s=>s.classList.remove('on','foto','ia','tags','ok','grid','alerta','ped','press','atend','toast'));
  document.querySelectorAll('.bl,.digitando').forEach(b=>b.classList.remove('show'));
  const w=document.getElementById('wa-body'); if(w)w.scrollTop=0;
  document.getElementById('cap-tx').classList.remove('on');
  document.getElementById('prog').style.width='0%';
}
function reiniciar(){rodar();}
</script>
</body>
</html>
