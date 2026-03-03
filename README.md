<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>FilmLog</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0a0f;
    --surface: #111118;
    --surface2: #18181f;
    --border: #2a2a35;
    --gold: #c9a84c;
    --gold-dim: #7a6230;
    --red: #e05252;
    --text: #e8e8ee;
    --text-dim: #7a7a8a;
    --text-muted: #44444f;
    --radius: 14px;
    --safe-top: env(safe-area-inset-top, 0px);
    --safe-bottom: env(safe-area-inset-bottom, 0px);
  }

- { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }

body {
font-family: ‘DM Sans’, sans-serif;
background: var(–bg);
color: var(–text);
min-height: 100dvh;
overflow-x: hidden;
}

/* –– TOP BAR –– */
.topbar {
position: fixed; top: 0; left: 0; right: 0; z-index: 100;
padding: calc(var(–safe-top) + 12px) 20px 12px;
background: linear-gradient(to bottom, #0a0a0f 60%, transparent);
display: flex; align-items: center; justify-content: space-between;
}
.logo {
font-family: ‘Playfair Display’, serif;
font-size: 22px; font-weight: 900; letter-spacing: -0.5px;
color: var(–gold);
}
.logo span { color: var(–text); }
.topbar-actions { display: flex; gap: 10px; }
.icon-btn {
width: 40px; height: 40px; border-radius: 50%;
background: var(–surface2); border: 1px solid var(–border);
display: flex; align-items: center; justify-content: center;
cursor: pointer; color: var(–text); font-size: 18px;
transition: all .2s;
}
.icon-btn:active { transform: scale(0.92); background: var(–border); }

/* –– MAIN CONTENT –– */
.content {
padding: calc(var(–safe-top) + 70px) 0 calc(var(–safe-bottom) + 80px);
min-height: 100dvh;
}

/* –– STATS BAR –– */
.stats-bar {
display: flex; gap: 10px;
padding: 0 16px 20px;
overflow-x: auto; scrollbar-width: none;
}
.stats-bar::-webkit-scrollbar { display: none; }
.stat-chip {
flex-shrink: 0;
background: var(–surface);
border: 1px solid var(–border);
border-radius: 100px;
padding: 8px 16px;
font-size: 13px;
color: var(–text-dim);
}
.stat-chip b { color: var(–gold); font-weight: 500; margin-right: 4px; }

/* –– FILTER/SORT ROW –– */
.filter-row {
display: flex; gap: 8px;
padding: 0 16px 16px;
overflow-x: auto; scrollbar-width: none;
}
.filter-row::-webkit-scrollbar { display: none; }
.pill {
flex-shrink: 0;
padding: 7px 14px; border-radius: 100px;
font-size: 13px; font-weight: 500; cursor: pointer;
border: 1px solid var(–border);
background: transparent; color: var(–text-dim);
transition: all .2s;
}
.pill.active { background: var(–gold); border-color: var(–gold); color: #0a0a0f; }
.pill:active { transform: scale(0.95); }

/* –– SORT SELECT –– */
.sort-row {
display: flex; align-items: center; gap: 8px;
padding: 0 16px 16px;
}
.sort-label { font-size: 13px; color: var(–text-muted); }
.sort-select {
background: var(–surface2); border: 1px solid var(–border);
border-radius: 8px; color: var(–text);
padding: 6px 10px; font-size: 13px; font-family: inherit;
cursor: pointer; outline: none;
}

/* –– FILM GRID –– */
.film-grid {
display: grid;
grid-template-columns: repeat(2, 1fr);
gap: 12px;
padding: 0 16px;
}

.film-card {
background: var(–surface);
border: 1px solid var(–border);
border-radius: var(–radius);
overflow: hidden;
cursor: pointer;
transition: transform .2s, border-color .2s;
position: relative;
}
.film-card:active { transform: scale(0.97); }
.film-card.highlighted { border-color: var(–gold); }

.film-poster {
width: 100%; aspect-ratio: 2/3;
object-fit: cover;
background: var(–surface2);
display: block;
}
.film-poster-placeholder {
width: 100%; aspect-ratio: 2/3;
background: var(–surface2);
display: flex; align-items: center; justify-content: center;
font-size: 40px; color: var(–text-muted);
}

.film-info { padding: 10px; }
.film-title {
font-family: ‘Playfair Display’, serif;
font-size: 14px; font-weight: 700;
line-height: 1.3;
margin-bottom: 4px;
display: -webkit-box;
-webkit-line-clamp: 2;
-webkit-box-orient: vertical;
overflow: hidden;
}
.film-year { font-size: 12px; color: var(–text-dim); margin-bottom: 6px; }

.film-rating {
display: flex; align-items: center; gap: 4px;
font-size: 13px; font-weight: 500;
}
.stars { color: var(–gold); letter-spacing: -1px; }
.stars .empty { color: var(–text-muted); }

.film-badges {
display: flex; flex-wrap: wrap; gap: 4px; margin-top: 6px;
}
.badge {
font-size: 10px; font-weight: 500;
padding: 3px 7px; border-radius: 100px;
background: var(–surface2); color: var(–text-dim);
border: 1px solid var(–border);
}
.badge.format { color: var(–gold); border-color: var(–gold-dim); }
.badge.rewatch { color: #7ec8a0; border-color: #2d5c42; }
.badge.date { color: var(–text-muted); font-size: 10px; }

.film-date { font-size: 11px; color: var(–text-muted); margin-top: 4px; }

/* –– BOTTOM NAV –– */
.bottom-nav {
position: fixed; bottom: 0; left: 0; right: 0; z-index: 100;
padding: 10px 0 calc(var(–safe-bottom) + 10px);
background: var(–surface);
border-top: 1px solid var(–border);
display: flex; justify-content: space-around;
}
.nav-item {
display: flex; flex-direction: column; align-items: center; gap: 3px;
cursor: pointer; color: var(–text-muted); font-size: 10px;
transition: color .2s;
padding: 4px 20px;
}
.nav-item.active { color: var(–gold); }
.nav-item svg { width: 22px; height: 22px; }
.nav-item:active { transform: scale(0.9); }

/* –– FAB –– */
.fab {
position: fixed; bottom: calc(var(–safe-bottom) + 70px); right: 20px; z-index: 99;
width: 56px; height: 56px; border-radius: 50%;
background: var(–gold);
box-shadow: 0 4px 20px rgba(201,168,76,0.4);
display: flex; align-items: center; justify-content: center;
cursor: pointer; font-size: 26px; color: #0a0a0f;
transition: transform .2s, box-shadow .2s;
}
.fab:active { transform: scale(0.92); box-shadow: 0 2px 10px rgba(201,168,76,0.3); }

/* –– MODAL OVERLAY –– */
.overlay {
position: fixed; inset: 0; z-index: 200;
background: rgba(0,0,0,0.75);
backdrop-filter: blur(4px);
display: flex; align-items: flex-end;
opacity: 0; pointer-events: none;
transition: opacity .3s;
}
.overlay.open { opacity: 1; pointer-events: all; }

.sheet {
background: var(–surface);
border-radius: 20px 20px 0 0;
width: 100%;
max-height: 94dvh;
overflow-y: auto;
transform: translateY(100%);
transition: transform .35s cubic-bezier(.32,.72,0,1);
padding-bottom: calc(var(–safe-bottom) + 20px);
}
.overlay.open .sheet { transform: translateY(0); }

.sheet-handle {
width: 40px; height: 4px; border-radius: 2px;
background: var(–border);
margin: 12px auto 4px;
}

.sheet-title {
font-family: ‘Playfair Display’, serif;
font-size: 22px; font-weight: 700;
padding: 12px 20px 16px;
}

/* –– SEARCH BOX –– */
.search-wrap { padding: 0 16px 16px; position: relative; }
.search-input {
width: 100%;
background: var(–surface2);
border: 1px solid var(–border);
border-radius: 12px;
padding: 12px 16px 12px 44px;
font-size: 16px; color: var(–text); font-family: inherit;
outline: none;
transition: border-color .2s;
}
.search-input:focus { border-color: var(–gold); }
.search-input::placeholder { color: var(–text-muted); }
.search-icon {
position: absolute; left: 28px; top: 50%;
transform: translateY(-50%);
color: var(–text-muted); font-size: 18px;
}

/* –– SEARCH RESULTS –– */
.search-results { padding: 0 16px; }
.search-result-item {
display: flex; gap: 12px; align-items: flex-start;
padding: 12px 0; border-bottom: 1px solid var(–border);
cursor: pointer;
}
.search-result-item:last-child { border-bottom: none; }
.result-thumb {
width: 50px; height: 75px; border-radius: 8px;
object-fit: cover; background: var(–surface2); flex-shrink: 0;
}
.result-info { flex: 1; }
.result-title { font-weight: 500; font-size: 15px; margin-bottom: 4px; }
.result-year { font-size: 13px; color: var(–text-dim); margin-bottom: 4px; }
.result-overview {
font-size: 12px; color: var(–text-muted);
display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden;
}

/* –– FORM FIELDS –– */
.form-section { padding: 0 20px 16px; }
.field-label { font-size: 13px; color: var(–text-dim); margin-bottom: 8px; font-weight: 500; }
.field-input {
width: 100%;
background: var(–surface2); border: 1px solid var(–border);
border-radius: 10px; padding: 12px 14px;
font-size: 15px; color: var(–text); font-family: inherit;
outline: none; transition: border-color .2s;
}
.field-input:focus { border-color: var(–gold); }

/* –– STAR RATING –– */
.star-row {
display: flex; gap: 8px; justify-content: center;
padding: 8px 0;
}
.star-btn {
font-size: 32px; cursor: pointer; transition: transform .15s;
color: var(–text-muted);
background: none; border: none;
}
.star-btn.lit { color: var(–gold); }
.star-btn:active { transform: scale(1.3); }

/* –– FORMAT PILLS –– */
.format-grid {
display: flex; flex-wrap: wrap; gap: 8px;
}
.format-pill {
padding: 8px 16px; border-radius: 100px;
border: 1px solid var(–border);
font-size: 13px; cursor: pointer; color: var(–text-dim);
transition: all .2s; background: transparent;
}
.format-pill.active {
background: rgba(201,168,76,0.15);
border-color: var(–gold); color: var(–gold);
}

/* –– DATE FIELDS –– */
.date-row { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }

/* –– SUBMIT BTN –– */
.submit-btn {
margin: 8px 20px 0;
width: calc(100% - 40px);
background: var(–gold); color: #0a0a0f;
border: none; border-radius: 14px;
padding: 16px; font-size: 16px; font-weight: 600;
font-family: inherit; cursor: pointer;
transition: opacity .2s, transform .2s;
}
.submit-btn:active { opacity: 0.85; transform: scale(0.98); }

/* –– DETAIL SHEET –– */
.detail-poster {
width: 100%; aspect-ratio: 16/9;
object-fit: cover;
background: var(–surface2);
}
.detail-poster-wrap {
position: relative;
}
.detail-poster-overlay {
position: absolute; inset: 0;
background: linear-gradient(to bottom, transparent 40%, var(–surface) 100%);
}
.detail-body { padding: 0 20px; }
.detail-title {
font-family: ‘Playfair Display’, serif;
font-size: 26px; font-weight: 900;
line-height: 1.2; margin-bottom: 4px;
}
.detail-meta { font-size: 13px; color: var(–text-dim); margin-bottom: 16px; }
.detail-overview { font-size: 14px; color: var(–text-dim); line-height: 1.6; margin-bottom: 20px; }

.detail-section-title {
font-size: 11px; font-weight: 600; letter-spacing: 1.5px;
text-transform: uppercase; color: var(–text-muted);
margin-bottom: 10px;
}
.detail-row { display: flex; gap: 8px; align-items: center; margin-bottom: 8px; }
.detail-icon { color: var(–gold); width: 18px; }

.action-row { display: flex; gap: 10px; margin-top: 16px; margin-bottom: 16px; }
.action-btn {
flex: 1; padding: 12px; border-radius: 12px;
border: 1px solid var(–border); background: var(–surface2);
color: var(–text); font-family: inherit; font-size: 13px; font-weight: 500;
cursor: pointer; transition: all .2s;
}
.action-btn.danger { border-color: var(–red); color: var(–red); }
.action-btn:active { transform: scale(0.97); }

/* –– EMPTY STATE –– */
.empty-state {
display: flex; flex-direction: column; align-items: center;
padding: 60px 40px; text-align: center; gap: 12px;
}
.empty-icon { font-size: 60px; opacity: 0.3; }
.empty-title { font-family: ‘Playfair Display’, serif; font-size: 20px; color: var(–text-dim); }
.empty-sub { font-size: 14px; color: var(–text-muted); }

/* –– LOADING –– */
.loader {
display: flex; justify-content: center; padding: 20px;
}
.spinner {
width: 28px; height: 28px; border-radius: 50%;
border: 3px solid var(–border);
border-top-color: var(–gold);
animation: spin .7s linear infinite;
}
@keyframes spin { to { transform: rotate(360deg); } }

/* –– DIVIDER –– */
.divider { height: 1px; background: var(–border); margin: 4px 0 16px; }

/* — TOAST — */
.toast {
position: fixed; top: calc(var(–safe-top) + 70px); left: 50%; z-index: 999;
transform: translateX(-50%) translateY(-20px);
background: var(–surface2); border: 1px solid var(–border);
border-radius: 100px; padding: 10px 20px;
font-size: 14px; color: var(–text);
opacity: 0; transition: all .3s;
white-space: nowrap;
pointer-events: none;
}
.toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }

/* REWATCH SECTION */
.rewatch-toggle {
display: flex; align-items: center; justify-content: space-between;
padding: 12px 14px;
background: var(–surface2); border: 1px solid var(–border);
border-radius: 10px; cursor: pointer;
}
.toggle-switch {
width: 44px; height: 26px; border-radius: 13px;
background: var(–border); position: relative;
transition: background .2s;
}
.toggle-switch.on { background: var(–gold); }
.toggle-knob {
position: absolute; top: 3px; left: 3px;
width: 20px; height: 20px; border-radius: 50%;
background: white; transition: transform .2s;
box-shadow: 0 1px 4px rgba(0,0,0,0.3);
}
.toggle-switch.on .toggle-knob { transform: translateX(18px); }

.rewatch-fields { display: none; margin-top: 12px; }
.rewatch-fields.visible { display: block; }

/* PROFILE / STATS PAGE */
.page { display: none; }
.page.active { display: block; }

.section-header {
padding: 4px 16px 12px;
font-family: ‘Playfair Display’, serif;
font-size: 18px; font-weight: 700;
}

.stats-card {
margin: 0 16px 12px;
background: var(–surface);
border: 1px solid var(–border);
border-radius: var(–radius);
padding: 16px 20px;
}
.stats-big { font-size: 48px; font-weight: 700; font-family: ‘Playfair Display’, serif; color: var(–gold); }
.stats-sub { font-size: 13px; color: var(–text-dim); margin-top: 2px; }

.stats-row { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin: 0 16px 12px; }
.stats-mini { background: var(–surface); border: 1px solid var(–border); border-radius: 12px; padding: 14px; }
.stats-mini-val { font-size: 28px; font-weight: 700; font-family: ‘Playfair Display’, serif; color: var(–text); }
.stats-mini-label { font-size: 12px; color: var(–text-dim); margin-top: 2px; }

.top-films-list { margin: 0 16px; }
.top-film-item {
display: flex; gap: 12px; align-items: center;
padding: 10px 0; border-bottom: 1px solid var(–border);
}
.top-rank { font-size: 20px; font-family: ‘Playfair Display’, serif; font-weight: 700; color: var(–gold); width: 28px; }
.top-thumb { width: 40px; height: 60px; border-radius: 6px; object-fit: cover; background: var(–surface2); flex-shrink: 0; }
.top-info { flex: 1; }
.top-title { font-size: 14px; font-weight: 500; }
.top-meta { font-size: 12px; color: var(–text-dim); }

/* WATCHLIST */
.watchlist-item {
display: flex; gap: 12px; align-items: center;
padding: 12px 16px; border-bottom: 1px solid var(–border);
cursor: pointer;
}
.watchlist-thumb { width: 44px; height: 66px; border-radius: 8px; object-fit: cover; background: var(–surface2); flex-shrink: 0; }
.watchlist-info { flex: 1; }
.watchlist-title { font-size: 15px; font-weight: 500; margin-bottom: 2px; }
.watchlist-year { font-size: 12px; color: var(–text-dim); }
.watchlist-remove { color: var(–text-muted); font-size: 20px; padding: 8px; cursor: pointer; }
</style>

</head>
<body>

<!-- TOP BAR -->

<div class="topbar">
  <div class="logo">Film<span>Log</span></div>
  <div class="topbar-actions">
    <div class="icon-btn" id="searchTopBtn">🔍</div>
  </div>
</div>

<!-- TOAST -->

<div class="toast" id="toast"></div>

<!-- PAGES -->

<div class="content">

  <!-- PAGE: WATCHED -->

  <div class="page active" id="pageWatched">
    <div class="stats-bar" id="statsBar"></div>
    <div class="filter-row" id="filterRow">
      <button class="pill active" data-filter="all">Все</button>
      <button class="pill" data-filter="5">★★★★★</button>
      <button class="pill" data-filter="4">★★★★</button>
      <button class="pill" data-filter="3">★★★</button>
      <button class="pill" data-filter="rewatch">Повтор</button>
    </div>
    <div class="sort-row">
      <span class="sort-label">Сортировка:</span>
      <select class="sort-select" id="sortSelect">
        <option value="date_desc">Дата ↓</option>
        <option value="date_asc">Дата ↑</option>
        <option value="rating_desc">Рейтинг ↓</option>
        <option value="rating_asc">Рейтинг ↑</option>
        <option value="title_asc">Название А-Я</option>
        <option value="title_desc">Название Я-А</option>
        <option value="year_desc">Год ↓</option>
      </select>
    </div>
    <div class="film-grid" id="filmGrid"></div>
  </div>

  <!-- PAGE: WATCHLIST -->

  <div class="page" id="pageWatchlist">
    <div class="section-header">Хочу посмотреть</div>
    <div id="watchlistContainer"></div>
  </div>

  <!-- PAGE: STATS -->

  <div class="page" id="pageStats">
    <div class="section-header">Статистика</div>
    <div id="statsContainer"></div>
  </div>

</div>

<!-- FAB -->

<div class="fab" id="fab">＋</div>

<!-- BOTTOM NAV -->

<div class="bottom-nav">
  <div class="nav-item active" data-page="pageWatched" id="navWatched">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8">
      <rect x="2" y="3" width="20" height="14" rx="2"/>
      <path d="M8 21h8M12 17v4"/>
    </svg>
    Просмотрено
  </div>
  <div class="nav-item" data-page="pageWatchlist" id="navWatchlist">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8">
      <path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/>
    </svg>
    Хочу
  </div>
  <div class="nav-item" data-page="pageStats" id="navStats">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8">
      <path d="M18 20V10M12 20V4M6 20v-6"/>
    </svg>
    Статистика
  </div>
</div>

<!-- === MODAL: ADD FILM === -->

<div class="overlay" id="addOverlay">
  <div class="sheet" id="addSheet">
    <div class="sheet-handle"></div>
    <div class="sheet-title" id="sheetTitle">Добавить фильм</div>

```
<!-- STEP 1: SEARCH -->
<div id="step1">
  <div class="search-wrap">
    <span class="search-icon">🔍</span>
    <input class="search-input" id="movieSearch" placeholder="Поиск фильма..." autocomplete="off">
  </div>
  <div id="searchLoader" class="loader" style="display:none"><div class="spinner"></div></div>
  <div class="search-results" id="searchResults"></div>
  <div style="padding:0 20px 16px">
    <div class="field-label">Или введите вручную</div>
    <input class="field-input" id="manualTitle" placeholder="Название фильма">
    <div style="height:10px"></div>
    <button class="submit-btn" onclick="selectManual()">Продолжить →</button>
  </div>
</div>

<!-- STEP 2: DETAILS -->
<div id="step2" style="display:none">
  <div style="display:flex;gap:12px;padding:0 20px 16px;align-items:flex-start">
    <img id="selectedPoster" style="width:70px;height:105px;border-radius:10px;object-fit:cover;background:var(--surface2)" src="" onerror="this.style.display='none'">
    <div>
      <div style="font-family:'Playfair Display',serif;font-size:18px;font-weight:700" id="selectedTitle"></div>
      <div style="font-size:13px;color:var(--text-dim);margin-top:4px" id="selectedYear"></div>
      <div style="font-size:12px;color:var(--text-muted);margin-top:4px;line-height:1.4" id="selectedOverview"></div>
    </div>
  </div>
  <div class="divider"></div>

  <!-- RATING -->
  <div class="form-section">
    <div class="field-label">Оценка</div>
    <div class="star-row" id="starRow">
      <button class="star-btn" data-val="1">★</button>
      <button class="star-btn" data-val="2">★</button>
      <button class="star-btn" data-val="3">★</button>
      <button class="star-btn" data-val="4">★</button>
      <button class="star-btn" data-val="5">★</button>
    </div>
  </div>

  <!-- WATCH DATE -->
  <div class="form-section">
    <div class="field-label">Дата просмотра</div>
    <input class="field-input" type="datetime-local" id="watchDate">
  </div>

  <!-- FORMAT -->
  <div class="form-section">
    <div class="field-label">Формат просмотра</div>
    <div class="format-grid" id="formatGrid">
      <button class="format-pill" data-fmt="Кинотеатр">🎬 Кинотеатр</button>
      <button class="format-pill" data-fmt="IMAX">🔭 IMAX</button>
      <button class="format-pill" data-fmt="4DX">🎪 4DX</button>
      <button class="format-pill" data-fmt="Blu-ray">💿 Blu-ray</button>
      <button class="format-pill" data-fmt="4K UHD">📀 4K UHD</button>
      <button class="format-pill" data-fmt="Стриминг">📱 Стриминг</button>
      <button class="format-pill" data-fmt="DVD">📼 DVD</button>
      <button class="format-pill" data-fmt="Скачал">⬇️ Скачал</button>
    </div>
  </div>

  <!-- NOTES -->
  <div class="form-section">
    <div class="field-label">Заметки (необязательно)</div>
    <input class="field-input" id="watchNotes" placeholder="Краткие впечатления...">
  </div>

  <!-- REWATCH -->
  <div class="form-section">
    <div class="field-label">Повторный просмотр</div>
    <div class="rewatch-toggle" onclick="toggleRewatch()">
      <span style="font-size:14px">Запланировать повтор</span>
      <div class="toggle-switch" id="rewatchToggle"><div class="toggle-knob"></div></div>
    </div>
    <div class="rewatch-fields" id="rewatchFields">
      <div style="height:10px"></div>
      <div class="field-label">Дата повтора</div>
      <input class="field-input" type="date" id="rewatchDate" style="margin-bottom:10px">
      <div class="field-label">Формат повтора</div>
      <div class="format-grid" id="rewatchFormatGrid">
        <button class="format-pill" data-fmt="Кинотеатр">🎬 Кинотеатр</button>
        <button class="format-pill" data-fmt="IMAX">🔭 IMAX</button>
        <button class="format-pill" data-fmt="4DX">🎪 4DX</button>
        <button class="format-pill" data-fmt="Blu-ray">💿 Blu-ray</button>
        <button class="format-pill" data-fmt="4K UHD">📀 4K UHD</button>
        <button class="format-pill" data-fmt="Стриминг">📱 Стриминг</button>
        <button class="format-pill" data-fmt="DVD">📼 DVD</button>
        <button class="format-pill" data-fmt="Скачал">⬇️ Скачал</button>
      </div>
    </div>
  </div>

  <button class="submit-btn" onclick="saveFilm()">Сохранить в журнал</button>
  <div style="height:10px"></div>
  <button class="action-btn" style="margin:0 20px;width:calc(100% - 40px)" onclick="goBackToSearch()">← Назад к поиску</button>
</div>
```

  </div>
</div>

<!-- === MODAL: DETAIL === -->

<div class="overlay" id="detailOverlay">
  <div class="sheet" id="detailSheet">
    <div class="sheet-handle"></div>
    <div id="detailContent"></div>
  </div>
</div>

<!-- === MODAL: TMDB KEY === -->

<div class="overlay" id="keyOverlay">
  <div class="sheet">
    <div class="sheet-handle"></div>
    <div class="sheet-title">🔑 TMDB API</div>
    <div style="padding:0 20px 16px;font-size:14px;color:var(--text-dim);line-height:1.6">
      Для поиска фильмов нужен бесплатный ключ TMDB.<br><br>
      1. Зарегистрируйтесь на <b style="color:var(--gold)">themoviedb.org</b><br>
      2. Перейдите в Settings → API<br>
      3. Скопируйте <b style="color:var(--gold)">API Read Access Token</b>
    </div>
    <div class="form-section">
      <input class="field-input" id="apiKeyInput" placeholder="Вставьте Bearer token здесь..." style="font-size:13px">
    </div>
    <button class="submit-btn" onclick="saveApiKey()">Сохранить и продолжить</button>
    <div style="height:10px"></div>
    <button class="action-btn" style="margin:0 20px;width:calc(100% - 40px)" onclick="closeKeyModal()">Без поиска (вводить вручную)</button>
  </div>
</div>

<script>
// ==================== STATE ====================
let films = JSON.parse(localStorage.getItem('filmlog_films') || '[]');
let watchlist = JSON.parse(localStorage.getItem('filmlog_watchlist') || '[]');
let tmdbKey = localStorage.getItem('filmlog_tmdb') || '';
let selectedFilmData = null;
let currentRating = 0;
let currentFormat = '';
let rewatchFormat = '';
let rewatchOn = false;
let activeFilter = 'all';
let currentDetailId = null;
let searchTimer = null;

// ==================== INIT ====================
document.addEventListener('DOMContentLoaded', () => {
  if (!tmdbKey) openKeyModal();
  renderAll();
  setupListeners();
  setDefaultDateTime();
});

function setDefaultDateTime() {
  const now = new Date();
  const pad = n => String(n).padStart(2,'0');
  const val = `${now.getFullYear()}-${pad(now.getMonth()+1)}-${pad(now.getDate())}T${pad(now.getHours())}:${pad(now.getMinutes())}`;
  document.getElementById('watchDate').value = val;
}

// ==================== RENDER ====================
function renderAll() {
  renderGrid();
  renderStatsBar();
  renderStats();
  renderWatchlist();
}

function getFilteredSorted() {
  let arr = [...films];
  if (activeFilter === 'rewatch') arr = arr.filter(f => f.rewatchDate);
  else if (activeFilter !== 'all') arr = arr.filter(f => f.rating == activeFilter);
  const sort = document.getElementById('sortSelect').value;
  arr.sort((a,b) => {
    if (sort === 'date_desc') return new Date(b.watchDate) - new Date(a.watchDate);
    if (sort === 'date_asc') return new Date(a.watchDate) - new Date(b.watchDate);
    if (sort === 'rating_desc') return (b.rating||0) - (a.rating||0);
    if (sort === 'rating_asc') return (a.rating||0) - (b.rating||0);
    if (sort === 'title_asc') return a.title.localeCompare(b.title, 'ru');
    if (sort === 'title_desc') return b.title.localeCompare(a.title, 'ru');
    if (sort === 'year_desc') return (b.year||0) - (a.year||0);
    return 0;
  });
  return arr;
}

function renderGrid() {
  const grid = document.getElementById('filmGrid');
  const arr = getFilteredSorted();
  if (!arr.length) {
    grid.innerHTML = `<div class="empty-state" style="grid-column:1/-1">
      <div class="empty-icon">🎬</div>
      <div class="empty-title">Пусто</div>
      <div class="empty-sub">Нажмите + чтобы добавить первый фильм</div>
    </div>`;
    return;
  }
  grid.innerHTML = arr.map(f => {
    const stars = [1,2,3,4,5].map(i => `<span class="${i <= f.rating ? '' : 'empty'}">★</span>`).join('');
    const dateStr = f.watchDate ? new Date(f.watchDate).toLocaleDateString('ru',{day:'numeric',month:'short',year:'numeric'}) : '';
    const poster = f.poster
      ? `<img class="film-poster" src="${f.poster}" loading="lazy" onerror="this.parentNode.innerHTML='<div class=film-poster-placeholder>🎬</div>'">`
      : `<div class="film-poster-placeholder">🎬</div>`;
    return `<div class="film-card" onclick="openDetail('${f.id}')">
      ${poster}
      <div class="film-info">
        <div class="film-title">${f.title}</div>
        <div class="film-year">${f.year || ''}</div>
        <div class="film-rating"><div class="stars">${stars}</div></div>
        <div class="film-badges">
          ${f.format ? `<span class="badge format">${f.format}</span>` : ''}
          ${f.rewatchDate ? `<span class="badge rewatch">↻ повтор</span>` : ''}
        </div>
        <div class="film-date">${dateStr}</div>
      </div>
    </div>`;
  }).join('');
}

function renderStatsBar() {
  const bar = document.getElementById('statsBar');
  const total = films.length;
  const avgRating = total ? (films.reduce((a,f)=>a+(f.rating||0),0)/total).toFixed(1) : 0;
  const rewatches = films.filter(f=>f.rewatchDate).length;
  bar.innerHTML = `
    <div class="stat-chip"><b>${total}</b> просмотрено</div>
    <div class="stat-chip"><b>${avgRating}</b> средняя оценка</div>
    <div class="stat-chip"><b>${rewatches}</b> повторов</div>
  `;
}

function renderStats() {
  const c = document.getElementById('statsContainer');
  const total = films.length;
  const avgRating = total ? (films.reduce((a,f)=>a+(f.rating||0),0)/total).toFixed(1) : '—';
  const rated5 = films.filter(f=>f.rating===5).length;
  const rewatches = films.filter(f=>f.rewatchDate).length;
  const formats = {};
  films.forEach(f => { if(f.format) formats[f.format] = (formats[f.format]||0)+1; });
  const topFormat = Object.entries(formats).sort((a,b)=>b[1]-a[1])[0];
  const topFilms = [...films].sort((a,b)=>(b.rating||0)-(a.rating||0)).slice(0,5);

  c.innerHTML = `
    <div class="stats-card">
      <div class="stats-big">${total}</div>
      <div class="stats-sub">фильмов просмотрено</div>
    </div>
    <div class="stats-row">
      <div class="stats-mini">
        <div class="stats-mini-val">${avgRating}</div>
        <div class="stats-mini-label">средняя оценка</div>
      </div>
      <div class="stats-mini">
        <div class="stats-mini-val">${rated5}</div>
        <div class="stats-mini-label">шедевров ★★★★★</div>
      </div>
      <div class="stats-mini">
        <div class="stats-mini-val">${rewatches}</div>
        <div class="stats-mini-label">повторных просмотров</div>
      </div>
      <div class="stats-mini">
        <div class="stats-mini-val">${topFormat ? topFormat[0] : '—'}</div>
        <div class="stats-mini-label">любимый формат</div>
      </div>
    </div>
    ${topFilms.length ? `
    <div class="section-header">Топ фильмов</div>
    <div class="top-films-list">
      ${topFilms.map((f,i) => {
        const stars = '★'.repeat(f.rating||0);
        const thumb = f.poster ? `<img class="top-thumb" src="${f.poster}" onerror="this.src=''">` : `<div class="top-thumb" style="display:flex;align-items:center;justify-content:center;font-size:20px">🎬</div>`;
        return `<div class="top-film-item">
          <div class="top-rank">${i+1}</div>
          ${thumb}
          <div class="top-info">
            <div class="top-title">${f.title}</div>
            <div class="top-meta">${f.year||''} · <span style="color:var(--gold)">${stars}</span></div>
          </div>
        </div>`;
      }).join('')}
    </div>` : ''}
  `;
}

function renderWatchlist() {
  const c = document.getElementById('watchlistContainer');
  if (!watchlist.length) {
    c.innerHTML = `<div class="empty-state">
      <div class="empty-icon">⭐</div>
      <div class="empty-title">Список пуст</div>
      <div class="empty-sub">Добавляйте фильмы которые хотите посмотреть</div>
    </div>`;
    return;
  }
  c.innerHTML = watchlist.map(f => {
    const thumb = f.poster
      ? `<img class="watchlist-thumb" src="${f.poster}" onerror="this.src=''">`
      : `<div class="watchlist-thumb" style="display:flex;align-items:center;justify-content:center;font-size:24px">🎬</div>`;
    return `<div class="watchlist-item">
      ${thumb}
      <div class="watchlist-info">
        <div class="watchlist-title">${f.title}</div>
        <div class="watchlist-year">${f.year||''}</div>
      </div>
      <div class="watchlist-remove" onclick="removeWatchlist('${f.id}',event)">✕</div>
    </div>`;
  }).join('');
}

// ==================== NAVIGATION ====================
function setupListeners() {
  document.querySelectorAll('.nav-item').forEach(item => {
    item.addEventListener('click', () => {
      const pageId = item.dataset.page;
      document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'));
      document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
      item.classList.add('active');
      document.getElementById(pageId).classList.add('active');
    });
  });

  document.getElementById('fab').addEventListener('click', openAddModal);
  document.getElementById('searchTopBtn').addEventListener('click', openAddModal);

  document.querySelectorAll('[data-filter]').forEach(btn => {
    btn.addEventListener('click', () => {
      activeFilter = btn.dataset.filter;
      document.querySelectorAll('[data-filter]').forEach(b=>b.classList.remove('active'));
      btn.classList.add('active');
      renderGrid();
    });
  });

  document.getElementById('sortSelect').addEventListener('change', renderGrid);

  // Close overlays on backdrop click
  ['addOverlay','detailOverlay'].forEach(id => {
    document.getElementById(id).addEventListener('click', e => {
      if (e.target.id === id) closeOverlay(id);
    });
  });

  // Stars
  document.querySelectorAll('#starRow .star-btn').forEach(btn => {
    btn.addEventListener('click', () => {
      currentRating = parseInt(btn.dataset.val);
      updateStars();
    });
  });

  // Format pills
  setupFormatPills('#formatGrid', v => currentFormat = v);
  setupFormatPills('#rewatchFormatGrid', v => rewatchFormat = v);

  // Search
  document.getElementById('movieSearch').addEventListener('input', e => {
    clearTimeout(searchTimer);
    const q = e.target.value.trim();
    if (q.length < 2) { document.getElementById('searchResults').innerHTML=''; return; }
    searchTimer = setTimeout(() => searchTMDB(q), 500);
  });
}

function setupFormatPills(selector, cb) {
  document.querySelectorAll(selector + ' .format-pill').forEach(pill => {
    pill.addEventListener('click', () => {
      const val = pill.dataset.fmt;
      document.querySelectorAll(selector + ' .format-pill').forEach(p=>p.classList.remove('active'));
      pill.classList.add('active');
      cb(val);
    });
  });
}

// ==================== MODALS ====================
function openOverlay(id) {
  const o = document.getElementById(id);
  o.classList.add('open');
  document.body.style.overflow = 'hidden';
}
function closeOverlay(id) {
  const o = document.getElementById(id);
  o.classList.remove('open');
  document.body.style.overflow = '';
}

function openAddModal() {
  resetAddForm();
  openOverlay('addOverlay');
}

function resetAddForm() {
  document.getElementById('step1').style.display = 'block';
  document.getElementById('step2').style.display = 'none';
  document.getElementById('movieSearch').value = '';
  document.getElementById('searchResults').innerHTML = '';
  document.getElementById('manualTitle').value = '';
  document.getElementById('watchNotes').value = '';
  currentRating = 0; currentFormat = ''; rewatchFormat = ''; rewatchOn = false;
  updateStars();
  document.querySelectorAll('.format-pill').forEach(p=>p.classList.remove('active'));
  document.getElementById('rewatchToggle').classList.remove('on');
  document.getElementById('rewatchFields').classList.remove('visible');
  document.getElementById('rewatchDate').value = '';
  document.getElementById('sheetTitle').textContent = 'Добавить фильм';
  setDefaultDateTime();
}

function goBackToSearch() {
  document.getElementById('step1').style.display = 'block';
  document.getElementById('step2').style.display = 'none';
}

function updateStars() {
  document.querySelectorAll('#starRow .star-btn').forEach(btn => {
    btn.classList.toggle('lit', parseInt(btn.dataset.val) <= currentRating);
  });
}

function toggleRewatch() {
  rewatchOn = !rewatchOn;
  document.getElementById('rewatchToggle').classList.toggle('on', rewatchOn);
  document.getElementById('rewatchFields').classList.toggle('visible', rewatchOn);
}

// ==================== TMDB SEARCH ====================
async function searchTMDB(query) {
  if (!tmdbKey) { showManualOnly(); return; }
  document.getElementById('searchLoader').style.display = 'flex';
  document.getElementById('searchResults').innerHTML = '';
  try {
    const res = await fetch(`https://api.themoviedb.org/3/search/movie?query=${encodeURIComponent(query)}&language=ru-RU&include_adult=false`, {
      headers: { Authorization: `Bearer ${tmdbKey}`, 'Content-Type': 'application/json' }
    });
    const data = await res.json();
    document.getElementById('searchLoader').style.display = 'none';
    if (!data.results || !data.results.length) {
      document.getElementById('searchResults').innerHTML = `<div style="padding:20px;text-align:center;color:var(--text-muted);font-size:14px">Ничего не найдено</div>`;
      return;
    }
    const items = data.results.slice(0,8).map(m => {
      const thumb = m.poster_path ? `<img class="result-thumb" src="https://image.tmdb.org/t/p/w185${m.poster_path}" loading="lazy">` : `<div class="result-thumb" style="display:flex;align-items:center;justify-content:center;font-size:24px;border-radius:8px;background:var(--surface2)">🎬</div>`;
      const year = m.release_date ? m.release_date.slice(0,4) : '';
      const overview = m.overview || '';
      return `<div class="search-result-item" onclick="selectMovie(${m.id})">
        ${thumb}
        <div class="result-info">
          <div class="result-title">${m.title}</div>
          <div class="result-year">${year}${m.original_title && m.original_title !== m.title ? ' · ' + m.original_title : ''}</div>
          <div class="result-overview">${overview}</div>
        </div>
      </div>`;
    });
    document.getElementById('searchResults').innerHTML = items.join('');
  } catch(e) {
    document.getElementById('searchLoader').style.display = 'none';
    document.getElementById('searchResults').innerHTML = `<div style="padding:20px;text-align:center;color:var(--text-muted);font-size:14px">Ошибка поиска. Проверьте API ключ.</div>`;
  }
}

async function selectMovie(tmdbId) {
  if (!tmdbKey) return;
  try {
    const res = await fetch(`https://api.themoviedb.org/3/movie/${tmdbId}?language=ru-RU`, {
      headers: { Authorization: `Bearer ${tmdbKey}` }
    });
    const m = await res.json();
    selectedFilmData = {
      tmdbId: m.id,
      title: m.title,
      originalTitle: m.original_title,
      year: m.release_date ? m.release_date.slice(0,4) : '',
      poster: m.poster_path ? `https://image.tmdb.org/t/p/w500${m.poster_path}` : '',
      backdrop: m.backdrop_path ? `https://image.tmdb.org/t/p/w780${m.backdrop_path}` : '',
      overview: m.overview || '',
      genres: (m.genres||[]).map(g=>g.name).join(', '),
      runtime: m.runtime,
      tmdbRating: m.vote_average
    };
    showStep2();
  } catch(e) { showToast('Ошибка загрузки данных'); }
}

function selectManual() {
  const title = document.getElementById('manualTitle').value.trim();
  if (!title) { showToast('Введите название'); return; }
  selectedFilmData = { title, year: '', poster: '', backdrop: '', overview: '', genres: '' };
  showStep2();
}

function showStep2() {
  const d = selectedFilmData;
  document.getElementById('selectedTitle').textContent = d.title;
  document.getElementById('selectedYear').textContent = [d.year, d.genres].filter(Boolean).join(' · ');
  document.getElementById('selectedOverview').textContent = d.overview.slice(0,120) + (d.overview.length > 120 ? '…' : '');
  const img = document.getElementById('selectedPoster');
  if (d.poster) { img.src = d.poster; img.style.display = 'block'; } else { img.style.display = 'none'; }
  document.getElementById('step1').style.display = 'none';
  document.getElementById('step2').style.display = 'block';
  document.getElementById('addSheet').scrollTop = 0;
}

// ==================== SAVE FILM ====================
function saveFilm() {
  if (!selectedFilmData) return;
  const d = selectedFilmData;
  const id = 'f' + Date.now();
  const film = {
    id,
    tmdbId: d.tmdbId,
    title: d.title,
    originalTitle: d.originalTitle,
    year: d.year,
    poster: d.poster,
    backdrop: d.backdrop,
    overview: d.overview,
    genres: d.genres,
    runtime: d.runtime,
    tmdbRating: d.tmdbRating,
    rating: currentRating,
    format: currentFormat,
    watchDate: document.getElementById('watchDate').value || new Date().toISOString(),
    notes: document.getElementById('watchNotes').value,
    rewatchDate: rewatchOn ? document.getElementById('rewatchDate').value : '',
    rewatchFormat: rewatchOn ? rewatchFormat : '',
    addedAt: new Date().toISOString()
  };
  films.unshift(film);
  save();
  closeOverlay('addOverlay');
  renderAll();
  showToast('✓ Фильм добавлен в журнал');
}

// ==================== DETAIL ====================
function openDetail(id) {
  currentDetailId = id;
  const f = films.find(x=>x.id===id);
  if (!f) return;
  renderDetail(f);
  openOverlay('detailOverlay');
}

function renderDetail(f) {
  const stars = [1,2,3,4,5].map(i=>`<span style="color:${i<=f.rating?'var(--gold)':'var(--text-muted)'}"">★</span>`).join('');
  const dateStr = f.watchDate ? new Date(f.watchDate).toLocaleString('ru',{day:'numeric',month:'long',year:'numeric',hour:'2-digit',minute:'2-digit'}) : '';
  const rewatchStr = f.rewatchDate ? new Date(f.rewatchDate).toLocaleDateString('ru',{day:'numeric',month:'long',year:'numeric'}) : '';

  const img = (f.backdrop || f.poster) ? `
    <div class="detail-poster-wrap">
      <img class="detail-poster" src="${f.backdrop || f.poster}" onerror="this.style.display='none'">
      <div class="detail-poster-overlay"></div>
    </div>` : '';

  document.getElementById('detailContent').innerHTML = `
    ${img}
    <div class="detail-body">
      <div class="detail-title">${f.title}</div>
      <div class="detail-meta">${[f.year, f.genres, f.runtime ? f.runtime+'мин' : ''].filter(Boolean).join(' · ')}</div>
      ${f.overview ? `<div class="detail-overview">${f.overview}</div>` : ''}
      
      <div class="detail-section-title">Просмотр</div>
      <div class="detail-row">
        <span class="detail-icon">★</span>
        <span style="font-size:18px">${stars}</span>
      </div>
      ${dateStr ? `<div class="detail-row"><span class="detail-icon">📅</span><span style="font-size:14px;color:var(--text-dim)">${dateStr}</span></div>` : ''}
      ${f.format ? `<div class="detail-row"><span class="detail-icon">🎬</span><span style="font-size:14px;color:var(--gold)">${f.format}</span></div>` : ''}
      ${f.notes ? `<div class="detail-row"><span class="detail-icon">📝</span><span style="font-size:14px;color:var(--text-dim)">${f.notes}</span></div>` : ''}

      ${rewatchStr ? `
      <div style="height:12px"></div>
      <div class="detail-section-title">Повторный просмотр</div>
      <div class="detail-row"><span class="detail-icon">🔄</span><span style="font-size:14px;color:var(--text-dim)">${rewatchStr}</span></div>
      ${f.rewatchFormat ? `<div class="detail-row"><span class="detail-icon">🎬</span><span style="font-size:14px;color:var(--gold)">${f.rewatchFormat}</span></div>` : ''}
      ` : ''}

      ${f.tmdbRating ? `
      <div style="height:12px"></div>
      <div class="detail-section-title">TMDB</div>
      <div class="detail-row"><span class="detail-icon">🌐</span><span style="font-size:14px;color:var(--text-dim)">Рейтинг: ${f.tmdbRating.toFixed(1)}</span></div>
      ` : ''}

      <div class="action-row">
        <button class="action-btn" onclick="addToWatchlistFromDetail()">+ В список желаний</button>
        <button class="action-btn danger" onclick="deleteFilm()">Удалить</button>
      </div>
    </div>
  `;
}

function deleteFilm() {
  films = films.filter(f=>f.id !== currentDetailId);
  save(); renderAll();
  closeOverlay('detailOverlay');
  showToast('Фильм удалён');
}

function addToWatchlistFromDetail() {
  const f = films.find(x=>x.id===currentDetailId);
  if (!f) return;
  if (watchlist.find(w=>w.tmdbId && w.tmdbId===f.tmdbId)) { showToast('Уже в списке желаний'); return; }
  watchlist.push({ id:'w'+Date.now(), tmdbId:f.tmdbId, title:f.title, year:f.year, poster:f.poster });
  save(); renderWatchlist();
  showToast('Добавлено в список желаний');
}

function removeWatchlist(id, e) {
  e.stopPropagation();
  watchlist = watchlist.filter(w=>w.id!==id);
  save(); renderWatchlist();
}

// ==================== API KEY ====================
function openKeyModal() { openOverlay('keyOverlay'); }
function saveApiKey() {
  const k = document.getElementById('apiKeyInput').value.trim();
  if (!k) { showToast('Введите ключ'); return; }
  tmdbKey = k;
  localStorage.setItem('filmlog_tmdb', k);
  closeOverlay('keyOverlay');
  showToast('✓ API ключ сохранён');
}
function closeKeyModal() { closeOverlay('keyOverlay'); }
function showManualOnly() {}

// ==================== UTILS ====================
function save() {
  localStorage.setItem('filmlog_films', JSON.stringify(films));
  localStorage.setItem('filmlog_watchlist', JSON.stringify(watchlist));
}

function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'), 2500);
}
</script>

</body>
</html>
