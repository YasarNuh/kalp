<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8">
  <title>Kalpli Site</title>
  <style>
    body {
      margin: 0;
      height: 100vh;
      background: #0a0a0a;
      display: flex;
      justify-content: center;
      align-items: center;
      overflow: hidden;
      cursor: pointer;
    }

    .heart {
      width: 120px;
      height: 120px;
      background: red;
      position: relative;
      transform: rotate(45deg);
      animation: beat 0.6s infinite;
      box-shadow: 0 0 25px red;
    }

    .heart::before,
    .heart::after {
      content: "";
      width: 120px;
      height: 120px;
      background: red;
      position: absolute;
      border-radius: 50%;
    }

    .heart::before {
      top: -60px;
      left: 0;
    }

    .heart::after {
      left: -60px;
      top: 0;
    }

    @keyframes beat {
      0% { transform: rotate(45deg) scale(1); box-shadow: 0 0 20px red; }
      50% { transform: rotate(45deg) scale(1.25); box-shadow: 0 0 50px red; }
      100% { transform: rotate(45deg) scale(1); box-shadow: 0 0 20px red; }
    }

    /* Etraf efekti */
    .particle {
      position: absolute;
      width: 10px;
      height: 10px;
      background: rgb(255, 40, 40);
      border-radius: 50%;
      pointer-events: none;
      animation: explode 0.6s linear forwards;
    }

    @keyframes explode {
      to {
        transform: translate(var(--x), var(--y)) scale(0);
        opacity: 0;
      }
    }
  </style>
</head>
<body>

  <div class="heart" id="heart"></div>

  <script>
    const heart = document.getElementById("heart");

    function spawnParticles(x, y, count = 20) {
      for (let i = 0; i < count; i++) {
        const p = document.createElement("div");
        p.classList.add("particle");

        const angle = Math.random() * 2 * Math.PI;
        const distance = 100 + Math.random() * 80;

        p.style.left = x + "px";
        p.style.top = y + "px";
        p.style.setProperty('--x', Math.cos(angle) * distance + "px");
        p.style.setProperty('--y', Math.sin(angle) * distance + "px");

        document.body.appendChild(p);

        setTimeout(() => p.remove(), 600);
      }
    }

    // Kalp otomatik atınca efekt
    setInterval(() => {
      const rect = heart.getBoundingClientRect();
      const x = rect.left + rect.width / 2;
      const y = rect.top + rect.height / 2;
      spawnParticles(x, y, 8);
    }, 600);

    // Tıklayınca büyük efekt
    document.addEventListener("click", (e) => {
      spawnParticles(e.clientX, e.clientY, 25);
    });
  </script>

</body>
</html>

