[index_15.html](https://github.com/user-attachments/files/32332606/index_15.html)
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Night PASS | 東京ナイトラウンジ・キャバクラ検索</title>
<meta name="description" content="Night PASS（ナイトパス）は、キャバクラ・ラウンジ・クラブなど東京の夜のお店を検索できる紹介サイトです。エリア・業態・キーワードから、気になる一軒を探せます。" id="meta-description">
<link rel="canonical" id="article-canonical">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Shippori+Mincho:wght@500;700;800&family=Zen+Kaku+Gothic+New:wght@400;500;700;900&family=Cormorant+Garamond:ital,wght@0,500;1,500&display=swap" rel="stylesheet">
<style>
  :root{
    /* 案7「淡い水色 雲のようなグラデーション」を採用したライトテーマ。
       footer・toast・小さな削除バッジは従来どおりネイビーの引き締め要素として残す
       （--ink / --ink-elevated / --cream は変更していません）。 */
    --bg:#dceefb;
    --bg-elevated:#eef6fc;
    --card:#ffffff;
    --card-line:#d3e6f4;
    --terracotta:#c9a961;
    --terracotta-soft:#e0c48a;
    --olive:#7ea3c4;
    --olive-soft:#6f93b3;
    --text:#132844;
    --text-muted:#5b7b93;
    --text-faint:#8fa8bd;
    --input-bg:#f4f9fd;
    --ink:#060f1c;
    --ink-elevated:#0a1729;
    --cream:#f3ead0;
    --shadow-warm: 0 0 18px rgba(201,169,97,0.30);
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    background:
      radial-gradient(900px 550px at 18% 15%, rgba(255,255,255,0.95), transparent 60%),
      radial-gradient(1000px 650px at 85% 85%, rgba(179,214,241,0.55), transparent 60%),
      var(--bg);
    color:var(--text);
    font-family:'Zen Kaku Gothic New', sans-serif;
    min-height:100vh;
    -webkit-font-smoothing:antialiased;
  }
  .serif{ font-family:'Shippori Mincho', serif; }
  .eyebrow{
    font-family:'Cormorant Garamond', serif;
    font-style:italic;
    letter-spacing:0.22em;
    color:var(--terracotta);
    font-size:13px;
    text-transform:uppercase;
  }
  a{ color:inherit; text-decoration:none; }
  button{ font-family:inherit; cursor:pointer; }
  input,select,textarea{ font-family:inherit; }

  /* ---------- topbar (紺・ゴールドの額縁) ---------- */
  .topbar{
    display:flex; align-items:center; justify-content:space-between;
    padding:22px clamp(18px,4vw,56px);
    border-bottom:1px solid rgba(201,169,97,0.22);
    position:sticky; top:0; z-index:40;
    background:rgba(255,255,255,0.85);
    backdrop-filter:blur(10px);
  }
  .brand{ display:flex; align-items:center; gap:10px; cursor:pointer; }
  .brand-icon{ flex:0 0 auto; display:block; }
  .brand-text{ display:flex; flex-direction:column; gap:2px; }
  .brand .mark{
    font-family:'Shippori Mincho', serif;
    font-weight:800;
    font-size:22px;
    letter-spacing:0.06em;
    color:var(--terracotta);
  }
  .brand .sub{ font-size:10px; letter-spacing:0.32em; color:#8fa8bd; }
  .nav-actions{ display:flex; align-items:center; gap:10px; }
  .btn-ghost{
    background:transparent; border:1px solid var(--card-line); color:var(--text-muted);
    padding:9px 16px; border-radius:999px; font-size:13px; letter-spacing:0.03em;
    transition:.2s;
  }
  .btn-ghost:hover{ border-color:var(--terracotta); color:var(--terracotta); }

  main{ display:none; }
  main.active{ display:block; }

  /* ---------- hero / search ---------- */
  .hero{
    padding:56px clamp(18px,4vw,56px) 20px;
    text-align:center;
  }
  .hero h1{
    font-family:'Shippori Mincho', serif;
    font-weight:800;
    font-size:clamp(28px,4.4vw,46px);
    line-height:1.35;
    margin:14px 0 8px;
    text-wrap:balance;
  }
  .hero h1 .accent{ color:var(--terracotta); }
  .hero p.lead{ color:var(--text-muted); font-size:14.5px; max-width:520px; margin:0 auto; line-height:1.9;}

  .search-panel{
    max-width:920px; margin:34px auto 0;
    background:linear-gradient(180deg, #ffffff, #f8fbfe);
    border:1px solid var(--card-line);
    border-radius:18px;
    padding:20px clamp(14px,3vw,28px);
    box-shadow: 0 20px 50px rgba(19,40,68,0.10);
    position:relative;
  }
  .search-panel::before{
    content:"";
    position:absolute; inset:-1px;
    border-radius:18px;
    padding:1px;
    background:linear-gradient(120deg, rgba(201,169,97,0.45), transparent 30%, transparent 70%, rgba(19,40,68,0.12));
    -webkit-mask:linear-gradient(#000 0 0) content-box, linear-gradient(#000 0 0);
    -webkit-mask-composite:xor; mask-composite:exclude;
    pointer-events:none;
  }
  .search-grid{
    display:grid;
    grid-template-columns: 1.3fr 1fr 1fr 1fr auto;
    gap:12px;
  }
  @media (max-width:900px){ .search-grid{ grid-template-columns: 1fr 1fr; } }

  .field label{
    display:block; font-size:11px; letter-spacing:0.14em; color:var(--text-faint);
    margin-bottom:6px; text-transform:uppercase;
  }
  .field input, .field select{
    width:100%; background:var(--input-bg); border:1px solid var(--card-line);
    color:var(--text); padding:11px 12px; border-radius:9px; font-size:14px; outline:none;
    transition:.15s;
  }
  .field input:focus, .field select:focus{ border-color:var(--terracotta); box-shadow:0 0 0 3px rgba(201,169,97,0.16); }
  .field select{ appearance:none; background-image:linear-gradient(45deg, transparent 50%, var(--terracotta) 50%), linear-gradient(135deg, var(--terracotta) 50%, transparent 50%); background-position: calc(100% - 18px) center, calc(100% - 13px) center; background-size:5px 5px, 5px 5px; background-repeat:no-repeat; }

  .btn-search{
    background:linear-gradient(120deg, var(--terracotta), #93773c);
    border:none; color:#0e1c2e; font-weight:700; padding:0 26px; border-radius:9px; font-size:14px;
    letter-spacing:0.04em; box-shadow:0 8px 22px rgba(201,169,97,0.32);
    transition:.2s; white-space:nowrap;
  }
  .btn-search:hover{ transform:translateY(-1px); box-shadow:0 10px 26px rgba(201,169,97,0.44); }

  /* ---------- quick icon filters ---------- */
  .quick-filters{
    max-width:1180px; margin:36px auto 0; padding:0 clamp(18px,4vw,56px);
    display:flex; flex-direction:column; gap:24px;
  }
  .quick-block .quick-label{
    font-size:11.5px; letter-spacing:0.14em; color:var(--text-faint); text-transform:uppercase;
    margin-bottom:12px; display:flex; align-items:center; gap:8px;
  }
  .quick-block .quick-label::after{ content:""; flex:1; height:1px; background:var(--card-line); }
  .quick-icons{ display:flex; gap:16px; flex-wrap:wrap; }
  .quick-chip{
    display:flex; flex-direction:column; align-items:center; gap:8px; width:76px;
    cursor:pointer; background:none; border:none; padding:0; color:inherit;
  }
  .quick-chip .circle{
    width:58px; height:58px; border-radius:50%; background:var(--card); border:1px solid var(--card-line);
    display:flex; align-items:center; justify-content:center; transition:.2s;
    box-shadow:0 2px 8px rgba(6,15,28,0.10);
  }
  .quick-chip .circle svg{ width:23px; height:23px; stroke:var(--text-muted); fill:none; }
  .quick-chip .label{ font-size:11.5px; color:var(--text-muted); text-align:center; line-height:1.3; transition:.2s; }
  .quick-chip:hover .circle{ border-color:var(--terracotta); transform:translateY(-2px); }
  .quick-chip.active .circle{
    background:linear-gradient(135deg, rgba(201,169,97,0.22), rgba(6,15,28,0.18));
    border-color:var(--terracotta); box-shadow:var(--shadow-warm);
  }
  .quick-chip.active .circle svg{ stroke:var(--terracotta); }
  .quick-chip.active .label{ color:var(--terracotta); }

  /* 人気エリアのクイックフィルター：アイコンなしの長方形ボックスに地名だけを表示 */
  .quick-chip.area-box-chip{ width:auto; }
  .quick-chip .area-box{
    min-width:76px; height:46px; padding:0 18px; border-radius:10px;
    background:var(--card); border:1px solid var(--card-line);
    display:flex; align-items:center; justify-content:center; transition:.2s;
    box-shadow:0 2px 8px rgba(6,15,28,0.10);
    font-size:13px; font-weight:700; color:var(--text-muted); white-space:nowrap;
  }
  .quick-chip:hover .area-box{ border-color:var(--terracotta); transform:translateY(-2px); }
  .quick-chip.active .area-box{
    background:linear-gradient(135deg, rgba(201,169,97,0.22), rgba(6,15,28,0.18));
    border-color:var(--terracotta); box-shadow:var(--shadow-warm); color:var(--terracotta);
  }

  .result-meta{
    max-width:1180px; margin:38px auto 14px; padding:0 clamp(18px,4vw,56px);
    display:flex; align-items:baseline; justify-content:space-between; gap:12px; flex-wrap:wrap;
  }
  .result-meta h2{ font-family:'Shippori Mincho',serif; font-size:19px; font-weight:700; margin:0; }
  .result-meta .count{ color:var(--terracotta); }
  .sort-inline{ display:flex; align-items:center; gap:10px; font-size:12.5px; color:var(--text-muted); flex-wrap:wrap; }
  .sort-inline select{ background:var(--card); border:1px solid var(--card-line); color:var(--text); border-radius:7px; padding:6px 10px; font-size:12.5px; }
  .loc-btn{
    background:var(--card); border:1px solid var(--card-line); color:var(--text-muted);
    padding:7px 14px; border-radius:999px; font-size:12.5px; display:inline-flex; align-items:center; gap:6px;
    transition:.2s;
  }
  .loc-btn:hover{ border-color:var(--terracotta); color:var(--terracotta); }
  .loc-btn.active{ border-color:var(--olive-soft); color:var(--olive-soft); background:rgba(111,147,179,0.14); }
  .dist-badge{ font-size:11px; color:var(--text-faint); margin-top:2px; }

  /* ---------- grid / cards ---------- */
  .grid{
    max-width:1180px; margin:0 auto; padding:0 clamp(18px,4vw,56px) 70px;
    display:grid; grid-template-columns:repeat(auto-fill, minmax(268px,1fr)); gap:20px;
  }
  .card{
    background:var(--card); border:1px solid var(--card-line); border-radius:16px; overflow:hidden;
    cursor:pointer; transition:.22s; display:flex; flex-direction:column;
    box-shadow:0 2px 10px rgba(6,15,28,0.06);
  }
  .show-all-wrap{ grid-column:1/-1; text-align:center; padding:16px 0 6px; }
  .btn-show-all{
    background:transparent; border:1px solid var(--terracotta); color:var(--terracotta);
    padding:13px 32px; border-radius:999px; font-size:13.5px; font-weight:700; cursor:pointer; transition:.18s;
  }
  .btn-show-all:hover{ background:rgba(201,169,97,0.12); }
  .card:hover{ transform:translateY(-4px); border-color:rgba(201,169,97,0.5); box-shadow:0 16px 34px rgba(6,15,28,0.14); }
  .card .photo{
    height:150px; position:relative; display:flex; align-items:center; justify-content:center;
    font-family:'Shippori Mincho',serif; font-size:40px; font-weight:800; color:rgba(201,169,97,0.35);
    overflow:hidden; background:linear-gradient(160deg, #1c3454, #142943);
  }
  .card .photo img{ width:100%; height:100%; object-fit:cover; }
  .card .photo .badge{
    position:absolute; top:10px; left:10px; background:rgba(6,15,28,0.06); border:1px solid rgba(201,169,97,0.5);
    color:var(--terracotta); font-size:10.5px; padding:4px 9px; border-radius:999px; letter-spacing:0.04em;
  }
  .card .body{ padding:16px 16px 18px; display:flex; flex-direction:column; gap:8px; flex:1; }
  .card .name{ font-family:'Shippori Mincho',serif; font-weight:700; font-size:17px; }
  .card .loc{ font-size:12px; color:var(--text-muted); letter-spacing:0.02em; }
  .card .catch{ font-size:12.5px; color:var(--text-muted); line-height:1.7; flex:1; }
  .card .foot{ display:flex; align-items:center; justify-content:space-between; margin-top:4px; }
  .budget{ color:var(--terracotta); font-weight:700; font-size:13px; }
  .tags{ display:flex; flex-wrap:wrap; gap:6px; }
  .tag{ font-size:10.5px; color:var(--olive-soft); border:1px solid rgba(111,147,179,0.45); padding:3px 8px; border-radius:999px; }
  .empty{ grid-column:1/-1; text-align:center; padding:70px 20px; color:var(--text-faint); }
  .empty .serif{ font-size:18px; color:var(--text-muted); display:block; margin-bottom:8px; }

  /* ---------- detail ---------- */
  .detail-wrap{ max-width:820px; margin:0 auto; padding:26px clamp(18px,4vw,56px) 80px; }
  .back{ display:inline-flex; align-items:center; gap:6px; color:var(--text-muted); font-size:13px; margin-bottom:18px; }
  .back:hover{ color:var(--terracotta); }
  .detail-photo{
    width:100%; aspect-ratio:16/9; border-radius:18px; overflow:hidden; position:relative;
    background:linear-gradient(160deg, #1c3454, #142943); border:1px solid var(--card-line);
    display:flex; align-items:center; justify-content:center;
    font-family:'Shippori Mincho',serif; font-size:56px; color:rgba(201,169,97,0.35); font-weight:800;
  }
  .detail-photo img{ width:100%; height:100%; object-fit:cover; cursor:zoom-in; }
  .thumb-row{ display:flex; gap:10px; margin-top:12px; }
  .thumb{
    flex:1 1 0; min-width:0; aspect-ratio:16/9; border-radius:8px; overflow:hidden; padding:0;
    border:2px solid transparent; background:none; cursor:pointer; opacity:.65; transition:.15s;
  }
  .thumb img{ width:100%; height:100%; object-fit:cover; display:block; cursor:zoom-in; }
  .thumb:hover{ opacity:1; }
  .thumb.active{ border-color:var(--terracotta); opacity:1; }

  /* ---------- lightbox (photo popup) ---------- */
  .lightbox{
    position:fixed; inset:0; background:rgba(3,8,16,0.92); z-index:200;
    display:none; align-items:center; justify-content:center; padding:34px;
    cursor:zoom-out;
  }
  .lightbox.show{ display:flex; }
  .lightbox img{
    max-width:92vw; max-height:88vh; object-fit:contain; border-radius:12px;
    box-shadow:0 24px 70px rgba(0,0,0,0.55); cursor:default;
  }
  .lightbox-close{
    position:absolute; top:20px; right:22px; width:42px; height:42px; border-radius:50%;
    background:rgba(255,255,255,0.08); border:1px solid rgba(255,255,255,0.28); color:#f3ead0;
    font-size:19px; line-height:1; display:flex; align-items:center; justify-content:center;
    cursor:pointer; transition:.15s;
  }
  .lightbox-close:hover{ background:rgba(255,255,255,0.16); border-color:var(--terracotta); color:var(--terracotta); }
  .detail-head{ margin-top:22px; display:flex; align-items:flex-start; justify-content:space-between; gap:16px; flex-wrap:wrap; }
  .detail-head .eyebrow{ display:block; margin-bottom:6px; }
  .detail-head h1{ font-family:'Shippori Mincho',serif; font-size:clamp(24px,3.4vw,32px); margin:0 0 6px; font-weight:800; text-wrap:balance; }
  .detail-head .loc{ color:var(--text-muted); font-size:13.5px; }
  .sns-row{ display:flex; gap:10px; }
  .sns-btn{
    width:42px; height:42px; border-radius:50%; border:1px solid var(--card-line);
    display:flex; align-items:center; justify-content:center; background:var(--card);
    transition:.2s;
  }
  .sns-btn svg{ width:19px; height:19px; stroke:var(--text-muted); fill:none; }
  .sns-btn:hover{ border-color:var(--terracotta); box-shadow:var(--shadow-warm); }
  .sns-btn:hover svg{ stroke:var(--terracotta); }
  .sns-btn.disabled{ opacity:0.3; pointer-events:none; }

  .detail-stats{ display:flex; gap:10px; flex-wrap:wrap; margin:22px 0 6px; }
  .stat-chip{ background:var(--card); border:1px solid var(--card-line); border-radius:11px; padding:10px 16px; }
  .stat-chip .k{ font-size:10.5px; color:var(--text-faint); letter-spacing:0.08em; }
  .stat-chip .v{ font-size:15px; color:var(--terracotta); font-weight:700; margin-top:2px; }

  .detail-tags{ display:flex; flex-wrap:wrap; gap:8px; margin:18px 0; }
  .section-title{ font-family:'Shippori Mincho',serif; font-size:16px; font-weight:700; margin:30px 0 10px; padding-bottom:8px; border-bottom:1px solid var(--card-line); }
  .desc{ color:var(--text-muted); line-height:2; font-size:14.5px; white-space:pre-wrap; }
  .store-desc-body{ display:flex; flex-direction:column; gap:16px; }
  .store-desc-body p{ color:var(--text-muted); line-height:2; font-size:14.5px; white-space:pre-wrap; margin:0; }
  .store-desc-body .desc-img{ width:100%; border-radius:14px; border:1px solid var(--card-line); display:block; }
  .store-desc-body .desc-img-caption{ font-size:12px; color:var(--text-faint); text-align:center; margin-top:-10px; }

  .info-grid{ display:flex; flex-direction:column; gap:10px; }
  .info-row{ display:flex; gap:16px; font-size:13.5px; padding:10px 0; border-bottom:1px dashed var(--card-line); }
  .info-row:last-child{ border-bottom:none; }
  .info-row .ik{ width:88px; flex-shrink:0; color:var(--text-faint); font-size:11.5px; letter-spacing:0.06em; padding-top:2px; }
  .info-row .iv{ color:var(--text); line-height:1.7; }
  .map-link{ color:var(--terracotta); font-size:12.5px; margin-left:8px; white-space:nowrap; }
  .map-link:hover{ text-decoration:underline; }

  /* ---------- cast (在籍キャスト) ---------- */
  .cast-grid{ display:grid; grid-template-columns:repeat(auto-fill, minmax(130px,1fr)); gap:14px; }
  .cast-card{ background:var(--card); border:1px solid var(--card-line); border-radius:13px; padding:16px 10px; text-align:center; }
  .cast-avatar{
    width:52px; height:52px; border-radius:50%; margin:0 auto 10px; color:var(--cream);
    display:flex; align-items:center; justify-content:center;
    font-family:'Shippori Mincho',serif; font-weight:800; font-size:19px;
  }
  .cast-avatar-photo{ overflow:hidden; }
  .cast-avatar-photo img{ width:100%; height:100%; object-fit:cover; display:block; }
  .cast-name{ font-size:13.5px; font-weight:700; color:var(--text); }
  .cast-catch{ font-size:11.5px; color:var(--text-muted); line-height:1.6; margin-top:5px; }

  .apply-bar{
    margin-top:34px; display:flex; gap:16px; flex-wrap:wrap; align-items:center;
    padding:20px; border-radius:14px; background:linear-gradient(120deg, rgba(201,169,97,0.14), rgba(6,15,28,0.12));
    border:1px solid var(--card-line);
  }
  .apply-buttons{ display:flex; flex-direction:column; gap:10px; }
  .btn-apply{
    background:linear-gradient(120deg, var(--terracotta), #93773c); color:#0e1c2e; border:none; padding:13px 26px;
    border-radius:999px; font-weight:700; font-size:14px; box-shadow:0 8px 22px rgba(201,169,97,0.32);
    text-align:center;
  }
  .btn-line{
    display:inline-flex; align-items:center; justify-content:center;
    background:#06C755; color:#fff; border:none; padding:12px 26px;
    border-radius:999px; font-weight:700; font-size:13.5px; box-shadow:0 6px 18px rgba(6,199,85,0.30);
    width:fit-content; transition:.2s;
  }
  .btn-line:hover{ filter:brightness(1.06); transform:translateY(-1px); }
  .apply-bar .info{ font-size:12.5px; color:var(--text-muted); }

  /* ---------- admin ---------- */
  .admin-wrap{ max-width:960px; margin:0 auto; padding:34px clamp(18px,4vw,56px) 90px; }
  .admin-gate{ max-width:360px; margin:80px auto; text-align:center; }
  .admin-gate .serif{ font-size:20px; margin-bottom:14px; display:block; }
  .admin-gate input{ width:100%; background:var(--card); border:1px solid var(--card-line); color:var(--text); padding:12px 14px; border-radius:9px; margin:14px 0; text-align:center; letter-spacing:0.1em; }
  .admin-gate .hint{ font-size:11.5px; color:var(--text-faint); margin-top:8px; }
  .admin-header{ display:flex; align-items:center; justify-content:space-between; margin-bottom:22px; flex-wrap:wrap; gap:10px; }
  .admin-header h1{ font-family:'Shippori Mincho',serif; font-size:24px; margin:0; }

  /* ---------- manager cards (popular areas / tag presets) ---------- */
  .manager-card{ background:var(--card); border:1px solid var(--card-line); border-radius:14px; padding:20px 22px; margin-bottom:18px; }
  .manager-card h3{ font-family:'Shippori Mincho',serif; font-size:15px; margin:0 0 4px; }
  .manager-card .field-hint{ margin-top:0; }
  .manager-chips{ display:flex; flex-wrap:wrap; gap:8px; margin:14px 0; }
  .manager-chip{
    display:inline-flex; align-items:center; gap:6px; background:var(--input-bg); border:1px solid var(--card-line);
    color:var(--text); font-size:12.5px; padding:6px 6px 6px 13px; border-radius:999px;
  }
  .manager-chip-label{ cursor:pointer; }
  .manager-chip-label:hover{ color:var(--terracotta); text-decoration:underline; }
  .chip-x{ background:none; border:none; color:var(--text-faint); font-size:15px; line-height:1; cursor:pointer; padding:3px 5px; border-radius:50%; }
  .chip-x:hover{ color:#e0685a; background:rgba(224,104,90,0.16); }
  .manager-add-row{ display:flex; gap:8px; flex-wrap:wrap; }
  .manager-add-row input{
    flex:1; background:var(--input-bg); border:1px solid var(--card-line); border-radius:8px;
    padding:9px 12px; font-size:13px; color:var(--text); outline:none; min-width:120px;
  }
  .manager-add-row input:focus{ border-color:var(--terracotta); }
  .manager-add-row select{
    background:var(--input-bg); border:1px solid var(--card-line); border-radius:8px;
    padding:9px 10px; font-size:13px; color:var(--text); outline:none; flex:0 0 auto;
  }
  .manager-add-row select:focus{ border-color:var(--terracotta); }
  .btn-manager-add{ background:var(--terracotta); color:#0e1c2e; border:none; padding:0 20px; border-radius:8px; font-size:13px; font-weight:700; }
  .btn-manager-add:hover{ background:var(--terracotta-soft); }
  .manager-empty{ color:var(--text-faint); font-size:12.5px; padding:2px 0 12px; }

  /* ---------- tag presets inside store form ---------- */
  .tag-preset-chips{ display:flex; flex-wrap:wrap; gap:6px; margin-top:9px; }
  .tag-chip{
    background:var(--input-bg); border:1px solid var(--card-line); color:var(--text-muted);
    font-size:11.5px; padding:5px 11px; border-radius:999px; cursor:pointer; transition:.15s;
  }
  .tag-chip:hover{ border-color:var(--terracotta); color:var(--terracotta); }
  .tag-chip.active{ background:rgba(201,169,97,0.18); border-color:var(--terracotta); color:var(--terracotta); font-weight:700; }

  /* ---------- area chip picker (single-row horizontal scroll) ---------- */
  .area-chip-scroll{
    display:flex; flex-wrap:nowrap; gap:7px; overflow-x:auto; overflow-y:hidden;
    padding:4px 2px 10px; margin-top:6px; -webkit-overflow-scrolling:touch;
  }
  .area-chip-scroll::-webkit-scrollbar{ height:6px; }
  .area-chip-scroll::-webkit-scrollbar-thumb{ background:var(--card-line); border-radius:99px; }
  .area-chip{
    flex:0 0 auto; white-space:nowrap; background:var(--input-bg); border:1px solid var(--card-line);
    color:var(--text-muted); font-size:12px; padding:7px 14px; border-radius:999px; cursor:pointer; transition:.15s;
  }
  .area-chip:hover{ border-color:var(--terracotta); color:var(--terracotta); }
  .area-chip.active{ background:rgba(201,169,97,0.18); border-color:var(--terracotta); color:var(--terracotta); font-weight:700; }
  .area-chip.normal-area{ border-style:dashed; }
  .area-chip.normal-area.active{ background:rgba(126,163,196,0.18); border-color:var(--olive); color:var(--olive-soft); border-style:solid; }

  /* ---------- photo upload slots (admin) ---------- */
  .photo-slots{ display:flex; gap:14px; flex-wrap:wrap; margin-top:8px; }
  .photo-slot{ display:flex; flex-direction:column; align-items:center; gap:6px; }
  .photo-drop{
    width:128px; height:128px; border:1.5px dashed var(--card-line); border-radius:12px;
    background:var(--input-bg); display:flex; align-items:center; justify-content:center;
    cursor:pointer; overflow:hidden; position:relative; transition:.15s;
  }
  .photo-drop:hover{ border-color:var(--terracotta); background:rgba(201,169,97,0.08); }
  .photo-drop.drag-over{ border-color:var(--terracotta); background:rgba(201,169,97,0.15); }
  .photo-drop.has-image{ border-style:solid; }
  .photo-drop img{ width:100%; height:100%; object-fit:cover; }
  .photo-drop-hint{ display:flex; flex-direction:column; align-items:center; gap:4px; color:var(--text-faint); font-size:11px; text-align:center; line-height:1.5; padding:8px; }
  .photo-drop-hint span{ font-size:24px; line-height:1; color:var(--terracotta); }
  .photo-remove{ background:none; border:none; color:var(--text-faint); font-size:11.5px; cursor:pointer; padding:2px 6px; }
  .photo-remove:hover{ color:#e0685a; }
  .photo-slot-label{ font-size:11px; color:var(--text-faint); }
  .admin-panel{ display:grid; grid-template-columns: 1fr 1.3fr; gap:22px; align-items:start; }
  @media (max-width:860px){ .admin-panel{ grid-template-columns:1fr; } }
  .admin-list{ background:var(--card); border:1px solid var(--card-line); border-radius:14px; padding:10px; max-height:640px; overflow:auto; }
  .admin-row{ display:flex; align-items:center; justify-content:space-between; padding:12px 10px; border-radius:9px; cursor:pointer; gap:8px; }
  .admin-row:hover{ background:rgba(201,169,97,0.07); }
  .admin-row.active{ background:rgba(201,169,97,0.13); border:1px solid rgba(201,169,97,0.35); }
  .admin-row .rn{ font-size:13.5px; font-weight:700; }
  .admin-row .ra{ font-size:11px; color:var(--text-faint); }
  .admin-row .del{ color:var(--text-faint); font-size:12px; padding:5px 8px; border-radius:6px; }
  .admin-row .del:hover{ color:#e0685a; background:rgba(224,104,90,0.16); }
  .admin-add{ width:100%; margin-top:10px; background:transparent; border:1px dashed var(--card-line); color:var(--terracotta); padding:11px; border-radius:9px; font-size:13px; }
  .admin-add:hover{ border-color:var(--terracotta); }
  .admin-list-toolbar{ display:flex; align-items:center; justify-content:flex-end; gap:8px; font-size:12.5px; color:var(--text-muted); margin-bottom:8px; }
  .admin-list-toolbar select{ background:var(--card); border:1px solid var(--card-line); color:var(--text); border-radius:7px; padding:6px 10px; font-size:12.5px; }
  .admin-list-pager{ display:flex; align-items:center; justify-content:center; gap:10px; margin-top:10px; font-size:12.5px; color:var(--text-muted); flex-wrap:wrap; }
  .admin-list-pager button{ background:var(--input-bg); border:1px solid var(--card-line); color:var(--text-muted); padding:6px 14px; border-radius:8px; cursor:pointer; font-size:12.5px; }
  .admin-list-pager button:hover:not(:disabled){ border-color:var(--terracotta); color:var(--terracotta); }
  .admin-list-pager button:disabled{ opacity:.4; cursor:default; }
  .admin-list-pager .page-info{ white-space:nowrap; }

  .admin-form{ background:var(--card); border:1px solid var(--card-line); border-radius:14px; padding:22px; }
  .admin-form h3{ font-family:'Shippori Mincho',serif; margin:0 0 16px; font-size:16px; }
  .form-grid{ display:grid; grid-template-columns:1fr 1fr; gap:12px; }
  .form-grid .full{ grid-column:1/-1; }
  .form-grid label{ display:block; font-size:11px; color:var(--text-faint); letter-spacing:0.06em; margin-bottom:5px; }
  .form-grid input, .form-grid select, .form-grid textarea{
    width:100%; background:var(--input-bg); border:1px solid var(--card-line); color:var(--text);
    padding:10px 11px; border-radius:8px; font-size:13.5px; outline:none;
  }
  .form-grid textarea{ resize:vertical; min-height:100px; line-height:1.7; }
  .form-grid input:focus, .form-grid select:focus, .form-grid textarea:focus{ border-color:var(--terracotta); }
  .form-actions{ display:flex; gap:10px; margin-top:18px; align-items:center; }
  .btn-save{ background:linear-gradient(120deg, var(--terracotta), #93773c); border:none; color:#0e1c2e; font-weight:800; padding:11px 22px; border-radius:9px; font-size:13.5px; }
  .save-flag{ font-size:12px; color:var(--terracotta); opacity:0; transition:.3s; }
  .save-flag.show{ opacity:1; }
  .field-hint{ font-size:10.5px; color:var(--text-faint); margin-top:4px; }

  .cast-row{ display:flex; gap:8px; align-items:center; margin-bottom:8px; }
  .cast-row input{
    flex:1; background:var(--input-bg); border:1px solid var(--card-line); color:var(--text);
    padding:9px 11px; border-radius:8px; font-size:13px; outline:none;
  }
  .cast-row input:focus{ border-color:var(--terracotta); }
  .cast-photo-wrap{ position:relative; flex-shrink:0; }
  .cast-photo-drop{
    width:44px; height:44px; border-radius:50%; flex-shrink:0; position:relative;
    border:1.5px dashed var(--card-line); background:var(--input-bg);
    display:flex; align-items:center; justify-content:center; cursor:pointer; overflow:hidden; transition:.15s;
  }
  .cast-photo-drop:hover{ border-color:var(--terracotta); }
  .cast-photo-drop.has-image{ border-style:solid; }
  .cast-photo-drop img{ width:100%; height:100%; object-fit:cover; display:block; }
  .cast-photo-drop .plus{ font-size:15px; color:var(--terracotta); line-height:1; }
  .cast-photo-remove{
    position:absolute; top:-4px; right:-4px; width:16px; height:16px; border-radius:50%;
    background:var(--ink-elevated); border:1px solid var(--card-line); color:var(--text-faint);
    font-size:10px; line-height:14px; text-align:center; cursor:pointer; padding:0;
  }
  .cast-photo-remove:hover{ color:#e0685a; }

  .toast{
    position:fixed; bottom:24px; left:50%; transform:translateX(-50%) translateY(20px);
    background:var(--ink); border:1px solid rgba(201,169,97,0.3); color:var(--cream);
    padding:12px 22px; border-radius:999px; font-size:13px; box-shadow:0 10px 30px rgba(6,15,28,0.25);
    opacity:0; pointer-events:none; transition:.25s; z-index:100;
  }
  .toast.show{ opacity:1; transform:translateX(-50%) translateY(0); }

  footer{ text-align:center; padding:30px; background:var(--ink); color:#b3a173; font-size:11.5px; border-top:1px solid rgba(201,169,97,0.22); }
  .footer-links{ display:flex; justify-content:center; gap:18px; margin-bottom:12px; flex-wrap:wrap; }
  .footer-links a{ color:#d8cdb4; font-size:12px; letter-spacing:0.03em; }
  .footer-links a:hover{ color:var(--terracotta); text-decoration:underline; }

  /* ---------- static pages (利用規約 / 運営会社情報) ---------- */
  .static-page{ max-width:760px; margin:0 auto; padding:40px clamp(18px,4vw,56px) 90px; }
  .static-page h1{ font-family:'Shippori Mincho',serif; font-size:clamp(22px,3vw,28px); margin:0 0 24px; font-weight:800; }
  .static-page .desc{ color:var(--text-muted); line-height:2; font-size:14.5px; white-space:pre-wrap; }
  .static-page .empty-note{ color:var(--text-faint); font-size:13.5px; }
  .company-table{ display:flex; flex-direction:column; gap:0; }
  .company-table .info-row{ display:flex; gap:16px; font-size:13.5px; padding:14px 0; border-bottom:1px dashed var(--card-line); }
  .company-table .info-row:last-child{ border-bottom:none; }
  .company-table .ik{ width:120px; flex-shrink:0; color:var(--text-faint); font-size:11.5px; letter-spacing:0.06em; padding-top:2px; }
  .company-table .iv{ color:var(--text); line-height:1.8; white-space:pre-wrap; }
  .toggle-row{ display:flex; align-items:center; gap:10px; margin:14px 0; font-size:13px; color:var(--text-muted); }
  .toggle-row input{ width:16px; height:16px; accent-color:var(--terracotta); cursor:pointer; }
  .publish-badge{ display:inline-flex; align-items:center; gap:6px; font-size:11.5px; padding:4px 11px; border-radius:999px; font-weight:700; }
  .publish-badge.on{ background:rgba(80,180,120,0.16); color:#6fce9a; border:1px solid rgba(80,180,120,0.35); }
  .publish-badge.off{ background:rgba(201,169,97,0.10); color:var(--text-faint); border:1px solid var(--card-line); }
  .platinum-badge{ display:inline-flex; align-items:center; font-size:10px; font-weight:700; padding:2px 8px; border-radius:999px; margin-left:6px; background:rgba(201,169,97,0.18); color:var(--terracotta); border:1px solid rgba(201,169,97,0.4); vertical-align:middle; }
  .platinum-count-hint{ font-size:12px; color:var(--text-muted); margin:-6px 0 14px; }
  .platinum-count-hint.over{ color:#e0685a; }
  .admin-tabs{ display:flex; gap:8px; margin:14px 0 18px; border-bottom:1px solid var(--card-line); }
  .admin-tab-btn{
    background:none; border:none; border-bottom:2px solid transparent; color:var(--text-muted);
    padding:9px 4px; margin-bottom:-1px; font-size:13.5px; font-weight:700; cursor:pointer; transition:.15s;
  }
  .admin-tab-btn + .admin-tab-btn{ margin-left:14px; }
  .admin-tab-btn:hover{ color:var(--terracotta); }
  .admin-tab-btn.active{ color:var(--terracotta); border-bottom-color:var(--terracotta); }

  /* ---------- コラム / ブログ (columns) ---------- */
  .publish-badge.scheduled{ background:rgba(126,163,196,0.16); color:var(--olive); border:1px solid rgba(126,163,196,0.4); }
  .columns-page{ max-width:1180px; }
  .column-grid{
    display:grid; grid-template-columns:repeat(auto-fill, minmax(268px,1fr)); gap:20px; margin-top:10px;
  }
  .column-card{
    background:var(--card); border:1px solid var(--card-line); border-radius:16px; overflow:hidden;
    cursor:pointer; transition:.22s; display:flex; flex-direction:column;
    box-shadow:0 2px 10px rgba(6,15,28,0.06);
  }
  .column-card:hover{ transform:translateY(-4px); border-color:rgba(201,169,97,0.5); box-shadow:0 16px 34px rgba(6,15,28,0.14); }
  .column-card .photo{
    height:150px; position:relative; display:flex; align-items:center; justify-content:center;
    font-family:'Shippori Mincho',serif; font-size:34px; font-weight:800; color:rgba(201,169,97,0.35);
    overflow:hidden; background:linear-gradient(160deg, #1c3454, #142943);
  }
  .column-card .photo img{ width:100%; height:100%; object-fit:cover; }
  .column-card .body{ padding:16px 16px 18px; display:flex; flex-direction:column; gap:8px; flex:1; }
  .column-card .name{ font-family:'Shippori Mincho',serif; font-weight:700; font-size:16px; line-height:1.5; }
  .column-card .excerpt{ font-size:12.5px; color:var(--text-muted); line-height:1.7; flex:1; }
  .column-meta{ font-size:11.5px; color:var(--text-faint); letter-spacing:0.02em; }
  .article-cover{
    width:100%; aspect-ratio:16/9; border-radius:18px; overflow:hidden; position:relative;
    background:linear-gradient(160deg, #1c3454, #142943); border:1px solid var(--card-line);
  }
  .article-cover img{ width:100%; height:100%; object-fit:cover; }
  .article-date{ font-size:12.5px; color:var(--text-faint); margin-top:10px; }
  .article-body{ margin-top:24px; display:flex; flex-direction:column; gap:18px; }
  .article-body h2{ font-family:'Shippori Mincho',serif; font-size:clamp(19px,2.4vw,23px); font-weight:800; margin:10px 0 0; color:var(--text); }
  .article-body h3{ font-family:'Shippori Mincho',serif; font-size:clamp(16px,2vw,18px); font-weight:700; margin:6px 0 0; color:var(--text); }
  .article-body p{ font-size:14.5px; line-height:2; color:var(--text-muted); white-space:pre-wrap; margin:0; }
  .article-body .article-img{ width:100%; border-radius:14px; border:1px solid var(--card-line); display:block; }
  .article-body .img-caption{ font-size:12px; color:var(--text-faint); text-align:center; margin-top:-8px; }
  .article-body .article-link a{ color:var(--terracotta); font-size:14px; text-decoration:underline; }
  .article-btn-wrap{ text-align:center; margin:6px 0; }
  .article-btn{ display:inline-block; background:var(--terracotta); color:#0e1c2e; padding:12px 30px; border-radius:999px; font-weight:700; font-size:13.5px; }
  .article-btn:hover{ background:var(--terracotta-soft); }
  .article-not-found{ text-align:center; padding:70px 20px; color:var(--text-faint); }

  /* ---------- admin: article block editor ---------- */
  .block-row{
    background:var(--card); border:1px solid var(--card-line); border-radius:10px; padding:12px;
    display:flex; flex-direction:column; gap:8px;
  }
  .block-row + .block-row{ margin-top:10px; }
  .block-row-head{ display:flex; align-items:center; justify-content:space-between; gap:8px; }
  .block-type-label{ font-size:11px; font-weight:700; color:var(--terracotta); letter-spacing:0.06em; text-transform:uppercase; }
  .block-row-actions{ display:flex; gap:4px; }
  .block-row-actions button{
    background:none; border:1px solid var(--card-line); color:var(--text-muted); width:26px; height:26px;
    border-radius:6px; font-size:12px; cursor:pointer; line-height:1;
  }
  .block-row-actions button:hover:not(:disabled){ border-color:var(--terracotta); color:var(--terracotta); }
  .block-row-actions button:disabled{ opacity:.3; cursor:default; }
  .block-field-row{ display:flex; gap:8px; flex-wrap:wrap; }
  .block-field-row > *{ flex:1 1 160px; }
  .block-add-row{ display:flex; gap:8px; flex-wrap:wrap; margin-top:12px; }
  .block-add-row select{
    background:var(--input-bg); border:1px solid var(--card-line); border-radius:8px;
    padding:9px 10px; font-size:13px; color:var(--text);
  }
  .block-img-preview{ max-width:160px; border-radius:8px; border:1px solid var(--card-line); display:block; }

  /* ---------- コラム：静的HTML書き出し（SEO） ---------- */
  .seo-export-box{
    background:rgba(201,169,97,0.06); border:1px solid var(--card-line); border-radius:12px;
    padding:16px 18px; margin:14px 0 18px;
  }
  .seo-export-box-title{ font-family:'Shippori Mincho',serif; font-weight:700; font-size:14px; color:var(--text); margin-bottom:6px; }
  .seo-export-box code{ background:rgba(201,169,97,0.14); padding:1px 5px; border-radius:4px; font-size:11px; }
  .seo-export-box .btn-manager-add{ margin-top:12px; }
  .article-export-btn{
    background:none; border:1px solid var(--card-line); color:var(--text-muted); font-size:11px;
    padding:4px 10px; border-radius:999px; cursor:pointer; white-space:nowrap;
  }
  .article-export-btn:hover{ border-color:var(--terracotta); color:var(--terracotta); }

</style>
</head>
<body>


<header class="topbar">
  <div class="brand" onclick="go('home')">
    <svg class="brand-icon" width="30" height="30" viewBox="0 0 72 72" fill="none" aria-hidden="true">
      <path d="M46 14C35 14 26 22.9 26 34C26 45.1 35 54 46 54C40.8 49.7 37.5 42.3 37.5 34C37.5 25.7 40.8 18.3 46 14Z" fill="var(--terracotta)"/>
      <circle cx="54" cy="19" r="1.8" fill="var(--terracotta)"/>
      <circle cx="59" cy="29" r="1.1" fill="var(--terracotta-soft)"/>
    </svg>
    <div class="brand-text">
      <span class="mark">Night PASS</span>
      <span class="sub">TOKYO NIGHT LOUNGE GUIDE</span>
    </div>
  </div>
  <div class="nav-actions">
    <a class="btn-ghost" onclick="go('columns')">コラム</a>
    <a class="btn-ghost" onclick="go('admin')">店舗管理（アドミン）</a>
  </div>
</header>

<main id="view-home" class="active">
  <section class="hero">
    <span class="eyebrow">Night Entertainment Guide</span>
    <h1>今夜、心ときめく一軒が、<br class="brk"><span class="accent">ここで見つかる。</span></h1>
    <p class="lead">エリア・業態・ご予算から、行きたいお店を検索。写真と雰囲気を見てから、電話やLINEで気軽にご予約を。</p>

    <div class="search-panel">
      <div class="search-grid">
        <div class="field">
          <label>キーワード</label>
          <input id="f-keyword" type="text" placeholder="店名・エリア・こだわりで検索">
        </div>
        <div class="field">
          <label>都道府県</label>
          <select id="f-prefecture" onchange="handlePrefectureChangeInSearch()">
            <option value="">すべて</option>
          <option value="北海道">北海道</option>
          <option value="青森県">青森県</option>
          <option value="岩手県">岩手県</option>
          <option value="宮城県">宮城県</option>
          <option value="秋田県">秋田県</option>
          <option value="山形県">山形県</option>
          <option value="福島県">福島県</option>
          <option value="茨城県">茨城県</option>
          <option value="栃木県">栃木県</option>
          <option value="群馬県">群馬県</option>
          <option value="埼玉県">埼玉県</option>
          <option value="千葉県">千葉県</option>
          <option value="東京都">東京都</option>
          <option value="神奈川県">神奈川県</option>
          <option value="新潟県">新潟県</option>
          <option value="富山県">富山県</option>
          <option value="石川県">石川県</option>
          <option value="福井県">福井県</option>
          <option value="山梨県">山梨県</option>
          <option value="長野県">長野県</option>
          <option value="岐阜県">岐阜県</option>
          <option value="静岡県">静岡県</option>
          <option value="愛知県">愛知県</option>
          <option value="三重県">三重県</option>
          <option value="滋賀県">滋賀県</option>
          <option value="京都府">京都府</option>
          <option value="大阪府">大阪府</option>
          <option value="兵庫県">兵庫県</option>
          <option value="奈良県">奈良県</option>
          <option value="和歌山県">和歌山県</option>
          <option value="鳥取県">鳥取県</option>
          <option value="島根県">島根県</option>
          <option value="岡山県">岡山県</option>
          <option value="広島県">広島県</option>
          <option value="山口県">山口県</option>
          <option value="徳島県">徳島県</option>
          <option value="香川県">香川県</option>
          <option value="愛媛県">愛媛県</option>
          <option value="高知県">高知県</option>
          <option value="福岡県">福岡県</option>
          <option value="佐賀県">佐賀県</option>
          <option value="長崎県">長崎県</option>
          <option value="熊本県">熊本県</option>
          <option value="大分県">大分県</option>
          <option value="宮崎県">宮崎県</option>
          <option value="鹿児島県">鹿児島県</option>
          <option value="沖縄県">沖縄県</option>
          </select>
        </div>
        <div class="field">
          <label>エリア</label>
          <select id="f-area"><option value="">すべて</option></select>
        </div>
        <div class="field">
          <label>業態</label>
          <select id="f-genre"><option value="">すべて</option></select>
        </div>
        <div class="field" style="align-self:end;">
          <button class="btn-search" onclick="handleSearchClick()">検索する</button>
        </div>
      </div>
    </div>

    <div class="quick-filters">
      <div class="quick-block">
        <div class="quick-label">業態から探す</div>
        <div class="quick-icons" id="genre-icons"></div>
      </div>
      <div class="quick-block">
        <div class="quick-label">人気エリアから探す</div>
        <div class="quick-icons" id="area-icons"></div>
      </div>
    </div>
  </section>

  <div class="result-meta">
    <h2>掲載店舗 <span class="count" id="result-count">0</span> 件</h2>
    <div class="sort-inline">
      <button class="loc-btn" id="loc-btn" onclick="useMyLocation()">📍 現在地から探す</button>
      並び替え：
      <select id="f-sort" onchange="applyFilters()">
        <option value="new">新着順</option>
        <option value="budget-asc">セット料金が安い順</option>
        <option value="name">店名順</option>
        <option value="distance" id="distance-option" disabled>現在地から近い順</option>
      </select>
    </div>
  </div>

  <div class="grid" id="store-grid"></div>
</main>

<main id="view-detail">
  <div class="detail-wrap" id="detail-content"></div>
</main>

<main id="view-admin">
  <div class="admin-wrap" id="admin-content"></div>
</main>

<main id="view-terms">
  <div class="static-page" id="terms-content"></div>
</main>

<main id="view-company">
  <div class="static-page" id="company-content"></div>
</main>

<main id="view-columns">
  <div class="static-page columns-page" id="columns-content"></div>
</main>

<main id="view-article">
  <div class="detail-wrap" id="article-content"></div>
</main>

<footer>
  <div class="footer-links" id="footer-links"></div>
  Night PASS — 夜のお店紹介サイト（デモ） / 掲載内容はアドミン画面から編集できます
</footer>
<div class="toast" id="toast"></div>
<div class="lightbox" id="lightbox" onclick="closeLightbox()">
  <button type="button" class="lightbox-close" onclick="event.stopPropagation(); closeLightbox()">✕</button>
  <img id="lightbox-img" src="" alt="" onclick="event.stopPropagation()">
</div>

<script>
/* ---------------- storage layer ----------------
   Uses the Artifact "db" capability (claude.use('db')) when running as
   a published Claude Artifact with db granted — shared across every
   viewer, store-per-document so photo uploads don't blow one giant
   document's size limit. Falls back to the browser's localStorage
   when hosted standalone (e.g. GitHub Pages). See README.md. */
const dbPromise = (async () => {
  try{
    if(window.claude && typeof window.claude.use === 'function'){
      const db = await window.claude.use('db');
      if(db) return db;
    }
  }catch(e){ /* not available in this view */ }
  return null;
})();
async function getDb(){ return await dbPromise; }

async function loadConfigValue(key){
  const db = await getDb();
  if(db){
    try{
      const snap = await db.collection('site').doc(key).get();
      if(snap.exists){
        const data = snap.data();
        if(data && data.value !== undefined && data.value !== null) return data.value;
      }
    }catch(e){ /* fall through */ }
    return null;
  }
  try{
    const raw = localStorage.getItem('yorupass:' + key);
    if(raw) return JSON.parse(raw);
  }catch(e){}
  return null;
}
async function saveConfigValue(key, value){
  const db = await getDb();
  if(db){
    try{ await db.collection('site').doc(key).set({ value }); return true; }catch(e){ return false; }
  }
  try{ localStorage.setItem('yorupass:' + key, JSON.stringify(value)); return true; }catch(e){ return false; }
}

/* ---------------- data layer ---------------- */
const ADMIN_PASS = 'yorupass2026';

/* ---------------- admin user accounts ---------------- */
const DEFAULT_ADMIN_USERS = [{ id:'u-admin', username:'admin', password: ADMIN_PASS }];
let ADMIN_USERS = DEFAULT_ADMIN_USERS.slice();
let adminCurrentUser = '';

async function loadAdminUsers(){
  const v = await loadConfigValue('adminUsers');
  if(Array.isArray(v) && v.length){ ADMIN_USERS = v; return; }
  ADMIN_USERS = DEFAULT_ADMIN_USERS.slice();
  try{ await saveConfigValue('adminUsers', ADMIN_USERS); }catch(e){}
}
async function saveAdminUsers(){ return await saveConfigValue('adminUsers', ADMIN_USERS); }

const DEFAULT_STORES = [
  {
    id:'s1', name:'Club ROSALIE 銀座', area:'銀座', genre:'キャバクラ', prefecture:'東京都', platinum:true,
    catch:'落ち着いた大人の社交場。初めての方も安心のシステムでご案内。',
    wage:'¥15,000〜（60分・税サ込）', tags:['初回割引あり','個室あり','会員制','送り可'],
    photos:[], instagram:'https://www.instagram.com/', tiktok:'',
    phone:'03-1234-5678', email:'reserve@example.com', lineUrl:'https://lin.ee/example1',
    address:'東京都中央区銀座7-5-12 〇〇ビル5F', hours:'20:00〜翌1:00（L.O.翌0:30）', closedDay:'日曜日',
    description:'銀座の路地に佇む、落ち着いた大人のためのラウンジです。初めてのお客様にもスタッフが丁寧にご案内いたしますので、お一人でもお気軽にお立ち寄りください。接待やご会食のご利用、女性同伴のお客様も歓迎しております。',
    casts:[{name:'美咲',catch:'明るい笑顔でお迎えします♪ お酒の相談もどうぞ。'},{name:'麗奈',catch:'ワインとシャンパンには自信あり。聞き上手が特技です。'},{name:'彩乃',catch:'今月入店したばかりです。よろしくお願いします！'}]
  },
  {
    id:'s2', name:'Lounge AMOUR 六本木', area:'六本木', genre:'ラウンジ', prefecture:'東京都', platinum:true,
    catch:'International loungeで多国籍なゲストと乾杯を。',
    wage:'¥12,000〜（セット90分）', tags:['英語対応可','外国人スタッフ在籍','カジュアル利用OK'],
    photos:[], instagram:'https://www.instagram.com/', tiktok:'https://www.tiktok.com/',
    phone:'03-2345-6789', email:'info@example.com', lineUrl:'',
    address:'東京都港区六本木3-14-9 〇〇ビル3F', hours:'19:30〜翌2:00', closedDay:'月曜日',
    description:'六本木の交差点近くにあるインターナショナルラウンジ。英語対応可能なスタッフが多数在籍しており、海外からのお客様にもご好評をいただいています。カジュアルな雰囲気で、初めての夜遊びにもおすすめです。',
    casts:[{name:'Yuki',catch:'Speak English & Japanese! Let’s have a great night.'},{name:'ののか',catch:'ダーツと会話が得意です。気軽に声かけてください。'}]
  },
  {
    id:'s3', name:'CLUB NOIR 西麻布', area:'西麻布', genre:'クラブ', prefecture:'東京都', platinum:true,
    catch:'会員制の隠れ家クラブ。VIPルーム完備。',
    wage:'¥20,000〜（フリータイム）', tags:['VIPルームあり','会員制','シャンパンコールあり'],
    photos:[], instagram:'https://www.instagram.com/', tiktok:'',
    phone:'03-3456-7890', email:'noir@example.com', lineUrl:'https://lin.ee/example3',
    address:'東京都港区西麻布1-2-3 〇〇ビルB1', hours:'21:00〜翌4:00（二部制）', closedDay:'日曜・祝日',
    description:'西麻布の路地裏、看板を出さない完全会員制のクラブです。落ち着いたVIPルームを3室ご用意しており、記念日のシャンパンコールなど特別な一夜を演出いたします。ご紹介制中心のため、まずはお電話にてご相談ください。',
    casts:[{name:'凛',catch:'シャンパンタワーはお任せください。'},{name:'碧',catch:'落ち着いた会話がお好きな方にぴったりです。'}]
  },
  {
    id:'s4', name:'Girls Bar Sourire 歌舞伎町', area:'新宿・歌舞伎町', genre:'ガールズバー', prefecture:'東京都',
    catch:'気軽に立ち寄れるカジュアルガールズバー。',
    wage:'¥3,000〜（30分・チャージ込）', tags:['一人利用歓迎','女性一人でも安心','明朗会計'],
    photos:[], instagram:'https://www.instagram.com/', tiktok:'https://www.tiktok.com/',
    phone:'03-4567-8901', email:'sourire@example.com', lineUrl:'',
    address:'東京都新宿区歌舞伎町1-8-2 〇〇ビル4F', hours:'19:00〜翌3:00', closedDay:'不定休',
    description:'歌舞伎町の路面店でアクセス良好。明朗会計でお財布にやさしく、お一人でもふらっと立ち寄れるカジュアルなガールズバーです。女性のお客様、女子会でのご利用も大歓迎です。',
    casts:[{name:'ゆあ',catch:'カラオケが得意です！一緒に盛り上がりましょう。'},{name:'みお',catch:'お酒は弱いですが、お話するのは大好きです。'}]
  },
  {
    id:'s5', name:'スナック 月あかり', area:'赤坂', genre:'スナック', prefecture:'東京都', platinum:true,
    catch:'ママの手料理とカラオケが自慢の隠れ家スナック。',
    wage:'¥5,000〜（チャージ・お通し込）', tags:['カラオケあり','アットホーム','常連多数'],
    photos:[], instagram:'', tiktok:'',
    phone:'03-5678-9012', email:'tsukiakari@example.com', lineUrl:'',
    address:'東京都港区赤坂3-11-5 〇〇ビル2F', hours:'19:00〜翌1:00', closedDay:'日曜日',
    description:'赤坂の路地裏で20年続く、ママの手料理が自慢のアットホームなスナックです。カラオケの機材も充実しており、常連のお客様同士の会話も弾みます。一人でふらっと来られる方も多くいらっしゃいます。',
    casts:[{name:'ママ・薫',catch:'手料理と昔話が得意です。ゆっくりしていってね。'}]
  },
  {
    id:'s6', name:'コンカフェ Melty Star', area:'渋谷', genre:'コンカフェ', prefecture:'東京都',
    catch:'キラキラ制服が可愛いコンセプトカフェ。',
    wage:'¥2,500〜（1オーダー制）', tags:['写真撮影OK','学生歓迎','ノンアルコールあり'],
    photos:[], instagram:'https://www.instagram.com/', tiktok:'https://www.tiktok.com/',
    phone:'03-6789-0123', email:'meltystar@example.com', lineUrl:'',
    address:'東京都渋谷区宇田川町15-1 〇〇ビル6F', hours:'17:00〜23:00', closedDay:'水曜日',
    description:'渋谷センター街にあるキラキラ制服が人気のコンセプトカフェです。ノンアルコールメニューも充実しており、20歳未満の方や飲めない方にも安心してご利用いただけます。店内での写真撮影もOKです。',
    casts:[{name:'ふわり',catch:'一緒に写真撮ろうね！ノンアルカクテル作るの得意です。'},{name:'きらら',catch:'ゲームの話で盛り上がれます。'}]
  },
  {
    id:'s7', name:'ニュークラブ 花時-Hanadoki-', area:'恵比寿', genre:'ニュークラブ', prefecture:'東京都', platinum:true,
    catch:'上質な接待に応える老舗ニュークラブ。',
    wage:'¥18,000〜（60分）', tags:['接待利用に人気','個室あり','要予約'],
    photos:[], instagram:'https://www.instagram.com/', tiktok:'',
    phone:'03-7890-1234', email:'hanadoki@example.com', lineUrl:'https://lin.ee/example7',
    address:'東京都渋谷区恵比寿1-9-4 〇〇ビル7F', hours:'19:00〜翌0:30', closedDay:'日曜・祝日',
    description:'恵比寿で30年続く老舗のニュークラブです。落ち着いた内装の個室をご用意しており、大切な接待やご会食にご利用いただいております。マナーを心得たスタッフが、上質な時間をお約束いたします。',
    casts:[{name:'紗英',catch:'お客様のお話をじっくり伺うのが信条です。'},{name:'have not decided',catch:''}]
  },
  {
    id:'s8', name:'ダイニング&Bar NOCT', area:'新橋', genre:'ダイニングバー', prefecture:'東京都',
    catch:'食事もお酒も本格派。二次会にも人気。',
    wage:'¥4,000〜（飲み放題付き）', tags:['食事充実','飲み放題あり','二次会利用OK'],
    photos:[], instagram:'https://www.instagram.com/', tiktok:'',
    phone:'03-8901-2345', email:'noct@example.com', lineUrl:'',
    address:'東京都港区新橋2-15-6 〇〇ビル1F', hours:'17:00〜翌2:00', closedDay:'年中無休',
    description:'新橋駅から徒歩2分、食事メニューも充実したダイニングバーです。一次会はもちろん、飲み放題付きコースがお得な二次会利用としても人気。カジュアルな雰囲気で、女性キャストとの会話も楽しめます。',
    casts:[{name:'るい',catch:'お酒に合うおつまみ選び、お任せください。'},{name:'あんず',catch:'サッカーの話ができます！'}]
  }
];

let STORES = [];
let currentDetailId = null;
let currentArticleSlug = null;
let adminUnlocked = false;
let adminSelectedId = null;
let adminArticleSelectedId = null;
let adminListPage = 1;
let adminListPageSize = 10;
let adminSitePageTab = 'terms';
let adminMainTab = 'stores';
function switchAdminMainTab(tab){
  adminMainTab = tab;
  const storesPanel = document.getElementById('admin-tab-panel-stores');
  const columnsPanel = document.getElementById('admin-tab-panel-columns');
  const settingsPanel = document.getElementById('admin-tab-panel-settings');
  if(storesPanel) storesPanel.hidden = (tab !== 'stores');
  if(columnsPanel) columnsPanel.hidden = (tab !== 'columns');
  if(settingsPanel) settingsPanel.hidden = (tab !== 'settings');
  document.querySelectorAll('#admin-main-tabs .admin-tab-btn').forEach(btn=>{
    btn.classList.toggle('active', btn.dataset.tab === tab);
  });
}
function switchSitePageTab(tab){
  adminSitePageTab = tab;
  const termsPanel = document.getElementById('site-page-tab-terms');
  const companyPanel = document.getElementById('site-page-tab-company');
  if(termsPanel) termsPanel.hidden = (tab !== 'terms');
  if(companyPanel) companyPanel.hidden = (tab !== 'company');
  document.querySelectorAll('#site-page-tabs .admin-tab-btn').forEach(btn=>{
    btn.classList.toggle('active', btn.dataset.tab === tab);
  });
}

function normalizeDescriptionBlock(b){
  const type = ['text','image'].includes(b && b.type) ? b.type : 'text';
  return {
    type,
    text: String((b && b.text) || ''),
    src: String((b && b.src) || ''),
    alt: String((b && b.alt) || ''),
    caption: String((b && b.caption) || ''),
  };
}
function normalizeStore(s){
  const photos = Array.isArray(s.photos) ? s.photos.filter(Boolean).slice(0,4) : (s.photo ? [s.photo] : []);
  const casts = Array.isArray(s.casts) ? s.casts.filter(c=>c && c.name).slice(0,12).map(c=>({name:String(c.name), catch:String(c.catch||''), photo:String(c.photo||'')})) : [];
  // stores saved before the prefecture field existed default to 東京都 so
  // existing data keeps showing up under the search engine's 都道府県 filter.
  const prefecture = s.prefecture || '東京都';
  // stores saved before the 店舗紹介文 block editor existed only have a plain-text
  // `description` string. Migrate that into a single 本文 block so old data keeps
  // displaying correctly, while new stores use descriptionBlocks going forward.
  let descriptionBlocks = Array.isArray(s.descriptionBlocks) ? s.descriptionBlocks.map(normalizeDescriptionBlock) : [];
  if(descriptionBlocks.length === 0 && s.description){
    descriptionBlocks = [normalizeDescriptionBlock({ type:'text', text:s.description })];
  }
  return Object.assign({}, s, { photos, casts, prefecture, descriptionBlocks });
}

async function loadStores(){
  const db = await getDb();
  if(db){
    try{
      const snap = await db.collection('stores').get();
      if(!snap.empty){
        STORES = snap.docs.map(d => normalizeStore(d.data()));
        return;
      }
    }catch(e){ /* fall through to seeding */ }
    STORES = DEFAULT_STORES.map(normalizeStore);
    try{ await Promise.all(STORES.map(s => db.collection('stores').doc(s.id).set(s))); }catch(e){}
    return;
  }
  try{
    const raw = localStorage.getItem('yorupass:stores');
    if(raw){ STORES = JSON.parse(raw).map(normalizeStore); return; }
  }catch(e){ /* not found yet */ }
  STORES = DEFAULT_STORES.map(normalizeStore);
  try{ localStorage.setItem('yorupass:stores', JSON.stringify(STORES)); }catch(e){}
}

async function persistStore(store){
  const db = await getDb();
  if(db){
    try{ await db.collection('stores').doc(store.id).set(store); return true; }catch(e){ return false; }
  }
  try{ localStorage.setItem('yorupass:stores', JSON.stringify(STORES)); return true; }catch(e){ return false; }
}

async function removeStoreFromStorage(id){
  const db = await getDb();
  if(db){
    try{ await db.collection('stores').doc(id).delete(); return true; }catch(e){ return false; }
  }
  try{ localStorage.setItem('yorupass:stores', JSON.stringify(STORES)); return true; }catch(e){ return false; }
}

/* ---------------- utils ---------------- */
function esc(s){
  return (s||'').replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
}
function showToast(msg){
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  clearTimeout(showToast._h);
  showToast._h = setTimeout(()=> t.classList.remove('show'), 2200);
}
function mainPhoto(store){
  return (store.photos && store.photos[0]) || '';
}
function cardPhotoHtml(store){
  const src = mainPhoto(store);
  const initial = (store.name||'?').trim().charAt(0);
  const inner = src ? `<img src="${esc(src)}" alt="${esc(store.name)}">` : esc(initial);
  return `<div class="photo">${inner}<span class="badge">${esc(store.genre)}</span></div>`;
}

let currentGalleryPhotos = [];
function galleryHtml(store){
  const photos = Array.isArray(store.photos) ? store.photos.filter(Boolean) : [];
  currentGalleryPhotos = photos;
  const initial = (store.name||'?').trim().charAt(0);
  const mainInner = photos[0]
    ? `<img src="${esc(photos[0])}" alt="${esc(store.name)}" id="gallery-main-img" onclick="openLightboxByIndex(0)">`
    : `<span>${esc(initial)}</span>`;
  const subPhotos = photos.slice(1, 4); // サブ写真は最大3枚まで、メイン写真の下に横並びで表示
  const thumbs = subPhotos.length > 0
    ? `<div class="thumb-row">${subPhotos.map((p,i)=>`
        <button type="button" class="thumb" onclick="openLightboxByIndex(${i+1})">
          <img src="${esc(p)}" alt="${esc(store.name)} サブ写真${i+1}">
        </button>
      `).join('')}</div>`
    : '';
  return `<div class="detail-photo">${mainInner}</div>${thumbs}`;
}
function openLightboxByIndex(idx){
  openLightbox(currentGalleryPhotos[idx]);
}
function openLightbox(src){
  if(!src) return;
  const img = document.getElementById('lightbox-img');
  const lb = document.getElementById('lightbox');
  if(!img || !lb) return;
  img.src = src;
  lb.classList.add('show');
}
function closeLightbox(){
  const lb = document.getElementById('lightbox');
  if(lb) lb.classList.remove('show');
}
document.addEventListener('keydown', (e) => { if(e.key === 'Escape') closeLightbox(); });
function igIcon(){
  return `<svg viewBox="0 0 24 24" stroke-width="1.7"><rect x="3" y="3" width="18" height="18" rx="6"/><circle cx="12" cy="12" r="4.2"/><circle cx="17.2" cy="6.8" r="1.1" fill="currentColor" stroke="none"/></svg>`;
}
function ttIcon(){
  return `<svg viewBox="0 0 24 24" stroke-width="1.7"><path d="M14 3v10.8a3.6 3.6 0 1 1-3-3.55"/><path d="M14 3c.5 2.6 2.3 4.3 5 4.6"/></svg>`;
}

/* ---------------- quick filter icons ---------------- */
const GENRE_ICONS = {
  'キャバクラ': `<svg viewBox="0 0 24 24" stroke-width="1.6"><path d="M12 3c-2.2 1.6-3.5 3.4-3.5 5.3 0 2.4 1.8 3.9 3.5 3.9s3.5-1.5 3.5-3.9C15.5 6.4 14.2 4.6 12 3Z"/><path d="M12 12.2V19M8.5 21h7"/></svg>`,
  'ラウンジ': `<svg viewBox="0 0 24 24" stroke-width="1.6"><path d="M4 5h16l-8 9-8-9Z"/><path d="M12 14v7M8.5 21h7"/><circle cx="15" cy="6.3" r="0.9" fill="currentColor" stroke="none"/></svg>`,
  'クラブ': `<svg viewBox="0 0 24 24" stroke-width="1.6"><path d="M10 17.5a2.5 2.5 0 1 1-2-4.9M10 17.5V5.5l8-1.6v10.6"/><path d="M18 14.5a2.5 2.5 0 1 1-2-4.9"/></svg>`,
  'ガールズバー': `<svg viewBox="0 0 24 24" stroke-width="1.6"><path d="M12 20.3S3.8 15.4 3.8 9.6A4.4 4.4 0 0 1 12 7.2a4.4 4.4 0 0 1 8.2 2.4c0 5.8-8.2 10.7-8.2 10.7Z"/></svg>`,
  'スナック': `<svg viewBox="0 0 24 24" stroke-width="1.6"><rect x="9" y="3" width="6" height="11" rx="3"/><path d="M6 11a6 6 0 0 0 12 0M12 17v4M9 21h6"/></svg>`,
  'コンカフェ': `<svg viewBox="0 0 24 24" stroke-width="1.6"><path d="M6 4 8 10M18 4l-2 6"/><circle cx="12" cy="13.5" r="6.5"/><path d="M9.3 13.8c0 .7.5 1.1.9.5M14.7 13.8c0 .7-.5 1.1-.9.5"/></svg>`,
  'ニュークラブ': `<svg viewBox="0 0 24 24" stroke-width="1.6"><path d="M4 18h16l-1.4-8.5L14 13 12 6l-2 7-4.6-3.5L4 18Z"/><path d="M4 20.5h16"/></svg>`,
  'ダイニングバー': `<svg viewBox="0 0 24 24" stroke-width="1.6"><path d="M7 3v6a3 3 0 0 0 3 3v9M7 3c0 3 0 6 3 6M7 3c0 3 0 6-3 3"/><path d="M16 3c-1.8 0-3 2-3 5s1.2 5 3 5v8"/></svg>`,
  'その他': `<svg viewBox="0 0 24 24" stroke-width="1.6"><path d="M12 3v4M12 17v4M3 12h4M17 12h4M6 6l2.8 2.8M15.2 15.2 18 18M18 6l-2.8 2.8M8.8 15.2 6 18"/></svg>`
};
function genreIconFor(g){
  return GENRE_ICONS[g] || GENRE_ICONS['その他'];
}
function pinIcon(){
  return `<svg viewBox="0 0 24 24" stroke-width="1.6"><path d="M12 21s7-6.2 7-11.3A7 7 0 0 0 5 9.7C5 14.8 12 21 12 21Z"/><circle cx="12" cy="9.6" r="2.4"/></svg>`;
}
function lineIcon(){
  return `<svg viewBox="0 0 24 24" stroke-width="1.7" style="width:16px;height:16px;vertical-align:-3px;margin-right:5px;"><path d="M4 12c0-4.4 3.8-8 8.5-8S21 7.6 21 12s-3.8 8-8.5 8c-.9 0-1.8-.1-2.6-.4L6 21l1-3.8C5.2 15.8 4 14 4 12Z"/></svg>`;
}

/* ---------------- cast (在籍キャスト) ---------------- */
function castAvatarStyle(i){
  const palette = [
    'linear-gradient(135deg, var(--terracotta), var(--olive))',
    'linear-gradient(135deg, var(--olive), var(--terracotta-soft))',
    'linear-gradient(135deg, var(--terracotta-soft), var(--olive-soft))'
  ];
  return palette[i % palette.length];
}
function castsHtml(store){
  const casts = Array.isArray(store.casts) ? store.casts.filter(c=>c && c.name) : [];
  if(casts.length === 0){
    return `<div class="desc" style="color:var(--text-faint);">在籍キャストの情報は準備中です。</div>`;
  }
  return `<div class="cast-grid">${casts.map((c,i)=>`
    <div class="cast-card">
      ${c.photo
        ? `<div class="cast-avatar cast-avatar-photo"><img src="${esc(c.photo)}" alt="${esc(c.name)}"></div>`
        : `<div class="cast-avatar" style="background:${castAvatarStyle(i)}">${esc((c.name||'?').trim().charAt(0))}</div>`}
      <div class="cast-name">${esc(c.name)}</div>
      ${c.catch ? `<div class="cast-catch">${esc(c.catch)}</div>` : ''}
    </div>
  `).join('')}</div>`;
}

/* ---------------- prefectures (都道府県, fixed 47) ---------------- */
const PREFECTURES = ['北海道','青森県','岩手県','宮城県','秋田県','山形県','福島県','茨城県','栃木県','群馬県','埼玉県','千葉県','東京都','神奈川県','新潟県','富山県','石川県','福井県','山梨県','長野県','岐阜県','静岡県','愛知県','三重県','滋賀県','京都府','大阪府','兵庫県','奈良県','和歌山県','鳥取県','島根県','岡山県','広島県','山口県','徳島県','香川県','愛媛県','高知県','福岡県','佐賀県','長崎県','熊本県','大分県','宮崎県','鹿児島県','沖縄県'];
function prefectureOptionsHtml(selected){
  return PREFECTURES.map(p=>`<option value="${esc(p)}" ${p===selected?'selected':''}>${esc(p)}</option>`).join('');
}

/* ---------------- popular areas / tag presets (admin-managed) ----------------
   Areas are {name, prefecture} objects so search/admin can filter エリア by
   都道府県. normalizeAreaList() upgrades older data saved as plain strings
   (pre-都道府県 releases) by assuming 東京都, so existing sites keep working. */
const DEFAULT_AREAS = ['銀座','六本木','西麻布','新宿・歌舞伎町','赤坂','渋谷','恵比寿','新橋','池袋'].map(name=>({name, prefecture:'東京都'}));
let POPULAR_AREAS = DEFAULT_AREAS.slice();

const DEFAULT_NORMAL_AREAS = [];
let NORMAL_AREAS = DEFAULT_NORMAL_AREAS.slice();

const DEFAULT_GENRES = ['キャバクラ','ラウンジ','クラブ','ガールズバー','スナック','コンカフェ','ニュークラブ','ダイニングバー','その他'];
let GENRE_LIST = DEFAULT_GENRES.slice();

async function loadGenres(){
  const v = await loadConfigValue('genres');
  if(v && v.length){ GENRE_LIST = v; return; }
  GENRE_LIST = DEFAULT_GENRES.slice();
  try{ await saveConfigValue('genres', GENRE_LIST); }catch(e){}
}
async function saveGenres(){ return await saveConfigValue('genres', GENRE_LIST); }

const DEFAULT_TAG_PRESETS = ['初回割引あり','個室あり','会員制','送り可','カラオケあり','VIPルームあり','シャンパンコールあり','女性一人でも安心','明朗会計','アットホーム','常連多数','写真撮影OK','学生歓迎','ノンアルコールあり','接待利用に人気','要予約','食事充実','飲み放題あり','二次会利用OK','英語対応可','外国人スタッフ在籍','カジュアル利用OK'];
let TAG_PRESETS = DEFAULT_TAG_PRESETS.slice();

function normalizeAreaList(list){
  if(!Array.isArray(list)) return [];
  return list.map(item => typeof item === 'string' ? {name:item, prefecture:'東京都'} : {name:item.name, prefecture:item.prefecture||'東京都'});
}

async function loadAreas(){
  const v = await loadConfigValue('areas');
  if(v){ POPULAR_AREAS = normalizeAreaList(v); return; }
  POPULAR_AREAS = DEFAULT_AREAS.slice();
  try{ await saveConfigValue('areas', POPULAR_AREAS); }catch(e){}
}
async function saveAreas(){ return await saveConfigValue('areas', POPULAR_AREAS); }

async function loadNormalAreas(){
  const v = await loadConfigValue('normalAreas');
  if(v){ NORMAL_AREAS = normalizeAreaList(v); return; }
  NORMAL_AREAS = DEFAULT_NORMAL_AREAS.slice();
  try{ await saveConfigValue('normalAreas', NORMAL_AREAS); }catch(e){}
}
async function saveNormalAreas(){ return await saveConfigValue('normalAreas', NORMAL_AREAS); }

/* areas registry helpers (name-based lookups used across search/admin) */
function allAreas(){ return [...POPULAR_AREAS, ...NORMAL_AREAS]; }
function areaExists(name){ return allAreas().some(a=>a.name===name); }
function prefectureForAreaName(name){
  const found = allAreas().find(a=>a.name===name);
  return found ? found.prefecture : '';
}
function areaNamesForPrefecture(prefecture){
  let areas = allAreas();
  if(prefecture) areas = areas.filter(a=>a.prefecture===prefecture);
  return [...new Set(areas.map(a=>a.name))].sort((a,b)=>a.localeCompare(b,'ja'));
}

async function loadTagPresets(){
  const v = await loadConfigValue('tagPresets');
  if(v){ TAG_PRESETS = v; return; }
  TAG_PRESETS = DEFAULT_TAG_PRESETS.slice();
  try{ await saveConfigValue('tagPresets', TAG_PRESETS); }catch(e){}
}
async function saveTagPresets(){ return await saveConfigValue('tagPresets', TAG_PRESETS); }

/* ---------------- static pages: 利用規約 / 運営会社情報 ---------------- */
const DEFAULT_TERMS = { content:'', published:false };
let SITE_TERMS = Object.assign({}, DEFAULT_TERMS);

const DEFAULT_COMPANY = {
  name:'', representative:'', address:'', phone:'', email:'', founded:'', business:'', note:'', published:false
};
let SITE_COMPANY = Object.assign({}, DEFAULT_COMPANY);

async function loadTerms(){
  const v = await loadConfigValue('terms');
  if(v && typeof v === 'object'){ SITE_TERMS = Object.assign({}, DEFAULT_TERMS, v); return; }
  SITE_TERMS = Object.assign({}, DEFAULT_TERMS);
}
async function saveTerms(){ return await saveConfigValue('terms', SITE_TERMS); }

async function loadCompany(){
  const v = await loadConfigValue('company');
  if(v && typeof v === 'object'){ SITE_COMPANY = Object.assign({}, DEFAULT_COMPANY, v); return; }
  SITE_COMPANY = Object.assign({}, DEFAULT_COMPANY);
}
async function saveCompany(){ return await saveConfigValue('company', SITE_COMPANY); }

/* ---------------- SEO設定（サイトの公開URL / 静的書き出しの基準URL） ----------------
   記事ごとの静的HTML書き出し機能で canonical URL を組み立てるために使う、
   サイトの公開先ベースURL（例：https://ユーザー名.github.io/リポジトリ名/）。
   未設定でも動作するが、設定しておくと canonical タグが正しく発行される。 */
const DEFAULT_SEO = { baseUrl:'' };
let SITE_SEO = Object.assign({}, DEFAULT_SEO);
async function loadSeoSettings(){
  const v = await loadConfigValue('seo');
  if(v && typeof v === 'object'){ SITE_SEO = Object.assign({}, DEFAULT_SEO, v); return; }
  SITE_SEO = Object.assign({}, DEFAULT_SEO);
}
async function saveSeoSettings(){ return await saveConfigValue('seo', SITE_SEO); }
function normalizedSeoBaseUrl(){
  const raw = (SITE_SEO.baseUrl || '').trim();
  if(!raw) return '';
  return raw.endsWith('/') ? raw : raw + '/';
}

/* ---------------- コラム / ブログ・NEWS記事 (SEO article CMS) ---------------- */
let ARTICLES = [];

function slugify(str){
  return (str||'')
    .toString().trim().toLowerCase()
    .replace(/[^a-z0-9\-\s]/g, '')
    .replace(/\s+/g, '-')
    .replace(/-+/g, '-')
    .replace(/^-|-$/g, '');
}
function suggestArticleSlug(title, existingId){
  let base = slugify(title);
  if(!base) base = 'column-' + Date.now().toString(36);
  let candidate = base;
  let i = 2;
  while(ARTICLES.some(a => a.slug === candidate && a.id !== existingId)){
    candidate = `${base}-${i}`;
    i++;
  }
  return candidate;
}

function normalizeArticleBlock(b){
  const type = ['h2','h3','paragraph','image','link','button'].includes(b && b.type) ? b.type : 'paragraph';
  return {
    type,
    text: String((b && b.text) || ''),
    src: String((b && b.src) || ''),
    alt: String((b && b.alt) || ''),
    caption: String((b && b.caption) || ''),
    linkType: ['store','article','external'].includes(b && b.linkType) ? b.linkType : 'external',
    targetId: String((b && b.targetId) || ''),
    url: String((b && b.url) || ''),
  };
}
function normalizeArticle(a){
  return Object.assign({
    id:'', slug:'', title:'', seoTitle:'', seoDescription:'', excerpt:'',
    coverImage:'', status:'draft', publishAt:'', blocks:[], createdAt:'', updatedAt:''
  }, a, {
    blocks: Array.isArray(a.blocks) ? a.blocks.map(normalizeArticleBlock) : []
  });
}

async function loadArticles(){
  const db = await getDb();
  if(db){
    try{
      const snap = await db.collection('articles').get();
      ARTICLES = snap.docs.map(d => normalizeArticle(d.data()));
      return;
    }catch(e){ ARTICLES = []; return; }
  }
  try{
    const raw = localStorage.getItem('yorupass:articles');
    ARTICLES = raw ? JSON.parse(raw).map(normalizeArticle) : [];
  }catch(e){ ARTICLES = []; }
}
async function persistArticle(article){
  const db = await getDb();
  if(db){
    try{ await db.collection('articles').doc(article.id).set(article); return true; }catch(e){ return false; }
  }
  try{ localStorage.setItem('yorupass:articles', JSON.stringify(ARTICLES)); return true; }catch(e){ return false; }
}
async function removeArticleFromStorage(id){
  const db = await getDb();
  if(db){
    try{ await db.collection('articles').doc(id).delete(); return true; }catch(e){ return false; }
  }
  try{ localStorage.setItem('yorupass:articles', JSON.stringify(ARTICLES)); return true; }catch(e){ return false; }
}

/* an article is publicly visible once it is published, or once a scheduled
   article's publishAt time has passed (evaluated against the viewer's own
   clock — this is a static site with no server, so "scheduled publishing"
   simply means the article stays hidden from renderColumnsList/renderArticleDetail
   until a visitor loads the page at or after that time). */
function isArticleVisible(article){
  if(!article) return false;
  if(article.status === 'published') return true;
  if(article.status === 'scheduled' && article.publishAt){
    return new Date(article.publishAt).getTime() <= Date.now();
  }
  return false;
}
function getPublicArticles(){
  return ARTICLES.filter(isArticleVisible).sort((a,b) => (b.publishAt || b.updatedAt || '').localeCompare(a.publishAt || a.updatedAt || ''));
}
function findArticleBySlug(slug){
  return ARTICLES.find(a => a.slug === slug);
}
function articleStatusLabel(article){
  if(article.status === 'published') return '公開中';
  if(article.status === 'scheduled') return isArticleVisible(article) ? '公開中（予約）' : '予約投稿';
  return '下書き';
}
function articleStatusClass(article){
  if(article.status === 'published' || (article.status === 'scheduled' && isArticleVisible(article))) return 'on';
  if(article.status === 'scheduled') return 'scheduled';
  return 'off';
}

function renderQuickFilters(){
  const gWrap = document.getElementById('genre-icons');
  gWrap.innerHTML = GENRE_LIST.map(g => `
    <button type="button" class="quick-chip" data-genre="${esc(g)}" onclick="toggleGenreFilter('${esc(g)}')">
      <span class="circle">${genreIconFor(g)}</span>
      <span class="label">${esc(g)}</span>
    </button>
  `).join('');

  const aWrap = document.getElementById('area-icons');
  aWrap.innerHTML = POPULAR_AREAS.map(a => `
    <button type="button" class="quick-chip area-box-chip" data-area="${esc(a.name)}" onclick="toggleAreaFilter('${esc(a.name)}')">
      <span class="area-box">${esc(a.name)}</span>
    </button>
  `).join('');
}

function toggleGenreFilter(g){
  const sel = document.getElementById('f-genre');
  sel.value = (sel.value === g) ? '' : g;
  applyFilters();
}
function toggleAreaFilter(a){
  const sel = document.getElementById('f-area');
  const turningOn = sel.value !== a;
  if(turningOn){
    // a popular-area quick chip may belong to a different prefecture than
    // whatever is currently selected in #f-prefecture, so reset the
    // prefecture filter and rebuild #f-area's full option list first.
    const prefSel = document.getElementById('f-prefecture');
    if(prefSel) prefSel.value = '';
    rebuildAreaSelectOptions('');
    sel.value = a;
  } else {
    sel.value = '';
  }
  applyFilters();
}
function syncQuickChips(){
  const genreVal = document.getElementById('f-genre').value;
  const areaVal = document.getElementById('f-area').value;
  document.querySelectorAll('#genre-icons .quick-chip').forEach(el=>{
    el.classList.toggle('active', el.dataset.genre === genreVal && genreVal !== '');
  });
  document.querySelectorAll('#area-icons .quick-chip').forEach(el=>{
    el.classList.toggle('active', el.dataset.area === areaVal && areaVal !== '');
  });
}

/* ---------------- nearby / geolocation ---------------- */
const AREA_COORDS = {
  '銀座':{lat:35.6717,lng:139.7650},
  '六本木':{lat:35.6627,lng:139.7307},
  '渋谷':{lat:35.6595,lng:139.7005},
  '新宿':{lat:35.6905,lng:139.7005},
  '新宿・歌舞伎町':{lat:35.6938,lng:139.7034},
  '恵比寿':{lat:35.6467,lng:139.7100},
  '代官山':{lat:35.6488,lng:139.6994},
  '中目黒':{lat:35.6446,lng:139.6989},
  '浅草':{lat:35.7118,lng:139.7966},
  '池袋':{lat:35.7295,lng:139.7109},
  '西麻布':{lat:35.6564,lng:139.7239},
  '新橋':{lat:35.6665,lng:139.7583},
  '赤坂':{lat:35.6737,lng:139.7368},
  '上野':{lat:35.7141,lng:139.7774},
  '五反田':{lat:35.6262,lng:139.7238}
};
const DEFAULT_COORDS = {lat:35.6812,lng:139.7671}; // 東京駅を仮の中心地とする
let userLocation = null;

function coordsForStore(s){
  if(typeof s.lat === 'number' && typeof s.lng === 'number' && !isNaN(s.lat) && !isNaN(s.lng)){
    return {lat:s.lat, lng:s.lng};
  }
  if(s.area && AREA_COORDS[s.area]) return AREA_COORDS[s.area];
  const key = s.area ? Object.keys(AREA_COORDS).find(k => s.area.includes(k) || k.includes(s.area)) : null;
  if(key) return AREA_COORDS[key];
  return DEFAULT_COORDS;
}
function haversineKm(lat1,lng1,lat2,lng2){
  const R = 6371;
  const dLat = (lat2-lat1) * Math.PI/180;
  const dLng = (lng2-lng1) * Math.PI/180;
  const a = Math.sin(dLat/2)**2 + Math.cos(lat1*Math.PI/180)*Math.cos(lat2*Math.PI/180)*Math.sin(dLng/2)**2;
  return R * 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a));
}
function distanceForStore(s){
  if(!userLocation) return null;
  const c = coordsForStore(s);
  return haversineKm(userLocation.lat, userLocation.lng, c.lat, c.lng);
}
function useMyLocation(){
  const btn = document.getElementById('loc-btn');
  if(!navigator.geolocation){ showToast('お使いのブラウザは位置情報に対応していません'); return; }
  btn.textContent = '📍 取得中...';
  navigator.geolocation.getCurrentPosition(
    pos => {
      userLocation = {lat:pos.coords.latitude, lng:pos.coords.longitude};
      btn.textContent = '📍 現在地から検索中';
      btn.classList.add('active');
      document.getElementById('distance-option').disabled = false;
      document.getElementById('f-sort').value = 'distance';
      applyFilters();
      showToast('現在地から近い順に表示しています');
    },
    () => {
      btn.textContent = '📍 現在地から探す';
      showToast('現在地を取得できませんでした。位置情報の利用を許可してください。');
    },
    {timeout:10000}
  );
}

/* ---------------- navigation ---------------- */
function go(view){
  document.querySelectorAll('main').forEach(m => m.classList.remove('active'));
  document.getElementById('view-'+view).classList.add('active');
  window.scrollTo({top:0, behavior:'smooth'});
  if(view === 'admin') renderAdmin();
  if(view === 'terms') renderTermsPage();
  if(view === 'company') renderCompanyPage();
  if(view === 'columns') renderColumnsList();
  if(view !== 'article'){
    resetArticleSeo();
    if(location.hash.indexOf('#/column/') === 0){
      history.replaceState(null, '', location.pathname + location.search);
    }
  }
}

/* ---------------- コラム記事の個別URL（ハッシュルーティング） ----------------
   静的な単一HTMLサイトのためサーバー側ルーティングは持たないが、記事ごとに
   #/column/<slug> という固有URLを発行し、直接アクセス・再読み込み・共有時に
   その記事へ自動的に遷移できるようにする。あわせてタイトル・meta descriptionを
   記事のSEO設定に合わせて書き換える。 */
const DEFAULT_DOCUMENT_TITLE = document.title;
let DEFAULT_META_DESCRIPTION = '';
function applyArticleSeo(article){
  const metaEl = document.getElementById('meta-description');
  if(metaEl && !DEFAULT_META_DESCRIPTION) DEFAULT_META_DESCRIPTION = metaEl.getAttribute('content') || '';
  document.title = (article.seoTitle || article.title || 'コラム') + ' | Night PASS';
  if(metaEl) metaEl.setAttribute('content', article.seoDescription || article.excerpt || DEFAULT_META_DESCRIPTION);
  // 静的書き出し（column/<slug>.html）が本来のクロール対象URLなので、
  // ベースURLが設定されていれば canonical タグでそちらを指し示す（WordPress的な正規化）。
  const canonicalEl = document.getElementById('article-canonical');
  const baseUrl = normalizedSeoBaseUrl();
  if(canonicalEl){
    if(baseUrl) canonicalEl.setAttribute('href', baseUrl + 'column/' + encodeURIComponent(article.slug) + '.html');
    else canonicalEl.removeAttribute('href');
  }
}
function resetArticleSeo(){
  document.title = DEFAULT_DOCUMENT_TITLE;
  const metaEl = document.getElementById('meta-description');
  if(metaEl && DEFAULT_META_DESCRIPTION) metaEl.setAttribute('content', DEFAULT_META_DESCRIPTION);
  const canonicalEl = document.getElementById('article-canonical');
  if(canonicalEl) canonicalEl.removeAttribute('href');
}
function openArticle(slug){
  const article = findArticleBySlug(slug);
  if(!article || (!isArticleVisible(article) && !adminUnlocked)){
    currentArticleSlug = slug;
    go('article');
    renderArticleDetail();
    return;
  }
  currentArticleSlug = slug;
  go('article');
  renderArticleDetail();
  applyArticleSeo(article);
  if(location.hash !== '#/column/' + encodeURIComponent(slug)){
    history.pushState(null, '', '#/column/' + encodeURIComponent(slug));
  }
}
function handleHashRoute(){
  const m = /^#\/column\/(.+)$/.exec(location.hash);
  if(m){
    const slug = decodeURIComponent(m[1]);
    if(slug !== currentArticleSlug || !document.getElementById('view-article').classList.contains('active')){
      openArticle(slug);
    }
  }
}
window.addEventListener('hashchange', handleHashRoute);
window.addEventListener('popstate', handleHashRoute);

/* ---------------- static pages: 利用規約 / 運営会社情報 ---------------- */
function renderFooterLinks(){
  const wrap = document.getElementById('footer-links');
  if(!wrap) return;
  const links = [];
  if(SITE_TERMS.published) links.push(`<a onclick="go('terms')">利用規約</a>`);
  if(SITE_COMPANY.published) links.push(`<a onclick="go('company')">運営会社情報</a>`);
  wrap.innerHTML = links.join('');
}

function renderTermsPage(){
  const el = document.getElementById('terms-content');
  if(!el) return;
  const body = SITE_TERMS.content
    ? `<div class="desc">${esc(SITE_TERMS.content)}</div>`
    : `<div class="empty-note">利用規約は準備中です。</div>`;
  el.innerHTML = `
    <a class="back" onclick="go('home')">← トップに戻る</a>
    <h1 style="margin-top:18px;">利用規約</h1>
    ${body}
  `;
}

function renderCompanyPage(){
  const el = document.getElementById('company-content');
  if(!el) return;
  const c = SITE_COMPANY;
  const rows = [
    ['会社名', c.name],
    ['代表者', c.representative],
    ['所在地', c.address],
    ['電話番号', c.phone],
    ['メールアドレス', c.email],
    ['設立', c.founded],
    ['事業内容', c.business],
    ['備考', c.note],
  ].filter(([,v]) => v);
  const body = rows.length
    ? `<div class="company-table">${rows.map(([k,v]) => `<div class="info-row"><div class="ik">${esc(k)}</div><div class="iv">${esc(v)}</div></div>`).join('')}</div>`
    : `<div class="empty-note">運営会社情報は準備中です。</div>`;
  el.innerHTML = `
    <a class="back" onclick="go('home')">← トップに戻る</a>
    <h1 style="margin-top:18px;">運営会社情報</h1>
    ${body}
  `;
}

/* ---------------- home / search ---------------- */
/* rebuilds #f-area's option list from the registered areas (areaNamesForPrefecture),
   optionally scoped to a chosen 都道府県 (e.g. 宮城県 → only its registered
   municipalities). Preserves the current selection when it is still valid. */
function rebuildAreaSelectOptions(prefecture){
  const areaSel = document.getElementById('f-area');
  if(!areaSel) return;
  const prevVal = areaSel.value;
  const areas = areaNamesForPrefecture(prefecture);
  areaSel.innerHTML = '<option value="">すべて</option>' + areas.map(a=>`<option value="${esc(a)}">${esc(a)}</option>`).join('');
  areaSel.value = areas.includes(prevVal) ? prevVal : '';
}

function handlePrefectureChangeInSearch(){
  const prefSel = document.getElementById('f-prefecture');
  const areaSel = document.getElementById('f-area');
  if(areaSel) areaSel.value = '';
  rebuildAreaSelectOptions(prefSel ? prefSel.value : '');
}

function populateFilterOptions(){
  const genres = [...new Set(STORES.map(s=>s.genre))].sort();
  const genreSel = document.getElementById('f-genre');
  genreSel.innerHTML = '<option value="">すべて</option>' + genres.map(g=>`<option value="${esc(g)}">${esc(g)}</option>`).join('');
  const prefSel = document.getElementById('f-prefecture');
  rebuildAreaSelectOptions(prefSel ? prefSel.value : '');
}

function wageNumber(store){
  const m = (store.wage||'').match(/[\d,]+/);
  return m ? parseInt(m[0].replace(/,/g,''),10) : 0;
}

function handleSearchClick(){
  applyFilters();
  const resultSection = document.querySelector('.result-meta');
  if(resultSection) resultSection.scrollIntoView({ behavior: 'smooth', block: 'start' });
}

let showAllStores = false;

function showAllStoresHandler(){
  showAllStores = true;
  applyFilters();
}

function applyFilters(){
  const kw = document.getElementById('f-keyword').value.trim().toLowerCase();
  const prefectureSel = document.getElementById('f-prefecture');
  const prefecture = prefectureSel ? prefectureSel.value : '';
  const area = document.getElementById('f-area').value;
  const genre = document.getElementById('f-genre').value;
  const sort = document.getElementById('f-sort').value;
  const isSearching = !!(kw || prefecture || area || genre);

  let list = STORES.filter(s=>{
    if(prefecture && s.prefecture !== prefecture) return false;
    if(area && s.area !== area) return false;
    if(genre && s.genre !== genre) return false;
    if(kw){
      const hay = [s.name, s.area, s.prefecture, s.genre, s.catch, (s.tags||[]).join(' ')].join(' ').toLowerCase();
      if(!hay.includes(kw)) return false;
    }
    return true;
  });

  if(sort === 'budget-asc') list = list.slice().sort((a,b)=> wageNumber(a)-wageNumber(b));
  else if(sort === 'name') list = list.slice().sort((a,b)=> a.name.localeCompare(b.name,'ja'));
  else if(sort === 'distance' && userLocation) list = list.slice().sort((a,b)=> distanceForStore(a) - distanceForStore(b));

  syncQuickChips();

  let displayList = list;
  let showMoreButton = false;
  if(!isSearching && !showAllStores){
    displayList = list.filter(s=>s.platinum).slice(0,10);
    showMoreButton = displayList.length < list.length;
  }

  renderGrid(displayList, sort === 'distance' && !!userLocation, showMoreButton);
}

function renderGrid(list, showDistance, showMoreButton){
  const grid = document.getElementById('store-grid');
  document.getElementById('result-count').textContent = list.length;
  if(list.length === 0 && !showMoreButton){
    grid.innerHTML = `<div class="empty"><span class="serif">該当するお店が見つかりませんでした</span>キーワードやエリアを変えて、もう一度検索してみてください。</div>`;
    return;
  }
  const cardsHtml = list.length ? list.map(s => `
    <div class="card" onclick="openDetail('${s.id}')">
      ${cardPhotoHtml(s)}
      <div class="body">
        <div class="name">${esc(s.name)}</div>
        <div class="loc">${esc(s.area)} ・ ${esc(s.genre)}</div>
        <div class="catch">${esc(s.catch)}</div>
        <div class="tags">${(s.tags||[]).slice(0,3).map(t=>`<span class="tag">${esc(t)}</span>`).join('')}</div>
        <div class="foot"><span class="budget">セット ${esc(s.wage)}</span></div>
        ${showDistance ? `<div class="dist-badge">📍現在地から約${distanceForStore(s).toFixed(1)}km</div>` : ''}
      </div>
    </div>
  `).join('') : `<div class="empty" style="grid-column:1/-1;"><span class="serif">プラチナプラン契約店が登録されていません</span>下のボタンから全ての店舗をご覧いただけます。</div>`;

  grid.innerHTML = cardsHtml + (showMoreButton ? `
    <div class="show-all-wrap">
      <button type="button" class="btn-show-all" onclick="showAllStoresHandler()">全ての店舗情報を見る</button>
    </div>
  ` : '');
}

/* ---------------- detail ---------------- */
function mapUrl(s){
  const q = s.address ? s.address : `${s.name} ${s.area}`;
  return `https://www.google.com/maps/search/?api=1&query=${encodeURIComponent(q)}`;
}
function renderStoreDescriptionHtml(s){
  const blocks = s.descriptionBlocks || [];
  const html = blocks.map(b => {
    if(b.type === 'text') return b.text ? `<p>${esc(b.text)}</p>` : '';
    if(b.type === 'image'){
      if(!b.src) return '';
      return `<img class="desc-img" src="${esc(b.src)}" alt="${esc(b.alt)}">` + (b.caption ? `<div class="desc-img-caption">${esc(b.caption)}</div>` : '');
    }
    return '';
  }).join('');
  return `<div class="store-desc-body">${html || '<p>この店舗の詳細情報は準備中です。</p>'}</div>`;
}

function openDetail(id){
  currentDetailId = id;
  const s = STORES.find(x=>x.id===id);
  if(!s) return;
  const el = document.getElementById('detail-content');
  const hasIg = !!s.instagram, hasTt = !!s.tiktok;
  const hasPhone = !!s.phone, hasMail = !!s.email, hasLine = !!s.lineUrl;
  el.innerHTML = `
    <a class="back" onclick="go('home')">← 検索結果に戻る</a>
    ${galleryHtml(s)}
    <div class="detail-head">
      <div>
        <span class="eyebrow">${esc(s.genre)} ・ ${esc(s.area)}</span>
        <h1>${esc(s.name)}</h1>
        <div class="loc">${esc(s.catch)}</div>
      </div>
      <div class="sns-row">
        <a class="sns-btn ${hasIg?'':'disabled'}" href="${hasIg? esc(s.instagram) : '#'}" target="_blank" rel="noopener" title="Instagram">${igIcon()}</a>
        <a class="sns-btn ${hasTt?'':'disabled'}" href="${hasTt? esc(s.tiktok) : '#'}" target="_blank" rel="noopener" title="TikTok">${ttIcon()}</a>
      </div>
    </div>

    <div class="section-title" style="margin-top:22px;">在籍キャスト</div>
    ${castsHtml(s)}

    <div class="detail-stats">
      <div class="stat-chip"><div class="k">セット料金目安</div><div class="v">${esc(s.wage)}</div></div>
      <div class="stat-chip"><div class="k">エリア</div><div class="v">${esc(s.area)}</div></div>
      <div class="stat-chip"><div class="k">業態</div><div class="v">${esc(s.genre)}</div></div>
    </div>
    <div class="detail-tags">${(s.tags||[]).map(t=>`<span class="tag">${esc(t)}</span>`).join('')}</div>

    <div class="section-title">店舗情報</div>
    <div class="info-grid">
      <div class="info-row"><div class="ik">住所</div><div class="iv">${s.address? esc(s.address) : '準備中'} ${s.address? `<a class="map-link" href="${mapUrl(s)}" target="_blank" rel="noopener">地図で見る →</a>`:''}</div></div>
      <div class="info-row"><div class="ik">営業時間</div><div class="iv">${s.hours? esc(s.hours) : '準備中'}</div></div>
      <div class="info-row"><div class="ik">定休日</div><div class="iv">${s.closedDay? esc(s.closedDay) : '準備中'}</div></div>
    </div>

    <div class="section-title">お店について</div>
    ${renderStoreDescriptionHtml(s)}

    <div class="apply-bar">
      <div class="apply-buttons">
        <a class="btn-apply" href="${hasPhone? 'tel:'+esc(s.phone) : (hasMail? 'mailto:'+esc(s.email) : '#')}">${hasPhone? '電話でご予約・お問い合わせ' : 'この店舗に問い合わせる'}</a>
        ${hasLine ? `<a class="btn-line" href="${esc(s.lineUrl)}" target="_blank" rel="noopener">${lineIcon()}LINEで来店相談</a>` : ''}
      </div>
      <span class="info">${hasMail? 'メールでのお問い合わせ：'+esc(s.email) : (hasPhone? '':'お問い合わせ先は準備中です')}</span>
    </div>
  `;
  go('detail');
}

/* ---------------- コラム / ブログ（公開画面） ---------------- */
function articleDateLabel(article){
  const iso = article.publishAt || article.updatedAt || article.createdAt || '';
  if(!iso) return '';
  const d = new Date(iso);
  if(isNaN(d.getTime())) return '';
  return `${d.getFullYear()}.${String(d.getMonth()+1).padStart(2,'0')}.${String(d.getDate()).padStart(2,'0')}`;
}
function resolveArticleBlockLink(block){
  if(block.linkType === 'store'){
    const store = STORES.find(s=>s.id===block.targetId);
    if(!store) return null;
    return { href:'#', attrs:`onclick="event.preventDefault(); openDetail('${esc(store.id)}')"` };
  }
  if(block.linkType === 'article'){
    const target = ARTICLES.find(a=>a.id===block.targetId);
    if(!target) return null;
    return { href:'#', attrs:`onclick="event.preventDefault(); openArticle('${esc(target.slug)}')"` };
  }
  if(block.url){
    return { href: esc(block.url), attrs:'target="_blank" rel="noopener"' };
  }
  return null;
}
function renderArticleBlocksHtml(blocks){
  return (blocks||[]).map(b => {
    if(b.type === 'h2') return b.text ? `<h2>${esc(b.text)}</h2>` : '';
    if(b.type === 'h3') return b.text ? `<h3>${esc(b.text)}</h3>` : '';
    if(b.type === 'paragraph') return b.text ? `<p>${esc(b.text)}</p>` : '';
    if(b.type === 'image'){
      if(!b.src) return '';
      return `<img class="article-img" src="${esc(b.src)}" alt="${esc(b.alt)}">` + (b.caption ? `<div class="img-caption">${esc(b.caption)}</div>` : '');
    }
    if(b.type === 'link'){
      const link = resolveArticleBlockLink(b);
      if(!link || !b.text) return '';
      return `<div class="article-link"><a href="${link.href}" ${link.attrs}>${esc(b.text)}</a></div>`;
    }
    if(b.type === 'button'){
      const link = resolveArticleBlockLink(b);
      if(!link || !b.text) return '';
      return `<div class="article-btn-wrap"><a class="article-btn" href="${link.href}" ${link.attrs}>${esc(b.text)}</a></div>`;
    }
    return '';
  }).join('');
}
function renderColumnsList(){
  const el = document.getElementById('columns-content');
  if(!el) return;
  const list = getPublicArticles();
  const cards = list.map(a => `
    <div class="column-card" onclick="openArticle('${esc(a.slug)}')">
      <div class="photo">${a.coverImage ? `<img src="${esc(a.coverImage)}" alt="${esc(a.title)}">` : esc((a.title||'?').trim().charAt(0))}</div>
      <div class="body">
        <div class="name">${esc(a.title)}</div>
        <div class="excerpt">${esc(a.excerpt)}</div>
        <div class="column-meta">${esc(articleDateLabel(a))}</div>
      </div>
    </div>
  `).join('');
  el.innerHTML = `
    <a class="back" onclick="go('home')">← トップに戻る</a>
    <h1 style="margin-top:18px;">コラム</h1>
    ${list.length ? `<div class="column-grid">${cards}</div>` : `<div class="empty-note">公開中の記事はまだありません。</div>`}
  `;
}
function renderArticleDetail(){
  const el = document.getElementById('article-content');
  if(!el) return;
  const article = findArticleBySlug(currentArticleSlug);
  if(!article || (!isArticleVisible(article) && !adminUnlocked)){
    el.innerHTML = `
      <a class="back" onclick="go('columns')">← コラム一覧に戻る</a>
      <div class="article-not-found"><span class="serif" style="display:block;font-size:18px;color:var(--text-muted);margin-bottom:8px;">記事が見つかりませんでした</span>URLをご確認いただくか、コラム一覧からお探しください。</div>
    `;
    return;
  }
  const previewNotice = (!isArticleVisible(article) && adminUnlocked)
    ? `<div class="publish-badge ${articleStatusClass(article)}" style="margin-bottom:14px;">プレビュー中（${esc(articleStatusLabel(article))}・まだ一般には公開されていません）</div>`
    : '';
  el.innerHTML = `
    <a class="back" onclick="go('columns')">← コラム一覧に戻る</a>
    ${previewNotice}
    <span class="eyebrow">Night PASS Column</span>
    <h1 style="font-family:'Shippori Mincho',serif;font-weight:800;font-size:clamp(24px,3.4vw,32px);margin:10px 0 4px;text-wrap:balance;">${esc(article.title)}</h1>
    <div class="article-date">${esc(articleDateLabel(article))}</div>
    ${article.coverImage ? `<div class="article-cover" style="margin-top:18px;"><img src="${esc(article.coverImage)}" alt="${esc(article.title)}"></div>` : ''}
    <div class="article-body">${renderArticleBlocksHtml(article.blocks)}</div>
  `;
}

/* ---------------- コラム記事の静的HTML書き出し（本物のクロール可能URL） ----------------
   このサイトはサーバーを持たない1ファイル構成のため、#/column/<slug> という
   ハッシュURLだけでは検索エンジンが記事を正しくインデックスできない場合がある。
   そこで、記事ごとに実際に独立したHTMLファイル（例：column/ginza-guide.html）を
   その場で生成してダウンロードできるようにし、GitHub Pages上の index.html と
   同じ階層に作った「column」フォルダへアップロードすることで、WordPressのような
   本物のクロール可能URLを発行できるようにする。
   タイトル・本文・メタ情報が最初から書き出されたHTMLの中に含まれているため、
   ハッシュルーティングのSPA表示よりも検索エンジンに正確に認識されやすい。 */
function resolveArticleBlockLinkForStaticExport(block){
  if(block.linkType === 'store'){
    const store = STORES.find(s=>s.id===block.targetId);
    if(!store) return null;
    return { href: '../index.html#/detail/' + encodeURIComponent(store.id), attrs:'' };
  }
  if(block.linkType === 'article'){
    const target = ARTICLES.find(a=>a.id===block.targetId);
    if(!target) return null;
    // 同じ column フォルダに書き出されている前提の相対リンク。
    // まだ書き出していない記事の場合は、SPA側のハッシュURLにフォールバックする。
    return { href: encodeURIComponent(target.slug) + '.html', attrs:'', fallbackHref: '../index.html#/column/' + encodeURIComponent(target.slug) };
  }
  if(block.url){
    return { href: esc(block.url), attrs:'target="_blank" rel="noopener"' };
  }
  return null;
}
function renderArticleBlocksHtmlForStaticExport(blocks){
  return (blocks||[]).map(b => {
    if(b.type === 'h2') return b.text ? `<h2>${esc(b.text)}</h2>` : '';
    if(b.type === 'h3') return b.text ? `<h3>${esc(b.text)}</h3>` : '';
    if(b.type === 'paragraph') return b.text ? `<p>${esc(b.text)}</p>` : '';
    if(b.type === 'image'){
      if(!b.src) return '';
      return `<img class="article-img" src="${esc(b.src)}" alt="${esc(b.alt)}">` + (b.caption ? `<div class="img-caption">${esc(b.caption)}</div>` : '');
    }
    if(b.type === 'link'){
      const link = resolveArticleBlockLinkForStaticExport(b);
      if(!link || !b.text) return '';
      return `<div class="article-link"><a href="${link.href}" ${link.attrs}>${esc(b.text)}</a></div>`;
    }
    if(b.type === 'button'){
      const link = resolveArticleBlockLinkForStaticExport(b);
      if(!link || !b.text) return '';
      return `<div class="article-btn-wrap"><a class="article-btn" href="${link.href}" ${link.attrs}>${esc(b.text)}</a></div>`;
    }
    return '';
  }).join('');
}
/* 静的書き出しページのヘッダーでも、サイト本体と同じ三日月アイコンのロゴを表示する */
const BRAND_ICON_SVG = `<svg class="brand-icon" width="30" height="30" viewBox="0 0 72 72" fill="none" aria-hidden="true">
      <path d="M46 14C35 14 26 22.9 26 34C26 45.1 35 54 46 54C40.8 49.7 37.5 42.3 37.5 34C37.5 25.7 40.8 18.3 46 14Z" fill="var(--terracotta)"/>
      <circle cx="54" cy="19" r="1.8" fill="var(--terracotta)"/>
      <circle cx="59" cy="29" r="1.1" fill="var(--terracotta-soft)"/>
    </svg>`;
function buildArticleStaticHtml(article){
  const styleEl = document.querySelector('style');
  const styleTag = styleEl ? `<style>${styleEl.textContent}</style>` : '';
  const baseUrl = normalizedSeoBaseUrl();
  const pageTitle = (article.seoTitle || article.title || 'コラム') + ' | Night PASS';
  const pageDesc = article.seoDescription || article.excerpt || '';
  const canonicalUrl = baseUrl ? baseUrl + 'column/' + encodeURIComponent(article.slug) + '.html' : '';
  const isPublished = article.status === 'published';
  const robotsTag = isPublished ? '' : `\n<meta name="robots" content="noindex,follow">`;
  const dateLabel = articleDateLabel(article);
  return `<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>${esc(pageTitle)}</title>
${pageDesc ? `<meta name="description" content="${esc(pageDesc)}">` : ''}${canonicalUrl ? `\n<link rel="canonical" href="${esc(canonicalUrl)}">` : ''}${robotsTag}
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Shippori+Mincho:wght@500;700;800&family=Zen+Kaku+Gothic+New:wght@400;500;700;900&family=Cormorant+Garamond:ital,wght@0,500;1,500&display=swap" rel="stylesheet">
${styleTag}
</head>
<body>
<header class="topbar">
  <a class="brand" href="../index.html" style="text-decoration:none;">
    ${BRAND_ICON_SVG}
    <div class="brand-text">
      <span class="mark">Night PASS</span>
      <span class="sub">TOKYO NIGHT LOUNGE GUIDE</span>
    </div>
  </a>
  <div class="nav-actions"><a class="btn-ghost" href="./index.html">コラム一覧</a><a class="btn-ghost" href="../index.html">トップへ戻る</a></div>
</header>
<main class="active">
  <div class="detail-wrap">
    ${!isPublished ? `<div class="publish-badge ${articleStatusClass(article)}" style="margin-bottom:14px;">この書き出しは「${esc(articleStatusLabel(article))}」状態の記事です（検索エンジンにはインデックスされない設定で書き出されています）</div>` : ''}
    <a class="back" href="./index.html">← コラム一覧に戻る</a>
    <span class="eyebrow">Night PASS Column</span>
    <h1 style="font-family:'Shippori Mincho',serif;font-weight:800;font-size:clamp(24px,3.4vw,32px);margin:10px 0 4px;text-wrap:balance;">${esc(article.title)}</h1>
    <div class="article-date">${esc(dateLabel)}</div>
    ${article.coverImage ? `<div class="article-cover" style="margin-top:18px;"><img src="${esc(article.coverImage)}" alt="${esc(article.title)}"></div>` : ''}
    <div class="article-body">${renderArticleBlocksHtmlForStaticExport(article.blocks)}</div>
  </div>
</main>
</body>
</html>
`;
}
function buildColumnArchiveHtml(articles){
  const styleEl = document.querySelector('style');
  const styleTag = styleEl ? `<style>${styleEl.textContent}</style>` : '';
  const baseUrl = normalizedSeoBaseUrl();
  const canonicalUrl = baseUrl ? baseUrl + 'column/' : '';
  const cards = articles.map(a => `
    <a class="column-card" href="${encodeURIComponent(a.slug)}.html" style="text-decoration:none;">
      <div class="photo">${a.coverImage ? `<img src="${esc(a.coverImage)}" alt="${esc(a.title)}">` : esc((a.title||'?').trim().charAt(0))}</div>
      <div class="body">
        <div class="name">${esc(a.title)}</div>
        <div class="excerpt">${esc(a.excerpt)}</div>
        <div class="column-meta">${esc(articleDateLabel(a))}</div>
      </div>
    </a>
  `).join('');
  return `<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>コラム一覧 | Night PASS</title>
<meta name="description" content="Night PASSのコラム・お役立ち記事の一覧ページです。">
${canonicalUrl ? `<link rel="canonical" href="${esc(canonicalUrl)}">` : ''}
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Shippori+Mincho:wght@500;700;800&family=Zen+Kaku+Gothic+New:wght@400;500;700;900&family=Cormorant+Garamond:ital,wght@0,500;1,500&display=swap" rel="stylesheet">
${styleTag}
</head>
<body>
<header class="topbar">
  <a class="brand" href="../index.html" style="text-decoration:none;">
    ${BRAND_ICON_SVG}
    <div class="brand-text">
      <span class="mark">Night PASS</span>
      <span class="sub">TOKYO NIGHT LOUNGE GUIDE</span>
    </div>
  </a>
  <div class="nav-actions"><a class="btn-ghost" href="../index.html">トップへ戻る</a></div>
</header>
<main class="active">
  <div class="static-page columns-page">
    <a class="back" href="../index.html">← トップに戻る</a>
    <h1 style="margin-top:18px;">コラム</h1>
    ${articles.length ? `<div class="column-grid">${cards}</div>` : `<div class="empty-note">公開中の記事はまだありません。</div>`}
  </div>
</main>
</body>
</html>
`;
}
/* ファイルのダウンロードを提供する。Claude Artifacts上で開いている場合は
   ブラウザへの直接ダウンロードがブロックされる（サンドボックスの制約）ため、
   window.claude.downloads（Artifactsが提供するダウンロード許可の仕組み）を
   優先的に使う。GitHub Pagesやローカルファイルとして開いている通常の
   ブラウザ環境では window.claude が存在しないため、従来どおり
   Blob + <a download> でそのままダウンロードする。 */
async function offerFileDownload(filename, htmlContent){
  if(window.claude){
    try{
      let downloads = null;
      if(typeof window.claude.use === 'function') downloads = await window.claude.use('downloads');
      else if(window.claude.downloads) downloads = window.claude.downloads;
      if(!downloads){
        showToast('このプレビュー環境ではファイルのダウンロードに対応していません。GitHub Pages等で公開したページからお試しください');
        return false;
      }
      await downloads.save({ filename, data: htmlContent });
      return true;
    }catch(e){
      showToast('ダウンロードが許可されませんでした' + (e && e.code ? `（${e.code}）` : ''));
      return false;
    }
  }
  const blob = new Blob([htmlContent], { type:'text/html;charset=utf-8' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = filename;
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  setTimeout(()=>URL.revokeObjectURL(url), 4000);
  return true;
}
async function exportArticleStaticHtml(id){
  const article = ARTICLES.find(a=>a.id===id);
  if(!article) return;
  if(!article.slug){ showToast('スラッグが未設定のため書き出せません。先に保存してください'); return; }
  const ok = await offerFileDownload(article.slug + '.html', buildArticleStaticHtml(article));
  if(ok) showToast(`「${article.title}」を ${article.slug}.html として書き出しました`);
}
async function exportAllPublicArticlesStatic(){
  const list = getPublicArticles();
  if(!list.length){ showToast('公開中の記事がまだありません'); return; }
  const archiveOk = await offerFileDownload('index.html', buildColumnArchiveHtml(list));
  if(!archiveOk) return;
  for(let i=0;i<list.length;i++){
    await new Promise(r=>setTimeout(r, 350));
    await offerFileDownload(list[i].slug + '.html', buildArticleStaticHtml(list[i]));
  }
  showToast(`記事${list.length}件と一覧ページ（index.html）をまとめて書き出しました`);
}

/* ---------------- admin ---------------- */
function emptyStoreDraft(){
  return { id:'', name:'', area:'', prefecture:'', genre:'キャバクラ', platinum:false, catch:'', wage:'', tags:[], photos:[], casts:[], instagram:'', tiktok:'', lineUrl:'', phone:'', email:'', address:'', hours:'', closedDay:'', description:'', descriptionBlocks:[] };
}

/* ---- photo upload (drag & drop / click to browse, up to 3 per store) ---- */
let adminPhotoDraft = ['', '', '', ''];
let adminStoreDescBlocksDraft = [];

/* ---- 店舗紹介文の本文ブロックエディタ（本文の途中に写真を挿入できる） ---- */
const DESC_BLOCK_TYPE_LABELS = { text:'本文', image:'写真' };
function addStoreDescBlock(type){
  adminStoreDescBlocksDraft.push(normalizeDescriptionBlock({type}));
  renderStoreDescBlocksEditor();
}
function removeStoreDescBlock(i){ adminStoreDescBlocksDraft.splice(i,1); renderStoreDescBlocksEditor(); }
function moveStoreDescBlock(i, dir){
  const j = i + dir;
  if(j < 0 || j >= adminStoreDescBlocksDraft.length) return;
  const tmp = adminStoreDescBlocksDraft[i];
  adminStoreDescBlocksDraft[i] = adminStoreDescBlocksDraft[j];
  adminStoreDescBlocksDraft[j] = tmp;
  renderStoreDescBlocksEditor();
}
function updateStoreDescBlockField(i, field, value){
  if(adminStoreDescBlocksDraft[i]) adminStoreDescBlocksDraft[i][field] = value;
}
function handleStoreDescBlockImageInput(e, i){
  const file = e.target.files && e.target.files[0];
  if(file){
    readAndCompressImage(file, STORE_PHOTO_ATTEMPTS, STORE_PHOTO_TARGET_LEN, dataUrl => {
      if(adminStoreDescBlocksDraft[i]) adminStoreDescBlocksDraft[i].src = dataUrl;
      renderStoreDescBlocksEditor();
    });
  }
  e.target.value = '';
}
function renderStoreDescBlockRowHtml(b, i, total){
  const head = `
    <div class="block-row-head">
      <span class="block-type-label">${esc(DESC_BLOCK_TYPE_LABELS[b.type] || b.type)}</span>
      <div class="block-row-actions">
        <button type="button" onclick="moveStoreDescBlock(${i},-1)" ${i===0?'disabled':''} title="上へ">↑</button>
        <button type="button" onclick="moveStoreDescBlock(${i},1)" ${i===total-1?'disabled':''} title="下へ">↓</button>
        <button type="button" onclick="removeStoreDescBlock(${i})" title="削除">×</button>
      </div>
    </div>`;
  let body = '';
  if(b.type === 'text'){
    body = `<textarea rows="4" placeholder="お店の雰囲気、こだわり、こんなシーンにおすすめ...等" oninput="updateStoreDescBlockField(${i},'text',this.value)">${esc(b.text)}</textarea>`;
  } else if(b.type === 'image'){
    body = `
      <div style="display:flex; gap:12px; align-items:flex-start; flex-wrap:wrap;">
        <div>
          ${b.src ? `<img src="${esc(b.src)}" class="block-img-preview" alt="">` : ''}
          <div style="margin-top:6px;">
            <input type="file" id="store-desc-block-img-file-${i}" accept="image/*" hidden onchange="handleStoreDescBlockImageInput(event,${i})">
            <button type="button" class="btn-manager-add" onclick="document.getElementById('store-desc-block-img-file-${i}').click()">画像を選択</button>
          </div>
        </div>
        <div style="flex:1 1 200px; display:flex; flex-direction:column; gap:8px;">
          <input type="text" placeholder="代替テキスト（alt）" value="${esc(b.alt)}" oninput="updateStoreDescBlockField(${i},'alt',this.value)">
          <input type="text" placeholder="キャプション（任意）例：店舗入り口" value="${esc(b.caption)}" oninput="updateStoreDescBlockField(${i},'caption',this.value)">
        </div>
      </div>`;
  }
  return `<div class="block-row">${head}${body}</div>`;
}
function renderStoreDescBlocksEditor(){
  const wrap = document.getElementById('store-desc-blocks-editor');
  if(!wrap) return;
  wrap.innerHTML = adminStoreDescBlocksDraft.length
    ? adminStoreDescBlocksDraft.map((b,i) => renderStoreDescBlockRowHtml(b, i, adminStoreDescBlocksDraft.length)).join('')
    : `<div class="manager-empty">まだブロックがありません。下のボタンから本文や写真を追加してください。</div>`;
}

function renderPhotoSlots(){
  const wrap = document.getElementById('photo-slots');
  if(!wrap) return;
  wrap.innerHTML = [0,1,2,3].map(i => {
    const src = adminPhotoDraft[i];
    return `
      <div class="photo-slot">
        <div class="photo-drop ${src?'has-image':''}"
             ondragover="event.preventDefault(); this.classList.add('drag-over')"
             ondragleave="this.classList.remove('drag-over')"
             ondrop="handlePhotoDrop(event, ${i})"
             onclick="document.getElementById('photo-file-${i}').click()">
          ${src
            ? `<img src="${esc(src)}" alt="店舗写真${i+1}">`
            : `<div class="photo-drop-hint"><span>＋</span>ドロップ<br>または選択</div>`}
          <input type="file" id="photo-file-${i}" accept="image/*" hidden onchange="handlePhotoInput(event, ${i})">
        </div>
        ${src ? `<button type="button" class="photo-remove" onclick="event.stopPropagation(); removePhoto(${i})">削除</button>` : `<span class="photo-slot-label">${i===0?'メイン写真':'サブ写真'+i}</span>`}
      </div>
    `;
  }).join('');
}

function handlePhotoDrop(e, idx){
  e.preventDefault();
  e.currentTarget.classList.remove('drag-over');
  const file = e.dataTransfer && e.dataTransfer.files && e.dataTransfer.files[0];
  if(file) processPhotoFile(file, idx);
}
function handlePhotoInput(e, idx){
  const file = e.target.files && e.target.files[0];
  if(file) processPhotoFile(file, idx);
  e.target.value = '';
}
/* ---- shared image compression (store photos / cast photos) ----
   共有データベースは1店舗あたり256KBまで。店舗写真（最大4枚）と
   キャスト写真の両方がこの中に収まるよう、用途ごとに目標サイズを
   分けて段階的に圧縮する。 */
function compressImageEl(img, maxDim, quality){
  let w = img.width, h = img.height;
  if(w > maxDim || h > maxDim){
    if(w > h){ h = Math.round(h * maxDim / w); w = maxDim; }
    else{ w = Math.round(w * maxDim / h); h = maxDim; }
  }
  const canvas = document.createElement('canvas');
  canvas.width = w; canvas.height = h;
  canvas.getContext('2d').drawImage(img, 0, 0, w, h);
  return canvas.toDataURL('image/jpeg', quality);
}
function compressImageToTarget(img, attempts, targetLen){
  let dataUrl = '';
  for(const [dim,q] of attempts){
    dataUrl = compressImageEl(img, dim, q);
    if(dataUrl.length <= targetLen) break;
  }
  return dataUrl;
}
function readAndCompressImage(file, attempts, targetLen, onDone){
  if(!file.type || !file.type.startsWith('image/')){ showToast('画像ファイルを選択してください'); return; }
  const reader = new FileReader();
  reader.onload = () => {
    const img = new Image();
    img.onload = () => onDone(compressImageToTarget(img, attempts, targetLen));
    img.onerror = () => showToast('画像を読み込めませんでした');
    img.src = reader.result;
  };
  reader.onerror = () => showToast('画像を読み込めませんでした');
  reader.readAsDataURL(file);
}

const STORE_PHOTO_ATTEMPTS = [[560,0.55],[420,0.45],[320,0.38],[240,0.3]];
const STORE_PHOTO_TARGET_LEN = 35000;
const CAST_PHOTO_ATTEMPTS = [[260,0.55],[200,0.45],[160,0.35]];
const CAST_PHOTO_TARGET_LEN = 15000;

function processPhotoFile(file, idx){
  readAndCompressImage(file, STORE_PHOTO_ATTEMPTS, STORE_PHOTO_TARGET_LEN, dataUrl => {
    adminPhotoDraft[idx] = dataUrl;
    renderPhotoSlots();
  });
}
function removePhoto(idx){
  adminPhotoDraft[idx] = '';
  renderPhotoSlots();
}

/* ---- cast (在籍キャスト) rows in the store form ---- */
let adminCastDraft = [];
function renderCastRows(){
  const wrap = document.getElementById('cast-rows');
  if(!wrap) return;
  if(adminCastDraft.length===0){ wrap.innerHTML = `<div class="manager-empty">キャストが未登録です</div>`; return; }
  wrap.innerHTML = adminCastDraft.map((c,i)=>{
    const photo = c.photo || '';
    return `
    <div class="cast-row">
      <div class="cast-photo-wrap">
        <div class="cast-photo-drop ${photo?'has-image':''}" onclick="document.getElementById('cast-photo-file-${i}').click()">
          ${photo ? `<img src="${esc(photo)}" alt="キャスト写真">` : `<span class="plus">＋</span>`}
          <input type="file" id="cast-photo-file-${i}" accept="image/*" hidden onchange="handleCastPhotoInput(event, ${i})">
        </div>
        ${photo ? `<button type="button" class="cast-photo-remove" onclick="event.stopPropagation(); removeCastPhoto(${i})" title="削除">×</button>` : ''}
      </div>
      <input type="text" placeholder="キャスト名（源氏名）" value="${esc(c.name)}" oninput="updateCastField(${i},'name',this.value)">
      <input type="text" placeholder="一言コメント" value="${esc(c.catch)}" oninput="updateCastField(${i},'catch',this.value)">
      <button type="button" class="chip-x" onclick="removeCastRow(${i})" title="削除">×</button>
    </div>
  `;
  }).join('');
}
function addCastRow(){ adminCastDraft.push({name:'', catch:'', photo:''}); renderCastRows(); }
function updateCastField(i, field, val){ if(adminCastDraft[i]) adminCastDraft[i][field] = val; }
function removeCastRow(i){ adminCastDraft.splice(i,1); renderCastRows(); }
function handleCastPhotoInput(e, idx){
  const file = e.target.files && e.target.files[0];
  if(file) processCastPhotoFile(file, idx);
  e.target.value = '';
}
function processCastPhotoFile(file, idx){
  readAndCompressImage(file, CAST_PHOTO_ATTEMPTS, CAST_PHOTO_TARGET_LEN, dataUrl => {
    if(adminCastDraft[idx]) adminCastDraft[idx].photo = dataUrl;
    renderCastRows();
  });
}
function removeCastPhoto(idx){
  if(adminCastDraft[idx]) adminCastDraft[idx].photo = '';
  renderCastRows();
}

/* ---- area picker: single-row horizontal scroll of chips (popular + normal areas) ----
   prefectureFilter (optional) scopes the chip list to areas registered under
   that 都道府県, matching the admin store form's 都道府県→エリア cascading UX. */
function areaChipsHtml(currentArea, prefectureFilter){
  let popular = POPULAR_AREAS.slice();
  let normal = NORMAL_AREAS.slice();
  if(prefectureFilter){
    popular = popular.filter(a=>a.prefecture===prefectureFilter);
    normal = normal.filter(a=>a.prefecture===prefectureFilter);
  }
  const known = new Set([...popular, ...normal].map(a=>a.name));
  const chips = [];
  if(currentArea && !known.has(currentArea)){
    chips.push(`<button type="button" class="area-chip active" data-area="${esc(currentArea)}" onclick="selectAreaChip('${esc(currentArea)}')">${esc(currentArea)}</button>`);
  }
  popular.forEach(a=>{
    chips.push(`<button type="button" class="area-chip ${a.name===currentArea?'active':''}" data-area="${esc(a.name)}" onclick="selectAreaChip('${esc(a.name)}')">${esc(a.name)}</button>`);
  });
  normal.forEach(a=>{
    chips.push(`<button type="button" class="area-chip normal-area ${a.name===currentArea?'active':''}" data-area="${esc(a.name)}" onclick="selectAreaChip('${esc(a.name)}')">${esc(a.name)}</button>`);
  });
  if(chips.length===0){
    return prefectureFilter
      ? `<div class="manager-empty">選択した都道府県に登録済みのエリアがありません。下の「人気エリアの管理」または「エリア追加」から登録してください</div>`
      : `<div class="manager-empty">エリアがまだ登録されていません。下の「人気エリアの管理」または「エリア追加」から登録してください</div>`;
  }
  return chips.join('');
}

function selectAreaChip(area){
  const input = document.getElementById('af-area');
  if(!input) return;
  input.value = area;
  const wrap = document.getElementById('af-area-chips');
  if(wrap){
    wrap.querySelectorAll('.area-chip').forEach(el=>{
      el.classList.toggle('active', el.dataset.area === area);
    });
  }
}

function refreshAreaChips(){
  const input = document.getElementById('af-area');
  const wrap = document.getElementById('af-area-chips');
  const prefSel = document.getElementById('af-prefecture');
  if(!input || !wrap) return;
  wrap.innerHTML = areaChipsHtml(input.value, prefSel ? prefSel.value : '');
}

function handlePrefectureChangeInForm(){
  const input = document.getElementById('af-area');
  if(input) input.value = '';
  refreshAreaChips();
}

function renderTagChipsHtml(currentTagsStr){
  const current = (currentTagsStr||'').split(',').map(t=>t.trim()).filter(Boolean);
  if(TAG_PRESETS.length===0) return `<div class="manager-empty">タグがまだ登録されていません</div>`;
  return TAG_PRESETS.map(t => `
    <button type="button" class="tag-chip ${current.includes(t)?'active':''}" onclick="toggleTagPreset('${esc(t)}')">${esc(t)}</button>
  `).join('');
}

function toggleTagPreset(tag){
  const input = document.getElementById('af-tags');
  if(!input) return;
  let current = input.value.split(',').map(t=>t.trim()).filter(Boolean);
  if(current.includes(tag)) current = current.filter(t=>t!==tag);
  else current.push(tag);
  input.value = current.join(', ');
  const chipsWrap = document.getElementById('tag-preset-chips');
  if(chipsWrap) chipsWrap.innerHTML = renderTagChipsHtml(input.value);
}

/* ---- popular area manager ---- */
function renderAreaManager(){
  const wrap = document.getElementById('area-manager-list');
  if(!wrap) return;
  if(POPULAR_AREAS.length===0){ wrap.innerHTML = `<div class="manager-empty">エリアがまだ登録されていません</div>`; return; }
  wrap.innerHTML = POPULAR_AREAS.map(a => `
    <span class="manager-chip">${esc(a.name)}（${esc(a.prefecture)}）<button type="button" class="chip-x" onclick="handleDeleteArea('${esc(a.name)}')" title="削除">×</button></span>
  `).join('');
}

async function handleAddArea(){
  const input = document.getElementById('new-area-input');
  const prefSel = document.getElementById('new-area-prefecture');
  const v = input.value.trim();
  const pref = prefSel && prefSel.value ? prefSel.value : '東京都';
  if(!v){ showToast('エリア名を入力してください'); return; }
  if(areaExists(v)){ showToast('すでに登録されています'); return; }
  POPULAR_AREAS.push({name:v, prefecture:pref});
  const ok = await saveAreas();
  input.value = '';
  renderAreaManager();
  renderQuickFilters();
  syncQuickChips();
  refreshAreaChips();
  populateFilterOptions();
  showToast(ok ? `「${v}」を人気エリアに追加しました` : `「${v}」を追加しましたが、保存に失敗しました。もう一度お試しください`);
}

async function handleDeleteArea(a){
  POPULAR_AREAS = POPULAR_AREAS.filter(x => x.name !== a);
  const ok = await saveAreas();
  renderAreaManager();
  renderQuickFilters();
  syncQuickChips();
  refreshAreaChips();
  populateFilterOptions();
  showToast(ok ? `「${a}」を削除しました` : '削除に失敗しました。もう一度お試しください');
}

/* ---- normal (non-popular) area manager ---- */
function renderNormalAreaManager(){
  const wrap = document.getElementById('normal-area-manager-list');
  if(!wrap) return;
  if(NORMAL_AREAS.length===0){ wrap.innerHTML = `<div class="manager-empty">通常エリアはまだ登録されていません</div>`; return; }
  wrap.innerHTML = NORMAL_AREAS.map(a => `
    <span class="manager-chip">${esc(a.name)}（${esc(a.prefecture)}）<button type="button" class="chip-x" onclick="handleDeleteNormalArea('${esc(a.name)}')" title="削除">×</button></span>
  `).join('');
}

async function handleAddNormalArea(){
  const input = document.getElementById('new-normal-area-input');
  const prefSel = document.getElementById('new-normal-area-prefecture');
  const v = input.value.trim();
  const pref = prefSel && prefSel.value ? prefSel.value : '東京都';
  if(!v){ showToast('エリア名を入力してください'); return; }
  if(areaExists(v)){ showToast('すでに登録されています'); return; }
  NORMAL_AREAS.push({name:v, prefecture:pref});
  const ok = await saveNormalAreas();
  input.value = '';
  renderNormalAreaManager();
  refreshAreaChips();
  populateFilterOptions();
  showToast(ok ? `「${v}」を通常エリアに追加しました` : `「${v}」を追加しましたが、保存に失敗しました。もう一度お試しください`);
}

async function handleDeleteNormalArea(a){
  NORMAL_AREAS = NORMAL_AREAS.filter(x => x.name !== a);
  const ok = await saveNormalAreas();
  renderNormalAreaManager();
  refreshAreaChips();
  populateFilterOptions();
  showToast(ok ? `「${a}」を削除しました` : '削除に失敗しました。もう一度お試しください');
}

/* ---- genre (業種) manager ---- */
function refreshGenreSelect(){
  const genreSel = document.getElementById('af-genre');
  if(genreSel) genreSel.innerHTML = GENRE_LIST.map(g=>`<option ${g===genreSel.value?'selected':''}>${esc(g)}</option>`).join('');
}

function renderGenreManager(){
  const wrap = document.getElementById('genre-manager-list');
  if(!wrap) return;
  if(GENRE_LIST.length===0){ wrap.innerHTML = `<div class="manager-empty">業種がまだ登録されていません</div>`; return; }
  wrap.innerHTML = GENRE_LIST.map(g => `
    <span class="manager-chip"><span class="manager-chip-label" onclick="handleRenameGenre('${esc(g)}')" title="クリックして名称を変更">${esc(g)}</span><button type="button" class="chip-x" onclick="handleDeleteGenre('${esc(g)}')" title="削除">×</button></span>
  `).join('');
}

async function handleAddGenre(){
  const input = document.getElementById('new-genre-input');
  const v = input.value.trim();
  if(!v){ showToast('業種名を入力してください'); return; }
  if(GENRE_LIST.includes(v)){ showToast('すでに登録されています'); return; }
  GENRE_LIST.push(v);
  const ok = await saveGenres();
  input.value = '';
  renderGenreManager();
  renderQuickFilters();
  syncQuickChips();
  refreshGenreSelect();
  showToast(ok ? `「${v}」を追加しました` : `「${v}」を追加しましたが、保存に失敗しました。もう一度お試しください`);
}

async function handleDeleteGenre(g){
  if(GENRE_LIST.length <= 1){ showToast('最低1つは業種が必要です'); return; }
  GENRE_LIST = GENRE_LIST.filter(x => x !== g);
  const ok = await saveGenres();
  renderGenreManager();
  renderQuickFilters();
  syncQuickChips();
  refreshGenreSelect();
  showToast(ok ? `「${g}」を削除しました` : '削除に失敗しました。もう一度お試しください');
}

async function handleRenameGenre(oldName){
  const input = prompt('新しい業種名を入力してください', oldName);
  if(input === null) return;
  const v = input.trim();
  if(!v){ showToast('業種名を入力してください'); return; }
  if(v === oldName) return;
  if(GENRE_LIST.includes(v)){ showToast('その業種名はすでに使われています'); return; }
  const idx = GENRE_LIST.indexOf(oldName);
  if(idx === -1) return;
  GENRE_LIST[idx] = v;
  if(GENRE_ICONS[oldName] && !GENRE_ICONS[v]) GENRE_ICONS[v] = GENRE_ICONS[oldName];
  const ok = await saveGenres();

  const affected = STORES.filter(s => s.genre === oldName);
  affected.forEach(s => { s.genre = v; });
  if(affected.length){
    try{ await Promise.all(affected.map(s => persistStore(s))); }catch(e){}
  }

  renderGenreManager();
  renderQuickFilters();
  syncQuickChips();
  refreshGenreSelect();
  populateFilterOptions();
  applyFilters();
  renderAdminList();
  showToast(ok ? `「${oldName}」を「${v}」に変更しました` : '変更しましたが、保存に失敗しました。もう一度お試しください');
}

/* ---- tag preset manager ---- */
function renderTagManager(){
  const wrap = document.getElementById('tag-manager-list');
  if(!wrap) return;
  if(TAG_PRESETS.length===0){ wrap.innerHTML = `<div class="manager-empty">タグがまだ登録されていません</div>`; return; }
  wrap.innerHTML = TAG_PRESETS.map(t => `
    <span class="manager-chip">${esc(t)}<button type="button" class="chip-x" onclick="handleDeleteTagPreset('${esc(t)}')" title="削除">×</button></span>
  `).join('');
}

async function handleAddTagPreset(){
  const input = document.getElementById('new-tag-input');
  const v = input.value.trim();
  if(!v){ showToast('タグを入力してください'); return; }
  if(TAG_PRESETS.includes(v)){ showToast('すでに登録されています'); return; }
  TAG_PRESETS.push(v);
  const ok = await saveTagPresets();
  input.value = '';
  renderTagManager();
  const chipsWrap = document.getElementById('tag-preset-chips');
  const tagsInput = document.getElementById('af-tags');
  if(chipsWrap && tagsInput) chipsWrap.innerHTML = renderTagChipsHtml(tagsInput.value);
  showToast(ok ? `「${v}」を追加しました` : `「${v}」を追加しましたが、保存に失敗しました。もう一度お試しください`);
}

async function handleDeleteTagPreset(t){
  TAG_PRESETS = TAG_PRESETS.filter(x => x !== t);
  const ok = await saveTagPresets();
  renderTagManager();
  const chipsWrap = document.getElementById('tag-preset-chips');
  const tagsInput = document.getElementById('af-tags');
  if(chipsWrap && tagsInput) chipsWrap.innerHTML = renderTagChipsHtml(tagsInput.value);
  showToast(ok ? `「${t}」を削除しました` : '削除に失敗しました。もう一度お試しください');
}

/* ---- 利用規約 / 運営会社情報 editors ---- */
async function handleSaveTerms(){
  const content = document.getElementById('terms-editor').value;
  const published = document.getElementById('terms-published').checked;
  SITE_TERMS = { content, published };
  const ok = await saveTerms();
  renderFooterLinks();
  const badge = document.getElementById('terms-publish-badge');
  if(badge){ badge.textContent = published ? '公開中' : '非公開'; badge.className = 'publish-badge ' + (published?'on':'off'); }
  showToast(ok ? '利用規約を保存しました' : '保存に失敗しました。もう一度お試しください');
}

async function handleSaveCompany(){
  SITE_COMPANY = {
    name: document.getElementById('company-name').value.trim(),
    representative: document.getElementById('company-representative').value.trim(),
    address: document.getElementById('company-address').value.trim(),
    phone: document.getElementById('company-phone').value.trim(),
    email: document.getElementById('company-email').value.trim(),
    founded: document.getElementById('company-founded').value.trim(),
    business: document.getElementById('company-business').value.trim(),
    note: document.getElementById('company-note').value.trim(),
    published: document.getElementById('company-published').checked,
  };
  const ok = await saveCompany();
  renderFooterLinks();
  const badge = document.getElementById('company-publish-badge');
  if(badge){ badge.textContent = SITE_COMPANY.published ? '公開中' : '非公開'; badge.className = 'publish-badge ' + (SITE_COMPANY.published?'on':'off'); }
  showToast(ok ? '運営会社情報を保存しました' : '保存に失敗しました。もう一度お試しください');
}

async function handleSaveSeoSettings(){
  SITE_SEO = { baseUrl: document.getElementById('seo-base-url').value.trim() };
  const ok = await saveSeoSettings();
  const flag = document.getElementById('seo-save-flag');
  if(flag){
    flag.textContent = ok ? '保存しました' : '保存に失敗しました（再試行してください）';
    flag.classList.add('show');
    setTimeout(()=>flag.classList.remove('show'), 2200);
  }
  showToast(ok ? 'SEO設定を保存しました' : '保存に失敗しました。もう一度お試しください');
}

/* ---- admin user manager ---- */
function renderUserManager(){
  const wrap = document.getElementById('user-manager-list');
  if(!wrap) return;
  if(ADMIN_USERS.length===0){ wrap.innerHTML = `<div class="manager-empty">ユーザーが登録されていません</div>`; return; }
  wrap.innerHTML = ADMIN_USERS.map(u => `
    <span class="manager-chip">${esc(u.username)}${u.username===adminCurrentUser?'<span style="color:var(--terracotta); font-size:10.5px; margin-left:4px;">（ログイン中）</span>':''}<button type="button" class="chip-x" onclick="handleDeleteUser('${esc(u.id)}')" title="削除">×</button></span>
  `).join('');
}

async function handleAddUser(){
  const uInput = document.getElementById('new-user-username');
  const pInput = document.getElementById('new-user-password');
  const username = uInput.value.trim();
  const password = pInput.value;
  if(!username || !password){ showToast('ユーザー名とパスワードを入力してください'); return; }
  if(ADMIN_USERS.some(u => u.username === username)){ showToast('そのユーザー名はすでに使われています'); return; }
  ADMIN_USERS.push({ id: 'u-' + Date.now().toString(36) + Math.random().toString(36).slice(2,6), username, password });
  const ok = await saveAdminUsers();
  uInput.value = ''; pInput.value = '';
  renderUserManager();
  showToast(ok ? `ユーザー「${username}」を追加しました` : `ユーザー「${username}」を追加しましたが、保存に失敗しました。もう一度お試しください`);
}

async function handleDeleteUser(id){
  if(ADMIN_USERS.length <= 1){ showToast('最低1人はユーザーが必要です'); return; }
  const target = ADMIN_USERS.find(u => u.id === id);
  ADMIN_USERS = ADMIN_USERS.filter(u => u.id !== id);
  const ok = await saveAdminUsers();
  renderUserManager();
  showToast(ok ? (target ? `「${target.username}」を削除しました` : '削除しました') : '削除に失敗しました。もう一度お試しください');
}

function renderAdmin(){
  const el = document.getElementById('admin-content');
  if(!adminUnlocked){
    el.innerHTML = `
      <div class="admin-gate">
        <span class="serif">アドミンログイン</span>
        <div style="color:var(--text-muted); font-size:12.5px; line-height:1.8;">店舗情報の編集にはユーザー名とパスワードが必要です</div>
        <input type="text" id="admin-user-input" placeholder="ユーザー名" autocomplete="username">
        <input type="password" id="admin-pass-input" placeholder="パスワードを入力" autocomplete="current-password">
        <button class="btn-search" style="width:100%;" onclick="tryAdminLogin()">ログイン</button>
        <div class="hint">デモ用アカウント：admin / yorupass2026</div>
      </div>`;
    return;
  }
  const selected = STORES.find(s=>s.id===adminSelectedId) || null;
  el.innerHTML = `
    <div class="admin-header">
      <h1>掲載店舗の管理</h1>
      <div style="display:flex; align-items:center; gap:14px;">
        <span style="font-size:12px; color:var(--text-faint);">ログイン中：${esc(adminCurrentUser)}さん</span>
        <a class="btn-ghost" onclick="adminLogout()">ログアウト</a>
        <a class="btn-ghost" onclick="go('home')">サイトを見る</a>
      </div>
    </div>

    <div class="admin-tabs" id="admin-main-tabs">
      <button type="button" class="admin-tab-btn ${adminMainTab==='stores'?'active':''}" data-tab="stores" onclick="switchAdminMainTab('stores')">店舗管理</button>
      <button type="button" class="admin-tab-btn ${adminMainTab==='columns'?'active':''}" data-tab="columns" onclick="switchAdminMainTab('columns')">コラム管理</button>
      <button type="button" class="admin-tab-btn ${adminMainTab==='settings'?'active':''}" data-tab="settings" onclick="switchAdminMainTab('settings')">設定</button>
    </div>

    <div id="admin-tab-panel-stores" ${adminMainTab==='stores'?'':'hidden'}>
      <div class="manager-card">
        <h3>人気エリアの管理</h3>
        <div class="field-hint">ホーム画面の「人気エリアから探す」に表示され、店舗登録時のエリア選択肢にもなります。</div>
        <div class="manager-chips" id="area-manager-list"></div>
        <div class="manager-add-row">
          <select id="new-area-prefecture">${prefectureOptionsHtml('東京都')}</select>
          <input type="text" id="new-area-input" placeholder="新しいエリア名（例：北新地）">
          <button type="button" class="btn-manager-add" onclick="handleAddArea()">追加</button>
        </div>
      </div>

      <div class="manager-card">
        <h3>業種の管理</h3>
        <div class="field-hint">ホーム画面の「業態から探す」に表示され、店舗登録時の業態選択肢にもなります。名前をクリックすると名称を変更できます（既存の店舗の業態も自動的に更新されます）。</div>
        <div class="manager-chips" id="genre-manager-list"></div>
        <div class="manager-add-row">
          <input type="text" id="new-genre-input" placeholder="新しい業種名（例：メイドカフェ）">
          <button type="button" class="btn-manager-add" onclick="handleAddGenre()">追加</button>
        </div>
      </div>

      <div class="manager-card">
        <h3>エリア追加</h3>
        <div class="field-hint">ここに追加した通常エリアは、店舗登録時のエリア選択肢には追加されますが、ホーム画面の「人気エリアから探す」（1ページ目）には表示されません。</div>
        <div class="manager-chips" id="normal-area-manager-list"></div>
        <div class="manager-add-row">
          <select id="new-normal-area-prefecture">${prefectureOptionsHtml('東京都')}</select>
          <input type="text" id="new-normal-area-input" placeholder="新しいエリア名（例：中洲）">
          <button type="button" class="btn-manager-add" onclick="handleAddNormalArea()">追加</button>
        </div>
      </div>

      <div class="manager-card">
        <h3>よく使うタグの管理</h3>
        <div class="field-hint">店舗編集フォームでワンクリックで追加・削除できるタグの候補です。</div>
        <div class="manager-chips" id="tag-manager-list"></div>
        <div class="manager-add-row">
          <input type="text" id="new-tag-input" placeholder="新しいタグ（例：貸切可）">
          <button type="button" class="btn-manager-add" onclick="handleAddTagPreset()">追加</button>
        </div>
      </div>

      <div class="admin-panel">
        <div>
          <div class="platinum-count-hint" id="platinum-count-hint"></div>
          <div class="admin-list-toolbar">
            表示件数：
            <select id="admin-list-pagesize" onchange="handleAdminPageSizeChange()">
              <option value="10" ${adminListPageSize===10?'selected':''}>10件</option>
              <option value="30" ${adminListPageSize===30?'selected':''}>30件</option>
              <option value="50" ${adminListPageSize===50?'selected':''}>50件</option>
            </select>
          </div>
          <div class="admin-list" id="admin-list"></div>
          <div class="admin-list-pager" id="admin-list-pager"></div>
          <button class="admin-add" onclick="selectAdminStore(null,true)">＋ 新しい店舗を追加</button>
        </div>
        <div id="admin-form-wrap"></div>
      </div>
    </div>

    <div id="admin-tab-panel-columns" ${adminMainTab==='columns'?'':'hidden'}>
      <div class="admin-panel">
        <div>
          <div class="field-hint" style="margin-top:0;">SEO記事（コラム／ニュース）を作成・編集できます。下書き・公開・予約投稿を切り替えられ、公開済みの記事には固有のURL（#/column/スラッグ）が発行されます。</div>
          <div class="seo-export-box">
            <div class="seo-export-box-title">SEO対策：記事を本物のクロール可能URLとして書き出す</div>
            <div class="field-hint" style="margin-top:0;">このサイトはサーバーを持たない1ファイル構成のため、#/column/スラッグ というハッシュURLだけでは検索エンジンが記事を正確にインデックスできないことがあります。下のボタンから、公開中の記事を実際に独立したHTMLファイル（例：<code>ginza-guide.html</code>）として書き出せます。ダウンロードされたファイルを、<code>index.html</code>と同じ場所に作った「<code>column</code>」フォルダへアップロードすると、<code>https://あなたのサイト/column/ginza-guide.html</code> という本物のURLとして検索エンジンに認識されるようになります（記事を追加・編集するたびに、再度書き出してアップロードし直す必要があります）。</div>
            <button type="button" class="btn-manager-add" onclick="exportAllPublicArticlesStatic()">📦 公開中の記事をすべて書き出す（一覧ページ付き）</button>
          </div>
          <div class="admin-list" id="article-admin-list"></div>
          <button class="admin-add" onclick="selectAdminArticle(null,true)">＋ 新しい記事を追加</button>
        </div>
        <div id="article-form-wrap"></div>
      </div>
    </div>

    <div id="admin-tab-panel-settings" ${adminMainTab==='settings'?'':'hidden'}>
      <div class="manager-card">
        <h3>ユーザー管理</h3>
        <div class="field-hint">アドミン画面にログインできるユーザーを管理します。最低1人は必要です。パスワードはこのサイトのデータと同じ場所に保存される簡易的なものなので、重要なパスワードの使い回しは避けてください。</div>
        <div class="manager-chips" id="user-manager-list"></div>
        <div class="manager-add-row">
          <input type="text" id="new-user-username" placeholder="ユーザー名">
          <input type="password" id="new-user-password" placeholder="パスワード">
          <button type="button" class="btn-manager-add" onclick="handleAddUser()">追加</button>
        </div>
      </div>

      <div class="manager-card">
        <h3>サイト情報ページ</h3>
        <div class="field-hint">利用規約・運営会社情報を編集できます。それぞれ個別に公開・非公開を切り替えられます。</div>
        <div class="admin-tabs" id="site-page-tabs">
          <button type="button" class="admin-tab-btn ${adminSitePageTab==='terms'?'active':''}" data-tab="terms" onclick="switchSitePageTab('terms')">利用規約</button>
          <button type="button" class="admin-tab-btn ${adminSitePageTab==='company'?'active':''}" data-tab="company" onclick="switchSitePageTab('company')">運営会社情報</button>
        </div>

        <div id="site-page-tab-terms" ${adminSitePageTab==='terms'?'':'hidden'}>
          <div class="toggle-row" style="margin-top:0;">
            <span class="publish-badge ${SITE_TERMS.published?'on':'off'}" id="terms-publish-badge">${SITE_TERMS.published?'公開中':'非公開'}</span>
            <a class="btn-ghost" style="padding:4px 12px; font-size:11.5px;" onclick="go('terms')">プレビュー</a>
          </div>
          <div class="form-grid" style="margin-top:10px;">
            <div class="full">
              <label>本文</label>
              <textarea id="terms-editor" rows="8" placeholder="利用規約の本文を入力してください">${esc(SITE_TERMS.content)}</textarea>
            </div>
          </div>
          <label class="toggle-row"><input type="checkbox" id="terms-published" ${SITE_TERMS.published?'checked':''}> 公開する（フッターに「利用規約」リンクを表示）</label>
          <div class="form-actions">
            <button type="button" class="btn-save" onclick="handleSaveTerms()">保存する</button>
          </div>
        </div>

        <div id="site-page-tab-company" ${adminSitePageTab==='company'?'':'hidden'}>
          <div class="toggle-row" style="margin-top:0;">
            <span class="publish-badge ${SITE_COMPANY.published?'on':'off'}" id="company-publish-badge">${SITE_COMPANY.published?'公開中':'非公開'}</span>
            <a class="btn-ghost" style="padding:4px 12px; font-size:11.5px;" onclick="go('company')">プレビュー</a>
          </div>
          <div class="form-grid" style="margin-top:10px;">
            <div><label>会社名</label><input id="company-name" value="${esc(SITE_COMPANY.name)}"></div>
            <div><label>代表者</label><input id="company-representative" value="${esc(SITE_COMPANY.representative)}"></div>
            <div class="full"><label>所在地</label><input id="company-address" value="${esc(SITE_COMPANY.address)}"></div>
            <div><label>電話番号</label><input id="company-phone" value="${esc(SITE_COMPANY.phone)}"></div>
            <div><label>メールアドレス</label><input id="company-email" value="${esc(SITE_COMPANY.email)}"></div>
            <div><label>設立</label><input id="company-founded" value="${esc(SITE_COMPANY.founded)}"></div>
            <div><label>事業内容</label><input id="company-business" value="${esc(SITE_COMPANY.business)}"></div>
            <div class="full"><label>備考</label><textarea id="company-note" rows="3" placeholder="任意の補足事項があれば入力してください">${esc(SITE_COMPANY.note)}</textarea></div>
          </div>
          <label class="toggle-row"><input type="checkbox" id="company-published" ${SITE_COMPANY.published?'checked':''}> 公開する（フッターに「運営会社情報」リンクを表示）</label>
          <div class="form-actions">
            <button type="button" class="btn-save" onclick="handleSaveCompany()">保存する</button>
          </div>
        </div>
      </div>

      <div class="manager-card">
        <h3>SEO設定</h3>
        <div class="field-hint">コラム記事を「静的HTMLとして書き出す」機能で、canonical（正規）URLを正しく発行するために使う、サイトの公開先URLです。例：GitHub Pagesで公開している場合は <code>https://ユーザー名.github.io/リポジトリ名/</code> のように、末尾にスラッシュを付けて入力してください。未入力のままでもサイトは通常どおり動作しますが、canonicalタグや書き出したHTMLの正規URLが発行されません。</div>
        <div class="form-grid" style="margin-top:10px;">
          <div class="full"><label>サイトの公開URL（ベースURL）</label><input id="seo-base-url" value="${esc(SITE_SEO.baseUrl)}" placeholder="https://ユーザー名.github.io/リポジトリ名/"></div>
        </div>
        <div class="form-actions">
          <button type="button" id="seo-save-btn" class="btn-save" onclick="handleSaveSeoSettings()">保存する</button>
          <span class="save-flag" id="seo-save-flag">保存しました</span>
        </div>
      </div>
    </div>
  `;
  renderAdminList();
  renderAdminForm(selected);
  renderGenreManager();
  renderAreaManager();
  renderNormalAreaManager();
  renderTagManager();
  renderUserManager();
  const selectedArticle = ARTICLES.find(a=>a.id===adminArticleSelectedId) || null;
  renderArticleAdminList();
  renderArticleAdminForm(selectedArticle);
}

function tryAdminLogin(){
  const u = document.getElementById('admin-user-input').value.trim();
  const p = document.getElementById('admin-pass-input').value;
  const match = ADMIN_USERS.find(x => x.username === u && x.password === p);
  if(match){
    adminUnlocked = true;
    adminCurrentUser = match.username;
    renderAdmin();
  }else{
    showToast('ユーザー名またはパスワードが違います');
  }
}

function adminLogout(){
  adminUnlocked = false;
  adminCurrentUser = '';
  renderAdmin();
}

function handleAdminPageSizeChange(){
  const sel = document.getElementById('admin-list-pagesize');
  adminListPageSize = parseInt(sel.value, 10) || 10;
  adminListPage = 1;
  renderAdminList();
}

function goAdminListPage(p){
  adminListPage = p;
  renderAdminList();
  const listEl = document.getElementById('admin-list');
  if(listEl) listEl.scrollTo({top:0, behavior:'smooth'});
}

function renderAdminList(){
  const list = document.getElementById('admin-list');
  const pager = document.getElementById('admin-list-pager');
  const hint = document.getElementById('platinum-count-hint');
  if(hint){
    const count = STORES.filter(s=>s.platinum).length;
    hint.textContent = `プラチナプラン契約店：${count} / 10件${count>10?'（上限を超えています。トップページには先頭10件のみ表示されます）':''}`;
    hint.classList.toggle('over', count>10);
  }
  if(STORES.length===0){
    list.innerHTML = `<div style="padding:20px; color:var(--text-faint); font-size:13px;">店舗がまだ登録されていません</div>`;
    if(pager) pager.innerHTML = '';
    return;
  }

  const totalPages = Math.max(1, Math.ceil(STORES.length / adminListPageSize));
  if(adminListPage > totalPages) adminListPage = totalPages;
  if(adminListPage < 1) adminListPage = 1;
  const startIdx = (adminListPage - 1) * adminListPageSize;
  const pageStores = STORES.slice(startIdx, startIdx + adminListPageSize);

  list.innerHTML = pageStores.map(s=>`
    <div class="admin-row ${s.id===adminSelectedId?'active':''}" onclick="selectAdminStore('${s.id}')">
      <div>
        <div class="rn">${esc(s.name)}${s.platinum?'<span class="platinum-badge">プラチナ</span>':''}</div>
        <div class="ra">${esc(s.prefecture||'')}${s.prefecture?' ':''}${esc(s.area)} ・ ${esc(s.genre)}</div>
      </div>
      <span class="del" onclick="event.stopPropagation(); deleteStore('${s.id}')">削除</span>
    </div>
  `).join('');

  if(pager){
    if(totalPages <= 1){ pager.innerHTML = ''; }
    else{
      pager.innerHTML = `
        <button type="button" onclick="goAdminListPage(${adminListPage-1})" ${adminListPage<=1?'disabled':''}>← 前へ</button>
        <span class="page-info">${adminListPage} / ${totalPages} ページ（全${STORES.length}件）</span>
        <button type="button" onclick="goAdminListPage(${adminListPage+1})" ${adminListPage>=totalPages?'disabled':''}>次へ →</button>
      `;
    }
  }
}

function selectAdminStore(id, isNew){
  adminSelectedId = isNew ? null : id;
  renderAdminList();
  renderAdminForm(isNew ? emptyStoreDraft() : STORES.find(s=>s.id===id));
  const formWrap = document.getElementById('admin-form-wrap');
  if(formWrap) formWrap.scrollIntoView({ behavior:'smooth', block:'start' });
}

function renderAdminForm(store){
  const wrap = document.getElementById('admin-form-wrap');
  if(!store){
    wrap.innerHTML = `<div class="admin-form" style="text-align:center; color:var(--text-faint); padding:60px 20px;">左のリストから店舗を選ぶか、<br>「＋ 新しい店舗を追加」を押してください</div>`;
    return;
  }
  const isNew = !store.id;
  adminPhotoDraft = [0,1,2,3].map(i => (store.photos && store.photos[i]) || '');
  adminCastDraft = (store.casts||[]).map(c => ({name:c.name||'', catch:c.catch||'', photo:c.photo||''}));
  adminStoreDescBlocksDraft = (store.descriptionBlocks||[]).map(normalizeDescriptionBlock);
  wrap.innerHTML = `
    <div class="admin-form">
      <h3>${isNew ? '新規店舗を追加' : '店舗情報を編集：'+esc(store.name)}</h3>
      <label class="toggle-row" style="margin-top:2px;">
        <input type="checkbox" id="af-platinum" ${store.platinum?'checked':''}> プラチナプラン契約店
      </label>
      <div class="field-hint" style="margin-top:0;">チェックした店舗のみ、トップページ1ページ目に最大10件まで表示されます（検索結果には条件に一致するすべての店舗が表示されます）。</div>
      <div class="form-grid">
        <div><label>店舗名</label><input id="af-name" value="${esc(store.name)}"></div>
        <div><label>業態</label>
          <select id="af-genre">
            ${GENRE_LIST.map(g=>`<option ${store.genre===g?'selected':''}>${esc(g)}</option>`).join('')}
          </select>
        </div>
        <div><label>都道府県</label>
          <select id="af-prefecture" onchange="handlePrefectureChangeInForm()">
            <option value="">選択してください</option>
            ${prefectureOptionsHtml(store.prefecture||'')}
          </select>
        </div>
        <div class="full"><label>エリア</label>
          <input type="hidden" id="af-area" value="${esc(store.area)}">
          <div class="area-chip-scroll" id="af-area-chips">${areaChipsHtml(store.area, store.prefecture||'')}</div>
          <div class="field-hint">まず都道府県を選ぶと、その都道府県に登録済みの「人気エリア」（実線）・「通常エリア」（点線）が横スクロールで表示されます（下の「人気エリアの管理」「エリア追加」から追加できます）</div>
        </div>
        <div><label>セット料金表記</label><input id="af-wage" value="${esc(store.wage)}" placeholder="例：¥15,000〜(60分)"></div>
        <div class="full"><label>キャッチコピー</label><input id="af-catch" value="${esc(store.catch)}" placeholder="一覧に表示される一言"></div>
        <div class="full">
          <label>タグ（カンマ区切り）</label>
          <input id="af-tags" value="${esc((store.tags||[]).join(', '))}" placeholder="個室あり, 会員制, カラオケあり">
          <div class="field-hint">よく使うタグをクリックすると追加・削除できます</div>
          <div class="tag-preset-chips" id="tag-preset-chips">${renderTagChipsHtml((store.tags||[]).join(', '))}</div>
        </div>
        <div class="full">
          <label>店舗写真（メイン1枚＋サブ3枚）</label>
          <div class="photo-slots" id="photo-slots"></div>
          <div class="field-hint">クリック、またはドラッグ＆ドロップで画像をアップロードできます。1枚目が一覧・詳細ページのメイン写真、2〜4枚目がメイン写真の下に並ぶサブ写真になります。タップで拡大表示できます。</div>
        </div>
        <div class="full">
          <label>在籍キャスト</label>
          <div id="cast-rows"></div>
          <button type="button" class="btn-manager-add" style="margin-top:4px;" onclick="addCastRow()">＋ キャストを追加</button>
          <div class="field-hint">丸いアイコンをクリックすると写真を登録できます。源氏名と一言コメントもあわせて入力してください。</div>
        </div>
        <div class="full"><label>住所</label><input id="af-address" value="${esc(store.address)}" placeholder="例：東京都中央区銀座7-5-12"></div>
        <div><label>営業時間</label><input id="af-hours" value="${esc(store.hours)}" placeholder="例：20:00〜翌1:00"></div>
        <div><label>定休日</label><input id="af-closed" value="${esc(store.closedDay)}" placeholder="例：日曜日"></div>
        <div><label>Instagram URL</label><input id="af-ig" value="${esc(store.instagram)}" placeholder="https://www.instagram.com/..."></div>
        <div><label>TikTok URL</label><input id="af-tt" value="${esc(store.tiktok)}" placeholder="https://www.tiktok.com/..."></div>
        <div><label>電話番号</label><input id="af-phone" value="${esc(store.phone)}"></div>
        <div><label>予約受付メール</label><input id="af-email" value="${esc(store.email)}"></div>
        <div class="full"><label>LINE 相談先URL</label><input id="af-line" value="${esc(store.lineUrl)}" placeholder="https://line.me/... または https://lin.ee/...">
          <div class="field-hint">入力すると詳細ページに「LINEで来店相談」ボタンが表示されます</div>
        </div>
        <div><label>緯度（任意）</label><input id="af-lat" value="${store.lat!=null?esc(String(store.lat)):''}" placeholder="例：35.6717">
          <div class="field-hint">未入力ならエリア名から自動推定</div>
        </div>
        <div><label>経度（任意）</label><input id="af-lng" value="${store.lng!=null?esc(String(store.lng)):''}" placeholder="例：139.7650"></div>
        <div class="full">
          <label>店舗紹介文</label>
          <div id="store-desc-blocks-editor"></div>
          <div class="block-add-row">
            <select id="af-new-desc-block-type">
              <option value="text">本文</option>
              <option value="image">写真</option>
            </select>
            <button type="button" class="btn-manager-add" onclick="addStoreDescBlock(document.getElementById('af-new-desc-block-type').value)">＋ ブロックを追加</button>
          </div>
          <div class="field-hint">お店の雰囲気やこだわりを本文ブロックで入力し、店舗入り口やキャストの写真を好きな位置に挿入できます。↑↓ボタンで並び替えできます。</div>
        </div>
      </div>
      <div class="form-actions">
        <button class="btn-save" onclick="saveAdminForm('${isNew?'':store.id}')">保存する</button>
        <span class="save-flag" id="save-flag">保存しました</span>
      </div>
    </div>
  `;
  renderPhotoSlots();
  renderCastRows();
  renderStoreDescBlocksEditor();
}

async function saveAdminForm(existingId){
  const draft = {
    id: existingId || ('s' + Date.now()),
    name: document.getElementById('af-name').value.trim() || '無題の店舗',
    genre: document.getElementById('af-genre').value,
    platinum: document.getElementById('af-platinum').checked,
    prefecture: document.getElementById('af-prefecture').value,
    area: document.getElementById('af-area').value.trim(),
    wage: document.getElementById('af-wage').value.trim(),
    catch: document.getElementById('af-catch').value.trim(),
    tags: document.getElementById('af-tags').value.split(',').map(t=>t.trim()).filter(Boolean),
    photos: adminPhotoDraft.filter(Boolean),
    casts: adminCastDraft.map(c=>({name:(c.name||'').trim(), catch:(c.catch||'').trim(), photo:c.photo||''})).filter(c=>c.name),
    address: document.getElementById('af-address').value.trim(),
    hours: document.getElementById('af-hours').value.trim(),
    closedDay: document.getElementById('af-closed').value.trim(),
    instagram: document.getElementById('af-ig').value.trim(),
    tiktok: document.getElementById('af-tt').value.trim(),
    lineUrl: document.getElementById('af-line').value.trim(),
    phone: document.getElementById('af-phone').value.trim(),
    email: document.getElementById('af-email').value.trim(),
    descriptionBlocks: adminStoreDescBlocksDraft.map(normalizeDescriptionBlock),
    description: adminStoreDescBlocksDraft.filter(b=>b.type==='text' && b.text).map(b=>b.text).join('\n\n'),
    lat: (()=>{ const v=document.getElementById('af-lat').value.trim(); return v===''? null : parseFloat(v); })(),
    lng: (()=>{ const v=document.getElementById('af-lng').value.trim(); return v===''? null : parseFloat(v); })(),
  };
  const idx = STORES.findIndex(s=>s.id===draft.id);
  if(idx >= 0) STORES[idx] = draft; else STORES.push(draft);

  const ok = await persistStore(draft);
  adminSelectedId = draft.id;
  populateFilterOptions();
  applyFilters();
  renderAdminList();
  const flag = document.getElementById('save-flag');
  flag.textContent = ok ? '保存しました' : '保存に失敗しました（再試行してください）';
  flag.classList.add('show');
  setTimeout(()=>flag.classList.remove('show'), 2200);
  showToast(ok ? `「${draft.name}」を保存しました` : '保存に失敗しました');
}

async function deleteStore(id){
  const s = STORES.find(x=>x.id===id);
  if(!s) return;
  if(!confirm(`「${s.name}」を削除しますか？`)) return;
  STORES = STORES.filter(x=>x.id!==id);
  if(adminSelectedId === id) adminSelectedId = null;
  await removeStoreFromStorage(id);
  populateFilterOptions();
  applyFilters();
  renderAdmin();
  showToast('店舗を削除しました');
}

/* ---------------- admin: コラム記事の管理 ---------------- */
function emptyArticleDraft(){
  return { id:'', slug:'', title:'', seoTitle:'', seoDescription:'', excerpt:'', coverImage:'', status:'draft', publishAt:'', blocks:[] };
}
let adminArticleCoverDraft = '';
let adminArticleBlocksDraft = [];

function renderArticleAdminList(){
  const list = document.getElementById('article-admin-list');
  if(!list) return;
  if(ARTICLES.length===0){
    list.innerHTML = `<div style="padding:20px; color:var(--text-faint); font-size:13px;">記事がまだ登録されていません</div>`;
    return;
  }
  const sorted = ARTICLES.slice().sort((a,b) => (b.updatedAt||'').localeCompare(a.updatedAt||''));
  list.innerHTML = sorted.map(a => `
    <div class="admin-row ${a.id===adminArticleSelectedId?'active':''}" onclick="selectAdminArticle('${esc(a.id)}')">
      <div>
        <div class="rn">${esc(a.title || '（無題）')} <span class="publish-badge ${articleStatusClass(a)}">${esc(articleStatusLabel(a))}</span></div>
        <div class="ra">/#/column/${esc(a.slug || '')}</div>
      </div>
      <div style="display:flex; align-items:center; gap:8px;">
        <button type="button" class="article-export-btn" onclick="event.stopPropagation(); exportArticleStaticHtml('${esc(a.id)}')" title="この記事を本物のクロール可能URL用の静的HTMLとして書き出す">静的HTML書き出し</button>
        <span class="del" onclick="event.stopPropagation(); deleteArticleAdmin('${esc(a.id)}')">削除</span>
      </div>
    </div>
  `).join('');
}

function selectAdminArticle(id, isNew){
  adminArticleSelectedId = isNew ? null : id;
  renderArticleAdminList();
  renderArticleAdminForm(isNew ? emptyArticleDraft() : ARTICLES.find(a=>a.id===id));
  const formWrap = document.getElementById('article-form-wrap');
  if(formWrap) formWrap.scrollIntoView({ behavior:'smooth', block:'start' });
}

function autofillArticleSlug(existingId){
  const slugInput = document.getElementById('af-article-slug');
  const titleInput = document.getElementById('af-article-title');
  if(!slugInput || !titleInput) return;
  if(slugInput.value.trim()) return; // don't overwrite a slug the admin already set
  slugInput.value = suggestArticleSlug(titleInput.value, existingId);
}

function handleArticleStatusChange(){
  const statusSel = document.getElementById('af-article-status');
  const scheduleRow = document.getElementById('af-article-schedule-row');
  if(scheduleRow) scheduleRow.hidden = (statusSel.value !== 'scheduled');
}

/* ---- cover image ---- */
function handleArticleCoverInput(e){
  const file = e.target.files && e.target.files[0];
  if(file){
    readAndCompressImage(file, STORE_PHOTO_ATTEMPTS, STORE_PHOTO_TARGET_LEN, dataUrl => {
      adminArticleCoverDraft = dataUrl;
      renderArticleCoverPreview();
    });
  }
  e.target.value = '';
}
function removeArticleCover(){ adminArticleCoverDraft = ''; renderArticleCoverPreview(); }
function renderArticleCoverPreview(){
  const wrap = document.getElementById('article-cover-slot');
  if(!wrap) return;
  wrap.classList.toggle('has-image', !!adminArticleCoverDraft);
  wrap.innerHTML = adminArticleCoverDraft
    ? `<img src="${esc(adminArticleCoverDraft)}" alt="">`
    : `<div class="photo-drop-hint"><span>＋</span>クリックして<br>カバー画像を選択</div>`;
  const removeBtnWrap = document.getElementById('article-cover-remove-wrap');
  if(removeBtnWrap) removeBtnWrap.hidden = !adminArticleCoverDraft;
}

/* ---- content block editor (見出しH2/H3・本文・画像・内部リンク・ボタン) ---- */
function addArticleBlock(type){
  adminArticleBlocksDraft.push(normalizeArticleBlock({type}));
  renderArticleBlocksEditor();
}
function removeArticleBlock(i){ adminArticleBlocksDraft.splice(i,1); renderArticleBlocksEditor(); }
function moveArticleBlock(i, dir){
  const j = i + dir;
  if(j < 0 || j >= adminArticleBlocksDraft.length) return;
  const tmp = adminArticleBlocksDraft[i];
  adminArticleBlocksDraft[i] = adminArticleBlocksDraft[j];
  adminArticleBlocksDraft[j] = tmp;
  renderArticleBlocksEditor();
}
function updateArticleBlockField(i, field, value){
  if(adminArticleBlocksDraft[i]) adminArticleBlocksDraft[i][field] = value;
  if(field === 'linkType') renderArticleBlocksEditor(); // re-render to swap target-picker fields
}
function handleArticleBlockImageInput(e, i){
  const file = e.target.files && e.target.files[0];
  if(file){
    readAndCompressImage(file, STORE_PHOTO_ATTEMPTS, STORE_PHOTO_TARGET_LEN, dataUrl => {
      if(adminArticleBlocksDraft[i]) adminArticleBlocksDraft[i].src = dataUrl;
      renderArticleBlocksEditor();
    });
  }
  e.target.value = '';
}
const BLOCK_TYPE_LABELS = { h2:'見出し（H2）', h3:'見出し（H3）', paragraph:'本文', image:'画像', link:'内部リンク／外部リンク', button:'ボタン' };

function articleLinkTargetFieldsHtml(b, i){
  const typeSel = `
    <select onchange="updateArticleBlockField(${i},'linkType',this.value)">
      <option value="external" ${b.linkType==='external'?'selected':''}>外部URL</option>
      <option value="store" ${b.linkType==='store'?'selected':''}>内部リンク（店舗ページ）</option>
      <option value="article" ${b.linkType==='article'?'selected':''}>内部リンク（他の記事）</option>
    </select>`;
  let targetField = '';
  if(b.linkType === 'store'){
    targetField = `<select onchange="updateArticleBlockField(${i},'targetId',this.value)">
      <option value="">店舗を選択してください</option>
      ${STORES.map(s=>`<option value="${esc(s.id)}" ${b.targetId===s.id?'selected':''}>${esc(s.name)}</option>`).join('')}
    </select>`;
  } else if(b.linkType === 'article'){
    targetField = `<select onchange="updateArticleBlockField(${i},'targetId',this.value)">
      <option value="">記事を選択してください</option>
      ${ARTICLES.map(a=>`<option value="${esc(a.id)}" ${b.targetId===a.id?'selected':''}>${esc(a.title||'（無題）')}</option>`).join('')}
    </select>`;
  } else {
    targetField = `<input type="text" placeholder="https://..." value="${esc(b.url)}" oninput="updateArticleBlockField(${i},'url',this.value)">`;
  }
  return `<div class="block-field-row">${typeSel}${targetField}</div>`;
}

function renderArticleBlockRowHtml(b, i, total){
  const head = `
    <div class="block-row-head">
      <span class="block-type-label">${esc(BLOCK_TYPE_LABELS[b.type] || b.type)}</span>
      <div class="block-row-actions">
        <button type="button" onclick="moveArticleBlock(${i},-1)" ${i===0?'disabled':''} title="上へ">↑</button>
        <button type="button" onclick="moveArticleBlock(${i},1)" ${i===total-1?'disabled':''} title="下へ">↓</button>
        <button type="button" onclick="removeArticleBlock(${i})" title="削除">×</button>
      </div>
    </div>`;
  let body = '';
  if(b.type === 'h2' || b.type === 'h3'){
    body = `<input type="text" placeholder="見出しを入力" value="${esc(b.text)}" oninput="updateArticleBlockField(${i},'text',this.value)">`;
  } else if(b.type === 'paragraph'){
    body = `<textarea rows="4" placeholder="本文を入力" oninput="updateArticleBlockField(${i},'text',this.value)">${esc(b.text)}</textarea>`;
  } else if(b.type === 'image'){
    body = `
      <div style="display:flex; gap:12px; align-items:flex-start; flex-wrap:wrap;">
        <div>
          ${b.src ? `<img src="${esc(b.src)}" class="block-img-preview" alt="">` : ''}
          <div style="margin-top:6px;">
            <input type="file" id="block-img-file-${i}" accept="image/*" hidden onchange="handleArticleBlockImageInput(event,${i})">
            <button type="button" class="btn-manager-add" onclick="document.getElementById('block-img-file-${i}').click()">画像を選択</button>
          </div>
        </div>
        <div style="flex:1 1 200px; display:flex; flex-direction:column; gap:8px;">
          <input type="text" placeholder="代替テキスト（alt）" value="${esc(b.alt)}" oninput="updateArticleBlockField(${i},'alt',this.value)">
          <input type="text" placeholder="キャプション（任意）" value="${esc(b.caption)}" oninput="updateArticleBlockField(${i},'caption',this.value)">
        </div>
      </div>`;
  } else if(b.type === 'link' || b.type === 'button'){
    body = `
      ${articleLinkTargetFieldsHtml(b, i)}
      <input type="text" placeholder="${b.type==='button'?'ボタンのラベル':'リンクの表示テキスト'}" value="${esc(b.text)}" oninput="updateArticleBlockField(${i},'text',this.value)">
    `;
  }
  return `<div class="block-row">${head}${body}</div>`;
}

function renderArticleBlocksEditor(){
  const wrap = document.getElementById('article-blocks-editor');
  if(!wrap) return;
  wrap.innerHTML = adminArticleBlocksDraft.length
    ? adminArticleBlocksDraft.map((b,i) => renderArticleBlockRowHtml(b, i, adminArticleBlocksDraft.length)).join('')
    : `<div class="manager-empty">まだブロックがありません。下のボタンから見出しや本文、画像などを追加してください。</div>`;
}

function renderArticleAdminForm(article){
  const wrap = document.getElementById('article-form-wrap');
  if(!wrap) return;
  if(!article){
    wrap.innerHTML = `<div class="admin-form" style="text-align:center; color:var(--text-faint); padding:60px 20px;">左のリストから記事を選ぶか、<br>「＋ 新しい記事を追加」を押してください</div>`;
    return;
  }
  const isNew = !article.id;
  adminArticleCoverDraft = article.coverImage || '';
  adminArticleBlocksDraft = (article.blocks || []).map(normalizeArticleBlock);
  wrap.innerHTML = `
    <div class="admin-form">
      <h3>${isNew ? '新規記事を追加' : '記事を編集：'+esc(article.title || '（無題）')}</h3>
      <div class="form-grid">
        <div class="full"><label>タイトル</label><input id="af-article-title" value="${esc(article.title)}" onblur="autofillArticleSlug('${isNew?'':esc(article.id)}')" placeholder="記事のタイトル（H1として表示されます）"></div>
        <div class="full">
          <label>URLスラッグ</label>
          <input id="af-article-slug" value="${esc(article.slug)}" placeholder="例：ginza-kyabakura-guide">
          <div class="field-hint">公開URL：#/column/スラッグ　※半角英数字とハイフンのみ。空欄のままタイトル入力欄を離れると自動で候補が入ります。</div>
        </div>
        <div>
          <label>ステータス</label>
          <select id="af-article-status" onchange="handleArticleStatusChange()">
            <option value="draft" ${article.status==='draft'?'selected':''}>下書き</option>
            <option value="published" ${article.status==='published'?'selected':''}>公開</option>
            <option value="scheduled" ${article.status==='scheduled'?'selected':''}>予約投稿</option>
          </select>
        </div>
        <div id="af-article-schedule-row" ${article.status==='scheduled'?'':'hidden'}>
          <label>公開日時（予約投稿）</label>
          <input type="datetime-local" id="af-article-publish-at" value="${esc(article.publishAt)}">
        </div>
        <div class="full"><label>抜粋（コラム一覧に表示される要約）</label><input id="af-article-excerpt" value="${esc(article.excerpt)}" placeholder="一覧カードに表示される一言サマリー"></div>
        <div class="full">
          <label>カバー画像</label>
          <div id="article-cover-slot" class="photo-drop" style="width:240px;height:135px;cursor:pointer;" onclick="document.getElementById('article-cover-file').click()"></div>
          <input type="file" id="article-cover-file" accept="image/*" hidden onchange="handleArticleCoverInput(event)">
          <div id="article-cover-remove-wrap" hidden><button type="button" class="photo-remove" onclick="removeArticleCover()">画像を削除</button></div>
        </div>
        <div class="full"><label>SEOタイトル（未入力時はタイトルを使用）</label><input id="af-article-seo-title" value="${esc(article.seoTitle)}" placeholder="検索結果・タブに表示されるタイトル"></div>
        <div class="full"><label>SEOディスクリプション（未入力時は抜粋を使用）</label><input id="af-article-seo-desc" value="${esc(article.seoDescription)}" placeholder="検索結果に表示される説明文（120字程度推奨）"></div>
        <div class="full">
          <label>本文ブロック</label>
          <div id="article-blocks-editor"></div>
          <div class="block-add-row">
            <select id="af-new-block-type">
              <option value="h2">見出し（H2）</option>
              <option value="h3">見出し（H3）</option>
              <option value="paragraph">本文</option>
              <option value="image">画像</option>
              <option value="link">内部リンク／外部リンク</option>
              <option value="button">ボタン</option>
            </select>
            <button type="button" class="btn-manager-add" onclick="addArticleBlock(document.getElementById('af-new-block-type').value)">＋ ブロックを追加</button>
          </div>
          <div class="field-hint">見出し（H1）は記事タイトルが自動的に使われます。H2・H3・本文・画像・リンク・ボタンを組み合わせて記事を構成してください。↑↓ボタンで並び替えできます。</div>
        </div>
      </div>
      <div class="form-actions">
        <button class="btn-save" onclick="saveArticleAdminForm('${isNew?'':esc(article.id)}')">保存する</button>
        <span class="save-flag" id="article-save-flag">保存しました</span>
      </div>
    </div>
  `;
  renderArticleCoverPreview();
  renderArticleBlocksEditor();
}

async function saveArticleAdminForm(existingId){
  const title = document.getElementById('af-article-title').value.trim();
  let slug = slugify(document.getElementById('af-article-slug').value.trim());
  if(!slug) slug = suggestArticleSlug(title, existingId);
  if(ARTICLES.some(a => a.slug === slug && a.id !== existingId)){
    showToast(`スラッグ「${slug}」は既に使用されています。別のスラッグを入力してください`);
    return;
  }
  const status = document.getElementById('af-article-status').value;
  const publishAtInput = document.getElementById('af-article-publish-at');
  const draft = normalizeArticle({
    id: existingId || ('a' + Date.now()),
    title: title || '無題の記事',
    slug,
    status,
    publishAt: (status === 'scheduled' && publishAtInput) ? publishAtInput.value : '',
    excerpt: document.getElementById('af-article-excerpt').value.trim(),
    coverImage: adminArticleCoverDraft,
    seoTitle: document.getElementById('af-article-seo-title').value.trim(),
    seoDescription: document.getElementById('af-article-seo-desc').value.trim(),
    blocks: adminArticleBlocksDraft,
    createdAt: (ARTICLES.find(a=>a.id===existingId) || {}).createdAt || new Date().toISOString(),
    updatedAt: new Date().toISOString(),
  });
  const idx = ARTICLES.findIndex(a=>a.id===draft.id);
  if(idx >= 0) ARTICLES[idx] = draft; else ARTICLES.push(draft);

  const ok = await persistArticle(draft);
  adminArticleSelectedId = draft.id;
  renderArticleAdminList();
  renderArticleAdminForm(draft);
  const flag = document.getElementById('article-save-flag');
  if(flag){
    flag.textContent = ok ? '保存しました' : '保存に失敗しました（再試行してください）';
    flag.classList.add('show');
    setTimeout(()=>flag.classList.remove('show'), 2200);
  }
  showToast(ok ? `「${draft.title}」を保存しました` : '保存に失敗しました');
}

async function deleteArticleAdmin(id){
  const a = ARTICLES.find(x=>x.id===id);
  if(!a) return;
  if(!confirm(`「${a.title || '無題の記事'}」を削除しますか？`)) return;
  ARTICLES = ARTICLES.filter(x=>x.id!==id);
  if(adminArticleSelectedId === id) adminArticleSelectedId = null;
  await removeArticleFromStorage(id);
  renderArticleAdminList();
  renderArticleAdminForm(ARTICLES.find(x=>x.id===adminArticleSelectedId) || null);
  showToast('記事を削除しました');
}

/* ---------------- boot ---------------- */
(async function init(){
  document.getElementById('store-grid').innerHTML = `<div class="empty"><span class="serif">読み込み中...</span></div>`;
  await Promise.all([loadStores(), loadAreas(), loadNormalAreas(), loadTagPresets(), loadGenres(), loadTerms(), loadCompany(), loadAdminUsers(), loadArticles(), loadSeoSettings()]);
  populateFilterOptions();
  renderQuickFilters();
  applyFilters();
  renderFooterLinks();
  document.getElementById('f-keyword').addEventListener('keydown', e=>{ if(e.key==='Enter') applyFilters(); });
  handleHashRoute();
})();

</script>
</body>
</html>
