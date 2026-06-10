/* BACKGROUND */
const c=document.getElementById('bg');
const x=c.getContext('2d');
let w,h;

function resize(){
  w=c.width=innerWidth;
  h=c.height=innerHeight;
}
resize();
addEventListener('resize',resize);

let p=[...Array(60)].map(()=>({
  x:Math.random()*w,
  y:Math.random()*h,
  vx:(Math.random()-.5)*.4,
  vy:(Math.random()-.5)*.4
}));

function draw(){
  x.clearRect(0,0,w,h);
  p.forEach(a=>{
    a.x+=a.vx;
    a.y+=a.vy;

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

/* TYPE EFFECT */
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

/* UI BUILD */
["C++","Python","C","DSA","Git","Linux"].forEach(s=>{
  let d=document.createElement("div");
  d.className="chip";
  d.textContent=s;
  skills.appendChild(d);
});

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
