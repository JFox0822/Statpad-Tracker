# Statpad-Tracker[index (78).html](https://github.com/user-attachments/files/27608326/index.78.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>StatPad Tracker</title>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { background: #070d18; color: #e2e8f0; font-family: 'Inter', system-ui, sans-serif; min-height: 100vh; padding-bottom: 60px; }

  /* ── Header ── */
  .header { background: #0d1625; border-bottom: 1px solid #1e3a5f; padding: 18px 24px; }
  .header h1 { font-size: 22px; font-weight: 800; color: #fff; }
  .header p  { color: #64748b; font-size: 13px; margin-top: 4px; }

  /* ── Tabs ── */
  .tabs { display: flex; gap: 2px; padding: 16px 24px 0; border-bottom: 1px solid #1e3a5f; overflow-x: auto; }
  .tab  { padding: 8px 18px; border-radius: 8px 8px 0 0; cursor: pointer; font-size: 13px; font-weight: 600;
          background: transparent; color: #64748b; border: 1px solid transparent; border-bottom: none; white-space: nowrap; }
  .tab.active { background: #111827; color: #fff; border-color: #1e3a5f; }

  /* ── Body ── */
  .body { max-width: 660px; margin: 0 auto; padding: 24px 16px; }

  /* ── Cards ── */
  .card { background: #111827; border: 1px solid #1e3a5f; border-radius: 12px; padding: 20px; margin-bottom: 20px; }
  .card-title { font-weight: 800; font-size: 17px; margin-bottom: 16px; }

  /* ── Form ── */
  label.lbl { display: block; font-size: 11px; color: #64748b; font-weight: 700; text-transform: uppercase; letter-spacing: 1px; margin-bottom: 6px; margin-top: 14px; }
  label.lbl:first-child { margin-top: 0; }
  select, textarea, input[type=text] {
    width: 100%; background: #1a2740; border: 1px solid #1e3a5f; border-radius: 8px;
    padding: 10px 14px; color: #e2e8f0; font-size: 14px; outline: none; font-family: inherit;
  }
  textarea { resize: vertical; min-height: 110px; font-family: monospace; font-size: 13px; }
  .btn { display: block; width: 100%; margin-top: 12px; background: #2563eb; color: #fff;
         border: none; border-radius: 8px; padding: 12px; font-weight: 700; font-size: 15px; cursor: pointer; }
  .btn:hover { background: #1d4ed8; }
  .msg { margin-top: 10px; font-size: 13px; color: #94a3b8; min-height: 20px; }

  /* ── Setup banner ── */
  .setup-banner { background: #1a1000; border: 1px solid #b45309; border-radius: 12px; padding: 18px 20px; margin-bottom: 20px; }
  .setup-banner h3 { color: #f59e0b; font-size: 15px; margin-bottom: 8px; }
  .setup-banner p  { color: #94a3b8; font-size: 13px; line-height: 1.6; }
  .setup-banner a  { color: #3b82f6; }
  .setup-banner input { margin-top: 10px; }
  .btn-sm { display: inline-block; margin-top: 10px; background: #b45309; color: #fff;
            border: none; border-radius: 6px; padding: 8px 14px; font-weight: 700; font-size: 13px; cursor: pointer; }

  /* ── Win tally ── */
  .bar-row { margin-bottom: 16px; }
  .bar-label { display: flex; justify-content: space-between; align-items: center; margin-bottom: 6px; }
  .bar-name  { font-weight: 700; font-size: 15px; }
  .bar-wins  { font-weight: 900; font-size: 18px; }
  .bar-track { height: 10px; background: #1a2740; border-radius: 5px; overflow: hidden; }
  .bar-fill  { height: 100%; border-radius: 5px; transition: width 0.4s; }

  /* ── Game log ── */
  .game-group { margin-bottom: 24px; }
  .game-header { display: flex; align-items: center; gap: 10px; padding-bottom: 8px; border-bottom: 1px solid #1e3a5f; margin-bottom: 10px; }
  .game-title  { font-weight: 800; font-size: 15px; }
  .game-date   { color: #64748b; font-size: 12px; }
  .game-stat   { margin-left: auto; color: #64748b; font-size: 12px; font-weight: 700; }
  .entry-row   { display: flex; align-items: center; gap: 12px; padding: 10px 14px; border-radius: 8px; margin-bottom: 6px; }
  .entry-name  { font-weight: 700; flex: 1; }
  .entry-score { font-weight: 900; font-size: 20px; }
  .entry-stat  { color: #64748b; font-size: 12px; min-width: 32px; }
  .entry-pct   { color: #64748b; font-size: 12px; min-width: 50px; text-align: right; }
  .del-btn     { background: transparent; border: none; color: #475569; cursor: pointer; font-size: 16px; padding: 0; line-height: 1; }
  .del-btn:hover { color: #ef4444; }

  /* ── Stat breakdown ── */
  .stat-pill { display: inline-block; padding: 5px 14px; border-radius: 20px; margin: 4px; cursor: pointer;
               font-size: 13px; font-weight: 700; border: 1px solid #1e3a5f; background: #1a2740; color: #94a3b8; }
  .stat-pill.active { background: #1e3a5f; color: #fff; border-color: #3b82f6; }
  .stat-table { width: 100%; border-collapse: collapse; font-size: 14px; margin-top: 16px; }
  .stat-table th { text-align: left; color: #64748b; font-size: 11px; font-weight: 700; text-transform: uppercase;
                   letter-spacing: 1px; padding: 6px 10px; border-bottom: 1px solid #1e3a5f; }
  .stat-table td { padding: 10px 10px; border-bottom: 1px solid #0f1924; }
  .stat-table tr:last-child td { border-bottom: none; }
  .stat-table tr:hover td { background: #0d1625; }
  .no-data { color: #64748b; text-align: center; padding: 30px 0; font-size: 14px; }

  /* ── Medals ── */
  .m0::before { content: '🥇 '; }
  .m1::before { content: '🥈 '; }
  .m2::before { content: '🥉 '; }
</style>
</head>
<body>

<div class="header">
  <h1>⚾ StatPad Tracker</h1>
  <p>Luke · Jacob · Chris · Tommy</p>
</div>

<div class="tabs">
  <div class="tab active" onclick="showTab('tally')">🏆 Win Tally</div>
  <div class="tab" onclick="showTab('stats')">📊 Stat Breakdown</div>
  <div class="tab" onclick="showTab('log')">📋 Game Log</div>
  <div class="tab" onclick="showTab('submit')">➕ Submit</div>
  <div class="tab" onclick="showTab('setup')">⚙️ Setup</div>
</div>

<div class="body">
  <div id="tab-tally"></div>
  <div id="tab-stats" style="display:none"></div>
  <div id="tab-log"   style="display:none"></div>
  <div id="tab-submit" style="display:none"></div>
  <div id="tab-setup" style="display:none"></div>
</div>

<script>
// ─── Config ──────────────────────────────────────────────────────────────────
// Fill these in with your JSONBin details (see Setup tab)
const CONFIG = {
  BIN_ID:  localStorage.getItem('sp_bin_id')  || '',
  API_KEY: localStorage.getItem('sp_api_key') || '',
};

const PLAYERS = ['Luke', 'Jacob', 'Chris', 'Tommy'];
const COLORS   = { Luke:'#3b82f6', Jacob:'#22c55e', Chris:'#f59e0b', Tommy:'#ef4444' };
const MEDALS   = ['🥇','🥈','🥉',''];

let entries = [];   // { date, gameNumber, player, score, stat, percentile, guesses }
let activeStatTab = null;

// ─── JSONBin helpers ──────────────────────────────────────────────────────────
async function fetchData() {
  if (!CONFIG.BIN_ID || !CONFIG.API_KEY) return [];
  try {
    const r = await fetch(`https://api.jsonbin.io/v3/b/${CONFIG.BIN_ID}/latest`, {
      headers: { 'X-Master-Key': CONFIG.API_KEY }
    });
    const j = await r.json();
    return j.record?.entries ?? [];
  } catch { return []; }
}

async function pushData(newEntries) {
  if (!CONFIG.BIN_ID || !CONFIG.API_KEY) return;
  await fetch(`https://api.jsonbin.io/v3/b/${CONFIG.BIN_ID}`, {
    method: 'PUT',
    headers: { 'Content-Type': 'application/json', 'X-Master-Key': CONFIG.API_KEY },
    body: JSON.stringify({ entries: newEntries })
  });
}

// ─── Parse share text ─────────────────────────────────────────────────────────
function parseShare(text) {
  const gameMatch  = text.match(/#(\d+)/);
  const scoreMatch = text.match(/Total Score:\s*([\d.]+)\s*([A-Za-z+\/]+)/i);
  const guessMatch = text.match(/Guesses?:\s*(\d+)/i);
  const pctMatch   = text.match(/Percentile:\s*([\d.]+)%/i);
  if (!scoreMatch) return null;
  return {
    gameNumber:  gameMatch  ? parseInt(gameMatch[1])    : null,
    score:       parseFloat(scoreMatch[1]),
    stat:        scoreMatch[2].toUpperCase(),
    guesses:     guessMatch ? parseInt(guessMatch[1])   : null,
    percentile:  pctMatch   ? parseFloat(pctMatch[1])   : null,
  };
}

// ─── Derived stats ────────────────────────────────────────────────────────────
function getWinCounts() {
  const counts = Object.fromEntries(PLAYERS.map(p => [p, 0]));
  const byGame = groupByGame();
  Object.values(byGame).forEach(group => {
    if (!group.length) return;
    const best = group.reduce((a,b) => b.score > a.score ? b : a, group[0]);
    counts[best.player] = (counts[best.player] || 0) + 1;
  });
  return counts;
}

function groupByGame() {
  const map = {};
  entries.forEach(e => {
    const key = e.gameNumber != null ? `g${e.gameNumber}` : e.date;
    if (!map[key]) map[key] = [];
    map[key].push(e);
  });
  return map;
}

function getStatList() {
  return [...new Set(entries.map(e => e.stat))].sort();
}

function getStatBreakdown(stat) {
  const filtered = entries.filter(e => e.stat === stat);
  return PLAYERS.map(player => {
    const rows = filtered.filter(e => e.player === player);
    if (!rows.length) return { player, games: 0, high: '-', avg: '-', bestPct: '-', avgPct: '-' };
    const scores = rows.map(e => e.score);
    const pcts   = rows.filter(e => e.percentile != null).map(e => e.percentile);
    return {
      player,
      games:   rows.length,
      high:    Math.max(...scores),
      avg:     (scores.reduce((a,b) => a+b, 0) / scores.length).toFixed(1),
      bestPct: pcts.length ? Math.min(...pcts).toFixed(1) + '%' : '-',
      avgPct:  pcts.length ? (pcts.reduce((a,b)=>a+b,0)/pcts.length).toFixed(1) + '%' : '-',
    };
  }).sort((a,b) => (b.high === '-' ? -1 : 0) || b.high - a.high);
}

// ─── Utility ──────────────────────────────────────────────────────────────────
function today() { return new Date().toLocaleDateString('en-CA'); }
function fmtDate(d) {
  if (!d) return '';
  const [y,m,day] = d.split('-');
  return new Date(+y,+m-1,+day).toLocaleDateString('en-US',{month:'short',day:'numeric',year:'numeric'});
}

// ─── Render functions ─────────────────────────────────────────────────────────
function renderTally() {
  const counts  = getWinCounts();
  const board   = PLAYERS.map(p => ({ name:p, wins:counts[p] })).sort((a,b)=>b.wins-a.wins);
  const maxWins = Math.max(...board.map(w=>w.wins), 1);
  const notSetup = !CONFIG.BIN_ID || !CONFIG.API_KEY;

  let html = '';
  if (notSetup) html += setupBanner();

  html += `<div class="card"><div class="card-title">Win Tally</div>`;
  board.forEach((w,i) => {
    const pct = ((w.wins/maxWins)*100).toFixed(1);
    html += `
      <div class="bar-row">
        <div class="bar-label">
          <span class="bar-name">${MEDALS[i]||''} ${w.name}</span>
          <span class="bar-wins" style="color:${COLORS[w.name]}">${w.wins} ${w.wins===1?'win':'wins'}</span>
        </div>
        <div class="bar-track">
          <div class="bar-fill" style="width:${pct}%;background:${COLORS[w.name]}"></div>
        </div>
      </div>`;
  });
  html += `</div>`;
  document.getElementById('tab-tally').innerHTML = html;
}

function renderStats() {
  const statList = getStatList();
  if (!activeStatTab && statList.length) activeStatTab = statList[0];

  let html = `<div class="card"><div class="card-title">Stat Breakdown</div>`;

  if (!statList.length) {
    html += `<div class="no-data">No data yet — submit some results first!</div></div>`;
    document.getElementById('tab-stats').innerHTML = html;
    return;
  }

  // Stat pills
  html += `<div>`;
  statList.forEach(s => {
    html += `<span class="stat-pill ${s===activeStatTab?'active':''}" onclick="selectStat('${s}')">${s}</span>`;
  });
  html += `</div>`;

  // Table for active stat
  if (activeStatTab) {
    const rows = getStatBreakdown(activeStatTab);
    html += `
      <table class="stat-table">
        <thead><tr>
          <th>Player</th><th>Games</th><th>High Score</th><th>Avg Score</th><th>Best Percentile</th><th>Avg Percentile</th>
        </tr></thead><tbody>`;
    rows.forEach((r,i) => {
      const medal = r.games > 0 ? (MEDALS[i]||'') : '';
      html += `<tr>
        <td><span style="font-weight:700;color:${COLORS[r.player]}">${medal} ${r.player}</span></td>
        <td>${r.games}</td>
        <td style="font-weight:700">${r.high}</td>
        <td>${r.avg}</td>
        <td style="color:${r.bestPct!=='-'?'#22c55e':'#64748b'}">${r.bestPct}</td>
        <td>${r.avgPct}</td>
      </tr>`;
    });
    html += `</tbody></table>`;

    // Per-game breakdown for this stat
    const gameDays = entries.filter(e=>e.stat===activeStatTab);
    const byGameKeys = [...new Set(gameDays.map(e=>e.gameNumber!=null?`g${e.gameNumber}`:e.date))];
    if (byGameKeys.length) {
      html += `<div style="margin-top:24px;font-weight:700;font-size:14px;color:#94a3b8;margin-bottom:10px">All ${activeStatTab} Games</div>`;
      byGameKeys.forEach(key => {
        const group  = gameDays.filter(e=>(e.gameNumber!=null?`g${e.gameNumber}`:e.date)===key);
        const sorted = [...group].sort((a,b)=>b.score-a.score);
        const gNum   = group[0].gameNumber;
        html += `<div style="margin-bottom:14px">
          <div style="font-size:13px;color:#64748b;margin-bottom:6px">
            ${gNum?`Game #${gNum} · `:''} ${fmtDate(group[0].date)}
          </div>`;
        sorted.forEach((e,i)=>{
          html += `<div class="entry-row" style="background:${i===0?'#0f1f0f':'#0d1625'};border:1px solid ${i===0?'#1a4a1a':'#1a2e4a'}">
            <span>${MEDALS[i]||''}</span>
            <span class="entry-name" style="color:${COLORS[e.player]}">${e.player}</span>
            <span class="entry-score">${e.score}</span>
            <span class="entry-stat">${e.stat}</span>
            ${e.percentile!=null?`<span class="entry-pct">${e.percentile}%</span>`:'<span class="entry-pct"></span>'}
          </div>`;
        });
        html += `</div>`;
      });
    }
  }

  html += `</div>`;
  document.getElementById('tab-stats').innerHTML = html;
}

function renderLog() {
  const byGame  = groupByGame();
  const keys    = Object.keys(byGame).sort().reverse();

  let html = `<div class="card"><div class="card-title">Game Log</div>`;
  if (!keys.length) { html += `<div class="no-data">No results yet. Submit the first one!</div>`; }

  keys.forEach(key => {
    const group  = byGame[key];
    const sorted = [...group].sort((a,b)=>b.score-a.score);
    const gNum   = group[0].gameNumber;
    const stat   = group[0].stat;
    const date   = group[0].date;

    html += `<div class="game-group">
      <div class="game-header">
        <span class="game-title">${gNum ? `Game #${gNum}` : fmtDate(date)}</span>
        ${gNum&&date ? `<span class="game-date">${fmtDate(date)}</span>` : ''}
        <span class="game-stat">${stat}</span>
      </div>`;

    sorted.forEach((e,i)=>{
      const idx = entries.indexOf(e);
      html += `<div class="entry-row" style="background:${i===0?'#0f1f0f':'#0d1625'};border:1px solid ${i===0?'#1a4a1a':'#1a2e4a'}">
        <span>${MEDALS[i]||''}</span>
        <span class="entry-name" style="color:${COLORS[e.player]}">${e.player}</span>
        <span class="entry-score">${e.score}</span>
        <span class="entry-stat">${e.stat}</span>
        ${e.percentile!=null?`<span class="entry-pct">${e.percentile}%</span>`:'<span class="entry-pct"></span>'}
        <button class="del-btn" onclick="deleteEntry(${idx})">✕</button>
      </div>`;
    });
    html += `</div>`;
  });

  html += `</div>`;
  document.getElementById('tab-log').innerHTML = html;
}

function renderSubmit() {
  const notSetup = !CONFIG.BIN_ID || !CONFIG.API_KEY;
  let html = '';
  if (notSetup) html += setupBanner();

  html += `
    <div class="card">
      <div class="card-title">Add a Result</div>
      <label class="lbl">Player</label>
      <select id="s-player">
        ${PLAYERS.map(p=>`<option>${p}</option>`).join('')}
      </select>
      <label class="lbl">Paste StatPad share text</label>
      <textarea id="s-raw" placeholder="⚾️💎 StatpadGame #90 ⚾️💎&#10;&#10;Total Score: 14 WAR 🔥&#10;Guesses: 6&#10;Percentile: 13.5%"></textarea>
      <button class="btn" onclick="submitEntry()">Submit</button>
      <div class="msg" id="s-msg"></div>
    </div>`;
  document.getElementById('tab-submit').innerHTML = html;
}

function renderSetup() {
  document.getElementById('tab-setup').innerHTML = `
    <div class="card">
      <div class="card-title">⚙️ Setup — JSONBin</div>
      <p style="color:#94a3b8;font-size:14px;line-height:1.7;margin-bottom:16px">
        JSONBin stores your shared scores in the cloud so all four of you see the same data.
        It's free — takes about 2 minutes.
      </p>
      <ol style="color:#94a3b8;font-size:14px;line-height:2;padding-left:20px">
        <li>Go to <a href="https://jsonbin.io" target="_blank" style="color:#3b82f6">jsonbin.io</a> and create a free account</li>
        <li>Click <strong style="color:#e2e8f0">API Keys</strong> → copy your <strong style="color:#e2e8f0">Master Key</strong></li>
        <li>Click <strong style="color:#e2e8f0">Bins → Create Bin</strong>, paste <code style="color:#22c55e">{"entries":[]}</code>, save it</li>
        <li>Copy the <strong style="color:#e2e8f0">Bin ID</strong> from the URL or dashboard</li>
        <li>Paste both below and click Save</li>
      </ol>

      <label class="lbl" style="margin-top:20px">Master Key</label>
      <input type="text" id="cfg-key" placeholder="$2a$10$..." value="${CONFIG.API_KEY}" />
      <label class="lbl">Bin ID</label>
      <input type="text" id="cfg-bin" placeholder="64a3b2c1e3f..." value="${CONFIG.BIN_ID}" />
      <button class="btn" onclick="saveConfig()" style="margin-top:12px">Save & Test Connection</button>
      <div class="msg" id="cfg-msg"></div>
    </div>`;
}

function setupBanner() {
  return `<div class="setup-banner">
    <h3>⚠️ Setup needed to sync data</h3>
    <p>Go to the <strong>Setup tab</strong> and add your JSONBin credentials so all four players share the same data.
    Until then, scores only save locally in your browser.</p>
  </div>`;
}

// ─── Actions ──────────────────────────────────────────────────────────────────
async function submitEntry() {
  const player = document.getElementById('s-player').value;
  const raw    = document.getElementById('s-raw').value;
  const msg    = document.getElementById('s-msg');
  const parsed = parseShare(raw);

  if (!parsed) { msg.textContent = '❌ Couldn\'t read the score — paste the full StatPad share text.'; return; }

  const dupe = entries.find(e => e.player===player && e.gameNumber!=null && e.gameNumber===parsed.gameNumber);
  if (dupe) { msg.textContent = `⚠️ ${player} already has a score for Game #${parsed.gameNumber}.`; return; }

  msg.textContent = 'Saving…';
  const newEntry = { date: today(), ...parsed, player };
  entries = [newEntry, ...entries];

  await pushData(entries);
  renderAll();
  document.getElementById('s-raw').value = '';
  document.getElementById('s-msg').textContent =
    `✅ Saved! ${player}: ${parsed.score} ${parsed.stat}${parsed.gameNumber?` — Game #${parsed.gameNumber}`:''}`;
}

async function deleteEntry(idx) {
  if (!confirm('Delete this entry?')) return;
  entries.splice(idx, 1);
  await pushData(entries);
  renderAll();
}

function selectStat(stat) {
  activeStatTab = stat;
  renderStats();
}

async function saveConfig() {
  const key = document.getElementById('cfg-key').value.trim();
  const bin = document.getElementById('cfg-bin').value.trim();
  const msg = document.getElementById('cfg-msg');
  if (!key || !bin) { msg.textContent = '⚠️ Both fields are required.'; return; }
  msg.textContent = 'Testing…';
  try {
    const r = await fetch(`https://api.jsonbin.io/v3/b/${bin}/latest`, { headers: { 'X-Master-Key': key } });
    if (!r.ok) throw new Error('Bad response');
    localStorage.setItem('sp_api_key', key);
    localStorage.setItem('sp_bin_id',  bin);
    CONFIG.API_KEY = key; CONFIG.BIN_ID = bin;
    const j = await r.json();
    entries = j.record?.entries ?? [];
    msg.textContent = '✅ Connected! Data loaded.';
    renderAll();
  } catch {
    msg.textContent = '❌ Connection failed — double-check your Key and Bin ID.';
  }
}

// ─── Tab switching ─────────────────────────────────────────────────────────────
function showTab(name) {
  ['tally','stats','log','submit','setup'].forEach(t => {
    document.getElementById(`tab-${t}`).style.display = t===name?'block':'none';
  });
  document.querySelectorAll('.tab').forEach((el,i) => {
    el.classList.toggle('active', ['tally','stats','log','submit','setup'][i]===name);
  });
  if (name==='stats') renderStats();
}

function renderAll() {
  renderTally();
  renderStats();
  renderLog();
  renderSubmit();
  renderSetup();
}

// ─── Init ─────────────────────────────────────────────────────────────────────
(async () => {
  entries = await fetchData();
  renderAll();
})();
</script>
</body>
</html>
