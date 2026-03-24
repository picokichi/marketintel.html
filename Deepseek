<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>桶屋ストーリーAI - 低位株アナリスト</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            background: #f5f7fb;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            padding: 20px 16px 80px;
            color: #1e293b;
        }

        .container {
            max-width: 600px;
            margin: 0 auto;
        }

        .app-header {
            text-align: center;
            margin-bottom: 24px;
        }
        .app-header h1 {
            font-size: 1.8rem;
            font-weight: 700;
            background: linear-gradient(135deg, #1e3c72, #2b4c7c);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        .app-header p {
            font-size: 0.8rem;
            color: #5b6e8c;
            margin-top: 6px;
        }

        .card {
            background: white;
            border-radius: 24px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.05);
            border: 1px solid #eef2f6;
        }

        .btn-primary {
            background: #1e3c72;
            color: white;
            border: none;
            padding: 14px 20px;
            border-radius: 60px;
            font-weight: 600;
            font-size: 1rem;
            width: 100%;
            cursor: pointer;
            transition: all 0.2s ease;
        }
        .btn-primary:active {
            background: #0f2b4f;
            transform: scale(0.98);
        }
        .btn-secondary {
            background: #f1f5f9;
            color: #1e3c72;
            border: 1px solid #cbd5e1;
            padding: 10px 14px;
            border-radius: 40px;
            font-weight: 500;
            font-size: 0.85rem;
            cursor: pointer;
        }
        .btn-secondary:active {
            background: #e6edf4;
        }
        .btn-small {
            background: #f1f5f9;
            color: #1e3c72;
            border: 1px solid #cbd5e1;
            padding: 6px 12px;
            border-radius: 30px;
            font-weight: 500;
            font-size: 0.75rem;
            cursor: pointer;
        }
        .btn-success {
            background: #10b981;
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 30px;
            font-weight: 500;
            font-size: 0.75rem;
            cursor: pointer;
        }

        textarea {
            width: 100%;
            padding: 14px;
            border-radius: 20px;
            border: 1px solid #cfdfed;
            font-family: 'SF Mono', monospace;
            font-size: 0.8rem;
            background: #fafcff;
            resize: vertical;
        }

        .label {
            font-weight: 600;
            margin-bottom: 8px;
            display: block;
            font-size: 0.85rem;
            color: #334155;
        }

        .flex-btns {
            display: flex;
            gap: 12px;
            margin-top: 12px;
            flex-wrap: wrap;
        }

        .diff-box {
            background: #fef9e6;
            border-left: 5px solid #f5b042;
            padding: 12px 16px;
            border-radius: 16px;
            font-size: 0.8rem;
            margin: 12px 0;
            max-height: 200px;
            overflow-y: auto;
        }

        .stock-card {
            background: #f8fafc;
            border-radius: 18px;
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

        .alert-banner {
            background: #fef3c7;
            border-left: 4px solid #f59e0b;
            padding: 12px;
            border-radius: 12px;
            margin-bottom: 16px;
            font-size: 0.85rem;
        }

        hr {
            margin: 16px 0;
            border: 0;
            height: 1px;
            background: #e2e8f0;
        }

        .footer-note {
            font-size: 0.7rem;
            text-align: center;
            color: #7e8b9e;
            margin-top: 20px;
        }

        .news-item {
            background: #f1f5f9;
            padding: 10px;
            border-radius: 14px;
            margin-bottom: 10px;
        }

        .status-badge {
            display: inline-block;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.7rem;
            font-weight: 600;
        }
        .status-pending { background: #fef9c3; color: #854d0e; }
        .status-hit { background: #dcfce7; color: #166534; }
        .status-miss { background: #fee2e2; color: #991b1b; }
        
        .result-input-area {
            margin-top: 12px;
            padding-top: 12px;
            border-top: 1px dashed #e2e8f0;
        }
    </style>
</head>
<body>
<div class="container">
    <div class="app-header">
        <h1>📈 桶屋ストーリーAI</h1>
        <p>“風が吹けば桶屋が儲かる”理論で低位株発掘 | AI判定コピペ完結型</p>
    </div>

    <!-- STEP 1: 記事生成ボタン -->
    <div class="card">
        <button id="generateArticleBtn" class="btn-primary">✨ 記事生成プロンプトを出力</button>
        <div class="label" style="margin-top: 14px;">📋 ① このプロンプトをAIにコピペ</div>
        <textarea id="promptOutput" rows="5" readonly placeholder="プロンプトが表示されます"></textarea>
        <div class="flex-btns">
            <button id="copyPromptBtn" class="btn-secondary">📋 コピー</button>
        </div>
        <div class="footer-note">※ AIはウェブ検索機能を使って最新の株価・ニュースを取得してください</div>
    </div>

    <!-- STEP 2: AI生成JSON貼り付け -->
    <div class="card">
        <div class="label">📥 ② AIが生成した記事データ（JSON）を貼り付け</div>
        <textarea id="jsonInput" rows="6" placeholder='{
  "title": "記事タイトル",
  "newsChain": [{"headline": "ニュース", "detail": "詳細"}],
  "causalStory": "桶屋理論ストーリー",
  "stocks": [
    {
      "name": "企業名",
      "code": "証券コード",
      "currentPrice": 850,
      "prediction": "up",
      "reasoning": "選出理由"
    }
  ]
}'></textarea>
        <button id="applyArticleBtn" class="btn-primary" style="margin-top: 12px;">✅ 記事を読み込む</button>
    </div>

    <!-- 記事プレビューエリア -->
    <div class="card" id="previewCard" style="display: none;">
        <h3 style="font-size: 1.2rem;">📰 記事プレビュー</h3>
        <div id="articlePreview"></div>
        <hr>
        <div class="label">🔍 ③ 校正・ファクトチェック用プロンプト</div>
        <textarea id="factCheckPrompt" rows="3" readonly></textarea>
        <div class="flex-btns">
            <button id="copyFactCheckBtn" class="btn-secondary">📋 コピー（AIへ）</button>
        </div>
        <div class="label" style="margin-top: 12px;">✍️ ④ 校正後AIの出力を貼り付け</div>
        <textarea id="revisedJsonInput" rows="4" placeholder='{
  "revisedArticle": {...},
  "changes": "変更点の説明"
}'></textarea>
        <button id="applyRevisedBtn" class="btn-secondary">🔄 修正反映 & 差分表示</button>
        <div id="diffDisplay" class="diff-box" style="display: none;"></div>
        <div class="flex-btns">
            <button id="approveFinalBtn" class="btn-primary">✅ 承認して正式記事生成</button>
        </div>
    </div>

    <!-- 最終出力 -->
    <div class="card" id="finalOutputCard" style="display: none;">
        <h3>📢 正式記事（承認済）</h3>
        <div class="label">🐦 X（Twitter）投稿用</div>
        <textarea id="xOutput" rows="3" readonly></textarea>
        <div class="label">📝 note / ブログ用</div>
        <textarea id="noteOutput" rows="6" readonly></textarea>
        <div class="flex-btns">
            <button id="copyXBtn" class="btn-secondary">X用コピー</button>
            <button id="copyNoteBtn" class="btn-secondary">note用コピー</button>
        </div>
    </div>

    <!-- 予測トラッカー（AI判定コピペ反映型） -->
    <div class="card">
        <h3>🎯 予測トラッカー</h3>
        <div id="alertArea"></div>
        <div id="trackerList">📊 まだ承認済み記事がありません</div>
        
        <!-- AI判定結果貼り付けエリア（全銘柄一括反映用） -->
        <div class="result-input-area" id="batchResultArea" style="display: none;">
            <div class="label">🤖 AI判定結果を貼り付け（一括反映）</div>
            <textarea id="aiResultInput" rows="4" placeholder='例:
銘柄: 大黒天物産 (2790)
現在株価: 890円
判定: 的中

銘柄: 日本航空 (9201)
現在株価: 2450円
判定: はずれ'></textarea>
            <button id="applyAiResultBtn" class="btn-secondary" style="margin-top: 8px;">📋 判定を一括反映</button>
            <div class="footer-note">※ AIの回答をそのまま貼り付けると自動で判定を反映します</div>
        </div>
        
        <div class="flex-btns" style="margin-top: 12px;">
            <button id="showBatchAreaBtn" class="btn-secondary">📊 AI判定結果を一括反映</button>
            <button id="batchCheckPromptBtn" class="btn-secondary">🔍 全銘柄チェック用プロンプト出力</button>
        </div>
        <div class="footer-note">※ 各銘柄の「AI判定結果を貼り付け」から個別反映も可能です</div>
    </div>
</div>

<script>
    // 予測トラッカー管理
    let predictions = [];
    let currentArticleData = null;
    let originalArticleString = "";
    
    // ローカルストレージ操作
    function saveTracker() {
        localStorage.setItem('bucket_tracker_v4', JSON.stringify(predictions));
    }
    
    function loadTracker() {
        const stored = localStorage.getItem('bucket_tracker_v4');
        if (stored) {
            predictions = JSON.parse(stored);
        } else {
            predictions = [];
        }
        renderTracker();
        checkOneWeekAlerts();
    }
    
    // 1週間経過チェック＆アラート表示
    function checkOneWeekAlerts() {
        const now = new Date();
        const oneWeekAgo = new Date(now.getTime() - 7 * 24 * 60 * 60 * 1000);
        let hasAlert = false;
        
        predictions.forEach(pred => {
            const publishDate = new Date(pred.publishDate);
            const isPending = pred.status === 'pending';
            const isOverOneWeek = publishDate <= oneWeekAgo;
            
            if (isPending && isOverOneWeek && !pred.alertShown) {
                pred.alertShown = true;
                hasAlert = true;
                saveTracker();
            }
        });
        
        const alertArea = document.getElementById('alertArea');
        const pendingOverWeek = predictions.filter(p => p.status === 'pending' && new Date(p.publishDate) <= oneWeekAgo);
        
        if (pendingOverWeek.length > 0) {
            let alertHtml = '';
            pendingOverWeek.forEach(pred => {
                const days = Math.floor((now - new Date(pred.publishDate)) / (1000 * 3600 * 24));
                alertHtml += `
                    <div class="alert-banner">
                        ⏰ <strong>判定時期です！</strong><br>
                        ${pred.company} (${pred.code}) は公開から${days}日経過しました。<br>
                        下の「AI判定結果を貼り付け」で判定を反映してください。
                    </div>
                `;
            });
            alertArea.innerHTML = alertHtml;
        } else {
            alertArea.innerHTML = '';
        }
    }
    
    // AI判定テキストをパースして反映（自然言語対応）
    function parseAiResultAndUpdate(resultText, targetStockCode = null) {
        const lines = resultText.split('\n');
        let currentCompany = null;
        let currentPrice = null;
        let currentResult = null;
        let updatedCount = 0;
        
        // 正規表現パターン
        const companyPattern = /(?:銘柄|企業名)[:：]\s*([^（\n]+)(?:（([^）]+)）)?/;
        const codePattern = /（([^）]+)）|コード[:：]\s*(\d+)/;
        const pricePattern = /(?:現在株価|株価)[:：]\s*([\d,]+)\s*円/;
        const resultPattern = /判定[:：]\s*[【〔]?(的中|はずれ|当たり|外れ)[】〕]?/;
        
        let currentBlock = '';
        
        for (let i = 0; i <= lines.length; i++) {
            const line = lines[i] || '';
            currentBlock += line + '\n';
            
            // ブロックの区切り（空行または次の銘柄開始）
            const isNextStock = line.includes('銘柄') || line.includes('企業名');
            const isEnd = i === lines.length;
            
            if ((isNextStock && currentBlock.trim()) || isEnd) {
                if (currentBlock.trim()) {
                    // 企業名抽出
                    let companyMatch = currentBlock.match(companyPattern);
                    let companyName = companyMatch ? companyMatch[1].trim() : null;
                    
                    // コード抽出
                    let codeMatch = currentBlock.match(codePattern);
                    let stockCode = codeMatch ? (codeMatch[2] || codeMatch[1]) : null;
                    
                    // 株価抽出
                    let priceMatch = currentBlock.match(pricePattern);
                    let currentPriceVal = priceMatch ? parseInt(priceMatch[1].replace(/,/g, '')) : null;
                    
                    // 判定抽出
                    let resultMatch = currentBlock.match(resultPattern);
                    let result = null;
                    if (resultMatch) {
                        const resultTextMatch = resultMatch[1];
                        if (resultTextMatch === '的中' || resultTextMatch === '当たり') result = 'hit';
                        if (resultTextMatch === 'はずれ' || resultTextMatch === '外れ') result = 'miss';
                    }
                    
                    // 該当する予測を探して更新
                    if (companyName || stockCode) {
                        let targetPred = null;
                        if (targetStockCode) {
                            targetPred = predictions.find(p => p.code === targetStockCode);
                        } else {
                            // 企業名またはコードで検索
                            targetPred = predictions.find(p => 
                                (companyName && p.company.includes(companyName)) || 
                                (stockCode && p.code === stockCode)
                            );
                        }
                        
                        if (targetPred && result) {
                            targetPred.status = result;
                            targetPred.lastCheckDate = new Date().toISOString();
                            targetPred.aiResultRaw = currentBlock;
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
            return { success: true, count: updatedCount };
        }
        return { success: false, count: 0 };
    }
    
    // 個別銘柄用の判定反映モーダル
    function showResultModalForStock(idx) {
        const pred = predictions[idx];
        const existingModal = document.getElementById('resultModal');
        if (existingModal) existingModal.remove();
        
        const modal = document.createElement('div');
        modal.id = 'resultModal';
        modal.style.cssText = `
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.7);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            padding: 20px;
        `;
        
        modal.innerHTML = `
            <div style="background: white; border-radius: 28px; max-width: 500px; width: 100%; max-height: 80%; overflow: auto; padding: 20px;">
                <h3 style="margin-bottom: 12px;">🎯 ${pred.company} (${pred.code})</h3>
                <div style="background: #f8fafc; padding: 12px; border-radius: 16px; margin-bottom: 16px;">
                    <div>📈 予想: ${pred.direction === 'up' ? '上昇' : '下落'}</div>
                    <div>💰 公開時株価: ${pred.priceAtPrediction}円</div>
                </div>
                <div class="label">🤖 AIの判定結果を貼り付け</div>
                <textarea id="modalResultText" rows="5" placeholder="例：
銘柄: ${pred.company}
現在株価: 920円
判定: 的中"></textarea>
                <div class="flex-btns" style="margin-top: 16px;">
                    <button id="modalApplyBtn" class="btn-primary">✅ 反映する</button>
                    <button id="modalCloseBtn" class="btn-secondary">閉じる</button>
                </div>
                <div class="footer-note">AIの回答をそのまま貼り付けて「反映する」を押してください</div>
            </div>
        `;
        
        document.body.appendChild(modal);
        
        document.getElementById('modalApplyBtn').onclick = () => {
            const resultText = document.getElementById('modalResultText').value;
            if (!resultText.trim()) {
                alert('判定結果を貼り付けてください');
                return;
            }
            const parsed = parseAiResultAndUpdate(resultText, pred.code);
            if (parsed.success) {
                alert(`${pred.company} の判定を反映しました！`);
                modal.remove();
            } else {
                alert('判定結果を解析できませんでした。\n「銘柄: 企業名\n現在株価: ○○円\n判定: 的中」のような形式で入力してください。');
            }
        };
        document.getElementById('modalCloseBtn').onclick = () => modal.remove();
        modal.onclick = (e) => { if (e.target === modal) modal.remove(); };
    }
    
    // 全銘柄一括反映エリアの表示/非表示
    function toggleBatchArea() {
        const area = document.getElementById('batchResultArea');
        area.style.display = area.style.display === 'none' ? 'block' : 'none';
    }
    
    // 全銘柄一括反映
    function applyBatchAiResult() {
        const resultText = document.getElementById('aiResultInput').value;
        if (!resultText.trim()) {
            alert('AIの判定結果を貼り付けてください');
            return;
        }
        const parsed = parseAiResultAndUpdate(resultText);
        if (parsed.success) {
            alert(`${parsed.count}件の判定を反映しました！`);
            document.getElementById('aiResultInput').value = '';
            toggleBatchArea();
        } else {
            alert('判定結果を解析できませんでした。\n以下のような形式で入力してください：\n\n銘柄: 企業名\n現在株価: ○○円\n判定: 的中\n\n銘柄: 企業名2\n現在株価: △△円\n判定: はずれ');
        }
    }
    
    // 全銘柄チェック用プロンプト出力
    function generateBatchCheckPrompt() {
        const pendingPredictions = predictions.filter(p => p.status === 'pending');
        if (pendingPredictions.length === 0) {
            alert('判定待ちの銘柄はありません。全銘柄すでに判定済みです。');
            return;
        }
        
        let prompt = `【一括株価チェック依頼】
以下の銘柄について、**ウェブ検索機能を使って**それぞれ現在の株価を調べ、判定結果を教えてください。

`;
        pendingPredictions.forEach((pred, i) => {
            prompt += `${i+1}. ${pred.company} (${pred.code})
   - 公開時株価: ${pred.priceAtPrediction}円
   - 予想方向: ${pred.direction === 'up' ? '上昇' : '下落'}
   - 判定条件: ${pred.direction === 'up' ? '現在株価 > ' + pred.priceAtPrediction + '円 → 的中' : '現在株価 < ' + pred.priceAtPrediction + '円 → 的中'}

`;
        });
        
        prompt += `【出力形式】
各銘柄ごとに以下の形式で出力してください：

銘柄: 企業名 (コード)
現在株価: ○○円
判定: 【的中】 または 【はずれ】

よろしくお願いします。`;
        
        showPromptModal(prompt, '📊 全銘柄一括チェック用プロンプト');
    }
    
    // プロンプト表示用モーダル
    function showPromptModal(promptText, title) {
        const existingModal = document.getElementById('promptModal');
        if (existingModal) existingModal.remove();
        
        const modal = document.createElement('div');
        modal.id = 'promptModal';
        modal.style.cssText = `
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.7);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            padding: 20px;
        `;
        
        modal.innerHTML = `
            <div style="background: white; border-radius: 28px; max-width: 500px; width: 100%; max-height: 80%; overflow: auto; padding: 20px;">
                <h3 style="margin-bottom: 12px;">${title}</h3>
                <textarea id="modalPromptText" readonly style="width: 100%; height: 250px; font-family: monospace; font-size: 0.8rem; padding: 12px; border-radius: 16px; border: 1px solid #ddd;">${promptText}</textarea>
                <div class="flex-btns" style="margin-top: 16px;">
                    <button id="modalCopyBtn" class="btn-secondary">📋 コピー</button>
                    <button id="modalCloseBtn" class="btn-secondary">閉じる</button>
                </div>
                <div class="footer-note">プロンプトをコピーしてAIに貼り付け、判定結果を「AI判定結果を貼り付け」から反映してください</div>
            </div>
        `;
        
        document.body.appendChild(modal);
        
        document.getElementById('modalCopyBtn').onclick = () => {
            const textarea = document.getElementById('modalPromptText');
            textarea.select();
            textarea.setSelectionRange(0, 99999);
            document.execCommand('copy');
            alert('コピーしました。AIアプリに貼り付けて判定を取得してください。');
        };
        document.getElementById('modalCloseBtn').onclick = () => modal.remove();
        modal.onclick = (e) => { if (e.target === modal) modal.remove(); };
    }
    
    // トラッカー表示
    function renderTracker() {
        const container = document.getElementById('trackerList');
        if (!predictions.length) {
            container.innerHTML = '📊 まだ承認済み記事がありません。記事を承認すると予測が追加されます。';
            return;
        }
        
        const hitCount = predictions.filter(p => p.status === 'hit').length;
        const missCount = predictions.filter(p => p.status === 'miss').length;
        const pendingCount = predictions.filter(p => p.status === 'pending').length;
        
        let html = `<div style="margin-bottom: 16px; padding: 8px; background: #f8fafc; border-radius: 16px; text-align: center;">
            🎯 的中率: ${hitCount}/${predictions.length} (当たり:${hitCount} / はずれ:${missCount} / 判定待ち:${pendingCount})
        </div>`;
        
        predictions.forEach((pred, idx) => {
            const statusClass = pred.status === 'hit' ? 'status-hit' : (pred.status === 'miss' ? 'status-miss' : 'status-pending');
            const statusText = pred.status === 'hit' ? '✅ 的中' : (pred.status === 'miss' ? '❌ はずれ' : '⏳ 判定待ち');
            const publishDateObj = new Date(pred.publishDate);
            const now = new Date();
            const daysPassed = Math.floor((now - publishDateObj) / (1000 * 3600 * 24));
            
            html += `
                <div class="tracker-item">
                    <div style="display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 8px;">
                        <div>
                            <strong>${pred.company}</strong><br>
                            <span style="font-size: 0.75rem; color: #5b6e8c;">${pred.code}</span>
                        </div>
                        <span class="status-badge ${statusClass}">${statusText}</span>
                    </div>
                    <div style="font-size: 0.8rem; margin-top: 10px;">
                        📈 予想: ${pred.direction === 'up' ? '上昇' : '下落'} | 
                        予想時株価: ${pred.priceAtPrediction}円<br>
                        📅 公開日: ${publishDateObj.toLocaleDateString()} (${daysPassed}日前)
                        ${pred.lastCheckDate ? `<br>🔄 最終判定: ${new Date(pred.lastCheckDate).toLocaleDateString()}` : ''}
                    </div>
                    <div class="flex-btns" style="margin-top: 12px;">
                        <button class="btn-small" onclick="showCheckPrompt(${idx})">🔍 チェック用プロンプト出力</button>
                        <button class="btn-small" onclick="showResultModalForStock(${idx})">📋 AI判定結果を貼り付け</button>
                    </div>
                </div>
            `;
        });
        container.innerHTML = html;
    }
    
    // 個別チェック用プロンプト出力
    window.showCheckPrompt = function(idx) {
        const pred = predictions[idx];
        const prompt = `【株価チェック依頼】
銘柄: ${pred.company} (${pred.code})
公開時株価: ${pred.priceAtPrediction}円
予想方向: ${pred.direction === 'up' ? '上昇' : '下落'}

現在の株価をウェブ検索で調べて、以下の形式で出力してください：

銘柄: ${pred.company} (${pred.code})
現在株価: ○○円
判定: 【的中】 または 【はずれ】`;
        
        showPromptModal(prompt, `${pred.company} の株価チェック用プロンプト`);
    };
    
    window.showResultModalForStock = showResultModalForStock;
    
    // プロンプト生成
    function generatePrompt() {
        const now = new Date();
        const prompt = `【あなたの役割】株式アナリスト / 金融ライター

【タスク】「風が吹けば桶屋が儲かる」理論を使って、初心者向けの投資記事を生成してください。

【必須条件】
1. **ウェブ検索機能を使って**、現在時刻(${now.toLocaleString()})から過去24時間以内の世界情勢・金融ニュースを調査してください。
2. 複数のニュースを組み合わせ、意外な因果関係で「低位株（株価1000円未満）」に注目する理論を構築。
3. 注目株の選出は「テーマ × 時価総額 × バリュエーション × 出遅れ」でスクリーニング。
4. **各銘柄の証券コードと現在の株価は必ずウェブ検索で最新の情報を取得**し、1,000円未満であることを確認。
5. 出力は以下のJSON形式のみ。

{
  "title": "【桶屋理論】〇〇という意外な連鎖で注目の低位株",
  "newsChain": [
    {"headline": "ニュース1の見出し", "detail": "詳細"},
    {"headline": "ニュース2の見出し", "detail": "詳細"}
  ],
  "causalStory": "桶屋理論の説明（200字程度）",
  "stocks": [
    {
      "name": "企業名",
      "code": "証券コード",
      "currentPrice": 株価（1000未満）,
      "prediction": "up または down",
      "reasoning": "選出理由"
    }
  ]
}`;
        document.getElementById('promptOutput').value = prompt;
    }
    
    // 記事読み込み＆プレビュー
    function loadArticleFromJson(jsonText) {
        try {
            const data = JSON.parse(jsonText);
            let invalidStocks = [];
            if (data.stocks) {
                data.stocks.forEach((s) => {
                    if (s.currentPrice >= 1000) invalidStocks.push(`${s.name}: ${s.currentPrice}円`);
                });
            }
            if (invalidStocks.length > 0) {
                alert(`⚠️ 低位株（1000円未満）の条件を満たしていない銘柄があります:\n${invalidStocks.join('\n')}\n\nファクトチェックで修正してください。`);
            }
            
            currentArticleData = data;
            originalArticleString = JSON.stringify(data, null, 2);
            displayPreview(data);
            
            const factPrompt = `【ファクトチェック＆校正依頼】
以下の記事データについて:
1. 各銘柄の株価が本当に1,000円未満か、最新のウェブ検索で再確認。
2. ニュースの因果関係に矛盾がないか。
3. 「テーマ×時価総額×バリュエーション×出遅れ」の観点で妥当性をチェック。

修正が必要な場合は、修正後のJSONを "revisedArticle" フィールドに、変更点の要約を "changes" フィールドに含めて出力してください。

元記事:
${JSON.stringify(data, null, 2)}`;
            
            document.getElementById('factCheckPrompt').value = factPrompt;
            document.getElementById('previewCard').style.display = 'block';
            document.getElementById('finalOutputCard').style.display = 'none';
        } catch(e) {
            alert('JSON解析エラー: ' + e.message);
        }
    }
    
    function displayPreview(data) {
        let newsHtml = data.newsChain.map(n => `
            <div class="news-item">
                <strong>📌 ${n.headline}</strong><br>
                <span style="font-size:0.85rem;">${n.detail}</span>
            </div>
        `).join('');
        
        let stocksHtml = '';
        for(let s of data.stocks) {
            stocksHtml += `
                <div class="stock-card">
                    <strong>${s.name} (${s.code})</strong><br>
                    💰 株価: ${s.currentPrice}円<br>
                    🎯 ${s.prediction === 'up' ? '📈 上昇予想' : '📉 下落予想'}<br>
                    📖 ${s.reasoning}
                </div>
            `;
        }
        
        const previewHtml = `
            <h3>${data.title}</h3>
            <div style="margin: 12px 0;"><strong>🔗 ニュース連鎖</strong><br>${newsHtml}</div>
            <div style="background:#f1f5f9; padding:14px; border-radius:16px;"><strong>🏺 桶屋ストーリー</strong><br>${data.causalStory}</div>
            <div style="margin-top:12px;"><strong>🎯 注目低位株</strong>${stocksHtml}</div>
        `;
        document.getElementById('articlePreview').innerHTML = previewHtml;
    }
    
    function applyRevised() {
        const revisedText = document.getElementById('revisedJsonInput').value;
        if (!revisedText) return alert('校正後AIの出力を貼り付けてください');
        try {
            const revisedObj = JSON.parse(revisedText);
            let newArticle = revisedObj.revisedArticle;
            if (!newArticle) throw new Error('revisedArticleフィールドがありません');
            
            const newArticleStr = JSON.stringify(newArticle, null, 2);
            const oldLines = originalArticleString.split('\n');
            const newLines = newArticleStr.split('\n');
            let diffHtml = `<strong>✍️ 変更点</strong><br>${revisedObj.changes || '修正が反映されました'}<br><br>`;
            let diffCount = 0;
            for(let i=0; i<Math.min(oldLines.length, newLines.length) && diffCount < 15; i++) {
                if(oldLines[i] !== newLines[i]) {
                    diffHtml += `❌ 修正前: ${oldLines[i]}<br>✅ 修正後: ${newLines[i]}<br>`;
                    diffCount++;
                }
            }
            document.getElementById('diffDisplay').style.display = 'block';
            document.getElementById('diffDisplay').innerHTML = diffHtml;
            currentArticleData = newArticle;
            originalArticleString = newArticleStr;
            displayPreview(currentArticleData);
        } catch(e) {
            alert('修正JSONのパースに失敗: ' + e.message);
        }
    }
    
    function approveFinal() {
        if (!currentArticleData) return alert('記事が読み込まれていません');
        
        const xContent = `📈【桶屋ストーリーAI】\n${currentArticleData.title}\n\n${currentArticleData.causalStory.substring(0,90)}...\n\n🎯 注目低位株\n${currentArticleData.stocks.map(s => `${s.name}(${s.code}) ${s.prediction==='up'?'上昇期待':'下落警戒'}`).join(' / ')}\n\n#株初心者 #低位株 #桶屋理論`;
        
        let noteContent = `# ${currentArticleData.title}\n\n`;
        noteContent += `## 🔍 ニュース連鎖\n\n`;
        currentArticleData.newsChain.forEach(n => {
            noteContent += `### ${n.headline}\n${n.detail}\n\n`;
        });
        noteContent += `## 🧠 桶屋が儲かる理論\n\n${currentArticleData.causalStory}\n\n`;
        noteContent += `## 🎯 注目の低位株\n\n`;
        currentArticleData.stocks.forEach(s => {
            noteContent += `### ${s.name}（${s.code}）\n- 株価: ${s.currentPrice}円\n- 予想: ${s.prediction === 'up' ? '上昇' : '下落'}\n- 理由: ${s.reasoning}\n\n`;
        });
        noteContent += `---\n※本記事は投資助言を目的としたものではありません。`;
        
        document.getElementById('xOutput').value = xContent;
        document.getElementById('noteOutput').value = noteContent;
        document.getElementById('finalOutputCard').style.display = 'block';
        
        // 予測トラッカー追加
        const publishDate = new Date().toISOString();
        for (let stock of currentArticleData.stocks) {
            const exists = predictions.find(p => p.code === stock.code && p.publishDate.split('T')[0] === publishDate.split('T')[0]);
            if (!exists) {
                predictions.push({
                    id: Date.now() + Math.random(),
                    company: stock.name,
                    code: stock.code,
                    priceAtPrediction: stock.currentPrice,
                    direction: stock.prediction,
                    publishDate: publishDate,
                    lastCheckDate: null,
                    status: 'pending',
                    alertShown: false
                });
            }
        }
        saveTracker();
        renderTracker();
        alert('正式記事が生成されました！\n予測トラッカーに追加しました。\n1週間後にアラートが表示されます。');
    }
    
    function copyText(textareaId) {
        const textarea = document.getElementById(textareaId);
        textarea.select();
        textarea.setSelectionRange(0, 99999);
        document.execCommand('copy');
        alert('コピーしました');
    }
    
    // イベント登録
    document.getElementById('generateArticleBtn').addEventListener('click', generatePrompt);
    document.getElementById('copyPromptBtn').addEventListener('click', () => copyText('promptOutput'));
    document.getElementById('applyArticleBtn').addEventListener('click', () => {
        const json = document.getElementById('jsonInput').value;
        if (json.trim()) loadArticleFromJson(json);
        else alert('JSONを貼り付けてください');
    });
    document.getElementById('copyFactCheckBtn').addEventListener('click', () => copyText('factCheckPrompt'));
    document.getElementById('applyRevisedBtn').addEventListener('click', applyRevised);
    document.getElementById('approveFinalBtn').addEventListener('click', approveFinal);
    document.getElementById('copyXBtn').addEventListener('click', () => copyText('xOutput'));
    document.getElementById('copyNoteBtn').addEventListener('click', () => copyText('noteOutput'));
    document.getElementById('showBatchAreaBtn').addEventListener('click', toggleBatchArea);
    document.getElementById('batchCheckPromptBtn').addEventListener('click', generateBatchCheckPrompt);
    document.getElementById('applyAiResultBtn').addEventListener('click', applyBatchAiResult);
    
    // 初期化
    loadTracker();
    
    // 1時間ごとにアラートチェック
    setInterval(() => {
        checkOneWeekAlerts();
    }, 60 * 60 * 1000);
</script>
</body>
</html>
