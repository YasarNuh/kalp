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
        const distance = 80 + Math.random() * 80;

        p.style.left = x + "px";
        p.style.top = y + "px";
        p.style.setProperty('--x', Math.cos(angle) * distance + "px");
        p.style.setProperty('--y', Math.sin(angle) * distance + "px");

        document.body.appendChild(p);
        setTimeout(() => p.remove(), 600);
      }
    }

    // Kalp atışı efekti
    setInterval(() => {
      const rect = heart.getBoundingClientRect();
      const x = rect.left + rect.width / 2;
      const y = rect.top + rect.height / 2;
      spawnParticles(x, y, 8);
    }, 600);

    // Tıklayınca ekstra partikül efekti
    document.addEventListener("click", (e) => {
      spawnParticles(e.clientX, e.clientY, 25);
    });
  </script>

</body>
</html>
