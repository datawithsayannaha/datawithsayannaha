<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Sayan Naha — Data Analyst Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet"/>
<style>
  :root {
    --violet: #8b5cf6;
    --pink: #ec4899;
    --orange: #f97316;
    --blue: #3b82f6;
    --green: #10b981;
    --bg: #050508;
    --bg-card: #0f0f1a;
    --border: #1e1b33;
    --text: #f1f0ff;
    --muted: #94a3b8;
  }

  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    font-family: 'Syne', sans-serif;
    color: var(--text);
    overflow-x: hidden;
    line-height: 1.6;
  }

  /* CUSTOM CURSOR - Desktop only for better UX */
  @media (min-width: 1024px) {
    .cursor {
      width: 10px; height: 10px; background: var(--violet); border-radius: 50%;
      position: fixed; pointer-events: none; z-index: 9999; mix-blend-mode: screen;
    }
    .cursor-follower {
      width: 30px; height: 30px; border: 1px solid rgba(139,92,246,0.4); border-radius: 50%;
      position: fixed; pointer-events: none; z-index: 9998; transition: transform 0.1s ease;
    }
  }

  canvas#bg { position: fixed; inset: 0; z-index: 0; pointer-events: none; }

  .page { position: relative; z-index: 2; max-width: 900px; margin: 0 auto; padding: 0 24px 100px; }

  /* NAV */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    padding: 20px 40px; display: flex; justify-content: space-between; align-items: center;
    backdrop-filter: blur(12px); border-bottom: 1px solid rgba(255,255,255,0.05);
  }
  .nav-logo { font-family: 'Space Mono', monospace; font-weight: 700; color: var(--violet); }
  .nav-links { display: flex; gap: 24px; }
  .nav-links a { font-family: 'Space Mono', monospace; font-size: 11px; text-decoration: none; color: var(--muted); text-transform: uppercase; letter-spacing: 1px; transition: 0.3s; }
  .nav-links a:hover { color: var(--text); }

  /* HERO */
  .hero { text-align: center; padding: 160px 0 80px; }
  .hero-eyebrow { font-family: 'Space Mono', monospace; font-size: 12px; color: var(--violet); letter-spacing: 4px; margin-bottom: 16px; text-transform: uppercase; }
  .hero-name { font-size: clamp(40px, 8vw, 80px); font-weight: 800; letter-spacing: -2px; margin-bottom: 20px; background: linear-gradient(to right, #fff, var(--violet), var(--pink)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
  .hero-tagline { font-size: 18px; color: var(--muted); max-width: 600px; margin: 0 auto 40px; }

  /* BUTTONS */
  .social-btn {
    display: inline-flex; align-items: center; gap: 10px; padding: 12px 24px;
    background: var(--bg-card); border: 1px solid var(--border); border-radius: 50px;
    color: var(--text); text-decoration: none; font-family: 'Space Mono', monospace; font-size: 13px; transition: 0.3s;
  }
  .social-btn:hover { border-color: var(--violet); transform: translateY(-3px); background: rgba(139,92,246,0.05); }

  /* SECTION LABELS */
  .section-label { font-family: 'Space Mono', monospace; font-size: 12px; color: var(--violet); letter-spacing: 3px; text-transform: uppercase; margin: 80px 0 30px; display: flex; align-items: center; gap: 15px; }
  .section-label::after { content: ''; height: 1px; flex: 1; background: linear-gradient(90deg, var(--border), transparent); }

  /* CARDS */
  .card { background: var(--bg-card); border: 1px solid var(--border); border-radius: 20px; padding: 30px; transition: 0.4s ease; position: relative; overflow: hidden; }
  .card:hover { border-color: rgba(139,92,246,0.4); transform: translateY(-5px); box-shadow: 0 20px 40px rgba(0,0,0,0.4); }

  /* SKILLS (No Bars) */
  .skills-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; }
  .skill-header { display: flex; align-items: center; gap: 12px; margin-bottom: 10px; }
  .skill-level { font-family: 'Space Mono', monospace; font-size: 10px; background: rgba(139,92,246,0.1); color: var(--violet); padding: 2px 8px; border-radius: 4px; margin-left: auto; }
  .skill-name { font-weight: 700; font-size: 18px; }
  .skill-desc { font-size: 13px; color: var(--muted); font-family: 'Space Mono', monospace; }

  /* PROJECTS */
  .project-card { margin-bottom: 20px; display: flex; flex-direction: column; gap: 15px; }
  .proj-tags { display: flex; gap: 10px; flex-wrap: wrap; }
  .tag { font-family: 'Space Mono', monospace; font-size: 10px; padding: 4px 12px; border-radius: 20px; background: #161625; border: 1px solid var(--border); color: var(--muted); }

  /* FOOTER */
  footer { text-align: center; padding: 60px 0; border-top: 1px solid var(--border); margin-top: 100px; color: var(--muted); font-family: 'Space Mono', monospace; font-size: 12px; }

  /* REVEAL ANIMATION */
  .reveal { opacity: 0; transform: translateY(30px); transition: 0.8s ease-out; }
  .reveal.active { opacity: 1; transform: translateY(0); }

  @media (max-width: 600px) {
    .nav-links { display: none; }
    .hero { padding-top: 120px; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-follower" id="follower"></div>
<canvas id="bg"></canvas>

<nav>
  <div class="nav-logo">SN_ANALYST</div>
  <div class="nav-links">
    <a href="#about">About</a>
    <a href="#skills">Skills</a>
    <a href="#projects">Projects</a>
    <a href="#connect">Connect</a>
  </div>
</nav>

<div class="page">
  <!-- HERO -->
  <section class="hero">
    <div class="hero-eyebrow">⟨ Portfolio 2026 ⟩</div>
    <h1 class="hero-name">Sayan Naha</h1>
    <p class="hero-tagline">Data Analyst turning complex datasets into clear, actionable business insights.</p>
    <div style="display: flex; gap: 15px; justify-content: center; flex-wrap: wrap;">
      <a href="https://linkedin.com/in/YOUR_USERNAME" class="social-btn">LinkedIn</a>
      <a href="https://github.com/YOUR_USERNAME" class="social-btn">GitHub</a>
      <a href="mailto:youremail@gmail.com" class="social-btn" style="background: var(--violet); border: none;">Contact Me</a>
    </div>
  </section>

  <!-- ABOUT -->
  <section id="about" class="reveal">
    <div class="section-label">About Me</div>
    <div class="card">
      <p style="color: var(--muted); font-size: 17px;">
        As an aspiring <strong style="color: #fff;">Data Analyst</strong> based in India, I specialize in cleaning messy data and building visual stories. I am currently looking for WFH or Private Sector opportunities where I can apply my analytical mindset to solve real business problems.
      </p>
    </div>
  </section>

  <!-- SKILLS -->
  <section id="skills" class="reveal">
    <div class="section-label">Technical Stack</div>
    <div class="skills-grid">
      <div class="card">
        <div class="skill-header"><span>🐍</span> <span class="skill-name">Python</span> <span class="skill-level">Advanced</span></div>
        <p class="skill-desc">Pandas, NumPy, Matplotlib, Seaborn for deep EDA.</p>
      </div>
      <div class="card">
        <div class="skill-header"><span>🗄️</span> <span class="skill-name">SQL</span> <span class="skill-level">Expert</span></div>
        <p class="skill-desc">Complex Joins, CTEs, and Query Optimization.</p>
      </div>
      <div class="card">
        <div class="skill-header"><span>📊</span> <span class="skill-name">Power BI</span> <span class="skill-level">Intermediate</span></div>
        <p class="skill-desc">Interactive Dashboards & DAX scripting.</p>
      </div>
      <div class="card">
        <div class="skill-header"><span>📗</span> <span class="skill-name">Excel</span> <span class="skill-level">Expert</span></div>
        <p class="skill-desc">Automation, Pivot Tables & Advanced Formulas.</p>
      </div>
    </div>
  </section>

  <!-- PROJECTS -->
  <section id="projects" class="reveal">
    <div class="section-label">Featured Projects</div>
    
    <div class="card project-card">
      <h3 style="font-size: 22px;">Sales Performance Analytics</h3>
      <p class="skill-desc">A comprehensive Power BI dashboard analyzing revenue trends across different regions and product categories.</p>
      <div class="proj-tags">
        <span class="tag">Power BI</span> <span class="tag">DAX</span> <span class="tag">Data Modeling</span>
      </div>
    </div>

    <div class="card project-card" style="margin-top: 20px;">
      <h3 style="font-size: 22px;">Customer Churn Analysis</h3>
      <p class="skill-desc">Using SQL and Python to identify patterns in customer behavior and predicting potential churn risks.</p>
      <div class="proj-tags">
        <span class="tag">PostgreSQL</span> <span class="tag">Python</span> <span class="tag">Seaborn</span>
      </div>
    </div>
  </section>

  <!-- CONNECT -->
  <section id="connect" class="reveal" style="text-align: center;">
    <div class="section-label">Connect</div>
    <div class="card" style="background: linear-gradient(to bottom right, #0f0f1a, #1a1a2e);">
      <h2 style="margin-bottom: 10px;">Ready to work together?</h2>
      <p style="color: var(--muted); margin-bottom: 30px;">Currently open to full-time roles and freelance projects.</p>
      <a href="mailto:youremail@gmail.com" class="social-btn" style="background: #fff; color: #000; font-weight: 700;">Say Hello</a>
    </div>
  </section>

  <footer>
    <p>&copy; 2026 Sayan Naha. Crafted with Code & Logic.</p>
  </footer>
</div>

<script>
  // Cursor Logic
  const cursor = document.getElementById('cursor');
  const follower = document.getElementById('follower');
  
  if(cursor) {
    document.addEventListener('mousemove', (e) => {
      cursor.style.transform = `translate(${e.clientX}px, ${e.clientY}px)`;
      setTimeout(() => {
        follower.style.transform = `translate(${e.clientX - 10}px, ${e.clientY - 10}px)`;
      }, 50);
    });
  }

  // Background Animation
  const canvas = document.getElementById('bg');
  const ctx = canvas.getContext('2d');
  let w, h;

  function setCanvasSize() {
    w = canvas.width = window.innerWidth;
    h = canvas.height = window.innerHeight;
  }
  setCanvasSize();
  window.addEventListener('resize', setCanvasSize);

  const dots = Array.from({ length: 50 }, () => ({
    x: Math.random() * w,
    y: Math.random() * h,
    r: Math.random() * 2,
    vx: (Math.random() - 0.5) * 0.5,
    vy: (Math.random() - 0.5) * 0.5
  }));

  function animate() {
    ctx.clearRect(0, 0, w, h);
    ctx.fillStyle = "rgba(139, 92, 246, 0.15)";
    dots.forEach(d => {
      d.x += d.vx; d.y += d.vy;
      if(d.x < 0 || d.x > w) d.vx *= -1;
      if(d.y < 0 || d.y > h) d.vy *= -1;
      ctx.beginPath();
      ctx.arc(d.x, d.y, d.r, 0, Math.PI*2);
      ctx.fill();
    });
    requestAnimationFrame(animate);
  }
  animate();

  // Scroll Reveal
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if(entry.isIntersecting) entry.target.classList.add('active');
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
</script>
</body>
</html>
