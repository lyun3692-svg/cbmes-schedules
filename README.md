
<!DOCTYPE html>
<!--
  QUICK GUIDE: WHERE TO CHANGE THINGS (search for the capitalized heading)
  - Schedules, logo, banner ..... "SCHEDULE DATA" (inside the script at the bottom)
  - Colors ...................... "1. COLORS" (inside the style section)
  - Fonts and text sizes ........ "2. FONTS AND TEXT SIZES"
  - Page wording ................ the header text below, and "WORDING" in the script
  - Time format (12h or 24h) .... "TIME FORMAT" in the script
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<!-- SECURITY: this page can only show its own content. It cannot contact other sites, submit forms or load
     outside scripts. Images must come from this site or be embedded. To use a logo hosted on another site,
     add its address after img-src (this also lets that site see your visitors, so prefer uploading the file). -->
<meta http-equiv="Content-Security-Policy" content="default-src 'none'; script-src 'unsafe-inline'; style-src 'unsafe-inline'; img-src 'self' data:; font-src 'self'; connect-src 'none'; form-action 'none'; base-uri 'none'; object-src 'none'">
<meta name="referrer" content="no-referrer">
<title>CBMES Faculty Schedules</title>
<style>
/* ===== 1. COLORS (light theme) =====
   Change the hex values (#rrggbb) to restyle the whole site.
   --bg page background | --surface panels and table cells | --text main text | --muted secondary text
   --line borders | --sel selected faculty row | --head table header and toggle background
   --class-* class blocks (background, border, text) | --consult-* consultation blocks
   --accent links, focus outline and the highlight on a searched course code */
:root{--bg:#f3f4f6;--surface:#ffffff;--text:#111827;--muted:#6b7280;--line:#e5e7eb;--sel:#e5e7eb;--hover:#f9fafb;--head:#f9fafb;
--class-bg:#e3fbec;--class-line:#9fdcb8;--class-ink:#14532d;--consult-bg:#fff0c7;--consult-line:#f0c75e;--consult-ink:#6b4300;--accent:#2563eb;color-scheme:light}
/* Dark theme: same names, used when a device is in dark mode. Keep the two dark blocks identical. */
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#0b0f14;--surface:#151a21;--text:#e5e7eb;--muted:#9aa4b2;--line:#2a323c;--sel:#262e38;--hover:#1b222a;--head:#1b222a;--class-bg:#123524;--class-line:#2f7a52;--class-ink:#b6f0cf;--consult-bg:#3a2d0c;--consult-line:#8a6a1f;--consult-ink:#ffdf91;--accent:#7aa2ff;color-scheme:dark}}
:root[data-theme="dark"]{--bg:#0b0f14;--surface:#151a21;--text:#e5e7eb;--muted:#9aa4b2;--line:#2a323c;--sel:#262e38;--hover:#1b222a;--head:#1b222a;--class-bg:#123524;--class-line:#2f7a52;--class-ink:#b6f0cf;--consult-bg:#3a2d0c;--consult-line:#8a6a1f;--consult-ink:#ffdf91;--accent:#7aa2ff;color-scheme:dark}

/* ===== 2. FONTS AND TEXT SIZES =====
   --font: put your preferred font first; the others are fallbacks used if it is not installed.
   To use a font file, upload it, add an @font-face rule here, and name it first in --font.
   --fs-title page title | --fs-body normal text | --fs-small secondary text | --fs-block text inside timetable blocks
   --radius roundness of panels */
:root{--font:Inter,system-ui,-apple-system,"Segoe UI",Roboto,sans-serif;--fs-title:1.9rem;--fs-body:1rem;--fs-small:.86rem;--fs-block:.78rem;--radius:12px}

/* ===== 3. LAYOUT AND DEVICES (phones, tablets, laptops) ===== */
:root{box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
html{scroll-padding-top:env(safe-area-inset-top,0px);-webkit-text-size-adjust:100%}
*,*::before,*::after{box-sizing:border-box}
[hidden]{display:none!important}
body{margin:0;background:var(--bg);color:var(--text);font:var(--fs-body)/1.5 var(--font)}
.wrap{max-width:1200px;margin:0 auto;padding:0 max(16px,env(safe-area-inset-right,0px)) 0 max(16px,env(safe-area-inset-left,0px))}
.banner{height:clamp(96px,16vw,200px);overflow:hidden;background:var(--head);border-bottom:1px solid var(--line)}
.banner img{display:block;width:100%;height:100%;object-fit:cover}
.top{background:var(--surface);border-bottom:1px solid var(--line);padding:24px 0}
.brand{display:flex;align-items:center;gap:16px;margin-bottom:16px}
.logo{flex:none;width:84px;height:84px}
.logo img{display:block;width:100%;height:100%;object-fit:contain}
.logo.empty-img,.banner.empty-img{display:flex;align-items:center;justify-content:center;color:var(--muted);font-size:var(--fs-small);text-align:center;border:1px dashed var(--muted)}
.logo.empty-img{border-radius:var(--radius)}
.banner.empty-img{border-width:0 0 1px}
.eyebrow{margin:0 0 6px;font-size:.78rem;font-weight:600;letter-spacing:.12em;text-transform:uppercase;color:var(--muted)}
h1{margin:0 0 8px;font-size:var(--fs-title);line-height:1.2}
.lead{margin:0;max-width:640px;color:var(--muted)}
.termrow{display:flex;flex-wrap:wrap;align-items:center;gap:12px;margin:0;color:var(--muted);font-size:.9rem}
.pill{padding:8px 14px;border:1px solid var(--line);border-radius:8px;color:var(--text)}
.note{margin:14px 0 0;padding:10px 12px;border:1px solid var(--consult-line);background:var(--consult-bg);color:var(--consult-ink);border-radius:8px;font-size:.9rem}
main{padding:20px 0 48px}
.layout{display:grid;gap:16px;align-items:start}
@media (min-width:900px){.layout{grid-template-columns:340px 1fr}}
.panel{background:var(--surface);border:1px solid var(--line);border-radius:var(--radius);padding:16px;overflow:hidden}
.ph{margin:0 0 12px;font-size:1.05rem}
.searches{display:grid;gap:10px}
input{width:100%;min-height:44px;padding:10px 14px;font:inherit;font-size:16px;color:var(--text);background:var(--surface);border:1px solid var(--line);border-radius:8px}/* 16px stops iPhones zooming in */
:focus-visible{outline:2px solid var(--accent);outline-offset:2px}
.faculty{margin:14px -16px -16px;border-top:1px solid var(--line);max-height:min(60vh,520px);overflow-y:auto}
.row{display:block;width:100%;min-height:56px;text-align:left;padding:12px 16px;border:0;border-bottom:1px solid var(--line);background:var(--surface);color:var(--text);font:inherit;cursor:pointer}
.row:hover{background:var(--hover)}
.row[aria-pressed="true"]{background:var(--sel)}
.rt{display:block;font-weight:600;font-size:.92rem;text-transform:uppercase}
.rs{display:block;color:var(--muted);font-size:var(--fs-small)}
.tools{display:flex;flex-wrap:wrap;justify-content:space-between;align-items:center;gap:12px;padding-bottom:14px;border-bottom:1px solid var(--line)}
.legend{display:flex;flex-wrap:wrap;align-items:center;gap:8px;font-size:var(--fs-small);color:var(--muted)}
.sw{display:inline-block;width:14px;height:14px;border-radius:4px;border:1px solid}
.sw.class{background:var(--class-bg);border-color:var(--class-line)}
.sw.consult{background:var(--consult-bg);border-color:var(--consult-line);margin-left:8px}
.segs{display:inline-flex;padding:3px;border:1px solid var(--line);border-radius:10px;background:var(--head)}
.seg{min-height:40px;border:0;background:transparent;color:var(--muted);font:inherit;font-size:.9rem;padding:6px 16px;border-radius:8px;cursor:pointer}
.seg[aria-pressed="true"]{background:var(--surface);color:var(--text);box-shadow:0 0 0 1px var(--line)}
/* content-visibility lets the browser skip drawing professors that are off screen, so Display all stays fast */
.prof{padding-top:18px;content-visibility:auto;contain-intrinsic-size:auto 780px}
.prof+.prof{margin-top:22px;border-top:1px solid var(--line)}
.pname{margin:0;font-size:1.1rem;text-transform:uppercase}
.psub{margin:2px 0 0;color:var(--muted);font-size:.9rem;overflow-wrap:anywhere}
.psub a{color:var(--accent)}

/* ===== 4. TIMETABLE AND BLOCKS ===== */
.scroll{overflow-x:auto;margin-top:14px}
table{border-collapse:collapse;width:100%;min-width:640px;table-layout:fixed}
th,td{border:1px solid var(--line);padding:5px;font-size:.8rem;text-align:center;vertical-align:middle}
th{background:var(--head);font-weight:600}
th:first-child{width:100px;position:sticky;left:0;z-index:1;box-shadow:1px 0 0 var(--line)}/* time column stays visible when scrolling sideways */
th.time{height:72px;font-weight:400;color:var(--muted)}
.blk{display:flex;flex-direction:column;justify-content:center;align-items:center;border:1px solid;border-radius:6px;padding:6px 8px;text-align:center;font-size:var(--fs-block);line-height:1.35;overflow-wrap:anywhere}
td .blk{min-height:60px}
.blk.class{background:var(--class-bg);border-color:var(--class-line);color:var(--class-ink)}
.blk.consult{background:var(--consult-bg);border-color:var(--consult-line);color:var(--consult-ink)}
.blk.hit{box-shadow:0 0 0 2px var(--accent)}
.first{font-weight:700}
.list{margin-top:12px}
.lrow{display:flex;align-items:center;gap:16px;padding:10px 0;border-top:1px solid var(--line)}
.lwhen{flex:none;width:130px;text-align:center}
.lrow .blk{flex:1;max-width:260px}
.sub{color:var(--muted);font-size:var(--fs-small)}
.empty{margin:0;padding:28px 8px;text-align:center;color:var(--muted)}
@media (max-width:600px){.logo{width:64px;height:64px}.lwhen{width:104px}}
</style>
</head>
<body>
<div class="banner" id="banner" hidden></div>
<header class="top">
  <div class="wrap">
    <div class="brand">
      <div class="logo" id="logo" hidden></div>
      <div>
        <!-- PAGE WORDING: edit the three texts below -->
        <p class="eyebrow">Read-only</p>
        <h1>CBMES Faculty Schedules</h1>
        <p class="lead">School of Chemical, Biological and Materials Engineering and Sciences. Class and consultation schedules published by the department. No sign-in required.</p>
      </div>
    </div>
    <p class="termrow"><span class="pill" id="term"></span><span id="upd"></span></p>
    <div id="note"></div>
  </div>
</header>

<main class="wrap">
  <noscript><p class="note">This page needs JavaScript turned on to show the schedules.</p></noscript>
  <div class="layout">
    <section class="panel">
      <h2 class="ph">Faculty</h2>
      <div class="searches">
        <input id="qn" type="search" maxlength="60" autocomplete="off" spellcheck="false" placeholder="Search instructor" aria-label="Search instructor name">
        <input id="qc" type="search" maxlength="30" autocomplete="off" spellcheck="false" placeholder="Search course code" aria-label="Search course code">
      </div>
      <div class="faculty" id="faculty"></div>
    </section>

    <section class="panel" id="schedpanel">
      <div class="tools" id="tools" hidden>
        <div class="legend"><span class="sw class"></span>Class<span class="sw consult"></span>CNSLT = Consultation hours</div>
        <div class="segs" role="group" aria-label="View">
          <button class="seg" type="button" data-v="grid">Timetable</button>
          <button class="seg" type="button" data-v="list">List</button>
        </div>
      </div>
      <div id="sched"></div>
    </section>
  </div>
</main>

<script>
/* ===== SCHEDULE DATA: edit this part only =====
   name:     "LAST, FIRST (MIDDLE)" (the page sorts professors A to Z by itself)
   email:    the professor's official school email (it is public, so never use a personal address)
   classes:  [day, start, course code, section, room]
   consults: [day, start, room]
   day:      Mon Tue Wed Thu Fri Sat Sun
   start:    07:30  09:00  10:30  12:00  13:30  15:00  16:30  18:00  19:30
   logo:     file name of the department logo, e.g. "logo.png" (upload it next to this file)
   banner:   file name of the top banner, e.g. "banner.jpg" (upload it next to this file)
   Mistakes (wrong day or time, two entries in one block) are listed in the browser console (F12). */
const DATA = {
  logo: "",
  banner: "",
  term: "2nd Term, AY 2026–2027",
  updated: "2026-11-03",
  sample: true,
  profs: [
    { name: "ALMENDRALA, MICHELLE (CARAVANA)",
      classes: [["Tue","12:00","CM011","A14","NW300"],["Thu","12:00","CM011","A14","NW300"],["Sat","12:00","CM011","A14","ONLINE"],["Sat","7:30","MATH621","D01","ONLINE"],["Sat","7:30","MATH621","D01","ONLINE"]],
      consults: [["Fri","13:30","NW12A"]] },
    { name: "Bautista, Joel (Mendoza)",
      classes: [["Mon","10:30","BEN137P","A21","NW10C"],["Wed","10:30","BEN137P","A21","NW10C"],["Fri","10:30","BEN137P","A21","ONLINE"],["Mon","18:00","BEN174P","C21","NW10C"],["Wed","16:30","BEN174P","C21","NW10B"],["Wed","18:00","BEN174P","C21","NW10B"],["Fri","16:30","BEN174P","C21","ONLINE"]],
      consults: [["Tue","13:30","NW10A"],["Thu","15:00","ONLINE"]] },
    { name: "Dela Cruz, Liza (Santos)",
      classes: [["Tue","19:30","ME133-3","B1","ONLINE"],["Sat","15:00","ME133-3","B1","N101"],["Sat","16:30","ME133-3","B1","N101"]],
      consults: [["Wed","12:00","N101"],["Thu","13:30","N101"]] },
    { name: "Dizon, Rafael (Lim)",
      classes: [["Mon","09:00","CHE220","D11","W305"],["Thu","09:00","CHE220","D11","W305"],["Tue","13:30","CHE220L","D12","LAB4"],["Thu","13:30","CHE220L","D12","LAB4"]],
      consults: [["Mon","13:30","W305"]] },
    { name: "Garcia, Elena (Torres)",
      classes: [["Thu","07:30","EE22L-2","B3","N200B"],["Thu","09:00","EE22L-2","B3","N200B"],["Thu","10:30","EE22L-2","B3","N200B"]],
      consults: [["Mon","15:00","N200A"]] },
    { name: "Villanueva, Paolo (Garcia)",
      classes: [["Tue","07:30","MSE101","E31","NW11A"],["Fri","07:30","MSE101","E31","NW11A"],["Wed","13:30","MSE101L","E32","LAB2"]],
      consults: [["Thu","12:00","NW11A"],["Sat","09:00","ONLINE"]] }
  ]
};
/* ===== end of data ===== */

/* ===== WORDING: short labels used inside the blocks ===== */
const CONSULT_LABEL = "CNSLT";

const DAYS = ["Mon","Tue","Wed","Thu","Fri","Sat","Sun"];
const ABBR = ["M","T","W","TH","F","S","SU"];          // column headings of the timetable
const FULL = ["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"];
const STARTS = ["07:30","09:00","10:30","12:00","13:30","15:00","16:30","18:00","19:30"];
const ENDS = STARTS.slice(1).concat("21:00");           // blocks are 1 hour 30 minutes long
const EMAIL = /^[^\s@<>?&"']+@[^\s@<>?&"']+\.[^\s@<>?&"']+$/;
const $ = id => document.getElementById(id);
const norm = s => String(s).toLowerCase().replace(/[^a-z0-9]/g, "");

/* Pages are built with textContent only, never innerHTML, so schedule text can never run as code. */
function el(tag, cls, text) {
  const e = document.createElement(tag);
  if (cls) e.className = cls;
  if (text != null) e.textContent = text;
  return e;
}

/* TIME FORMAT: shows 7:30 AM. For 24-hour time, replace the body with: return t; */
function fmt(t) {
  const h = +t.slice(0, 2);
  return (h % 12 || 12) + ":" + t.slice(3) + (h >= 12 ? " PM" : " AM");
}
function span(start) { return fmt(start) + " - " + fmt(ENDS[STARTS.indexOf(start)]); }

/* Prepare professors once: alphabetical, with a lowercase last name for search ranking */
const profs = DATA.profs.map(p => ({
  name: p.name,
  classes: p.classes || [],
  consults: p.consults || [],
  last: p.name.split(",")[0].trim().toLowerCase(),
  find: p.name.toLowerCase().replace(/[,()]/g, " "),
  codes: (p.classes || []).map(c => norm(c[2]))
})).sort((a, b) => a.name.localeCompare(b.name));

/* Helps the person editing: lists bad entries in the browser console (F12) */
(function checkData() {
  profs.forEach(p => {
    const seen = {};
    p.consults.concat(p.classes).forEach(c => {
      const key = c[0] + c[1];
      if (!DAYS.includes(c[0]) || !STARTS.includes(c[1])) console.warn("Skipped, invalid day or start time:", p.name, c[0], c[1]);
      else if (seen[key]) console.warn("Two entries share one block:", p.name, c[0], c[1]);
      seen[key] = 1;
    });
  });
})();

/* Name search: every word must match somewhere; last-name matches rank first
   0 exact last name, 1 last name starts with, 2 a last-name word starts with,
   3 inside the last name, 4 first or middle name only */
function rank(p, tokens) {
  if (!tokens.every(t => p.find.includes(t))) return -1;
  let best = 4;
  tokens.forEach(t => {
    let r = 4;
    if (p.last === t) r = 0;
    else if (p.last.startsWith(t)) r = 1;
    else if (p.last.split(" ").some(w => w.startsWith(t))) r = 2;
    else if (p.last.includes(t)) r = 3;
    if (r < best) best = r;
  });
  return best;
}

function matches() {
  const tokens = $("qn").value.toLowerCase().split(/[\s,]+/).filter(Boolean);
  const code = norm($("qc").value);
  return profs
    .map(p => ({ p: p, r: tokens.length ? rank(p, tokens) : 0 }))
    .filter(x => x.r >= 0 && (!code || x.p.codes.some(c => c.includes(code))))
    .sort((a, b) => a.r - b.r || a.p.name.localeCompare(b.p.name))
    .map(x => x.p);
}

function counts(p) {
  const n = p.classes.length, m = p.consults.length;
  return n + (n === 1 ? " class" : " classes") + " · " + m + (m === 1 ? " consultation" : " consultations");
}

/* Consultations go in first so a class always wins if two entries share a block */
function entries(p) {
  const out = [];
  p.consults.forEach(c => out.push({ day: c[0], start: c[1], kind: "consult", lines: [CONSULT_LABEL, c[2]] }));
  p.classes.forEach(c => out.push({ day: c[0], start: c[1], kind: "class", lines: [c[2], c[3], c[4]] }));
  return out.filter(e => DAYS.includes(e.day) && STARTS.includes(e.start));
}

function block(e, code) {
  const hit = code && e.kind === "class" && norm(e.lines[0]).includes(code);
  const b = el("div", "blk " + e.kind + (hit ? " hit" : ""));
  e.lines.filter(Boolean).forEach((t, i) => b.appendChild(el("div", i === 0 ? "first" : null, t)));
  return b;
}

function timetable(p, code) {
  const map = {};
  entries(p).forEach(e => { map[e.day + e.start] = e; });
  const table = el("table");
  const head = el("tr");
  ["Time"].concat(ABBR).forEach(h => head.appendChild(el("th", null, h)));
  table.appendChild(el("thead")).appendChild(head);
  const body = el("tbody");
  STARTS.forEach(s => {
    const row = el("tr");
    const th = el("th", "time");
    th.scope = "row";
    th.appendChild(el("div", null, fmt(s)));
    th.appendChild(el("div", null, fmt(ENDS[STARTS.indexOf(s)])));
    row.appendChild(th);
    DAYS.forEach(d => {
      const td = el("td");
      if (map[d + s]) td.appendChild(block(map[d + s], code));
      row.appendChild(td);
    });
    body.appendChild(row);
  });
  table.appendChild(body);
  const wrap = el("div", "scroll");
  wrap.appendChild(table);
  return wrap;
}

function listView(p, code) {
  const box = el("div", "list");
  const es = entries(p).sort((a, b) => DAYS.indexOf(a.day) - DAYS.indexOf(b.day) || a.start.localeCompare(b.start));
  if (!es.length) box.appendChild(el("p", "empty", "No sessions listed."));
  es.forEach(e => {
    const row = el("div", "lrow");
    const when = el("div", "lwhen");
    when.appendChild(el("strong", null, FULL[DAYS.indexOf(e.day)]));
    when.appendChild(el("div", "sub", span(e.start)));
    row.appendChild(when);
    row.appendChild(block(e, code));
    box.appendChild(row);
  });
  return box;
}

function profSection(p, code) {
  const s = el("section", "prof");
  s.appendChild(el("h2", "pname", p.name));
  s.appendChild(el("p", "psub", DATA.term + " · " + counts(p)));
  s.appendChild(view === "grid" ? timetable(p, code) : listView(p, code));
  return s;
}

let shown = [];     // professors matching the current searches
let sel = null;     // null, "all", or one professor
/* Phones start in List view (easier to read); larger screens start in Timetable view */
let view = window.matchMedia("(max-width: 700px)").matches ? "list" : "grid";

function row(title, sub, value) {
  const b = el("button", "row");
  b.type = "button";
  b._sel = value;
  b.appendChild(el("span", "rt", title));
  b.appendChild(el("span", "rs", sub));
  b.addEventListener("click", () => {
    sel = sel === value ? null : value;
    refresh();
    if (sel && window.matchMedia("(max-width: 899px)").matches) {
      const calm = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
      $("schedpanel").scrollIntoView({ behavior: calm ? "auto" : "smooth", block: "start" });
    }
  });
  return b;
}

function renderList() {
  const box = $("faculty");
  box.replaceChildren();
  if (!shown.length) { box.appendChild(el("p", "empty", "No faculty match your search.")); return; }
  box.appendChild(row("Display all", shown.length + (shown.length === 1 ? " faculty member" : " faculty members"), "all"));
  shown.forEach(p => box.appendChild(row(p.name, counts(p), p)));
}

function refresh() {
  document.querySelectorAll("#faculty .row").forEach(b => b.setAttribute("aria-pressed", String(b._sel === sel)));
  document.querySelectorAll(".seg").forEach(b => b.setAttribute("aria-pressed", String(b.dataset.v === view)));
  const show = sel === "all" ? shown : sel ? [sel] : [];
  const out = $("sched");
  out.replaceChildren();
  $("tools").hidden = !show.length;
  if (!show.length) {
    out.appendChild(el("p", "empty", "Select a faculty member to view their schedule, or choose Display all."));
    return;
  }
  const code = norm($("qc").value);
  const frag = document.createDocumentFragment();   // build off-screen, then add once (faster for Display all)
  show.forEach(p => frag.appendChild(profSection(p, code)));
  out.appendChild(frag);
}

function update() {
  shown = matches();
  if (sel && sel !== "all" && !shown.includes(sel)) sel = null;
  renderList();
  refresh();
}

/* Logo and banner: show the image if one is set; show a dashed placeholder only while sample data is on */
function setImage(box, src, alt, hint) {
  if (src) {
    const img = el("img");
    img.src = src;
    img.alt = alt;
    img.decoding = "async";
    img.addEventListener("error", () => { box.hidden = true; });
    box.appendChild(img);
    box.hidden = false;
  } else if (DATA.sample) {
    box.className += " empty-img";
    box.appendChild(el("span", null, hint));
    box.hidden = false;
  }
}
setImage($("logo"), DATA.logo, "CBMES logo", "Logo");
setImage($("banner"), DATA.banner, "", "Banner image goes here (about 1600 × 300)");

$("term").textContent = DATA.term;
$("upd").textContent = "Updated " + DATA.updated;
if (DATA.sample) $("note").appendChild(el("p", "note", "Sample data only. Replace the schedules in the data section before sharing this page with students."));

/* Wait 150 ms after typing stops before searching, so fast typists do not trigger extra work */
let timer;
const later = () => { clearTimeout(timer); timer = setTimeout(update, 150); };
$("qn").addEventListener("input", later);
$("qc").addEventListener("input", later);
document.querySelectorAll(".seg").forEach(b => b.addEventListener("click", () => { view = b.dataset.v; refresh(); }));
update();
</script>
</body>
</html>
