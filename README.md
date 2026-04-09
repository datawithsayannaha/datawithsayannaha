<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Sayan Naha - Data Analyst Portfolio. Specializing in Python, SQL, and Power BI.">
    <title>Sayan Naha | Data Analyst Portfolio</title>
    
    <!-- Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;700;800&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --violet: #8b5cf6; --pink: #ec4899; --bg: #050508;
            --bg-card: #0f0f1a; --border: #1e1b33; --text: #f1f0ff; --muted: #94a3b8;
        }

        *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            background: var(--bg); font-family: 'Syne', sans-serif;
            color: var(--text); overflow-x: hidden; line-height: 1.6;
        }

        canvas#bg { position: fixed; inset: 0; z-index: 0; pointer-events: none; }
        .page { position: relative; z-index: 2; max-width: 900px; margin: 0 auto; padding: 0 24px 100px; }

        /* Navigation */
        nav {
            position: fixed; top: 0; width: 100%; z-index: 100; padding: 20px 40px;
            display: flex; justify-content: space-between; align-items: center;
            backdrop-filter: blur(15px); border-bottom: 1px solid rgba(255,255,255,0.05);
        }
        .nav-logo { font-family: 'Space Mono', monospace; font-weight: 700; color: var(--violet); }
        .nav-links { display: flex; gap: 24px; }
        .nav-links a { 
            font-family: 'Space Mono', monospace; font-size: 11px; text-decoration: none; 
            color: var(--muted); text-transform: uppercase; transition: 0.3s; 
        }
        .nav-links a:hover { color: var(--text); }

        /* Hero Section */
        .hero { text-align: center; padding: 160px 0 80px; }
        .hero-name { 
            font-size: clamp(40px, 8vw, 80px); font-weight: 800; letter-spacing: -2px; 
            background: linear-gradient(to right, #fff, var(--violet), var(--pink));
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
        }
        .hero-tagline { font-size: 18px; color: var(--muted); max-width: 600px; margin: 20px auto 40px; }

        /* Global Card Style */
        .card { 
            background: var(--bg-card); border: 1px solid var(--border); 
            border-radius: 20px; padding: 30px; transition: 0.4s ease; 
        }
        .card:hover { border-color: var(--violet); transform: translateY(-5px); }

        /* Skill & Project Grids */
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; }
        .skill-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px; }
        .skill-level { font-family: 'Space Mono', monospace; font-size: 10px; color: var(--violet); background: rgba(139,92,246,0.1); padding: 2px 8px; border-radius: 4px; }

        .section-label { 
            font-family: 'Space Mono', monospace; font-size: 12px; color: var(--violet); 
            letter-spacing: 3px; text-transform: uppercase; margin: 80px 0 30px; 
            display: flex; align-items: center; gap: 15px; 
        }
        .section-label::after { content: ''; height: 1px; flex: 1; background: linear-gradient(90deg, var(--border), transparent); }

        .social-btn {
            display: inline-flex; align-items: center; gap: 10px; padding: 12px 28px;
            background: var(--violet); border-radius: 50px; color: white;
            text-decoration: none; font-family: 'Space Mono', monospace; font-weight: 700; transition: 0.3s;
        }
        .social-btn:hover { filter: brightness(1.2); transform: scale(1.05); }

        /* Animations */
        .reveal { opacity: 0; transform: translateY(30px); transition: 0.8s ease-out; }
        .reveal.active { opacity: 1; transform: translateY(0); }

        @media (max-width: 600px) { .nav-links { display: none; } }
    </style>
</head>
<body>

<canvas id="bg"></canvas>

<nav>
    <div class="nav-logo">SN_ANALYST</div>
    <div class="nav-links">
        <a href="#about">About</a>
        <a href="#skills">Skills</a>
        <a href="#projects">Projects</a>
    </div>
</nav>

<div class="page">
    <section class="hero">
        <p style="font-family: 'Space Mono'; color: var(--violet); letter-spacing: 4px;">DATA ANALYST</p>
        <h1 class="hero-name">Sayan Naha</h1>
        <p class="hero-tagline">Turning complex datasets into actionable business stories.</p>
        <a href="mailto:youremail@gmail.com" class="social-btn">Let's Talk</a>
    </section>

    <section id="about" class="reveal">
        <div class="section-label">About</div>
        <div class="card">
            <p style="color: var(--muted);">Aspiring Data Analyst based in India. Focused on cleaning data, identifying trends, and creating high-impact visualizations for private sector growth.</p>
        </div>
    </section>

    <section id="skills" class="reveal">
        <div class="section-label">Tech Stack</div>
        <div class="grid">
            <div class="card">
                <div class="skill-header"><strong>Python</strong> <span class="skill-level">Advanced</span></div>
                <p style="font-size: 13px; color: var(--muted);">EDA, Pandas, NumPy, Matplotlib.</p>
            </div>
            <div class="card">
                <div class="skill-header"><strong>SQL</strong> <span class="skill-level">Expert</span></div>
                <p style="font-size: 13px; color: var(--muted);">CTEs, Joins, Query Optimization.</p>
            </div>
            <div class="card">
                <div class="skill-header"><strong>Power BI</strong> <span class="skill-level">Mid</span></div>
                <p style="font-size: 13px; color: var(--muted);">DAX, Interactive Reporting.</p>
            </div>
        </div>
    </section>

    <section id="projects" class="reveal">
        <div class="section-label">Projects</div>
        <div class="grid">
            <div class="card">
                <h3>Sales Dashboard</h3>
                <p style="font-size: 13px; color: var(--muted); margin: 10px 0;">Automated sales tracking with Power BI.</p>
            </div>
            <div class="card">
                <h3>Churn Analysis</h3>
                <p style="font-size: 13px; color: var(--muted); margin: 10px 0;">Customer behavior prediction using SQL.</p>
            </div>
        </div>
    </section>

    <footer style="text-align: center; padding: 60px 0; color: var(--muted); font-family: 'Space Mono'; font-size: 10px;">
        © 2026 SAYAN NAHA | BUILT FOR DATA
    </footer>
</div>

<script>
    // Simple Star Animation
    const canvas = document.getElementById('bg');
    const ctx = canvas.getContext('2d');
    let w, h;
    const setSize = () => { w = canvas.width = window.innerWidth; h = canvas.height = window.innerHeight; };
    window.onresize = setSize; setSize();

    const dots = Array.from({length: 40}, () => ({
        x: Math.random() * w, y: Math.random() * h,
        vx: (Math.random()-0.5)*0.3, vy: (Math.random()-0.5)*0.3
    }));

    function draw() {
        ctx.clearRect(0,0,w,h);
        ctx.fillStyle = "rgba(139, 92, 246, 0.2)";
        dots.forEach(d => {
            d.x += d.vx; d.y += d.vy;
            if(d.x<0 || d.x>w) d.vx*=-1; if(d.y<0 || d.y>h) d.vy*=-1;
            ctx.beginPath(); ctx.arc(d.x, d.y, 1.5, 0, Math.PI*2); ctx.fill();
        });
        requestAnimationFrame(draw);
    }
    draw();

    // Intersection Observer for Reveal
    const obs = new IntersectionObserver(es => {
        es.forEach(e => { if(e.isIntersecting) e.target.classList.add('active'); });
    }, {threshold: 0.1});
    document.querySelectorAll('.reveal').forEach(r => obs.observe(r));
</script>

</body>
</html>
