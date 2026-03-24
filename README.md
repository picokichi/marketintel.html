<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes, viewport-fit=cover">
    <title>桶屋ストーリーAI - 低位株アナリスト</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background: #f5f7fb;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            padding: 16px;
            color: #1e293b;
            font-size: 16px;
            line-height: 1.5;
        }

        .container {
            max-width: 600px;
            margin: 0 auto;
        }

        .card {
            background: white;
            border-radius: 20px;
            padding: 20px;
            margin-bottom: 16px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.04);
            border: 1px solid #eef2f6;
        }

        .btn-primary, .btn-secondary, .btn-small {
            cursor: pointer;
            transition: all 0.2s ease;
            border: none;
            border-radius: 44px;
            font-weight: 600;
            text-align: center;
        }
        .btn-primary {
            background: #1e3c72;
            color: white;
            padding: 14px 20px;
            font-size: 16px;
            width: 100%;
        }
        .btn-primary:active { background: #0f2b4f; transform: scale(0.98); }
        .btn-secondary {
            background: #f1f5f9;
            color: #1e3c72;
            border: 1px solid #cbd5e1;
            padding: 12px 16px;
            font-size: 14px;
        }
        .btn-small {
            background: #f1f5f9;
            color: #1e3c72;
            border: 1px solid #cbd5e1;
            padding: 8px 14px;
            font-size: 13px;
            display: inline-block;
        }
        .btn-small:active { background: #e6edf4; }
        .btn-disabled {
            opacity: 0.5;
            pointer-events: none;
        }

        textarea {
            width: 100%;
            padding: 14px;
            border-radius: 16px;
            border: 1px solid #cfdfed;
            font-family: 'SF Mono', monospace;
            font-size: 14px;
            background: #fafcff;
            resize: vertical;
        }

        .label {
            font-weight: 600;
            margin-bottom: 8px;
            font-size: 14px;
            color: #334155;
        }

        .flex-btns {
            display: flex;
            gap: 12px;
            margin-top: 12px;
            flex-wrap: wrap;
        }

        .scenario-grid {
            display: flex;
            flex-direction: column;
            gap: 16px;
            margin: 16px 0;
        }
        .scenario-card {
            background: white;
            border: 2px solid #e2edf7;
            border-radius: 20px;
            padding: 16px;
            cursor: pointer;
            transition: all 0.2s;
            position: relative;
        }
        .scenario-card.selected {
            border-color: #1e3c72;
            background: #f0f4fa;
        }
        .scenario-card.used {
            opacity: 0.6;
            background: #f1f5f9;
            cursor: not-allowed;
            border-color: #cbd5e1;
        }
        .scenario-card.used::after {
            content: "✓ 使用済み";
            position: absolute;
            top: 12px;
            right: 12px;
            background: #94a3b8;
            color: white;
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 11px;
            font-weight: 600;
        }
        .scenario-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 8px;
            margin-bottom: 12px;
            padding-right: 80px;
        }
        .scenario-title {
            font-weight: 700;
            font-size: 17px;
        }
        .probability {
            background: #10b981;
            color: white;
            padding: 4px 12px;
            border-radius: 30px;
            font-size: 13px;
            font-weight: 600;
        }
        .probability-low {
            background: #f59e0b;
        }
        .scenario-chain {
            font-size: 13px;
            color: #475569;
            margin-bottom: 12px;
            padding: 8px;
            background: #f8fafc;
            border-radius: 12px;
        }
        .scenario-metaphor {
            font-size: 13px;
            color: #1e3c72;
            font-style: italic;
            margin-bottom: 8px;
        }
        .scenario-stocks {
            font-size: 12px;
            color: #5b6e8c;
        }
        .used-badge-small {
            background: #94a3b8;
            color: white;
            padding: 2px 8px;
            border-radius: 12px;
            font-size: 10px;
            margin-left: 8px;
        }

        /* 履歴表示 */
        .history-item {
            background: #f8fafc;
            padding: 10px;
            border-radius: 12px;
            margin-bottom: 8px;
            font-size: 13px;
            border-left: 3px solid #cbd5e1;
        }
        .history-date {
            font-size: 11px;
            color: #94a3b8;
        }

        .story-highlight {
            background: linear-gradient(135deg, #fef9e6, #fff4e0);
            border-left: 4px solid #f5b042;
            padding: 16px;
            border-radius: 16px;
            margin: 16px 0;
        }
        .metaphor-badge {
            background: #eef2ff;
            padding: 6px 12px;
            border-radius: 40px;
            display: inline-block;
            font-size: 13px;
            color: #1e3c72;
            margin-bottom: 12px;
        }
        .news-item {
            background: #f8fafc;
            padding: 12px;
            border-radius: 14px;
            margin-bottom: 10px;
            border-left: 3px solid #cbd5e1;
        }
        .stock-card {
            background: #f8fafc;
            border-radius: 16px;
            padding: 14px;
            margin-top: 12px;
            border: 1px solid #e2edf7;
        }
        .tracker-item {
            background: #ffffff;
            border-radius: 16px;
            padding: 14px;
            margin-bottom: 12px;
            border: 1px solid #e2edf7;
        }
        .status-badge {
            display: inline-block;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
        }
        .status-pending { background: #fef9c3; color: #854d0e; }
        .status-hit { background: #dcfce7; color: #166534; }
        .status-miss { background: #fee2e2; color: #991b1b; }
        .alert-banner {
            background: #fef3c7;
            border-left: 4px solid #f59e0b;
            padding: 12px;
            border-radius: 12px;
            margin-bottom: 16px;
            font-size: 14px;
        }
        .footer-note {
            font-size: 12px;
            text-align: center;
            color: #7e8b9e;
            margin-top: 16px;
        }
        hr {
            margin: 16px 0;
            border: 0;
            height: 1px;
            background: #e2e8f0;
        }
        .step-indicator {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            font-size: 12px;
            color: #94a3b8;
        }
        .step-active {
            color: #1e3c72;
            font-weight: 600;
        }
        .summary-box {
            background: #f1f5f9;
            border-radius: 12px;
            padding: 12px;
            margin-bottom: 16px;
        }
    </style>
</head>
<body>
<div class="container">
    <!-- ステップ表示 -->
    <div class="step-indicator">
        <span id="step1" class="step-active">① 記事生成</span>
        <span>→</span>
        <span id="step2">② 選択</span>
        <span>→</span>
        <span id="step3">③ 校正</span>
        <span>→</span>
        <span id="step4">④ 公開</span>
        <span>→</span>
        <span id="step5">⑤ 検証</span>
    </div>

    <!-- 使用履歴サマリー -->
    <div class="card" id="historyCard">
        <h3 style="font-size: 16px;">📋 最近使用したシナリオ</h3>
        <div id="usedHistoryList">まだ使用履歴はありません</div>
        <button id="clearHistoryBtn" class="btn-small" style="margin-top: 12px;">🗑 履歴をクリア</button>
    </div>

    <!-- STEP 1: 記事生成プロンプト -->
    <div class="card" id="step1Card">
        <button id="generateArticleBtn" class="btn-primary">✨ 記事生成プロンプトを出力</button>
        <div class="label" style="margin-top: 14px;">📋 ① AIにコピペするプロンプト</div>
        <textarea id="promptOutput" rows="8" readonly></textarea>
        <div class="flex-btns">
            <button id="copyPromptBtn" class="btn-secondary">📋 コピー</button>
        </div>
        <div class="footer-note">※ AIはウェブ検索を使って最新ニュース・株価を取得してください</div>
    </div>

    <!-- STEP 2: 複数因果関係記事選択 -->
    <div class="card" id="scenarioCard" style="display: none;">
        <div class="label">🎭 3つの異なる因果関係から記事を選ぶ</div>
        <div id="scenarioList" class="scenario-grid"></div>
        <div class="footer-note">使用済みのシナリオは選択できません。新しい記事を生成してください</div>
    </div>

    <!-- STEP 3: JSON貼り付け＆プレビュー -->
    <div class="card" id="jsonCard">
        <div class="label">📥 ② AIが生成したJSONを貼り付け</div>
        <textarea id="jsonInput" rows="6" placeholder='AIが出力したJSONをここに貼り付け'></textarea>
        <button id="applyArticleBtn" class="btn-primary" style="margin-top: 12px;">✅ 読み込む</button>
    </div>

    <!-- 記事プレビュー -->
    <div class="card" id="previewCard" style="display: none;">
        <h3 style="font-size: 18px;">📰 記事プレビュー</h3>
        <div id="articlePreview"></div>
        <hr>
        <div class="label">🔍 ③ 校正・ファクトチェック用プロンプト</div>
        <textarea id="factCheckPrompt" rows="3" readonly></textarea>
        <div class="flex-btns">
            <button id="copyFactCheckBtn" class="btn-secondary">📋 コピー</button>
        </div>
        <div class="label" style="margin-top: 12px;">✍️ ④ 校正後AIの出力を貼り付け</div>
        <textarea id="revisedJsonInput" rows="4" placeholder='{"revisedArticle": {...}, "changes": "変更点"}'></textarea>
        <button id="applyRevisedBtn" class="btn-secondary">🔄 修正反映</button>
        <div id="diffDisplay" style="display: none;" class="alert-banner"></div>
        <button id="approveFinalBtn" class="btn-primary" style="margin-top: 16px;">✅ 承認して公開</button>
    </div>

    <!-- 最終出力 -->
    <div class="card" id="finalOutputCard" style="display: none;">
        <h3>📢 正式記事</h3>
        <div class="label">🐦 X投稿用</div>
        <textarea id="xOutput" rows="3" readonly></textarea>
        <div class="label">📝 note/ブログ用</div>
        <textarea id="noteOutput" rows="6" readonly></textarea>
        <div class="flex-btns">
            <button id="copyXBtn" class="btn-secondary">X用コピー</button>
            <button id="copyNoteBtn" class="btn-secondary">note用コピー</button>
        </div>
    </div>

    <!-- 予測トラッカー -->
    <div class="card">
        <h3>🎯 予測トラッカー</h3>
        <div id="alertArea"></div>
        <div id="trackerList">📊 まだ公開済み記事がありません</div>
        <div class="flex-btns" style="margin-top: 12px;">
            <button id="batchCheckPromptBtn" class="btn-secondary">📊 全銘柄チェック用プロンプト</button>
        </div>
        <div id="batchResultArea" style="display: none; margin-top: 12px;">
            <div class="label">🤖 AI判定結果を貼り付け（一括反映）</div>
            <textarea id="aiResultInput" rows="4" placeholder='銘柄: 企業名
現在株価: ○○円
判定: 的中'></textarea>
            <button id="applyAiResultBtn" class="btn-secondary" style="margin-top: 8px;">📋 判定を反映</button>
        </div>
        <div class="footer-note">※ 公開後1週間でアラート表示。AI判定結果をコピペで反映できます</div>
    </div>
</div>

<script>
    // データ管理
    let predictions = [];
    let currentArticleData = null;
    let originalArticleString = "";
    let multipleScenarios = [];
    
    // 使用済みシナリオの履歴（タイトルと生成日時を保存）
    let usedScenarios = [];

    // ローカルストレージ
    function saveAllData() {
        localStorage.setItem('bucket_tracker_v7', JSON.stringify(predictions));
        localStorage.setItem('used_scenarios_v7', JSON.stringify(usedScenarios));
    }
    
    function loadAllData() {
        const storedTracker = localStorage.getItem('bucket_tracker_v7');
        predictions = storedTracker ? JSON.parse(storedTracker) : [];
        
        const storedUsed = localStorage.getItem('used_scenarios_v7');
        usedScenarios = storedUsed ? JSON.parse(storedUsed) : [];
        
        renderTracker();
        checkOneWeekAlerts();
        renderUsedHistory();
    }
    
    function saveTracker() {
        localStorage.setItem('bucket_tracker_v7', JSON.stringify(predictions));
        saveAllData();
    }
    
    function saveUsedScenarios() {
        localStorage.setItem('used_scenarios_v7', JSON.stringify(usedScenarios));
        renderUsedHistory();
    }
    
    // シナリオが使用済みかチェック
    function isScenarioUsed(scenarioTitle, scenarioChain) {
        // タイトルまたは主要ニュースチェーンで重複チェック
        return usedScenarios.some(used => 
            used.title === scenarioTitle || 
            used.chainKey === scenarioChain.substring(0, 100)
        );
    }
    
    // シナリオを使用済みとして記録
    function markScenarioAsUsed(scenario) {
        const chainKey = scenario.newsChain.map(n => n.headline).join(' → ').substring(0, 100);
        usedScenarios.unshift({
            title: scenario.title,
            chainKey: chainKey,
            publishedAt: new Date().toISOString(),
            stocks: scenario.stocks.map(s => `${s.name}(${s.code})`).join(', ')
        });
        // 最大20件まで保持
        if (usedScenarios.length > 20) usedScenarios = usedScenarios.slice(0, 20);
        saveUsedScenarios();
    }
    
    // 使用履歴表示
    function renderUsedHistory() {
        const container = document.getElementById('usedHistoryList');
        if (!usedScenarios.length) {
            container.innerHTML = 'まだ使用履歴はありません。記事を公開するとここに表示されます。';
            return;
        }
        let html = '';
        usedScenarios.slice(0, 10).forEach(scenario => {
            const date = new Date(scenario.publishedAt);
            html += `
                <div class="history-item">
                    <div><strong>${scenario.title.substring(0, 50)}${scenario.title.length > 50 ? '...' : ''}</strong></div>
                    <div class="history-date">📅 ${date.toLocaleDateString()} ${date.toLocaleTimeString().slice(0,5)}</div>
                    <div style="font-size: 11px; color: #64748b;">🔗 ${scenario.chainKey.substring(0, 60)}...</div>
                    <div style="font-size: 11px;">🎯 ${scenario.stocks}</div>
                </div>
            `;
        });
        container.innerHTML = html;
    }
    
    function clearHistory() {
        if (confirm('使用履歴をすべて削除します。よろしいですか？')) {
            usedScenarios = [];
            saveUsedScenarios();
            renderUsedHistory();
            alert('履歴をクリアしました。これまで使用したシナリオがリセットされました。');
        }
    }

    function checkOneWeekAlerts() {
        const now = new Date();
        const oneWeekAgo = new Date(now.getTime() - 7 * 24 * 60 * 60 * 1000);
        const pendingOverWeek = predictions.filter(p => p.status === 'pending' && new Date(p.publishDate) <= oneWeekAgo);
        const alertArea = document.getElementById('alertArea');
        if (pendingOverWeek.length > 0) {
            alertArea.innerHTML = pendingOverWeek.map(p => `
                <div class="alert-banner">
                    ⏰ <strong>判定時期です！</strong> ${p.company} (${p.code}) 公開から1週間以上経過<br>
                    ↓ 下の「全銘柄チェック用プロンプト」で判定をお願いします
                </div>
            `).join('');
        } else {
            alertArea.innerHTML = '';
        }
    }

    // AI判定テキスト解析
    function parseAiResultAndUpdate(resultText) {
        const lines = resultText.split('\n');
        let updatedCount = 0;
        const companyPattern = /(?:銘柄|企業名)[:：]\s*([^（\n]+)/;
        const codePattern = /（([^）]+)）|コード[:：]\s*(\d+)/;
        const resultPattern = /判定[:：]\s*[【〔]?(的中|はずれ|当たり|外れ)[】〕]?/;

        let currentBlock = '';
        for (let i = 0; i <= lines.length; i++) {
            const line = lines[i] || '';
            currentBlock += line + '\n';
            const isNextStock = line.includes('銘柄') || line.includes('企業名');
            if ((isNextStock && currentBlock.trim()) || i === lines.length) {
                if (currentBlock.trim()) {
                    const companyMatch = currentBlock.match(companyPattern);
                    const companyName = companyMatch ? companyMatch[1].trim() : null;
                    const codeMatch = currentBlock.match(codePattern);
                    const stockCode = codeMatch ? (codeMatch[2] || codeMatch[1]) : null;
                    const resultMatch = currentBlock.match(resultPattern);
                    let result = null;
                    if (resultMatch) {
                        const rt = resultMatch[1];
                        if (rt === '的中' || rt === '当たり') result = 'hit';
                        if (rt === 'はずれ' || rt === '外れ') result = 'miss';
                    }
                    if ((companyName || stockCode) && result) {
                        const target = predictions.find(p => 
                            (companyName && p.company.includes(companyName)) || 
                            (stockCode && p.code === stockCode)
                        );
                        if (target && target.status === 'pending') {
                            target.status = result;
                            target.lastCheckDate = new Date().toISOString();
                            updatedCount++;
                        }
                    }
                }
                currentBlock = '';
            }
        }
        if (updatedCount > 0) {
            saveTracker();
            renderTracker();
            checkOneWeekAlerts();
        }
        return updatedCount;
    }

    // プロンプト生成（使用済みシナリオを避ける指示付き）
    function generatePrompt() {
        const now = new Date();
        const usedTitles = usedScenarios.map(s => s.title).join('、');
        const avoidInstruction = usedScenarios.length > 0 
            ? `\n【重要】以下のシナリオは既に使用済みです。これらと**異なる因果関係**のシナリオを生成してください：\n${usedTitles}\n`
            : '';
        
        const prompt = `【あなたの役割】人気金融ブロガー。難しい用語を使わず、比喩や擬人化でわかりやすく伝えるのが得意。

【タスク】過去24時間以内の世界情勢・金融ニュースをウェブ検索で調査し、**3つの異なる因果関係の連鎖**をそれぞれ独立した記事として生成してください。
${avoidInstruction}
【重要】求められていること：
- 1つのニュースから3つの記事を書くのではありません
- **異なるニュースの組み合わせから生まれる3つの異なる因果関係**をそれぞれ記事にします
- 例：
  記事A: 原油価格下落 → 物流コスト減 → 輸入品値下げ → 対象企業A
  記事B: 金利上昇 → 円高進行 → インバウンド需要変化 → 対象企業B
  記事C: 半導体不足解消 → 自動車生産回復 → 部品メーカー好転 → 対象企業C

【各記事に含める要素】
1. **因果関係の連鎖**（ニュースA → B → C → 注目株）をわかりやすく説明
2. **比喩または擬人化**を使って理解しやすく（例：「原油価格は風邪をひいた巨人」）
3. **このシナリオが現実化する確率**（%表記）
4. 注目低位株（株価1000円未満）を1〜2社選出。**株価・コードはウェブ検索で最新確認**
5. 記事内に「あなたはこのシナリオ、何点だと思う？」という読者への問いかけ
6. 株価の数値は記事本文に記載しない（トラッカー用として内部保持のみ）

【出力形式】JSON
{
  "scenarios": [
    {
      "title": "記事タイトル",
      "probability": 65,
      "metaphor": "ここで使う比喩や擬人化",
      "newsChain": [
        {"headline": "ニュース1", "detail": "詳細", "source": "メディア名"},
        {"headline": "ニュース2", "detail": "詳細"}
      ],
      "causalStory": "因果関係のストーリー（200字程度）",
      "stocks": [
        {
          "name": "企業名",
          "code": "証券コード",
          "currentPrice": 株価,
          "prediction": "up",
          "reasoning": "選出理由"
        }
      ]
    }
  ]
}

注意: scenarios配列に3つの異なる因果関係の記事を入れてください。それぞれ独立した内容で、異なるニュース起点から導かれるものを選んでください。`;
        document.getElementById('promptOutput').value = prompt;
    }

    // 複数シナリオ表示（使用済みはグレーアウト）
    function displayScenarios(data) {
        if (!data.scenarios || data.scenarios.length < 2) {
            alert('シナリオが2つ以上見つかりませんでした。AIに「3つの異なる因果関係」を生成するよう再度依頼してください。');
            return false;
        }
        
        // 使用済みチェック
        const scenariosWithStatus = data.scenarios.map(scenario => {
            const isUsed = isScenarioUsed(scenario.title, scenario.newsChain.map(n => n.headline).join(' → '));
            return { ...scenario, isUsed };
        });
        
        multipleScenarios = scenariosWithStatus;
        const container = document.getElementById('scenarioList');
        
        if (scenariosWithStatus.every(s => s.isUsed)) {
            container.innerHTML = `
                <div class="alert-banner" style="background: #fee2e2; border-left-color: #ef4444;">
                    ⚠️ 生成された3つのシナリオはすべて過去に使用済みです。<br>
                    「記事生成プロンプトを出力」から新しいプロンプトを生成し、AIに再度依頼してください。
                </div>
            `;
            return false;
        }
        
        container.innerHTML = scenariosWithStatus.map((s, idx) => `
            <div class="scenario-card ${s.isUsed ? 'used' : ''}" data-idx="${idx}" ${s.isUsed ? 'style="cursor: not-allowed;"' : ''}>
                <div class="scenario-header">
                    <div class="scenario-title">📖 ${s.title}</div>
                    <div class="probability ${s.probability < 50 ? 'probability-low' : ''}">実現確率 ${s.probability}%</div>
                </div>
                <div class="scenario-chain">
                    🔗 ${s.newsChain.map(n => n.headline).join(' → ')}
                </div>
                <div class="scenario-metaphor">
                    💡 ${s.metaphor}
                </div>
                <div class="scenario-stocks">
                    🎯 注目銘柄: ${s.stocks.map(st => `${st.name}(${st.code})`).join(', ')}
                </div>
            </div>
        `).join('');
        
        document.querySelectorAll('.scenario-card:not(.used)').forEach(card => {
            card.onclick = () => {
                document.querySelectorAll('.scenario-card').forEach(c => c.classList.remove('selected'));
                card.classList.add('selected');
                const idx = parseInt(card.dataset.idx);
                selectScenario(idx);
            };
        });
        
        document.getElementById('scenarioCard').style.display = 'block';
        document.getElementById('step2').classList.add('step-active');
        return true;
    }

    function selectScenario(idx) {
        const scenario = multipleScenarios[idx];
        if (scenario.isUsed) {
            alert('このシナリオは既に使用済みです。別のシナリオを選ぶか、新しい記事を生成してください。');
            return;
        }
        
        currentArticleData = {
            title: scenario.title,
            newsChain: scenario.newsChain,
            causalStory: `${scenario.metaphor}\n\n${scenario.causalStory}\n\n📌 【読者への問いかけ】あなたはこのシナリオ、何点だと思う？コメントで教えてください！`,
            stocks: scenario.stocks,
            metaphor: scenario.metaphor,
            probability: scenario.probability
        };
        originalArticleString = JSON.stringify(currentArticleData, null, 2);
        displayPreview(currentArticleData);
        document.getElementById('previewCard').style.display = 'block';
        document.getElementById('scenarioCard').style.display = 'none';
        document.getElementById('step3').classList.add('step-active');
        
        const factPrompt = `【ファクトチェック＆校正依頼】
以下の記事データについて：
1. **最重要：各銘柄の現在の株価をウェブ検索で再確認**し、1000円未満であること。数値が古い場合は修正してください。
2. ニュースの因果関係に矛盾がないか確認。
3. 比喩・擬人化が適切か。

修正が必要な場合は、修正後のJSONを "revisedArticle" に、変更点の要約を "changes" に含めて出力してください。

元記事:
${JSON.stringify(currentArticleData, null, 2)}`;
        document.getElementById('factCheckPrompt').value = factPrompt;
    }

    function displayPreview(data) {
        let newsHtml = '';
        if (data.newsChain) {
            newsHtml = data.newsChain.map(n => `
                <div class="news-item">
                    <strong>📌 ${n.headline}</strong><br>
                    <span style="font-size: 14px;">${n.detail}</span>
                    ${n.source ? `<div style="font-size: 11px; color: #94a3b8; margin-top: 4px;">📰 ${n.source}</div>` : ''}
                </div>
            `).join('');
        }
        
        let stocksHtml = '';
        for(let s of data.stocks) {
            stocksHtml += `<div class="stock-card">
                <strong>${s.name} (${s.code})</strong><br>
                🎯 ${s.prediction === 'up' ? '📈 上昇予想' : '📉 下落予想'}<br>
                📖 ${s.reasoning}
            </div>`;
        }
        
        const previewHtml = `
            ${data.probability ? `<div style="background: #10b981; color: white; padding: 6px 12px; border-radius: 30px; display: inline-block; margin-bottom: 12px; font-size: 13px;">🎲 実現確率 ${data.probability}%</div>` : ''}
            <div class="metaphor-badge">✨ 比喩でひも解く</div>
            <div class="story-highlight">${data.metaphor || ''}</div>
            ${newsHtml ? `<div style="margin: 16px 0;"><strong>📰 ニュース連鎖</strong><br>${newsHtml}</div>` : ''}
            <div style="margin: 16px 0;"><strong>🏺 ストーリー</strong><br>${data.causalStory}</div>
            <div><strong>🎯 注目低位株（株価1000円未満）</strong>${stocksHtml}</div>
        `;
        document.getElementById('articlePreview').innerHTML = previewHtml;
    }

    function loadArticleFromJson(jsonText) {
        try {
            const data = JSON.parse(jsonText);
            if (data.scenarios && data.scenarios.length >= 2) {
                displayScenarios(data);
                document.getElementById('jsonCard').style.display = 'none';
                document.getElementById('step1Card').style.display = 'none';
            } else if (data.stocks) {
                currentArticleData = data;
                originalArticleString = JSON.stringify(data, null, 2);
                displayPreview(data);
                document.getElementById('previewCard').style.display = 'block';
                document.getElementById('jsonCard').style.display = 'none';
                document.getElementById('step1Card').style.display = 'none';
                const factPrompt = `【ファクトチェック】株価をウェブ検索で再確認し修正あれば対応。\n${JSON.stringify(data, null, 2)}`;
                document.getElementById('factCheckPrompt').value = factPrompt;
            } else {
                alert('JSON形式が正しくありません。scenarios（3つ以上の因果関係）または stocks フィールドが必要です。');
            }
        } catch(e) {
            alert('JSON解析エラー: ' + e.message);
        }
    }

    function applyRevised() {
        const revisedText = document.getElementById('revisedJsonInput').value;
        if (!revisedText) return alert('校正後AIの出力を貼り付けてください');
        try {
            const revisedObj = JSON.parse(revisedText);
            const newArticle = revisedObj.revisedArticle;
            if (!newArticle) throw new Error('revisedArticleフィールドがありません');
            currentArticleData = newArticle;
            originalArticleString = JSON.stringify(newArticle, null, 2);
            displayPreview(currentArticleData);
            document.getElementById('diffDisplay').style.display = 'block';
            document.getElementById('diffDisplay').innerHTML = `✍️ ${revisedObj.changes || '修正が反映されました'}`;
        } catch(e) {
            alert('修正JSONのパース失敗: ' + e.message);
        }
    }

    function approveFinal() {
        if (!currentArticleData) return alert('記事がありません');
        
        // 使用済みとして記録（選択されたシナリオ）
        const selectedScenario = {
            title: currentArticleData.title,
            newsChain: currentArticleData.newsChain || [],
            stocks: currentArticleData.stocks
        };
        markScenarioAsUsed(selectedScenario);
        
        const stocksSimple = currentArticleData.stocks.map(s => `${s.name}(${s.code})`).join(' / ');
        const xContent = `📈【桶屋ストーリーAI】\n${currentArticleData.title}\n\n確率${currentArticleData.probability || '?'}%のシナリオ\n\n${currentArticleData.causalStory.substring(0, 70)}...\n\n🎯 ${stocksSimple}\n\n#株初心者 #低位株 #桶屋理論`;
        
        let noteContent = `# ${currentArticleData.title}\n\n`;
        noteContent += `🎲 **実現確率: ${currentArticleData.probability || '?'}%**\n\n`;
        noteContent += `## 🧠 比喩で理解する\n${currentArticleData.metaphor || ''}\n\n`;
        if (currentArticleData.newsChain) {
            noteContent += `## 📰 ニュース連鎖\n\n`;
            currentArticleData.newsChain.forEach(n => {
                noteContent += `### ${n.headline}\n${n.detail}\n${n.source ? `（${n.source}）` : ''}\n\n`;
            });
        }
        noteContent += `## 📖 ストーリー\n${currentArticleData.causalStory}\n\n`;
        noteContent += `## 🎯 注目の低位株\n\n`;
        currentArticleData.stocks.forEach(s => {
            noteContent += `### ${s.name}（${s.code}）\n- 予想: ${s.prediction === 'up' ? '上昇期待 📈' : '下落警戒 📉'}\n- 理由: ${s.reasoning}\n\n`;
        });
        noteContent += `---\n💡 この記事はAIが生成しました。投資判断はご自身の責任でお願いします。`;
        
        document.getElementById('xOutput').value = xContent;
        document.getElementById('noteOutput').value = noteContent;
        document.getElementById('finalOutputCard').style.display = 'block';
        document.getElementById('step4').classList.add('step-active');
        
        const publishDate = new Date().toISOString();
        for (let stock of currentArticleData.stocks) {
            if (!predictions.find(p => p.code === stock.code && p.publishDate.split('T')[0] === publishDate.split('T')[0])) {
                predictions.push({
                    id: Date.now() + Math.random(),
                    company: stock.name,
                    code: stock.code,
                    priceAtPrediction: stock.currentPrice,
                    direction: stock.prediction,
                    publishDate: publishDate,
                    status: 'pending'
                });
            }
        }
        saveTracker();
        renderTracker();
        alert('記事公開完了！\nこのシナリオは使用済みとして記録され、次回以降の選択肢から除外されます。');
    }

    function renderTracker() {
        const container = document.getElementById('trackerList');
        if (!predictions.length) {
            container.innerHTML = '📊 まだ公開済み記事がありません';
            return;
        }
        const hit = predictions.filter(p => p.status === 'hit').length;
        const miss = predictions.filter(p => p.status === 'miss').length;
        const pending = predictions.filter(p => p.status === 'pending').length;
        let html = `<div style="margin-bottom: 12px;">🎯 的中 ${hit}/${predictions.length} (はずれ:${miss} 判定待ち:${pending})</div>`;
        predictions.forEach((p) => {
            const statusClass = p.status === 'hit' ? 'status-hit' : (p.status === 'miss' ? 'status-miss' : 'status-pending');
            const statusText = p.status === 'hit' ? '的中' : (p.status === 'miss' ? 'はずれ' : '判定待ち');
            html += `<div class="tracker-item">
                <div style="display:flex; justify-content:space-between;">
                    <strong>${p.company} (${p.code})</strong>
                    <span class="status-badge ${statusClass}">${statusText}</span>
                </div>
                <div style="font-size:13px;">予想: ${p.direction === 'up' ? '上昇' : '下落'} / 公開時: ${p.priceAtPrediction}円</div>
                <button class="btn-small" style="margin-top:8px;" onclick="showSingleCheckPrompt('${p.company}', '${p.code}', ${p.priceAtPrediction}, '${p.direction}')">🔍 チェック用プロンプト</button>
            </div>`;
        });
        container.innerHTML = html;
    }

    window.showSingleCheckPrompt = function(company, code, price, direction) {
        const prompt = `【株価チェック】
銘柄: ${company} (${code})
公開時株価: ${price}円
予想: ${direction === 'up' ? '上昇' : '下落'}

現在の株価をウェブ検索で調べ、以下形式で出力：
銘柄: ${company} (${code})
現在株価: ○○円
判定: 【的中】 または 【はずれ】`;
        showModal(prompt, `${company} チェック用プロンプト`);
    };

    function showModal(content, title) {
        const modal = document.createElement('div');
        modal.style.cssText = 'position:fixed;top:0;left:0;right:0;bottom:0;background:rgba(0,0,0,0.7);display:flex;align-items:center;justify-content:center;z-index:1000;padding:20px;';
        modal.innerHTML = `<div style="background:white;border-radius:28px;max-width:500px;width:100%;padding:20px;">
            <h3 style="margin-bottom:12px;">${title}</h3>
            <textarea readonly style="width:100%;height:200px;margin:12px 0;padding:12px;border-radius:16px;font-family:monospace;font-size:13px;">${content}</textarea>
            <button class="btn-secondary" onclick="this.closest('div').parentElement.remove()">閉じる</button>
        </div>`;
        document.body.appendChild(modal);
    }

    function generateBatchCheckPrompt() {
        const pending = predictions.filter(p => p.status === 'pending');
        if (!pending.length) return alert('判定待ちの銘柄はありません');
        let prompt = `【一括株価チェック依頼】\n以下の銘柄の現在株価をウェブ検索で調べてください：\n\n`;
        pending.forEach(p => {
            prompt += `・${p.company} (${p.code}) 公開時${p.priceAtPrediction}円 / 予想:${p.direction === 'up' ? '上昇' : '下落'}\n`;
        });
        prompt += `\n【出力形式】\n銘柄: 企業名\n現在株価: ○○円\n判定: 【的中】または【はずれ】\n\n※各銘柄ごとに改行区切りで出力してください。`;
        showModal(prompt, '全銘柄チェック用プロンプト');
    }

    function applyBatchResult() {
        const text = document.getElementById('aiResultInput').value;
        if (!text) return alert('判定結果を貼り付けてください');
        const count = parseAiResultAndUpdate(text);
        alert(`${count}件の判定を反映しました`);
        document.getElementById('aiResultInput').value = '';
        document.getElementById('batchResultArea').style.display = 'none';
    }

    function copyText(id) {
        const t = document.getElementById(id);
        t.select();
        document.execCommand('copy');
        alert('コピーしました');
    }

    // イベント登録
    document.getElementById('generateArticleBtn').onclick = generatePrompt;
    document.getElementById('copyPromptBtn').onclick = () => copyText('promptOutput');
    document.getElementById('applyArticleBtn').onclick = () => loadArticleFromJson(document.getElementById('jsonInput').value);
    document.getElementById('copyFactCheckBtn').onclick = () => copyText('factCheckPrompt');
    document.getElementById('applyRevisedBtn').onclick = applyRevised;
    document.getElementById('approveFinalBtn').onclick = approveFinal;
    document.getElementById('copyXBtn').onclick = () => copyText('xOutput');
    document.getElementById('copyNoteBtn').onclick = () => copyText('noteOutput');
    document.getElementById('batchCheckPromptBtn').onclick = generateBatchCheckPrompt;
    document.getElementById('applyAiResultBtn').onclick = applyBatchResult;
    document.getElementById('clearHistoryBtn').onclick = clearHistory;
    
    // トグルボタン
    const toggleBtn = document.createElement('button');
    toggleBtn.className = 'btn-small';
    toggleBtn.textContent = '📋 判定結果を貼り付け';
    toggleBtn.style.marginLeft = '8px';
    toggleBtn.onclick = () => {
        const area = document.getElementById('batchResultArea');
        area.style.display = area.style.display === 'none' ? 'block' : 'none';
    };
    document.getElementById('batchCheckPromptBtn').insertAdjacentElement('afterend', toggleBtn);

    loadAllData();
</script>
</body>
</html>
