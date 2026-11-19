<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>แดชบอร์ดงานสำรวจอุบัติเหตุ</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+Thai:wght@400;500;700&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js"></script>
<style>
:root{--bg:#eef2f4;--panel:#fff;--ink:#14232b;--mute:#5d6f78;--line:#d5dee2;--teal:#0f6b6b;--amber:#d99a00;--red:#c2412d}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font-family:"IBM Plex Sans Thai",system-ui,sans-serif;line-height:1.5}
.wrap{max-width:1100px;margin:0 auto;padding:24px 16px 48px}
header{display:flex;flex-wrap:wrap;justify-content:space-between;align-items:end;gap:12px;margin-bottom:20px}
h1{font-size:1.5rem;margin:0}
.sub{color:var(--mute);font-size:.9rem;margin:2px 0 0}
.ctrl{display:flex;gap:6px;flex-wrap:wrap}
button,.file{font:inherit;border:1px solid var(--line);background:var(--panel);color:var(--ink);padding:6px 14px;border-radius:6px;cursor:pointer}
button[aria-pressed=true]{background:var(--teal);border-color:var(--teal);color:#fff}
button:focus-visible,.file:focus-within{outline:2px solid var(--amber);outline-offset:2px}
.file input{position:absolute;opacity:0;width:0}
.kpis{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:12px;margin-bottom:16px}
.kpi{background:var(--panel);border:1px solid var(--line);border-radius:8px;padding:14px 16px}
.kpi b{display:block;font-size:1.9rem;font-weight:700;line-height:1.2}
.kpi span{color:var(--mute);font-size:.85rem}
.kpi.warn b{color:var(--red)}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(320px,1fr));gap:12px}
.card{background:var(--panel);border:1px solid var(--line);border-radius:8px;padding:14px 16px}
.card.wide{grid-column:1/-1}
.card h2{font-size:1rem;margin:0 0 10px}
.chart{position:relative;height:260px}
.card.wide .chart{height:300px}
#msg{background:#fff6e0;border:1px solid var(--amber);border-radius:8px;padding:12px 16px;margin-bottom:16px;display:none}
.ch{display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:8px;margin-bottom:10px}.ch h2{margin:0}
footer{color:var(--mute);font-size:.8rem;margin-top:16px}
</style>
</head>
<body>
<div class="wrap">
<header>
  <div>
    <h1>แดชบอร์ดงานสำรวจอุบัติเหตุ</h1>
    <p class="sub" id="updated">กำลังโหลดข้อมูล…</p>
  </div>
  <div class="ctrl" id="range" role="group" aria-label="ช่วงเวลา">
    <button data-d="7">7 วัน</button>
    <button data-d="30" aria-pressed="true">30 วัน</button>
    <button data-d="90">90 วัน</button>
    <button data-d="0">ทั้งหมด</button>
    <label class="file">เลือกไฟล์ CSV<input type="file" id="file" accept=".csv"></label>
  </div>
</header>

<div id="msg"></div>

<section class="kpis">
  <div class="kpi"><b id="k-cases">–</b><span>จำนวนเคสทั้งหมด</span></div>
  <div class="kpi"><b id="k-cost">–</b><span>ค่าสำรวจภัยรวม (บาท)</span></div>
  <div class="kpi"><b id="k-avg">–</b><span>ค่าสำรวจภัยเฉลี่ยต่อเคส (บาท)</span></div>
  <div class="kpi warn"><b id="k-pending">–</b><span>งานค้าง (ยังไม่ส่งงาน)</span></div>
</section>

<section class="grid">
  <div class="card wide"><div class="ch"><h2 id="daily-title">จำนวนเคสและค่าสำรวจภัย (รายวัน)</h2><div class="ctrl" id="group" role="group" aria-label="จัดกลุ่มข้อมูล"><button data-g="day" aria-pressed="true">รายวัน</button><button data-g="half">ราย 15 วัน</button><button data-g="month">รายเดือน</button></div></div><div class="chart"><canvas id="c-daily"></canvas></div></div>
  <div class="card"><h2>เวลาเกิดเหตุ (รายชั่วโมง)</h2><div class="chart"><canvas id="c-hour"></canvas></div></div>
  <div class="card"><h2>สถานะงาน</h2><div class="chart"><canvas id="c-status"></canvas></div></div>
  <div class="card"><h2>จำนวนเคสตามอัตราค่าสำรวจภัย</h2><div class="chart"><canvas id="c-tier"></canvas></div></div>
</section>
<footer>แสดงเฉพาะข้อมูลสรุป ไม่แสดงเลขที่รับแจ้งหรือเลขกรมธรรม์</footer>
</div>

<script>
// ใส่ลิงก์ CSV จาก Google Sheets (ไฟล์ > แชร์ > เผยแพร่ไปยังเว็บ > เลือกชีต + CSV)
const CSV_URL = "";

const COL = {status:"สถานะ", date:"วันที่ ค.ศ.", time:"เวลาเกิดเหตุ", cost:"ค่าใช้จ่ายสำรวจภัย", pulled:"ดึงข้อมูลเมื่อ"};
const DONE = "ส่งงานแล้ว";
let ALL = [], range = 30, group = "day", charts = {};

function parseCSV(t){
  const rows=[]; let r=[], f="", q=false;
  for(let i=0;i<t.length;i++){
    const c=t[i];
    if(q){ if(c=='"'){ if(t[i+1]=='"'){f+='"';i++} else q=false } else f+=c }
    else if(c=='"') q=true;
    else if(c==',') {r.push(f);f=""}
    else if(c=='\n'){r.push(f);rows.push(r);r=[];f=""}
    else if(c!='\r') f+=c;
  }
  if(f||r.length){r.push(f);rows.push(r)}
  const h=rows.shift().map(s=>s.trim());
  return rows.filter(x=>x.length>1).map(x=>Object.fromEntries(h.map((k,i)=>[k,(x[i]||"").trim()])));
}

function load(text){
  ALL = parseCSV(text).map(o=>({
    status:o[COL.status]||"ไม่ระบุ",
    date:o[COL.date],
    hour:parseInt((o[COL.time]||"").split(":")[0],10),
    cost:Number(String(o[COL.cost]||"0").replace(/,/g,""))||0,
    pulled:o[COL.pulled]
  })).filter(r=>/^\d{4}-\d{2}-\d{2}$/.test(r.date));
  if(!ALL.length) return show("อ่านข้อมูลไม่ได้ ตรวจสอบว่าหัวคอลัมน์ตรงกับชีต (เช่น “วันที่ ค.ศ.”, “ค่าใช้จ่ายสำรวจภัย”)");
  show("");
  const p = ALL.map(r=>r.pulled).filter(Boolean).sort().pop();
  document.getElementById("updated").textContent = "ดึงข้อมูลล่าสุด " + (p||"–");
  render();
}
function show(m){const e=document.getElementById("msg");e.textContent=m;e.style.display=m?"block":"none"}

function render(){
  const last = ALL.map(r=>r.date).sort().pop();
  let rows = ALL;
  if(range){
    const cut = new Date(last); cut.setDate(cut.getDate()-range+1);
    const c = cut.toISOString().slice(0,10);
    rows = ALL.filter(r=>r.date>=c);
  }
  const n=rows.length, sum=rows.reduce((a,r)=>a+r.cost,0);
  const pending=rows.filter(r=>r.status!==DONE).length;
  const fmt=x=>x.toLocaleString("th-TH",{maximumFractionDigits:0});
  k("k-cases",fmt(n)); k("k-cost",fmt(sum)); k("k-avg",n?fmt(sum/n):"–"); k("k-pending",fmt(pending));

  const bk=r=>bucket(r.date); const days=[...new Set(rows.map(bk))].sort();
  document.getElementById("daily-title").textContent="จำนวนเคสและค่าสำรวจภัย ("+GN[group]+")";
  draw("c-daily",{type:"bar",data:{labels:days.map(labelOf),datasets:[
    {label:"จำนวนเคส",data:days.map(d=>rows.filter(r=>bk(r)===d).length),backgroundColor:"#0f6b6b",yAxisID:"y",order:2},
    {label:"ค่าสำรวจภัย (บาท)",data:days.map(d=>rows.filter(r=>bk(r)===d).reduce((a,r)=>a+r.cost,0)),type:"line",borderColor:"#d99a00",backgroundColor:"#d99a00",tension:.25,yAxisID:"y1",order:1}
  ]},options:{maintainAspectRatio:false,scales:{y:{beginAtZero:true,title:{display:true,text:"เคส"}},y1:{beginAtZero:true,position:"right",grid:{drawOnChartArea:false},title:{display:true,text:"บาท"}}}}});

  const hrs=[...Array(24).keys()];
  draw("c-hour",{type:"bar",data:{labels:hrs.map(h=>String(h).padStart(2,"0")+":00"),datasets:[{label:"เคส",data:hrs.map(h=>rows.filter(r=>r.hour===h).length),backgroundColor:"#0f6b6b"}]},options:{maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{beginAtZero:true,ticks:{precision:0}}}}});

  const st={}; rows.forEach(r=>st[r.status]=(st[r.status]||0)+1);
  draw("c-status",{type:"doughnut",data:{labels:Object.keys(st),datasets:[{data:Object.values(st),backgroundColor:Object.keys(st).map(s=>s===DONE?"#0f6b6b":"#c2412d")}]},options:{maintainAspectRatio:false,plugins:{legend:{position:"bottom"}}}});

  const tr={}; rows.forEach(r=>tr[r.cost]=(tr[r.cost]||0)+1);
  const keys=Object.keys(tr).sort((a,b)=>a-b);
  draw("c-tier",{type:"bar",data:{labels:keys.map(x=>fmt(+x)+" บาท"),datasets:[{label:"เคส",data:keys.map(x=>tr[x]),backgroundColor:"#d99a00"}]},options:{maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{beginAtZero:true,ticks:{precision:0}}}}});
}
const GN={day:"รายวัน",half:"ราย 15 วัน",month:"รายเดือน"};
const TM=["ม.ค.","ก.พ.","มี.ค.","เม.ย.","พ.ค.","มิ.ย.","ก.ค.","ส.ค.","ก.ย.","ต.ค.","พ.ย.","ธ.ค."];
function bucket(d){
  if(group==="month") return d.slice(0,7);
  if(group==="half") return d.slice(0,7)+(+d.slice(8,10)<=15?"-01":"-16");
  return d;
}
function labelOf(key){
  if(group==="day") return key;
  const m=TM[+key.slice(5,7)-1]+" "+key.slice(0,4);
  if(group==="month") return m;
  return (key.slice(8)==="01"?"1–15 ":"16–สิ้นเดือน ")+m;
}
function k(id,v){document.getElementById(id).textContent=v}
function draw(id,cfg){ if(charts[id]) charts[id].destroy(); charts[id]=new Chart(document.getElementById(id),cfg) }

document.getElementById("range").addEventListener("click",e=>{
  const b=e.target.closest("button[data-d]"); if(!b) return;
  range=+b.dataset.d;
  document.querySelectorAll("#range button").forEach(x=>x.setAttribute("aria-pressed",x===b));
  if(ALL.length) render();
});
document.getElementById("group").addEventListener("click",e=>{
  const b=e.target.closest("button[data-g]"); if(!b) return;
  group=b.dataset.g;
  document.querySelectorAll("#group button").forEach(x=>x.setAttribute("aria-pressed",x===b));
  if(ALL.length) render();
});
document.getElementById("file").addEventListener("change",e=>{
  const f=e.target.files[0]; if(f) f.text().then(load);
});

if(CSV_URL){
  fetch(CSV_URL).then(r=>r.text()).then(load).catch(()=>show("โหลดข้อมูลจาก Google Sheets ไม่สำเร็จ ตรวจสอบว่าเผยแพร่ชีตเป็น CSV แล้ว"));
}else{
  document.getElementById("updated").textContent = "ยังไม่ได้ตั้งค่า CSV_URL";
  show("ยังไม่ได้ใส่ลิงก์ CSV ในโค้ด (ตัวแปร CSV_URL) ระหว่างนี้กด “เลือกไฟล์ CSV” เพื่อทดลองดูแดชบอร์ดได้เลย");
}
</script>
</body>
</html>
