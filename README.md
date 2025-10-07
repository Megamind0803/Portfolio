# Portfolio
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Shridhar Gaikwad - Portfolio</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;800&display=swap" rel="stylesheet">
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      font-family: 'Poppins', sans-serif;
      background: #0b0f1a;
      color: white;
      overflow-x: hidden;
    }
    section { padding: 80px 20px; max-width: 1100px; margin: auto; }
    h1, h2, h3 { margin-bottom: 20px; }
    h1 { font-size: 3rem; font-weight: 800; }
    h2 { font-size: 2.2rem; font-weight: 700; text-align: center; }
    p { color: #cbd5e1; line-height: 1.6; }
    .btn {
      display: inline-block;
      margin-top: 30px;
      padding: 14px 28px;
      background: linear-gradient(90deg,#6366f1,#3b82f6);
      color: white;
      border-radius: 30px;
      text-decoration: none;
      transition: 0.3s;
    }
    .btn:hover { opacity: 0.85; transform: scale(1.05); }
    header {
      height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      text-align: center;
      position: relative;
      z-index: 1;
    }
    header h1 { font-size: 3.5rem; background: linear-gradient(90deg,#60a5fa,#a78bfa); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
    header p { font-size: 1.2rem; margin-top: 15px; color: #e2e8f0; }
    .services {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 25px;
      margin-top: 50px;
    }
    .card {
      background: rgba(255,255,255,0.05);
      border: 1px solid rgba(255,255,255,0.1);
      padding: 25px;
      border-radius: 15px;
      transition: 0.3s;
      backdrop-filter: blur(10px);
    }
    .card:hover {
      transform: translateY(-8px);
      border-color: #6366f1;
      box-shadow: 0 0 15px #6366f1aa;
    }
    ul { text-align: left; color: #94a3b8; margin-top: 15px; }
    footer { padding: 30px; text-align: center; color: #64748b; background: #0f172a; }
    canvas { position: fixed; top: 0; left: 0; width: 100%; height: 100%; z-index: -1; }
  </style>
</head>
<body>
  <canvas id="stars"></canvas>

  <!-- Hero -->
  <header>
    <h1>Shridhar Gaikwad</h1>
    <p>Digital Marketing | Website Development | SEO | Branding</p>
    <a href="#contact" class="btn">Contact Me</a>
  </header>

  <!-- About -->
  <section id="about">
    <h2>About Me</h2>
    <p>
      I specialize in helping businesses grow through smart digital marketing strategies, 
      high-performing websites, and powerful branding solutions. My focus is on creating 
      an impactful online presence that delivers real results.
    </p>
  </section>

  <!-- Services -->
  <section id="services">
    <h2>Services</h2>
    <div class="services">
      <div class="card">
        <h3>Website Development</h3>
        <ul>
          <li>Static Websites</li>
          <li>Dynamic Websites</li>
          <li>E-commerce Stores</li>
          <li>Portfolio Websites</li>
        </ul>
      </div>
      <div class="card">
        <h3>Digital Marketing</h3>
        <ul>
          <li>Social Media Marketing</li>
          <li>Influencer Marketing</li>
          <li>WhatsApp Funnel</li>
          <li>Content Strategy</li>
        </ul>
      </div>
      <div class="card">
        <h3>SEO & Ads</h3>
        <ul>
          <li>Search Engine Optimization</li>
          <li>Google Ads Setup</li>
          <li>Instagram & Facebook Ads</li>
          <li>Analytics & Tracking</li>
        </ul>
      </div>
    </div>
  </section>

  <!-- Contact -->
  <section id="contact">
    <h2>Contact Me</h2>
    <p>Email: <a href="mailto:shridharg1995@outlook.com" style="color:#38bdf8;">shridharg1995@outlook.com</a></p>
    <p>Phone: <span style="color:#38bdf8;">+91 7898841321</span></p>
    <a href="mailto:shridharg1995@outlook.com" class="btn">Send Email</a>
  </section>

  <footer>
    © <span id="year"></span> Shridhar Gaikwad. All rights reserved.
  </footer>

  <script>
    // Dynamic year
    document.getElementById("year").innerText = new Date().getFullYear();

    // Stars background
    const canvas = document.getElementById("stars");
    const ctx = canvas.getContext("2d");
    let stars = [];
    let w, h;

    function resize() {
      w = canvas.width = window.innerWidth;
      h = canvas.height = window.innerHeight;
    }
    window.addEventListener("resize", resize);
    resize();

    function initStars(count) {
      stars = [];
      for (let i = 0; i < count; i++) {
        stars.push({
          x: Math.random() * w,
          y: Math.random() * h,
          r: Math.random() * 2 + 1,
          dx: (Math.random() - 0.5) * 0.5,
          dy: (Math.random() - 0.5) * 0.5
        });
      }
    }
    initStars(200);

    function drawStars() {
      ctx.clearRect(0, 0, w, h);
      ctx.fillStyle = "white";
      stars.forEach(star => {
        ctx.beginPath();
        ctx.arc(star.x, star.y, star.r, 0, Math.PI * 2);
        ctx.fill();
        star.x += star.dx;
        star.y += star.dy;

        // Wrap stars around screen
        if (star.x < 0) star.x = w;
        if (star.x > w) star.x = 0;
        if (star.y < 0) star.y = h;
        if (star.y > h) star.y = 0;
      });
      requestAnimationFrame(drawStars);
    }
    drawStars();

    // Mouse movement attraction
    document.addEventListener("mousemove", (e) => {
      stars.forEach(star => {
        let dx = e.clientX - star.x;
        let dy = e.clientY - star.y;
        let dist = Math.sqrt(dx * dx + dy * dy);
        if (dist < 100) {
          star.x -= dx * 0.01;
          star.y -= dy * 0.01;
        }
      });
    });
  </script>
</body>
</html>