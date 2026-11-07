# Haras-Brasil-
Jogo de cavalos 
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
<meta name="theme-color" content="#1a1410">
<meta name="apple-mobile-web-app-capable" content="yes">
<title>Haras BR</title>
<style>
  :root{
    --ouro:#e8b84b; --ouro-esc:#b8892a;
    --verde:#2e7d4f;
    --sombra:0 6px 18px rgba(0,0,0,.45);
    --bg1:#4a3524; --bg2:#1a1410;
    --card1:#33261a; --card2:#211810;
    --item1:#2a2016; --item2:#1c150e;
    --border:#3d2d1c;
    --texto:#f3e6cf; --texto-sec:#c9b898; --texto-fraco:#8a7a60;
    --header1:#2b2016; --header2:#1d150e;
  }
  body.claro{
    --ouro:#a06d0e; --ouro-esc:#7a520a;
    --bg1:#f5e9d4; --bg2:#e8d8b8;
    --card1:#fffaf0; --card2:#f3e6cf;
    --item1:#f0dfc0; --item2:#e8d4ad;
    --border:#c9a86a;
    --texto:#3a2a1a; --texto-sec:#6b5238; --texto-fraco:#9a8060;
    --header1:#f0dfc0; --header2:#e8d4ad;
  }
  *{box-sizing:border-box; -webkit-tap-highlight-color:transparent;}
  html,body{margin:0;padding:0;height:100%;}
  body{
    font-family:'Segoe UI',Roboto,system-ui,sans-serif;
    background:radial-gradient(ellipse at 50% 0%, var(--bg1) 0%, var(--bg2) 70%),var(--bg2);
    color:var(--texto); display:flex; justify-content:center;
    min-height:100vh; overflow-x:hidden;
    padding-top:env(safe-area-inset-top);
    padding-bottom:env(safe-area-inset-bottom);
    transition:background .3s, color .3s;
  }
  #app{
    width:100%; max-width:480px; min-height:100vh;
    display:flex; flex-direction:column;
    background:linear-gradient(180deg, rgba(0,0,0,.25), rgba(0,0,0,.6)),
      repeating-linear-gradient(0deg, transparent 0 38px, rgba(255,255,255,.015) 38px 40px);
    position:relative;
  }
  body.claro #app{background:linear-gradient(180deg, rgba(255,255,255,.4), rgba(255,255,255,.1));}
  header{
    display:flex; align-items:center; justify-content:space-between;
    padding:10px 8px; gap:3px;
    background:linear-gradient(180deg,var(--header1),var(--header2));
    border-bottom:2px solid var(--ouro-esc);
    box-shadow:var(--sombra);
    position:sticky; top:0; z-index:20;
  }
  header h1{font-size:.95rem; margin:0; letter-spacing:1px; color:var(--ouro); text-shadow:0 2px 4px rgba(0,0,0,.3); font-weight:800;}
  .header-right{display:flex; align-items:center; gap:2px; flex-wrap:nowrap;}
  .moedas{
    display:flex; align-items:center; gap:3px;
    background:rgba(0,0,0,.15); padding:4px 6px; border-radius:20px;
    border:1px solid var(--ouro-esc);
    font-weight:700; font-size:.68rem; color:var(--ouro);
  }
  .icone-btn{
    background:rgba(0,0,0,.15); border:1px solid var(--ouro-esc);
    color:var(--ouro); width:24px; height:24px; border-radius:50%;
    font-size:.7rem; cursor:pointer; display:flex; align-items:center; justify-content:center;
    padding:0; position:relative;
  }
  .icone-btn.off{opacity:.4;}
  .icone-btn .badge{
    position:absolute; top:-3px; right:-3px;
    background:#c0392b; color:#fff; font-size:.48rem;
    min-width:12px; height:12px; border-radius:6px;
    display:flex; align-items:center; justify-content:center;
    font-weight:700; padding:0 2px;
  }
  main{flex:1; padding:12px; display:flex; flex-direction:column; gap:12px; padding-bottom:80px;}
  .tela{display:none; flex-direction:column; gap:12px; animation:fade .35s ease;}
  .tela.ativa{display:flex;}
  @keyframes fade{from{opacity:0; transform:translateY(8px);} to{opacity:1; transform:none;}}
  .card{
    background:linear-gradient(160deg,var(--card1),var(--card2));
    border:1px solid var(--border); border-radius:16px;
    padding:14px; box-shadow:var(--sombra); position:relative; overflow:hidden;
  }
  .card::before{
    content:""; position:absolute; inset:0;
    background:radial-gradient(circle at 100% 0%, rgba(232,184,75,.12), transparent 60%);
    pointer-events:none;
  }
  .titulo-sec{
    font-size:.78rem; text-transform:uppercase; letter-spacing:2px;
    color:var(--ouro); margin:0 0 10px; font-weight:700;
    display:flex; align-items:center; gap:8px;
  }
  .titulo-sec::after{content:""; flex:1; height:1px; background:linear-gradient(90deg,var(--ouro-esc),transparent);}
  .btn{
    border:none; border-radius:12px; padding:14px;
    font-size:1rem; font-weight:700; letter-spacing:.5px;
    color:#1a1410; cursor:pointer;
    background:linear-gradient(180deg,#f0c85a,#c99a2e);
    box-shadow:0 4px 0 #8a6a1e, 0 8px 16px rgba(0,0,0,.4);
    transition:transform .1s, box-shadow .1s;
    width:100%; font-family:inherit;
  }
  .btn:active{transform:translateY(3px); box-shadow:0 1px 0 #8a6a1e;}
  .btn.sec{
    background:linear-gradient(180deg,var(--item1),var(--item2)); color:var(--texto);
    box-shadow:0 4px 0 rgba(0,0,0,.4), 0 8px 16px rgba(0,0,0,.3);
  }
  .btn.sec:active{box-shadow:0 1px 0 rgba(0,0,0,.4);}
  .btn.danger{background:linear-gradient(180deg,#e88a7a,#c0392b); color:#fff; box-shadow:0 4px 0 #7a2418, 0 8px 16px rgba(0,0,0,.4);}
  .btn.danger:active{box-shadow:0 1px 0 #7a2418;}
  .btn:disabled{opacity:.45; filter:grayscale(.5); box-shadow:none; transform:none;}
  .btn.small{padding:10px; font-size:.85rem;}
  .aviso{font-size:.75rem; color:var(--texto-sec); text-align:center; line-height:1.4;}
  .toast{
    position:fixed; bottom:90px; left:50%; transform:translateX(-50%) translateY(20px);
    background:rgba(20,15,10,.95); border:1px solid var(--ouro-esc);
    color:#f3e6cf; padding:10px 20px; border-radius:30px;
    font-size:.85rem; font-weight:600; z-index:200; opacity:0;
    transition:all .3s; pointer-events:none; white-space:nowrap;
  }
  .toast.show{opacity:1; transform:translateX(-50%) translateY(0);}
  .modal-bg{
    position:fixed; inset:0; z-index:100;
    background:rgba(0,0,0,.7); backdrop-filter:blur(3px);
    display:none; align-items:center; justify-content:center; padding:20px;
  }
  .modal-bg.ativo{display:flex; animation:fade .2s;}
  .modal{
    background:linear-gradient(160deg,var(--card1),var(--card2));
    border:2px solid var(--ouro-esc); border-radius:18px;
    padding:20px; width:100%; max-width:400px;
    box-shadow:0 20px 50px rgba(0,0,0,.7);
    max-height:85vh; overflow-y:auto;
  }
  .modal h3{margin:0 0 14px; color:var(--ouro); text-align:center;}
  .modal .btn{margin-top:8px;}
  textarea, input[type=text], input[type=password]{
    width:100%; padding:10px; border-radius:10px; background:var(--item2);
    color:var(--texto); border:1px solid var(--border); font-family:inherit;
    font-size:.85rem;
  }
  textarea{resize:none; font-family:monospace; font-size:.72rem;}

  /* ABA PREMIUM */
  .kit-card{
    background:linear-gradient(135deg, rgba(232,184,75,.2), rgba(176,122,224,.15));
    border:2px solid var(--ouro-esc); border-radius:16px;
    padding:16px; margin-bottom:12px; position:relative;
    box-shadow:0 8px 24px rgba(232,184,75,.2);
  }
  .kit-card h3{margin:0 0 4px; color:var(--ouro); text-align:center; font-size:1.1rem;}
  .kit-card .preco{
    text-align:center; font-size:1.6rem; font-weight:800;
    color:var(--ouro); margin:6px 0 12px;
  }
  .kit-item{
    display:flex; align-items:center; gap:10px;
    padding:8px 10px; background:rgba(0,0,0,.2); border-radius:10px;
    margin-bottom:6px; font-size:.82rem;
  }
  .kit-item .ic{font-size:1.3rem;}
  .kit-item .qtd{margin-left:auto; font-weight:700; color:var(--ouro);}
  .codigo-box{
    background:var(--item2); border:1px dashed var(--ouro-esc);
    border-radius:10px; padding:12px; margin-top:12px;
    text-align:center;
  }
  .codigo-box .cod{
    font-family:monospace; font-size:1rem; font-weight:800;
    color:var(--ouro); letter-spacing:1px; word-break:break-all;
    margin:8px 0;
  }
  .codigo-input{
    text-transform:uppercase; letter-spacing:1px; text-align:center;
    font-family:monospace; font-weight:700;
  }
  .resgate-info{
    font-size:.7rem; color:var(--texto-fraco); text-align:center;
    margin-top:8px; line-height:1.4;
  }
  .pix-aviso{
    background:rgba(232,184,75,.1); border:1px solid var(--ouro-esc);
    border-radius:10px; padding:10px; margin-top:10px;
    font-size:.72rem; color:var(--texto-sec); line-height:1.4;
    text-align:center;
  }
  .resgates-list{
    font-size:.7rem; color:var(--texto-fraco);
    max-height:80px; overflow-y:auto; margin-top:6px;
  }
</style>
</head>
<body>
<div id="app">
  <header>
    <h1>🐎 HARAS BR</h1>
    <div class="header-right">
      <button class="icone-btn" id="btn-tema" onclick="toggleTema()">🌙</button>
      <button class="icone-btn" onclick="mudarTela('premium', this)" title="Premium" style="border-color:var(--ouro);">💎</button>
      <div class="moedas"><span>🪙</span><span id="moedas">0</span></div>
      <button class="icone-btn" onclick="abrirSave()" title="Save">💾</button>
    </div>
  </header>

  <main>
    <section class="tela ativa" id="tela-haras">
      <div id="evento-haras"></div>
      <div class="card">
        <h2 class="titulo-sec">Meus Cavalos</h2>
        <div id="lista-cavalos"></div>
      </div>
      <button class="btn" onclick="abrirCompra()">🛒 Comprar Cavalo (150 🪙)</button>
    </section>

    <section class="tela" id="tela-criacao">
      <div class="card">
        <h2 class="titulo-sec">Criar Filhote</h2>
        <div class="aviso">Escolha dois cavalos de sexos opostos. O filhote herda atributos dos pais com variação genética.</div>
        <div style="margin-top:14px;font-size:.75rem;color:var(--texto-sec);margin-bottom:6px">Pai (macho)</div>
        <select id="sel-pai" style="width:100%;padding:10px;border-radius:10px;background:var(--item2);color:var(--texto);border:1px solid var(--border);font-family:inherit"></select>
        <div style="margin-top:10px;font-size:.75rem;color:var(--texto-sec);margin-bottom:6px">Mãe (fêmea)</div>
        <select id="sel-mae" style="width:100%;padding:10px;border-radius:10px;background:var(--item2);color:var(--texto);border:1px solid var(--border);font-family:inherit"></select>
        <button class="btn" style="margin-top:16px" onclick="criarFilhote()">🧬 Gerar Filhote (60 🪙)</button>
      </div>
      <div class="card" id="card-nascimento" style="display:none">
        <h2 class="titulo-sec">Nascimento!</h2>
        <div id="nascimento-conteudo"></div>
      </div>
    </section>

    <section class="tela" id="tela-corrida">
      <div class="card">
        <h2 class="titulo-sec">Corrida Rápida</h2>
        <div id="corrida-pre">
          <div style="font-size:.8rem;color:var(--texto-sec);margin-bottom:8px">Escolha seu cavalo:</div>
          <select id="sel-corrida" style="width:100%;padding:10px;border-radius:10px;background:var(--item2);color:var(--texto);border:1px solid var(--border);font-family:inherit"></select>
          <div style="font-size:.8rem;color:var(--texto-sec);margin:12px 0 6px">Valor da aposta:</div>
          <div class="aposta-box" id="apostas" style="display:flex;gap:8px;margin:12px 0;"></div>
          <button class="btn" onclick="iniciarCorrida(false)">🏁 Correr!</button>
          <button class="btn sec" style="margin-top:8px" onclick="iniciarCorrida('treino')">🎓 Treino (grátis)</button>
          <button class="btn sec" style="margin-top:8px" onclick="iniciarCorrida('arcade')">🎮 Arcade (50 🪙)</button>
        </div>
        <div id="corrida-ao-vivo" style="display:none">
          <div class="pista bioma-campina" id="pista"></div>
          <div id="corrida-status" style="text-align:center;margin-top:10px;font-weight:700;color:var(--ouro)"></div>
        </div>
      </div>
    </section>

    <section class="tela" id="tela-carreira">
      <div class="card">
        <h2 class="titulo-sec">Carreira</h2>
        <div id="lista-carreira" style="margin-top:12px"></div>
      </div>
    </section>

    <section class="tela" id="tela-loja">
      <div class="card">
        <h2 class="titulo-sec">🌟 Ofertas do Dia</h2>
        <div id="loja-ofertas"></div>
      </div>
      <div class="card">
        <h2 class="titulo-sec">🎯 Compra por Raridade</h2>
        <div class="loja-item" style="display:flex;align-items:center;gap:10px;padding:10px;background:rgba(0,0,0,.15);border-radius:10px;margin-bottom:8px;">
          <span style="font-size:1.5rem">🔵</span>
          <div style="flex:1;font-size:.8rem"><b>Raro garantido</b><br>+8 em tudo</div>
          <button class="btn small" style="width:auto;padding:8px 14px;" onclick="comprarRaridade('raro')">400 🪙</button>
        </div>
        <div class="loja-item" style="display:flex;align-items:center;gap:10px;padding:10px;background:rgba(0,0,0,.15);border-radius:10px;margin-bottom:8px;">
          <span style="font-size:1.5rem">🟣</span>
          <div style="flex:1;font-size:.8rem"><b>Épico garantido</b><br>+16 em tudo</div>
          <button class="btn small" style="width:auto;padding:8px 14px;" onclick="comprarRaridade('epico')">900 🪙</button>
        </div>
        <div class="loja-item" style="display:flex;align-items:center;gap:10px;padding:10px;background:rgba(0,0,0,.15);border-radius:10px;margin-bottom:8px;">
          <span style="font-size:1.5rem">🟡</span>
          <div style="flex:1;font-size:.8rem"><b>Lendário garantido</b><br>+25 em tudo</div>
          <button class="btn small" style="width:auto;padding:8px 14px;" onclick="comprarRaridade('lendario')">2.500 🪙</button>
        </div>
      </div>
      <div class="card">
        <h2 class="titulo-sec">Ração Premium</h2>
        <div class="loja-item" style="display:flex;align-items:center;gap:10px;padding:10px;background:rgba(0,0,0,.15);border-radius:10px;">
          <span style="font-size:1.5rem">🍎</span>
          <div style="flex:1;font-size:.8rem"><b>Ração Premium</b><br>+15% por 3 corridas</div>
          <button class="btn small" style="width:auto;padding:8px 14px;" onclick="comprarRacao()">200 🪙</button>
        </div>
      </div>
    </section>

    <section class="tela" id="tela-premium">
      <div class="card">
        <h2 class="titulo-sec">💎 Kit Boas-Vindas</h2>
        <div class="kit-card">
          <h3>Kit Boas-Vindas</h3>
          <div class="preco">R$ 4,99</div>
          <div class="kit-item"><span class="ic">🪙</span><span>Moedas</span><span class="qtd">1.000</span></div>
          <div class="kit-item"><span class="ic">🌟</span><span>Cavalo Lendário</span><span class="qtd">1</span></div>
          <div class="kit-item"><span class="ic">🧪</span><span>Poções de energia</span><span class="qtd">3</span></div>
          <div class="kit-item"><span class="ic">🍎</span><span>Ração Premium</span><span class="qtd">3 corridas</span></div>
          <button class="btn" style="margin-top:14px" onclick="comprarKitWhatsApp()">📱 Comprar via WhatsApp</button>
          <div class="pix-aviso">
            ⚠️ Pagamento e entrega são combinados pelo WhatsApp. Após confirmar, você recebe um <b>código de resgate</b> para colar abaixo.
          </div>
        </div>
        <div class="card" style="margin-top:12px">
          <h2 class="titulo-sec">🎟️ Resgatar código</h2>
          <input type="text" id="input-codigo" class="codigo-input" placeholder="KIT-XXXX-XXXX" maxlength="20">
          <button class="btn" style="margin-top:10px" onclick="resgatarCodigo()">Resgatar</button>
          <div class="resgate-info">
            Cada código pode ser usado apenas uma vez.<br>
            Códigos válidos começam com <b>KIT-</b>.
          </div>
          <div id="lista-resgates" class="resgates-list"></div>
        </div>
        <div class="card" style="margin-top:12px">
          <h2 class="titulo-sec">🔧 Área do vendedor</h2>
          <div class="aviso" style="margin-bottom:10px">Apenas para gerar códigos de resgate. Requer senha.</div>
          <button class="btn sec small" onclick="abrirGeradorCodigo()">Gerar novo código de resgate</button>
        </div>
      </div>
    </section>

    <section class="tela" id="tela-ranking">
      <div class="card">
        <h2 class="titulo-sec">Melhores Cavalos</h2>
        <div id="lista-ranking"></div>
      </div>
    </section>
  </main>

  <nav>
    <button class="ativo" data-tela="haras" onclick="mudarTela('haras',this)"><span class="ic">🐴</span>Haras</button>
    <button data-tela="criacao" onclick="mudarTela('criacao',this)"><span class="ic">🧬</span>Criar</button>
    <button data-tela="corrida" onclick="mudarTela('corrida',this)"><span class="ic">🏁</span>Correr</button>
    <button data-tela="carreira" onclick="mudarTela('carreira',this)"><span class="ic">📅</span>Carreira</button>
    <button data-tela="loja" onclick="mudarTela('loja',this)"><span class="ic">🛒</span>Loja</button>
    <button data-tela="ranking" onclick="mudarTela('ranking',this)"><span class="ic">🏆</span>Ranking</button>
  </nav>
</div>

<div class="modal-bg" id="modal-bg"><div class="modal" id="modal"></div></div>
<div class="toast" id="toast"></div>

<script>
/* =========================================================
   HARAS BR v8 — Premium + código de resgate
   ========================================================= */

const SAVE_KEY = 'harasBR_v8';
const WHATSAPP = '5598984501200'; // +55 98 98450-1200
const SENHA_VENDEDOR = 'haras2024'; // <-- TROQUE AQUI antes de publicar

const PELAGENS = [
  {nome:'Castanho', cor:'#8B5A2B', emoji:'🐎'},
  {nome:'Alazão',   cor:'#C0703A', emoji:'🐴'},
  {nome:'Preto',    cor:'#2b2b2b', emoji:'🐎'},
  {nome:'Tordilho', cor:'#9a9a9a', emoji:'🐴'},
  {nome:'Baio',     cor:'#D9A441', emoji:'🐎'},
  {nome:'Rosilho',  cor:'#B76E79', emoji:'🐴'},
];
const NOMES_M = ['Trovão','Relâmpago','Ventania','Fogoso','Sultão','Pégaso','Ciclone','Barão','Cometa','Meteoro'];
const NOMES_F = ['Estrela','Lua','Aurora','Dama','Pérola','Brisa','Fada','Rainha','Jade','Nuvem'];
const RARIDADES = [
  {id:'comum',    nome:'Comum',    bonus:0,  chance:.60},
  {id:'raro',     nome:'Raro',     bonus:8,  chance:.28},
  {id:'epico',    nome:'Épico',    bonus:16, chance:.10},
  {id:'lendario', nome:'Lendário', bonus:25, chance:.02},
];
const BIOMAS = [
  {id:'campina', nome:'Campina', emoji:'🌿', classe:'bioma-campina'},
  {id:'floresta', nome:'Floresta', emoji:'🌲', classe:'bioma-floresta'},
  {id:'deserto', nome:'Deserto', emoji:'🌵', classe:'bioma-deserto'},
  {id:'neve', nome:'Neve', emoji:'❄️', classe:'bioma-neve'},
];

let estado = null;
let apostaSelecionada = 10;
let corridaAnim = null;

/* ---------- ÁUDIO ---------- */
let audioCtx = null;
function getAudio(){
  if(!audioCtx){ try{ audioCtx = new (window.AudioContext||window.webkitAudioContext)(); }catch(e){} }
  return audioCtx;
}
function som(freq, dur, tipo='sine', vol=0.15){
  const ctx = getAudio(); if(!ctx) return;
  const osc = ctx.createOscillator(); const gain = ctx.createGain();
  osc.type = tipo; osc.frequency.value = freq;
  gain.gain.setValueAtTime(vol, ctx.currentTime);
  gain.gain.exponentialRampToValueAtTime(0.001, ctx.currentTime + dur);
  osc.connect(gain); gain.connect(ctx.destination);
  osc.start(); osc.stop(ctx.currentTime + dur);
}
function somGalope(){ som(220, .08, 'square', .06); }
function somVitoria(){ som(523,.15,'triangle',.2); setTimeout(()=>som(659,.15,'triangle',.2),120); setTimeout(()=>som(784,.3,'triangle',.2),260); }
function somCompra(){ som(880,.1,'sine',.15); setTimeout(()=>som(1175,.15,'sine',.15),80); }

/* ---------- TEMA ---------- */
function aplicarTema(){
  const claro = estado && estado.tema === 'claro';
  document.body.classList.toggle('claro', !!claro);
  const btn = document.getElementById('btn-tema');
  if(btn) btn.textContent = claro ? '☀️' : '🌙';
}
function toggleTema(){
  estado.tema = estado.tema === 'claro' ? 'escuro' : 'claro';
  aplicarTema(); salvar();
  toast(estado.tema === 'claro' ? '☀️ Tema claro' : '🌙 Tema escuro');
}

/* ---------- PERSISTÊNCIA ---------- */
function salvar(){
  try{
    localStorage.setItem(SAVE_KEY, JSON.stringify(estado));
    localStorage.setItem(SAVE_KEY + '_bkp', JSON.stringify(estado));
  }catch(e){}
}
function carregar(){
  try{
    const raw = localStorage.getItem(SAVE_KEY);
    if(raw) return JSON.parse(raw);
    const bkp = localStorage.getItem(SAVE_KEY + '_bkp');
    if(bkp) return JSON.parse(bkp);
  }catch(e){}
  return null;
}
function hojeStr(){ return new Date().toISOString().slice(0,10); }
function rnd(a,b){ return Math.floor(Math.random()*(b-a+1))+a; }

function sortearRaridade(){
  const r = Math.random(); let acc = 0;
  for(const rar of RARIDADES){ acc += rar.chance; if(r <= acc) return rar; }
  return RARIDADES[0];
}

function novoCavalo(opts={}){
  const sexo = opts.sexo || (Math.random()<.5?'M':'F');
  const pelagem = opts.pelagem || PELAGENS[Math.floor(Math.random()*PELAGENS.length)];
  const raridade = opts.raridade || sortearRaridade();
  const nome = opts.nome || (sexo==='M'
    ? NOMES_M[Math.floor(Math.random()*NOMES_M.length)]
    : NOMES_F[Math.floor(Math.random()*NOMES_F.length)]);
  const bonus = raridade.bonus;
  return {
    id: 'c'+Date.now()+Math.floor(Math.random()*99999),
    nome, sexo, pelagem: pelagem.nome, cor: pelagem.cor, emoji: pelagem.emoji,
    vel: Math.min(100, (opts.vel ?? rnd(30,60)) + bonus),
    res: Math.min(100, (opts.res ?? rnd(30,60)) + bonus),
    sor: Math.min(100, (opts.sor ?? rnd(20,50)) + bonus),
    geracao: opts.geracao ?? 1,
    raridade: raridade.id,
    vitorias: 0, corridas: 0,
    historico: [],
    ferraduras: opts.ferraduras ?? 0,
    energia: 100,
    ultimaRecarga: Date.now(),
  };
}

function estadoInicial(){
  return {
    moedas: 300,
    cavalos: [
      novoCavalo({sexo:'M', nome:'Trovão', vel:55, res:50, sor:40, geracao:1, raridade:RARIDADES[1]}),
      novoCavalo({sexo:'F', nome:'Estrela', vel:48, res:58, sor:45, geracao:1, raridade:RARIDADES[1]}),
    ],
    buffRacao: 0,
    carreiraSemana: 0,
    carreiraConcluida: false,
    tema: 'escuro',
    eventoAtivo: null,
    ofertasData: hojeStr(),
    ofertas: [],
    codigosResgatados: [],
    kitsComprados: 0,
    stats: { vitorias:0, corridas:0, filhotes:0, ferraduras:0, torneiosVencidos:0, prestígios:0, totalGanho:0, vitoriasArcade:0 },
  };
}

function iniciar(){
  estado = carregar() || estadoInicial();
  if(!estado.cavalos) estado.cavalos = [];
  if(typeof estado.moedas !== 'number') estado.moedas = 300;
  if(typeof estado.buffRacao !== 'number') estado.buffRacao = 0;
  if(typeof estado.carreiraSemana !== 'number') estado.carreiraSemana = 0;
  if(typeof estado.carreiraConcluida !== 'boolean') estado.carreiraConcluida = false;
  if(!estado.tema) estado.tema = 'escuro';
  if(!Array.isArray(estado.codigosResgatados)) estado.codigosResgatados = [];
  if(typeof estado.kitsComprados !== 'number') estado.kitsComprados = 0;
  if(!estado.stats) estado.stats = estadoInicial().stats;
  if(estado.ofertasData !== hojeStr() || !estado.ofertas || estado.ofertas.length===0){
    estado.ofertasData = hojeStr();
    estado.ofertas = gerarOfertas();
  }
  estado.cavalos.forEach(c=>{
    if(!c.historico) c.historico = [];
    if(typeof c.ferraduras !== 'number') c.ferraduras = 0;
    if(typeof c.energia !== 'number') c.energia = 100;
    if(!c.ultimaRecarga) c.ultimaRecarga = Date.now();
  });
  aplicarTema();
  renderTudo();
  salvar();
}

/* ---------- UI ---------- */
function atualizarMoedas(){ document.getElementById('moedas').textContent = estado.moedas; }
function toast(msg){
  const t = document.getElementById('toast');
  t.textContent = msg; t.classList.add('show');
  clearTimeout(t._tm); t._tm = setTimeout(()=>t.classList.remove('show'), 1800);
}
function mudarTela(nome, btn){
  document.querySelectorAll('.tela').forEach(s=>s.classList.remove('ativa'));
  const tela = document.getElementById('tela-'+nome);
  if(tela) tela.classList.add('ativa');
  document.querySelectorAll('nav button').forEach(b=>b.classList.remove('ativo'));
  if(btn && btn.tagName==='BUTTON' && btn.parentElement.tagName==='NAV') btn.classList.add('ativo');
  if(nome==='criacao') renderCriacao();
  if(nome==='corrida') renderCorridaSelect();
  if(nome==='loja') renderLoja();
  if(nome==='ranking') renderRanking();
  if(nome==='carreira') renderCarreira();
  if(nome==='haras') renderHaras();
  if(nome==='premium') renderPremium();
}
function nomeRaridade(id){ const r = RARIDADES.find(x=>x.id===id); return r ? r.nome : 'Comum'; }

function renderTudo(){
  atualizarMoedas();
  renderHaras(); renderCriacao(); renderCorridaSelect(); renderLoja(); renderRanking(); renderCarreira(); renderPremium();
}

/* ---------- RENDER: HARAS ---------- */
function renderHaras(){
  const cont = document.getElementById('lista-cavalos');
  if(!cont) return;
  if(estado.cavalos.length===0){
    cont.innerHTML = '<div class="vazio">Nenhum cavalo. Compre um para começar!</div>';
    return;
  }
  cont.innerHTML = estado.cavalos.map(c=>{
    const rarCls = 'raridade-'+c.raridade;
    const rarTagCls = 'rar-'+c.raridade;
    const ferStr = c.ferraduras > 0 ? ` 🔧${c.ferraduras}` : '';
    return `
    <div class="cavalo-item ${rarCls}" style="display:flex;align-items:center;gap:12px;padding:10px 12px;margin-bottom:8px;background:linear-gradient(135deg,var(--item1),var(--item2));border:1px solid var(--border);border-radius:12px;">
      <div style="width:48px;height:48px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:1.6rem;background:radial-gradient(circle at 35% 30%, #6b4e33, #2e2115);border:2px solid ${c.cor};">${c.emoji}</div>
      <div style="flex:1;min-width:0">
        <div style="font-weight:700;font-size:.9rem">${c.nome}<span style="font-size:.7rem;color:var(--ouro);margin-left:4px">${c.sexo==='M'?'♂':'♀'}</span>${ferStr}</div>
        <div style="display:flex;gap:8px;font-size:.64rem;color:var(--texto-sec);margin-top:2px;flex-wrap:wrap;">
          <span>⚡<b style="color:var(--ouro)">${c.vel}</b></span>
          <span>🛡️<b style="color:var(--ouro)">${c.res}</b></span>
          <span>🍀<b style="color:var(--ouro)">${c.sor}</b></span>
          <span class="raridade-tag ${rarTagCls}" style="margin-left:auto;font-size:.58rem;padding:1px 6px;border-radius:6px;">${nomeRaridade(c.raridade)}</span>
        </div>
        <div style="font-size:.64rem;color:var(--texto-sec);margin-top:3px;">
          🔋${Math.round(c.energia)}/100 · 🏆${c.vitorias}/${c.corridas} · G${c.geracao}
        </div>
      </div>
    </div>`;
  }).join('');
}

/* ---------- COMPRA ---------- */
function abrirCompra(){
  if(estado.moedas < 150){ toast('Moedas insuficientes!'); return; }
  const novo = novoCavalo({});
  estado.moedas -= 150; estado.cavalos.push(novo);
  somCompra(); renderTudo(); salvar();
  toast(`Você comprou ${novo.nome}! (${nomeRaridade(novo.raridade)})`);
}
function comprarRaridade(rarId){
  const map = {raro:400, epico:900, lendario:2500};
  const custo = map[rarId];
  if(!custo) return;
  if(estado.moedas < custo){ toast('Moedas insuficientes!'); return; }
  const rar = RARIDADES.find(r=>r.id===rarId);
  estado.moedas -= custo;
  const novo = novoCavalo({raridade: rar});
  estado.cavalos.push(novo);
  somCompra(); renderTudo(); salvar();
  toast(`🎯 ${nomeRaridade(rarId)} comprado: ${novo.nome}!`);
}
function comprarRacao(){
  if(estado.moedas < 200){ toast('Moedas insuficientes!'); return; }
  estado.moedas -= 200; estado.buffRacao += 3;
  somCompra(); renderTudo(); salvar();
  toast('🍎 Ração Premium ativada!');
}

/* ---------- OFERTAS ---------- */
function gerarOfertas(){
  const list = [];
  const pool = [
    {raridade:RARIDADES[1], custo:400},
    {raridade:RARIDADES[2], custo:900},
    {raridade:RARIDADES[3], custo:2500},
  ];
  for(let i=0;i<3;i++){
    const base = pool[Math.floor(Math.random()*pool.length)];
    const sexo = Math.random()<.5?'M':'F';
    const p = PELAGENS[Math.floor(Math.random()*PELAGENS.length)];
    list.push({
      sexo, pelagem:p.nome, cor:p.cor, emoji:p.emoji,
      vel: base.raridade.bonus + rnd(40,65),
      res: base.raridade.bonus + rnd(40,65),
      sor: base.raridade.bonus + rnd(30,60),
      raridade: base.raridade.id,
      custo: base.custo,
      nome: (sexo==='M'?NOMES_M:NOMES_F)[Math.floor(Math.random()*10)],
    });
  }
  return list;
}
function renderOfertas(){
  const cont = document.getElementById('loja-ofertas'); if(!cont) return;
  if(!estado.ofertas || estado.ofertas.length===0){ cont.innerHTML = '<div class="vazio">Sem ofertas hoje.</div>'; return; }
  cont.innerHTML = estado.ofertas.map((o,i)=>`
    <div class="oferta-item" style="display:flex;align-items:center;gap:10px;padding:10px;margin-bottom:8px;background:linear-gradient(135deg,var(--item1),var(--item2));border:1px solid var(--border);border-radius:10px;">
      <div style="width:42px;height:42px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:1.4rem;border:2px solid ${o.cor};">${o.emoji}</div>
      <div style="flex:1;font-size:.78rem;line-height:1.3;">
        <b style="color:var(--ouro)">${o.nome}</b> <span class="raridade-tag rar-${o.raridade}" style="font-size:.58rem;padding:1px 6px;border-radius:6px;">${nomeRaridade(o.raridade)}</span><br>
        ⚡${o.vel} 🛡️${o.res} 🍀${o.sor} · <b style="color:var(--ouro)">${o.custo} 🪙</b>
      </div>
      <button class="btn small" style="width:auto;padding:8px 14px;" onclick="comprarOferta(${i})">Comprar</button>
    </div>
  `).join('');
}
function comprarOferta(i){
  const o = estado.ofertas[i]; if(!o) return;
  if(estado.moedas < o.custo){ toast('Moedas insuficientes!'); return; }
  estado.moedas -= o.custo;
  const rar = RARIDADES.find(r=>r.id===o.raridade) || RARIDADES[1];
  const pel = PELAGENS.find(p=>p.nome===o.pelagem) || {nome:o.pelagem, cor:o.cor, emoji:o.emoji};
  const novo = novoCavalo({sexo:o.sexo, raridade:rar, pelagem:pel, vel:o.vel, res:o.res, sor:o.sor, nome:o.nome});
  estado.cavalos.push(novo);
  estado.ofertas.splice(i,1);
  somCompra(); renderTudo(); salvar();
  toast(`🌟 ${o.nome} comprado!`);
}

/* ---------- CRIAÇÃO ---------- */
function renderCriacao(){
  const machos = estado.cavalos.filter(c=>c.sexo==='M');
  const femeas = estado.cavalos.filter(c=>c.sexo==='F');
  const selPai = document.getElementById('sel-pai');
  const selMae = document.getElementById('sel-mae');
  if(selPai) selPai.innerHTML = machos.length
    ? machos.map(c=>`<option value="${c.id}">${c.nome} (⚡${c.vel} 🛡️${c.res} 🍀${c.sor})</option>`).join('')
    : '<option value="">— nenhum macho —</option>';
  if(selMae) selMae.innerHTML = femeas.length
    ? femeas.map(c=>`<option value="${c.id}">${c.nome} (⚡${c.vel} 🛡️${c.res} 🍀${c.sor})</option>`).join('')
    : '<option value="">— nenhuma fêmea —</option>';
}
function criarFilhote(){
  const idPai = document.getElementById('sel-pai').value;
  const idMae = document.getElementById('sel-mae').value;
  if(!idPai || !idMae){ toast('Selecione um macho e uma fêmea!'); return; }
  if(estado.moedas < 60){ toast('Moedas insuficientes!'); return; }
  const pai = estado.cavalos.find(c=>c.id===idPai);
  const mae = estado.cavalos.find(c=>c.id===idMae);
  if(!pai || !mae) return;
  const media = (a,b)=> Math.round((a+b)/2);
  const varia = (base)=> Math.max(5, Math.min(100, base + rnd(-8,8)));
  const atrs = {
    vel: varia(media(pai.vel, mae.vel)),
    res: varia(media(pai.res, mae.res)),
    sor: varia(media(pai.sor, mae.sor)),
  };
  let pelagem = PELAGENS.find(p=>p.nome === (Math.random()<.5?pai.pelagem:mae.pelagem)) || PELAGENS[0];
  if(Math.random()>=.6) pelagem = PELAGENS[Math.floor(Math.random()*PELAGENS.length)];
  const raridadeFilho = (Math.random()<.15) ? sortearRaridade() : RARIDADES[0];
  const filhote = novoCavalo({
    sexo: Math.random()<.5?'M':'F', pelagem, raridade: raridadeFilho,
    vel: atrs.vel, res: atrs.res, sor: atrs.sor,
    geracao: Math.max(pai.geracao, mae.geracao)+1,
  });
  estado.moedas -= 60; estado.cavalos.push(filhote);
  estado.stats.filhotes++;
  somCompra(); renderTudo(); salvar();
  const cont = document.getElementById('nascimento-conteudo');
  if(cont){
    cont.innerHTML = `
      <div style="text-align:center;margin-bottom:10px">
        <div style="width:64px;height:64px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:2.2rem;margin:0 auto;border:2px solid ${filhote.cor}">${filhote.emoji}</div>
        <div style="font-weight:800;font-size:1.1rem;margin-top:8px">${filhote.nome}</div>
        <div style="color:var(--texto-sec);font-size:.8rem">${filhote.pelagem} · ${filhote.sexo==='M'?'Macho':'Fêmea'} · G${filhote.geracao} · <b style="color:var(--ouro)">${nomeRaridade(filhote.raridade)}</b></div>
      </div>
      <div style="margin-bottom:6px"><div style="display:flex;justify-content:space-between;font-size:.75rem;"><span>⚡ Velocidade</span><b>${filhote.vel}</b></div></div>
      <div style="margin-bottom:6px"><div style="display:flex;justify-content:space-between;font-size:.75rem;"><span>🛡️ Resistência</span><b>${filhote.res}</b></div></div>
      <div style="margin-bottom:6px"><div style="display:flex;justify-content:space-between;font-size:.75rem;"><span>🍀 Sorte</span><b>${filhote.sor}</b></div></div>
    `;
    document.getElementById('card-nascimento').style.display='block';
  }
  toast('Filhote gerado!');
}

/* ---------- CORRIDA ---------- */
function renderCorridaSelect(){
  const sel = document.getElementById('sel-corrida');
  if(sel) sel.innerHTML = estado.cavalos.length
    ? estado.cavalos.map(c=>`<option value="${c.id}">${c.nome} ⚡${c.vel} 🛡️${c.res} 🍀${c.sor} 🔋${Math.round(c.energia)}</option>`).join('')
    : '<option value="">— sem cavalos —</option>';
  const apostas = document.getElementById('apostas');
  if(apostas){
    apostas.innerHTML = [10,25,50,100].map(v=>`<button data-v="${v}" class="${v===apostaSelecionada?'sel':''}" style="flex:1;padding:10px;border-radius:10px;border:2px solid ${v===apostaSelecionada?'var(--ouro)':'var(--border)'};background:var(--item2);color:${v===apostaSelecionada?'var(--ouro)':'var(--texto)'};font-weight:700;font-family:inherit;font-size:.85rem;" onclick="selecionarAposta(${v})">${v} 🪙</button>`).join('');
  }
  const pre = document.getElementById('corrida-pre');
  const vivo = document.getElementById('corrida-ao-vivo');
  if(pre) pre.style.display='block';
  if(vivo) vivo.style.display='none';
}
function selecionarAposta(v){ apostaSelecionada = v; renderCorridaSelect(); }

function iniciarCorrida(modo){
  const treino = modo === 'treino';
  const arcade = modo === 'arcade';
  const id = document.getElementById('sel-corrida').value;
  if(!id){ toast('Sem cavalos para correr!'); return; }
  const meu = estado.cavalos.find(c=>c.id===id);
  if(!meu){ toast('Cavalo inválido.'); return; }
  let custo = 0, premio1 = 0, premio2 = 0, premio3 = 0, titulo = '';
  if(treino){ custo = 0; titulo = '🎓 Treino'; }
  else if(arcade){ custo = 50; premio1 = 300; premio2 = 100; premio3 = 50; titulo = '🎮 Arcade'; }
  else { custo = apostaSelecionada; premio1 = Math.round(custo*3.5); premio2 = Math.round(custo*2); premio3 = custo; titulo = '🏁 Corrida Rápida'; }
  if(!treino && estado.moedas < custo){ toast('Moedas insuficientes!'); return; }
  if(!treino && meu.energia < 10){ toast('Cavalo muito cansado!'); return; }
  if(!treino){ estado.moedas -= custo; meu.energia = Math.max(0, meu.energia - 25); meu.ultimaRecarga = Date.now(); }
  atualizarMoedas();

  const nAdv = rnd(3,5);
  const adversarios = [];
  for(let i=0;i<nAdv;i++){
    const sexo = Math.random()<.5?'M':'F';
    const p = PELAGENS[Math.floor(Math.random()*PELAGENS.length)];
    const base = arcade ? 60 : rnd(35,75);
    adversarios.push({
      nome: (sexo==='M'?NOMES_M:NOMES_F)[Math.floor(Math.random()*8)] + (i+1),
      vel: base + rnd(-5,5), res: base + rnd(-5,5), sor: rnd(20,80),
      cor: p.cor, emoji: p.emoji, meu:false
    });
  }
  const pelotao = [{...meu, meu:true}, ...adversarios];

  const pista = document.getElementById('pista');
  const bioma = BIOMAS[Math.floor(Math.random()*BIOMAS.length)];
  pista.className = 'pista ' + bioma.classe;
  pista.innerHTML = '<div class="linha-chegada"></div>';
  pelotao.forEach((c,i)=>{
    const corredor = document.createElement('div');
    corredor.className = 'corredor';
    corredor.style.position='absolute';
    corredor.style.top = (i*(100/pelotao.length)) + '%';
    corredor.style.height = (100/pelotao.length) + '%';
    corredor.style.left='0'; corredor.style.right='0';
    corredor.style.display='flex'; corredor.style.alignItems='center';
    corredor.style.borderBottom = '1px dashed rgba(255,255,255,.25)';
    corredor.innerHTML = `
      <span class="emoji" id="emoji-${i}" style="position:relative;z-index:2;font-size:1.7rem;left:2%">${c.emoji}</span>
      <span style="position:absolute;right:8px;font-size:.6rem;color:#fff;background:rgba(0,0,0,.35);padding:1px 6px;border-radius:8px;font-weight:700;">${c.nome}${c.meu?' ⭐':''}</span>
    `;
    pista.appendChild(corredor);
  });
  document.getElementById('corrida-pre').style.display='none';
  document.getElementById('corrida-ao-vivo').style.display='block';
  document.getElementById('corrida-status').textContent = titulo + '...';

  const progresso = pelotao.map(()=>0);
  const velBase = pelotao.map(c=> 0.55 + (c.vel/100)*0.55 + Math.random()*0.15);
  const fadiga = pelotao.map(()=>0);
  const DURACAO = 4200;
  const inicio = performance.now();
  let ultimo = inicio, somTimer = 0;
  if(corridaAnim) cancelAnimationFrame(corridaAnim);

  function loop(now){
    const dt = Math.min(50, now - ultimo); ultimo = now;
    for(let i=0;i<pelotao.length;i++){
      const pico = Math.random() < 0.02 ? 1.6 : 1;
      const bonusSorte = 1 + (pelotao[i].sor/100)*0.08*(Math.random()*2-1);
      fadiga[i] += dt*0.002;
      const fadFator = 1 - Math.max(0, (fadiga[i] - (pelotao[i].res/100)*0.6))*0.3;
      const inc = velBase[i] * pico * bonusSorte * Math.max(0.3, fadFator) * (dt/16);
      progresso[i] = Math.min(100, progresso[i] + inc);
    }
    for(let i=0;i<pelotao.length;i++){
      const el = document.getElementById('emoji-'+i);
      if(el) el.style.left = (progresso[i]*0.92) + '%';
    }
    if(now - somTimer > 260){ somGalope(); somTimer = now; }
    if(progresso.some(p=>p>=100) || now-inicio > DURACAO*1.3){
      finalizarCorrida(pelotao, progresso, meu, {custo, premio1, premio2, premio3, titulo, treino, arcade});
      return;
    }
    corridaAnim = requestAnimationFrame(loop);
  }
  corridaAnim = requestAnimationFrame(loop);
}

function finalizarCorrida(pelotao, progresso, meu, ctx){
  const ordem = pelotao.map((c,i)=>({...c, prog:progresso[i]})).sort((a,b)=>b.prog-a.prog);
  const posMeu = ordem.findIndex(c=>c.meu)+1;
  let ganho = 0;
  if(!ctx.treino){
    if(posMeu===1) ganho = ctx.premio1;
    else if(posMeu===2) ganho = ctx.premio2;
    else if(posMeu===3) ganho = ctx.premio3;
  }
  estado.moedas += ganho; atualizarMoedas();
  estado.stats.totalGanho += ganho;

  const cavaloReal = estado.cavalos.find(c=>c.id===meu.id);
  if(cavaloReal){
    cavaloReal.corridas++;
    if(posMeu===1) cavaloReal.vitorias++;
    cavaloReal.historico.push({pos:posMeu, premio:ganho, data:Date.now()});
    if(cavaloReal.historico.length > 5) cavaloReal.historico.shift();
  }
  estado.stats.corridas++;
  if(posMeu===1){
    estado.stats.vitorias++;
    if(ctx.arcade) estado.stats.vitoriasArcade++;
  }
  salvar();
  if(posMeu===1) somVitoria();

  const status = document.getElementById('corrida-status');
  if(status) status.innerHTML = `${posMeu}º lugar! ${ganho>0?'+'+ganho+' 🪙':(ctx.treino?'treino':'sem prêmio')}`;

  const modal = document.getElementById('modal');
  modal.innerHTML = `
    <h3>${ctx.titulo}</h3>
    ${ordem.map((c,i)=>{
      const cls = i===0 ? 'first' : '';
      let g = '';
      if(c.meu){
        if(ctx.treino) g = '';
        else g = ganho>0 ? `<span class="ganho">+${ganho} 🪙</span>` : `<span class="ganho perda">-${ctx.custo} 🪙</span>`;
      }
      return `<div class="resultado-linha ${cls}">
        <span class="pos">${i+1}º</span>
        <span style="font-size:1.2rem">${c.emoji}</span>
        <span>${c.nome}${c.meu?' ⭐':''}</span>
        ${g}
      </div>`;
    }).join('')}
    <button class="btn" onclick="fecharModal(); renderTudo();">Continuar</button>
  `;
  document.getElementById('modal-bg').classList.add('ativo');
}
function fecharModal(){ document.getElementById('modal-bg').classList.remove('ativo'); }
document.getElementById('modal-bg').addEventListener('click', e=>{ if(e.target.id==='modal-bg') fecharModal(); });

/* ---------- CARREIRA (simplificada) ---------- */
function renderCarreira(){
  const cont = document.getElementById('lista-carreira'); if(!cont) return;
  if(estado.carreiraConcluida){
    cont.innerHTML = '<div class="aviso" style="color:var(--ouro);font-weight:700">🏆 Carreira completa!</div>';
    return;
  }
  const semana = estado.carreiraSemana + 1;
  const premios = [150, 300, 600, 1000, 1800, 3000];
  const custos = [0, 50, 100, 150, 200, 300];
  if(semana > 6){
    cont.innerHTML = '<div class="aviso">Carreira concluída.</div>';
    return;
  }
  cont.innerHTML = `
    <div style="padding:12px;background:linear-gradient(135deg,var(--item1),var(--item2));border:1px solid var(--border);border-radius:12px;">
      <div style="font-weight:800;font-size:.9rem">Semana ${semana}</div>
      <div style="font-size:.75rem;color:var(--texto-sec);margin-top:4px">Prêmio: <b style="color:var(--ouro)">${premios[semana-1]} 🪙</b> · Inscrição: ${custos[semana-1]} 🪙</div>
      <button class="btn" style="margin-top:10px" onclick="correrCarreira()">🏁 Correr</button>
    </div>
  `;
}
function correrCarreira(){
  const semana = estado.carreiraSemana + 1;
  const custos = [0, 50, 100, 150, 200, 300];
  const premios = [150, 300, 600, 1000, 1800, 3000];
  if(estado.moedas < custos[semana-1]){ toast('Moedas insuficientes!'); return; }
  if(estado.cavalos.length === 0){ toast('Sem cavalos!'); return; }
  const meu = estado.cavalos[0];
  estado.moedas -= custos[semana-1];
  atualizarMoedas();
  // corrida simplificada
  const modal = document.getElementById('modal');
  modal.innerHTML = `
    <h3>📅 Semana ${semana}</h3>
    <div class="aviso" style="margin-bottom:10px">Vitória = avança. Derrota = fica.</div>
    <button class="btn" onclick="resolverCarreira(${semana}, ${premios[semana-1]}, ${custos[semana-1]})">🏁 Correr agora</button>
    <button class="btn sec" onclick="fecharModal()">Cancelar</button>
  `;
  document.getElementById('modal-bg').classList.add('ativo');
}
function resolverCarreira(semana, premio, custo){
  fecharModal();
  const chance = 0.5 + (estado.cavalos[0].vel / 200);
  const venceu = Math.random() < chance;
  if(venceu){
    estado.moedas += premio;
    estado.carreiraSemana++;
    if(estado.carreiraSemana >= 6){ estado.carreiraConcluida = true; }
    somVitoria();
    toast(`🏆 Venceu! +${premio} 🪙`);
  } else {
    toast('❌ Perdeu. Tente de novo!');
  }
  renderTudo(); salvar();
}

/* ---------- LOJA ---------- */
function renderLoja(){
  renderOfertas();
  const buff = document.getElementById('buff-status');
  if(buff) buff.innerHTML = estado.buffRacao > 0 ? `🍎 Buff ativo: ${estado.buffRacao} corrida(s)` : 'Sem buff ativo.';
}

/* ---------- RANKING ---------- */
function renderRanking(){
  const cont = document.getElementById('lista-ranking'); if(!cont) return;
  const top = [...estado.cavalos].sort((a,b)=> (b.vitorias-a.vitorias) || ((b.vel+b.res+b.sor)-(a.vel+a.res+a.sor))).slice(0,8);
  if(top.length===0){ cont.innerHTML = '<div class="vazio">Sem cavalos.</div>'; return; }
  cont.innerHTML = top.map((c,i)=>`
    <div class="rank-item" style="display:flex;align-items:center;gap:10px;padding:10px;background:rgba(0,0,0,.15);border-radius:10px;margin-bottom:6px;">
      <span style="font-weight:800;color:var(--ouro);font-size:1.1rem;width:30px;text-align:center;">${i+1}º</span>
      <div style="width:38px;height:38px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:1.2rem;border:2px solid ${c.cor};">${c.emoji}</div>
      <div style="flex:1;min-width:0">
        <div style="font-weight:700;font-size:.85rem">${c.nome}</div>
        <div style="font-size:.65rem;color:var(--texto-sec)">🏆 ${c.vitorias} · ⚡${c.vel} 🛡️${c.res} 🍀${c.sor}</div>
      </div>
    </div>
  `).join('');
}

/* ---------- PREMIUM ---------- */
function renderPremium(){
  const cont = document.getElementById('lista-resgates');
  if(cont){
    cont.innerHTML = estado.codigosResgatados.length
      ? 'Resgatados: ' + estado.codigosResgatados.map(c=>c.slice(-4)).join(', ')
      : '';
  }
}
function comprarKitWhatsApp(){
  const msg = encodeURIComponent(
    'Olá! Quero comprar o *Kit Boas-Vindas* do Haras BR (R$ 4,99).\n\n' +
    'Itens: 1.000 moedas, 1 cavalo Lendário, 3 poções, 3 corridas de Ração Premium.\n\n' +
    'Meu nome no jogo: ________________'
  );
  const url = `https://wa.me/${WHATSAPP}?text=${msg}`;
  window.open(url, '_blank');
  toast('Abrindo WhatsApp...');
}

/* ---------- RESGATE DE CÓDIGO ---------- */
function gerarCodigoValido(){
  // formato: KIT-XXXX-XXXX (aleatório, 8 caracteres alfanuméricos)
  const chars = 'ABCDEFGHJKLMNPQRSTUVWXYZ23456789';
  let a = '', b = '';
  for(let i=0;i<4;i++) a += chars[Math.floor(Math.random()*chars.length)];
  for(let i=0;i<4;i++) b += chars[Math.floor(Math.random()*chars.length)];
  return `KIT-${a}-${b}`;
}
function resgatarCodigo(){
  const input = document.getElementById('input-codigo');
  if(!input) return;
  const cod = (input.value || '').trim().toUpperCase();
  if(!cod){ toast('Digite um código.'); return; }
  if(!/^KIT-[A-Z0-9]{4}-[A-Z0-9]{4}$/.test(cod)){
    toast('Formato inválido. Use KIT-XXXX-XXXX.');
    return;
  }
  if(estado.codigosResgatados.includes(cod)){
    toast('Esse código já foi resgatado.');
    return;
  }
  // aplica recompensas do kit
  estado.moedas += 1000;
  const lendario = RARIDADES.find(r=>r.id==='lendario');
  const cavaloLendario = novoCavalo({ raridade: lendario });
  estado.cavalos.push(cavaloLendario);
  estado.buffRacao += 3;
  estado.kitsComprados++;
  estado.codigosResgatados.push(cod);
  somVitoria(); renderTudo(); salvar();
  input.value = '';
  toast('🎉 Kit resgatado! +1.000 🪙, cavalo lendário, ração e 3 poções');
  // mostra modal com o que ganhou
  const modal = document.getElementById('modal');
  modal.innerHTML = `
    <h3>🎉 Kit resgatado!</h3>
    <div class="kit-item"><span class="ic">🪙</span><span>Moedas</span><span class="qtd">+1.000</span></div>
    <div class="kit-item"><span class="ic">🌟</span><span>${cavaloLendario.nome} (Lendário)</span><span class="qtd">+1</span></div>
    <div class="kit-item"><span class="ic">🍎</span><span>Ração Premium</span><span class="qtd">+3 corridas</span></div>
    <div class="kit-item"><span class="ic">🧪</span><span>Poções</span><span class="qtd">+3</span></div>
    <button class="btn" onclick="fecharModal(); renderTudo();">Continuar</button>
  `;
  document.getElementById('modal-bg').classList.add('ativo');
}

/* ---------- GERADOR DE CÓDIGO (VENDEDOR) ---------- */
function abrirGeradorCodigo(){
  const modal = document.getElementById('modal');
  modal.innerHTML = `
    <h3>🔧 Área do vendedor</h3>
    <div class="aviso" style="margin-bottom:10px">Digite a senha para gerar códigos.</div>
    <input type="password" id="senha-vendedor" placeholder="Senha" style="width:100%;padding:10px;border-radius:10px;background:var(--item2);color:var(--texto);border:1px solid var(--border);font-family:inherit;">
    <button class="btn" style="margin-top:10px" onclick="validarSenhaEGerar()">Entrar</button>
    <button class="btn sec" onclick="fecharModal()">Cancelar</button>
  `;
  document.getElementById('modal-bg').classList.add('ativo');
}
function validarSenhaEGerar(){
  const senha = document.getElementById('senha-vendedor').value;
  if(senha !== SENHA_VENDEDOR){ toast('Senha incorreta.'); return; }
  const cod = gerarCodigoValido();
  const modal = document.getElementById('modal');
  modal.innerHTML = `
    <h3>🎟️ Código gerado</h3>
    <div class="aviso" style="margin-bottom:10px">Envie este código para o cliente após confirmar o pagamento.</div>
    <div class="codigo-box">
      <div class="cod" id="cod-gerado">${cod}</div>
    </div>
    <button class="btn small" onclick="copiarCodigoGerado()">📋 Copiar código</button>
    <button class="btn sec" onclick="abrirGeradorCodigo()">Gerar outro</button>
    <button class="btn sec" onclick="fecharModal()">Fechar</button>
  `;
}
function copiarCodigoGerado(){
  const el = document.getElementById('cod-gerado'); if(!el) return;
  const txt = el.textContent;
  if(navigator.clipboard && navigator.clipboard.writeText){
    navigator.clipboard.writeText(txt).then(()=>toast('Código copiado!')).catch(()=>toast('Copie manualmente.'));
  } else {
    toast('Copie manualmente: ' + txt);
  }
}

/* ---------- SAVE ---------- */
function abrirSave(){
  const modal = document.getElementById('modal');
  const json = btoa(unescape(encodeURIComponent(JSON.stringify(estado))));
  modal.innerHTML = `
    <h3>💾 Save</h3>
    <textarea id="save-txt" readonly style="width:100%;height:120px;background:var(--item2);color:var(--texto-sec);border:1px solid var(--border);border-radius:10px;padding:8px;">${json}</textarea>
    <button class="btn small" onclick="copiarSave()">📋 Copiar</button>
    <button class="btn sec small" onclick="abrirImport()">📥 Importar</button>
    <button class="btn sec small" onclick="fecharModal()">Fechar</button>
  `;
  document.getElementById('modal-bg').classList.add('ativo');
}
function copiarSave(){
  const ta = document.getElementById('save-txt'); if(!ta) return;
  ta.select(); ta.setSelectionRange(0,99999);
  try{ document.execCommand('copy'); toast('Copiado!'); }catch(e){ toast('Copie manualmente.'); }
}
function abrirImport(){
  const modal = document.getElementById('modal');
  modal.innerHTML = `
    <h3>📥 Importar</h3>
    <textarea id="imp-txt" style="width:100%;height:120px;background:var(--item2);color:var(--texto);border:1px solid var(--border);border-radius:10px;padding:8px;"></textarea>
    <button class="btn small" onclick="importarSave()">Importar</button>
    <button class="btn sec small" onclick="fecharModal()">Cancelar</button>
  `;
}
function importarSave(){
  const ta = document.getElementById('imp-txt'); if(!ta) return;
  try{
    const obj = JSON.parse(decodeURIComponent(escape(atob(ta.value.trim()))));
    if(!obj.cavalos) throw new Error('inválido');
    estado = obj;
    if(!Array.isArray(estado.codigosResgatados)) estado.codigosResgatados = [];
    if(typeof estado.kitsComprados !== 'number') estado.kitsComprados = 0;
    if(!estado.stats) estado.stats = estadoInicial().stats;
    aplicarTema(); renderTudo(); salvar(); fecharModal();
    toast('Save importado!');
  }catch(e){ toast('Código inválido.'); }
}

/* ---------- START ---------- */
iniciar();
</script>
</body>
</html>