<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Para Ti 🌻</title>
<style>
  /* --- ESTILOS GENERALES --- */
  * { margin: 0; padding: 0; box-sizing: border-box; }
  
  body {
    background: radial-gradient(ellipse at bottom, #1b2735 0%, #090a0f 100%);
    height: 100vh;
    overflow: hidden;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
  }

  /* --- ESTRELLAS DE FONDO --- */
  .star {
    position: absolute;
    background: white;
    border-radius: 50%;
    animation: twinkle var(--duration) infinite ease-in-out;
  }

  @keyframes twinkle {
    0%, 100% { opacity: 0.2; transform: scale(0.8); }
    50% { opacity: 1; transform: scale(1.2); }
  }

  /* --- PANTALLA DE INICIO --- */
  #start-screen {
    z-index: 100;
    transition: opacity 0.8s ease;
  }

  #start-btn {
    padding: 18px 40px;
    font-size: 1.3rem;
    background: linear-gradient(45deg, #ffeb3b, #fbc02d);
    color: #3e2723;
    border: none;
    border-radius: 50px;
    font-weight: bold;
    cursor: pointer;
    box-shadow: 0 0 30px rgba(255, 235, 59, 0.4);
    animation: pulse 2s infinite;
  }

  @keyframes pulse {
    0% { transform: scale(1); box-shadow: 0 0 20px rgba(255, 235, 59, 0.4); }
    50% { transform: scale(1.05); box-shadow: 0 0 40px rgba(255, 235, 59, 0.7); }
    100% { transform: scale(1); box-shadow: 0 0 20px rgba(255, 235, 59, 0.4); }
  }

  /* --- MENSAJE PRINCIPAL --- */
  #main-content {
    display: none;
    z-index: 50;
    opacity: 0;
    transition: opacity 1.5s ease;
  }

  h1 {
    font-size: 2.5rem;
    color: #ffeb3b;
    text-shadow: 0 0 15px #fbc02d, 0 0 30px #ff9800;
    margin-bottom: 15px;
    animation: glow 3s infinite alternate;
  }

  p {
    font-size: 1.3rem;
    color: #fff9c4;
    line-height: 1.6;
    max-width: 90%;
    margin: 0 auto;
  }

  @keyframes glow {
    from { text-shadow: 0 0 10px #fbc02d, 0 0 20px #ff9800; }
    to { text-shadow: 0 0 20px #ffeb3b, 0 0 40px #ff9800, 0 0 10px white; }
  }

  /* --- FLORES FLOTANTES --- */
  .floating-flower {
    position: absolute;
    font-size: 2rem;
    pointer-events: none;
    z-index: 10;
    animation: floatUp 8s linear forwards;
  }

  @keyframes floatUp {
    0% {
      transform: translateY(110vh) rotate(0deg) scale(0.5);
      opacity: 0;
    }
    10% {
      opacity: 1;
      transform: translateY(90vh) rotate(20deg) scale(1);
    }
    100% {
      transform: translateY(-20vh) rotate(360deg) scale(1.2);
      opacity: 0;
    }
  }
</style>
</head>
<body>

  <!-- Pantalla de inicio -->
  <div id="start-screen">
    <button id="start-btn">🌻 Toca para ver tu sorpresa 🌻</button>
  </div>

  <!-- Contenido principal (oculto al inicio) -->
  <div id="main-content">
    <!-- ✏️ CAMBIA EL NOMBRE Y EL MENSAJE AQUÍ ABAJO -->
    <h1>¡Feliz Día de las Flores Amarillas, mi querida Moya💛✨!</h1>
    <p>
      Aunque hoy nos separe la distancia, no quería dejar pasar este día sin enviarte estas flores virtuales y recordarte lo mucho que agradezco tus casi 3 años de amistad. Gracias por ser tan detallista y por cada uno de tus regalitos virtuales; siempre me alegran el día.
      Quiero que recuerdes que, sin importar los kilómetros, siempre estaré aquí con contigo y para ti, apoyándote en todo. ¡Eres mi mejor amiga y te quiero muchísimo, Mishelle! 🌼<br>
        Con todo mi cariño, By.<br>
      ✨ Te quiero y amo mucho ✨
    </p>
  </div>

  <!-- Audio (Opcional) -->
  <!-- Puedes cambiar el 'src' por un enlace directo a un archivo .mp3 -->
  <audio id="bg-music" loop>
    <source src="https://files.catbox.moe/bqiqoz.mp3" type="audio/mpeg">
  </audio>

<script>
  // 1. Generar estrellas de fondo
  function createStars() {
    const body = document.body;
    for (let i = 0; i < 150; i++) {
      const star = document.createElement('div');
      star.className = 'star';
      const size = Math.random() * 3 + 1 + 'px';
      star.style.width = size;
      star.style.height = size;
      star.style.left = Math.random() * 100 + 'vw';
      star.style.top = Math.random() * 100 + 'vh';
      star.style.setProperty('--duration', (Math.random() * 3 + 2) + 's');
      body.appendChild(star);
    }
  }
  createStars();

  // 2. Lógica del botón de inicio
  const startBtn = document.getElementById('start-btn');
  const startScreen = document.getElementById('start-screen');
  const mainContent = document.getElementById('main-content');
  const music = document.getElementById('bg-music');

  startBtn.addEventListener('click', () => {
    // Desvanecer pantalla de inicio
    startScreen.style.opacity = '0';
    setTimeout(() => {
      startScreen.style.display = 'none';
      mainContent.style.display = 'block';
      // Pequeño retraso para que la transición de opacidad funcione
      setTimeout(() => {
        mainContent.style.opacity = '1';
      }, 50);
    }, 800);

    // Intentar reproducir música (ignora el error si el navegador lo bloquea)
    music.volume = 0.5; // Volumen al 50%
    music.play().catch(e => console.log("Audio bloqueado o no disponible:", e));

    // Iniciar lluvia de flores
    setInterval(createFloatingFlower, 300); // Una flor cada 300ms
  });

  // 3. Crear flores flotantes (¡Aquí estaba el error antes!)
  function createFloatingFlower() {
    const flower = document.createElement('div');
    flower.className = 'floating-flower';
    flower.innerHTML = '🌻'; // <-- ¡AQUÍ ESTÁ LA FLOR!
    
    // Posición y tamaño aleatorios
    flower.style.left = Math.random() * 95 + 'vw';
    flower.style.fontSize = (Math.random() * 1.5 + 1.5) + 'rem';
    
    // Duración de la animación ligeramente aleatoria para que se vea natural
    flower.style.animationDuration = (Math.random() * 4 + 6) + 's';
    
    document.body.appendChild(flower);

    // Eliminar la flor del DOM después de que termine la animación para no saturar la memoria
    setTimeout(() => {
      flower.remove();
    }, 10000);
  }
</script>

</body>
</html>
