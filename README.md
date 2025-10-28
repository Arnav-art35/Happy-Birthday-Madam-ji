
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Happy Birthday Madam Ji — Magical Cake Time</title>
<link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Nunito:wght@300;600;800&display=swap" rel="stylesheet">
<style>
  :root{
    --bg1:#0f172a;
    --accent1:#ff7ab6;
    --accent2:#7afcff;
    --card-bg: #fff8f3;
  }
  html,body{height:100%;margin:0;font-family: 'Nunito', system-ui, sans-serif;background: linear-gradient(180deg,#0f172a 0%, #3a1651 60%); color:#fff; overflow:hidden}
  .center {
    position:absolute; left:50%; top:50%; transform:translate(-50%,-50%); text-align:center;
  }

  /* Colorful header */
  .rainbow-text {
    font-family: 'Pacifico', cursive;
    font-size: clamp(28px, 6vw, 72px);
    background: linear-gradient(90deg, #ff5f7a, #ffb86b, #ffd56b, #7afcff, #7affb0, #d97bff);
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
    text-shadow: 0 6px 24px rgba(0,0,0,0.35);
    letter-spacing: 2px;
    margin: 8px 0 12px;
  }
  .sub {
    font-size: clamp(14px, 2.4vw, 20px);
    color: #ffe8f8;
    margin-bottom: 16px;
    text-shadow: 0 4px 10px rgba(0,0,0,0.28);
  }
  .btn {
    background: linear-gradient(90deg,#ff7ab6,#7afcff);
    border:none;color:#0a0a0a;padding:12px 20px;border-radius:999px;font-weight:700;cursor:pointer;
    box-shadow: 0 8px 30px rgba(0,0,0,0.35);
    transition: transform .18s ease;
  }
  .btn:active{transform:translateY(2px) scale(.995)}
  /* Balloons */
  .balloon {
    position:absolute; width:60px;height:80px;border-radius:60% 60% 60% 60%;
    transform-origin:center bottom;
    animation: floatY 6s ease-in-out infinite;
    box-shadow: inset -6px -8px 16px rgba(255,255,255,0.15), 0 10px 20px rgba(0,0,0,0.25);
  }
  .balloon::after{
    content:""; position:absolute; left:50%; transform:translateX(-50%); top:74%;
    width:2px;height:40px;background:rgba(255,255,255,0.25); filter: blur(.4px);
  }
  @keyframes floatY {
    0%{transform: translateY(0) rotate(-3deg)}
    50%{transform: translateY(-18px) rotate(3deg)}
    100%{transform: translateY(0) rotate(-3deg)}
  }
  /* Scene container */
  #scene{width:100vw;height:100vh;position:relative;overflow:hidden}
  .top-left{position:absolute;left:4vw;top:6vh}
  .top-right{position:absolute;right:4vw;top:6vh}

  /* Cake area */
  .cake-area{position:relative; width:100%; height:60vh; display:flex; align-items:center; justify-content:center; flex-direction:column;}
  .event-title {
    font-family:'Pacifico'; font-size: clamp(20px,4vw,40px); color:#fff; margin-bottom:8px;
    background: linear-gradient(90deg,#ffd27a,#ff7ab6,#c27bff);
    -webkit-background-clip:text;background-clip:text;color:transparent;
  }
  /* Cake */
  .cake {
    position:relative;
    width:360px; max-width:80vw; height:200px; margin-top:14px;
    display:flex; align-items:flex-end; justify-content:center;
    cursor:pointer;
  }
  .cake-layer{
    width:320px; height:140px; border-radius:18px 18px 12px 12px;
    background: linear-gradient(180deg,#f6d0d9,#f0a8c6);
    box-shadow: 0 12px 30px rgba(0,0,0,0.45);
    position:relative;
  }
  .cake-icing{
    position:absolute; top:-22px; left:6px; right:6px; height:44px; border-radius:22px;
    background: linear-gradient(90deg,#fff,#fff6ea);
    box-shadow: inset 0 -6px 10px rgba(0,0,0,0.06);
    z-index:6;
  }
  .candles{position:absolute; top:-42px; left:50%; transform:translateX(-50%); display:flex; gap:14px; z-index:9}
  .candle{
    width:10px;height:36px;background:linear-gradient(180deg,#fff6d6,#ffef9c);border-radius:3px;position:relative;
  }
  .flame{
    width:14px;height:18px;background: radial-gradient(circle at 50% 30%, #ffd86a 0%, #ff8b3b 45%, transparent 50%); border-radius:60% 60% 60% 60%;
    position:absolute; top:-14px; left:50%; transform:translateX(-50%); filter:drop-shadow(0 6px 10px rgba(255,150,50,0.3));
    animation: flicker 500ms infinite;
  }
  .smoke{position:absolute; top:-6px; left:50%; transform:translateX(-50%); opacity:0; pointer-events:none;}
  .smoke svg{filter: blur(1px); opacity:.9}
  @keyframes flicker{
    0%{transform:translateX(-50%) scale(.98)}
    50%{transform:translateX(-48%) scale(1.05)}
    100%{transform:translateX(-50%) scale(.98)}
  }

  /* After celebration text */
  .big-final {
    position: absolute; left:50%; top:50%; transform: translate(-50%,-50%) scale(0.85);
    opacity:0; transition:all .9s ease; text-align:center; z-index:40; pointer-events:none;
  }
  .big-final.show {opacity:1; transform:translate(-50%,-50%) scale(1); }
  .big-final .text {
    font-family:'Pacifico'; font-size: clamp(32px,6vw,80px);
    background: linear-gradient(90deg,#ff8bc6,#ffd56b,#7afcff,#b6ff7a);
    -webkit-background-clip:text;background-clip:text;color:transparent;
    text-shadow: 0 8px 40px rgba(0,0,0,0.45);
  }

  /* Fireworks canvas */
  canvas#fx { position:absolute; inset:0; pointer-events:none; z-index:30; }

  /* Card modal */
  .card-modal { position: absolute; inset:0; display:flex; align-items:center; justify-content:center; z-index:50; background: linear-gradient(180deg, rgba(6,6,15,0.55), rgba(6,6,15,0.75)); opacity:0; pointer-events:none; transition:opacity .35s ease; }
  .card-modal.show { opacity:1; pointer-events:auto }
  .card {
    width: min(880px, 92vw); height:520px; background: linear-gradient(180deg,#fff,#fffef6); border-radius:18px;
    box-shadow: 0 20px 60px rgba(5,5,10,0.6); display:flex; overflow:hidden; transform:translateY(12px);
  }
  .card-side {
    width:33.3333%; padding:28px; box-sizing:border-box; display:flex; flex-direction:column; align-items:center; justify-content:center;
    border-right:1px solid rgba(0,0,0,0.04);
  }
  .card-side:last-child { border-right:none }
  .card-front .front-title {
    font-family:'Pacifico'; font-size: clamp(20px, 3.6vw, 36px); background:linear-gradient(90deg,#ff7ab6,#ffd56b,#7afcff);
    -webkit-background-clip:text;color:transparent; margin-bottom:10px;
  }
  .card-front .emoji { font-size:40px; margin-top:8px; }
  .card-second .cake-svg { width: 80%; height:auto; filter: drop-shadow(0 8px 30px rgba(0,0,0,0.25)); }
  .card-third .wishes { text-align:left; font-size:16px; color:#1b1b1b; line-height:1.45; background: linear-gradient(90deg,#ff7ab6,#ffd56b,#7afcff); -webkit-background-clip:text; color:transparent; padding:12px; border-radius:8px }
  .card-actions { position:absolute; right:18px; top:18px; display:flex; gap:8px; }
  .close-btn { background: rgba(255,255,255,0.95); border:none; padding:10px 14px; border-radius:999px; cursor:pointer; box-shadow:0 6px 18px rgba(0,0,0,0.2) }
  .next-btn { background: linear-gradient(90deg,#7afcff,#ff7ab6); color:#051426; border:none; padding:10px 14px; border-radius:999px; cursor:pointer; box-shadow:0 6px 20px rgba(0,0,0,0.2) }

  /* small footer note */
  .note { position:absolute; bottom:12px; left:50%; transform:translateX(-50%); font-size:13px; color: #ffdfee; opacity:0.9 }
  @media (max-width:900px){
    .card{height:86vh; flex-direction:column}
    .card-side{width:100%; height:33.333%; border-right:none; border-bottom:1px solid rgba(0,0,0,.06)}
    .card-side:last-child{border-bottom:none}
    .card-actions{position:fixed; right:10px; top:10px}
  }
</style>
</head>
<body>
<div id="scene">
  <!-- Balloons floating -->
  <div class="balloon" style="left:6vw; top:20vh; background:linear-gradient(180deg,#ff7ab6,#ffb3e2); transform: rotate(-8deg); animation-duration:5s;"></div>
  <div class="balloon" style="left:20vw; top:14vh; background:linear-gradient(180deg,#7afcff,#7ab8ff); animation-duration:6s;"></div>
  <div class="balloon" style="right:10vw; top:22vh; background:linear-gradient(180deg,#ffd56b,#ff7a7a); animation-duration:7.2s;"></div>
  <div class="balloon" style="right:24vw; top:12vh; background:linear-gradient(180deg,#b6ff7a,#7effd8); animation-duration:5.6s;"></div>

  <div class="center top-left" style="left:50%; transform:translate(-50%, -44vh);">
    <div class="rainbow-text">HAPPY BIRTHDAY MADAM JI</div>
    <div class="sub">Make a wish — magical moments ahead 🎈</div>
    <button id="startBtn" class="btn">Start Magical Cake Time</button>
  </div>

  <div class="center cake-area" style="top:52%;">
    <div class="event-title" id="eventTitle">Magical Cake Time</div>
    <div class="cake" id="cake" title="Click cake to blow out candles">
      <div class="cake-layer" id="cakeLayer">
        <div class="cake-icing"></div>
        <!-- candles -->
        <div class="candles" id="candles">
          <div class="candle"><div class="flame"></div></div>
          <div class="candle"><div class="flame"></div></div>
          <div class="candle"><div class="flame"></div></div>
        </div>
      </div>
    </div>
    <div style="margin-top:8px;color:#ffe8f8;font-size:14px">Click the cake to blow the candles!</div>
  </div>

  <!-- Fireworks canvas -->
  <canvas id="fx"></canvas>

  <!-- Final big greeting -->
  <div class="big-final" id="finalMsg" aria-hidden="true">
    <div class="text">HAPPY BIRTHDAY MADAM JI 💐</div>
  </div>

  <!-- Card modal -->
  <div class="card-modal" id="cardModal" role="dialog" aria-hidden="true">
    <div class="card" role="document">
      <div class="card-side card-front" id="cardFront">
        <div class="front-title">HAPPY BIRTHDAY CUTIE 🎂</div>
        <div style="font-size:16px;color:#333;margin-top:10px">A small card from someone special 💖</div>
      </div>
      <div class="card-side card-second">
        <!-- SVG cake picture -->
        <svg class="cake-svg" viewBox="0 0 200 160" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
          <defs>
            <linearGradient id="g1" x1="0" x2="1">
              <stop offset="0" stop-color="#ffd56b"/><stop offset="1" stop-color="#ff7ab6"/>
            </linearGradient>
            <linearGradient id="g2" x1="0" x2="1">
              <stop offset="0" stop-color="#ffffff"/><stop offset="1" stop-color="#fff6ea"/>
            </linearGradient>
          </defs>
          <rect x="18" y="70" width="164" height="64" rx="10" fill="url(#g1)" stroke="#d16c9c" stroke-opacity="0.2"/>
          <ellipse cx="100" cy="72" rx="82" ry="16" fill="url(#g2)" />
          <rect x="44" y="40" width="112" height="32" rx="8" fill="#ffe8f0" />
          <!-- candles -->
          <g transform="translate(40,20)">
            <rect x="10" y="30" width="6" height="24" fill="#fff7c6" />
            <circle cx="13" cy="26" r="7" fill="#ffd86a"/>
            <rect x="46" y="30" width="6" height="24" fill="#fff7c6" />
            <circle cx="49" cy="26" r="7" fill="#ffb86b"/>
            <rect x="82" y="30" width="6" height="24" fill="#fff7c6" />
            <circle cx="85" cy="26" r="7" fill="#ff8b3b"/>
          </g>
        </svg>
        <div style="margin-top:14px;color:#222;font-weight:600">Cake — made with love 🍰</div>
      </div>
      <div class="card-side card-third">
        <div style="font-weight:700;color:#222;margin-bottom:10px">My Wishes</div>
        <div class="wishes" id="wishesText">
Hyee ✨ . Wish you the “Happiest Birthday ever” !🎂 You make every day brighter just by being you .💐 Hope your day is as amazing as your smile !😊 You’re a rare kind of magic, 🪄 and I hope your birthday shines just as beautifully as you do.👰 May LORD KRISHNA bless you .🍀
        </div>
      </div>
      <div class="card-actions">
        <button id="closeCard" class="close-btn" title="Close">Close</button>
      </div>
    </div>
  </div>

  <div class="note">Tip: Click the cake to blow candles → enjoy fireworks → then open the card.</div>
</div>

<script>
/* Basic scene flow */
const startBtn = document.getElementById('startBtn');
const eventTitle = document.getElementById('eventTitle');
const cake = document.getElementById('cake');
const candles = document.getElementById('candles');
const flames = document.querySelectorAll('.flame');
const smokeEls = [];
const finalMsg = document.getElementById('finalMsg');
const fxCanvas = document.getElementById('fx');
const cardModal = document.getElementById('cardModal');
const closeCard = document.getElementById('closeCard');

let candlesLit = true;
let fireworksActive = false;
let fxCtx, fxW, fxH, particles = [];

/* Resize canvas */
function resizeFx(){
  fxW = fxCanvas.width = window.innerWidth;
  fxH = fxCanvas.height = window.innerHeight;
  fxCtx = fxCanvas.getContext('2d');
}
window.addEventListener('resize', resizeFx);
resizeFx();

/* helper: create smoke SVG for each candle (hidden initially) */
function makeSmoke(){
  candles.querySelectorAll('.candle').forEach((c, i) => {
    const s = document.createElementNS('http://www.w3.org/2000/svg', 'svg');
    s.setAttribute('width','40'); s.setAttribute('height','60'); s.style.position='absolute';
    s.style.left = (i*24 - 8) + 'px'; s.style.top = '-40px'; s.style.opacity = '0';
    s.innerHTML = `
      <g fill="none" stroke="rgba(200,200,210,0.5)" stroke-width="2" stroke-linecap="round">
        <path d="M10 40 C 6 30, 18 20, 10 10" stroke-opacity="0.8" />
        <path d="M20 40 C 14 30, 26 20, 20 10" stroke-opacity="0.6" />
      </g>
    `;
    c.appendChild(s);
    smokeEls.push(s);
  });
}
makeSmoke();

/* start button */
startBtn.addEventListener('click', () => {
  // small animation: hide header and move attention to cake
  document.querySelector('.center.top-left').style.transition = 'all .7s ease';
  document.querySelector('.center.top-left').style.transform = 'translate(-50%, -64vh) scale(.96)';
  document.querySelector('.center.top-left').style.opacity = '0.92';
  // highlight event title
  eventTitle.style.transform = 'translateY(-6px)';
  eventTitle.style.textShadow = '0 12px 40px rgba(0,0,0,0.5)';
});

/* cake click = blow candles */
cake.addEventListener('click', async () => {
  if(!candlesLit) return;
  candlesLit = false;
  // animate flames disappearing & show smoke
  flames.forEach((f, idx) => {
    f.style.transition = 'all .9s ease';
    f.style.transform = 'scale(.1) translateY(-8px)';
    f.style.opacity = '0';
  });
  smokeEls.forEach((s, i) => {
    s.style.transition = 'all 1.2s ease';
    s.style.opacity = '1';
    s.animate([{ transform:'translateY(0) scale(0.9)', opacity:1 }, { transform:'translateY(-40px) scale(1.4)', opacity:0 }], { duration:2200, easing:'cubic-bezier(.2,.8,.2,1)'});
  });

  // small "puff" sound effect (optional using webapi)
  try {
    const ctx = new (window.AudioContext || window.webkitAudioContext)();
    const o = ctx.createOscillator();
    const g = ctx.createGain();
    o.type='triangle'; o.frequency.setValueAtTime(600, ctx.currentTime);
    g.gain.setValueAtTime(0.0001, ctx.currentTime);
    o.connect(g); g.connect(ctx.destination);
    g.gain.exponentialRampToValueAtTime(0.1, ctx.currentTime + 0.01);
    g.gain.exponentialRampToValueAtTime(0.0001, ctx.currentTime + 0.25);
    o.start(); o.stop(ctx.currentTime + 0.28);
  } catch(e){ /* ignore audio errors */ }

  // wait a bit, then start fireworks
  await new Promise(r => setTimeout(r, 900));
  startFireworks(6);
  // show final message after a delay
  setTimeout(()=> {
    finalMsg.classList.add('show');
    // small pop
    document.body.animate([{filter:'brightness(1)'},{filter:'brightness(1.06)'}],{duration:700,iterations:1, easing:'ease-out'});
  }, 1500);

  // after fireworks, open card modal automatically
  setTimeout(()=> {
    openCard();
  }, 4800);
});

/* Fireworks particle system */
function rand(min,max){return Math.random()*(max-min)+min}
function startFireworks(count=5){
  fireworksActive = true;
  // spawn several bursts
  for(let i=0;i<count;i++){
    setTimeout(()=> spawnBurst(rand(0.15*fxW,0.85*fxW), rand(0.08*fxH,0.5*fxH), Math.floor(rand(28,48)) ), i*420);
  }
  // run draw loop
  let t0 = performance.now();
  function loop(now){
    const dt = now - t0; t0 = now;
    fxCtx.clearRect(0,0,fxW,fxH);
    // subtle background glows (optional)
    for(let i=particles.length-1;i>=0;i--){
      const p = particles[i];
      p.vx *= 0.995;
      p.vy += 0.08;
      p.x += p.vx * (dt/16);
      p.y += p.vy * (dt/16);
      p.life -= (dt/16) * 0.7;
      const alpha = Math.max(0, p.life/ p.maxLife);
      fxCtx.beginPath();
      fxCtx.fillStyle = `rgba(${p.color.r},${p.color.g},${p.color.b},${alpha})`;
      fxCtx.arc(p.x, p.y, p.size * (0.6 + alpha*0.8), 0, Math.PI*2);
      fxCtx.fill();
      if(p.life<=0 || p.y>fxH+30) particles.splice(i,1);
    }
    if(fireworksActive && particles.length>0) requestAnimationFrame(loop);
  }
  requestAnimationFrame(loop);
}
/* spawn one burst */
function spawnBurst(x,y, num){
  const baseHue = Math.floor(rand(0,360));
  for(let i=0;i<num;i++){
    const angle = rand(0,Math.PI*2);
    const speed = rand(1.8,6.6);
    const color = hsvToRgb(baseHue + rand(-20,20), rand(60,100), rand(70,100));
    particles.push({
      x,y,
      vx: Math.cos(angle)*speed,
      vy: Math.sin(angle)*speed,
      life: rand(50,120),
      maxLife: rand(60,140),
      size: rand(1.2,3.8),
      color
    });
  }
}
/* HSV -> RGB helper (returns obj) */
function hsvToRgb(h,s,v){
  s/=100; v/=100;
  const k = (n)=> (n + h/60) % 6;
  const f = (n)=> v - v*s*Math.max(Math.min(k(n),4 - k(n),1),0);
  // approximate via formula simpler: convert using standard algorithm
  let c = v*s;
  let x = c*(1 - Math.abs((h/60)%2 -1));
  let m = v - c;
  let r=0,g=0,b=0;
  if(h<60){ r=c; g=x; b=0 }
  else if(h<120){ r=x; g=c; b=0 }
  else if(h<180){ r=0; g=c; b=x }
  else if(h<240){ r=0; g=x; b=c }
  else if(h<300){ r=x; g=0; b=c }
  else { r=c; g=0; b=x }
  r=Math.round((r+m)*255); g=Math.round((g+m)*255); b=Math.round((b+m)*255);
  return {r,g,b};
}

/* Card logic */
function openCard(){
  cardModal.classList.add('show');
  cardModal.setAttribute('aria-hidden','false');
}
function closeCardFunc(){
  cardModal.classList.remove('show');
  cardModal.setAttribute('aria-hidden','true');
}
closeCard.addEventListener('click', closeCardFunc);

/* also allow click final message to open card */
finalMsg.addEventListener('click', openCard);

/* allow pressing 'c' to open card, or 'r' to restart */
window.addEventListener('keydown', (e)=>{
  if(e.key.toLowerCase()==='c') openCard();
  if(e.key.toLowerCase()==='r') location.reload();
});

/* touch-friendly: also open card if user taps cake after fireworks */
cake.addEventListener('dblclick', () => {
  if(!candlesLit) openCard();
});

/* small accessibility: allow Enter key to start if focused on startBtn */
startBtn.addEventListener('keydown', (e)=>{
  if(e.key==='Enter') startBtn.click();
});

/* Prevent mobile overscroll */
document.addEventListener('touchmove', (e)=>{ /* nothing */ }, {passive:false});

/* End of script */
</script>
</body>
</html>