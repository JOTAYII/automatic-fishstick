<!doctype html>
<html lang="es">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>🎧 SpotiFake — Completo</title>
<style>
  :root{
    --green:#1db954;
    --bg1:#121212;
    --card:#181818;
    --muted:#9aa6b2;
  }
  *{box-sizing:border-box}
  body {
    font-family: "Inter", sans-serif;
    background: linear-gradient(180deg,var(--bg1),#000);
    color: #fff;
    margin: 0;
    min-height: 100vh;
  }
  header {
    background: var(--green);
    color: #000;
    padding: 16px 24px;
    font-weight: bold;
    font-size: 22px;
    letter-spacing: 0.5px;
    display:flex;
    align-items:center;
    justify-content:space-between;
  }
  .container {
    display: grid;
    grid-template-columns: 260px 1fr;
    gap: 16px;
    padding: 16px;
    height: calc(100vh - 68px);
  }
  nav {
    background: #181818;
    padding: 16px;
    overflow-y: auto;
    border-radius: 10px;
    border-right: 1px solid #222;
  }
  nav h3 {
    font-size: 14px;
    color: var(--muted);
    margin-top: 6px;
    margin-bottom: 12px;
    text-transform: uppercase;
  }
  nav button {
    display: block;
    background: none;
    border: none;
    color: #fff;
    text-align: left;
    padding: 10px 8px;
    cursor: pointer;
    width: 100%;
    border-radius: 8px;
    transition: background .18s, transform .12s;
  }
  nav button:hover {
    background: rgba(29,185,84,0.12);
    transform: translateX(6px);
  }
  main {
    background: #0f0f0f;
    padding: 20px;
    border-radius: 10px;
    overflow-y: auto;
  }
  .card {
    background: linear-gradient(180deg,#161616,#111);
    padding: 12px;
    border-radius: 10px;
    margin-bottom: 12px;
    box-shadow: 0 6px 20px rgba(0,0,0,0.6);
    transition: transform .16s;
  }
  .card:hover { transform: translateY(-6px); }
  .title { font-weight: 700; font-size: 16px; }
  .small { font-size: 13px; color: #aaa; }
  .btn {
    background: var(--green);
    color: #000;
    border: none;
    border-radius: 6px;
    padding: 6px 10px;
    cursor: pointer;
    font-weight: 600;
    margin-top: 8px;
  }
  .btn:hover { background: #1ed760; }
  img.cover { width: 100%; border-radius: 8px; margin-bottom: 10px; display:block; }
  .grid { display:grid; grid-template-columns: repeat(auto-fill, minmax(220px,1fr)); gap:14px; }
  .artist-row { display:flex; gap:12px; align-items:center; }
  .artist-photo { width:60px; height:60px; border-radius:8px; object-fit:cover; border:2px solid var(--green); }
  footer { height: 70px; } /* space for comfortable scroll */
  .search { width:100%; padding:10px; border-radius:8px; border:1px solid #222; background:#0b0b0b; color:#fff; margin-top:8px; }
  .controls { display:flex; gap:8px; margin-top:10px; flex-wrap:wrap; }
  .btn-danger { background:#e74c3c; color:#fff; border:none; padding:6px 10px; border-radius:6px; cursor:pointer; }

  /* Banner de conexión e indicadores */
  #netBanner {
    position: fixed;
    top: 12px;
    right: 12px;
    padding: 8px 12px;
    border-radius: 10px;
    z-index: 9999;
    font-weight:700;
    display:none;
    box-shadow: 0 6px 18px rgba(0,0,0,0.6);
  }
  #pendingIndicator {
    background: rgba(0,0,0,0.08);
    padding: 6px 10px;
    border-radius: 8px;
    font-size:13px;
    color:#fff;
    display:flex;
    gap:8px;
    align-items:center;
  }
  #pendingIndicator .dot { width:10px; height:10px; border-radius:50%; background:var(--green); display:inline-block; }

  /* Small badges */
  .badge { background:rgba(255,255,255,0.04); padding:4px 8px; border-radius:6px; font-size:13px; }
  .muted { color:var(--muted); font-size:13px; }
  table { width:100%; border-collapse: collapse; }
  th, td { padding:8px; text-align:left; border-bottom:1px solid rgba(255,255,255,0.04); font-size:14px; }
  .muted-small { color:#9aa6b2; font-size:12px; }
</style>
</head>
<body>
<header>
  <div>🎵 SpotiFake — Todos los artistas</div>
  <div style="display:flex;gap:12px;align-items:center">
    <div id="pendingIndicator" style="display:none">
      <span class="dot"></span>
      <span id="pendingCount">0</span> pendientes
    </div>
    <div id="userBadge" class="badge" title="Usuario activo">Invitado</div>
  </div>
</header>

<div class="container">
  <nav>
    <h3>Tablas simuladas</h3>
    <button onclick="showTable('artists')">Artistas</button>
    <button onclick="showTable('albums')">Álbumes</button>
    <button onclick="showTable('songs')">Canciones</button>
    <button onclick="showTable('playlists')">Playlists</button>
    <button onclick="showTable('users')">Usuarios</button>
    <button onclick="showTable('history')">Historial</button>

    <input id="quickSearch" class="search" placeholder="Buscar (artista, álbum, canción)">

    <div class="controls">
      <button class="btn" id="btnCreatePlaylist">➕ Crear playlist</button>
      <button class="btn btn-danger" id="btnReset">🔁 Reset DB</button>
    </div>

    <div style="margin-top:14px;color:#bbb;font-size:13px">
      <div><strong>Playlists:</strong></div>
      <div id="playlistList" style="margin-top:8px"></div>
    </div>
  </nav>

  <main id="mainContent">
    <h2>Bienvenido 🎶</h2>
    <p class="small">Explora artistas, álbumes, canciones y crea tus playlists personalizadas. Usa el buscador rápido o el menú lateral.</p>
    <div style="height:10px"></div>
  </main>
</div>

<div id="netBanner"></div>

<footer></footer>

<script>
// --------------------- Datos base ---------------------
const rawArtists = [
"Adele","Twenty One Pilots","Chace Atlantic","Eminem","2Pac","Coldplay","Jay-Z","Ice Cube","Kendrick Lamar","Rihanna",
"The Weeknd","Paulo Londra","Duki","Billie Eilish","Bruno Mars","Khea","Cazzu","Alvaro Diaz","Justin Bieber","Kanye West",
"Rauw Alejandro","Myke Towers","Travis Scott","Sech","Quevedo","Trueno","Milo J","Arcángel","Alemán","Cartel de Santa",
"Santa Grifa","Santa Fe Klan","Shawn Mendes","MC Davo","Young Miko","De La Rose","Katteyes","J Balvin","Bad Bunny","Ozuna",
"Anuel AA","Daddy Yankee","STRANGEHUMAN","Maluma","Pitbull","Grupo Frontera","Lit Killah","Snoop Dogg","Post Malone","Zoé",
"Joji","Skrillex","Peso Pluma","Travis Scott","Drake","Fuerza Regida","System Of Down","Marshmello","Melanie Martinez","Nanpa Basico",
"The Weeknd","Baby Metal","Nskq","Rels B","Caifanes","GEMINI","Feid","Doja Cat","Bogueto","El Malilla","Plan B","Don Omar",
"Interpuesto","LATIN MAFIA","Nicki Nicole","Nirvana","Belanova","De La Guetto","Ramstein","JOTAYI","21 Savage","Videoclub",
"d4vd","Slipknot","Nathy Peluso","Bizarrap","Alfredo Olivas","Morad","Linkin Park","Bryant Myers","Eladio Carreon","Humbe",
"Lil Peep","Jon Z","Big Soto","Tiago PZK","Kidd Keo","Dei V","Millonario","Gorillaz"
];

// Normalize and dedupe
const seen = new Set();
const artistNames = [];
for (let n of rawArtists) {
  if (!n) continue;
  const name = String(n).trim();
  const k = name.toLowerCase();
  if (!seen.has(k)) { seen.add(k); artistNames.push(name); }
}

// --------------------- Local DB ---------------------
const STORAGE_KEY = "spotifyDB_complete_v2";
const OFFLINE_QUEUE_KEY = "spoti_offline_queue_v2";

let db = JSON.parse(localStorage.getItem(STORAGE_KEY) || "null");
if (!db) {
  db = {
    users: [
      { id: 1, name: "Invitado" },
      { id: 2, name: "Ana Torres" },
      { id: 3, name: "Luis Pérez" }
    ],
    currentUserId: 1,
    artists: artistNames.map((name, idx) => ({
      id: idx+1,
      name,
      genre: "Varied",
      photo: `https://i.ytimg.com/vi/AM7HIvSdMX4/hqdefault.jpg`
    })),
    albums: [],
    songs: [],
    playlists: [{ id: 1, name: "Favoritos 2025", songs: [] }],
    history: [], // { songId, playedAt, userId }
    offlineSongs: [] // downloaded songs list (ids)
  };
  localStorage.setItem(STORAGE_KEY, JSON.stringify(db));
}

// offline queue (for both playlist adds and song downloads)
let offlineQueue = JSON.parse(localStorage.getItem(OFFLINE_QUEUE_KEY) || "[]");

// --------------------- Generación albums/songs ---------------------
function ensureAlbumsSongs() {
  if (db.albums.length > 0 || db.songs.length > 0) return;
  let albumId = 1;
  let songId = 1;
  db.artists.forEach(a => {
    db.albums.push({
      id: albumId,
      title: `${a.name} Hits`,
      artistId: a.id,
      year: 2020 + (a.id % 5),
      cover: `https://via.placeholder.com/400/222222/FFFFFF?text=${encodeURIComponent(a.name + " Album")}`
    });
    db.songs.push({ id: songId++, title: `Canción 1 - ${a.name}`, albumId: albumId, artistId: a.id, duration: "3:30" });
    db.songs.push({ id: songId++, title: `Canción 2 - ${a.name}`, albumId: albumId, artistId: a.id, duration: "3:45" });
    albumId++;
  });
  saveDB();
}
ensureAlbumsSongs();

function saveDB() {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(db));
  renderPlaylistList();
  renderUserBadge();
}

// --------------------- Indicadores / banners ---------------------
const netBannerEl = document.getElementById("netBanner");
let netBannerTimer = null;
function showNetBanner(text, color = "rgba(0,0,0,0.5)", timeout = 2200){
  netBannerEl.innerText = text;
  netBannerEl.style.background = color;
  netBannerEl.style.display = "block";
  clearTimeout(netBannerTimer);
  if (timeout > 0) netBannerTimer = setTimeout(()=> netBannerEl.style.display = "none", timeout);
}

// pending indicator
function updatePendingIndicator(){
  const el = document.getElementById("pendingIndicator");
  const countEl = document.getElementById("pendingCount");
  const totalPending = offlineQueue.length;
  if (totalPending === 0) {
    el.style.display = "none";
    countEl.innerText = "0";
  } else {
    el.style.display = "flex";
    countEl.innerText = totalPending;
  }
}
updatePendingIndicator();

// user badge
function renderUserBadge(){
  const b = document.getElementById("userBadge");
  const u = db.users.find(x=>x.id===db.currentUserId) || { name: "Invitado" };
  b.innerText = u.name;
}
renderUserBadge();

// --------------------- Offline queue utils ---------------------
function saveOfflineQueue(){ localStorage.setItem(OFFLINE_QUEUE_KEY, JSON.stringify(offlineQueue)); updatePendingIndicator(); }

function enqueue(action){
  // action: { type: 'playlist_add' | 'download', payload: {...}, addedAt }
  offlineQueue.push(Object.assign({}, action, { addedAt: new Date().toISOString() }));
  saveOfflineQueue();
}

// --------------------- Sync processing ---------------------
function syncOfflineQueue(){
  if (!navigator.onLine) return;
  if (!offlineQueue || offlineQueue.length === 0) {
    showNetBanner("✅ Sin pendientes por sincronizar", "rgba(37, 211, 102, 0.95)", 1400);
    return;
  }

  showNetBanner(`🔄 Sincronizando ${offlineQueue.length} elementos…`, "rgba(255,255,255,0.12)", 1200);

  const results = [];
  offlineQueue.forEach(item => {
    if (item.type === 'playlist_add') {
      const { songId, playlistId } = item.payload;
      const p = db.playlists.find(x => x.id === playlistId);
      if (p && !p.songs.includes(songId)) {
        p.songs.push(songId);
        results.push({ ok:true, item });
      } else {
        results.push({ ok:false, item });
      }
    } else if (item.type === 'download') {
      const { songId, userId } = item.payload;
      if (!db.offlineSongs.includes(songId)) {
        db.offlineSongs.push(songId);
        results.push({ ok:true, item });
      } else {
        results.push({ ok:false, item });
      }
    }
  });

  // clear queue and persist
  offlineQueue = [];
  saveOfflineQueue();
  saveDB();

  const successCount = results.filter(r=>r.ok).length;
  const failCount = results.length - successCount;
  showNetBanner(`✔ Sincronizado: ${successCount} guardadas, ${failCount} no aplicadas`, "rgba(37, 211, 102, 0.95)", 3000);
}

// --------------------- UI rendering helpers ---------------------
const main = document.getElementById("mainContent");
function capitalize(s){ return s.charAt(0).toUpperCase()+s.slice(1); }

function renderPlaylistList(){
  const el = document.getElementById("playlistList");
  el.innerHTML = db.playlists.map(p=>`<div style="padding:6px;border-radius:6px;background:rgba(255,255,255,0.02);margin-bottom:6px;cursor:pointer" onclick="viewPlaylist(${p.id})">${p.name}</div>`).join("");
}
renderPlaylistList();

function isSongOffline(songId){ return db.offlineSongs.includes(songId); }

// --------------------- SHOW TABLE (ARTISTS / ALBUMS / SONGS / PLAYLISTS / USERS / HISTORY) ---------------------
function showTable(type) {
  if (!type) return;
  main.innerHTML = `<h2>${capitalize(type)}</h2>`;
  if (type === "artists") {
    const grid = document.createElement("div"); grid.className = "grid";
    db.artists.forEach(a => {
      const card = document.createElement("div"); card.className = "card";
      card.innerHTML = `
        <div class="artist-row">
          <img src="${a.photo}" class="artist-photo" alt="${a.name}">
          <div style="flex:1">
            <div class="title">${a.name}</div>
            <div class="meta small">${a.genre}</div>
            <div style="margin-top:8px"><button class="btn" onclick="showArtist(${a.id})">Ver álbumes</button></div>
          </div>
        </div>`;
      grid.appendChild(card);
    });
    main.appendChild(grid);

  } else if (type === "albums") {
    const grid = document.createElement("div"); grid.className = "grid";
    db.albums.forEach(al => {
      const artist = db.artists.find(x => x.id === al.artistId) || { name: "(desconocido)" };
      const card = document.createElement("div"); card.className = "card";
      card.innerHTML = `
        <img src="${al.cover}" class="cover" alt="${al.title}">
        <div class="title">${al.title}</div>
        <div class="small">${artist.name} • ${al.year}</div>
        <div style="margin-top:8px"><button class="btn" onclick="showAlbum(${al.id})">Ver canciones</button></div>
      `;
      grid.appendChild(card);
    });
    main.appendChild(grid);

  } else if (type === "songs") {
    const grid = document.createElement("div"); grid.className = "grid";
    db.songs.forEach(s => {
      const artist = db.artists.find(a => a.id === s.artistId) || {};
      const album = db.albums.find(al => al.id === s.albumId) || {};
      const card = document.createElement("div"); card.className = "card";
      const offline = isSongOffline(s.id);
      card.innerHTML = `
        <div class="title">${s.title}</div>
        <div class="small">${artist.name} • ${album.title || ""} • ${s.duration}</div>
        <div style="margin-top:8px;display:flex;gap:8px;flex-wrap:wrap">
          <button class="btn" onclick="playSongId(${s.id})">▶ Reproducir</button>
          <button class="btn" onclick="addToPlaylistPrompt(${s.id})">+ Playlist</button>
          ${offline ? `<button class="btn" disabled style="background:#6b6b6b">✔ Guardada</button>` : `<button class="btn" onclick="saveSongOffline(${s.id})">⬇ Guardar</button>`}
        </div>
      `;
      grid.appendChild(card);
    });
    main.appendChild(grid);

  } else if (type === "playlists") {
    main.innerHTML = `<h2>Playlists</h2>`;
    const container = document.createElement("div");
    db.playlists.forEach(p => {
      const card = document.createElement("div"); card.className = "card";
      const songCount = p.songs.length;
      card.innerHTML = `
        <div class="title">${p.name}</div>
        <div class="small">${songCount ? songCount + " canciones" : "Sin canciones"}</div>
        <div style="margin-top:8px;display:flex;gap:8px">
          <button class="btn" onclick="viewPlaylist(${p.id})">Administrar</button>
          <button class="btn btn-danger" onclick="deletePlaylist(${p.id})">Eliminar</button>
        </div>`;
      container.appendChild(card);
    });
    main.appendChild(container);

  } else if (type === "users") {
    main.innerHTML = `<h2>Usuarios</h2><div class="small">Gestión simple de usuarios</div>`;
    const container = document.createElement("div");
    const table = document.createElement("table");
    table.innerHTML = `<thead><tr><th>ID</th><th>Nombre</th><th>Acciones</th></tr></thead>`;
    const tbody = document.createElement("tbody");
    db.users.forEach(u=>{
      const tr = document.createElement("tr");
      tr.innerHTML = `<td>${u.id}</td><td>${u.name}</td><td>
        <button class="btn" onclick="setCurrentUser(${u.id})">Seleccionar</button>
        <button class="btn btn-danger" onclick="deleteUser(${u.id})">Eliminar</button>
      </td>`;
      tbody.appendChild(tr);
    });
    table.appendChild(tbody);
    container.appendChild(table);
    const addBtn = document.createElement("div");
    addBtn.style.marginTop = "10px";
    addBtn.innerHTML = `<button class="btn" onclick="createUserPrompt()">➕ Nuevo usuario</button>`;
    container.appendChild(addBtn);
    main.appendChild(container);

  } else if (type === "history") {
    main.innerHTML = `<h2>Historial de reproducción</h2><div class="small">Últimas reproducciones (por usuario)</div>`;
    const table = document.createElement("table");
    table.innerHTML = `<thead><tr><th>Fecha</th><th>Canción</th><th>Usuario</th></tr></thead>`;
    const tbody = document.createElement("tbody");
    const sorted = db.history.slice().sort((a,b)=> new Date(b.playedAt) - new Date(a.playedAt));
    sorted.forEach(h=>{
      const s = db.songs.find(x=>x.id===h.songId) || { title: `ID ${h.songId}` };
      const u = db.users.find(x=>x.id===h.userId) || { name: "Invitado" };
      const tr = document.createElement("tr");
      tr.innerHTML = `<td class="muted-small">${new Date(h.playedAt).toLocaleString()}</td><td>${s.title}</td><td>${u.name}</td>`;
      tbody.appendChild(tr);
    });
    table.appendChild(tbody);
    main.appendChild(table);
  }
}

// --------------------- Mostrar artista / álbum / álbum canciones ---------------------
function showArtist(id) {
  const artist = db.artists.find(a => a.id === id);
  if (!artist) return alert("Artista no encontrado");
  const albums = db.albums.filter(al => al.artistId === id);
  main.innerHTML = `<h2>${artist.name}</h2><div class="small">${artist.genre}</div>`;
  const grid = document.createElement("div"); grid.className = "grid";
  albums.forEach(al => {
    const card = document.createElement("div"); card.className = "card";
    card.innerHTML = `
      <img src="${al.cover}" class="cover" alt="${al.title}">
      <div class="title">${al.title}</div>
      <div class="small">Año: ${al.year}</div>
      <div style="margin-top:8px"><button class="btn" onclick="showAlbum(${al.id})">Ver canciones</button></div>
    `;
    grid.appendChild(card);
  });
  main.appendChild(grid);
}

function showAlbum(id) {
  const album = db.albums.find(a => a.id === id);
  if (!album) return alert("Álbum no encontrado");
  const artist = db.artists.find(ar => ar.id === album.artistId) || {};
  const songs = db.songs.filter(s => s.albumId === id);
  main.innerHTML = `<h2>${album.title}</h2><div class="small">${artist.name} • ${album.year}</div>`;
  const grid = document.createElement("div"); grid.className = "grid";
  songs.forEach(s => {
    const offline = isSongOffline(s.id);
    const card = document.createElement("div"); card.className = "card";
    card.innerHTML = `
      <div class="title">${s.title}</div>
      <div class="small">${s.duration}</div>
      <div style="margin-top:8px;display:flex;gap:8px;flex-wrap:wrap">
        <button class="btn" onclick="playSongId(${s.id})">▶ Reproducir</button>
        <button class="btn" onclick="addToPlaylistPrompt(${s.id})">+ Playlist</button>
        ${offline ? `<button class="btn" disabled style="background:#6b6b6b">✔ Guardada</button>` : `<button class="btn" onclick="saveSongOffline(${s.id})">⬇ Guardar</button>`}
      </div>
    `;
    grid.appendChild(card);
  });
  main.appendChild(grid);
}

// --------------------- Reproducción y registro de historial ---------------------
let audioCtx = null, currentOsc = null, isMuted = false;
function ensureAudioCtx(){ if(!audioCtx) audioCtx = new (window.AudioContext||window.webkitAudioContext)(); }

function playSo
