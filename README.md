# -2
เอาไว้เก็บผลงานทั้งหมดของปวช.2
<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="theme-color" content="#3730a3">
<title>GPA Calculator</title>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}

:root{
  --bg:#f1f5f9;
  --card:#fff;
  --text:#1e293b;
  --muted:#64748b;
  --border:#e2e8f0;
  --primary:#4f46e5;
  --primary-dark:#3730a3;
  --shadow:0 8px 30px rgba(79,70,229,.14);
  --r:14px;
}

body{
  font-family:system-ui,-apple-system,'Noto Sans Thai','Leelawadee',Tahoma,sans-serif;
  background:var(--bg);
  color:var(--text);
  min-height:100vh;
  padding-bottom:90px;
  -webkit-tap-highlight-color:transparent;
}

/* ── Header ───────────────────────────────────────── */
header{
  background:linear-gradient(145deg,#312e81 0%,#4f46e5 55%,#7c3aed 100%);
  padding:50px 20px 70px;
  text-align:center;
  position:relative;
  overflow:hidden;
}
header::before{
  content:'';
  position:absolute;inset:0;
  background:
    radial-gradient(ellipse at 25% 60%,rgba(255,255,255,.07) 0%,transparent 55%),
    radial-gradient(ellipse at 80% 10%,rgba(167,139,250,.25) 0%,transparent 50%);
}
header h1{
  position:relative;
  color:#fff;
  font-size:1.55rem;
  font-weight:700;
  letter-spacing:.3px;
}
header p{
  position:relative;
  color:rgba(255,255,255,.6);
  font-size:.72rem;
  margin-top:4px;
  letter-spacing:2px;
  text-transform:uppercase;
}

/* ── GPA Card ─────────────────────────────────────── */
.gpa-card{
  margin:-50px 15px 0;
  background:var(--card);
  border-radius:20px;
  box-shadow:var(--shadow);
  padding:22px 18px 18px;
}

.gpa-top{
  display:flex;
  align-items:center;
  gap:18px;
}

/* circle */
.circle-wrap{
  position:relative;
  width:116px;height:116px;
  flex-shrink:0;
}
.circle-wrap svg{
  transform:rotate(-90deg);
  overflow:visible;
}
#cBg{
  fill:none;stroke:#f1f5f9;stroke-width:9;
}
#cFg{
  fill:none;
  stroke:var(--primary);
  stroke-width:9;
  stroke-linecap:round;
  /* r=45  C=2π×45=282.74 */
  stroke-dasharray:282.74;
  stroke-dashoffset:282.74;
  transition:stroke-dashoffset .75s cubic-bezier(.4,0,.2,1),stroke .35s;
}
.c-label{
  position:absolute;inset:0;
  display:flex;flex-direction:column;
  align-items:center;justify-content:center;
}
#gpaNum{
  font-size:1.85rem;font-weight:700;
  color:var(--text);
  line-height:1;
  transition:color .35s;
}
.c-sub{
  font-size:.62rem;color:var(--muted);
  margin-top:3px;letter-spacing:1px;
  text-transform:uppercase;
}

/* stats */
.gpa-stats{flex:1;}
.stat-row{display:flex;gap:14px;margin-bottom:10px;}
.stat-num{
  font-size:1.4rem;font-weight:700;
  color:var(--primary);
  transition:color .35s;
}
.stat-lbl{font-size:.68rem;color:var(--muted);}

/* pill */
.pill{
  display:flex;align-items:center;gap:6px;
  border-radius:99px;
  padding:4px 11px 4px 7px;
  font-size:.76rem;font-weight:600;
  transition:background .35s,color .35s;
  background:#f0fdf4;color:#15803d;
  opacity:0;
  transform:translateY(4px);
  transition:opacity .3s,transform .3s,background .3s,color .3s;
}
.pill.show{opacity:1;transform:translateY(0);}
.p-dot{
  width:7px;height:7px;border-radius:50%;
  background:#15803d;
  transition:background .35s;
  flex-shrink:0;
}

/* level bar */
.lvl-bar{
  display:flex;gap:5px;
  margin-top:14px;
}
.lvl{
  flex:1;padding:7px 3px;
  border-radius:8px;text-align:center;
  font-size:.63rem;font-weight:600;
  opacity:.4;
  transition:opacity .3s,box-shadow .3s;
  line-height:1.3;
}
.lvl span{font-size:.56rem;font-weight:400;display:block;margin-top:2px;}
.lvl.on{opacity:1;}

/* ── Content ──────────────────────────────────────── */
.wrap{padding:0 15px;}

.sec{
  font-size:.7rem;font-weight:700;
  color:var(--muted);
  text-transform:uppercase;
  letter-spacing:1.2px;
  margin:22px 0 10px 2px;
}

/* ── Subject card ─────────────────────────────────── */
.sc{
  background:var(--card);
  border:1.5px solid var(--border);
  border-radius:var(--r);
  padding:13px 13px 12px;
  margin-bottom:9px;
  animation:pop .22s cubic-bezier(.4,0,.2,1);
}
@keyframes pop{
  from{opacity:0;transform:scale(.97) translateY(-6px)}
  to  {opacity:1;transform:scale(1)   translateY(0)}
}
.sc-top{
  display:flex;align-items:center;
  gap:8px;margin-bottom:10px;
}
.badge{
  width:25px;height:25px;
  background:linear-gradient(135deg,#4f46e5,#7c3aed);
  border-radius:7px;
  display:grid;place-items:center;
  font-size:.68rem;font-weight:700;color:#fff;
  flex-shrink:0;
}
.name-inp{
  flex:1;min-width:0;
  border:none;outline:none;
  font-size:.87rem;font-weight:500;
  color:var(--text);background:transparent;
  font-family:inherit;
}
.name-inp::placeholder{color:#c7d2fe;}
.del{
  background:none;border:none;cursor:pointer;
  color:#cbd5e1;font-size:.95rem;
  padding:3px 5px;border-radius:6px;
  transition:color .2s,background .2s;
  line-height:1;
}
.del:hover{color:#ef4444;background:#fef2f2;}

.sc-row{display:grid;grid-template-columns:1fr 1fr;gap:8px;}
.field label{
  display:block;
  font-size:.63rem;font-weight:700;
  color:var(--muted);
  text-transform:uppercase;letter-spacing:.6px;
  margin-bottom:4px;
}
select{
  width:100%;
  border:1.5px solid var(--border);
  border-radius:8px;
  padding:8px 26px 8px 10px;
  font-size:.87rem;font-weight:600;
  color:var(--text);background:#fff;
  font-family:inherit;
  cursor:pointer;outline:none;
  -webkit-appearance:none;appearance:none;
  background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='10' height='10' viewBox='0 0 24 24' fill='none' stroke='%2394a3b8' stroke-width='2.5'%3E%3Cpolyline points='6 9 12 15 18 9'/%3E%3C/svg%3E");
  background-repeat:no-repeat;
  background-position:right 9px center;
  transition:border-color .2s;
}
select:focus{border-color:var(--primary);}

/* ── Add btn ──────────────────────────────────────── */
.add-btn{
  width:100%;
  padding:13px;
  border:2px dashed #c7d2fe;
  background:#eef2ff;
  color:var(--primary);
  border-radius:12px;
  font-size:.88rem;font-weight:600;
  cursor:pointer;font-family:inherit;
  transition:all .2s;
  margin-bottom:8px;
}
.add-btn:hover{background:#e0e7ff;border-color:#818cf8;}

/* ── Empty ────────────────────────────────────────── */
.empty{
  text-align:center;padding:26px 20px;
  color:var(--muted);font-size:.88rem;
}
.empty span{font-size:2.4rem;display:block;margin-bottom:7px;}

/* ── Reset btn ────────────────────────────────────── */
.reset-btn{
  width:100%;padding:12px;
  background:none;
  border:1.5px solid var(--border);
  color:var(--muted);
  border-radius:12px;font-size:.83rem;font-weight:500;
  cursor:pointer;font-family:inherit;
  transition:all .2s;margin-top:6px;
}
.reset-btn:hover{background:#fef2f2;border-color:#fca5a5;color:#ef4444;}
</style>
</head>
<body>

<header>
  <h1>🎓 คำนวณ GPA</h1>
  <p>Grade Point Average</p>
</header>

<div class="gpa-card">
  <div class="gpa-top">
    <!-- Progress ring  r=45  C≈282.74 -->
    <div class="circle-wrap">
      <svg width="116" height="116" viewBox="0 0 116 116">
        <circle id="cBg" cx="58" cy="58" r="45"/>
        <circle id="cFg" cx="58" cy="58" r="45"/>
      </svg>
      <div class="c-label">
        <span id="gpaNum">-</span>
        <span class="c-sub">GPA / 4.00</span>
      </div>
    </div>

    <div class="gpa-stats">
      <div class="stat-row">
        <div>
          <div class="stat-num" id="sCr">0</div>
          <div class="stat-lbl">หน่วยกิตรวม</div>
        </div>
        <div>
          <div class="stat-num" id="sSub">0</div>
          <div class="stat-lbl">วิชา</div>
        </div>
      </div>
      <div class="pill" id="pill">
        <span class="p-dot" id="pDot"></span>
        <span id="pTxt"></span>
      </div>
    </div>
  </div>

  <!-- Level indicator -->
  <div class="lvl-bar">
    <div class="lvl" id="lv1" style="background:#f0fdf4;color:#15803d;">≥3.50<span>เกียรตินิยม อ.1</span></div>
    <div class="lvl" id="lv2" style="background:#eff6ff;color:#1d4ed8;">≥3.00<span>เกียรตินิยม อ.2</span></div>
    <div class="lvl" id="lv3" style="background:#fff7ed;color:#c2410c;">≥2.00<span>ผ่านเกณฑ์</span></div>
    <div class="lvl" id="lv4" style="background:#fef2f2;color:#b91c1c;">&lt;2.00<span>ต้องปรับปรุง</span></div>
  </div>
</div>

<div class="wrap">
  <div class="sec">รายวิชา</div>
  <div id="list"></div>
  <button class="add-btn" onclick="addSubject()">＋ เพิ่มวิชา</button>
  <button class="reset-btn" onclick="resetAll()">🗑 ล้างข้อมูลทั้งหมด</button>
</div>

<script>
/* ── Data ─────────────────────────────────────────── */
const GRADES=[
  {l:'A',   v:4.0, c:'#10b981'},
  {l:'B+',  v:3.5, c:'#3b82f6'},
  {l:'B',   v:3.0, c:'#6366f1'},
  {l:'C+',  v:2.5, c:'#f59e0b'},
  {l:'C',   v:2.0, c:'#f97316'},
  {l:'D+',  v:1.5, c:'#f43f5e'},
  {l:'D',   v:1.0, c:'#ef4444'},
  {l:'F',   v:0.0, c:'#9ca3af'},
];
const CREDITS=[1,1.5,2,2.5,3,3.5,4,4.5,5,6];

let subs=[];

function load(){
  try{ subs=JSON.parse(localStorage.getItem('gpa_data')||'[]'); }
  catch(e){ subs=[]; }
}
function save(){ try{ localStorage.setItem('gpa_data',JSON.stringify(subs)); }catch(e){} }

function gObj(l){ return GRADES.find(g=>g.l===l)||GRADES[0]; }

/* ── Render subjects ──────────────────────────────── */
function render(){
  const el=document.getElementById('list');
  if(!subs.length){
    el.innerHTML='<div class="empty"><span>📚</span>กดปุ่มด้านล่างเพื่อเพิ่มวิชาแรก</div>';
    calc(); return;
  }
  el.innerHTML=subs.map((s,i)=>`
    <div class="sc">
      <div class="sc-top">
        <div class="badge">${i+1}</div>
        <input class="name-inp" placeholder="ชื่อวิชา (ไม่บังคับ)"
          value="${escHtml(s.name||'')}"
          oninput="subs[${i}].name=this.value;save()">
        <button class="del" onclick="removeSub(${i})" title="ลบ">✕</button>
      </div>
      <div class="sc-row">
        <div class="field">
          <label>หน่วยกิต</label>
          <select onchange="subs[${i}].credit=parseFloat(this.value);save();calc()">
            ${CREDITS.map(c=>`<option value="${c}"${s.credit==c?' selected':''}>${c}</option>`).join('')}
          </select>
        </div>
        <div class="field">
          <label>เกรด</label>
          <select style="color:${gObj(s.grade).c}"
            onchange="subs[${i}].grade=this.value;this.style.color=gObj(this.value).c;save();calc()">
            ${GRADES.map(g=>`<option value="${g.l}"${s.grade===g.l?' selected':''} style="color:${g.c}">${g.l} = ${g.v.toFixed(1)}</option>`).join('')}
          </select>
        </div>
      </div>
    </div>
  `).join('');
  calc();
}

function escHtml(s){ return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;'); }

/* ── Calculate & update UI ────────────────────────── */
function calc(){
  const totalCr = subs.reduce((a,s)=>a+parseFloat(s.credit||0),0);
  const totalPt = subs.reduce((a,s)=>a+parseFloat(s.credit||0)*gObj(s.grade).v,0);
  const gpa     = totalCr>0 ? totalPt/totalCr : null;

  document.getElementById('sCr').textContent  = totalCr.toFixed(1);
  document.getElementById('sSub').textContent = subs.length;

  const numEl = document.getElementById('gpaNum');
  const fg    = document.getElementById('cFg');
  const pill  = document.getElementById('pill');
  const pDot  = document.getElementById('pDot');
  const pTxt  = document.getElementById('pTxt');
  const C     = 2*Math.PI*45; // 282.74

  // reset levels
  ['lv1','lv2','lv3','lv4'].forEach(id=>{
    const el=document.getElementById(id);
    el.classList.remove('on');
    el.style.boxShadow='none';
  });

  if(gpa===null){
    numEl.textContent='-'; numEl.style.color='var(--text)';
    fg.style.strokeDashoffset=C; fg.style.stroke='var(--primary)';
    pill.classList.remove('show');
    return;
  }

  numEl.textContent=gpa.toFixed(2);

  let color,lvId,txt,bg;
  if     (gpa>=3.5){color='#10b981';lvId='lv1';txt='🏆 เกียรตินิยมอันดับ 1';bg='#f0fdf4';}
  else if(gpa>=3.0){color='#3b82f6';lvId='lv2';txt='⭐ เกียรตินิยมอันดับ 2';bg='#eff6ff';}
  else if(gpa>=2.0){color='#f59e0b';lvId='lv3';txt='✅ ผ่านเกณฑ์';            bg='#fff7ed';}
  else             {color='#ef4444';lvId='lv4';txt='❌ ต้องปรับปรุง GPA';    bg='#fef2f2';}

  numEl.style.color = color;
  fg.style.stroke   = color;
  fg.style.strokeDashoffset = C*(1-Math.min(gpa,4)/4);

  pill.style.background=bg; pill.style.color=color;
  pDot.style.background=color; pTxt.textContent=txt;
  pill.classList.add('show');

  const lvEl=document.getElementById(lvId);
  lvEl.classList.add('on');
  lvEl.style.boxShadow=`0 0 0 2px ${color}`;
}

/* ── Actions ──────────────────────────────────────── */
function addSubject(){
  subs.push({name:'',credit:3,grade:'A'});
  save(); render();
  // scroll to bottom
  setTimeout(()=>window.scrollTo({top:document.body.scrollHeight,behavior:'smooth'}),50);
}

function removeSub(i){
  subs.splice(i,1);
  save(); render();
}

function resetAll(){
  if(!subs.length) return;
  if(confirm('ล้างข้อมูลทั้งหมดใช่ไหม?')){
    subs=[]; save(); render();
  }
}

/* ── Init ─────────────────────────────────────────── */
load();
render();
</script>
</body>
</html>
