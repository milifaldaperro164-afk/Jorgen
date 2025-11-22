<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Jorge</title>

<style>
body {
    margin: 0;
    padding: 0;
    background: #000;
    color: #cfffff;
    font-family: "Courier New", monospace;
    text-align: center;
    overflow: hidden;
}

/* Título con brillo suave */
h1 {
    font-size: 55px;
    margin-top: 40px;
    animation: glow 4s infinite alternate;
}
h2 {
    font-size: 40px;
    margin-top: -10px;
    animation: glow 5s infinite alternate;
}
@keyframes glow {
    from { text-shadow: 0 0 10px #00ffff; color: #00eaff; }
    to   { text-shadow: 0 0 25px #00ffc6; color: #7fffd9; }
}

/* Piscis flotando y brillando */
.piscis {
    font-size: 90px;
    margin: 40px 0;
    animation: flotar 3s infinite ease-in-out, glow 6s infinite alternate;
}
@keyframes flotar {
    0% { transform: translateY(0); }
    50% { transform: translateY(-8px); }
    100% { transform: translateY(0); }
}

/* Humo elegante */
.humo {
    position: absolute;
    top: 170px;
    left: 50%;
    width: 350px;
    height: 170px;
    transform: translateX(-50%);
    background: radial-gradient(circle, rgba(0,255,255,0.20) 0%, transparent 70%);
    filter: blur(22px);
    animation: humo 5s infinite alternate ease-in-out;
    z-index: -1;
}
@keyframes humo {
    0% { opacity: 0.3; }
    100% { opacity: 0.6; }
}

/* Poema con separación entre versos */
.poema {
    font-size: 22px;
    width: 90%;
    max-width: 500px;
    margin: 20px auto;
    white-space: pre-line;
    line-height: 2.4; /* espacio entre versos */
    opacity: 0;
    animation: fade 1s forwards 1.5s;
}
@keyframes fade { from { opacity: 0; } to { opacity: 1; } }

/* Matrix suave */
canvas {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: -10;
}
</style>
</head>

<body>

<canvas id="matrix"></canvas>

<h1>JORGE</h1>
<h2>BAREIRO</h2>

<div class="humo"></div>

<div class="piscis">♓</div>

<div id="poema" class="poema"></div>

<!-- Sonido suave -->
<audio autoplay loop>
    <source src="https://files.catbox.moe/9q8x5m.mp3" type="audio/mpeg">
</audio>

<script>
// Poema letra por letra con separación entre versos
const texto = `Tu sonrisa calma mis noches,
y tu mirada enciende mis días.

En cada silencio te siento,
y en cada pensamiento te encuentro.`;

let i = 0;
function escribir() {
    if (i < texto.length) {
        document.getElementById("poema").innerText += texto.charAt(i);
        i++;
        setTimeout(escribir, 40);
    }
}
setTimeout(escribir, 1200);

// MATRIX suave
const canvas = document.getElementById("matrix");
const ctx = canvas.getContext("2d");
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

const letras = "01";
const tam = 18;
const columnas = canvas.width / tam;
const lluvia = Array.from({length: columnas}, () => 1);

function draw() {
    ctx.fillStyle = "rgba(0,0,0,0.05)";
    ctx.fillRect(0,0,canvas.width,canvas.height);
    ctx.fillStyle = "rgba(0,255,170,0.7)";
    ctx.font = tam + "px monospace";
    lluvia.forEach((y,i)=>{
        ctx.fillText(letras[Math.floor(Math.random()*letras.length)], i*tam, y*tam);
        lluvia[i] = (y*tam > canvas.height && Math.random() > 0.975) ? 0 : y+1;
    });
}
setInterval(draw, 50);
</script>

</body>
</html>
