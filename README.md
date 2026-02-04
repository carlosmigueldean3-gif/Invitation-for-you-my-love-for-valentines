# Invitation-for-you-my-love-for-valentines
index.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>For Reyzel ❤️</title>

<!-- Google Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Playfair+Display&display=swap" rel="stylesheet">

<!-- Leaflet Map -->
<link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css"/>

<style>
body {
  margin: 0;
  font-family: 'Playfair Display', serif;
  background: radial-gradient(circle at top, #3b0a2a, #120010);
  color: #fff;
  overflow-x: hidden;
}

/* Falling hearts */
.heart {
  position: fixed;
  top: -10px;
  color: pink;
  animation: fall linear infinite;
  font-size: 18px;
}
@keyframes fall {
  to { transform: translateY(110vh); }
}

/* Envelope */
#envelope {
  width: 320px;
  height: 200px;
  background: #f5e6dc;
  margin: 40px auto;
  border-radius: 6px;
  position: relative;
  cursor: pointer;
}
#letter {
  display: none;
  padding: 20px;
  font-family: 'Great Vibes', cursive;
  font-size: 28px;
  color: #5a1a2b;
}

/* Controls */
.section {
  max-width: 900px;
  margin: 40px auto;
  padding: 20px;
  background: rgba(255,255,255,0.08);
  border-radius: 12px;
}

button, select {
  padding: 10px 16px;
  border: none;
  border-radius: 20px;
  background: #ff6f91;
  color: white;
  cursor: pointer;
}

input, textarea {
  width: 100%;
  padding: 10px;
  border-radius: 8px;
  border: none;
}

/* Gallery */
#gallery img {
  max-width: 180px;
  margin: 10px;
  border-radius: 12px;
  border: 8px solid pink;
}

/* Map */
#map {
  height: 300px;
  border-radius: 12px;
}
</style>
</head>

<body>

<!-- Hearts -->
<script>
for(let i=0;i<30;i++){
  let h=document.createElement("div");
  h.className="heart";
  h.innerHTML="❤";
  h.style.left=Math.random()*100+"vw";
  h.style.animationDuration=5+Math.random()*5+"s";
  document.body.appendChild(h);
}
</script>

<h1 style="text-align:center;">Happy Valentine’s Day, Reyzel Abuniawan 💖</h1>

<!-- Envelope -->
<div id="envelope" onclick="openEnvelope()">
  <div id="letter">
    <textarea placeholder="Type your message for Reyzel here..."></textarea>
  </div>
</div>

<!-- Music -->
<div class="section">
  <button onclick="toggleMusic()">🎹 Toggle Piano Music</button>
  <audio id="music" loop>
    <source src="https://cdn.pixabay.com/audio/2022/03/15/audio_7fcb92df45.mp3" type="audio/mpeg">
  </audio>
</div>

<!-- Countdown -->
<div class="section" id="countdown"></div>

<!-- Poem Generator -->
<div class="section">
  <button onclick="generatePoem()">💌 Generate Secret Romantic Poem</button>
  <p id="poem"></p>
</div>

<!-- Gallery -->
<div class="section">
  <h2>Our Cherished Memories 🌸</h2>
  <select onchange="changeBorder(this.value)">
    <option value="pink">Pink Roses</option>
    <option value="lavender">Lavender</option>
    <option value="gold">Golden Bloom</option>
  </select>
  <input type="file" multiple accept="image/*" onchange="loadImages(event)">
  <div id="gallery"></div>
</div>

<!-- Map -->
<div class="section">
  <h2>Our Favorite Places 🗺️</h2>
  <div id="map"></div>
</div>

<!-- Wax Seal -->
<div class="section">
  <h2>Seal the Envelope 🔴</h2>
  <select onchange="seal(this.value)">
    <option value="❤️">Heart</option>
    <option value="🌹">Rose</option>
    <option value="✨">Star</option>
  </select>
  <div id="sealDisplay" style="font-size:40px;"></div>
</div>

<script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>
<script>
function openEnvelope(){
  document.getElementById("letter").style.display="block";
}

function toggleMusic(){
  let m=document.getElementById("music");
  m.paused ? m.play() : m.pause();
}

function generatePoem(){
  const lines=[
    "Your smile is my favorite place to stay.",
    "Every heartbeat whispers your name.",
    "In every lifetime, I would still choose you.",
    "Love found its meaning the day I met you."
  ];
  document.getElementById("poem").innerText=
    "For Reyzel,\n" +
    lines[Math.floor(Math.random()*lines.length)];
}

function loadImages(e){
  const g=document.getElementById("gallery");
  for(let file of e.target.files){
    let img=document.createElement("img");
    img.src=URL.createObjectURL(file);
    g.appendChild(img);
  }
}

function changeBorder(color){
  document.querySelectorAll("#gallery img").forEach(img=>{
    img.style.borderColor=color;
  });
}

function seal(symbol){
  document.getElementById("sealDisplay").innerText=symbol;
}

// Countdown
const target=new Date("Feb 14, 2026");
setInterval(()=>{
  const now=new Date();
  const diff=target-now;
  document.getElementById("countdown").innerText=
    "Countdown to Valentine’s Day: " +
    Math.floor(diff/86400000)+" days 💕";
},1000);

// Map
const map=L.map('map').setView([0,0],2);
L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png').addTo(map);
map.on('click',e=>{
  L.marker(e.latlng).addTo(map)
    .bindPopup("A memory with Reyzel 💖").openPopup();
});
</script>

</body>
</html>
