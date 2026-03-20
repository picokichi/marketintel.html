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
.track-due{background:rgba(250,204,21,.15);color:var(–flat);animation:pulse 1.5s ease-in-out infinite;}
@keyframes pulse{0%,100%{opacity:1;}50%{opacity:.5;}}

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
.price-badge{display:inline-flex;align-items:center;gap:5px;background:rgba(0,0,0,.3);border:1px solid rgba(99,179,237,.15);border-radius:6px;padding:3px 9px;margin-top:4px;font-family:var(–sans);}
.price-val{font-size:12px;font-weight:700;color:var(–text);}
.price-chg-up{font-size:10px;color:var(–up);}
.price-chg-down{font-size:10px;color:var(–down);}
.price-chg-flat{font-size:10px;color:var(–flat);}
.price-loading{font-size:10px;color:var(–muted);animation:pulse 1s ease-in-out infinite;}
/* Check & Diff UI */
.check-badge{display:inline-flex;align-items:center;gap:4px;border-radius:5px;padding:2px 8px;font-size:10px;font-family:var(–sans);font-weight:700;}
.check-error{background:rgba(239,68,68,.15);color:var(–down);border:1px solid rgba(239,68,68,.3);}
.check-warn{background:rgba(245,158,11,.15);color:var(–flat);border:1px solid rgba(245,158,11,.3);}
.check-ok{background:rgba(34,197,94,.12);color:var(–up);border:1px solid rgba(34,197,94,.25);}
.diff-block{border-radius:8px;overflow:hidden;margin-bottom:10px;border:1px solid var(–border);}
.diff-orig{background:rgba(239,68,68,.07);padding:9px 12px;border-bottom:1px solid var(–border);}
.diff-new{background:rgba(34,197,94,.07);padding:9px 12px;}
.diff-label{font-size:9px;font-family:var(–sans);font-weight:700;margin-bottom:3px;}
.diff-text{font-size:12px;line-height:1.7;color:var(–text);}
.step-indicator{display:flex;align-items:center;gap:6px;margin-bottom:14px;font-family:var(–sans);}
.step-dot{width:22px;height:22px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:700;flex-shrink:0;}
.step-active{background:var(–accent);color:white;}
.step-done{background:rgba(34,197,94,.2);color:var(–up);}
.step-pending{background:rgba(99,179,237,.1);color:var(–muted);}
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
    <p style="font-size:11px;color:var(--muted);font-family:var(--sans);margin-bottom:10px;">記事の冒頭・X投稿に自動挿入されます。<br>「AIの分析」の前に置く<strong style="color:var(--text)">あなた自身の感情・視点</strong>です。</p>

```
<!-- Tab selector -->
<div style="display:flex;gap:4px;margin-bottom:10px;">
  <button id="tabHuman" onclick="switchAuthorTab('human')" style="flex:1;padding:7px;border-radius:7px;border:none;font-size:11px;font-family:var(--sans);font-weight:700;cursor:pointer;background:rgba(250,204,21,.2);color:#f59e0b;">😊 素直な反応</button>
  <button id="tabAI" onclick="switchAuthorTab('ai')" style="flex:1;padding:7px;border-radius:7px;border:none;font-size:11px;font-family:var(--sans);font-weight:700;cursor:pointer;background:rgba(99,179,237,.08);color:var(--muted);">🤖 AI生成コメント</button>
</div>

<!-- Human reaction templates -->
<div id="humanOpts">
  <p style="font-size:10px;color:var(--muted);font-family:var(--sans);margin-bottom:7px;">👆 タップして選ぶだけ。金融知識ゼロでもOK。</p>
  <div id="humanOptList"></div>
</div>

<!-- AI generated comments -->
<div id="aiOpts" class="hidden">
  <p style="font-size:10px;color:var(--muted);font-family:var(--sans);margin-bottom:7px;">AIが記事のテーマに合わせて3パターン生成しました</p>
  <div id="authorOpts"></div>
</div>

<div style="display:flex;gap:7px;margin-top:10px;">
  <button class="btn btn-o" style="flex:1;padding:10px;" onclick="skipAuthor()">スキップ</button>
  <button class="btn btn-p" id="authorOkBtn" style="flex:2;padding:10px;" onclick="confirmAuthor()" disabled>この一言で進む →</button>
</div>
```

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

  <!-- CHECK FLOW: Step1 - Generate check prompt -->

  <div id="vCheck" class="hidden">
    <button class="back-btn" onclick="backToSelect()">← 記事選択へ戻る</button>
    <h2 style="font-size:15px;font-weight:700;font-family:var(--sans);margin-bottom:4px;">🔍 ステップ①: ChatGPTでチェック</h2>
    <p style="font-size:11px;color:var(--muted);font-family:var(--sans);margin-bottom:12px;">チェックプロンプトをコピーしてChatGPTに貼り付けてください</p>
    <div class="step-indicator">
      <div class="step-dot step-active">1</div><span style="font-size:11px;color:var(--accent2)">チェックプロンプトをChatGPTへ</span>
      <div class="step-dot step-pending" style="margin-left:auto">2</div><span style="font-size:11px;color:var(--muted)">結果を貼り付け</span>
    </div>
    <textarea id="checkPromptText" readonly style="width:100%;height:160px;background:rgba(0,0,0,.4);border:1px solid var(--border);border-radius:8px;color:#a0aec0;font-size:10px;font-family:monospace;padding:9px;line-height:1.5;resize:none;-webkit-user-select:text;user-select:text;margin-bottom:8px;"></textarea>
    <div style="display:flex;gap:7px;margin-bottom:12px;">
      <button class="btn btn-p" id="cpCheckBtn" onclick="copyCheckPrompt()" style="flex:1;padding:10px;font-size:12px;">📋 コピー</button>
      <a href="https://chatgpt.com" target="_blank" class="btn btn-g" style="flex:1;padding:10px;font-size:12px;text-decoration:none;display:flex;align-items:center;justify-content:center;">🤖 ChatGPTを開く</a>
    </div>
    <div style="font-size:11px;font-weight:700;color:var(--accent2);font-family:var(--sans);margin-bottom:5px;">📋 チェック結果JSONを貼り付け</div>
    <textarea id="checkResultText" style="width:100%;height:110px;background:rgba(0,0,0,.4);border:1px solid var(--border);border-radius:8px;color:#a0aec0;font-size:11px;font-family:var(--sans);padding:9px;line-height:1.6;resize:none;" placeholder='{"checks":[...]} の形式で貼り付けてください'></textarea>
    <div style="display:flex;gap:7px;margin-top:8px;">
      <button class="btn btn-o" onclick="skipCheck()" style="flex:1;padding:10px;font-size:12px;">スキップして公開</button>
      <button class="btn btn-p" onclick="loadCheckResult()" style="flex:2;padding:10px;font-size:12px;">✅ チェック結果を読み込む</button>
    </div>
    <div id="checkErr" class="hidden" style="margin-top:8px;background:rgba(239,68,68,.08);border:1px solid rgba(239,68,68,.25);border-radius:8px;padding:10px;font-size:11px;color:#fc8181;font-family:var(--sans);"></div>
  </div>

  <!-- CHECK FLOW: Step2 - Show check results & generate fix prompt -->

  <div id="vCheckResult" class="hidden">
    <button class="back-btn" onclick="showView('vCheck')">← チェックへ戻る</button>
    <h2 style="font-size:15px;font-weight:700;font-family:var(--sans);margin-bottom:4px;">📋 チェック結果</h2>
    <div id="checkSummary" style="margin-bottom:12px;"></div>
    <div id="checkIssueList" style="margin-bottom:14px;"></div>
    <div id="fixPromptSection" class="hidden">
      <div style="font-size:11px;font-weight:700;color:var(--accent2);font-family:var(--sans);margin-bottom:5px;">🔧 ステップ②: Claudeで修正</div>
      <p style="font-size:11px;color:var(--muted);font-family:var(--sans);margin-bottom:8px;">修正プロンプトをコピーしてClaude.aiに貼り付けてください</p>
      <textarea id="fixPromptText" readonly style="width:100%;height:140px;background:rgba(0,0,0,.4);border:1px solid var(--border);border-radius:8px;color:#a0aec0;font-size:10px;font-family:monospace;padding:9px;line-height:1.5;resize:none;-webkit-user-select:text;user-select:text;margin-bottom:8px;"></textarea>
      <div style="display:flex;gap:7px;margin-bottom:12px;">
        <button class="btn btn-p" id="cpFixBtn" onclick="copyFixPrompt()" style="flex:1;padding:10px;font-size:12px;">📋 コピー</button>
        <a href="https://claude.ai" target="_blank" class="btn btn-g" style="flex:1;padding:10px;font-size:12px;text-decoration:none;display:flex;align-items:center;justify-content:center;">🤖 Claudeを開く</a>
      </div>
      <div style="font-size:11px;font-weight:700;color:var(--accent2);font-family:var(--sans);margin-bottom:5px;">📋 修正済みJSONを貼り付け</div>
      <textarea id="fixResultText" style="width:100%;height:110px;background:rgba(0,0,0,.4);border:1px solid var(--border);border-radius:8px;color:#a0aec0;font-size:11px;font-family:var(--sans);padding:9px;line-height:1.6;resize:none;" placeholder='{"articles":[...]} の形式で貼り付けてください'></textarea>
      <div style="display:flex;gap:7px;margin-top:8px;">
        <button class="btn btn-o" onclick="skipFix()" style="flex:1;padding:10px;font-size:12px;">修正せず公開</button>
        <button class="btn btn-p" onclick="loadFixResult()" style="flex:2;padding:10px;font-size:12px;">✅ 修正済みを読み込む</button>
      </div>
    </div>
    <div id="noIssuesSection" class="hidden">
      <div style="background:rgba(34,197,94,.08);border:1px solid rgba(34,197,94,.25);border-radius:8px;padding:12px;text-align:center;font-family:var(--sans);">
        <div style="font-size:16px;margin-bottom:4px;">✅</div>
        <div style="font-size:13px;font-weight:700;color:var(--up);margin-bottom:4px;">問題なし！</div>
        <div style="font-size:11px;color:var(--muted);">チェックに全て合格しました</div>
      </div>
      <button class="btn btn-p" style="margin-top:10px;padding:12px;" onclick="proceedToAuthor()">この記事で進む →</button>
    </div>
  </div>

  <!-- CHECK FLOW: Step3 - Diff viewer -->

  <div id="vDiff" class="hidden">
    <button class="back-btn" onclick="showView('vCheckResult')">← チェック結果へ戻る</button>
    <h2 style="font-size:15px;font-weight:700;font-family:var(--sans);margin-bottom:4px;">🔎 修正前後の比較</h2>
    <p style="font-size:11px;color:var(--muted);font-family:var(--sans);margin-bottom:12px;">修正内容を確認して承認・却下してください</p>
    <div id="diffList" style="margin-bottom:14px;"></div>
    <div style="display:flex;gap:7px;">
      <button class="btn btn-o" style="flex:1;padding:11px;" onclick="rejectFix()">🗑 記事を破棄</button>
      <button class="btn btn-g" style="flex:1;padding:11px;" onclick="skipFix()">元のまま公開</button>
      <button class="btn btn-p" style="flex:2;padding:11px;" onclick="approveFix()">✅ 修正を承認して進む</button>
    </div>
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
  <p style="font-size:11px;color:var(--muted);font-family:var(--sans);margin-bottom:10px;">Xで信頼を積む最強の武器。記事公開から<strong style="color:var(--accent2)">1週間後</strong>が判定期限です。</p>
  <div style="background:rgba(250,204,21,.06);border:1px solid rgba(250,204,21,.2);border-radius:8px;padding:9px 12px;margin-bottom:14px;font-size:10px;font-family:var(--sans);color:#a0aec0;line-height:1.8;">
    📌 判定方法: 予測した銘柄が「予測方向と同じ動き」をしていれば的中<br>
    例) ↑上昇予測 → 1週間後に株価が上がっていれば ✓ 的中<br>
    ⏰ 期限が来た予測は自動でハイライト表示されます
  </div>
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
    <div class="lbl" style="margin-bottom:9px;">🤖 J-Quants APIキー（予測自動判定）</div>
    <p style="font-size:10px;color:var(--muted);font-family:var(--sans);margin-bottom:8px;line-height:1.7;">
      登録: <a href="https://application.jpx-jquants.com" target="_blank" style="color:var(--accent2)">application.jpx-jquants.com</a>（無料）<br>
      設定するとアプリを開くたびに判定期限を過ぎた予測を自動判定します
    </p>
    <input class="aff-in" id="jqToken" placeholder="Bearer eyJ..." style="margin-bottom:8px;font-family:monospace;font-size:11px;">
    <button class="btn btn-p" style="padding:10px;" onclick="saveJQ()">💾 保存する</button>
    <div id="jqStatus" style="font-size:10px;font-family:var(--sans);color:var(--muted);margin-top:6px;"></div>
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
  jqToken:DB.g('mi_jqtoken')||'',
  jqRefreshToken:DB.g('mi_jqrefresh')||'',
  baselinePrices:DB.g('mi_baselines')||{},
  cands:[],selIdx:null,curArt:null,backFrom:'select',
  authorOpts:[],selAuthor:null,authorCategoryHook:'',
  preds:DB.g('mi_preds')||[],
  checkCand:null,checkResult:null,fixedCand:null,
};

window.onload=()=>{
  loadAffUI();updateStatus();renderClickStats();
  document.getElementById('genInv').value=S.inv;
  document.getElementById('noteUrl').value=S.noteUrl;
  document.getElementById('jqToken').value=S.jqToken;
  // Check for due predictions and update tab badge
  setTimeout(()=>{
    const now=new Date().getTime();
    const due=S.preds.filter(p=>p.result==='pending'&&p.deadlineTs&&now>=p.deadlineTs).length;
    const tab=document.querySelector('.tab[onclick*="track"]');
    if(tab&&due>0)tab.textContent=`予測 ⏰${due}`;
    // Auto-judge if J-Quants token is set
    if(S.jqToken&&due>0)autoJudgeAll();
  },500);
};

// ── Tab ──────────────────────────────────────────────────
function goTab(t,el){
  document.querySelectorAll('.tab').forEach(b=>b.classList.remove('on'));
  el.classList.add('on');
  ['tNew','tPub','tTrack','tCfg'].forEach(id=>document.getElementById(id).classList.add('hidden'));
  const map={new:'tNew',pub:'tPub',track:'tTrack',cfg:'tCfg'};
  document.getElementById(map[t]).classList.remove('hidden');
  if(t==='pub')renderPubList();
  if(t==='track'){renderTrack();}
}

function showHome(){['vSelect','vArticle','vAuthor','vCheck','vCheckResult','vDiff'].forEach(id=>{const el=document.getElementById(id);if(el)el.classList.add('hidden');});document.getElementById('vHome').classList.remove('hidden');}
function showSelect(){['vHome','vArticle','vAuthor','vCheck','vCheckResult','vDiff'].forEach(id=>{const el=document.getElementById(id);if(el)el.classList.add('hidden');});document.getElementById('vSelect').classList.remove('hidden');}
function showAuthor(){['vHome','vSelect','vArticle','vCheck','vCheckResult','vDiff'].forEach(id=>{const el=document.getElementById(id);if(el)el.classList.add('hidden');});document.getElementById('vAuthor').classList.remove('hidden');}

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

  // Generate current datetime string at button-press moment
  const now=new Date();
  const todayStr=now.toLocaleDateString('ja-JP',{year:'numeric',month:'long',day:'numeric',weekday:'long'})+' '+now.toLocaleTimeString('ja-JP',{hour:'2-digit',minute:'2-digit'});

  const p='あなたは個人投資家向けの人気金融ブロガーです。「読まれる・シェアされる・他にはない」記事を書くのが得意です。\n\n【本日の日時（システム自動取得・変更禁止）】\n'+todayStr+'\nこの日時を全ての記事・日付表現の基準とすること。「明日」「来週」「今週」「先週」などの相対表現はこの日時から計算して使用すること。この日時と異なる日付を記事に使用することは絶対に禁止。\n\n株価に影響しそうな最新の金融ニュースを3つピックアップし、以下のスタイルで記事を書いてください。\n\n【リサーチのルール】\n・各トピックについて必ず異なるメディア（日経・Bloomberg・Reuters・Yahoo!ファイナンス・東洋経済・会社四季報など）の記事を最低3つ参照すること\n・各メディアの論調の違い・温度差を記事の中で明示すること\n・複数ソースを比較した上での独自分析・見解を必ず加えること\n・株価・出来高・騰落率などの具体的な数字を入れること。確認できた数字には（○○報道）と出典を明記し、推計・概算の場合は「〜と推定される」と注釈を入れること\n・そのニュースから3手先に何が起きるかの連鎖予測を文章として自然に組み込むこと\n\n【文体・スタイルのルール】\n・タイトルは「数字」「問い」「驚き」「逆説」で始める\n・冒頭1〜2文で読者を引き込むフックを入れる（毎記事で異なる表現を使うこと）\n・「だからどうなる？」「投資家として何をすべきか？」まで踏み込む\n・専門用語は必ずかみ砕いて説明する\n・筆者の見解・予測を強めに断言する\n・読者への問いかけを最低1回入れる\n・締めは「次に注目すべきポイント」で終わる\n\n【銘柄提示のルール】\n・【注目株発掘プロセス・厳守】以下のステップを必ず順番通りに実行すること:\\n  Step1: 記事テーマが決まったら「○○関連 低位株」「○○テーマ 小型株」でWeb検索し候補を3〜4社リストアップする\\n  Step2: 各候補について「企業名 証券コード」でWeb検索してコードを確認する（記憶でのコード出力は絶対禁止）\\n  Step3: 各候補について「証券コード 株価」でWeb検索して当日または前日終値を確認する\\n  Step4: 1000円未満の銘柄を注目株として採用する。複数ある場合は最も株価が低い銘柄を優先する\\n  Step5: 4社試して全て1000円超の場合は最も株価が低い銘柄を採用し、その旨をspotlight_reasonに記載する\\n  Step6: 各記事で異なる銘柄を選ぶこと。同じ銘柄の使い回しは禁止\\n・関連株Aについても「企業名 証券コード」でWeb検索してコードを確認してから出力すること\\n・【厳守】株価の具体的な数値・確認日・終値は一切出力に記載しないこと。「○月○日終値○○円確認済み」のような記述はspotlight_reasonを含む全フィールドで完全禁止。株価確認は選定目的のみ\\n・各銘柄に上昇/下降/横ばいの予測と50字以内の根拠を付ける\n\n【筆者コメントのルール】\n・各記事に「筆者の今日の一言」として異なるトーンの3パターンを生成すること\n・パターン1: 強気・煽り系（「これは乗り遅れたら一生後悔する」「今すぐ口座を開け」系）\n・パターン2: 中立・分析系（「両面を見て自分で判断する」「データが示す通り」系）\n・パターン3: 警戒・逆張り系（「みんなが強気のときこそ疑え」「ここに落とし穴がある」系）\n\n【X投稿文のルール】\n・各記事にX専用の投稿文を別途作成\n・冒頭は数字・驚き・問い・対立構造のいずれかで始める\n・銘柄名・証券コード・予測方向（↑↓→）を必ず含める\n・ハッシュタグは #日本株 #株式投資 #小型株 #個人投資家 を末尾に\n・280文字以内\n\n【記事カテゴリ】以下から1つ割り当て: 金融政策/半導体/エネルギー/海運/アクティビスト/決算/マクロ経済/為替/不動産/防衛・宇宙\n\n【その他条件】\n・記事は全て日本語、800〜1000字\n・過去に記事にした情報以外を選ぶ\n・3件全て一度に出力（選択待ち不要）'+avoidNote+'\n\n以下のJSON形式のみで出力（説明文不要・JSONだけ）:\n```json\n{"articles":[{"id":"1","title":"タイトル","summary":"概要100字","content":"本文800〜1000字","category":"カテゴリ","x_post":"X投稿文280字以内","author_comments":["強気系一言","中立系一言","警戒系一言"],"stock_a_name":"関連株A企業名","stock_a_ticker":"7203","stock_a_pred":"上昇","stock_a_reason":"根拠50字","spotlight_name":"注目株企業名","spotlight_ticker":"1234","spotlight_pred":"上昇","spotlight_reason":"ニュースとの因果関係と根拠50字","sources":["URL1","URL2","URL3"]},{"id":"2",...},{"id":"3",...}]}\n```';

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
      stockA:{name:a.stock_a_name,ticker:a.stock_a_ticker,prediction:a.stock_a_pred,reason:a.stock_a_reason},
      spotlight:{name:a.spotlight_name,ticker:a.spotlight_ticker,prediction:a.spotlight_pred,reason:a.spotlight_reason},
    },
    sources:Array.isArray(a.sources)?a.sources.filter(Boolean):[a.source].filter(Boolean),
  }));
}

function loadPaste(){
  const raw=document.getElementById('pasteText').value.trim();
  if(!raw){showErr('テキストが空です');return;}
  try{
    const js=extractJson(raw);
    const d=JSON.parse(js);
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
  document.querySelectorAll('.author-opt').forEach(el=>el.classList.remove('sel'));
  document.getElementById('aopt'+i).classList.add('sel');
  document.getElementById('authorOkBtn').disabled=false;
}

function confirmAuthor(){
  if(S.selAuthor===null||S.selIdx===null)return;
  let chosen='';
  if(typeof S.selAuthor==='string'&&S.selAuthor.startsWith('human_')){
    const idx=parseInt(S.selAuthor.replace('human_',''));
    chosen=HUMAN_TEMPLATES[idx]?.txt||'';
  } else {
    chosen=S.authorOpts[S.selAuthor]||'';
  }
  S.cands[S.selIdx].chosenComment=chosen;
  S.cands[S.selIdx].categoryHook=S.authorCategoryHook||getCategoryHook(S.cands[S.selIdx].category||'');
  finalPublish(S.cands[S.selIdx]);
}

function skipAuthor(){
  if(S.selIdx===null){renderCands();showSelect();return;}
  S.cands[S.selIdx].chosenComment='';
  S.cands[S.selIdx].categoryHook=S.authorCategoryHook||getCategoryHook(S.cands[S.selIdx].category||'');
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
            ${[a.relatedStocks.stockA,a.relatedStocks.spotlight].filter(s=>s&&s.name).map((s,i)=>`
              <span class="badge">${i===1?'<span style="color:#f59e0b;margin-right:2px">★</span>':''}<span style="color:#a0aec0">${s.name}</span><span style="color:${pc(s.prediction)};font-weight:700;margin-left:3px">${pi(s.prediction)}${s.prediction}</span></span>`).join('')}
          </div>
        </div>
      </div></div>`;
    el.appendChild(d);
  });
}

function selCand(i){S.selIdx=i;document.getElementById('pubBtn').disabled=false;renderCands();}

function doPublish(){
  if(S.selIdx===null)return;
  const cand=S.cands[S.selIdx];
  // Go to check flow first
  S.checkCand=cand;
  S.checkResult=null;
  S.fixedCand=null;
  startCheckFlow(cand);
}

function backToSelect(){showSelect();}

function showView(id){
  ['vHome','vSelect','vAuthor','vArticle','vCheck','vCheckResult','vDiff'].forEach(v=>{
    const el=document.getElementById(v);
    if(el)el.classList.add('hidden');
  });
  const target=document.getElementById(id);
  if(target)target.classList.remove('hidden');
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

// ── Check Flow ───────────────────────────────────────────
function startCheckFlow(cand){
  const artJson=JSON.stringify({articles:[{
    id:cand.id,title:cand.title,summary:cand.summary,content:cand.content,
    category:cand.category,x_post:cand.xPost,
    stock_a_name:cand.relatedStocks.stockA?.name,stock_a_ticker:cand.relatedStocks.stockA?.ticker,
    stock_a_pred:cand.relatedStocks.stockA?.prediction,stock_a_reason:cand.relatedStocks.stockA?.reason,
    spotlight_name:cand.relatedStocks.spotlight?.name,spotlight_ticker:cand.relatedStocks.spotlight?.ticker,
    spotlight_pred:cand.relatedStocks.spotlight?.prediction,spotlight_reason:cand.relatedStocks.spotlight?.reason,
    sources:cand.sources
  }]},null,2);

  const prompt=`以下の金融記事JSONをチェックしてください。

【チェック項目】
①コンプライアンス: 断定的な投資勧誘・誇大表現（「必ず上がる」「今すぐ買え」「絶対に儲かる」等）を検出
②ファクト: 数字・社名・証券コードの整合性（コードと社名が一致しているか）
③ソース: URLが実在しそうか、一次ソースか（公式サイト・主要メディアか）
④読みやすさ: 1段落が極端に長い・難解な専門用語の未説明・誤字脱字

【出力ルール】
・JSON形式のみで出力（説明文・マークダウン不要）
・severity: "error"（必ず修正）/"warn"（要確認）/"ok"（問題なし）
・問題がなければempty配列で返す

{"checks":[{"article_id":"1","type":"compliance","severity":"error","field":"content","issue":"問題の説明","suggestion":"修正案"},{"article_id":"1","type":"fact","severity":"ok","field":"stock_a_ticker","issue":"","suggestion":""}]}

===対象JSON===
${artJson}`;

  document.getElementById('checkPromptText').value=prompt;
  document.getElementById('checkResultText').value='';
  document.getElementById('checkErr').classList.add('hidden');
  showView('vCheck');
}

function copyCheckPrompt(){
  const t=document.getElementById('checkPromptText');t.select();t.setSelectionRange(0,99999);
  try{document.execCommand('copy');}catch(e){}
  try{navigator.clipboard.writeText(t.value).catch(()=>{});}catch(e){}
  const b=document.getElementById('cpCheckBtn');b.textContent='✅ コピーしました';
  setTimeout(()=>{b.textContent='📋 コピー';},2000);
}

function sanitizeJson(raw){
  return raw
    .replace(/\u201c|\u201d|\u2018|\u2019/g,'"') // 全角引用符→半角
    .replace(/[\u2018\u2019]/g,"'")                 // 全角シングルクォート→半角
    .replace(/\u2014|\u2013/g,'-')                  // 全角ダッシュ→半角
    .replace(/[\u00a0]/g,' ')                        // ノーブレークスペース→半角スペース
    .trim();
}

function extractJson(raw){
  // Try code block first
  const m=raw.match(/```(?:json)?\s*([\s\S]*?)```/);
  if(m)return sanitizeJson(m[1]);
  // Try first { ... } block
  const start=raw.indexOf('{');
  const end=raw.lastIndexOf('}');
  if(start!==-1&&end!==-1&&end>start)return sanitizeJson(raw.slice(start,end+1));
  return sanitizeJson(raw);
}

function loadCheckResult(){
  const raw=document.getElementById('checkResultText').value.trim();
  if(!raw){document.getElementById('checkErr').textContent='⚠️ テキストが空です';document.getElementById('checkErr').classList.remove('hidden');return;}
  try{
    const js=extractJson(raw);
    const d=JSON.parse(js);
    S.checkResult=d.checks||[];
    renderCheckResult();
    showView('vCheckResult');
  }catch(e){
    document.getElementById('checkErr').textContent='⚠️ 読み込み失敗: '+e.message+'（ヒント: ChatGPTの出力をそのままコピーしてください）';
    document.getElementById('checkErr').classList.remove('hidden');
  }
}

function skipCheck(){
  S.checkResult=[];
  proceedToAuthor();
}

function renderCheckResult(){
  const checks=S.checkResult||[];
  const errors=checks.filter(c=>c.severity==='error');
  const warns=checks.filter(c=>c.severity==='warn');
  const issues=checks.filter(c=>c.severity!=='ok'&&c.issue);

  // Summary
  const sumEl=document.getElementById('checkSummary');
  sumEl.innerHTML=`<div style="display:flex;gap:8px;margin-bottom:8px;">
    <span class="check-badge check-error">🔴 要修正 ${errors.length}件</span>
    <span class="check-badge check-warn">⚠️ 要確認 ${warns.length}件</span>
    <span class="check-badge check-ok">✅ 問題なし ${checks.filter(c=>c.severity==='ok').length}件</span>
  </div>`;

  // Issues list
  const listEl=document.getElementById('checkIssueList');
  if(issues.length===0){
    listEl.innerHTML='';
    document.getElementById('noIssuesSection').classList.remove('hidden');
    document.getElementById('fixPromptSection').classList.add('hidden');
    return;
  }
  document.getElementById('noIssuesSection').classList.add('hidden');
  document.getElementById('fixPromptSection').classList.remove('hidden');

  listEl.innerHTML=issues.map(c=>`
    <div style="background:var(--surface);border:1px solid ${c.severity==='error'?'rgba(239,68,68,.3)':'rgba(245,158,11,.3)'};border-radius:8px;padding:11px;margin-bottom:8px;">
      <div style="display:flex;align-items:center;gap:6px;margin-bottom:5px;">
        <span class="check-badge ${c.severity==='error'?'check-error':'check-warn'}">${c.severity==='error'?'🔴 要修正':'⚠️ 要確認'}</span>
        <span style="font-size:10px;color:var(--muted);font-family:var(--sans)">${c.type} / ${c.field}</span>
      </div>
      <div style="font-size:12px;color:var(--text);margin-bottom:4px">${c.issue}</div>
      ${c.suggestion?`<div style="font-size:11px;color:var(--accent2);font-family:var(--sans)">💡 ${c.suggestion}</div>`:''}
    </div>`).join('');

  // Build fix prompt
  const artJson=JSON.stringify({articles:[{
    id:S.checkCand.id,title:S.checkCand.title,summary:S.checkCand.summary,
    content:S.checkCand.content,category:S.checkCand.category,x_post:S.checkCand.xPost,
    stock_a_name:S.checkCand.relatedStocks.stockA?.name,stock_a_ticker:S.checkCand.relatedStocks.stockA?.ticker,
    stock_a_pred:S.checkCand.relatedStocks.stockA?.prediction,stock_a_reason:S.checkCand.relatedStocks.stockA?.reason,
    spotlight_name:S.checkCand.relatedStocks.spotlight?.name,spotlight_ticker:S.checkCand.relatedStocks.spotlight?.ticker,
    spotlight_pred:S.checkCand.relatedStocks.spotlight?.prediction,spotlight_reason:S.checkCand.relatedStocks.spotlight?.reason,
    sources:S.checkCand.sources
  }]},null,2);
  const checksJson=JSON.stringify({checks:issues},null,2);

  const fixPrompt=`以下の金融記事JSONをチェック結果に基づいて修正してください。

【修正ルール】
・severity:"error"は必ず修正する
・severity:"warn"は内容を判断して修正する
・修正したフィールドはchangesに記録する
・記事の論旨・銘柄選定・予測は変更しない
・金融商品取引法に抵触する断定表現を除去し「〜の可能性がある」「〜と考えられる」に変換

【出力形式】JSONのみ（説明文不要）:
{"articles":[{全フィールドを含む記事JSON,"changes":[{"field":"フィールド名","original":"修正前の文","revised":"修正後の文","reason":"修正理由"}]}]}

===元の記事JSON===
${artJson}

===チェック結果===
${checksJson}`;

  document.getElementById('fixPromptText').value=fixPrompt;
}

function copyFixPrompt(){
  const t=document.getElementById('fixPromptText');t.select();t.setSelectionRange(0,99999);
  try{document.execCommand('copy');}catch(e){}
  try{navigator.clipboard.writeText(t.value).catch(()=>{});}catch(e){}
  const b=document.getElementById('cpFixBtn');b.textContent='✅ コピーしました';
  setTimeout(()=>{b.textContent='📋 コピー';},2000);
}

function loadFixResult(){
  const raw=document.getElementById('fixResultText').value.trim();
  if(!raw){alert('テキストが空です');return;}
  try{
    // Strict: only extract content between first { and last }
    const start=raw.indexOf('{');
    const end=raw.lastIndexOf('}');
    if(start===-1||end===-1||end<=start)throw new Error('JSONが見つかりません。{...}の形式で貼り付けてください');
    const js=sanitizeJson(raw.slice(start,end+1));
    const d=JSON.parse(js);
    if(!d.articles?.length)throw new Error('articles が見つかりません');
    const fixed=d.articles[0];
    // Build fixedCand preserving relatedStocks from original
    S.fixedCand={
      ...S.checkCand,
      title:fixed.title||S.checkCand.title,
      summary:fixed.summary||S.checkCand.summary,
      content:fixed.content||S.checkCand.content,
      xPost:fixed.x_post||S.checkCand.xPost,
      category:fixed.category||S.checkCand.category,
      authorComments:fixed.author_comments||S.checkCand.authorComments,
      // Rebuild relatedStocks from fixed JSON fields
      relatedStocks:{
        stockA:{
          name:fixed.stock_a_name||S.checkCand.relatedStocks?.stockA?.name,
          ticker:fixed.stock_a_ticker||S.checkCand.relatedStocks?.stockA?.ticker,
          prediction:fixed.stock_a_pred||S.checkCand.relatedStocks?.stockA?.prediction,
          reason:fixed.stock_a_reason||S.checkCand.relatedStocks?.stockA?.reason,
        },
        spotlight:{
          name:fixed.spotlight_name||S.checkCand.relatedStocks?.spotlight?.name,
          ticker:fixed.spotlight_ticker||S.checkCand.relatedStocks?.spotlight?.ticker,
          prediction:fixed.spotlight_pred||S.checkCand.relatedStocks?.spotlight?.prediction,
          reason:fixed.spotlight_reason||S.checkCand.relatedStocks?.spotlight?.reason,
        }
      },
      sources:fixed.sources||S.checkCand.sources,
      changes:fixed.changes||[]
    };
    renderDiff(fixed.changes||[]);
    showView('vDiff');
  }catch(e){
    alert('読み込み失敗: '+e.message+'\n\nヒント: JSONの{...}部分だけを貼り付けてください。説明文や```は不要です。');
  }
}

function renderDiff(changes){
  const el=document.getElementById('diffList');
  if(!changes.length){
    el.innerHTML='<div class="empty">変更箇所がありませんでした</div>';
    return;
  }
  el.innerHTML=changes.map(c=>`
    <div class="diff-block">
      <div style="background:rgba(99,179,237,.08);padding:6px 12px;font-size:9px;color:var(--accent2);font-family:var(--sans);font-weight:700;">
        📝 ${c.field} — ${c.reason||''}
      </div>
      <div class="diff-orig">
        <div class="diff-label" style="color:var(--down)">🔴 修正前</div>
        <div class="diff-text" style="color:#fc8181">${esc(c.original||'')}</div>
      </div>
      <div class="diff-new">
        <div class="diff-label" style="color:var(--up)">✅ 修正後</div>
        <div class="diff-text" style="color:#68d391">${esc(c.revised||'')}</div>
      </div>
    </div>`).join('');
}

function skipFix(){proceedToAuthor();}

function rejectFix(){
  if(!confirm('この記事を破棄しますか？'))return;
  S.checkCand=null;S.checkResult=null;S.fixedCand=null;
  showSelect();
}

function approveFix(){
  if(!S.fixedCand){proceedToAuthor();return;}
  // Replace checkCand with fixedCand
  if(S.selIdx!==null)S.cands[S.selIdx]={...S.cands[S.selIdx],...S.fixedCand};
  S.checkCand=S.cands[S.selIdx];
  proceedToAuthor();
}

function proceedToAuthor(){
  const cand=S.fixedCand||S.checkCand||S.cands[S.selIdx];
  if(!cand)return;
  if(cand.authorComments&&cand.authorComments.length>0){
    showAuthorForArticle(cand);
    return;
  }
  finalPublish(cand);
}

function finalPublish(cand){
  const art={...cand,publishedAt:new Date().toLocaleDateString('ja-JP')};
  // Save chosen comment back to cand
  if(S.selIdx!==null)S.cands[S.selIdx].chosenComment=art.chosenComment;
  // Add predictions to tracker
  ['stockA','spotlight'].forEach(k=>{
    const s=art.relatedStocks[k];
    if(s&&s.name){
      const pubDate=new Date();
      const deadline=new Date(pubDate.getTime()+7*24*3600000);
      const deadlineStr=deadline.toLocaleDateString('ja-JP',{month:'numeric',day:'numeric'});
      const predId=Date.now()+'_'+k;
      S.preds.push({id:predId,name:s.name,ticker:s.ticker,pred:s.prediction,reason:s.reason,artTitle:art.title,date:art.publishedAt,deadline:deadlineStr,deadlineTs:deadline.getTime(),result:'pending'});
      // Fetch baseline price asynchronously
      if(S.jqToken){
        fetchPrice(s.ticker).then(data=>{
          if(data){S.baselinePrices[predId]=data.latest;DB.s('mi_baselines',S.baselinePrices);}
        });
      }
    }
  });
  DB.s('mi_preds',S.preds);
  S.pub.unshift(art);DB.s('mi_pub',S.pub);
  S.curArt=art;S.backFrom='select';
  document.getElementById('artBody').innerHTML=buildArtHTML(art);
  ['vHome','vSelect','vAuthor','vCheck','vCheckResult','vDiff'].forEach(id=>{const el=document.getElementById(id);if(el)el.classList.add('hidden');});
  document.getElementById('vArticle').classList.remove('hidden');
  updateStatus();
  loadPricesForArticle(art);
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
  loadPricesForArticle(S.curArt);
}
function backPub(){document.getElementById('vArtPub').classList.add('hidden');renderPubList();}

// ── Prediction tracker ────────────────────────────────────
function renderTrack(){
  const now=new Date().getTime();
  const hits=S.preds.filter(p=>p.result==='hit').length;
  const misses=S.preds.filter(p=>p.result==='miss').length;
  const pend=S.preds.filter(p=>p.result==='pending').length;
  const due=S.preds.filter(p=>p.result==='pending'&&p.deadlineTs&&now>=p.deadlineTs).length;
  const total=hits+misses;
  document.getElementById('trackHit').textContent=hits;
  document.getElementById('trackMiss').textContent=misses;
  document.getElementById('trackPend').textContent=pend;
  document.getElementById('trackRate').textContent=total>0?Math.round(hits/total*100)+'%':'-%';

  // Show due badge on tab if any are overdue
  const tab=document.querySelector('.tab[onclick*="track"]');
  if(tab)tab.textContent=due>0?`予測 ⏰${due}`:'予測';

  const el=document.getElementById('trackList');
  if(!S.preds.length){el.innerHTML='<div class="empty">記事を公開すると予測が自動登録されます<br><span style="font-size:10px;color:#2d3748;font-family:var(--sans)">公開から1週間後に判定期限が自動設定されます</span></div>';return;}

  // Sort: due first, then pending, then judged
  const sorted=[...S.preds.entries()].sort(([_a,a],[_b,b])=>{
    if(a.result==='pending'&&b.result!=='pending')return -1;
    if(a.result!=='pending'&&b.result==='pending')return 1;
    return (b.deadlineTs||0)-(a.deadlineTs||0);
  });

  el.innerHTML=sorted.map(([ri,p])=>{
    const isDue=p.result==='pending'&&p.deadlineTs&&now>=p.deadlineTs;
    const daysLeft=p.deadlineTs?Math.ceil((p.deadlineTs-now)/(24*3600000)):null;
    const deadlineInfo=p.deadline?`判定期限: ${p.deadline}`:'';
    const timeLabel=p.result==='pending'?(
      isDue?'<span style="color:var(--flat);font-weight:700">⏰ 判定期限です！</span>':
      daysLeft!==null?`<span style="color:var(--muted);font-size:9px">${deadlineInfo}（残${daysLeft}日）</span>`:
      `<span style="color:var(--muted);font-size:9px">${deadlineInfo}</span>`
    ):`<span style="font-size:9px;color:var(--muted)">${p.date}予測</span>`;

    return `<div class="track-row" style="${isDue?'background:rgba(250,204,21,0.04);border-radius:8px;padding:8px;margin-bottom:2px;':''}">
      <div style="flex:1;min-width:0">
        <div class="track-name">${isDue?'⏰ ':''} ${p.name} <span style="font-size:10px;color:var(--muted)">${p.ticker}</span></div>
        <div class="track-pred">${pi(p.pred)}${p.pred}</div>
        <div style="margin-top:2px">${timeLabel}</div>
      </div>
      <div style="display:flex;gap:5px;align-items:center;flex-shrink:0;margin-left:8px">
        ${p.result==='pending'?`
          <button onclick="setPred(${ri},'hit')" style="padding:5px 10px;border-radius:5px;border:none;background:rgba(34,197,94,.15);color:var(--up);font-size:11px;cursor:pointer;font-family:var(--sans);font-weight:700;">✓ 的中</button>
          <button onclick="setPred(${ri},'miss')" style="padding:5px 10px;border-radius:5px;border:none;background:rgba(239,68,68,.15);color:var(--down);font-size:11px;cursor:pointer;font-family:var(--sans);font-weight:700;">✗ 外れ</button>
        `:`<div style="text-align:right"><span class="track-result ${p.result==='hit'?'track-hit':'track-miss'}">${p.result==='hit'?'✓ 的中':'✗ 外れ'}</span>${p.autoJudged?`<div style="font-size:9px;color:var(--muted);margin-top:2px;font-family:var(--sans)">${p.changePct>0?'+':''}${p.changePct}% 自動判定</div>`:''}</div>`}
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
  const weekStr=new Date().toLocaleDateString('ja-JP',{month:'numeric',day:'numeric'});
  const txt=`【週次予測レポート ${weekStr}】\n\n直近${total}件の1週間予測\n的中率: ${rate}%（${hits}勝${total-hits}敗）\n\n最近の的中予測:\n${recent}\n\n毎日1銘柄の予測を配信中📊\nフォローして投資の精度を上げてください。\n\n#日本株 #株式投資 #個人投資家 #小型株`;
  const el=document.getElementById('trackPost');
  el.innerHTML=`<div class="ex-block"><div class="ex-lbl">🐦 X投稿文</div><div class="ex-txt" id="tpTxt">${txt}</div><div style="display:flex;gap:6px;margin-top:7px;"><button class="cp-btn" style="flex:1;" onclick="doCopy('tpTxt',this)">📋 コピー</button><button class="btn btn-x" style="flex:1;padding:7px;font-size:11px;border-radius:7px;" onclick="openX('tpTxt')">𝕏 投稿する</button></div></div>`;
  el.classList.remove('hidden');
}

// ── Live price loader ────────────────────────────────────
async function loadPricesForArticle(art){
  if(!S.jqToken)return;
  const stocks=[art.relatedStocks.stockA,art.relatedStocks.spotlight].filter(s=>s&&s.name&&s.ticker);
  for(const s of stocks){
    updatePriceBadge(s.ticker,'株価取得中...',null,null);
    const data=await fetchPriceWithChange(s.ticker);
    if(data){
      updatePriceBadge(s.ticker,data.price,data.change,data.changePct,data);
    } else {
      updatePriceBadge(s.ticker,'取得失敗',null,null,null);
    }
  }
}

async function fetchPriceWithChange(ticker){
  const token=await getJQToken();
  if(!token)return null;
  // Fetch 30 days to always find the latest available close price
  const to=new Date().toISOString().slice(0,10).replace(/-/g,'');
  const from=new Date(Date.now()-30*24*3600000).toISOString().slice(0,10).replace(/-/g,'');
  // J-Quants uses 4-digit codes directly (NOT 5-digit)
  // For codes like 464A, use as-is; for 4-digit numeric, use as-is
  const code=ticker.replace(/[^0-9A-Za-z]/g,'');
  try{
    // Try auth refresh if token might be expired
    const freshToken=await getJQToken();
    const res=await fetch(`https://api.jquants.com/v1/prices/daily_quotes?code=${code}&from=${from}&to=${to}`,{
      headers:{Authorization:freshToken}
    });
    if(!res.ok){
      // Log error for debugging
      console.warn('J-Quants API error:',res.status,'for',code);
      return null;
    }
    const d=await res.json();
    const quotes=(d.daily_quotes||[]).filter(q=>q.Close!==null).sort((a,b)=>b.Date.localeCompare(a.Date));
    if(quotes.length<1)return null;
    const latest=quotes[0];
    const prev=quotes.length>1?quotes[1]:null;
    const price=latest.Close;
    const change=prev?price-prev.Close:0;
    const changePct=prev?((price-prev.Close)/prev.Close*100):0;
    return{price,change,changePct,date:latest.Date};
  }catch(e){
    console.warn('fetchPriceWithChange error:',e,ticker);
    return null;
  }
}

function updatePriceBadge(ticker,price,change,changePct,data){
  // Update all elements with this ticker (stockA and spotlight may share)
  document.querySelectorAll(`#price_${ticker}`).forEach(el=>{
    if(price===null||price==='株価取得中...'||price==='取得失敗'){
      el.innerHTML=`<span class="${price==='株価取得中...'?'price-loading':''}" style="font-size:10px;color:var(--muted)">${price}</span>`;
      return;
    }
    const fmt=new Intl.NumberFormat('ja-JP').format(price);
    const sign=change>=0?'+':'';
    const cls=change>0?'price-chg-up':change<0?'price-chg-down':'price-chg-flat';
    const arrow=change>0?'▲':change<0?'▼':'－';
    // Format date for display (YYYYMMDD → M/D)
    const dateStr=data&&data.date?data.date.replace(/(\d{4})(\d{2})(\d{2})/,(_,y,m,d)=>`${parseInt(m)}/${parseInt(d)}終値`):'終値';
    el.innerHTML=`
      <span class="price-val">${fmt}円</span>
      <span class="${cls}">${arrow}${sign}${changePct.toFixed(1)}%</span>
      <span style="font-size:9px;color:var(--muted);margin-left:2px">${dateStr}</span>
    `;
  });
}

// ── Article HTML builder ──────────────────────────────────
function buildArtHTML(a){
  const stocks=[{l:'関連株A',s:a.relatedStocks.stockA,star:false},{l:'★ 注目株',s:a.relatedStocks.spotlight,star:true}].filter(x=>x.s&&x.s.name);
  const xTxt=buildX(a);
  const freeNote=buildFreeNote(a);
  const paidNote=buildPaidNote(a);
  const affHtml=buildAffHtml(a);

  return `
    ${a.category?`<div style="display:inline-block;background:rgba(99,179,237,.15);border:1px solid rgba(99,179,237,.3);border-radius:5px;padding:2px 9px;font-size:10px;color:var(--accent2);font-family:var(--sans);margin-bottom:8px;">${a.category}</div>`:''}
    <h1 style="font-size:18px;font-weight:900;line-height:1.55;margin-bottom:10px">${a.title}</h1>

    <div style="background:rgba(250,204,21,.06);border:1px solid rgba(250,204,21,.2);border-radius:10px;padding:12px 14px;margin-bottom:14px;">
      <div style="font-size:11px;font-weight:700;color:#f59e0b;font-family:var(--sans);margin-bottom:${a.chosenComment?'8px':'0'}">
        📱 ${a.categoryHook||'今日のニュースをAIに分析させてみた'}
      </div>
      ${a.chosenComment?`<div style="font-size:12px;line-height:1.8;color:#fef3c7;font-style:italic;border-top:1px solid rgba(250,204,21,.15);padding-top:7px;margin-top:2px;">「${a.chosenComment}」</div>`:''}
    </div>

    <div class="card mb12" style="background:rgba(99,179,237,.05);border-color:rgba(99,179,237,.25)">
      <div class="lbl">概要</div>
      <div style="font-size:12px;line-height:1.8;color:#cbd5e0">${a.summary}</div>
    </div>
    <div style="font-size:13px;line-height:2.1;margin-bottom:18px;white-space:pre-line">${a.content}</div>

    <div class="stocks-box">
      <div class="s-hd">📊 関連銘柄・株価予測</div>
      ${stocks.map(({l,s,star})=>`
        <div class="s-row" style="${star?'background:rgba(250,204,21,0.04);':''}" >
          <div style="flex:1;min-width:0">
            <div style="font-size:9px;color:${star?'#f59e0b':'var(--muted)'};margin-bottom:2px;font-family:var(--sans);font-weight:${star?'700':'400'}">${l}</div>
            <div style="font-size:13px;font-weight:700;margin-bottom:2px">${s.name} <span style="font-size:10px;color:var(--muted)">${s.ticker}</span></div>
            <div style="font-size:10px;color:#a0aec0;line-height:1.6;margin-bottom:4px">${s.reason}</div>
            <div class="price-badge" id="price_${s.ticker}">
              <span class="price-loading">株価取得中...</span>
            </div>
          </div>
          <div class="pred-box" style="background:${pc(s.prediction)}20;border:1px solid ${pc(s.prediction)}40;margin-left:8px">
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
        <div style="font-size:11px;color:#a0aec0;font-family:var(--sans);line-height:1.7">全文・詳細分析・毎日配信</div>
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
    const sa=a.relatedStocks.stockA,sp=a.relatedStocks.spotlight;
    base=a.title.replace(/——.*$/,'')+'\n\n'+a.content.split('\n')[0].slice(0,60)+'…\n\n'+(sa&&sa.name?'📌 '+sa.name+'('+sa.ticker+') '+pi(sa.prediction)+sa.prediction:'')+(sp&&sp.name?'\n★注目: '+sp.name+'('+sp.ticker+') '+pi(sp.prediction)+sp.prediction:'');
  }
  if(a.chosenComment)base='「'+a.chosenComment.slice(0,30)+'」\n\n'+base;
  if(!base.includes('#日本株'))base+='\n\n#日本株 #株式投資 #小型株 #個人投資家';
  return base.length>280?base.slice(0,276)+'...':base;
}

function buildFreeNote(a){
  const noteUrl=S.noteUrl||'https://note.com/';
  const ctaMap={'金融政策':'利上げ局面の投資戦略','半導体':'AI・半導体相場の深掘り分析','エネルギー':'原油・エネルギー相場の先読み','為替':'円安円高を先読みする分析','防衛・宇宙':'防衛・次世代エネルギーテーマ株分析'};
  const ctaTheme=ctaMap[a.category]||'最新の株式市場分析';
  const hook=a.categoryHook||getCategoryHook(a.category||'');
  const comment=`\n\n---\n\n**📱 ${hook}**${a.chosenComment?'\n\n> 「'+a.chosenComment+'」':''}\n`;
  const stocks=[{l:'関連株A',s:a.relatedStocks.stockA},{l:'★注目株',s:a.relatedStocks.spotlight}].filter(x=>x.s&&x.s.name);
  const tbl=stocks.map(({l,s})=>`| ${l} | ${s.name} | ${s.ticker} | ${pi(s.prediction)}${s.prediction} |`).join('\n');
  return `# ${a.title}\n${comment}\n## 概要\n${a.summary}\n\n---\n\n## 関連銘柄・株価予測\n\n| 区分 | 銘柄 | コード | 予測 |\n|------|------|--------|------|\n${tbl}\n\n---\n\n> 💎 **全文・詳細分析は有料マガジンで**\n> ${ctaTheme}を毎日配信中 → [AI金融アナリスト通信](${noteUrl})\n> 月額980円 | いつでも解約可能\n\n---\n\n*本記事はAIによる分析を含みます。投資判断はご自身の責任で行ってください。*`;
}

function buildPaidNote(a){
  const noteUrl=S.noteUrl||'https://note.com/';
  const aff=buildAffMd(a);
  const hook=a.categoryHook||getCategoryHook(a.category||'');
  const comment=`\n\n---\n\n**📱 ${hook}**${a.chosenComment?'\n\n> 「'+a.chosenComment+'」':''}\n`;
  const stocks=[{l:'関連株A',s:a.relatedStocks.stockA,star:false},{l:'★ 注目株',s:a.relatedStocks.spotlight,star:true}].filter(x=>x.s&&x.s.name);
  const tbl=stocks.map(({l,s})=>`| ${l} | ${s.name} | ${s.ticker} | ${pi(s.prediction)}${s.prediction} | ${s.reason} |`).join('\n');
  return `# ${a.title}\n${comment}\n## 概要\n${a.summary}\n\n---\n\n${a.content}\n\n---\n\n## 関連銘柄・株価予測\n\n| 区分 | 銘柄 | コード | 予測 | 根拠 |\n|------|------|--------|------|------|\n${tbl}\n\n${a.sources?.length?'**参照元（'+a.sources.length+'件）:** '+a.sources.join(' / '):''}\n\n---\n${aff}\n> 💡 この記事が役に立ったら「スキ」をお願いします！\n> フォロー＆マガジン購読で毎日の分析をお届けします → [AI金融アナリスト通信](${noteUrl})\n\n*本記事はAIによる分析を含みます。投資判断はご自身の責任で行ってください。*`;
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

function saveJQ(){
  const t=document.getElementById('jqToken').value.trim();
  S.jqToken=t;DB.s('mi_jqtoken',t);
  if(t){
    document.getElementById('jqStatus').textContent='✅ 保存しました。次回アプリ起動時から自動判定が有効になります。';
    document.getElementById('jqStatus').style.color='var(--up)';
  } else {
    document.getElementById('jqStatus').textContent='APIキーが空です';
  }
}

// ── J-Quants API ──────────────────────────────────────────
async function getJQToken(){
  // Try refresh token first
  if(S.jqRefreshToken){
    try{
      const res=await fetch('https://api.jquants.com/v1/token/auth_refresh?refreshtoken='+encodeURIComponent(S.jqRefreshToken));
      if(res.ok){
        const d=await res.json();
        if(d.idToken){S.jqToken='Bearer '+d.idToken;DB.s('mi_jqtoken',S.jqToken);return S.jqToken;}
      }
    }catch(e){}
  }
  return S.jqToken;
}

async function fetchPrice(ticker){
  const token=await getJQToken();
  if(!token)return null;
  // Get last 10 days of daily prices
  const to=new Date().toISOString().slice(0,10).replace(/-/g,'');
  const from=new Date(Date.now()-14*24*3600000).toISOString().slice(0,10).replace(/-/g,'');
  const code=ticker.replace(/[^0-9A-Za-z]/g,''); // J-Quants uses 4-digit codes as-is
  try{
    const res=await fetch(`https://api.jquants.com/v1/prices/daily_quotes?code=${code}&from=${from}&to=${to}`,{
      headers:{Authorization:token}
    });
    if(!res.ok)return null;
    const d=await res.json();
    const quotes=d.daily_quotes||[];
    if(!quotes.length)return null;
    // Return latest close price
    quotes.sort((a,b)=>b.Date.localeCompare(a.Date));
    return {latest:quotes[0].Close, date:quotes[0].Date, earliest:quotes[quotes.length-1].Close};
  }catch(e){return null;}
}

async function autoJudgeAll(){
  const now=Date.now();
  const duePreds=S.preds.filter(p=>p.result==='pending'&&p.deadlineTs&&now>=p.deadlineTs);
  if(!duePreds.length)return;

  // Show auto-judging indicator on track tab
  const tab=document.querySelector('.tab[onclick*="track"]');
  if(tab)tab.textContent='予測 ⏳';

  let judged=0;
  for(const p of duePreds){
    const priceData=await fetchPrice(p.ticker);
    if(!priceData)continue;

    // Get baseline price (price at time of prediction)
    const baseline=S.baselinePrices[p.id]||priceData.earliest;
    const current=priceData.latest;
    const changePct=(current-baseline)/baseline*100;

    let result='pending';
    if(p.pred==='上昇'&&changePct>1)result='hit';
    else if(p.pred==='上昇'&&changePct<=-1)result='miss';
    else if(p.pred==='下降'&&changePct<-1)result='hit';
    else if(p.pred==='下降'&&changePct>=1)result='miss';
    else if(p.pred==='横ばい'&&Math.abs(changePct)<=3)result='hit';
    else if(p.pred==='横ばい'&&Math.abs(changePct)>3)result='miss';

    if(result!=='pending'){
      const idx=S.preds.findIndex(x=>x.id===p.id);
      if(idx>=0){
        S.preds[idx].result=result;
        S.preds[idx].autoJudged=true;
        S.preds[idx].judgedPrice=current;
        S.preds[idx].baselinePrice=baseline;
        S.preds[idx].changePct=changePct.toFixed(1);
        judged++;
      }
    }
  }

  DB.s('mi_preds',S.preds);
  if(judged>0){
    const remaining=S.preds.filter(p=>p.result==='pending'&&p.deadlineTs&&now>=p.deadlineTs).length;
    if(tab)tab.textContent=remaining>0?`予測 ⏰${remaining}`:'予測';
    renderTrack();
  } else {
    const stillDue=S.preds.filter(p=>p.result==='pending'&&p.deadlineTs&&now>=p.deadlineTs).length;
    if(tab)tab.textContent=stillDue>0?`予測 ⏰${stillDue}`:'予測';
  }
}
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
