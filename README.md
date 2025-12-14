<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Birthday Mode</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
*{
  box-sizing:border-box;
  font-family:system-ui, sans-serif;
}
body{
  margin:0;
  min-height:100vh;
  background:linear-gradient(135deg,#020617,#0f172a);
  color:#fff;
  overflow:hidden;
}

/* PAGE TRANSITION */
.page{
  position:absolute;
  inset:0;
  display:flex;
  justify-content:center;
  align-items:center;
  opacity:0;
  transform:translateX(40px);
  transition:all .6s ease;
}
.page.active{
  opacity:1;
  transform:translateX(0);
  z-index:1;
}

/* CARD */
.card{
  width:90%;
  max-width:420px;
  background:#020617;
  border-radius:22px;
  padding:18px;
  border:1px solid #475569;
  box-shadow:0 20px 45px rgba(0,0,0,.7);
  text-align:center;
}

/* IMAGE */
.player-img{
  width:100%;
  border-radius:18px;
  margin-bottom:14px;
  animation:fadeImg .6s ease;
}
@keyframes fadeImg{
  from{opacity:0;transform:scale(1.05)}
  to{opacity:1;transform:scale(1)}
}

h1{
  font-size:1.35rem;
  margin:6px 0;
}
p{
  font-size:.9rem;
  color:#cbd5f5;
  line-height:1.45rem;
}

input{
  width:100%;
  padding:12px;
  border-radius:14px;
  border:none;
  margin-top:12px;
  font-size:1rem;
}

button{
  margin-top:16px;
  width:100%;
  padding:13px;
  border:none;
  border-radius:999px;
  background:#facc15;
  font-size:1rem;
  cursor:pointer;
  box-shadow:0 12px 28px rgba(250,204,21,.55);
}
button:hover{
  transform:translateY(-1px);
}

/* MOODS */
.moods button{
  background:#1e293b;
  color:#fff;
  margin:6px 0;
}

/* FINAL PAGE */
.green{
  background:#041f14;
  border:1px solid #22c55e;
}
.green h1,
.green p{
  color:#22c55e;
}

/* SECRET */
.secret{
  font-size:.8rem;
  color:#94a3b8;
  cursor:pointer;
  margin-top:8px;
}
.reveal{
  display:none;
  color:#f87171;
  margin-top:6px;
}
</style>
</head>

<body>

<!-- PAGE 1 -->
<div class="page active" id="p1">
  <div class="card">
    <img class="player-img" src="_GP26827.jpg">
    <h1>Before anything…</h1>
    <p>Tell me your name 👀</p>
    <input id="nameInput" placeholder="Type your name...">
    <button onclick="toPage2()">Continue</button>
  </div>
</div>

<!-- PAGE 2 -->
<div class="page" id="p2">
  <div class="card">
    <img class="player-img" src="17367646777361.jpeg">
    <h1 id="typing"></h1>

    <p>
      🎉 Birthday unlocked<br>
      🔓 Level up complete<br>
      ⚡ Aura scan in progress…
    </p>

    <p>
      🎂 Celebration: 100%<br>
      🧠 Wisdom: +1<br>
      😏 Confidence: Stable<br>
      🔥 Drama tolerance: Low
    </p>

    <p>
      Thanks for wishing me.<br>
      Now you’re officially part of today.
    </p>

    <button onclick="toPage3()">Next</button>
  </div>
</div>

<!-- PAGE 3 -->
<div class="page" id="p3">
  <div class="card">
    <img class="player-img" src="el-jugador-del-barcelona-raphinha-celebra-despues-de-anotar-un-gol-contra-el-benfica-durante-su-partido-de-la-uefa-champions-league-celebrado-en-el-estadio-da-luz-en-lisboa--portugal--efe-epa-tiago-petinga.jpg">
    <h1>Choose today’s vibe 🎧</h1>

    <div class="moods">
      <button onclick="setMood('Relax. Today is about me 😌')">😎 Chill</button>
      <button onclick="setMood('Birthday glow suits me well 😉')">😏 Flirty</button>
      <button onclick="setMood('Another year older, still unstoppable 🔥')">🔥 Savage</button>
      <button onclick="setMood('Grateful, calm, focused 🧠')">🧠 Deep</button>
    </div>

    <p id="moodText"></p>
    <button onclick="toPage4()">Next</button>
  </div>
</div>

<!-- PAGE 4 -->
<div class="page" id="p4">
  <div class="card">
    <img class="player-img" src="raphinha-mvp-benfica-barca.jpeg">
    <h1>🍰 Birthday Rule</h1>
    <p onclick="cake()" style="cursor:pointer">Tap the cake 🎂</p>
    <p id="cakeText"></p>

    <div class="secret" onclick="revealSecret()">Don’t click this.</div>
    <div class="reveal" id="secretText">
      2026 duniya khatm hai… 16 left.
    </div>

    <button onclick="toPage5()">Final Page</button>
  </div>
</div>

<!-- PAGE 5 -->
<div class="page" id="p5">
  <div class="card green">
    <img class="player-img" src="raphinha-barcelona-benfica-champions-league-oitavas-e1741778856618.webp">
    <h1 id="thanks"></h1>
    <p>Thanks for being part of my day 💚</p>
    <p>Same me. New age. Slightly upgraded.</p>
    <p>Have a good day❤️</p>
    <p style="font-size:.8rem">
      Bonus Line: “2026 duniya khatm ho jaye.... 16 Days left.☠️”
    </p>
  </div>
</div>

<script>
let user="";

function switchPage(id){
  document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
  document.getElementById(id).classList.add("active");
}

function toPage2(){
  user=document.getElementById("nameInput").value.trim();
  if(!user){
    alert("Please enter your name");
    return;
  }
  switchPage("p2");
  typeText(`Hey ${user} 👋\nIt’s my birthday today.`);
}
function toPage3(){switchPage("p3")}
function toPage4(){switchPage("p4")}
function toPage5(){
  document.getElementById("thanks").innerText=`Thank you ${user} 💚`;
  switchPage("p5");
}

/* Typing animation */
function typeText(text){
  let i=0;
  const el=document.getElementById("typing");
  el.innerText="";
  const t=setInterval(()=>{
    el.innerText+=text.charAt(i);
    i++;
    if(i>=text.length) clearInterval(t);
  },45);
}

/* Mood */
function setMood(t){
  document.getElementById("moodText").innerText=t;
}

/* Cake */
function cake(){
  document.getElementById("cakeText").innerText="Calories don’t count today 😌";
}

/* Secret */
function revealSecret(){
  document.getElementById("secretText").style.display="block";
}
</script>

</body>
</html>
