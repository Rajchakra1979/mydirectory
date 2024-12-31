<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Happy New Year 2025</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      overflow: hidden;
      background: #000;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
    }

    .message {
      color: #fff;
      font-family: 'Arial', sans-serif;
      text-align: center;
      font-size: 2rem;
      position: absolute;
      top: 10%;
      animation: fadeIn 2s ease-in-out;
    }

    @keyframes fadeIn {
      from {
        opacity: 0;
      }
      to {
        opacity: 1;
      }
    }

    canvas {
      position: absolute;
      top: 0;
      left: 0;
    }

    .balloons {
      position: absolute;
      bottom: -100px;
      width: 100%;
      display: flex;
      justify-content: space-around;
      animation: float 5s infinite ease-in-out;
    }

    .balloon {
      width: 50px;
      height: 80px;
      background: radial-gradient(circle, #ff7eb3 0%, #ff0000 70%);
      border-radius: 50%;
    }

    @keyframes float {
      0% {
        transform: translateY(0);
      }
      50% {
        transform: translateY(-100px);
      }
      100% {
        transform: translateY(0);
      }
    }
  </style>
</head>
<body>
  <canvas id="fireworks"></canvas>
  <div class="message">🎉 Happy New Year 2025! 🎉</div>
  <div class="balloons">
    <div class="balloon"></div>
    <div class="balloon"></div>
    <div class="balloon"></div>
  </div>
  <script>
    // Fireworks animation
    const canvas = document.getElementById('fireworks');
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    function Firework(x, y, color) {
      this.x = x;
      this.y = y;
      this.color = color;
      this.r = 2;
      this.draw = function () {
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.r, 0, Math.PI * 2);
        ctx.fillStyle = this.color;
        ctx.fill();
      };
    }

    let fireworks = [];
    function createFirework() {
      for (let i = 0; i < 20; i++) {
        const angle = Math.random() * 2 * Math.PI;
        const speed = Math.random() * 3 + 2;
        const color = `hsl(${Math.random() * 360}, 100%, 50%)`;
        fireworks.push(
          new Firework(
            canvas.width / 2 + Math.cos(angle) * speed * 50,
            canvas.height / 2 + Math.sin(angle) * speed * 50,
            color
          )
        );
      }
    }

    function animate() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      fireworks.forEach((fw, index) => {
        fw.draw();
        fw.x += (Math.random() - 0.5) * 4;
        fw.y += (Math.random() - 0.5) * 4;
        if (fw.r > 0.1) {
          fw.r -= 0.1;
        } else {
          fireworks.splice(index, 1);
        }
      });
      requestAnimationFrame(animate);
    }

    createFirework();
    animate();
    setInterval(createFirework, 1500);
  </script>
</body>
</html>
