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
:root {
  --bg: #0a0e1a;
  --surface: rgba(255,255,255,0.03);
  --border: rgba(99,179,237,0.15);
  --accent: #4299e1;
  --accent2: #63b3ed;
  --text: #e2e8f0;
  --muted: #718096;
  --up: #22c55e;
  --down: #ef4444;
  --flat: #f59e0b;
  --serif: 'Noto Serif JP', Georgia, serif;
  --sans: 'Noto Sans JP', sans-serif;
}
* { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
html, body { height: 100%; background: var(--bg); color: var(--text); font-family: var(--serif); -webkit-font-smoothing: antialiased; }
body::before {
  content: ''; position: fixed; inset: 0; z-index: 0; pointer-events: none;
  background-image: linear-gradient(rgba(99,179,237,0.03) 1px,transparent 1px), linear-gradient(90deg,rgba(99,179,237,0.03) 1px,transparent 1px);
  background-size: 36px 36px;
}
.header {
  position: fixed; top: 0; left: 0; right: 0; z-index: 100;
  height: 56px; padding: 0 16px;
  display: flex; align-items: center; justify-content: space-between;
  border-bottom: 1px solid var(--border);
  background: rgba(10,14,26,0.96);
  backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px);
}
.logo { display: flex; align-items: center; gap: 9px; }
.logo-mark {
  width: 28px; height: 28px; border-radius: 7px;
  background: linear-gradient(135deg,var(--accent2),var(--accent));
  display: flex; align-items: center; justify-content: center;
  font-size: 13px; font-weight: 900; color: white; font-family: var(--sans);
}
.logo-name { font-size: 13px; font-weight: 700; font-family: var(--sans); }
.logo-sub { font-size: 9px; color: var(--accent2); letter-spacing: .12em; font-family: var(--sans); }
.tabs { display: flex; gap: 3px; }
.tab { padding: 5px 11px; border-radius: 6px; border: none; cursor: pointer; font-size: 11px; font-family: var(--sans); background: transparent; color: var(--muted); transition: .2s; }
.tab.on { background: rgba(99,179,237,.2); color: var(--accent2); }
.main { position: relative; z-index: 1; max-width: 680px; margin: 0 auto; padding: 68px 14px 40px; }
.card { background: var(--surface); border: 1px solid var(--border); border-radius: 12px; padding: 14px; }
.btn { width: 100%; padding: 13px; border-radius: 9px; border: none; font-family: var(--sans); font-size: 13px; font-weight: 700; cursor: pointer; transition: .2s; display: flex; align-items: center; justify-content: center; gap: 6px; }
.btn-primary { background: linear-gradient(135deg,var(--accent),#3182ce); color: white; box-shadow: 0 4px 16px rgba(66,153,225,.3); }
.btn-primary:active { transform: scale(.98); opacity: .9; }
.btn-ghost { background: rgba(99,179,237,.08); color: var(--accent2); border: 1px solid rgba(99,179,237,.2); }
.btn-outline { background: transparent; border: 1px solid var(--border); color: var(--muted); }
.badge { display: inline-flex; align-items: center; gap: 3px; background: rgba(0,0,0,.35); border-radius: 5px; padding: 2px 7px; font-size: 10px; font-family: var(--sans); }
.new-tag { position: absolute; top: 10px; right: 10px; background: var(--accent); border-radius: 4px; padding: 2px 7px; font-size: 9px; color: white; font-weight: 700; font-family: var(--sans); }
.section-lbl { font-size: 9px; color: var(--accent2); margin-bottom: 3px; font-family: var(--sans); letter-spacing: .05em; text-transform: uppercase; }
.stocks-box { border: 1px solid var(--border); border-radius: 10px; overflow: hidden; margin-bottom: 16px; }
.stocks-head { background: rgba(99,179,237,.1); padding: 9px 13px; font-size: 10px; font-weight: 700; color: var(--accent2); font-family: var(--sans); }
.stock-row { padding: 12px 13px; border-top: 1px solid rgba(99,179,237,.08); display: flex; align-items: flex-start; justify-content: space-between; gap: 10px; }
.pred-box { flex-shrink: 0; border-radius: 8px; padding: 6px 10px; text-align: center; min-width: 48px; }
.pred-arrow { font-size: 17px; font-weight: 900; display: block; }
.pred-lbl { font-size: 9px; font-weight: 700; font-family: var(--sans); }
.export-wrap { margin-top: 20px; }
.export-head { font-size: 11px; font-weight: 700; color: var(--accent2); font-family: var(--sans); margin-bottom: 10px; letter-spacing: .05em; }
.export-block { background: rgba(0,0,0,.3); border: 1px solid var(--border); border-radius: 8px; padding: 12px; margin-bottom: 8px; }
.export-lbl { font-size: 9px; color: var(--muted); font-family: var(--sans); margin-bottom: 6px; }
.export-txt { font-size: 11px; color: #a0aec0; line-height: 1.7; font-family: var(--sans); white-space: pre-wrap; word-break: break-word; max-height: 110px; overflow: hidden; }
.copy-btn { margin-top: 8px; width: 100%; padding: 8px; border-radius: 7px; border: 1px solid var(--border); background: rgba(255,255,255,.04); color: var(--text); font-size: 11px; font-family: var(--sans); cursor: pointer; transition: .2s; }
.copy-btn.ok { background: rgba(34,197,94,.1); border-color: rgba(34,197,94,.3); color: var(--up); }
.affili-lbl { font-size: 11px; font-family: var(--sans); color: var(--muted); margin-bottom: 5px; display: block; }
.affili-in { width: 100%; padding: 10px 12px; background: rgba(255,255,255,.04); border: 1px solid var(--border); border-radius: 8px; color: var(--text); font-size: 12px; font-family: var(--sans); outline: none; margin-bottom: 8px; }
.affili-in:focus { border-color: var(--accent); }
.back-btn { display: inline-flex; align-items: center; gap: 5px; background: transparent; border: 1px solid var(--border); border-radius: 7px; padding: 6px 12px; color: var(--muted); font-size: 11px; cursor: pointer; margin-bottom: 16px; font-family: var(--sans); }
.empty { text-align: center; color: #4a5568; padding: 50px 0; font-family: var(--sans); font-size: 13px; }
.hidden { display: none !important; }
.mb8 { margin-bottom: 8px; } .mb12 { margin-bottom: 12px; } .mb16 { margin-bottom: 16px; }
.how-to-banner { background: rgba(99,179,237,.07); border: 1px solid rgba(99,179,237,.2); border-radius: 10px; padding: 13px; margin-bottom: 14px; }
.how-step { display: flex; align-items: flex-start; gap: 10px; margin-bottom: 8px; }
.how-step:last-child { margin-bottom: 0; }
.step-num { width: 20px; height: 20px; border-radius: 50%; background: var(--accent); color: white; font-size: 10px; font-weight: 700; font-family: var(--sans); display: flex; align-items: center; justify-content: center; flex-shrink: 0; margin-top: 1px; }
.step-txt { font-size: 11px; color: #a0aec0; line-height: 1.6; font-family: var(--sans); }
.step-txt strong { color: var(--text); }
</style>
</head>
<body>

<header class="header">
  <div class="logo">
    <div class="logo-mark">株</div>
    <div>
      <div class="logo-name">MarketIntel</div>
      <div class="logo-sub">AI FINANCIAL NEWS</div>
    </div>
  </div>
  <div class="tabs">
    <button class="tab on" onclick="goTab('new',this)">新着</button>
    <button class="tab" onclick="goTab('pub',this)">公開済み</button>
    <button class="tab" onclick="goTab('cfg',this)">設定</button>
  </div>
</header>

<main class="main">

  <!-- ===== NEW TAB ===== -->

  <div id="tNew">

```
<!-- Home -->
<div id="vHome">
  <div style="text-align:center;padding:12px 0 22px">
    <div style="font-size:36px;margin-bottom:8px">📊</div>
    <h1 style="font-size:20px;font-weight:900;font-family:var(--sans);margin-bottom:8px;background:linear-gradient(135deg,var(--accent2),#90cdf4);-webkit-background-clip:text;-webkit-text-fill-color:transparent;">MarketIntel</h1>
    <p style="font-size:12px;color:var(--muted);line-height:1.9;margin-bottom:20px;">株式市場の重要ニュースをAIが分析し<br>X・note・ブログ用コンテンツを自動生成</p>
  </div>

  <div class="how-to-banner mb16">
    <div style="font-size:11px;font-weight:700;color:var(--accent2);font-family:var(--sans);margin-bottom:10px;">📋 使い方</div>
    <div class="how-step"><div class="step-num">1</div><div class="step-txt">「記事を生成する」をタップ → プロンプトをコピー</div></div>
    <div class="how-step"><div class="step-num">2</div><div class="step-txt">Claude.aiアプリに貼り付けて送信</div></div>
    <div class="how-step"><div class="step-num">3</div><div class="step-txt">出力されたJSONをコピー</div></div>
    <div class="how-step"><div class="step-num">4</div><div class="step-txt">戻って<strong>「テキストを貼り付け」</strong>→ 読み込む → 記事を選んで公開</div></div>
  </div>

  <button class="btn btn-primary mb8" onclick="onGenerate()" style="font-size:14px;padding:14px;">
    ⚡ 記事を生成する
  </button>

  <div id="promptBox" class="hidden" style="margin-top:12px;">
    <div style="font-size:11px;font-weight:700;color:var(--accent2);font-family:var(--sans);margin-bottom:6px;">📋 プロンプト（コピーしてClaude.aiに貼り付け）</div>
    <textarea id="promptText" readonly style="width:100%;height:140px;background:rgba(0,0,0,.4);border:1px solid var(--border);border-radius:8px;color:#a0aec0;font-size:11px;font-family:var(--sans);padding:10px;line-height:1.6;resize:none;-webkit-user-select:text;user-select:text;"></textarea>
    <div style="display:flex;gap:8px;margin-top:8px;">
      <button class="btn btn-primary" id="copyPromptBtn" onclick="copyPrompt()" style="flex:1;padding:11px;font-size:12px;">📋 コピー</button>
      <a href="https://claude.ai" target="_blank" class="btn btn-ghost" style="flex:1;padding:11px;font-size:12px;text-decoration:none;display:flex;align-items:center;justify-content:center;">🤖 Claude.aiを開く</a>
    </div>
  </div>

  <div style="display:flex;gap:8px;margin-top:8px;">
    <button class="btn btn-ghost" onclick="document.getElementById('fileIn').click()" style="flex:1;padding:11px;font-size:12px;">
      📥 ファイルから
    </button>
    <button class="btn btn-ghost" onclick="showPasteBox()" style="flex:1;padding:11px;font-size:12px;">
      📋 テキストを貼り付け
    </button>
  </div>
  <input type="file" id="fileIn" accept=".json" class="hidden" onchange="loadJson(event)">

  <!-- Paste JSON box -->
  <div id="pasteBox" class="hidden" style="margin-top:10px;">
    <div style="font-size:11px;font-weight:700;color:var(--accent2);font-family:var(--sans);margin-bottom:6px;">📋 ClaudeのJSONをここに貼り付け</div>
    <textarea id="pasteText" style="width:100%;height:120px;background:rgba(0,0,0,.4);border:1px solid var(--border);border-radius:8px;color:#a0aec0;font-size:11px;font-family:var(--sans);padding:10px;line-height:1.6;resize:none;" placeholder='{"articles":[...]} の形式で貼り付けてください'></textarea>
    <div style="display:flex;gap:8px;margin-top:8px;">
      <button class="btn btn-outline" onclick="hidePasteBox()" style="flex:1;padding:10px;font-size:12px;">キャンセル</button>
      <button class="btn btn-primary" onclick="loadPastedJson()" style="flex:2;padding:10px;font-size:12px;">✅ 読み込む</button>
    </div>
  </div>

  <div id="homeMsg" class="hidden" style="margin-top:12px;background:rgba(34,197,94,.08);border:1px solid rgba(34,197,94,.25);border-radius:8px;padding:11px;font-size:11px;color:#68d391;font-family:var(--sans);line-height:1.7;"></div>
  <div id="homeErr" class="hidden" style="margin-top:12px;background:rgba(239,68,68,.08);border:1px solid rgba(239,68,68,.25);border-radius:8px;padding:11px;font-size:11px;color:#fc8181;font-family:var(--sans);line-height:1.7;"></div>
</div>

<!-- Article select -->
<div id="vSelect" class="hidden">
  <h2 style="font-size:15px;font-weight:700;font-family:var(--sans);margin-bottom:4px;">記事を選択</h2>
  <p style="font-size:11px;color:var(--muted);margin-bottom:14px;">公開する記事を1件選んでください</p>
  <div id="candList"></div>
  <div style="display:flex;gap:8px;margin-top:6px;">
    <button class="btn btn-outline" style="flex:1;padding:11px;" onclick="showHome()">戻る</button>
    <button class="btn btn-primary" id="pubBtn" style="flex:2;padding:11px;" onclick="doPublish()" disabled>この記事を公開する</button>
  </div>
</div>

<!-- Article detail (from new) -->
<div id="vArticle" class="hidden">
  <button class="back-btn" onclick="backFromArticle()">← 戻る</button>
  <div id="artBody"></div>
</div>
```

  </div>

  <!-- ===== PUB TAB ===== -->

  <div id="tPub" class="hidden">
    <h2 style="font-size:15px;font-weight:700;font-family:var(--sans);margin-bottom:14px;">公開済み記事</h2>
    <div id="pubList"></div>
    <!-- Article detail (from pub) -->
    <div id="vArtPub" class="hidden">
      <button class="back-btn" onclick="backFromPub()">← 公開済み一覧へ</button>
      <div id="artBodyPub"></div>
    </div>
  </div>

  <!-- ===== SETTINGS TAB ===== -->

  <div id="tCfg" class="hidden">
    <h2 style="font-size:15px;font-weight:700;font-family:var(--sans);margin-bottom:16px;">設定</h2>

```
<div class="card mb12">
  <div class="section-lbl" style="margin-bottom:10px;">💰 アフィリエイトリンク</div>
  <p style="font-size:10px;color:var(--muted);font-family:var(--sans);margin-bottom:12px;line-height:1.7;">記事末尾に自動挿入するリンクを登録。ASPで発行したURLを貼り付けてください。</p>
  <label class="affili-lbl">SBI証券</label>
  <input class="affili-in" id="aSBI" placeholder="https://accesstrade.net/...">
  <label class="affili-lbl">楽天証券</label>
  <input class="affili-in" id="aRak" placeholder="https://...">
  <label class="affili-lbl">GMOクリック証券</label>
  <input class="affili-in" id="aGMO" placeholder="https://...">
  <label class="affili-lbl">FX口座（任意）</label>
  <input class="affili-in" id="aFX" placeholder="https://...">
  <button class="btn btn-primary" style="padding:11px;" onclick="saveAffili()">💾 保存する</button>
</div>

<div class="card mb12">
  <div class="section-lbl" style="margin-bottom:10px;">🗂️ データ管理</div>
  <button class="btn btn-outline" style="padding:10px;font-size:12px;" onclick="clearAll()">公開済み記事を全件削除</button>
</div>

<div class="card">
  <div class="section-lbl" style="margin-bottom:8px;">📱 ホーム画面に追加する方法</div>
  <p style="font-size:11px;color:var(--muted);font-family:var(--sans);line-height:1.8;">
    Safari で開いている場合：<br>
    下の共有ボタン（□↑）→「ホーム画面に追加」→「追加」<br><br>
    追加後はアプリとして起動できます。
  </p>
</div>
```

  </div>

</main>

<script>
// ── Storage ──────────────────────────────────────────────
const DB = {
  g: k => { try { return JSON.parse(localStorage.getItem(k)); } catch { return null; } },
  s: (k,v) => { try { localStorage.setItem(k,JSON.stringify(v)); } catch {} },
};

// ── State ────────────────────────────────────────────────
let S = {
  pub: DB.g('mi_pub') || [],
  affili: DB.g('mi_affili') || { sbi:'', rak:'', gmo:'', fx:'' },
  cands: [],
  selIdx: null,
  curArt: null,
  backFrom: 'select', // 'select' | 'pub'
};

// ── Init ─────────────────────────────────────────────────
window.onload = () => {
  loadAffiliUI();
};

// ── Tab ──────────────────────────────────────────────────
function goTab(t, el) {
  document.querySelectorAll('.tab').forEach(b => b.classList.remove('on'));
  el.classList.add('on');
  ['tNew','tPub','tCfg'].forEach(id => document.getElementById(id).classList.add('hidden'));
  document.getElementById(t === 'new' ? 'tNew' : t === 'pub' ? 'tPub' : 'tCfg').classList.remove('hidden');
  if (t === 'pub') renderPubList();
}

// ── Views ────────────────────────────────────────────────
function showHome() {
  ['vSelect','vArticle'].forEach(id => document.getElementById(id).classList.add('hidden'));
  document.getElementById('vHome').classList.remove('hidden');
}

function showSelect() {
  ['vHome','vArticle'].forEach(id => document.getElementById(id).classList.add('hidden'));
  document.getElementById('vSelect').classList.remove('hidden');
}

// ── Generate: copy prompt + open Claude.ai ───────────────
function onGenerate() {
  const avoidTitles = S.pub.map(a => a.title).slice(0, 5);
  const avoidNote = avoidTitles.length ? '\n既出記事（除外）: ' + avoidTitles.join(' / ') : '';
  const prompt = '株価に関わりそうな金融ニュースを集めて3つピックアップして記事にしてください。\n\n条件:\n①記事は全て日本語。最後に参照元リンク貼り付け\n②ピックアップするニュースは過去に記事にした情報以外にする\n③記事の最後にニュースに関連する上場企業(大型株、中小型株それぞれ1社以上)を選定し、上昇下降予測を付け加えること\n④3件全ての記事を一度に出力すること（選択待ちは不要）' + avoidNote + '\n\n以下のJSON形式のみで出力してください（説明文不要・JSONだけ出力）:\n```json\n{"articles":[{"id":"1","title":"タイトル","summary":"概要100字","content":"本文500字","large_name":"大型株名","large_ticker":"7203","large_pred":"上昇","large_reason":"根拠50字","small_name":"中小株名","small_ticker":"4689","small_pred":"下降","small_reason":"根拠50字","source":"https://www.nikkei.com"},{"id":"2","title":"タイトル2","summary":"概要2","content":"本文2","large_name":"企業名","large_ticker":"6758","large_pred":"横ばい","large_reason":"根拠","small_name":"企業名","small_ticker":"3382","small_pred":"上昇","small_reason":"根拠","source":"https://www.bloomberg.co.jp"},{"id":"3","title":"タイトル3","summary":"概要3","content":"本文3","large_name":"企業名","large_ticker":"9984","large_pred":"下降","large_reason":"根拠","small_name":"企業名","small_ticker":"2413","small_pred":"上昇","small_reason":"根拠","source":"https://jp.reuters.com"}]}\n```';

  // Show prompt in textarea
  const box = document.getElementById('promptBox');
  const ta = document.getElementById('promptText');
  ta.value = prompt;
  box.classList.remove('hidden');

  // Scroll to prompt box
  setTimeout(() => box.scrollIntoView({ behavior: 'smooth', block: 'start' }), 100);
}

function copyPrompt() {
  const ta = document.getElementById('promptText');
  ta.select();
  ta.setSelectionRange(0, 99999);
  try {
    document.execCommand('copy');
  } catch(e) {}
  try {
    navigator.clipboard.writeText(ta.value).catch(() => {});
  } catch(e) {}
  const btn = document.getElementById('copyPromptBtn');
  btn.textContent = '✅ コピーしました';
  setTimeout(() => { btn.textContent = '📋 コピー'; }, 2000);
}

// ── Paste JSON directly ──────────────────────────────────
function showPasteBox() {
  document.getElementById('pasteBox').classList.remove('hidden');
  document.getElementById('pasteText').value = '';
  setTimeout(() => document.getElementById('pasteText').focus(), 100);
}
function hidePasteBox() {
  document.getElementById('pasteBox').classList.add('hidden');
}
function loadPastedJson() {
  const raw = document.getElementById('pasteText').value.trim();
  if (!raw) { showMsg('homeErr', '⚠️ テキストが空です'); return; }
  try {
    // Extract JSON from code block if present
    const match = raw.match(/```(?:json)?\s*([\s\S]*?)```/) || raw.match(/(\{[\s\S]*\})/);
    const jsonStr = match ? (match[1] || match[0]) : raw;
    const d = JSON.parse(jsonStr.trim());
    if (!d.articles?.length) throw new Error('articles が見つかりません');
    S.cands = d.articles.map(a => ({
      id: a.id, title: a.title, summary: a.summary, content: a.content,
      relatedStocks: {
        large: { name: a.large_name, ticker: a.large_ticker, prediction: a.large_pred, reason: a.large_reason },
        small: { name: a.small_name, ticker: a.small_ticker, prediction: a.small_pred, reason: a.small_reason },
      },
      sources: [a.source].filter(Boolean),
    }));
    S.selIdx = null;
    hidePasteBox();
    document.getElementById('homeMsg').classList.add('hidden');
    renderCands();
    showSelect();
  } catch(err) {
    showMsg('homeErr', '⚠️ 読み込みに失敗しました: ' + err.message);
  }
}

// ── Load JSON file ────────────────────────────────────────
function loadJson(e) {
  const file = e.target.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = ev => {
    try {
      const d = JSON.parse(ev.target.result);
      if (!d.articles?.length) throw new Error('articles が見つかりません');
      S.cands = d.articles.map(a => ({
        id: a.id, title: a.title, summary: a.summary, content: a.content,
        relatedStocks: {
          large: { name: a.large_name, ticker: a.large_ticker, prediction: a.large_pred, reason: a.large_reason },
          small: { name: a.small_name, ticker: a.small_ticker, prediction: a.small_pred, reason: a.small_reason },
        },
        sources: [a.source].filter(Boolean),
      }));
      S.selIdx = null;
      document.getElementById('homeMsg').classList.add('hidden');
      renderCands();
      showSelect();
    } catch(err) {
      showMsg('homeErr', '⚠️ ファイルの読み込みに失敗しました: ' + err.message);
    }
  };
  reader.readAsText(file);
  e.target.value = '';
}

// ── Candidates ────────────────────────────────────────────
function renderCands() {
  const el = document.getElementById('candList');
  el.innerHTML = '';
  S.cands.forEach((a, i) => {
    const on = S.selIdx === i;
    const d = document.createElement('div');
    d.style.marginBottom = '10px';
    d.innerHTML = `
      <div class="card" style="cursor:pointer;position:relative;border-color:${on?'rgba(99,179,237,.5)':'var(--border)'};background:${on?'rgba(99,179,237,.07)':'var(--surface)'};" onclick="selCand(${i})">
        <div style="display:flex;gap:9px">
          <div style="width:20px;height:20px;border-radius:50%;flex-shrink:0;background:${on?'var(--accent)':'rgba(99,179,237,.1)'};display:flex;align-items:center;justify-content:center;font-size:10px;color:white;font-weight:700;font-family:var(--sans)">${on?'✓':i+1}</div>
          <div style="flex:1">
            <div style="font-size:13px;font-weight:700;margin-bottom:5px;line-height:1.5">${a.title}</div>
            <div style="font-size:11px;color:var(--muted);line-height:1.7;margin-bottom:8px">${a.summary}</div>
            <div style="display:flex;gap:5px;flex-wrap:wrap">
              ${[a.relatedStocks.large, a.relatedStocks.small].map(s=>`
                <span class="badge"><span style="color:#a0aec0">${s.name}</span><span style="color:${pc(s.prediction)};font-weight:700;margin-left:3px">${pi(s.prediction)}${s.prediction}</span></span>`).join('')}
            </div>
          </div>
        </div>
      </div>`;
    el.appendChild(d);
  });
}

function selCand(i) {
  S.selIdx = i;
  document.getElementById('pubBtn').disabled = false;
  renderCands();
}

function doPublish() {
  if (S.selIdx === null) return;
  const art = { ...S.cands[S.selIdx], publishedAt: new Date().toLocaleDateString('ja-JP') };
  S.pub.unshift(art);
  DB.s('mi_pub', S.pub);
  S.curArt = art;
  S.backFrom = 'select';
  document.getElementById('artBody').innerHTML = buildArticleHTML(art);
  ['vHome','vSelect'].forEach(id => document.getElementById(id).classList.add('hidden'));
  document.getElementById('vArticle').classList.remove('hidden');
}

function backFromArticle() {
  document.getElementById('vArticle').classList.add('hidden');
  if (S.backFrom === 'select') showSelect();
  else showHome();
}

// ── Published ─────────────────────────────────────────────
function renderPubList() {
  const pubList = document.getElementById('pubList');
  const artPub = document.getElementById('vArtPub');
  artPub.classList.add('hidden');
  pubList.classList.remove('hidden');
  if (!S.pub.length) { pubList.innerHTML = '<div class="empty">まだ公開済み記事がありません</div>'; return; }
  pubList.innerHTML = S.pub.map((a,i) => `
    <div class="card mb8" style="cursor:pointer" onclick="openPub(${i})">
      <div style="font-size:13px;font-weight:700;margin-bottom:4px">${a.title}</div>
      <div style="font-size:11px;color:var(--muted);line-height:1.6;margin-bottom:3px">${a.summary}</div>
      <div style="font-size:9px;color:#2d3748;font-family:var(--sans)">公開日: ${a.publishedAt||'–'}</div>
    </div>`).join('');
}

function openPub(i) {
  S.curArt = S.pub[i];
  document.getElementById('pubList').classList.add('hidden');
  document.getElementById('artBodyPub').innerHTML = buildArticleHTML(S.curArt);
  document.getElementById('vArtPub').classList.remove('hidden');
}

function backFromPub() {
  document.getElementById('vArtPub').classList.add('hidden');
  renderPubList();
}

// ── Article HTML builder ──────────────────────────────────
function buildArticleHTML(a) {
  const ls = a.relatedStocks.large;
  const ss = a.relatedStocks.small;
  const xPost = buildX(a);
  const noteMd = buildNote(a);
  const affMd = buildAffili();

  return `
    <h1 style="font-size:18px;font-weight:900;line-height:1.55;margin-bottom:12px">${a.title}</h1>
    <div class="card mb12" style="background:rgba(99,179,237,.05);border-color:rgba(99,179,237,.25)">
      <div class="section-lbl">概要</div>
      <div style="font-size:12px;line-height:1.8;color:#cbd5e0">${a.summary}</div>
    </div>
    <div style="font-size:13px;line-height:2.1;margin-bottom:20px;white-space:pre-line">${a.content}</div>

    <div class="stocks-box">
      <div class="stocks-head">📊 関連銘柄・株価予測</div>
      ${[{l:'大型株',s:ls},{l:'中小型株',s:ss}].filter(x=>x.s).map(({l,s})=>`
        <div class="stock-row">
          <div>
            <div style="font-size:9px;color:var(--muted);margin-bottom:2px;font-family:var(--sans)">${l}</div>
            <div style="font-size:13px;font-weight:700;margin-bottom:2px">${s.name} <span style="font-size:10px;color:var(--muted)">${s.ticker}</span></div>
            <div style="font-size:10px;color:#a0aec0;line-height:1.6">${s.reason}</div>
          </div>
          <div class="pred-box" style="background:${pc(s.prediction)}20;border:1px solid ${pc(s.prediction)}40">
            <span class="pred-arrow" style="color:${pc(s.prediction)}">${pi(s.prediction)}</span>
            <span class="pred-lbl" style="color:${pc(s.prediction)}">${s.prediction}</span>
          </div>
        </div>`).join('')}
    </div>

    ${a.sources?.length?`
    <div style="margin-bottom:18px">
      <div class="section-lbl" style="margin-bottom:4px">参照元</div>
      ${a.sources.map(s=>`<a href="${s}" target="_blank" style="display:block;font-size:11px;color:var(--accent2);text-decoration:none;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;margin-bottom:3px">${s}</a>`).join('')}
    </div>`:''}

    <div class="export-wrap">
      <div class="export-head">📤 コンテンツ出力</div>
      <div class="export-block">
        <div class="export-lbl">🐦 X（Twitter）投稿文</div>
        <div class="export-txt" id="eX">${xPost}</div>
        <button class="copy-btn" onclick="doCopy('eX',this)">📋 コピーする</button>
      </div>
      <div class="export-block">
        <div class="export-lbl">📝 note用マークダウン（全文）</div>
        <div class="export-txt" id="eNote">${esc(noteMd)}</div>
        <button class="copy-btn" onclick="doCopy('eNote',this)">📋 コピーする</button>
      </div>
      ${affMd?`
      <div class="export-block">
        <div class="export-lbl">💰 アフィリエイト挿入ブロック</div>
        <div class="export-txt" id="eAff">${esc(affMd)}</div>
        <button class="copy-btn" onclick="doCopy('eAff',this)">📋 コピーする</button>
      </div>`:''}
    </div>`;
}

// ── Content builders ──────────────────────────────────────
function buildX(a) {
  const ls = a.relatedStocks.large, ss = a.relatedStocks.small;
  const body = a.summary.slice(0, 95);
  const stocks = `\n\n📌 ${ls.name}(${ls.ticker}) ${pi(ls.prediction)}${ls.prediction}\n📌 ${ss.name}(${ss.ticker}) ${pi(ss.prediction)}${ss.prediction}`;
  const tags = '\n\n#日本株 #株式投資 #金融ニュース #投資 #マーケット';
  let p = body + stocks + tags;
  return p.length > 280 ? p.slice(0,276)+'...' : p;
}

function buildNote(a) {
  const ls = a.relatedStocks.large, ss = a.relatedStocks.small;
  const aff = buildAffili();
  return `# ${a.title}\n\n## 概要\n${a.summary}\n\n---\n\n${a.content}\n\n---\n\n## 関連銘柄・株価予測\n\n| 区分 | 銘柄 | コード | 予測 | 根拠 |\n|------|------|--------|------|------|\n| 大型株 | ${ls.name} | ${ls.ticker} | ${pi(ls.prediction)}${ls.prediction} | ${ls.reason} |\n| 中小型株 | ${ss.name} | ${ss.ticker} | ${pi(ss.prediction)}${ss.prediction} | ${ss.reason} |\n\n${a.sources?.length?`**参照元:** ${a.sources.join(' / ')}`:''}\n\n---\n${aff}\n*本記事はAIによる分析を含みます。投資判断はご自身の責任で行ってください。*`;
}

function buildAffili() {
  const a = S.affili;
  const ls = [];
  if (a.sbi) ls.push(`- [SBI証券 口座開設（無料）](${a.sbi}) — 業界最大手・豊富な銘柄数`);
  if (a.rak) ls.push(`- [楽天証券 口座開設（無料）](${a.rak}) — 楽天ポイントが貯まる`);
  if (a.gmo) ls.push(`- [GMOクリック証券（無料）](${a.gmo}) — 手数料が業界最安水準`);
  if (a.fx) ls.push(`- [FX口座開設](${a.fx})`);
  return ls.length ? `## 💹 おすすめ証券口座\n\n${ls.join('\n')}\n` : '';
}

// ── Settings ─────────────────────────────────────────────
function saveAffili() {
  S.affili = { sbi: document.getElementById('aSBI').value.trim(), rak: document.getElementById('aRak').value.trim(), gmo: document.getElementById('aGMO').value.trim(), fx: document.getElementById('aFX').value.trim() };
  DB.s('mi_affili', S.affili);
  alert('保存しました ✓');
}
function loadAffiliUI() {
  document.getElementById('aSBI').value = S.affili.sbi||'';
  document.getElementById('aRak').value = S.affili.rak||'';
  document.getElementById('aGMO').value = S.affili.gmo||'';
  document.getElementById('aFX').value = S.affili.fx||'';
}
function clearAll() {
  if (!confirm('公開済み記事を全件削除しますか？')) return;
  S.pub = []; DB.s('mi_pub', []);
  alert('削除しました');
}

// ── Helpers ───────────────────────────────────────────────
function pc(p) { return p==='上昇'?'#22c55e':p==='下降'?'#ef4444':'#f59e0b'; }
function pi(p) { return p==='上昇'?'↑':p==='下降'?'↓':'→'; }
function esc(s) { return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }
function showMsg(id, txt) {
  const el = document.getElementById(id);
  el.innerHTML = txt.replace(/\n/g,'<br>');
  el.classList.remove('hidden');
}
async function doCopy(id, btn) {
  const text = document.getElementById(id).innerText;
  try { await navigator.clipboard.writeText(text); }
  catch { const ta=document.createElement('textarea'); ta.value=text; ta.style.cssText='position:fixed;opacity:0'; document.body.appendChild(ta); ta.select(); document.execCommand('copy'); document.body.removeChild(ta); }
  btn.textContent='✅ コピーしました'; btn.classList.add('ok');
  setTimeout(()=>{ btn.textContent='📋 コピーする'; btn.classList.remove('ok'); }, 2000);
}
</script>

</body>
</html>
