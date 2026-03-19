<!DOCTYPE html>

<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="MarketIntel">
<meta name="theme-color" content="#0a0e1a">
<title>MarketIntel</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Serif+JP:wght@400;700;900&family=Noto+Sans+JP:wght@400;700&display=swap" rel="stylesheet">
<style>
:root{--bg:#0a0e1a;--surface:rgba(255,255,255,0.03);--border:rgba(99,179,237,0.15);--accent:#4299e1;--accent2:#63b3ed;--text:#e2e8f0;--muted:#718096;--up:#22c55e;--down:#ef4444;--flat:#f59e0b;--serif:'Noto Serif JP',Georgia,serif;--sans:'Noto Sans JP',sans-serif;}
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
html,body{height:100%;background:var(--bg);color:var(--text);font-family:var(--serif);-webkit-font-smoothing:antialiased;}
body::before{content:'';position:fixed;inset:0;z-index:0;pointer-events:none;background-image:linear-gradient(rgba(99,179,237,0.03)1px,transparent 1px),linear-gradient(90deg,rgba(99,179,237,0.03)1px,transparent 1px);background-size:36px 36px;}
.hdr{position:fixed;top:0;left:0;right:0;z-index:100;height:56px;padding:0 14px;display:flex;align-items:center;justify-content:space-between;border-bottom:1px solid var(--border);background:rgba(10,14,26,0.96);backdrop-filter:blur(20px);-webkit-backdrop-filter:blur(20px);}
.logo{display:flex;align-items:center;gap:8px;}
.logo-m{width:27px;height:27px;border-radius:7px;background:linear-gradient(135deg,var(--accent2),var(--accent));display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:900;color:#fff;font-family:var(--sans);}
.logo-n{font-size:13px;font-weight:700;font-family:var(--sans);}
.logo-s{font-size:9px;color:var(--accent2);letter-spacing:.1em;font-family:var(--sans);}
.tabs{display:flex;gap:2px;}
.tab{padding:5px 9px;border-radius:6px;border:none;cursor:pointer;font-size:11px;font-family:var(--sans);background:transparent;color:var(--muted);transition:.2s;}
.tab.on{background:rgba(99,179,237,.2);color:var(--accent2);}
.main{position:relative;z-index:1;max-width:680px;margin:0 auto;padding:66px 13px 40px;}
.card{background:var(--surface);border:1px solid var(--border);border-radius:11px;padding:14px;}
.btn{width:100%;padding:12px;border-radius:9px;border:none;font-family:var(--sans);font-size:13px;font-weight:700;cursor:pointer;transition:.2s;display:flex;align-items:center;justify-content:center;gap:6px;}
.btn-p{background:linear-gradient(135deg,var(--accent),#3182ce);color:#fff;box-shadow:0 4px 14px rgba(66,153,225,.3);}
.btn-p:active{transform:scale(.98);}
.btn-g{background:rgba(99,179,237,.08);color:var(--accent2);border:1px solid rgba(99,179,237,.2);}
.btn-o{background:transparent;border:1px solid var(--border);color:var(--muted);}
.btn-x{background:#000;color:#fff;border:none;}
.btn-note{background:#41C9B4;color:#fff;border:none;}
.badge{display:inline-flex;align-items:center;gap:3px;background:rgba(0,0,0,.35);border-radius:5px;padding:2px 7px;font-size:10px;font-family:var(--sans);}
.lbl{font-size:9px;color:var(--accent2);margin-bottom:3px;font-family:var(--sans);letter-spacing:.05em;text-transform:uppercase;}
.stocks-box{border:1px solid var(--border);border-radius:10px;overflow:hidden;margin-bottom:14px;}
.s-hd{background:rgba(99,179,237,.1);padding:8px 12px;font-size:10px;font-weight:700;color:var(--accent2);font-family:var(--sans);}
.s-row{padding:11px 12px;border-top:1px solid rgba(99,179,237,.08);display:flex;align-items:flex-start;justify-content:space-between;gap:10px;}
.pred-box{flex-shrink:0;border-radius:7px;padding:5px 9px;text-align:center;min-width:46px;}
.pred-arr{font-size:16px;font-weight:900;display:block;}
.pred-lbl{font-size:9px;font-weight:700;font-family:var(--sans);}
.ex-wrap{margin-top:18px;}
.ex-hd{font-size:11px;font-weight:700;color:var(--accent2);font-family:var(--sans);margin-bottom:9px;letter-spacing:.05em;}
.ex-block{background:rgba(0,0,0,.3);border:1px solid var(--border);border-radius:8px;padding:11px;margin-bottom:8px;}
.ex-lbl{font-size:9px;color:var(--muted);font-family:var(--sans);margin-bottom:5px;}
.ex-txt{font-size:11px;color:#a0aec0;line-height:1.7;font-family:var(--sans);white-space:pre-wrap;word-break:break-word;max-height:100px;overflow:hidden;}
.cp-btn{margin-top:7px;width:100%;padding:7px;border-radius:7px;border:1px solid var(--border);background:rgba(255,255,255,.04);color:var(--text);font-size:11px;font-family:var(--sans);cursor:pointer;transition:.2s;}
.cp-btn.ok{background:rgba(34,197,94,.1);border-color:rgba(34,197,94,.3);color:var(--up);}
.aff-lbl{font-size:11px;font-family:var(--sans);color:var(--muted);margin-bottom:4px;display:block;}
.aff-in{width:100%;padding:9px 11px;background:rgba(255,255,255,.04);border:1px solid var(--border);border-radius:8px;color:var(--text);font-size:12px;font-family:var(--sans);outline:none;margin-bottom:7px;}
.aff-in:focus{border-color:var(--accent);}
.back-btn{display:inline-flex;align-items:center;gap:5px;background:transparent;border:1px solid var(--border);border-radius:7px;padding:5px 11px;color:var(--muted);font-size:11px;cursor:pointer;margin-bottom:14px;font-family:var(--sans);}
.empty{text-align:center;color:#4a5568;padding:40px 0;font-family:var(--sans);font-size:13px;}
.hidden{display:none!important;}
.mb8{margin-bottom:8px;}.mb12{margin-bottom:12px;}.mb14{margin-bottom:14px;}

/* Author comment selector */
.author-box{background:rgba(250,204,21,.06);border:1px solid rgba(250,204,21,.2);border-radius:10px;padding:13px;margin-bottom:12px;}
.author-title{font-size:11px;font-weight:700;color:#f59e0b;font-family:var(–sans);margin-bottom:8px;}
.author-opt{background:rgba(0,0,0,.3);border:1px solid rgba(250,204,21,.15);border-radius:8px;padding:10px 12px;margin-bottom:6px;cursor:pointer;transition:.2s;}
.author-opt:last-child{margin-bottom:0;}
.author-opt.sel{background:rgba(250,204,21,.1);border-color:rgba(250,204,21,.4);}
.author-opt-txt{font-size:12px;line-height:1.7;color:#e2e8f0;}
.author-opt-tag{font-size:9px;color:#f59e0b;font-family:var(–sans);margin-bottom:3px;}

/* Status bar */
.stat-bar{background:rgba(99,179,237,.06);border:1px solid rgba(99,179,237,.12);border-radius:8px;padding:9px 12px;margin-bottom:12px;display:flex;justify-content:space-between;font-family:var(–sans);}
.stat-item{font-size:9px;color:var(–muted);}
.stat-val{font-size:11px;font-weight:700;color:var(–accent2);margin-top:1px;}
.stat-warn{color:var(–flat);}

/* Prediction tracker */
.track-row{display:flex;align-items:center;justify-content:space-between;padding:8px 0;border-bottom:1px solid rgba(99,179,237,.07);font-family:var(–sans);}
.track-row:last-child{border-bottom:none;}
.track-name{font-size:12px;font-weight:700;}
.track-pred{font-size:10px;margin-top:1px;color:var(–muted);}
.track-result{font-size:11px;font-weight:700;padding:3px 8px;border-radius:5px;}
.track-pending{background:rgba(113,128,150,.15);color:var(–muted);}
.track-hit{background:rgba(34,197,94,.15);color:var(–up);}
.track-miss{background:rgba(239,68,68,.15);color:var(–down);}

/* How-to */
.how{background:rgba(99,179,237,.06);border:1px solid rgba(99,179,237,.18);border-radius:10px;padding:12px;margin-bottom:12px;}
.how-step{display:flex;align-items:flex-start;gap:9px;margin-bottom:7px;}
.how-step:last-child{margin-bottom:0;}
.step-n{width:19px;height:19px;border-radius:50%;background:var(–accent);color:#fff;font-size:10px;font-weight:700;font-family:var(–sans);display:flex;align-items:center;justify-content:center;flex-shrink:0;margin-top:1px;}
.step-t{font-size:11px;color:#a0aec0;line-height:1.6;font-family:var(–sans);}
.step-t strong{color:var(–text);}

/* Free/paid split preview */
.split-box{border:1px solid var(–border);border-radius:10px;overflow:hidden;margin-bottom:14px;}
.split-free{background:rgba(34,197,94,.05);border-bottom:2px dashed rgba(34,197,94,.3);padding:12px;}
.split-paid{background:rgba(250,204,21,.04);padding:12px;}
.split-tag{font-size:9px;font-weight:700;font-family:var(–sans);letter-spacing:.08em;margin-bottom:5px;}
</style>

</head>
<body>
<header class="hdr">
  <div class="logo">
    <div class="logo-m">株</div>
    <div><div class="logo-n">MarketIntel</div><div class="logo-s">AI FINANCIAL NEWS</div></div>
  </div>
  <div class="tabs">
    <button class="tab on" onclick="goTab('new',this)">新着</button>
    <button class="tab" onclick="goTab('pub',this)">公開済み</button>
    <button class="tab" onclick="goTab('track',this)">予測</button>
    <button class="tab" onclick="goTab('cfg',this)">設定</button>
  </div>
</header>

<main class="main">

<!-- ===== NEW TAB ===== -->

<div id="tNew">
  <div id="vHome">
    <div class="stat-bar">
      <div class="stat-item">最終生成<div class="stat-val" id="lastGenT">未生成</div></div>
      <div class="stat-item" style="text-align:center">公開済み<div class="stat-val" id="pubCnt">0件</div></div>
      <div class="stat-item" style="text-align:right">次回推奨<div class="stat-val" id="nextGenT">今すぐ ✅</div></div>
    </div>

```
<div class="how mb14">
  <div style="font-size:11px;font-weight:700;color:var(--accent2);font-family:var(--sans);margin-bottom:9px;">📋 使い方</div>
  <div class="how-step"><div class="step-n">1</div><div class="step-t">「記事を生成する」→ プロンプトをコピー</div></div>
  <div class="how-step"><div class="step-n">2</div><div class="step-t">Claude.aiアプリに貼り付けて送信</div></div>
  <div class="how-step"><div class="step-n">3</div><div class="step-t">出力されたJSONをコピー →「テキストを貼り付け」</div></div>
  <div class="how-step"><div class="step-n">4</div><div class="step-t"><strong>「今日の一言」を選ぶ</strong> → 記事を選んで公開</div></div>
</div>

<button class="btn btn-p mb8" onclick="onGenerate()" style="font-size:14px;padding:14px;">⚡ 記事を生成する</button>

<div id="promptBox" class="hidden mb8">
  <div style="font-size:11px;font-weight:700;color:var(--accent2);font-family:var(--sans);margin-bottom:5px;">📋 プロンプト</div>
  <textarea id="promptText" readonly style="width:100%;height:130px;background:rgba(0,0,0,.4);border:1px solid var(--border);border-radius:8px;color:#a0aec0;font-size:11px;font-family:var(--sans);padding:9px;line-height:1.6;resize:none;-webkit-user-select:text;user-select:text;"></textarea>
  <div style="display:flex;gap:7px;margin-top:7px;">
    <button class="btn btn-p" id="cpBtn" onclick="copyPrompt()" style="flex:1;padding:10px;font-size:12px;">📋 コピー</button>
    <a href="https://claude.ai" target="_blank" class="btn btn-g" style="flex:1;padding:10px;font-size:12px;text-decoration:none;display:flex;align-items:center;justify-content:center;">🤖 Claudeを開く</a>
  </div>
</div>

<div style="display:flex;gap:7px;margin-bottom:8px;">
  <button class="btn btn-g" onclick="document.getElementById('fileIn').click()" style="flex:1;padding:10px;font-size:12px;">📥 ファイルから</button>
  <button class="btn btn-g" onclick="showPaste()" style="flex:1;padding:10px;font-size:12px;">📋 テキストを貼り付け</button>
</div>
<input type="file" id="fileIn" accept=".json" class="hidden" onchange="loadFile(event)">

<div id="pasteBox" class="hidden mb8">
  <div style="font-size:11px;font-weight:700;color:var(--accent2);font-family:var(--sans);margin-bottom:5px;">📋 JSONをここに貼り付け</div>
  <textarea id="pasteText" style="width:100%;height:110px;background:rgba(0,0,0,.4);border:1px solid var(--border);border-radius:8px;color:#a0aec0;font-size:11px;font-family:var(--sans);padding:9px;line-height:1.6;resize:none;" placeholder='{"articles":[...]} の形式で貼り付けてください'></textarea>
  <div style="display:flex;gap:7px;margin-top:7px;">
    <button class="btn btn-o" onclick="hidePaste()" style="flex:1;padding:9px;font-size:12px;">キャンセル</button>
    <button class="btn btn-p" onclick="loadPaste()" style="flex:2;padding:9px;font-size:12px;">✅ 読み込む</button>
  </div>
</div>

<div id="homeMsg" class="hidden" style="margin-top:10px;background:rgba(34,197,94,.08);border:1px solid rgba(34,197,94,.25);border-radius:8px;padding:10px;font-size:11px;color:#68d391;font-family:var(--sans);line-height:1.7;"></div>
<div id="homeErr" class="hidden" style="margin-top:10px;background:rgba(239,68,68,.08);border:1px solid rgba(239,68,68,.25);border-radius:8px;padding:10px;font-size:11px;color:#fc8181;font-family:var(--sans);line-height:1.7;"></div>
```

  </div>

  <!-- Author comment selector -->

  <div id="vAuthor" class="hidden">
    <h2 style="font-size:15px;font-weight:700;font-family:var(--sans);margin-bottom:4px;">今日の一言を選ぶ</h2>
    <p style="font-size:11px;color:var(--muted);margin-bottom:12px;">AIが3パターン生成しました。最も「あなたらしい」一言を選んでください。記事冒頭とX投稿に自動挿入されます。</p>
    <div id="authorOpts"></div>
    <div style="display:flex;gap:7px;margin-top:8px;">
      <button class="btn btn-o" style="flex:1;padding:10px;" onclick="skipAuthor()">スキップ</button>
      <button class="btn btn-p" id="authorOkBtn" style="flex:2;padding:10px;" onclick="confirmAuthor()" disabled>この一言で進む →</button>
    </div>
  </div>

  <!-- Article select -->

  <div id="vSelect" class="hidden">
    <h2 style="font-size:15px;font-weight:700;font-family:var(--sans);margin-bottom:4px;">記事を選択</h2>
    <p style="font-size:11px;color:var(--muted);margin-bottom:12px;">公開する記事を1件選んでください</p>
    <div id="candList"></div>
    <div style="display:flex;gap:7px;margin-top:6px;">
      <button class="btn btn-o" style="flex:1;padding:10px;" onclick="showHome()">戻る</button>
      <button class="btn btn-p" id="pubBtn" style="flex:2;padding:10px;" onclick="doPublish()" disabled>この記事を公開する</button>
    </div>
  </div>

  <!-- Article detail -->

  <div id="vArticle" class="hidden">
    <button class="back-btn" onclick="backArt()">← 戻る</button>
    <div id="artBody"></div>
  </div>
</div>

<!-- ===== PUB TAB ===== -->

<div id="tPub" class="hidden">
  <h2 style="font-size:15px;font-weight:700;font-family:var(--sans);margin-bottom:12px;">公開済み記事</h2>
  <div id="pubList"></div>
  <div id="vArtPub" class="hidden">
    <button class="back-btn" onclick="backPub()">← 一覧へ</button>
    <div id="artBodyPub"></div>
  </div>
</div>

<!-- ===== PREDICTION TRACKER TAB ===== -->

<div id="tTrack" class="hidden">
  <h2 style="font-size:15px;font-weight:700;font-family:var(--sans);margin-bottom:6px;">📊 予測的中率トラッキング</h2>
  <p style="font-size:11px;color:var(--muted);font-family:var(--sans);margin-bottom:14px;">Xで信頼を積む最強の武器。予測結果を記録して実績を公開しましょう。</p>
  <div class="card mb12" id="trackSummary">
    <div style="display:flex;justify-content:space-around;text-align:center;font-family:var(--sans);">
      <div><div style="font-size:22px;font-weight:900;color:var(--up)" id="trackHit">0</div><div style="font-size:10px;color:var(--muted)">的中</div></div>
      <div><div style="font-size:22px;font-weight:900;color:var(--down)" id="trackMiss">0</div><div style="font-size:10px;color:var(--muted)">外れ</div></div>
      <div><div style="font-size:22px;font-weight:900;color:var(--flat)" id="trackPend">0</div><div style="font-size:10px;color:var(--muted)">判定待ち</div></div>
      <div><div style="font-size:22px;font-weight:900;color:var(--accent2)" id="trackRate">-%</div><div style="font-size:10px;color:var(--muted)">的中率</div></div>
    </div>
  </div>
  <div id="trackList"></div>
  <button class="btn btn-g mt8" style="margin-top:8px;padding:10px;font-size:12px;" onclick="genTrackPost()">🐦 的中率をXに投稿する</button>
  <div id="trackPost" class="hidden" style="margin-top:10px;"></div>
</div>

<!-- ===== SETTINGS TAB ===== -->

<div id="tCfg" class="hidden">
  <h2 style="font-size:15px;font-weight:700;font-family:var(--sans);margin-bottom:14px;">設定</h2>

  <div class="card mb12">
    <div class="lbl" style="margin-bottom:9px;">💰 アフィリエイトリンク</div>
    <p style="font-size:10px;color:var(--muted);font-family:var(--sans);margin-bottom:10px;line-height:1.7;">記事末尾に自動挿入。クリック数も計測されます。</p>
    <label class="aff-lbl">SBI証券</label><input class="aff-in" id="aSBI" placeholder="https://accesstrade.net/...">
    <label class="aff-lbl">楽天証券</label><input class="aff-in" id="aRak" placeholder="https://...">
    <label class="aff-lbl">GMOクリック証券</label><input class="aff-in" id="aGMO" placeholder="https://...">
    <label class="aff-lbl">FX口座（任意）</label><input class="aff-in" id="aFX" placeholder="https://...">
    <button class="btn btn-p" style="padding:10px;" onclick="saveAff()">💾 保存する</button>
  </div>

  <div class="card mb12">
    <div class="lbl" style="margin-bottom:9px;">📊 クリック計測</div>
    <div id="clickStats" style="font-size:11px;font-family:var(--sans);color:var(--muted);line-height:2;"></div>
    <button class="btn btn-o" style="padding:8px;font-size:11px;margin-top:8px;" onclick="resetClicks()">リセット</button>
  </div>

  <div class="card mb12">
    <div class="lbl" style="margin-bottom:9px;">⏱️ 更新頻度</div>
    <select id="genInv" style="width:100%;padding:9px;background:rgba(255,255,255,.04);border:1px solid var(--border);border-radius:8px;color:var(--text);font-size:12px;font-family:var(--sans);outline:none;margin-bottom:8px;">
      <option value="12">12時間ごと</option>
      <option value="24" selected>24時間ごと（推奨）</option>
      <option value="48">2日ごと</option>
    </select>
    <button class="btn btn-p" style="padding:10px;" onclick="saveInv()">💾 保存する</button>
  </div>

  <div class="card mb12">
    <div class="lbl" style="margin-bottom:9px;">🏷️ noteマガジンURL</div>
    <p style="font-size:10px;color:var(--muted);font-family:var(--sans);margin-bottom:8px;line-height:1.7;">有料マガジンのURLを設定するとnote CTAに自動挿入されます</p>
    <input class="aff-in" id="noteUrl" placeholder="https://note.com/あなたのID/m/xxx" style="margin-bottom:8px;">
    <button class="btn btn-p" style="padding:10px;" onclick="saveNote()">💾 保存する</button>
  </div>

  <div class="card mb12">
    <div class="lbl" style="margin-bottom:8px;">📱 ホーム画面に追加</div>
    <p style="font-size:11px;color:var(--muted);font-family:var(--sans);line-height:1.8;">Safari → 共有ボタン（□↑）→「ホーム画面に追加」</p>
  </div>

  <div class="card">
    <div class="lbl" style="margin-bottom:9px;">🗂️ データ管理</div>
    <button class="btn btn-o" style="padding:9px;font-size:12px;" onclick="clearAll()">公開済み記事を全件削除</button>
  </div>
</div>

</main>

<script>
const DB={g:k=>{try{return JSON.parse(localStorage.getItem(k));}catch{return null;}},s:(k,v)=>{try{localStorage.setItem(k,JSON.stringify(v));}catch{}}};

let S={
  pub:DB.g('mi_pub')||[],
  aff:DB.g('mi_aff')||{sbi:'',rak:'',gmo:'',fx:''},
  clicks:DB.g('mi_clicks')||{sbi:0,rak:0,gmo:0,fx:0},
  inv:DB.g('mi_inv')||24,
  lastGen:DB.g('mi_lastgen')||null,
  noteUrl:DB.g('mi_noteurl')||'',
  cands:[],selIdx:null,curArt:null,backFrom:'select',
  authorOpts:[],selAuthor:null,
  preds:DB.g('mi_preds')||[],
};

window.onload=()=>{loadAffUI();updateStatus();renderClickStats();document.getElementById('genInv').value=S.inv;document.getElementById('noteUrl').value=S.noteUrl;};

// ── Tab ──────────────────────────────────────────────────
function goTab(t,el){
  document.querySelectorAll('.tab').forEach(b=>b.classList.remove('on'));
  el.classList.add('on');
  ['tNew','tPub','tTrack','tCfg'].forEach(id=>document.getElementById(id).classList.add('hidden'));
  const map={new:'tNew',pub:'tPub',track:'tTrack',cfg:'tCfg'};
  document.getElementById(map[t]).classList.remove('hidden');
  if(t==='pub')renderPubList();
  if(t==='track')renderTrack();
}

function showHome(){['vSelect','vArticle','vAuthor'].forEach(id=>document.getElementById(id).classList.add('hidden'));document.getElementById('vHome').classList.remove('hidden');}
function showSelect(){['vHome','vArticle','vAuthor'].forEach(id=>document.getElementById(id).classList.add('hidden'));document.getElementById('vSelect').classList.remove('hidden');}
function showAuthor(){['vHome','vSelect','vArticle'].forEach(id=>document.getElementById(id).classList.add('hidden'));document.getElementById('vAuthor').classList.remove('hidden');}

// ── Status ────────────────────────────────────────────────
function updateStatus(){
  document.getElementById('pubCnt').textContent=S.pub.length+'件';
  if(S.lastGen){
    const d=new Date(S.lastGen);
    document.getElementById('lastGenT').textContent=d.toLocaleString('ja-JP',{month:'numeric',day:'numeric',hour:'2-digit',minute:'2-digit'});
    const next=new Date(d.getTime()+S.inv*3600000);
    const now=new Date();
    if(now>=next){document.getElementById('nextGenT').textContent='今すぐ ✅';document.getElementById('nextGenT').className='stat-val';}
    else{const h=Math.ceil((next-now)/3600000);document.getElementById('nextGenT').textContent=h+'時間後';document.getElementById('nextGenT').className='stat-val stat-warn';}
  }
}

// ── Prompt generation ─────────────────────────────────────
function onGenerate(){
  const avoid=S.pub.map(a=>a.title).slice(0,5);
  const avoidNote=avoid.length?'\n既出記事（除外）: '+avoid.join(' / '):'';

  const p='あなたは個人投資家向けの人気金融ブロガーです。「読まれる・シェアされる・他にはない」記事を書くのが得意です。\n\n株価に影響しそうな最新の金融ニュースを3つピックアップし、以下のスタイルで記事を書いてください。\n\n【リサーチのルール】\n・各トピックについて必ず異なるメディア（日経・Bloomberg・Reuters・Yahoo!ファイナンス・東洋経済・会社四季報など）の記事を最低3つ参照すること\n・各メディアの論調の違い・温度差を記事の中で明示すること\n・複数ソースを比較した上での独自分析・見解を必ず加えること\n・株価・出来高・騰落率などの具体的な数字を入れること。確認できた数字には（○○報道）と出典を明記し、推計・概算の場合は「〜と推定される」と注釈を入れること\n・そのニュースから3手先に何が起きるかの連鎖予測を文章として自然に組み込むこと\n\n【文体・スタイルのルール】\n・タイトルは「数字」「問い」「驚き」「逆説」で始める\n・冒頭1〜2文で読者を引き込むフックを入れる（毎記事で異なる表現を使うこと）\n・「だからどうなる？」「投資家として何をすべきか？」まで踏み込む\n・専門用語は必ずかみ砕いて説明する\n・筆者の見解・予測を強めに断言する\n・読者への問いかけを最低1回入れる\n・締めは「次に注目すべきポイント」で終わる\n\n【銘柄提示のルール】\n・大型株（時価総額1兆円超）を1社以上\n・中型株（時価総額1000億〜1兆円）を1社以上\n・小型株（株価1000円未満の隠れ恩恵株）を1社以上。ニュースとの直接的な因果関係を「〜だからこの会社の〜が増える」の形で説明すること\n・各銘柄に上昇/下降/横ばいの予測と50字以内の根拠を付ける\n\n【筆者コメントのルール】\n・各記事に「筆者の今日の一言」として異なるトーンの3パターンを生成すること\n・パターン1: 強気・煽り系（「これは乗り遅れたら一生後悔する」「今すぐ口座を開け」系）\n・パターン2: 中立・分析系（「両面を見て自分で判断する」「データが示す通り」系）\n・パターン3: 警戒・逆張り系（「みんなが強気のときこそ疑え」「ここに落とし穴がある」系）\n\n【X投稿文のルール】\n・各記事にX専用の投稿文を別途作成\n・冒頭は数字・驚き・問い・対立構造のいずれかで始める\n・銘柄名・証券コード・予測方向（↑↓→）を必ず含める\n・ハッシュタグは #日本株 #株式投資 #小型株 #個人投資家 を末尾に\n・280文字以内\n\n【記事カテゴリ】以下から1つ割り当て: 金融政策/半導体/エネルギー/海運/アクティビスト/決算/マクロ経済/為替/不動産/防衛・宇宙\n\n【その他条件】\n・記事は全て日本語、800〜1000字\n・過去に記事にした情報以外を選ぶ\n・3件全て一度に出力（選択待ち不要）'+avoidNote+'\n\n以下のJSON形式のみで出力（説明文不要・JSONだけ）:\n```json\n{"articles":[{"id":"1","title":"タイトル","summary":"概要100字","content":"本文800〜1000字","category":"カテゴリ","x_post":"X投稿文280字以内","author_comments":["強気系一言","中立系一言","警戒系一言"],"large_name":"大型株名","large_ticker":"7203","large_pred":"上昇","large_reason":"根拠50字","mid_name":"中型株名","mid_ticker":"6758","mid_pred":"横ばい","mid_reason":"根拠50字","small_name":"小型株名","small_ticker":"1234","small_pred":"上昇","small_reason":"因果関係と根拠50字","sources":["URL1","URL2","URL3"]},{"id":"2",...},{"id":"3",...}]}\n```';

  document.getElementById('promptText').value=p;
  document.getElementById('promptBox').classList.remove('hidden');
  S.lastGen=new Date().toISOString();DB.s('mi_lastgen',S.lastGen);updateStatus();
  setTimeout(()=>document.getElementById('promptBox').scrollIntoView({behavior:'smooth',block:'start'}),100);
}

function copyPrompt(){
  const ta=document.getElementById('promptText');ta.select();ta.setSelectionRange(0,99999);
  try{document.execCommand('copy');}catch(e){}
  try{navigator.clipboard.writeText(ta.value).catch(()=>{});}catch(e){}
  const b=document.getElementById('cpBtn');b.textContent='✅ コピーしました';
  setTimeout(()=>{b.textContent='📋 コピー';},2000);
}

// ── Paste / File ──────────────────────────────────────────
function showPaste(){document.getElementById('pasteBox').classList.remove('hidden');document.getElementById('pasteText').value='';setTimeout(()=>document.getElementById('pasteText').focus(),100);}
function hidePaste(){document.getElementById('pasteBox').classList.add('hidden');}

function parseArts(d){
  return d.articles.map(a=>({
    id:a.id,title:a.title,summary:a.summary,content:a.content,
    category:a.category||'',xPost:a.x_post||'',
    authorComments:Array.isArray(a.author_comments)?a.author_comments:[],
    chosenComment:'',
    relatedStocks:{
      large:{name:a.large_name,ticker:a.large_ticker,prediction:a.large_pred,reason:a.large_reason},
      mid:{name:a.mid_name,ticker:a.mid_ticker,prediction:a.mid_pred,reason:a.mid_reason},
      small:{name:a.small_name,ticker:a.small_ticker,prediction:a.small_pred,reason:a.small_reason},
    },
    sources:Array.isArray(a.sources)?a.sources.filter(Boolean):[a.source].filter(Boolean),
  }));
}

function loadPaste(){
  const raw=document.getElementById('pasteText').value.trim();
  if(!raw){showErr('テキストが空です');return;}
  try{
    const m=raw.match(/```(?:json)?\s*([\s\S]*?)```/)||raw.match(/(\{[\s\S]*\})/);
    const js=m?(m[1]||m[0]):raw;
    const d=JSON.parse(js.trim());
    if(!d.articles?.length)throw new Error('articles が見つかりません');
    S.cands=parseArts(d);S.selIdx=null;hidePaste();
    document.getElementById('homeMsg').classList.add('hidden');
    renderCands();showSelect();
  }catch(e){showErr('読み込み失敗: '+e.message);}
}

function loadFile(e){
  const f=e.target.files[0];if(!f)return;
  const r=new FileReader();
  r.onload=ev=>{
    try{const d=JSON.parse(ev.target.result);if(!d.articles?.length)throw new Error('articles が見つかりません');S.cands=parseArts(d);S.selIdx=null;renderCands();showSelect();}
    catch(e){showErr('ファイル読み込み失敗: '+e.message);}
  };
  r.readAsText(f);e.target.value='';
}

// showAuthorStep removed - now triggered per-article after selection

function selAuthor(i){
  S.selAuthor=i;
  document.querySelectorAll('.author-opt').forEach((el,idx)=>el.classList.toggle('sel',idx===i));
  document.getElementById('authorOkBtn').disabled=false;
}

function confirmAuthor(){
  if(S.selAuthor===null||S.selIdx===null)return;
  const chosen=S.authorOpts[S.selAuthor]||'';
  S.cands[S.selIdx].chosenComment=chosen;
  finalPublish(S.cands[S.selIdx]);
}

function skipAuthor(){
  if(S.selIdx===null){renderCands();showSelect();return;}
  S.cands[S.selIdx].chosenComment='';
  finalPublish(S.cands[S.selIdx]);
}

// ── Candidates ────────────────────────────────────────────
function renderCands(){
  const el=document.getElementById('candList');el.innerHTML='';
  S.cands.forEach((a,i)=>{
    const on=S.selIdx===i;
    const d=document.createElement('div');d.style.marginBottom='10px';
    d.innerHTML=`<div class="card" style="cursor:pointer;border-color:${on?'rgba(99,179,237,.5)':'var(--border)'};background:${on?'rgba(99,179,237,.07)':'var(--surface)'};" onclick="selCand(${i})">
      <div style="display:flex;gap:8px;">
        <div style="width:19px;height:19px;border-radius:50%;flex-shrink:0;background:${on?'var(--accent)':'rgba(99,179,237,.1)'};display:flex;align-items:center;justify-content:center;font-size:10px;color:#fff;font-weight:700;font-family:var(--sans)">${on?'✓':i+1}</div>
        <div style="flex:1">
          ${a.category?`<span style="display:inline-block;background:rgba(99,179,237,.15);border:1px solid rgba(99,179,237,.3);border-radius:4px;padding:1px 7px;font-size:9px;color:var(--accent2);font-family:var(--sans);margin-bottom:5px;">${a.category}</span>`:''}
          <div style="font-size:13px;font-weight:700;margin-bottom:4px;line-height:1.5">${a.title}</div>
          <div style="font-size:11px;color:var(--muted);line-height:1.6;margin-bottom:7px">${a.summary}</div>
          <div style="display:flex;gap:5px;flex-wrap:wrap">
            ${[a.relatedStocks.large,a.relatedStocks.mid,a.relatedStocks.small].filter(s=>s&&s.name).map(s=>`
              <span class="badge"><span style="color:#a0aec0">${s.name}</span><span style="color:${pc(s.prediction)};font-weight:700;margin-left:3px">${pi(s.prediction)}${s.prediction}</span></span>`).join('')}
          </div>
        </div>
      </div></div>`;
    el.appendChild(d);
  });
}

function selCand(i){S.selIdx=i;document.getElementById('pubBtn').disabled=false;renderCands();}

function doPublish(){
  if(S.selIdx===null)return;
  // Show author comment selector for the selected article
  const cand=S.cands[S.selIdx];
  if(cand.authorComments&&cand.authorComments.length>0){
    showAuthorForArticle(cand);
    return;
  }
  finalPublish(cand);
}

function showAuthorForArticle(cand){
  const labels=['🔥 強気・煽り系','📊 中立・分析系','⚠️ 警戒・逆張り系'];
  S.authorOpts=cand.authorComments;S.selAuthor=null;
  document.getElementById('authorOkBtn').disabled=true;
  document.getElementById('authorOpts').innerHTML=cand.authorComments.map((txt,i)=>`
    <div class="author-opt" id="aopt${i}" onclick="selAuthor(${i})">
      <div class="author-opt-tag">${labels[i]||'パターン'+(i+1)}</div>
      <div class="author-opt-txt">「${txt}」</div>
    </div>`).join('');
  // Update author screen title to show article title
  document.querySelector('#vAuthor h2').textContent='今日の一言を選ぶ';
  document.querySelector('#vAuthor p').textContent='「'+cand.title.slice(0,30)+'…」の記事に付ける一言を選んでください。';
  showAuthor();
}

function finalPublish(cand){
  const art={...cand,publishedAt:new Date().toLocaleDateString('ja-JP')};
  // Save chosen comment back to cand
  if(S.selIdx!==null)S.cands[S.selIdx].chosenComment=art.chosenComment;
  // Add predictions to tracker
  ['large','mid','small'].forEach(k=>{
    const s=art.relatedStocks[k];
    if(s&&s.name){
      S.preds.push({id:Date.now()+'_'+k,name:s.name,ticker:s.ticker,pred:s.prediction,reason:s.reason,artTitle:art.title,date:art.publishedAt,result:'pending'});
    }
  });
  DB.s('mi_preds',S.preds);
  S.pub.unshift(art);DB.s('mi_pub',S.pub);
  S.curArt=art;S.backFrom='select';
  document.getElementById('artBody').innerHTML=buildArtHTML(art);
  ['vHome','vSelect','vAuthor'].forEach(id=>document.getElementById(id).classList.add('hidden'));
  document.getElementById('vArticle').classList.remove('hidden');
  updateStatus();
}

function backArt(){
  document.getElementById('vArticle').classList.add('hidden');
  if(S.backFrom==='pub'){renderPubList();document.getElementById('tPub').classList.remove('hidden');}
  else showSelect();
}

// ── Published ─────────────────────────────────────────────
function renderPubList(){
  const pl=document.getElementById('pubList'),ap=document.getElementById('vArtPub');
  ap.classList.add('hidden');pl.classList.remove('hidden');
  if(!S.pub.length){pl.innerHTML='<div class="empty">まだ公開済み記事がありません</div>';return;}
  pl.innerHTML=S.pub.map((a,i)=>`
    <div class="card mb8" style="cursor:pointer" onclick="openPub(${i})">
      ${a.category?`<span style="display:inline-block;background:rgba(99,179,237,.1);border-radius:4px;padding:1px 7px;font-size:9px;color:var(--accent2);font-family:var(--sans);margin-bottom:4px;">${a.category}</span>`:''}
      <div style="font-size:13px;font-weight:700;margin-bottom:3px">${a.title}</div>
      <div style="font-size:11px;color:var(--muted);line-height:1.5;margin-bottom:3px">${a.summary}</div>
      <div style="font-size:9px;color:#2d3748;font-family:var(--sans)">公開日: ${a.publishedAt||'–'}</div>
    </div>`).join('');
}

function openPub(i){
  S.curArt=S.pub[i];S.backFrom='pub';
  document.getElementById('pubList').classList.add('hidden');
  document.getElementById('artBodyPub').innerHTML=buildArtHTML(S.curArt);
  document.getElementById('vArtPub').classList.remove('hidden');
}
function backPub(){document.getElementById('vArtPub').classList.add('hidden');renderPubList();}

// ── Prediction tracker ────────────────────────────────────
function renderTrack(){
  const hits=S.preds.filter(p=>p.result==='hit').length;
  const misses=S.preds.filter(p=>p.result==='miss').length;
  const pend=S.preds.filter(p=>p.result==='pending').length;
  const total=hits+misses;
  document.getElementById('trackHit').textContent=hits;
  document.getElementById('trackMiss').textContent=misses;
  document.getElementById('trackPend').textContent=pend;
  document.getElementById('trackRate').textContent=total>0?Math.round(hits/total*100)+'%':'-%';

  const el=document.getElementById('trackList');
  if(!S.preds.length){el.innerHTML='<div class="empty">記事を公開すると予測が自動登録されます</div>';return;}
  el.innerHTML=S.preds.slice().reverse().map((p,i)=>{
    const ri=S.preds.length-1-i;
    return `<div class="track-row">
      <div>
        <div class="track-name">${p.name} <span style="font-size:10px;color:var(--muted)">${p.ticker}</span></div>
        <div class="track-pred">${pi(p.pred)}${p.pred} — ${p.date}</div>
      </div>
      <div style="display:flex;gap:5px;align-items:center">
        ${p.result==='pending'?`
          <button onclick="setPred(${ri},'hit')" style="padding:4px 9px;border-radius:5px;border:none;background:rgba(34,197,94,.15);color:var(--up);font-size:11px;cursor:pointer;font-family:var(--sans);">✓ 的中</button>
          <button onclick="setPred(${ri},'miss')" style="padding:4px 9px;border-radius:5px;border:none;background:rgba(239,68,68,.15);color:var(--down);font-size:11px;cursor:pointer;font-family:var(--sans);">✗ 外れ</button>
        `:`<span class="track-result ${p.result==='hit'?'track-hit':'track-miss'}">${p.result==='hit'?'✓ 的中':'✗ 外れ'}</span>`}
      </div>
    </div>`;
  }).join('');
}

function setPred(i,result){S.preds[i].result=result;DB.s('mi_preds',S.preds);renderTrack();}

function genTrackPost(){
  const hits=S.preds.filter(p=>p.result==='hit').length;
  const total=S.preds.filter(p=>p.result!=='pending').length;
  if(total===0){alert('まだ結果が記録されていません');return;}
  const rate=Math.round(hits/total*100);
  const recent=S.preds.filter(p=>p.result==='hit').slice(-3).map(p=>`✅ ${p.name}(${p.ticker}) ${pi(p.pred)}${p.pred}`).join('\n');
  const txt=`【AI金融アナリストの予測的中率】\n\n直近${total}件の予測: ${rate}%的中\n\n最近の的中予測:\n${recent}\n\n毎日の分析を無料配信中。フォローして投資の精度を上げてください。\n\n#日本株 #株式投資 #個人投資家 #小型株`;
  const el=document.getElementById('trackPost');
  el.innerHTML=`<div class="ex-block"><div class="ex-lbl">🐦 X投稿文</div><div class="ex-txt" id="tpTxt">${txt}</div><div style="display:flex;gap:6px;margin-top:7px;"><button class="cp-btn" style="flex:1;" onclick="doCopy('tpTxt',this)">📋 コピー</button><button class="btn btn-x" style="flex:1;padding:7px;font-size:11px;border-radius:7px;" onclick="openX('tpTxt')">𝕏 投稿する</button></div></div>`;
  el.classList.remove('hidden');
}

// ── Article HTML builder ──────────────────────────────────
function buildArtHTML(a){
  const stocks=[{l:'大型株',s:a.relatedStocks.large},{l:'中型株',s:a.relatedStocks.mid},{l:'小型株（隠れ恩恵株）',s:a.relatedStocks.small}].filter(x=>x.s&&x.s.name);
  const xTxt=buildX(a);
  const freeNote=buildFreeNote(a);
  const paidNote=buildPaidNote(a);
  const affHtml=buildAffHtml(a);

  return `
    ${a.category?`<div style="display:inline-block;background:rgba(99,179,237,.15);border:1px solid rgba(99,179,237,.3);border-radius:5px;padding:2px 9px;font-size:10px;color:var(--accent2);font-family:var(--sans);margin-bottom:8px;">${a.category}</div>`:''}
    <h1 style="font-size:18px;font-weight:900;line-height:1.55;margin-bottom:10px">${a.title}</h1>

    ${a.chosenComment?`<div style="background:rgba(250,204,21,.08);border-left:3px solid #f59e0b;padding:10px 13px;margin-bottom:14px;border-radius:0 8px 8px 0;"><div style="font-size:9px;color:#f59e0b;font-family:var(--sans);margin-bottom:3px;">✍️ 筆者の一言</div><div style="font-size:12px;line-height:1.8;color:#fef3c7;font-style:italic;">「${a.chosenComment}」</div></div>`:''}

    <div class="card mb12" style="background:rgba(99,179,237,.05);border-color:rgba(99,179,237,.25)">
      <div class="lbl">概要</div>
      <div style="font-size:12px;line-height:1.8;color:#cbd5e0">${a.summary}</div>
    </div>
    <div style="font-size:13px;line-height:2.1;margin-bottom:18px;white-space:pre-line">${a.content}</div>

    <div class="stocks-box">
      <div class="s-hd">📊 関連銘柄・株価予測</div>
      ${stocks.map(({l,s})=>`
        <div class="s-row">
          <div>
            <div style="font-size:9px;color:var(--muted);margin-bottom:2px;font-family:var(--sans)">${l}</div>
            <div style="font-size:13px;font-weight:700;margin-bottom:2px">${s.name} <span style="font-size:10px;color:var(--muted)">${s.ticker}</span></div>
            <div style="font-size:10px;color:#a0aec0;line-height:1.6">${s.reason}</div>
          </div>
          <div class="pred-box" style="background:${pc(s.prediction)}20;border:1px solid ${pc(s.prediction)}40">
            <span class="pred-arr" style="color:${pc(s.prediction)}">${pi(s.prediction)}</span>
            <span class="pred-lbl" style="color:${pc(s.prediction)}">${s.prediction}</span>
          </div>
        </div>`).join('')}
    </div>

    ${a.sources?.length?`<div style="margin-bottom:16px"><div class="lbl" style="margin-bottom:4px">参照元（${a.sources.length}件）</div>${a.sources.map(s=>`<a href="${s}" target="_blank" style="display:block;font-size:11px;color:var(--accent2);text-decoration:none;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;margin-bottom:3px">${s}</a>`).join('')}</div>`:''}

    ${affHtml}

    <!-- Free/Paid split preview -->
    <div class="split-box mb12">
      <div class="split-free">
        <div class="split-tag" style="color:var(--up)">🆓 無料公開（X・note無料）</div>
        <div style="font-size:11px;color:#a0aec0;font-family:var(--sans);line-height:1.7">タイトル・概要・銘柄予測・筆者コメント</div>
      </div>
      <div class="split-paid">
        <div class="split-tag" style="color:var(--flat)">💎 有料マガジン限定（月額980円）</div>
        <div style="font-size:11px;color:#a0aec0;font-family:var(--sans);line-height:1.7">全文・小型株の詳細根拠・来週の注目銘柄・毎日30本</div>
      </div>
    </div>

    <div class="ex-wrap">
      <div class="ex-hd">📤 コンテンツ出力</div>

      <div class="ex-block">
        <div class="ex-lbl">🐦 X投稿文（筆者コメント入り・バズ仕様）</div>
        <div class="ex-txt" id="eX${a.id}">${buildX(a)}</div>
        <div style="display:flex;gap:6px;margin-top:7px;">
          <button class="cp-btn" style="flex:1;" onclick="doCopy('eX${a.id}',this)">📋 コピー</button>
          <button class="btn btn-x" style="flex:1;padding:7px;font-size:11px;border-radius:7px;" onclick="openX('eX${a.id}')">𝕏 投稿する</button>
        </div>
      </div>

      <div class="ex-block">
        <div class="ex-lbl">📝 note無料記事（集客用）</div>
        <div class="ex-txt" id="eFree${a.id}">${esc(freeNote)}</div>
        <button class="cp-btn" onclick="doCopy('eFree${a.id}',this)">📋 コピー</button>
      </div>

      <div class="ex-block">
        <div class="ex-lbl">💎 note有料記事（マガジン用・全文）</div>
        <div class="ex-txt" id="ePaid${a.id}">${esc(paidNote)}</div>
        <div style="display:flex;gap:6px;margin-top:7px;">
          <button class="cp-btn" style="flex:1;" onclick="doCopy('ePaid${a.id}',this)">📋 コピー</button>
          <button class="btn btn-note" style="flex:1;padding:7px;font-size:11px;border-radius:7px;" onclick="openNote()">note を開く</button>
        </div>
      </div>
    </div>`;
}

// ── Content builders ──────────────────────────────────────
function buildX(a){
  let base=a.xPost&&a.xPost.length>10?a.xPost:'';
  if(!base){
    const ls=a.relatedStocks.large,ss=a.relatedStocks.small;
    base=a.title.replace(/——.*$/,'')+'\n\n'+a.content.split('\n')[0].slice(0,60)+'…\n\n'+(ls&&ls.name?'📌 '+ls.name+'('+ls.ticker+') '+pi(ls.prediction)+ls.prediction:'')+(ss&&ss.name?'\n💎 '+ss.name+'('+ss.ticker+') '+pi(ss.prediction)+ss.prediction:'');
  }
  if(a.chosenComment)base='「'+a.chosenComment.slice(0,30)+'」\n\n'+base;
  if(!base.includes('#日本株'))base+='\n\n#日本株 #株式投資 #小型株 #個人投資家';
  return base.length>280?base.slice(0,276)+'...':base;
}

function buildFreeNote(a){
  const noteUrl=S.noteUrl||'https://note.com/';
  const ctaMap={'金融政策':'利上げ局面の投資戦略','半導体':'AI・半導体相場の深掘り分析','エネルギー':'原油・エネルギー相場の先読み','為替':'円安円高を先読みする分析','防衛・宇宙':'防衛・次世代エネルギーテーマ株分析'};
  const ctaTheme=ctaMap[a.category]||'最新の株式市場分析';
  const comment=a.chosenComment?`\n\n> ✍️ **筆者の一言**\n> 「${a.chosenComment}」\n`:'';
  const stocks=[{l:'大型株',s:a.relatedStocks.large},{l:'中型株',s:a.relatedStocks.mid},{l:'小型株',s:a.relatedStocks.small}].filter(x=>x.s&&x.s.name);
  const tbl=stocks.map(({l,s})=>`| ${l} | ${s.name} | ${s.ticker} | ${pi(s.prediction)}${s.prediction} |`).join('\n');
  return `# ${a.title}\n${comment}\n## 概要\n${a.summary}\n\n---\n\n## 関連銘柄・株価予測\n\n| 区分 | 銘柄 | コード | 予測 |\n|------|------|--------|------|\n${tbl}\n\n---\n\n> 💎 **全文・小型株の詳細根拠・毎日の分析は有料マガジンで**\n> ${ctaTheme}を毎日配信中 → [AI金融アナリスト通信](${noteUrl})\n> 月額980円 | いつでも解約可能\n\n---\n\n*本記事はAIによる分析を含みます。投資判断はご自身の責任で行ってください。*`;
}

function buildPaidNote(a){
  const noteUrl=S.noteUrl||'https://note.com/';
  const aff=buildAffMd(a);
  const comment=a.chosenComment?`\n\n> ✍️ **筆者の一言**\n> 「${a.chosenComment}」\n`:'';
  const stocks=[{l:'大型株',s:a.relatedStocks.large},{l:'中型株',s:a.relatedStocks.mid},{l:'小型株（隠れ恩恵株）',s:a.relatedStocks.small}].filter(x=>x.s&&x.s.name);
  const tbl=stocks.map(({l,s})=>`| ${l} | ${s.name} | ${s.ticker} | ${pi(s.prediction)}${s.prediction} | ${s.reason} |`).join('\n');
  return `# ${a.title}\n${comment}\n## 概要\n${a.summary}\n\n---\n\n${a.content}\n\n---\n\n## 関連銘柄・株価予測（詳細根拠付き）\n\n| 区分 | 銘柄 | コード | 予測 | 根拠 |\n|------|------|--------|------|------|\n${tbl}\n\n${a.sources?.length?'**参照元（'+a.sources.length+'件）:** '+a.sources.join(' / '):''}\n\n---\n${aff}\n> 💡 この記事が役に立ったら「スキ」をお願いします！\n> フォロー＆マガジン購読で毎日の分析をお届けします → [AI金融アナリスト通信](${noteUrl})\n\n*本記事はAIによる分析を含みます。投資判断はご自身の責任で行ってください。*`;
}

function buildAffMd(a){
  const af=S.aff;const ls=[];
  const ctxMap={'金融政策':'利上げ局面の今、まず口座を開設','半導体':'AI半導体銘柄を今すぐ買うなら','エネルギー':'原油・エネルギー株を手数料ゼロで','海運':'海運・高配当株への投資を始めるなら','為替':'円安を味方につけるFX口座','防衛・宇宙':'防衛テーマ株への投資を始めるなら'};
  const ctx=ctxMap[a.category]||'この記事の銘柄を手数料ゼロで買うなら';
  if(af.sbi)ls.push(`- [SBI証券 口座開設（無料）](${af.sbi}) — ${ctx}`);
  if(af.rak)ls.push(`- [楽天証券 口座開設（無料）](${af.rak}) — 楽天ポイントが貯まる`);
  if(af.gmo)ls.push(`- [GMOクリック証券（無料）](${af.gmo}) — 手数料が業界最安水準`);
  if(af.fx&&(a.category==='為替'||a.category==='マクロ経済'))ls.push(`- [FX口座開設](${af.fx}) — 為替変動を投資チャンスに`);
  return ls.length?`\n## 💹 おすすめ証券口座\n\n${ls.join('\n')}\n\n`:'';
}

function buildAffHtml(a){
  const af=S.aff;const ls=[];
  const ctxMap={'金融政策':'利上げ局面の今、まず口座を開設','半導体':'AI半導体銘柄を今すぐ買うなら','エネルギー':'原油・エネルギー株を手数料ゼロで','海運':'海運・高配当株への投資を始めるなら','為替':'円安を味方につけるFX口座','防衛・宇宙':'防衛テーマ株への投資を始めるなら'};
  const ctx=ctxMap[a.category]||'この記事の銘柄を手数料ゼロで買うなら';
  const t=(key,url,label,sub)=>`<a href="${url}" target="_blank" onclick="trackClick('${key}')" style="display:block;background:rgba(99,179,237,.05);border:1px solid rgba(99,179,237,.18);border-radius:8px;padding:9px 12px;margin-bottom:5px;text-decoration:none;color:var(--text);font-size:12px;font-family:var(--sans);"><span style="font-weight:700">${label}</span><span style="display:block;font-size:10px;color:var(--muted);margin-top:1px">${sub}</span></a>`;
  if(af.sbi)ls.push(t('sbi',af.sbi+'?utm_source=mi&utm_campaign=sbi_'+encodeURIComponent(a.category||''),'💹 SBI証券 口座開設（無料）',ctx));
  if(af.rak)ls.push(t('rak',af.rak+'?utm_source=mi&utm_campaign=rak','💹 楽天証券 口座開設（無料）','楽天ポイントが貯まる・初心者向け'));
  if(af.gmo)ls.push(t('gmo',af.gmo+'?utm_source=mi&utm_campaign=gmo','💹 GMOクリック証券（無料）','手数料が業界最安水準'));
  if(af.fx&&(a.category==='為替'||a.category==='マクロ経済'))ls.push(t('fx',af.fx+'?utm_source=mi&utm_campaign=fx','💹 FX口座開設','為替変動を投資チャンスに変える'));
  return ls.length?`<div style="margin-bottom:16px"><div class="lbl" style="margin-bottom:5px">💰 投資を始めるなら</div><div style="font-size:10px;color:var(--muted);font-family:var(--sans);margin-bottom:7px;">${ctx}</div>${ls.join('')}</div>`:'';
}

// ── Click tracking ────────────────────────────────────────
function trackClick(k){S.clicks[k]=(S.clicks[k]||0)+1;DB.s('mi_clicks',S.clicks);renderClickStats();}
function renderClickStats(){const c=S.clicks;document.getElementById('clickStats').innerHTML=[['SBI証券','sbi'],['楽天証券','rak'],['GMO','gmo'],['FX','fx']].map(([l,k])=>`${l}: <strong style="color:var(--accent2)">${c[k]||0}回</strong>`).join(' / ');}
function resetClicks(){if(!confirm('クリック数をリセットしますか？'))return;S.clicks={sbi:0,rak:0,gmo:0,fx:0};DB.s('mi_clicks',S.clicks);renderClickStats();}

// ── One-tap post ──────────────────────────────────────────
function openX(id){const t=encodeURIComponent(document.getElementById(id).innerText);window.open('https://x.com/intent/tweet?text='+t,'_blank');}
function openNote(){window.open(S.noteUrl||'https://note.com/','_blank');}

// ── Settings ─────────────────────────────────────────────
function saveAff(){S.aff={sbi:document.getElementById('aSBI').value.trim(),rak:document.getElementById('aRak').value.trim(),gmo:document.getElementById('aGMO').value.trim(),fx:document.getElementById('aFX').value.trim()};DB.s('mi_aff',S.aff);alert('保存しました ✓');}
function loadAffUI(){document.getElementById('aSBI').value=S.aff.sbi||'';document.getElementById('aRak').value=S.aff.rak||'';document.getElementById('aGMO').value=S.aff.gmo||'';document.getElementById('aFX').value=S.aff.fx||'';}
function saveInv(){S.inv=parseInt(document.getElementById('genInv').value);DB.s('mi_inv',S.inv);updateStatus();alert('保存しました ✓');}
function saveNote(){S.noteUrl=document.getElementById('noteUrl').value.trim();DB.s('mi_noteurl',S.noteUrl);alert('保存しました ✓');}
function clearAll(){if(!confirm('公開済み記事を全件削除しますか？'))return;S.pub=[];DB.s('mi_pub',[]);alert('削除しました');}

// ── Helpers ───────────────────────────────────────────────
function pc(p){return p==='上昇'?'#22c55e':p==='下降'?'#ef4444':'#f59e0b';}
function pi(p){return p==='上昇'?'↑':p==='下降'?'↓':'→';}
function esc(s){return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');}
function showErr(msg){const el=document.getElementById('homeErr');el.textContent='⚠️ '+msg;el.classList.remove('hidden');}
async function doCopy(id,btn){
  const t=document.getElementById(id).innerText;
  try{await navigator.clipboard.writeText(t);}catch{const ta=document.createElement('textarea');ta.value=t;ta.style.cssText='position:fixed;opacity:0';document.body.appendChild(ta);ta.select();document.execCommand('copy');document.body.removeChild(ta);}
  btn.textContent='✅ コピーしました';btn.classList.add('ok');
  setTimeout(()=>{btn.textContent='📋 コピー';btn.classList.remove('ok');},2000);
}
</script>

</body>
</html>
