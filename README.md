<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="MarketIntel">
<meta name="theme-color" content="#0a0e1a">
<title>MarketIntel — 因果連鎖分析</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Serif+JP:wght@400;700;900&family=Noto+Sans+JP:wght@400;700&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#0a0e1a;--surface:rgba(255,255,255,0.03);--border:rgba(99,179,237,0.15);
  --accent:#4299e1;--accent2:#63b3ed;--text:#e2e8f0;--muted:#718096;
  --up:#22c55e;--down:#ef4444;--flat:#f59e0b;
  --serif:'Noto Serif JP',Georgia,serif;--sans:'Noto Sans JP',sans-serif;
  --chain:#a78bfa;--chain-border:rgba(167,139,250,0.25);
}
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
html,body{height:100%;background:var(--bg);color:var(--text);font-family:var(--serif);-webkit-font-smoothing:antialiased;}
body::before{content:'';position:fixed;inset:0;z-index:0;pointer-events:none;
  background-image:linear-gradient(rgba(99,179,237,0.03)1px,transparent 1px),linear-gradient(90deg,rgba(99,179,237,0.03)1px,transparent 1px);
  background-size:36px 36px;}

/* ─── ヘッダー ─── */
.hdr{position:fixed;top:0;left:0;right:0;z-index:100;height:56px;padding:0 14px;
  display:flex;align-items:center;justify-content:space-between;
  border-bottom:1px solid var(--border);background:rgba(10,14,26,0.96);
  backdrop-filter:blur(20px);-webkit-backdrop-filter:blur(20px);}
.logo{display:flex;align-items:center;gap:8px;}
.logo-m{width:27px;height:27px;border-radius:7px;
  background:linear-gradient(135deg,var(--accent2),var(--accent));
  display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:900;color:#fff;font-family:var(--sans);}
.logo-n{font-size:13px;font-weight:700;font-family:var(--sans);}
.logo-s{font-size:9px;color:var(--accent2);letter-spacing:.1em;font-family:var(--sans);}
.tabs{display:flex;gap:2px;}
.tab{padding:5px 9px;border-radius:6px;border:none;cursor:pointer;font-size:11px;font-family:var(--sans);background:transparent;color:var(--muted);transition:.2s;}
.tab.on{background:rgba(99,179,237,.2);color:var(--accent2);}

/* ─── メイン ─── */
.main{position:relative;z-index:1;max-width:680px;margin:0 auto;padding:66px 13px 40px;}
.card{background:var(--surface);border:1px solid var(--border);border-radius:11px;padding:14px;}
.btn{width:100%;padding:12px;border-radius:9px;border:none;font-family:var(--sans);font-size:13px;font-weight:700;cursor:pointer;transition:.2s;display:flex;align-items:center;justify-content:center;gap:6px;}
.btn-p{background:linear-gradient(135deg,var(--accent),#3182ce);color:#fff;box-shadow:0 4px 14px rgba(66,153,225,.3);}
.btn-p:active{transform:scale(.98);}
.btn-p:disabled{opacity:.5;cursor:not-allowed;}
.btn-g{background:rgba(99,179,237,.08);color:var(--accent2);border:1px solid rgba(99,179,237,.2);}
.btn-o{background:transparent;border:1px solid var(--border);color:var(--muted);}
.badge{display:inline-flex;align-items:center;gap:3px;background:rgba(0,0,0,.35);border-radius:5px;padding:2px 7px;font-size:10px;font-family:var(--sans);}
.lbl{font-size:9px;color:var(--accent2);margin-bottom:3px;font-family:var(--sans);letter-spacing:.05em;text-transform:uppercase;}
.mb8{margin-bottom:8px;}.mb12{margin-bottom:12px;}.mb14{margin-bottom:14px;}
.hidden{display:none!important;}
.empty{text-align:center;color:#4a5568;padding:40px 0;font-family:var(--sans);font-size:13px;}

/* ─── セクションタイトル ─── */
.sec-title{font-size:13px;font-weight:700;color:var(--text);margin-bottom:10px;font-family:var(--sans);display:flex;align-items:center;gap:6px;}
.sec-title span{font-size:16px;}

/* ─── ニュース入力エリア ─── */
.news-input-wrap{margin-bottom:14px;}
.news-input-label{font-size:10px;color:var(--accent2);font-family:var(--sans);margin-bottom:5px;letter-spacing:.05em;}
.news-tags{display:flex;flex-wrap:wrap;gap:6px;margin-bottom:10px;min-height:32px;align-items:flex-start;}
.news-tag{display:inline-flex;align-items:center;gap:5px;background:rgba(99,179,237,.1);border:1px solid rgba(99,179,237,.25);border-radius:6px;padding:4px 9px;font-size:11px;font-family:var(--sans);color:var(--accent2);}
.news-tag-del{width:14px;height:14px;border-radius:50%;background:rgba(239,68,68,.2);color:#ef4444;border:none;cursor:pointer;font-size:10px;display:flex;align-items:center;justify-content:center;flex-shrink:0;}
.news-add-row{display:flex;gap:7px;}
.news-text-in{flex:1;padding:9px 11px;background:rgba(255,255,255,.04);border:1px solid var(--border);border-radius:8px;color:var(--text);font-size:12px;font-family:var(--sans);outline:none;}
.news-text-in:focus{border-color:var(--accent);}
.news-add-btn{padding:9px 14px;border-radius:8px;border:1px solid rgba(99,179,237,.3);background:rgba(99,179,237,.08);color:var(--accent2);font-size:12px;font-family:var(--sans);font-weight:700;cursor:pointer;white-space:nowrap;}

/* ─── サンプルボタン ─── */
.sample-row{display:flex;flex-wrap:wrap;gap:5px;margin-bottom:14px;}
.sample-btn{padding:4px 9px;border-radius:5px;border:1px solid rgba(167,139,250,.25);background:rgba(167,139,250,.07);color:#c4b5fd;font-size:10px;font-family:var(--sans);cursor:pointer;transition:.2s;}
.sample-btn:hover{background:rgba(167,139,250,.15);}

/* ─── 因果連鎖チェーン表示 ─── */
.chain-wrap{margin-bottom:16px;}
.chain-step{display:flex;gap:10px;position:relative;}
.chain-step:not(:last-child)::after{content:'';position:absolute;left:13px;top:27px;bottom:-14px;width:2px;
  background:linear-gradient(to bottom,rgba(167,139,250,.4),rgba(167,139,250,.05));}
.chain-step+.chain-step{margin-top:14px;}
.chain-num{width:26px;height:26px;border-radius:50%;
  background:linear-gradient(135deg,#a78bfa,#7c3aed);color:#fff;
  font-size:11px;font-weight:700;font-family:var(--sans);
  display:flex;align-items:center;justify-content:center;flex-shrink:0;
  box-shadow:0 2px 8px rgba(124,58,237,.35);}
.chain-body{flex:1;padding-bottom:4px;}
.chain-head{font-size:12px;font-weight:700;color:var(--text);margin-bottom:3px;}
.chain-desc{font-size:11px;color:#a0aec0;line-height:1.65;font-family:var(--sans);}
.chain-arrow{display:inline-flex;align-items:center;gap:4px;margin-top:5px;
  background:rgba(167,139,250,.1);border:1px solid rgba(167,139,250,.2);
  border-radius:4px;padding:2px 8px;font-size:10px;font-family:var(--sans);color:#c4b5fd;}

/* ─── 注目低位株カード ─── */
.lowprice-header{display:flex;align-items:center;gap:6px;margin-bottom:10px;}
.lowprice-badge{background:linear-gradient(135deg,rgba(250,204,21,.2),rgba(245,158,11,.1));
  border:1px solid rgba(250,204,21,.3);border-radius:6px;padding:3px 9px;
  font-size:10px;font-weight:700;font-family:var(--sans);color:#f59e0b;}
.stock-card{background:rgba(0,0,0,.25);border:1px solid var(--border);border-radius:10px;padding:12px;margin-bottom:8px;}
.stock-card-top{display:flex;align-items:flex-start;justify-content:space-between;gap:8px;margin-bottom:8px;}
.stock-name{font-size:14px;font-weight:700;}
.stock-ticker{font-size:10px;color:var(--muted);font-family:var(--sans);}
.stock-price-tag{flex-shrink:0;background:rgba(34,197,94,.1);border:1px solid rgba(34,197,94,.25);
  border-radius:7px;padding:4px 10px;text-align:center;}
.stock-price-val{font-size:13px;font-weight:700;color:var(--up);font-family:var(--sans);}
.stock-price-lbl{font-size:8px;color:#6ee7b7;font-family:var(--sans);}
.stock-reason{font-size:11px;color:#a0aec0;line-height:1.65;font-family:var(--sans);margin-bottom:8px;}
.stock-chain-tag{display:inline-flex;align-items:center;gap:4px;
  background:rgba(167,139,250,.08);border:1px solid rgba(167,139,250,.2);
  border-radius:4px;padding:2px 8px;font-size:10px;font-family:var(--sans);color:#c4b5fd;margin-right:4px;margin-bottom:3px;}
.confidence-bar{margin-top:8px;}
.confidence-label{display:flex;justify-content:space-between;font-size:9px;color:var(--muted);font-family:var(--sans);margin-bottom:3px;}
.confidence-track{height:4px;background:rgba(255,255,255,.07);border-radius:2px;overflow:hidden;}
.confidence-fill{height:100%;border-radius:2px;background:linear-gradient(90deg,var(--accent),#22c55e);transition:width 1s ease;}

/* ─── 結論ボックス ─── */
.conclusion-box{background:linear-gradient(135deg,rgba(66,153,225,0.08),rgba(99,179,237,0.04));
  border:1px solid rgba(99,179,237,0.3);border-radius:12px;padding:14px 16px;margin-bottom:16px;}
.conclusion-title{font-size:12px;font-weight:700;color:var(--accent2);font-family:var(--sans);margin-bottom:10px;}
.conclusion-item{display:flex;align-items:flex-start;gap:8px;margin-bottom:7px;}
.conclusion-item:last-child{margin-bottom:0;}
.conclusion-icon{width:20px;height:20px;border-radius:50%;background:rgba(99,179,237,.2);
  display:flex;align-items:center;justify-content:center;font-size:10px;flex-shrink:0;margin-top:1px;}
.conclusion-text{font-size:12px;line-height:1.7;color:#cbd5e0;font-family:var(--sans);}

/* ─── ローディング ─── */
.loading-wrap{text-align:center;padding:36px 0;}
.loading-spinner{width:36px;height:36px;border:3px solid rgba(99,179,237,.15);border-top-color:var(--accent2);
  border-radius:50%;animation:spin .8s linear infinite;margin:0 auto 12px;}
@keyframes spin{to{transform:rotate(360deg);}}
.loading-text{font-size:12px;color:var(--muted);font-family:var(--sans);line-height:1.7;}
.loading-step{font-size:11px;color:var(--accent2);font-family:var(--sans);margin-top:6px;opacity:.8;}

/* ─── エラーボックス ─── */
.error-box{background:rgba(239,68,68,.07);border:1px solid rgba(239,68,68,.25);border-radius:9px;padding:12px;margin-bottom:12px;font-size:12px;color:#fca5a5;font-family:var(--sans);line-height:1.65;}

/* ─── 免責 ─── */
.disclaimer{font-size:10px;color:#4a5568;font-family:var(--sans);line-height:1.7;text-align:center;margin-top:20px;padding:0 10px;}

/* ─── コピーボタン ─── */
.cp-btn{margin-top:10px;widt
