cat > /mnt/user-data/outputs/README.md << 'ENDOFFILE'
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<style>
  @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Rajdhani:wght@400;600;700&family=Orbitron:wght@400;700;900&display=swap');

  *{margin:0;padding:0;box-sizing:border-box}
  :root{
    --cyan:#00F7FF;
    --cyan2:#00BFFF;
    --dark:#060a0f;
    --dark2:#0a1020;
    --dark3:#0d1830;
    --grid:#0a2040;
    --text:#c8e4ff;
    --dim:#4a7a9b;
  }

  body{
    background:var(--dark);
    color:var(--text);
    font-family:'Rajdhani',sans-serif;
    overflow-x:hidden;
    min-height:100vh;
  }

  canvas#bg{position:fixed;top:0;left:0;width:100%;height:100%;z-index:0;opacity:.35}

  .wrapper{position:relative;z-index:1;max-width:860px;margin:0 auto;padding:0 20px 60px}

  .hero{text-align:center;padding:60px 0 40px;position:relative;overflow:hidden;}
  .hero::before{content:'';position:absolute;inset:-1px;background:radial-gradient(ellipse 70% 60% at 50% 50%, rgba(0,247,255,.06) 0%, transparent 70%);pointer-events:none;}
  .hero-handle{font-family:'Orbitron',monospace;font-size:clamp(2rem,6vw,3.5rem);font-weight:900;letter-spacing:.12em;color:var(--cyan);text-shadow:0 0 24px rgba(0,247,255,.5),0 0 60px rgba(0,247,255,.2);animation:pulseGlow 3s ease-in-out infinite;position:relative;display:inline-block;}
  .hero-handle::after{content:attr(data-text);position:absolute;left:0;top:0;color:var(--cyan2);animation:glitch 6s infinite;clip-path:polygon(0 30%,100% 30%,100% 60%,0 60%);opacity:.4;}
  @keyframes glitch{0%,90%,100%{transform:none;opacity:.4}91%{transform:translate(-2px,1px);opacity:.6}93%{transform:translate(2px,-1px);opacity:.3}95%{transform:translate(-1px,2px);opacity:.6}97%{transform:translate(1px,-2px);opacity:.3}99%{transform:translate(-2px,0);opacity:.5}}
  @keyframes pulseGlow{0%,100%{text-shadow:0 0 24px rgba(0,247,255,.5),0 0 60px rgba(0,247,255,.2)}50%{text-shadow:0 0 40px rgba(0,247,255,.9),0 0 100px rgba(0,247,255,.4),0 0 160px rgba(0,247,255,.1)}}
  .hero-tagline{font-family:'Share Tech Mono',monospace;color:var(--dim);font-size:.85rem;letter-spacing:.25em;margin-top:10px;text-transform:uppercase;}

  .type-container{margin:24px auto;max-width:560px;background:rgba(0,247,255,.04);border:1px solid rgba(0,247,255,.15);border-radius:6px;padding:14px 20px;display:flex;align-items:center;gap:10px;}
  .type-prompt{color:var(--cyan);font-family:'Share Tech Mono',monospace;font-size:.85rem}
  #typeText{font-family:'Share Tech Mono',monospace;font-size:.85rem;color:#7fcfff;flex:1;}
  .cursor{width:8px;height:14px;background:var(--cyan);display:inline-block;animation:blink .7s step-end infinite;vertical-align:middle;margin-left:2px;box-shadow:0 0 6px var(--cyan);}
  @keyframes blink{0%,100%{opacity:1}50%{opacity:0}}

  .section{margin:40px 0;padding:28px 30px;background:rgba(5,15,35,.8);border:1px solid rgba(0,247,255,.1);border-left:3px solid var(--cyan);border-radius:0 8px 8px 0;position:relative;overflow:hidden;animation:fadeSlide .6s ease forwards;opacity:0;}
  @keyframes fadeSlide{to{opacity:1;transform:none}from{opacity:0;transform:translateY(20px)}}
  .section::before{content:'';position:absolute;top:0;left:0;right:0;height:1px;background:linear-gradient(90deg,var(--cyan),transparent);}
  .sec-label{font-family:'Share Tech Mono',monospace;font-size:.7rem;color:var(--cyan);letter-spacing:.3em;text-transform:uppercase;margin-bottom:16px;opacity:.7;}
  .sec-title{font-family:'Orbitron',monospace;font-size:1.1rem;font-weight:700;color:var(--cyan);margin-bottom:18px;letter-spacing:.06em;}

  .skills-grid{display:flex;flex-wrap:wrap;gap:10px;margin-top:6px}
  .skill-chip{background:rgba(0,247,255,.07);border:1px solid rgba(0,247,255,.25);border-radius:4px;padding:8px 14px;font-family:'Share Tech Mono',monospace;font-size:.75rem;color:var(--cyan);letter-spacing:.05em;cursor:default;transition:all .2s;position:relative;overflow:hidden;}
  .skill-chip:hover{background:rgba(0,247,255,.15);border-color:var(--cyan);box-shadow:0 0 14px rgba(0,247,255,.3);transform:translateY(-2px);}

  .bar-item{margin-bottom:14px}
  .bar-meta{display:flex;justify-content:space-between;margin-bottom:6px}
  .bar-name{font-family:'Rajdhani',sans-serif;font-size:.9rem;font-weight:600;color:var(--text)}
  .bar-val{font-family:'Share Tech Mono',monospace;font-size:.75rem;color:var(--cyan)}
  .bar-track{height:6px;background:rgba(0,247,255,.08);border-radius:3px;overflow:hidden;}
  .bar-fill{height:100%;background:linear-gradient(90deg,var(--cyan2),var(--cyan));border-radius:3px;width:0;transition:width 1.4s cubic-bezier(.22,1,.36,1);box-shadow:0 0 8px rgba(0,247,255,.5);}

  .stats-row{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:14px;margin-top:6px}
  .stat-card{background:rgba(0,247,255,.04);border:1px solid rgba(0,247,255,.15);border-radius:8px;padding:18px 16px;text-align:center;position:relative;overflow:hidden;transition:all .25s;}
  .stat-card:hover{border-color:rgba(0,247,255,.5);background:rgba(0,247,255,.09);transform:translateY(-3px);box-shadow:0 8px 30px rgba(0,247,255,.15);}
  .stat-card::after{content:'';position:absolute;bottom:0;left:0;right:0;height:2px;background:linear-gradient(90deg,transparent,var(--cyan),transparent);opacity:0;transition:opacity .25s;}
  .stat-card:hover::after{opacity:1}
  .stat-num{font-family:'Orbitron',monospace;font-size:1.5rem;font-weight:700;color:var(--cyan);display:block;text-shadow:0 0 12px rgba(0,247,255,.4);}
  .stat-lbl{font-family:'Share Tech Mono',monospace;font-size:.65rem;color:var(--dim);letter-spacing:.15em;text-transform:uppercase;margin-top:6px;display:block;}

  .philo-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-top:6px}
  .philo-item{display:flex;align-items:flex-start;gap:10px;padding:14px;background:rgba(0,247,255,.04);border:1px solid rgba(0,247,255,.1);border-radius:6px;transition:all .2s;}
  .philo-item:hover{border-color:rgba(0,247,255,.35);background:rgba(0,247,255,.08);}
  .philo-icon{color:var(--cyan);font-size:1.1rem;flex-shrink:0;margin-top:2px}
  .philo-text{font-family:'Rajdhani',sans-serif;font-size:.95rem;font-weight:600;color:var(--text);line-height:1.4}
  .philo-sub{font-family:'Share Tech Mono',monospace;font-size:.68rem;color:var(--dim);margin-top:3px}

  .focus-list{display:flex;flex-direction:column;gap:10px;margin-top:6px}
  .focus-row{display:flex;align-items:center;gap:12px;padding:12px 16px;background:rgba(0,247,255,.04);border:1px solid rgba(0,247,255,.1);border-radius:6px;cursor:default;transition:all .2s;}
  .focus-row:hover{border-color:rgba(0,247,255,.4);background:rgba(0,247,255,.09);padding-left:22px;box-shadow:inset 3px 0 0 var(--cyan);}
  .focus-dot{width:8px;height:8px;border-radius:50%;background:var(--cyan);flex-shrink:0;box-shadow:0 0 8px var(--cyan);animation:dotPulse 2s ease-in-out infinite;}
  .focus-row:nth-child(2) .focus-dot{animation-delay:.3s}
  .focus-row:nth-child(3) .focus-dot{animation-delay:.6s}
  .focus-row:nth-child(4) .focus-dot{animation-delay:.9s}
  .focus-row:nth-child(5) .focus-dot{animation-delay:1.2s}
  @keyframes dotPulse{0%,100%{box-shadow:0 0 5px var(--cyan)}50%{box-shadow:0 0 14px var(--cyan),0 0 28px rgba(0,247,255,.3)}}
  .focus-label{font-family:'Rajdhani',sans-serif;font-size:.95rem;font-weight:600;color:var(--text)}
  .focus-tag{margin-left:auto;font-family:'Share Tech Mono',monospace;font-size:.65rem;color:var(--cyan);background:rgba(0,247,255,.1);border:1px solid rgba(0,247,255,.2);border-radius:3px;padding:2px 8px;letter-spacing:.1em;}

  .footer{text-align:center;padding:30px 0 0;font-family:'Share Tech Mono',monospace;font-size:.72rem;color:var(--dim);letter-spacing:.15em;border-top:1px solid rgba(0,247,255,.08);margin-top:20px;}
  .footer span{color:var(--cyan)}

  .scanline{position:fixed;top:0;left:0;width:100%;height:3px;background:rgba(0,247,255,.08);animation:scan 5s linear infinite;pointer-events:none;z-index:0;}
  @keyframes scan{0%{top:-3px}100%{top:100%}}

  @media(max-width:600px){
    .philo-grid{grid-template-columns:1fr}
    .hero-handle{font-size:2rem}
    .section{padding:20px 18px}
  }
</style>
</head>
<body>

<canvas id="bg"></canvas>
<div class="scanline"></div>

<div class="wrapper">

  <div class="hero">
    <div class="hero-handle" data-text="opsCHECKMATE">opsCHECKMATE</div>
    <div class="hero-tagline">// Elite Developer · Competitive Programmer · System Architect</div>
  </div>

  <div class="type-container">
    <span class="type-prompt">~/dev $</span>
    <span id="typeText"></span>
    <span class="cursor"></span>
  </div>

  <div class="section" style="animation-delay:.05s">
    <div class="sec-label">// 00 — Identity</div>
    <div class="sec-title">PROFILE.md</div>
    <p style="font-family:'Rajdhani',sans-serif;font-size:1.05rem;line-height:1.8;color:#a8ccdd">
      Highly driven developer obsessed with <span style="color:var(--cyan)">algorithms</span>, <span style="color:var(--cyan)">system design</span>, and high-performance code.
      I turn complex problems into clean, efficient, and scalable solutions. Every line of code is an act of precision.
    </p>
    <div style="margin-top:18px;padding:14px 18px;background:rgba(0,247,255,.05);border-left:2px solid var(--cyan);border-radius:0 4px 4px 0;font-family:'Share Tech Mono',monospace;font-size:.82rem;color:#7fcfff;line-height:2">
      Think deeply &nbsp;→&nbsp; Code clean &nbsp;→&nbsp; Optimize everything &nbsp;→&nbsp; Never stop improving
    </div>
  </div>

  <div class="section" style="animation-delay:.15s">
    <div class="sec-label">// 01 — Arsenal</div>
    <div class="sec-title">SKILLS MATRIX</div>
    <div class="skills-grid" id="skillsGrid"></div>
  </div>

  <div class="section" style="animation-delay:.25s">
    <div class="sec-label">// 02 — Proficiency</div>
    <div class="sec-title">LANGUAGE STATS</div>
    <div id="bars"></div>
  </div>

  <div class="section" style="animation-delay:.35s">
    <div class="sec-label">// 03 — Performance</div>
    <div class="sec-title">DASHBOARD</div>
    <div class="stats-row" id="statsRow"></div>
  </div>

  <div class="section" style="animation-delay:.45s">
    <div class="sec-label">// 04 — Mission</div>
    <div class="sec-title">CORE FOCUS</div>
    <div class="focus-list" id="focusList"></div>
  </div>

  <div class="section" style="animation-delay:.55s">
    <div class="sec-label">// 05 — Mindset</div>
    <div class="sec-title">CODING PHILOSOPHY</div>
    <div class="philo-grid" id="philoGrid"></div>
  </div>

  <div class="footer">
    <span>opsCHECKMATE</span> · Always online · <span>Never stop improving</span>
  </div>

</div>

<script>
const canvas = document.getElementById('bg');
const ctx = canvas.getContext('2d');
let W, H, particles = [];
function resize(){W=canvas.width=window.innerWidth;H=canvas.height=window.innerHeight}
resize();
window.addEventListener('resize',resize);
for(let i=0;i<70;i++){
  particles.push({x:Math.random()*2000,y:Math.random()*2000,vx:(Math.random()-.5)*.4,vy:(Math.random()-.5)*.4,r:Math.random()*1.5+.5,a:Math.random()})
}
function drawCanvas(){
  ctx.clearRect(0,0,W,H);
  particles.forEach(p=>{
    p.x+=p.vx;p.y+=p.vy;
    if(p.x<0)p.x=W;if(p.x>W)p.x=0;
    if(p.y<0)p.y=H;if(p.y>H)p.y=0;
    ctx.beginPath();ctx.arc(p.x,p.y,p.r,0,Math.PI*2);
    ctx.fillStyle=`rgba(0,247,255,${p.a*.6})`;ctx.fill();
  });
  for(let i=0;i<particles.length;i++){
    for(let j=i+1;j<particles.length;j++){
      const dx=particles[i].x-particles[j].x,dy=particles[i].y-particles[j].y;
      const d=Math.sqrt(dx*dx+dy*dy);
      if(d<120){ctx.beginPath();ctx.moveTo(particles[i].x,particles[i].y);ctx.lineTo(particles[j].x,particles[j].y);ctx.strokeStyle=`rgba(0,247,255,${.15*(1-d/120)})`;ctx.lineWidth=.5;ctx.stroke();}
    }
  }
  requestAnimationFrame(drawCanvas);
}
drawCanvas();

const phrases=['Elite Software Developer','Competitive Programmer','Algorithm Enthusiast','Clean Code Architect','Building Scalable Systems','Always Optimizing...'];
let pi=0,ci=0,deleting=false;
const typeEl=document.getElementById('typeText');
function typeLoop(){
  const word=phrases[pi];
  if(!deleting){typeEl.textContent=word.slice(0,++ci);if(ci===word.length){deleting=true;setTimeout(typeLoop,1800);return}}
  else{typeEl.textContent=word.slice(0,--ci);if(ci===0){deleting=false;pi=(pi+1)%phrases.length;setTimeout(typeLoop,400);return}}
  setTimeout(typeLoop,deleting?40:75);
}
typeLoop();

const skills=['C++','Python','C','Java','JavaScript','Git','Linux','VSCode','GitHub','DSA','System Design','OOP','SQL','Bash'];
const sg=document.getElementById('skillsGrid');
skills.forEach(s=>{const d=document.createElement('div');d.className='skill-chip';d.textContent=s;sg.appendChild(d);});

const langs=[{name:'C++',pct:92},{name:'Python',pct:85},{name:'C',pct:80},{name:'Java',pct:68},{name:'JavaScript',pct:60}];
const barCont=document.getElementById('bars');
langs.forEach(l=>{barCont.innerHTML+=`<div class="bar-item"><div class="bar-meta"><span class="bar-name">${l.name}</span><span class="bar-val">${l.pct}%</span></div><div class="bar-track"><div class="bar-fill" data-w="${l.pct}"></div></div></div>`;});
setTimeout(()=>{document.querySelectorAll('.bar-fill').forEach(b=>{b.style.width=b.dataset.w+'%';});},600);

const stats=[{num:'500+',lbl:'Problems Solved'},{num:'3',lbl:'Languages Mastered'},{num:'100%',lbl:'Commit Rate'},{num:'∞',lbl:'Learning Mode'}];
const sr=document.getElementById('statsRow');
stats.forEach(s=>{sr.innerHTML+=`<div class="stat-card"><span class="stat-num">${s.num}</span><span class="stat-lbl">${s.lbl}</span></div>`;});

const focuses=[{label:'Advanced Problem Solving (DSA)',tag:'CORE'},{label:'Competitive Programming',tag:'ACTIVE'},{label:'System Design & Architecture',tag:'DEEP DIVE'},{label:'Real-world Scalable Projects',tag:'BUILDING'},{label:'Performance Optimization',tag:'MASTERY'}];
const fl=document.getElementById('focusList');
focuses.forEach(f=>{fl.innerHTML+=`<div class="focus-row"><div class="focus-dot"></div><span class="focus-label">${f.label}</span><span class="focus-tag">${f.tag}</span></div>`;});

const philos=[{icon:'◈',title:'Readability > Complexity',sub:'Clean code that anyone can follow'},{icon:'◈',title:'Optimization > Hacks',sub:'Real performance, not shortcuts'},{icon:'◈',title:'Consistency > Motivation',sub:'Show up every single day'},{icon:'◈',title:'Practice > Theory',sub:'Ship and iterate relentlessly'}];
const pg=document.getElementById('philoGrid');
philos.forEach(p=>{pg.innerHTML+=`<div class="philo-item"><span class="philo-icon">${p.icon}</span><div><div class="philo-text">${p.title}</div><div class="philo-sub">${p.sub}</div></div></div>`;});
</script>
</body>
</html>
ENDOFFILE
