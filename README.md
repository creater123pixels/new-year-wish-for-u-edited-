<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>A Special New Year ✨</title>

<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Segoe UI',sans-serif}
body{
  background:radial-gradient(circle at top,#060b2c,#000);
  color:white;overflow:hidden;height:100vh
}

/* === DOORS === */
.door{
  position:fixed;top:0;width:50%;height:100%;
  background:linear-gradient(120deg,#020024,#050b40);
  z-index:10;transition:transform 1.6s ease
}
.left{left:0}
.right{right:0}
.open .left{transform:translateX(-100%)}
.open .right{transform:translateX(100%)}

/* === OPEN BUTTON === */
.open-btn{
  position:fixed;inset:0;margin:auto;
  width:220px;height:60px;border-radius:40px;
  background:linear-gradient(90deg,#ffd700,#ff9f1c);
  border:none;font-size:1.1rem;font-weight:600;
  cursor:pointer;z-index:11
}

/* === MAIN CONTENT === */
.container{
  opacity:0;transition:opacity 1.2s ease;
  position:relative;z-index:2;
  max-width:600px;padding:25px;text-align:center;
  margin:auto;top:50%;transform:translateY(-50%)
}
.show{opacity:1}

h1{
  font-size:2.4rem;
  background:linear-gradient(90deg,#ffd700,#ff9f1c);
  -webkit-background-clip:text;
  -webkit-text-fill-color:transparent
}

p{margin-top:18px;font-size:1.05rem;line-height:1.7}

/* === WISH BUTTON === */
.wish-btn{
  margin-top:25px;padding:12px 26px;
  border:none;border-radius:30px;
  background:linear-gradient(90deg,#7df9ff,#5ad);
  color:#000;font-weight:600;cursor:pointer
}

/* === FIREWORKS === */
canvas{position:fixed;inset:0;z-index:1}

/* === CHATBOT === */
.chatbot{
  position:fixed;bottom:15px;right:15px;
  width:280px;background:rgba(255,255,255,.08);
  backdrop-filter:blur(12px);
  border-radius:16px;z-index:5
}
.chat-head{padding:10px;font-weight:600}
.chat-body{height:140px;padding:10px;overflow:auto}
.msg.bot{color:#7df9ff;margin-bottom:8px}
.chat-input{display:flex}
.chat-input input{
  flex:1;background:none;border:none;color:white;padding:8px
}
.chat-input button{
  background:none;border:none;color:#7df9ff;padding:8px
}
/* === CHATBOT GLOW === */
.chatbot{
  background: radial-gradient(circle at top, #0b1d3a, #020617);
  border: 1px solid rgba(120,180,255,.25);
  box-shadow: 0 0 30px rgba(80,140,255,.2);
}

.chat-head{
  font-weight:600;
  color:#cce3ff;
  text-shadow:0 0 8px rgba(120,180,255,.6);
}

/* === BUTTONS === */
.chat-input button{
  background: linear-gradient(135deg,#1e3a8a,#2563eb);
  border:none;
  color:white;
  padding:10px 14px;
  border-radius:20px;
  cursor:pointer;
  box-shadow:0 0 12px rgba(80,140,255,.6);
  transition:.25s;
}

.chat-input button:hover{
  transform:scale(1.05);
  box-shadow:0 0 22px rgba(120,180,255,.9);
}

/* === TYPING EFFECT === */
.msg.bot::after{
  content:"";
  display:inline-block;
  width:6px;height:6px;
  background:#9ecbff;
  border-radius:50%;
  margin-left:6px;
  animation:blink 1.2s infinite;
}
@keyframes blink{
  0%,50%,100%{opacity:1}
  25%,75%{opacity:.2}
}
@media (max-width: 768px){

  /* CHATBOT SIZE */
  .chatbot{
    width:92%;
    max-width:360px;
    right:4%;
    bottom:4%;
    border-radius:18px;
  }

  /* CHAT BODY */
  .chat-body{
    max-height:260px;
    font-size:14px;
    padding:10px;
  }

  /* MESSAGES */
  .msg{
    line-height:1.4;
    padding:8px 12px;
    border-radius:14px;
    max-width:90%;
  }

  /* BUTTON AREA */
  .chat-input{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:8px;
    padding:10px;
  }

  .chat-input button{
    padding:12px 0;
    font-size:14px;
    border-radius:16px;
  }

  /* HEAD */
  .chat-head{
    font-size:15px;
    padding:10px;
  }

  /* WISH TEXT */
  #wishText{
    font-size:16px;
    line-height:1.6;
  }

  /* OPEN BUTTON */
  #openBtn{
    font-size:16px;
    padding:14px 24px;
  }
}
</style>
</head>

<body>

<canvas id="fx"></canvas>

<!-- Doors -->
<div class="door left"></div>
<div class="door right"></div>
<button class="open-btn" id="openBtn">✨ Open ✨</button>

<!-- Content -->
<div class="container" id="content">
  <h1>Happy New Year ✨</h1>
  <p id="wishText"></p>
  <button class="wish-btn" id="wishBtn">My Next Wish (9 left)</button>
</div>

<!-- FactBot 3 InnovEx -->
<div class="chatbot">
  <div class="chat-head">🌌 FactBot 3 InnovEx</div>

  <div class="chat-body" id="chatBody">
    <div class="msg bot">
      Hi 🙂 I’m FactBot 3 InnovEx — tonight, I’m your quiet midnight companion 🌙✨  
      Tap a button below.
    </div>
  </div>

  <div class="chat-input" style="justify-content:space-around">
    <button onclick="sendType('fact')">🧠 Fact</button>
    <button onclick="sendType('joke')">😄 Joke</button>
    <button onclick="sendType('quote')">💬 Quote</button>
    <button onclick="sendType('tip')">🌱 Tip</button>
  </div>
</div>


<script>
/* === WISHES === */
const wishes=[
"Before anything else, I just want you to know this was made with care. Not in a rush — but because you genuinely matter. May this year bring calm, clarity, and quiet confidence.",
"I hope this year treats you gently. That days feel kinder and pressure feels lighter. You deserve peace just as much as success.",
"May this year help you grow naturally — becoming stronger without noticing, and realizing one day how far you’ve come.",
"I hope you always have reasons to feel proud of yourself this year. Even small wins matter. Trying matters.",
"May this year surprise you in good ways — unexpected happiness, laughter, and moments that feel exciting again.",
"I’m really grateful for our friendship. Friends like you make years feel meaningful.",
"I hope you trust yourself more this year. You’re capable of more than you realize.",
"May your days be filled with small joys — music, quiet moments, and peaceful nights.",
"I hope this year gives you opportunities that excite you and challenges that show your strength.",
"As this year unfolds, I hope you feel supported, valued, and hopeful. May this year feel right."
];
let index=0;

/* === OPEN === */
openBtn.onclick=()=>{
  document.body.classList.add('open');
  openBtn.style.display="none";
  setTimeout(()=>{
    content.classList.add('show');
    wishText.textContent=wishes[0];
    startFireworks();
  },1200);
};

/* === NEXT WISH === */
wishBtn.onclick=()=>{
  index++;
  if(index<wishes.length){
    wishText.textContent=wishes[index];
    wishBtn.textContent=`My Next Wish (${wishes.length-index-1} left)`;
  }else{
    wishBtn.style.display="none";
  }
};

/* === FIREWORKS === */
const c=document.getElementById('fx'),ctx=c.getContext('2d');
function resize(){c.width=innerWidth;c.height=innerHeight}
resize();addEventListener('resize',resize);
const p=[];
function fire(){
  for(let i=0;i<60;i++)
    p.push({x:c.width/2,y:c.height*.6,a:Math.random()*6.28,v:2+Math.random()*4,l:80})
}
function animate(){
  requestAnimationFrame(animate);
  ctx.clearRect(0,0,c.width,c.height);
  p.forEach((o,i)=>{
    o.x+=Math.cos(o.a)*o.v;
    o.y+=Math.sin(o.a)*o.v;
    o.l--;
    ctx.fillStyle=`hsla(${o.l*4},100%,60%,.8)`;
    ctx.fillRect(o.x,o.y,2,2);
    if(o.l<=0)p.splice(i,1);
  });
}
function startFireworks(){
  setInterval(fire,900);
  animate();
}

/* === CHATBOT === */
const chatBody = document.getElementById("chatBody");

/* 🧠 FACTS */
const facts = [
  "Some stars you see tonight no longer exist — their light is still traveling 🌌",
  "There are more galaxies in the universe than grains of sand on Earth ✨",
  "A day on Venus is longer than a year on Venus 🪐",
  "Neutron stars are so dense that a spoonful weighs billions of tons 🌠",
  "The universe is still expanding — even right now 🌙",
  "Astronauts grow taller in space because gravity lets the spine relax 🚀"
];

/* 😄 JOKES */
const jokes = [
  "Why did the astronaut break up? They needed space 😄",
  "Why don’t stars gossip? Too much space drama 🌌",
  "I tried to read a book on gravity… couldn’t put it down 🚀"
];

/* 💬 QUOTES */
const quotes = [
  "Quiet moments often mean the most ✨",
  "You’re doing better than you think.",
  "Peace is progress.",
  "Some nights are meant to be gentle 🌙"
];

/* 🌱 TIPS */
const tips = [
  "Take a deep breath — nothing needs to be solved right now.",
  "Rest is productive too 🌱",
  "Drink some water and relax your shoulders 🙂",
  "Being kind to yourself counts as growth."
];
function addBotMsg(text){
  const div=document.createElement("div");
  div.className="msg bot";
  chatBody.appendChild(div);

  let i=0;
  const typing=setInterval(()=>{
    div.textContent+=text.charAt(i);
    i++;
    chatBody.scrollTop=chatBody.scrollHeight;
    if(i>=text.length) clearInterval(typing);
  },30);
}

function sendType(type){
  let reply = "";
  if(type==="fact") reply = facts[Math.floor(Math.random()*facts.length)];
  if(type==="joke") reply = jokes[Math.floor(Math.random()*jokes.length)];
  if(type==="quote") reply = quotes[Math.floor(Math.random()*quotes.length)];
  if(type==="tip") reply = tips[Math.floor(Math.random()*tips.length)];

  setTimeout(()=>addBotMsg(reply), 400);
}
</script>

</body>
</html>
