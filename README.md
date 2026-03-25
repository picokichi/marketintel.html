<!DOCTYPE html>

<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes, viewport-fit=cover">
    <title>桶屋ストーリーAI - 低位株アナリスト</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }

```
    :root {
        --navy: #1e3c72;
        --navy-dark: #0f2b4f;
        --navy-light: #f0f4fa;
        --green: #10b981;
        --amber: #f59e0b;
        --slate: #475569;
        --border: #e2edf7;
        --bg: #f5f7fb;
        --card: #ffffff;
    }

    body {
        background: var(--bg);
        font-family: -apple-system, BlinkMacSystemFont, 'Hiragino Sans', 'Yu Gothic', sans-serif;
        padding: 16px;
        color: #1e293b;
        font-size: 16px;
        line-height: 1.6;
    }

    .container { max-width: 600px; margin: 0 auto; }

    .app-header {
        text-align: center;
        padding: 20px 0 16px;
        margin-bottom: 8px;
    }
    .app-header h1 {
        font-size: 22px;
        font-weight: 800;
        color: var(--navy);
        letter-spacing: -0.5px;
    }
    .app-header p {
        font-size: 13px;
        color: var(--slate);
        margin-top: 4px;
    }

    .card {
        background: var(--card);
        border-radius: 20px;
        padding: 20px;
        margin-bottom: 16px;
        box-shadow: 0 2px 8px rgba(0,0,0,0.04);
        border: 1px solid #eef2f6;
    }

    /* ステップナビ */
    .step-nav {
        display: flex;
        justify-content: space-between;
        align-items: center;
        background: white;
        border-radius: 16px;
        padding: 12px 16px;
        margin-bottom: 16px;
        border: 1px solid var(--border);
        overflow-x: auto;
        gap: 4px;
    }
    .step-dot {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 4px;
        min-width: 44px;
    }
    .step-circle {
        width: 28px;
        height: 28px;
        border-radius: 50%;
        background: #e2e8f0;
        color: #94a3b8;
        font-size: 12px;
        font-weight: 700;
        display: flex;
        align-items: center;
        justify-content: center;
        transition: all 0.3s;
    }
    .step-circle.active { background: var(--navy); color: white; }
    .step-circle.done { background: var(--green); color: white; }
    .step-label {
        font-size: 10px;
        color: #94a3b8;
        text-align: center;
        white-space: nowrap;
    }
    .step-label.active { color: var(--navy); font-weight: 600; }
    .step-connector { flex: 1; height: 1px; background: #e2e8f0; min-width: 8px; }

    /* ボタン */
    .btn-primary, .btn-secondary, .btn-small, .btn-danger {
        cursor: pointer;
        transition: all 0.2s ease;
        border: none;
        border-radius: 44px;
        font-weight: 600;
        text-align: center;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        gap: 6px;
    }
    .btn-primary {
        background: var(--navy);
        color: white;
        padding: 14px 20px;
        font-size: 16px;
        width: 100%;
    }
    .btn-primary:active { background: var(--navy-dark); transform: scale(0.98); }
    .btn-primary:disabled { opacity: 0.5; pointer-events: none; }
    .btn-secondary {
        background: #f1f5f9;
        color: var(--navy);
        border: 1px solid #cbd5e1;
        padding: 12px 16px;
        font-size: 14px;
    }
    .btn-secondary:active { background: #e2e8f0; }
    .btn-small {
        background: #f1f5f9;
        color: var(--navy);
        border: 1px solid #cbd5e1;
        padding: 8px 14px;
        font-size: 13px;
    }
    .btn-small:active { background: #e6edf4; }
    .btn-danger {
        background: #fee2e2;
        color: #991b1b;
        border: 1px solid #fecaca;
        padding: 8px 14px;
        font-size: 13px;
    }

    textarea {
        width: 100%;
        padding: 14px;
        border-radius: 16px;
        border: 1px solid #cfdfed;
        font-family: 'SF Mono', 'Menlo', monospace;
        font-size: 13px;
        background: #fafcff;
        resize: vertical;
        line-height: 1.5;
    }

    .label {
        font-weight: 700;
        margin-bottom: 8px;
        font-size: 14px;
        color: #334155;
        display: flex;
        align-items: center;
        gap: 6px;
    }

    .flex-btns {
        display: flex;
        gap: 10px;
        margin-top: 12px;
        flex-wrap: wrap;
    }

    /* シナリオカード */
    .scenario-grid { display: flex; flex-direction: column; gap: 14px; margin: 14px 0; }
    .scenario-card {
        background: white;
        border: 2px solid var(--border);
        border-radius: 20px;
        padding: 16px;
        cursor: pointer;
        transition: all 0.2s;
        position: relative;
    }
    .scenario-card:active { transform: scale(0.99); }
    .scenario-card.selected { border-color: var(--navy); background: var(--navy-light); }
    .scenario-card.used {
        opacity: 0.55;
        background: #f8fafc;
        cursor: not-allowed;
        border-color: #cbd5e1;
    }
    .scenario-card.used::after {
        content: "✓ 使用済み";
        position: absolute;
        top: 12px; right: 12px;
        background: #94a3b8;
        color: white;
        padding: 3px 10px;
        border-radius: 20px;
        font-size: 11px;
        font-weight: 600;
    }
    .scenario-header {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        gap: 8px;
        margin-bottom: 10px;
        padding-right: 84px;
    }
    .scenario-title { font-weight: 700; font-size: 16px; line-height: 1.4; }
    .probability {
        position: absolute;
        top: 16px; right: 16px;
        background: var(--green);
        color: white;
        padding: 4px 12px;
        border-radius: 30px;
        font-size: 12px;
        font-weight: 700;
        white-space: nowrap;
    }
    .probability-low { background: var(--amber); }
    .scenario-chain {
        font-size: 13px;
        color: var(--slate);
        margin-bottom: 10px;
        padding: 8px 10px;
        background: #f8fafc;
        border-radius: 10px;
        line-height: 1.5;
    }
    .scenario-metaphor { font-size: 13px; color: var(--navy); font-style: italic; margin-bottom: 8px; }
    .scenario-stocks { font-size: 12px; color: #5b6e8c; }

    /* 記事プレビュー */
    .story-highlight {
        background: linear-gradient(135deg, #fef9e6, #fff4e0);
        border-left: 4px solid #f5b042;
        padding: 14px 16px;
        border-radius: 14px;
        margin: 12px 0;
        font-size: 15px;
        line-height: 1.7;
    }
    .metaphor-badge {
        background: #eef2ff;
        padding: 5px 12px;
        border-radius: 40px;
        display: inline-block;
        font-size: 12px;
        color: var(--navy);
        margin-bottom: 10px;
        font-weight: 600;
    }
    .news-item {
        background: #f8fafc;
        padding: 12px;
        border-radius: 12px;
        margin-bottom: 8px;
        border-left: 3px solid #cbd5e1;
        font-size: 14px;
    }
    .stock-card {
        background: #f8fafc;
        border-radius: 14px;
        padding: 14px;
        margin-top: 10px;
        border: 1px solid var(--border);
        font-size: 14px;
    }

    /* トラッカー */
    .tracker-item {
        background: white;
        border-radius: 14px;
        padding: 14px;
        margin-bottom: 10px;
        border: 1px solid var(--border);
        font-size: 14px;
    }
    .status-badge {
        display: inline-block;
        padding: 3px 12px;
        border-radius: 20px;
        font-size: 12px;
        font-weight: 600;
    }
    .status-pending { background: #fef9c3; color: #854d0e; }
    .status-hit { background: #dcfce7; color: #166534; }
    .status-miss { background: #fee2e2; color: #991b1b; }

    .alert-banner {
        background: #fef3c7;
        border-left: 4px solid var(--amber);
        padding: 12px 14px;
        border-radius: 12px;
        margin-bottom: 14px;
        font-size: 14px;
    }

    /* 履歴 */
    .history-item {
        background: #f8fafc;
        padding: 10px 12px;
        border-radius: 12px;
        margin-bottom: 8px;
        font-size: 13px;
        border-left: 3px solid #cbd5e1;
    }
    .history-date { font-size: 11px; color: #94a3b8; margin-top: 3px; }

    .footer-note {
        font-size: 12px;
        text-align: center;
        color: #7e8b9e;
        margin-top: 12px;
        line-height: 1.5;
    }
    hr { margin: 16px 0; border: 0; height: 1px; background: #e2e8f0; }

    .summary-box {
        background: #f1f5f9;
        border-radius: 12px;
        padding: 12px 14px;
        margin-bottom: 14px;
        font-size: 14px;
    }

    /* セルフチェックパネル */
    .selfcheck-panel {
        background: linear-gradient(135deg, #0f2b4f, #1e3c72);
        border-radius: 20px;
        padding: 20px;
        margin-bottom: 16px;
        color: white;
    }
    .selfcheck-panel h3 { font-size: 17px; margin-bottom: 14px; }
    .score-row {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 10px 0;
        border-bottom: 1px solid rgba(255,255,255,0.1);
        font-size: 14px;
    }
    .score-row:last-child { border-bottom: none; }
    .score-val {
        font-weight: 700;
        font-size: 16px;
        min-width: 50px;
        text-align: right;
    }
    .score-good { color: #6ee7b7; }
    .score-warn { color: #fcd34d; }
    .score-bad { color: #fca5a5; }
    .loading-dots::after {
        content: '';
        animation: dots 1.2s steps(4, end) infinite;
    }
    @keyframes dots {
        0%,20% { content: ''; }
        40% { content: '.'; }
        60% { content: '..'; }
        80%,100% { content: '...'; }
    }

    /* 折りたたみ */
    .collapsible-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        cursor: pointer;
        user-select: none;
    }
    .collapsible-header .toggle-icon {
        font-size: 12px;
        color: #94a3b8;
        transition: transform 0.2s;
    }
    .collapsible-header.open .toggle-icon { transform: rotate(180deg); }
    .collapsible-body { margin-top: 12px; }

    /* タグ */
    .tag {
        display: inline-block;
        padding: 3px 10px;
        border-radius: 20px;
        font-size: 11px;
        font-weight: 600;
        background: #eef2ff;
        color: var(--navy);
        margin-right: 4px;
        margin-top: 4px;
    }
</style>
```

</head>
<body>
<div class="container">

```
<!-- ヘッダー -->
<div class="app-header">
    <h1>🏺 桶屋ストーリーAI</h1>
    <p>因果関係の連鎖で読み解く低位株アナリスト</p>
</div>

<!-- ステップナビ -->
<div class="step-nav">
    <div class="step-dot">
        <div class="step-circle active" id="sc1">1</div>
        <div class="step-label active" id="sl1">生成</div>
    </div>
    <div class="step-connector"></div>
    <div class="step-dot">
        <div class="step-circle" id="sc2">2</div>
        <div class="step-label" id="sl2">選択</div>
    </div>
    <div class="step-connector"></div>
    <div class="step-dot">
        <div class="step-circle" id="sc3">3</div>
        <div class="step-label" id="sl3">校正</div>
    </div>
    <div class="step-connector"></div>
    <div class="step-dot">
        <div class="step-circle" id="sc4">4</div>
        <div class="step-label" id="sl4">公開</div>
    </div>
    <div class="step-connector"></div>
    <div class="step-dot">
        <div class="step-circle" id="sc5">5</div>
        <div class="step-label" id="sl5">検証</div>
    </div>
</div>

<!-- 使用履歴（折りたたみ） -->
<div class="card">
    <div class="collapsible-header" id="historyToggle">
        <span style="font-size:15px; font-weight:700;">📋 使用済みシナリオ履歴</span>
        <span class="toggle-icon">▼</span>
    </div>
    <div class="collapsible-body" id="historyBody" style="display:none;">
        <div id="usedHistoryList" style="margin-top: 8px;">まだ使用履歴はありません</div>
        <button id="clearHistoryBtn" class="btn-danger" style="margin-top: 12px;">🗑 履歴をクリア</button>
    </div>
</div>

<!-- STEP 1: プロンプト生成 -->
<div class="card" id="step1Card">
    <div class="label">✨ STEP 1 — 記事生成プロンプト</div>
    <button id="generateArticleBtn" class="btn-primary">プロンプトを生成する</button>
    <div id="promptArea" style="display:none; margin-top: 14px;">
        <div class="label" style="margin-top: 0;">📋 AIにコピペするプロンプト</div>
        <textarea id="promptOutput" rows="8" readonly></textarea>
        <div class="flex-btns">
            <button id="copyPromptBtn" class="btn-secondary">📋 プロンプトをコピー</button>
        </div>
        <div class="footer-note">※ AIはウェブ検索で最新ニュース・株価を取得してください</div>
    </div>
</div>

<!-- STEP 2: JSON貼り付け -->
<div class="card" id="jsonCard">
    <div class="label">📥 STEP 2 — AIが生成したJSONを貼り付け</div>
    <textarea id="jsonInput" rows="6" placeholder='AIが出力したJSONをここに貼り付け...'></textarea>
    <button id="applyArticleBtn" class="btn-primary" style="margin-top: 12px;">シナリオを表示する →</button>
</div>

<!-- STEP 2b: シナリオ選択 -->
<div class="card" id="scenarioCard" style="display: none;">
    <div class="label">🎭 STEP 2 — 3つの因果関係から記事を選ぶ</div>
    <div id="scenarioList" class="scenario-grid"></div>
    <div class="footer-note">使用済みシナリオは選択できません。新しい記事を生成してください</div>
</div>

<!-- STEP 3: プレビュー＆校正 -->
<div class="card" id="previewCard" style="display: none;">
    <div class="label">📰 STEP 3 — 記事プレビュー</div>
    <div id="articlePreview"></div>
    <hr>
    <div class="label">🔍 校正・ファクトチェック用プロンプト</div>
    <textarea id="factCheckPrompt" rows="3" readonly></textarea>
    <div class="flex-btns">
        <button id="copyFactCheckBtn" class="btn-secondary">📋 コピー</button>
    </div>
    <div class="label" style="margin-top: 14px;">✍️ 校正後のAI出力を貼り付け</div>
    <textarea id="revisedJsonInput" rows="4" placeholder='{"revisedArticle": {...}, "changes": "変更点"}'></textarea>
    <div class="flex-btns">
        <button id="applyRevisedBtn" class="btn-secondary">🔄 校正結果を反映してプレビュー更新</button>
    </div>
    <div id="diffDisplay" style="display: none;" class="alert-banner"></div>
    <button id="approveFinalBtn" class="btn-primary" style="margin-top: 16px;">📤 記事を確定・投稿テキストを生成 →</button>
</div>

<!-- STEP 4: 最終出力 -->
<div class="card" id="finalOutputCard" style="display: none;">
    <div class="label">📢 STEP 4 — 正式記事</div>
    <div class="label" style="margin-top:4px;">🐦 X（Twitter）投稿用</div>
    <textarea id="xOutput" rows="6" readonly></textarea>
    <div class="label" style="margin-top: 12px;">📝 note / ブログ用（Markdown）</div>
    <textarea id="noteOutput" rows="8" readonly></textarea>
    <div class="flex-btns">
        <button id="copyXBtn" class="btn-secondary">🐦 X用コピー</button>
        <button id="copyNoteBtn" class="btn-secondary">📝 note用コピー</button>
    </div>
</div>

<!-- セルフチェック -->
<div class="selfcheck-panel" id="selfCheckPanel" style="display:none;">
    <h3>🧪 AI記事品質チェック</h3>
    <div id="selfCheckContent">
        <div style="font-size:14px; opacity:0.8;" class="loading-dots">分析中</div>
    </div>
</div>

<!-- STEP 5: 予測トラッカー -->
<div class="card">
    <div class="label">🎯 STEP 5 — 予測トラッカー</div>
    <div id="alertArea"></div>
    <div id="trackerList" style="font-size:14px; color:#64748b;">📊 まだ公開済み記事がありません</div>
    <div class="flex-btns" style="margin-top: 12px;">
        <button id="batchCheckPromptBtn" class="btn-secondary">📊 全銘柄チェック用プロンプト</button>
        <button id="toggleBatchBtn" class="btn-small">📋 判定結果を貼り付け</button>
    </div>
    <div id="batchResultArea" style="display: none; margin-top: 12px;">
        <div class="label">🤖 AI判定結果を貼り付け</div>
        <textarea id="aiResultInput" rows="4" placeholder='銘柄: 企業名&#10;現在株価: ○○円&#10;判定: 的中'></textarea>
        <button id="applyAiResultBtn" class="btn-secondary" style="margin-top: 8px;">📋 判定を反映する</button>
    </div>
    <div class="footer-note">公開後1週間でアラート表示。AI判定結果をコピペで反映できます</div>
</div>
```

</div>

<script>
    // ─── データ管理 ───────────────────────────────
    let predictions = [];
    let currentArticleData = null;
    let originalArticleString = "";
    let multipleScenarios = [];
    let usedScenarios = [];

    function saveAllData() {
        localStorage.setItem('oke_tracker_v8', JSON.stringify(predictions));
        localStorage.setItem('oke_used_v8', JSON.stringify(usedScenarios));
    }

    function loadAllData() {
        predictions = JSON.parse(localStorage.getItem('oke_tracker_v8') || '[]');
        usedScenarios = JSON.parse(localStorage.getItem('oke_used_v8') || '[]');
        renderTracker();
        checkOneWeekAlerts();
        renderUsedHistory();
    }

    // ─── ステップ管理 ──────────────────────────────
    function setStep(n) {
        for (let i = 1; i <= 5; i++) {
            const c = document.getElementById('sc' + i);
            const l = document.getElementById('sl' + i);
            if (i < n) { c.className = 'step-circle done'; }
            else if (i === n) { c.className = 'step-circle active'; l.className = 'step-label active'; }
            else { c.className = 'step-circle'; l.className = 'step-label'; }
        }
    }

    // ─── 履歴 ──────────────────────────────────────
    function isScenarioUsed(title, chain) {
        return usedScenarios.some(u => u.title === title || u.chainKey === chain.substring(0, 100));
    }

    function markScenarioAsUsed(scenario) {
        const chainKey = (scenario.newsChain || []).map(n => n.headline).join(' → ').substring(0, 100);
        usedScenarios.unshift({
            title: scenario.title,
            chainKey,
            publishedAt: new Date().toISOString(),
            stocks: (scenario.stocks || []).map(s => `${s.name}(${s.code})`).join(', ')
        });
        if (usedScenarios.length > 20) usedScenarios = usedScenarios.slice(0, 20);
        saveAllData();
        renderUsedHistory();
    }

    function renderUsedHistory() {
        const el = document.getElementById('usedHistoryList');
        if (!usedScenarios.length) {
            el.innerHTML = '<span style="color:#94a3b8; font-size:13px;">まだ使用履歴はありません</span>';
            return;
        }
        el.innerHTML = usedScenarios.slice(0, 10).map(s => {
            const d = new Date(s.publishedAt);
            return `<div class="history-item">
                <strong>${s.title.substring(0, 50)}${s.title.length > 50 ? '…' : ''}</strong>
                <div class="history-date">📅 ${d.toLocaleDateString()} ${d.toLocaleTimeString().slice(0,5)}</div>
                <div style="font-size:11px;color:#64748b;margin-top:2px;">🎯 ${s.stocks}</div>
            </div>`;
        }).join('');
    }

    // ─── アラート ──────────────────────────────────
    function checkOneWeekAlerts() {
        const oneWeekAgo = new Date(Date.now() - 7 * 24 * 60 * 60 * 1000);
        const due = predictions.filter(p => p.status === 'pending' && new Date(p.publishDate) <= oneWeekAgo);
        document.getElementById('alertArea').innerHTML = due.map(p =>
            `<div class="alert-banner">⏰ <strong>判定時期です！</strong> ${p.company} (${p.code}) 公開から1週間以上経過</div>`
        ).join('');
    }

    // ─── プロンプト生成 ────────────────────────────
    function generatePrompt() {
        const usedTitles = usedScenarios.map(s => s.title).join('、');
        const avoidNote = usedScenarios.length > 0
            ? `\n【重要】以下のシナリオは使用済みです。これらと異なる因果関係を生成してください：\n${usedTitles}\n`
            : '';

        const prompt = `【あなたの役割】人気金融ブロガー。難しい用語を使わず、比喩や擬人化でわかりやすく伝えるのが得意。読者が「なるほど！」と膝を打つような語り口を意識する。
${avoidNote}
【タスク】過去24時間以内の世界情勢・金融ニュースをウェブ検索で調査し、3つの異なる因果関係の連鎖をそれぞれ独立した記事として生成してください。

【重要：3つはすべて異なるニュース起点】
記事A: 例）原油価格下落 → 物流コスト減 → 輸入品値下げ → 企業A
記事B: 例）金利上昇 → 円高 → インバウンド変化 → 企業B
記事C: 例）半導体不足解消 → 自動車生産回復 → 部品メーカー好転 → 企業C

【各記事の要素】
1. 因果関係の連鎖（ニュースA→B→C→注目株）をわかりやすく
2. 比喩または擬人化（例：「原油価格は風邪をひいた巨人」）
3. 文体：語尾は「〜かもしれない」「〜と読む」など推測調。断定を避け読者の想像を刺激する
4. シナリオ実現確率（%）
5. 注目低位株（株価1000円未満）を1〜2社。株価・コードはウェブ検索で最新確認
6. ※株価は1000円未満の銘柄のみ。それ以外は除外してください
7. 記事末尾：「あなたはこのシナリオ、何点だと思う？コメントで教えてください！」を必ず入れる
8. 株価の数値は記事本文には記載しない（トラッカー用として内部保持のみ）

【出力形式】JSON
{
  "scenarios": [
    {
      "title": "記事タイトル",
      "probability": 65,
      "metaphor": "ここで使う比喩や擬人化",
      "newsChain": [
        {"headline": "ニュース1", "detail": "詳細（2〜3文）", "source": "メディア名"},
        {"headline": "ニュース2", "detail": "詳細"}
      ],
      "causalStory": "因果関係のストーリー（200字程度、推測調の文体で）",
      "stocks": [
        {
          "name": "企業名",
          "code": "証券コード",
          "currentPrice": 株価（数値のみ）,
          "prediction": "up",
          "reasoning": "選出理由（低位株である理由も含める）"
        }
      ]
    }
  ]
}
scenarios配列に3つの独立した因果関係の記事を入れてください。`;

        document.getElementById('promptOutput').value = prompt;
        document.getElementById('promptArea').style.display = 'block';
        setStep(1);
    }

    // ─── シナリオ表示 ──────────────────────────────
    function displayScenarios(data) {
        if (!data.scenarios || data.scenarios.length < 2) {
            alert('シナリオが2つ以上見つかりませんでした。AIに再度依頼してください。');
            return false;
        }
        multipleScenarios = data.scenarios.map(s => ({
            ...s,
            isUsed: isScenarioUsed(s.title, s.newsChain.map(n => n.headline).join(' → '))
        }));

        const allUsed = multipleScenarios.every(s => s.isUsed);
        const container = document.getElementById('scenarioList');

        if (allUsed) {
            container.innerHTML = `<div class="alert-banner" style="background:#fee2e2;border-left-color:#ef4444;">
                ⚠️ 生成された3つのシナリオはすべて使用済みです。新しいプロンプトを生成してください。
            </div>`;
            return false;
        }

        container.innerHTML = multipleScenarios.map((s, idx) => `
            <div class="scenario-card ${s.isUsed ? 'used' : ''}" data-idx="${idx}">
                <div class="scenario-header">
                    <div class="scenario-title">📖 ${s.title}</div>
                </div>
                <div class="probability ${s.probability < 50 ? 'probability-low' : ''}">実現確率 ${s.probability}%</div>
                <div class="scenario-chain">🔗 ${s.newsChain.map(n => n.headline).join(' → ')}</div>
                <div class="scenario-metaphor">💡 ${s.metaphor}</div>
                <div class="scenario-stocks">🎯 注目銘柄: ${s.stocks.map(st => `${st.name}(${st.code})`).join(', ')}</div>
            </div>
        `).join('');

        document.querySelectorAll('.scenario-card:not(.used)').forEach(card => {
            card.onclick = () => {
                document.querySelectorAll('.scenario-card').forEach(c => c.classList.remove('selected'));
                card.classList.add('selected');
                selectScenario(parseInt(card.dataset.idx));
            };
        });

        document.getElementById('scenarioCard').style.display = 'block';
        setStep(2);
        return true;
    }

    function selectScenario(idx) {
        const s = multipleScenarios[idx];
        if (s.isUsed) { alert('このシナリオは使用済みです。'); return; }

        currentArticleData = {
            title: s.title,
            newsChain: s.newsChain,
            causalStory: `${s.metaphor}\n\n${s.causalStory}\n\n📌 あなたはこのシナリオ、何点だと思う？コメントで教えてください！`,
            stocks: s.stocks,
            metaphor: s.metaphor,
            probability: s.probability
        };
        originalArticleString = JSON.stringify(currentArticleData, null, 2);
        displayPreview(currentArticleData);

        document.getElementById('factCheckPrompt').value =
`【ファクトチェック＆校正依頼】
以下の記事データについて：
1. 各銘柄の現在株価をウェブ検索で再確認（1000円未満であること）
2. ニュースの因果関係に矛盾がないか
3. 比喩・擬人化が読者に伝わるか

修正がある場合は "revisedArticle" に修正後JSON、"changes" に変更点を出力してください。

元記事:
${JSON.stringify(currentArticleData, null, 2)}`;

        document.getElementById('previewCard').style.display = 'block';
        document.getElementById('scenarioCard').style.display = 'none';
        setStep(3);
        window.scrollTo({ top: document.getElementById('previewCard').offsetTop - 20, behavior: 'smooth' });
    }

    // ─── プレビュー描画 ────────────────────────────
    function displayPreview(data) {
        const newsHtml = (data.newsChain || []).map(n => `
            <div class="news-item">
                <strong>📌 ${n.headline}</strong><br>
                ${n.detail}
                ${n.source ? `<div style="font-size:11px;color:#94a3b8;margin-top:4px;">📰 ${n.source}</div>` : ''}
            </div>`).join('');

        const stocksHtml = (data.stocks || []).map(s => `
            <div class="stock-card">
                <strong>${s.name} (${s.code})</strong>
                <span class="tag">株価1000円未満の低位株</span><br>
                ${s.prediction === 'up' ? '📈 上昇予想' : '📉 下落予想'}<br>
                <span style="color:#475569;">📖 ${s.reasoning}</span>
            </div>`).join('');

        document.getElementById('articlePreview').innerHTML = `
            ${data.probability ? `<div style="background:var(--green);color:white;padding:5px 14px;border-radius:30px;display:inline-block;margin-bottom:12px;font-size:13px;font-weight:700;">🎲 実現確率 ${data.probability}%</div>` : ''}
            <div class="metaphor-badge">✨ 比喩でひも解く</div>
            <div class="story-highlight">${(data.metaphor || '').replace(/\n/g, '<br>')}</div>
            ${newsHtml ? `<div style="margin:14px 0;"><strong style="font-size:14px;">📰 ニュース連鎖</strong><div style="margin-top:8px;">${newsHtml}</div></div>` : ''}
            <div style="margin:14px 0;"><strong style="font-size:14px;">🏺 ストーリー</strong><p style="margin-top:8px;font-size:14px;line-height:1.7;">${(data.causalStory || '').replace(/\n/g, '<br>')}</p></div>
            <div><strong style="font-size:14px;">🎯 注目の低位株（1000円未満）</strong>${stocksHtml}</div>
        `;
    }

    // ─── JSON読み込み ──────────────────────────────
    function loadArticleFromJson(jsonText) {
        let data;
        try { data = JSON.parse(jsonText); }
        catch(e) { alert('JSON解析エラー: ' + e.message); return; }

        if (data.scenarios && data.scenarios.length >= 2) {
            displayScenarios(data);
            document.getElementById('jsonCard').style.display = 'none';
            document.getElementById('step1Card').style.display = 'none';
        } else {
            alert('JSONに scenarios フィールド（2件以上）が必要です。');
        }
    }

    // ─── 校正反映 ──────────────────────────────────
    function applyRevised() {
        const txt = document.getElementById('revisedJsonInput').value.trim();
        if (!txt) return alert('校正後AIの出力を貼り付けてください');
        try {
            const obj = JSON.parse(txt);
            if (!obj.revisedArticle) throw new Error('revisedArticleフィールドがありません');
            currentArticleData = obj.revisedArticle;
            displayPreview(currentArticleData);
            document.getElementById('diffDisplay').style.display = 'block';
            document.getElementById('diffDisplay').innerHTML = `✍️ ${obj.changes || '修正が反映されました'}`;
        } catch(e) {
            alert('修正JSONのパース失敗: ' + e.message);
        }
    }

    // ─── 公開承認 ──────────────────────────────────
    function approveFinal() {
        if (!currentArticleData) return alert('記事がありません');
        markScenarioAsUsed(currentArticleData);

        const stocks = currentArticleData.stocks;
        const stocksLine = stocks.map(s => `${s.name}(${s.code})`).join(' / ');
        const prob = currentArticleData.probability || '?';
        const story = (currentArticleData.causalStory || '').replace(/\n/g, ' ');

        // X用（140字ベース）
        const xContent = `📈【桶屋ストーリーAI】\n${currentArticleData.title}\n\n実現確率${prob}%のシナリオ\n\n${story.substring(0, 60)}…\n\n🎯 注目低位株: ${stocksLine}\n\nあなたは何点？👇\n#株初心者 #低位株 #桶屋理論 #日本株`;

        // note/ブログ用
        let note = `# ${currentArticleData.title}\n\n`;
        note += `> 🎲 **実現確率: ${prob}%** ｜ 低位株（1000円未満）に注目する理由を因果関係で読み解く\n\n`;
        note += `## 🧠 まず比喩で理解する\n\n${currentArticleData.metaphor || ''}\n\n`;
        if (currentArticleData.newsChain) {
            note += `## 📰 ニュースの連鎖\n\n`;
            currentArticleData.newsChain.forEach(n => {
                note += `### ${n.headline}\n${n.detail}\n${n.source ? `（出典: ${n.source}）` : ''}\n\n`;
            });
        }
        note += `## 📖 因果関係のストーリー\n\n${currentArticleData.causalStory}\n\n`;
        note += `## 🎯 注目の低位株（株価1000円未満）\n\n`;
        note += `> ※低位株とは株価1000円未満の銘柄。少額から投資しやすく、上昇時の％インパクトが大きい特徴があります。\n\n`;
        stocks.forEach(s => {
            note += `### ${s.name}（${s.code}）\n- **予想**: ${s.prediction === 'up' ? '上昇期待 📈' : '下落警戒 📉'}\n- **選出理由**: ${s.reasoning}\n\n`;
        });
        note += `---\n\n💬 **あなたはこのシナリオ、何点だと思いますか？**コメントで教えてください！\n\n`;
        note += `⚠️ *この記事はAIが生成した情報です。投資判断はご自身の責任でお願いします。株式投資にはリスクが伴います。*`;

        document.getElementById('xOutput').value = xContent;
        document.getElementById('noteOutput').value = note;
        document.getElementById('finalOutputCard').style.display = 'block';
        setStep(4);

        const pub = new Date().toISOString();
        stocks.forEach(s => {
            if (!predictions.find(p => p.code === s.code && p.publishDate.split('T')[0] === pub.split('T')[0])) {
                predictions.push({
                    id: Date.now() + Math.random(),
                    company: s.name, code: s.code,
                    priceAtPrediction: s.currentPrice,
                    direction: s.prediction,
                    publishDate: pub, status: 'pending'
                });
            }
        });
        saveAllData();
        renderTracker();

        // セルフチェック起動
        runSelfCheck(currentArticleData, xContent, note);

        window.scrollTo({ top: document.getElementById('finalOutputCard').offsetTop - 20, behavior: 'smooth' });
    }

    // ─── セルフチェック（Anthropic API） ──────────────
    async function runSelfCheck(articleData, xText, noteText) {
        const panel = document.getElementById('selfCheckPanel');
        const content = document.getElementById('selfCheckContent');
        panel.style.display = 'block';
        content.innerHTML = '<div style="font-size:14px;opacity:0.8;" class="loading-dots">AI×SNSコンサル視点で分析中</div>';

        const prompt = `あなたはAI×SNSマネタイズコンサルタントです。
以下の金融ブログ記事を評価してください。

【記事タイトル】${articleData.title}
【実現確率】${articleData.probability}%
【比喩】${articleData.metaphor}
【ストーリー】${articleData.causalStory}
【X投稿文】${xText}
【注目銘柄】${articleData.stocks.map(s => `${s.name}(${s.code}): ${s.reasoning}`).join(' / ')}

以下の5項目を100点満点で採点し、各項目に改善ポイントを1文で添えてください。
返答はJSON形式のみで出力してください（前後の説明・マークダウン不要）:
{
  "scores": [
    {"item": "読者の興味を引くタイトル・フック力", "score": 0, "advice": ""},
    {"item": "比喩・擬人化のわかりやすさ", "score": 0, "advice": ""},
    {"item": "X投稿のバズりやすさ（拡散・エンゲージメント）", "score": 0, "advice": ""},
    {"item": "因果関係の説得力・論理性", "score": 0, "advice": ""},
    {"item": "マネタイズ（フォロワー獲得・有料化）への貢献度", "score": 0, "advice": ""}
  ],
  "overall": 0,
  "topAdvice": "最も重要な改善点を1文で"
}`;

        try {
            const res = await fetch('https://api.anthropic.com/v1/messages', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                    model: 'claude-sonnet-4-20250514',
                    max_tokens: 1000,
                    messages: [{ role: 'user', content: prompt }]
                })
            });
            const data = await res.json();
            const raw = data.content.map(i => i.text || '').join('').replace(/```json|```/g, '').trim();
            const result = JSON.parse(raw);
            renderSelfCheck(result);
        } catch(e) {
            content.innerHTML = `<div style="font-size:13px;opacity:0.7;">チェック中にエラーが発生しました: ${e.message}</div>`;
        }
    }

    function renderSelfCheck(result) {
        const content = document.getElementById('selfCheckContent');
        const colorClass = s => s >= 75 ? 'score-good' : s >= 55 ? 'score-warn' : 'score-bad';

        let html = result.scores.map(s => `
            <div class="score-row">
                <div style="flex:1; font-size:13px; line-height:1.4;">
                    <div>${s.item}</div>
                    <div style="font-size:12px; opacity:0.7; margin-top:3px;">💡 ${s.advice}</div>
                </div>
                <div class="score-val ${colorClass(s.score)}">${s.score}</div>
            </div>
        `).join('');

        html += `<div style="margin-top:14px; padding-top:14px; border-top:1px solid rgba(255,255,255,0.15);">
            <div style="display:flex; justify-content:space-between; align-items:center;">
                <span style="font-weight:700;">総合スコア</span>
                <span class="score-val ${colorClass(result.overall)}" style="font-size:22px;">${result.overall}</span>
            </div>
            <div style="margin-top:10px; background:rgba(255,255,255,0.1); padding:12px; border-radius:12px; font-size:13px; line-height:1.6;">
                🏆 最重要改善点：${result.topAdvice}
            </div>
        </div>`;

        content.innerHTML = html;
    }

    // ─── トラッカー ────────────────────────────────
    function renderTracker() {
        const el = document.getElementById('trackerList');
        if (!predictions.length) {
            el.innerHTML = '<span style="color:#64748b;font-size:14px;">📊 まだ公開済み記事がありません</span>';
            return;
        }
        const hit = predictions.filter(p => p.status === 'hit').length;
        const miss = predictions.filter(p => p.status === 'miss').length;
        const pending = predictions.filter(p => p.status === 'pending').length;

        el.innerHTML = `<div class="summary-box">🎯 的中 <strong>${hit}</strong>/${predictions.length} ｜ はずれ ${miss} ｜ 判定待ち ${pending}</div>`
            + predictions.map(p => `
            <div class="tracker-item">
                <div style="display:flex;justify-content:space-between;align-items:center;">
                    <strong>${p.company} (${p.code})</strong>
                    <span class="status-badge ${p.status === 'hit' ? 'status-hit' : p.status === 'miss' ? 'status-miss' : 'status-pending'}">
                        ${p.status === 'hit' ? '的中' : p.status === 'miss' ? 'はずれ' : '判定待ち'}
                    </span>
                </div>
                <div style="font-size:13px;margin-top:4px;">予想: ${p.direction === 'up' ? '上昇' : '下落'} ／ 公開時: ${p.priceAtPrediction}円</div>
                <button class="btn-small" style="margin-top:8px;" onclick="showSingleCheckPrompt('${p.company}','${p.code}',${p.priceAtPrediction},'${p.direction}')">🔍 チェック用プロンプト</button>
            </div>`).join('');
    }

    // ─── モーダル ──────────────────────────────────
    function showModal(text, title) {
        const m = document.createElement('div');
        m.style.cssText = 'position:fixed;top:0;left:0;right:0;bottom:0;background:rgba(0,0,0,0.7);display:flex;align-items:center;justify-content:center;z-index:1000;padding:20px;';
        m.innerHTML = `<div style="background:white;border-radius:24px;max-width:500px;width:100%;padding:20px;">
            <h3 style="margin-bottom:12px;font-size:16px;">${title}</h3>
            <textarea readonly style="width:100%;height:180px;padding:12px;border-radius:14px;border:1px solid #e2e8f0;font-family:monospace;font-size:13px;">${text}</textarea>

```
        <div style="display:flex;gap:10px;margin-top:12px;">
            <button class="btn-primary" style="flex:1;" onclick="navigator.clipboard.writeText(\`${text.replace(/`/g, '\\`')}\`).then(()=>alert('コピーしました'))">📋 コピー</button>
            <button class="btn-secondary" onclick="this.closest('div').parentElement.remove()">閉じる</button>
        </div>
    </div>`;
    document.body.appendChild(m);
}

window.showSingleCheckPrompt = function(company, code, price, direction) {
    showModal(`【株価チェック】
```

銘柄: ${company} (${code})
公開時株価: ${price}円
予想: ${direction === ‘up’ ? ‘上昇’ : ‘下落’}

現在の株価をウェブ検索で調べ、以下形式で出力：
銘柄: ${company} (${code})
現在株価: ○○円
判定: 【的中】 または 【はずれ】`, `${company} チェック用プロンプト`);
};

```
function generateBatchCheckPrompt() {
    const pending = predictions.filter(p => p.status === 'pending');
    if (!pending.length) return alert('判定待ちの銘柄はありません');
    let txt = `【一括株価チェック依頼】\n以下の銘柄の現在株価をウェブ検索で調べてください：\n\n`;
    pending.forEach(p => { txt += `・${p.company} (${p.code}) 公開時${p.priceAtPrediction}円 / 予想:${p.direction === 'up' ? '上昇' : '下落'}\n`; });
    txt += `\n【出力形式】\n銘柄: 企業名\n現在株価: ○○円\n判定: 【的中】または【はずれ】\n\n各銘柄ごとに改行区切りで出力してください。`;
    showModal(txt, '全銘柄チェック用プロンプト');
}

function parseAndApplyBatch(text) {
    const lines = text.split('\n');
    let count = 0;
    const cp = /(?:銘柄|企業名)[:：]\s*([^（\n]+)/;
    const rp = /判定[:：]\s*[【〔]?(的中|はずれ|当たり|外れ)[】〕]?/;
    let block = '';
    for (let i = 0; i <= lines.length; i++) {
        const l = lines[i] || '';
        block += l + '\n';
        if ((l.includes('銘柄') || l.includes('企業名') || i === lines.length) && block.trim()) {
            const cm = block.match(cp); const rm = block.match(rp);
            if (cm && rm) {
                const name = cm[1].trim();
                const status = (rm[1] === '的中' || rm[1] === '当たり') ? 'hit' : 'miss';
                const t = predictions.find(p => p.company.includes(name) && p.status === 'pending');
                if (t) { t.status = status; t.lastCheckDate = new Date().toISOString(); count++; }
            }
            block = '';
        }
    }
    if (count > 0) { saveAllData(); renderTracker(); checkOneWeekAlerts(); }
    return count;
}

// ─── コピー（Clipboard API） ───────────────────
async function copyText(id) {
    const text = document.getElementById(id).value;
    try {
        await navigator.clipboard.writeText(text);
        alert('コピーしました');
    } catch {
        const el = document.getElementById(id);
        el.select();
        document.execCommand('copy');
        alert('コピーしました');
    }
}

// ─── イベント登録 ──────────────────────────────
document.getElementById('generateArticleBtn').onclick = generatePrompt;
document.getElementById('copyPromptBtn').onclick = () => copyText('promptOutput');
document.getElementById('applyArticleBtn').onclick = () => loadArticleFromJson(document.getElementById('jsonInput').value);
document.getElementById('copyFactCheckBtn').onclick = () => copyText('factCheckPrompt');
document.getElementById('applyRevisedBtn').onclick = applyRevised;
document.getElementById('approveFinalBtn').onclick = approveFinal;
document.getElementById('copyXBtn').onclick = () => copyText('xOutput');
document.getElementById('copyNoteBtn').onclick = () => copyText('noteOutput');
document.getElementById('batchCheckPromptBtn').onclick = generateBatchCheckPrompt;
document.getElementById('applyAiResultBtn').onclick = () => {
    const count = parseAndApplyBatch(document.getElementById('aiResultInput').value);
    alert(`${count}件の判定を反映しました`);
    document.getElementById('aiResultInput').value = '';
    document.getElementById('batchResultArea').style.display = 'none';
};
document.getElementById('clearHistoryBtn').onclick = () => {
    if (confirm('使用履歴をすべて削除しますか？')) {
        usedScenarios = [];
        saveAllData();
        renderUsedHistory();
    }
};
document.getElementById('toggleBatchBtn').onclick = () => {
    const a = document.getElementById('batchResultArea');
    a.style.display = a.style.display === 'none' ? 'block' : 'none';
};
document.getElementById('historyToggle').onclick = function() {
    const body = document.getElementById('historyBody');
    const isOpen = body.style.display !== 'none';
    body.style.display = isOpen ? 'none' : 'block';
    this.classList.toggle('open', !isOpen);
};

loadAllData();
```

</script>
</body>
</html>
