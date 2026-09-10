[index_11.html](https://github.com/user-attachments/files/32040033/index_11.html)
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Night PASS | 東京ナイトラウンジ・キャバクラ検索</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Shippori+Mincho:wght@500;700;800&family=Zen+Kaku+Gothic+New:wght@400;500;700;900&family=Cormorant+Garamond:ital,wght@0,500;1,500&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#0d1b30;
    --bg-elevated:#132844;
    --card:#122540;
    --card-line:rgba(201,169,97,0.22);
    --terracotta:#c9a961;
    --terracotta-soft:#e0c48a;
    --olive:#7ea3c4;
    --olive-soft:#6f93b3;
    --text:#eef1f6;
    --text-muted:#a3b3c6;
    --text-faint:#6d7e92;
    --input-bg:#0f2038;
    --ink:#060f1c;
    --ink-elevated:#0a1729;
    --cream:#f3ead0;
    --shadow-warm: 0 0 18px rgba(201,169,97,0.30);
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    background:
      radial-gradient(1200px 600px at 12% -10%, rgba(201,169,97,0.08), transparent 60%),
      radial-gradient(1000px 500px at 92% 0%, rgba(6,15,28,0.05), transparent 55%),
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
    background:rgba(6,15,28,0.94);
    backdrop-filter:blur(10px);
  }
  .brand{ display:flex; flex-direction:column; gap:2px; cursor:pointer; }
  .brand .mark{
    font-family:'Shippori Mincho', serif;
    font-weight:800;
    font-size:22px;
    letter-spacing:0.06em;
    color:var(--terracotta);
  }
  .brand .sub{ font-size:10px; letter-spacing:0.32em; color:#b3a173; }
  .nav-actions{ display:flex; align-items:center; gap:10px; }
  .btn-ghost{
    background:transparent; border:1px solid var(--card-line); color:var(--text-muted);
    padding:9px 16px; border-radius:999px; font-size:13px; letter-spacing:0.03em;
    transition:.2s;
  }
  .btn-ghost:hover{ border-color:var(--terracotta); color:var(--terracotta); }
  /* topbar is a dark band, so its ghost button needs light-on-dark colors */
  .topbar .btn-ghost{ border-color:rgba(253,248,239,0.22); color:#d8cdb4; }
  .topbar .btn-ghost:hover{ border-color:var(--terracotta); color:var(--terracotta); }

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
    background:linear-gradient(180deg, #16294a, #0f2038);
    border:1px solid var(--card-line);
    border-radius:18px;
    padding:20px clamp(14px,3vw,28px);
    box-shadow: 0 20px 50px rgba(6,15,28,0.10), inset 0 1px 0 rgba(255,255,255,0.06);
    position:relative;
  }
  .search-panel::before{
    content:"";
    position:absolute; inset:-1px;
    border-radius:18px;
    padding:1px;
    background:linear-gradient(120deg, rgba(201,169,97,0.45), transparent 30%, transparent 70%, rgba(6,15,28,0.40));
    -webkit-mask:linear-gradient(#000 0 0) content-box, linear-gradient(#000 0 0);
    -webkit-mask-composite:xor; mask-composite:exclude;
    pointer-events:none;
  }
  .search-grid{
    display:grid;
    grid-template-columns: 1.6fr 1fr 1fr auto;
    gap:12px;
  }
  @media (max-width:760px){ .search-grid{ grid-template-columns: 1fr 1fr; } }

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
  .detail-photo img{ width:100%; height:100%; object-fit:cover; }
  .thumb-row{ display:flex; gap:10px; margin-top:12px; }
  .thumb{
    width:76px; height:76px; border-radius:10px; overflow:hidden; padding:0;
    border:2px solid transparent; background:none; cursor:pointer; opacity:.65; transition:.15s; flex-shrink:0;
  }
  .thumb img{ width:100%; height:100%; object-fit:cover; display:block; }
  .thumb:hover{ opacity:1; }
  .thumb.active{ border-color:var(--terracotta); opacity:1; }
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
  .chip-x{ background:none; border:none; color:var(--text-faint); font-size:15px; line-height:1; cursor:pointer; padding:3px 5px; border-radius:50%; }
  .chip-x:hover{ color:#e0685a; background:rgba(224,104,90,0.16); }
  .manager-add-row{ display:flex; gap:8px; }
  .manager-add-row input{
    flex:1; background:var(--input-bg); border:1px solid var(--card-line); border-radius:8px;
    padding:9px 12px; font-size:13px; color:var(--text); outline:none;
  }
  .manager-add-row input:focus{ border-color:var(--terracotta); }
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

  /* ---------- scrollable select (area picker) ---------- */
  .form-grid select.scroll-select{
    background-image:none; padding:6px; height:150px; overflow-y:auto;
  }
  .form-grid select.scroll-select option{ padding:7px 8px; border-radius:5px; }

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

</style>
</head>
<body>


<header class="topbar">
  <div class="brand" onclick="go('home')">
    <span class="mark">Night PASS</span>
    <span class="sub">TOKYO NIGHT LOUNGE GUIDE</span>
  </div>
  <div class="nav-actions">
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
          <label>エリア</label>
          <select id="f-area"><option value="">すべて</option></select>
        </div>
        <div class="field">
          <label>業態</label>
          <select id="f-genre"><option value="">すべて</option></select>
        </div>
        <div class="field" style="align-self:end;">
          <button class="btn-search" onclick="applyFilters()">検索する</button>
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

<footer>Night PASS — 夜のお店紹介サイト（デモ） / 掲載内容はアドミン画面から編集できます</footer>
<div class="toast" id="toast"></div>

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
      const snap = await db.doc('site/' + key).get();
      if(snap.exists){
        const data = snap.data();
        if(data && Array.isArray(data.value)) return data.value;
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
    try{ await db.doc('site/' + key).set({ value }); return true; }catch(e){ return false; }
  }
  try{ localStorage.setItem('yorupass:' + key, JSON.stringify(value)); return true; }catch(e){ return false; }
}

/* ---------------- data layer ---------------- */
const ADMIN_PASS = 'yorupass2026';

const DEFAULT_STORES = [
  {
    id:'s1', name:'Club ROSALIE 銀座', area:'銀座', genre:'キャバクラ',
    catch:'落ち着いた大人の社交場。初めての方も安心のシステムでご案内。',
    wage:'¥15,000〜（60分・税サ込）', tags:['初回割引あり','個室あり','会員制','送り可'],
    photos:[], instagram:'https://www.instagram.com/', tiktok:'',
    phone:'03-1234-5678', email:'reserve@example.com', lineUrl:'https://lin.ee/example1',
    address:'東京都中央区銀座7-5-12 〇〇ビル5F', hours:'20:00〜翌1:00（L.O.翌0:30）', closedDay:'日曜日',
    description:'銀座の路地に佇む、落ち着いた大人のためのラウンジです。初めてのお客様にもスタッフが丁寧にご案内いたしますので、お一人でもお気軽にお立ち寄りください。接待やご会食のご利用、女性同伴のお客様も歓迎しております。',
    casts:[{name:'美咲',catch:'明るい笑顔でお迎えします♪ お酒の相談もどうぞ。'},{name:'麗奈',catch:'ワインとシャンパンには自信あり。聞き上手が特技です。'},{name:'彩乃',catch:'今月入店したばかりです。よろしくお願いします！'}]
  },
  {
    id:'s2', name:'Lounge AMOUR 六本木', area:'六本木', genre:'ラウンジ',
    catch:'International loungeで多国籍なゲストと乾杯を。',
    wage:'¥12,000〜（セット90分）', tags:['英語対応可','外国人スタッフ在籍','カジュアル利用OK'],
    photos:[], instagram:'https://www.instagram.com/', tiktok:'https://www.tiktok.com/',
    phone:'03-2345-6789', email:'info@example.com', lineUrl:'',
    address:'東京都港区六本木3-14-9 〇〇ビル3F', hours:'19:30〜翌2:00', closedDay:'月曜日',
    description:'六本木の交差点近くにあるインターナショナルラウンジ。英語対応可能なスタッフが多数在籍しており、海外からのお客様にもご好評をいただいています。カジュアルな雰囲気で、初めての夜遊びにもおすすめです。',
    casts:[{name:'Yuki',catch:'Speak English & Japanese! Let’s have a great night.'},{name:'ののか',catch:'ダーツと会話が得意です。気軽に声かけてください。'}]
  },
  {
    id:'s3', name:'CLUB NOIR 西麻布', area:'西麻布', genre:'クラブ',
    catch:'会員制の隠れ家クラブ。VIPルーム完備。',
    wage:'¥20,000〜（フリータイム）', tags:['VIPルームあり','会員制','シャンパンコールあり'],
    photos:[], instagram:'https://www.instagram.com/', tiktok:'',
    phone:'03-3456-7890', email:'noir@example.com', lineUrl:'https://lin.ee/example3',
    address:'東京都港区西麻布1-2-3 〇〇ビルB1', hours:'21:00〜翌4:00（二部制）', closedDay:'日曜・祝日',
    description:'西麻布の路地裏、看板を出さない完全会員制のクラブです。落ち着いたVIPルームを3室ご用意しており、記念日のシャンパンコールなど特別な一夜を演出いたします。ご紹介制中心のため、まずはお電話にてご相談ください。',
    casts:[{name:'凛',catch:'シャンパンタワーはお任せください。'},{name:'碧',catch:'落ち着いた会話がお好きな方にぴったりです。'}]
  },
  {
    id:'s4', name:'Girls Bar Sourire 歌舞伎町', area:'新宿・歌舞伎町', genre:'ガールズバー',
    catch:'気軽に立ち寄れるカジュアルガールズバー。',
    wage:'¥3,000〜（30分・チャージ込）', tags:['一人利用歓迎','女性一人でも安心','明朗会計'],
    photos:[], instagram:'https://www.instagram.com/', tiktok:'https://www.tiktok.com/',
    phone:'03-4567-8901', email:'sourire@example.com', lineUrl:'',
    address:'東京都新宿区歌舞伎町1-8-2 〇〇ビル4F', hours:'19:00〜翌3:00', closedDay:'不定休',
    description:'歌舞伎町の路面店でアクセス良好。明朗会計でお財布にやさしく、お一人でもふらっと立ち寄れるカジュアルなガールズバーです。女性のお客様、女子会でのご利用も大歓迎です。',
    casts:[{name:'ゆあ',catch:'カラオケが得意です！一緒に盛り上がりましょう。'},{name:'みお',catch:'お酒は弱いですが、お話するのは大好きです。'}]
  },
  {
    id:'s5', name:'スナック 月あかり', area:'赤坂', genre:'スナック',
    catch:'ママの手料理とカラオケが自慢の隠れ家スナック。',
    wage:'¥5,000〜（チャージ・お通し込）', tags:['カラオケあり','アットホーム','常連多数'],
    photos:[], instagram:'', tiktok:'',
    phone:'03-5678-9012', email:'tsukiakari@example.com', lineUrl:'',
    address:'東京都港区赤坂3-11-5 〇〇ビル2F', hours:'19:00〜翌1:00', closedDay:'日曜日',
    description:'赤坂の路地裏で20年続く、ママの手料理が自慢のアットホームなスナックです。カラオケの機材も充実しており、常連のお客様同士の会話も弾みます。一人でふらっと来られる方も多くいらっしゃいます。',
    casts:[{name:'ママ・薫',catch:'手料理と昔話が得意です。ゆっくりしていってね。'}]
  },
  {
    id:'s6', name:'コンカフェ Melty Star', area:'渋谷', genre:'コンカフェ',
    catch:'キラキラ制服が可愛いコンセプトカフェ。',
    wage:'¥2,500〜（1オーダー制）', tags:['写真撮影OK','学生歓迎','ノンアルコールあり'],
    photos:[], instagram:'https://www.instagram.com/', tiktok:'https://www.tiktok.com/',
    phone:'03-6789-0123', email:'meltystar@example.com', lineUrl:'',
    address:'東京都渋谷区宇田川町15-1 〇〇ビル6F', hours:'17:00〜23:00', closedDay:'水曜日',
    description:'渋谷センター街にあるキラキラ制服が人気のコンセプトカフェです。ノンアルコールメニューも充実しており、20歳未満の方や飲めない方にも安心してご利用いただけます。店内での写真撮影もOKです。',
    casts:[{name:'ふわり',catch:'一緒に写真撮ろうね！ノンアルカクテル作るの得意です。'},{name:'きらら',catch:'ゲームの話で盛り上がれます。'}]
  },
  {
    id:'s7', name:'ニュークラブ 花時-Hanadoki-', area:'恵比寿', genre:'ニュークラブ',
    catch:'上質な接待に応える老舗ニュークラブ。',
    wage:'¥18,000〜（60分）', tags:['接待利用に人気','個室あり','要予約'],
    photos:[], instagram:'https://www.instagram.com/', tiktok:'',
    phone:'03-7890-1234', email:'hanadoki@example.com', lineUrl:'https://lin.ee/example7',
    address:'東京都渋谷区恵比寿1-9-4 〇〇ビル7F', hours:'19:00〜翌0:30', closedDay:'日曜・祝日',
    description:'恵比寿で30年続く老舗のニュークラブです。落ち着いた内装の個室をご用意しており、大切な接待やご会食にご利用いただいております。マナーを心得たスタッフが、上質な時間をお約束いたします。',
    casts:[{name:'紗英',catch:'お客様のお話をじっくり伺うのが信条です。'},{name:'have not decided',catch:''}]
  },
  {
    id:'s8', name:'ダイニング&Bar NOCT', area:'新橋', genre:'ダイニングバー',
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
let adminUnlocked = false;
let adminSelectedId = null;

function normalizeStore(s){
  const photos = Array.isArray(s.photos) ? s.photos.filter(Boolean).slice(0,4) : (s.photo ? [s.photo] : []);
  const casts = Array.isArray(s.casts) ? s.casts.filter(c=>c && c.name).slice(0,12).map(c=>({name:String(c.name), catch:String(c.catch||''), photo:String(c.photo||'')})) : [];
  return Object.assign({}, s, { photos, casts });
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
    ? `<img src="${esc(photos[0])}" alt="${esc(store.name)}" id="gallery-main-img">`
    : `<span>${esc(initial)}</span>`;
  const thumbs = photos.length > 1
    ? `<div class="thumb-row">${photos.map((p,i)=>`
        <button type="button" class="thumb ${i===0?'active':''}" onclick="setGalleryPhoto(${i}, this)">
          <img src="${esc(p)}" alt="${esc(store.name)} 写真${i+1}">
        </button>
      `).join('')}</div>`
    : '';
  return `<div class="detail-photo">${mainInner}</div>${thumbs}`;
}
function setGalleryPhoto(idx, btn){
  const src = currentGalleryPhotos[idx];
  const mainImg = document.getElementById('gallery-main-img');
  if(mainImg && src) mainImg.src = src;
  document.querySelectorAll('.thumb-row .thumb').forEach(el=>el.classList.remove('active'));
  if(btn) btn.classList.add('active');
}
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

/* ---------------- popular areas / tag presets (admin-managed) ---------------- */
const DEFAULT_AREAS = ['銀座','六本木','西麻布','新宿・歌舞伎町','赤坂','渋谷','恵比寿','新橋','池袋'];
let POPULAR_AREAS = DEFAULT_AREAS.slice();

const GENRE_LIST = ['キャバクラ','ラウンジ','クラブ','ガールズバー','スナック','コンカフェ','ニュークラブ','ダイニングバー','その他'];

const DEFAULT_TAG_PRESETS = ['初回割引あり','個室あり','会員制','送り可','カラオケあり','VIPルームあり','シャンパンコールあり','女性一人でも安心','明朗会計','アットホーム','常連多数','写真撮影OK','学生歓迎','ノンアルコールあり','接待利用に人気','要予約','食事充実','飲み放題あり','二次会利用OK','英語対応可','外国人スタッフ在籍','カジュアル利用OK'];
let TAG_PRESETS = DEFAULT_TAG_PRESETS.slice();

async function loadAreas(){
  const v = await loadConfigValue('areas');
  if(v){ POPULAR_AREAS = v; return; }
  POPULAR_AREAS = DEFAULT_AREAS.slice();
  try{ await saveConfigValue('areas', POPULAR_AREAS); }catch(e){}
}
async function saveAreas(){ return await saveConfigValue('areas', POPULAR_AREAS); }

async function loadTagPresets(){
  const v = await loadConfigValue('tagPresets');
  if(v){ TAG_PRESETS = v; return; }
  TAG_PRESETS = DEFAULT_TAG_PRESETS.slice();
  try{ await saveConfigValue('tagPresets', TAG_PRESETS); }catch(e){}
}
async function saveTagPresets(){ return await saveConfigValue('tagPresets', TAG_PRESETS); }

function renderQuickFilters(){
  const gWrap = document.getElementById('genre-icons');
  gWrap.innerHTML = GENRE_LIST.map(g => `
    <button type="button" class="quick-chip" data-genre="${esc(g)}" onclick="toggleGenreFilter('${esc(g)}')">
      <span class="circle">${GENRE_ICONS[g]}</span>
      <span class="label">${esc(g)}</span>
    </button>
  `).join('');

  const aWrap = document.getElementById('area-icons');
  aWrap.innerHTML = POPULAR_AREAS.map(a => `
    <button type="button" class="quick-chip" data-area="${esc(a)}" onclick="toggleAreaFilter('${esc(a)}')">
      <span class="circle">${pinIcon()}</span>
      <span class="label">${esc(a)}</span>
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
  sel.value = (sel.value === a) ? '' : a;
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
}

/* ---------------- home / search ---------------- */
function populateFilterOptions(){
  const areas = [...new Set(STORES.map(s=>s.area))].sort();
  const genres = [...new Set(STORES.map(s=>s.genre))].sort();
  const areaSel = document.getElementById('f-area');
  const genreSel = document.getElementById('f-genre');
  areaSel.innerHTML = '<option value="">すべて</option>' + areas.map(a=>`<option value="${esc(a)}">${esc(a)}</option>`).join('');
  genreSel.innerHTML = '<option value="">すべて</option>' + genres.map(g=>`<option value="${esc(g)}">${esc(g)}</option>`).join('');
}

function wageNumber(store){
  const m = (store.wage||'').match(/[\d,]+/);
  return m ? parseInt(m[0].replace(/,/g,''),10) : 0;
}

function applyFilters(){
  const kw = document.getElementById('f-keyword').value.trim().toLowerCase();
  const area = document.getElementById('f-area').value;
  const genre = document.getElementById('f-genre').value;
  const sort = document.getElementById('f-sort').value;

  let list = STORES.filter(s=>{
    if(area && s.area !== area) return false;
    if(genre && s.genre !== genre) return false;
    if(kw){
      const hay = [s.name, s.area, s.genre, s.catch, (s.tags||[]).join(' ')].join(' ').toLowerCase();
      if(!hay.includes(kw)) return false;
    }
    return true;
  });

  if(sort === 'budget-asc') list = list.slice().sort((a,b)=> wageNumber(a)-wageNumber(b));
  else if(sort === 'name') list = list.slice().sort((a,b)=> a.name.localeCompare(b.name,'ja'));
  else if(sort === 'distance' && userLocation) list = list.slice().sort((a,b)=> distanceForStore(a) - distanceForStore(b));

  syncQuickChips();
  renderGrid(list, sort === 'distance' && !!userLocation);
}

function renderGrid(list, showDistance){
  const grid = document.getElementById('store-grid');
  document.getElementById('result-count').textContent = list.length;
  if(list.length === 0){
    grid.innerHTML = `<div class="empty"><span class="serif">該当するお店が見つかりませんでした</span>キーワードやエリアを変えて、もう一度検索してみてください。</div>`;
    return;
  }
  grid.innerHTML = list.map(s => `
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
  `).join('');
}

/* ---------------- detail ---------------- */
function mapUrl(s){
  const q = s.address ? s.address : `${s.name} ${s.area}`;
  return `https://www.google.com/maps/search/?api=1&query=${encodeURIComponent(q)}`;
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
    <div class="desc">${esc(s.description || 'この店舗の詳細情報は準備中です。')}</div>

    <div class="section-title">在籍キャスト</div>
    ${castsHtml(s)}

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

/* ---------------- admin ---------------- */
function emptyStoreDraft(){
  return { id:'', name:'', area:'', genre:'キャバクラ', catch:'', wage:'', tags:[], photos:[], casts:[], instagram:'', tiktok:'', lineUrl:'', phone:'', email:'', address:'', hours:'', closedDay:'', description:'' };
}

/* ---- photo upload (drag & drop / click to browse, up to 3 per store) ---- */
let adminPhotoDraft = ['', '', '', ''];

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
        ${src ? `<button type="button" class="photo-remove" onclick="event.stopPropagation(); removePhoto(${i})">削除</button>` : `<span class="photo-slot-label">写真${i+1}${i===0?'（メイン）':''}</span>`}
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

function areaOptionsHtml(currentArea){
  let list = POPULAR_AREAS.slice();
  if(currentArea && !list.includes(currentArea)) list = [currentArea, ...list];
  if(list.length===0) return `<option value="">（エリアが未登録です。下の「人気エリアの管理」から追加してください）</option>`;
  return list.map(a=>`<option value="${esc(a)}" ${a===currentArea?'selected':''}>${esc(a)}</option>`).join('');
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
    <span class="manager-chip">${esc(a)}<button type="button" class="chip-x" onclick="handleDeleteArea('${esc(a)}')" title="削除">×</button></span>
  `).join('');
}

async function handleAddArea(){
  const input = document.getElementById('new-area-input');
  const v = input.value.trim();
  if(!v){ showToast('エリア名を入力してください'); return; }
  if(POPULAR_AREAS.includes(v)){ showToast('すでに登録されています'); return; }
  POPULAR_AREAS.push(v);
  await saveAreas();
  input.value = '';
  renderAreaManager();
  renderQuickFilters();
  syncQuickChips();
  showToast(`「${v}」を追加しました`);
}

async function handleDeleteArea(a){
  POPULAR_AREAS = POPULAR_AREAS.filter(x => x !== a);
  await saveAreas();
  renderAreaManager();
  renderQuickFilters();
  syncQuickChips();
  const areaSel = document.getElementById('af-area');
  if(areaSel) areaSel.innerHTML = areaOptionsHtml(areaSel.value);
  showToast(`「${a}」を削除しました`);
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
  await saveTagPresets();
  input.value = '';
  renderTagManager();
  const chipsWrap = document.getElementById('tag-preset-chips');
  const tagsInput = document.getElementById('af-tags');
  if(chipsWrap && tagsInput) chipsWrap.innerHTML = renderTagChipsHtml(tagsInput.value);
  showToast(`「${v}」を追加しました`);
}

async function handleDeleteTagPreset(t){
  TAG_PRESETS = TAG_PRESETS.filter(x => x !== t);
  await saveTagPresets();
  renderTagManager();
  const chipsWrap = document.getElementById('tag-preset-chips');
  const tagsInput = document.getElementById('af-tags');
  if(chipsWrap && tagsInput) chipsWrap.innerHTML = renderTagChipsHtml(tagsInput.value);
  showToast(`「${t}」を削除しました`);
}

function renderAdmin(){
  const el = document.getElementById('admin-content');
  if(!adminUnlocked){
    el.innerHTML = `
      <div class="admin-gate">
        <span class="serif">アドミンログイン</span>
        <div style="color:var(--text-muted); font-size:12.5px; line-height:1.8;">店舗情報の編集にはパスコードが必要です</div>
        <input type="password" id="admin-pass-input" placeholder="パスコードを入力">
        <button class="btn-search" style="width:100%;" onclick="tryAdminLogin()">ログイン</button>
        <div class="hint">デモ用パスコード：yorupass2026</div>
      </div>`;
    return;
  }
  const selected = STORES.find(s=>s.id===adminSelectedId) || null;
  el.innerHTML = `
    <div class="admin-header">
      <h1>掲載店舗の管理</h1>
      <a class="btn-ghost" onclick="go('home')">サイトを見る</a>
    </div>

    <div class="manager-card">
      <h3>人気エリアの管理</h3>
      <div class="field-hint">ホーム画面の「人気エリアから探す」に表示され、店舗登録時のエリア選択肢にもなります。</div>
      <div class="manager-chips" id="area-manager-list"></div>
      <div class="manager-add-row">
        <input type="text" id="new-area-input" placeholder="新しいエリア名（例：北新地）">
        <button type="button" class="btn-manager-add" onclick="handleAddArea()">追加</button>
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
        <div class="admin-list" id="admin-list"></div>
        <button class="admin-add" onclick="selectAdminStore(null,true)">＋ 新しい店舗を追加</button>
      </div>
      <div id="admin-form-wrap"></div>
    </div>
  `;
  renderAdminList();
  renderAdminForm(selected);
  renderAreaManager();
  renderTagManager();
}

function tryAdminLogin(){
  const v = document.getElementById('admin-pass-input').value;
  if(v === ADMIN_PASS){
    adminUnlocked = true;
    renderAdmin();
  }else{
    showToast('パスコードが違います');
  }
}

function renderAdminList(){
  const list = document.getElementById('admin-list');
  if(STORES.length===0){ list.innerHTML = `<div style="padding:20px; color:var(--text-faint); font-size:13px;">店舗がまだ登録されていません</div>`; return; }
  list.innerHTML = STORES.map(s=>`
    <div class="admin-row ${s.id===adminSelectedId?'active':''}" onclick="selectAdminStore('${s.id}')">
      <div>
        <div class="rn">${esc(s.name)}</div>
        <div class="ra">${esc(s.area)} ・ ${esc(s.genre)}</div>
      </div>
      <span class="del" onclick="event.stopPropagation(); deleteStore('${s.id}')">削除</span>
    </div>
  `).join('');
}

function selectAdminStore(id, isNew){
  adminSelectedId = isNew ? null : id;
  renderAdminList();
  renderAdminForm(isNew ? emptyStoreDraft() : STORES.find(s=>s.id===id));
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
  wrap.innerHTML = `
    <div class="admin-form">
      <h3>${isNew ? '新規店舗を追加' : '店舗情報を編集：'+esc(store.name)}</h3>
      <div class="form-grid">
        <div><label>店舗名</label><input id="af-name" value="${esc(store.name)}"></div>
        <div><label>業態</label>
          <select id="af-genre">
            ${GENRE_LIST.map(g=>`<option ${store.genre===g?'selected':''}>${g}</option>`).join('')}
          </select>
        </div>
        <div><label>エリア</label>
          <select id="af-area" size="6" class="scroll-select">
            ${areaOptionsHtml(store.area)}
          </select>
          <div class="field-hint">登録済みの人気エリアからスクロールして選択します（下の「人気エリアの管理」から追加できます）</div>
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
          <label>店舗写真（最大4枚）</label>
          <div class="photo-slots" id="photo-slots"></div>
          <div class="field-hint">クリック、またはドラッグ＆ドロップで画像をアップロードできます。1枚目が一覧・詳細ページのメイン写真になります。</div>
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
        <div class="full"><label>店舗紹介文</label><textarea id="af-desc" placeholder="お店の雰囲気、こだわり、こんなシーンにおすすめ...等">${esc(store.description)}</textarea></div>
      </div>
      <div class="form-actions">
        <button class="btn-save" onclick="saveAdminForm('${isNew?'':store.id}')">保存する</button>
        <span class="save-flag" id="save-flag">保存しました</span>
      </div>
    </div>
  `;
  renderPhotoSlots();
  renderCastRows();
}

async function saveAdminForm(existingId){
  const draft = {
    id: existingId || ('s' + Date.now()),
    name: document.getElementById('af-name').value.trim() || '無題の店舗',
    genre: document.getElementById('af-genre').value,
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
    description: document.getElementById('af-desc').value.trim(),
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

/* ---------------- boot ---------------- */
(async function init(){
  document.getElementById('store-grid').innerHTML = `<div class="empty"><span class="serif">読み込み中...</span></div>`;
  await Promise.all([loadStores(), loadAreas(), loadTagPresets()]);
  populateFilterOptions();
  renderQuickFilters();
  applyFilters();
  document.getElementById('f-keyword').addEventListener('keydown', e=>{ if(e.key==='Enter') applyFilters(); });
})();

</script>
</body>
</html>
