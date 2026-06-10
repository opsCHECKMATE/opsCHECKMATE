<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
@import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Rajdhani:wght@400;600;700&family=Orbitron:wght@400;700;900&display=swap');

:root{
  --cyan:#00F7FF;
  --bg:#05080f;
  --text:#cfe9ff;
  --dim:#6aa9c9;
}

*{margin:0;padding:0;box-sizing:border-box}

body{
  background:var(--bg);
  color:var(--text);
  font-family:'Rajdhani',sans-serif;
  overflow-x:hidden;
}

/* smoother rendering */
*{
  -webkit-font-smoothing:antialiased;
  -moz-osx-font-smoothing:grayscale;
}

/* BACKGROUND */
canvas{
  position:fixed;
  inset:0;
  z-index:0;
  opacity:.35;
}

/* LAYOUT */
.wrapper{
  position:relative;
  z-index:1;
  max-width:900px;
  margin:auto;
  padding:20px;
}

/* HERO */
.hero{
  text-align:center;
  padding:60px 0 30px;
}

.hero-title{
  font-family:'Orbitron';
  font-size:clamp(2rem,5vw,3.2rem);
  color:var(--cyan);
  text-shadow:0 0 20px rgba(0,247,255,.4);
  letter-spacing:.1em;
}

.glow-line{
  font-family:'Share Tech Mono';
  color:var(--dim);
  margin-top:10px;
  font-size:.85rem;
}

/* TYPE */
.typebox{
  margin:25px auto;
  max-width:600px;
  padding:12px 16px;
  border:1px solid rgba(0,247,255,.2);
  background:rgba(0,247,255,.05);
  display:flex;
  gap:10px;
}

.cursor{
  width:8px;
  background:var(--cyan);
  animation:blink .7s infinite;
}

@keyframes blink{50%{opacity:0}}

/* SECTIONS */
.section{
  margin:30px 0;
  padding:22px;
  border-left:2px solid var(--cyan);
  background:rgba(255,255,255,.02);
  border-radius:8px;
}

.title{
  font-family:'Orbitron';
  color:var(--cyan);
  margin-bottom:10px;
  letter-spacing:.05em;
}

/* CHIPS */
.chips{
  display:flex;
  flex-wrap:wrap;
  gap:8px;
}

.chip{
  font-family:'Share Tech Mono';
  font-size:.75rem;
  padding:6px 10px;
  border:1px solid rgba(0,247,255,.25);
  color:var(--cyan);
  background:rgba(0,247,255,.05);
  border-radius:4px;
}

/* STATS */
.stats{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(120px,1fr));
  gap:10px;
}

.card{
  text-align:center;
  padding:14px;
  border:1px solid rgba(0,247,255,.2);
  background:rgba(0,247,255,.03);
}

.num{
  font-size:1.4rem;
  color:var(--cyan);
  font-family:'Orbitron';
}

/* BARS */
.bar{
  margin:10px 0;
}

.bar-top{
  display:flex;
  justify-content:space-between;
  font-size:.85rem;
}

.track{
  height:6px;
  background:#0b1a2b;
}

.fill{
  height:100%;
  width:0;
  background:linear-gradient(90deg,#00BFFF,#00F7FF);
  transition:1.2s ease;
}

/* LIST */
.list{
  display:flex;
  flex-direction:column;
  gap:8px;
}

.item{
  padding:10px;
  border:1px solid rgba(0,247,255,.15);
  background:rgba(0,247,255,.03);
}

/* FOOTER */
footer{
  text-align:center;
  padding:20px;
  font-family:'Share Tech Mono';
  color:var(--dim);
}

/* MOBILE */
@media(max-width:600px){
  .hero-title{font-size:1.8rem}
}
</style>
</head>

<body>

<canvas id="bg"></canvas>

<div class="wrapper">

  <div class="hero">
    <div class="hero-title">opsCHECKMATE</div>
    <div class="glow-line">// Elite Developer • Problem Solver • Architect</div>
  </div>

  <div class="typebox">
    <span style="color:var(--cyan)">~/dev</span>
    <span id="type"></span>
    <span class="cursor"></span>
  </div>

  <div class="section">
    <div class="title">ABOUT</div>
    <p>
      Passionate software developer focused on algorithms, system design, and scalable solutions.
    </p>
  </div>

  <div class="section">
    <div class="title">SKILLS</div>
    <div class="chips" id="skills"></div>
  </div>

  <div class="section">
    <div class="title">STATS</div>
    <div class="stats" id="stats"></div>
  </div>

  <div class="section">
    <div class="title">LANGUAGES</div>
    <div id="bars"></div>
  </div>

</div>

<footer>
  Always improving • Never stopping
</footer>

<script>
/* BACKGROUND */
const c=document.getElementById('bg');
const x=c.getContext('2d');
let w,h;
function resize(){w=c.width=innerWidth;h=c.height=innerHeight}
resize();addEventListener('resize',resize);

let p=[...Array(60)].map(()=>({
x:Math.random()*w,
y:Math.random()*h,
vx:(Math.random()-.5)*.4,
vy:(Math.random()-.5)*.4
}));

function draw(){
x.clearRect(0,0,w,h);
p.forEach(a=>{
a.x+=a.vx;a.y+=a.vy;
if(a.x>w)a.x=0;
if(a.x<0)a.x=w;
if(a.y>h)a.y=0;
if(a.y<0)a.y=h;

x.fillStyle="rgba(0,247,255,.4)";
x.fillRect(a.x,a.y,2,2);
});
requestAnimationFrame(draw);
}
draw();

/* TYPE */
const words=["Developer","Problem Solver","System Builder","Algorithm Thinker"];
let i=0,j=0,del=false;
const t=document.getElementById("type");

function type(){
let w=words[i];
t.textContent=w.substring(0,j);

if(!del && j<w.length){j++}
else if(del && j>0){j--}
else if(j===w.length){del=true;setTimeout(type,1000);return}
else{del=false;i=(i+1)%words.length}

setTimeout(type,del?50:90);
}
type();

/* SKILLS */
["C++","Python","C","DSA","Git","Linux"].forEach(s=>{
let d=document.createElement("div");
d.className="chip";
d.textContent=s;
skills.appendChild(d);
});

/* STATS */
[
["500+","Problems"],
["3","Languages"],
["∞","Learning"]
].forEach(s=>{
stats.innerHTML+=`
<div class="card">
<div class="num">${s[0]}</div>
<div>${s[1]}</div>
</div>`;
});

/* BARS */
[
["C++",90],
["Python",85],
["C",80]
].forEach(b=>{
bars.innerHTML+=`
<div class="bar">
<div class="bar-top"><span>${b[0]}</span><span>${b[1]}%</span></div>
<div class="track"><div class="fill" data-w="${b[1]}"></div></div>
</div>`;
});

setTimeout(()=>{
document.querySelectorAll(".fill").forEach(f=>{
f.style.width=f.dataset.w+"%";
});
},500);
</script>

</body>
</html>
