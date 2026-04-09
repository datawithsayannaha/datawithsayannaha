<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Sayan Naha — Data Analyst Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet"/>
<style>
  :root {
    --violet: #7c3aed;
    --pink: #ec4899;
    --orange: #f97316;
    --blue: #3b82f6;
    --green: #10b981;
    --amber: #f59e0b;
    --bg: #08080f;
    --bg2: #0d0c1a;
    --bg3: #110f22;
    --bg4: #16132b;
    --border: #1e1a38;
    --border2: #2d2a4a;
    --text: #e8e6ff;
    --muted: #6b7280;
    --sub: #9ca3d4;
  }

  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    font-family: 'Syne', sans-serif;
    color: var(--text);
    min-height: 100vh;
    overflow-x: hidden;
    cursor: none;
  }

  /* CUSTOM CURSOR */
  .cursor {
    width: 12px; height: 12px;
    background: var(--violet);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9999;
    transition: transform 0.1s;
    mix-blend-mode: screen;
  }
  .cursor-follower {
    width: 36px; height: 36px;
    border: 1px solid rgba(124,58,237,0.5);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9998;
    transition: all 0.15s ease;
  }

  /* CANVAS BACKGROUND */
  canvas#bg {
    position: fixed; top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0; opacity: 0.5;
  }

  /* GRAIN OVERLAY */
  body::before {
    content: '';
    position: fixed; inset: 0; z-index: 1;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.05'/%3E%3C/svg%3E");
    opacity: 0.35;
    pointer-events: none;
  }

  /* LAYOUT */
  .page { position: relative; z-index: 2; max-width: 860px; margin: 0 auto; padding: 0 24px 80px; }

  /* HERO */
  .hero {
    text-align: center;
    padding: 90px 0 60px;
    position: relative;
  }
  .hero-eyebrow {
    font-family: 'Space Mono', monospace;
    font-size: 11px; letter-spacing: 4px;
    text-transform: uppercase;
    color: var(--violet);
    margin-bottom: 20px;
    opacity: 0; animation: fadeUp 0.7s 0.2s forwards;
  }
  .hero-name {
    font-size: clamp(52px, 10vw, 96px);
    font-weight: 800;
    line-height: 1;
    letter-spacing: -3px;
    margin-bottom: 16px;
    background: linear-gradient(135deg, #a78bfa 0%, #ec4899 45%, #fb923c 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    filter: drop-shadow(0 0 40px rgba(124,58,237,0.3));
    opacity: 0; animation: fadeUp 0.8s 0.35s forwards;
  }
  .hero-role {
    font-family: 'Space Mono', monospace;
    font-size: 15px; color: var(--sub);
    letter-spacing: 2px; margin-bottom: 28px;
    opacity: 0; animation: fadeUp 0.8s 0.5s forwards;
  }
  .hero-tagline {
    font-size: 18px; color: #c4bbf0;
    max-width: 460px; margin: 0 auto 36px;
    line-height: 1.8;
    opacity: 0; animation: fadeUp 0.8s 0.65s forwards;
  }

  /* STATUS */
  .status-pill {
    display: inline-flex; align-items: center; gap: 8px;
    background: rgba(16,185,129,0.08);
    border: 1px solid rgba(16,185,129,0.25);
    border-radius: 50px; padding: 8px 20px;
    font-family: 'Space Mono', monospace;
    font-size: 12px; color: #34d399;
    margin-bottom: 36px;
    opacity: 0; animation: fadeUp 0.8s 0.75s forwards;
  }
  .status-dot {
    width: 8px; height: 8px; border-radius: 50%;
    background: #10b981; position: relative;
  }
  .status-dot::after {
    content: ''; position: absolute; inset: -3px;
    border-radius: 50%; border: 1.5px solid #10b981;
    animation: ping 1.5s infinite;
  }
  @keyframes ping {
    0% { transform: scale(1); opacity: 0.8; }
    100% { transform: scale(2.5); opacity: 0; }
  }

  /* SOCIAL LINKS */
  .socials {
    display: flex; gap: 14px; justify-content: center; flex-wrap: wrap;
    opacity: 0; animation: fadeUp 0.8s 0.85s forwards;
  }
  .social-btn {
    display: inline-flex; align-items: center; gap: 8px;
    padding: 10px 22px; border-radius: 50px;
    font-family: 'Space Mono', monospace; font-size: 12px; font-weight: 700;
    text-decoration: none; letter-spacing: 0.5px;
    border: 1px solid var(--border2); color: var(--text);
    background: var(--bg3);
    transition: all 0.3s; position: relative; overflow: hidden;
  }
  .social-btn::before {
    content: ''; position: absolute; inset: 0;
    background: linear-gradient(135deg, var(--violet), var(--pink));
    opacity: 0; transition: opacity 0.3s;
  }
  .social-btn:hover::before { opacity: 1; }
  .social-btn:hover { transform: translateY(-3px); box-shadow: 0 12px 30px rgba(124,58,237,0.3); border-color: transparent; }
  .social-btn span { position: relative; z-index: 1; }

  /* SCROLL INDICATOR */
  .scroll-hint {
    position: absolute; bottom: 0; left: 50%; transform: translateX(-50%);
    display: flex; flex-direction: column; align-items: center; gap: 8px;
    font-family: 'Space Mono', monospace; font-size: 10px;
    color: var(--muted); letter-spacing: 2px;
    opacity: 0; animation: fadeUp 0.8s 1.2s forwards;
  }
  .scroll-line {
    width: 1px; height: 40px;
    background: linear-gradient(180deg, var(--violet), transparent);
    animation: scrollPulse 2s infinite;
  }
  @keyframes scrollPulse { 0%,100% { opacity: 0.3; } 50% { opacity: 1; } }

  /* SECTION */
  .section { margin-bottom: 56px; }
  .section-label {
    font-family: 'Space Mono', monospace;
    font-size: 10px; letter-spacing: 4px;
    text-transform: uppercase; color: var(--violet);
    display: flex; align-items: center; gap: 16px;
    margin-bottom: 24px;
  }
  .section-label::after {
    content: ''; flex: 1; height: 1px;
    background: linear-gradient(90deg, rgba(124,58,237,0.4), transparent);
  }

  /* ABOUT CARD */
  .about-card {
    background: linear-gradient(135deg, #130f2b 0%, #0e1220 100%);
    border: 1px solid var(--border2);
    border-radius: 24px; padding: 32px;
    position: relative; overflow: hidden;
  }
  .about-card::before {
    content: ''; position: absolute; top: -1px; left: 24px; right: 24px; height: 2px;
    background: linear-gradient(90deg, transparent, var(--violet), var(--pink), var(--orange), transparent);
  }
  .about-card::after {
    content: ''; position: absolute;
    width: 300px; height: 300px; border-radius: 50%;
    background: radial-gradient(circle, rgba(124,58,237,0.07), transparent 70%);
    top: -100px; right: -80px; pointer-events: none;
  }
  .about-grid {
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 20px;
  }
  @media(max-width:500px){ .about-grid { grid-template-columns: 1fr; } }
  .about-item { display: flex; align-items: flex-start; gap: 14px; }
  .about-icon {
    font-size: 22px; min-width: 36px; height: 36px;
    background: rgba(124,58,237,0.1); border-radius: 10px;
    display: flex; align-items: center; justify-content: center;
    border: 1px solid rgba(124,58,237,0.2);
  }
  .about-label {
    font-family: 'Space Mono', monospace; font-size: 10px;
    color: var(--muted); text-transform: uppercase; letter-spacing: 1.5px;
    margin-bottom: 4px;
  }
  .about-val { font-size: 15px; font-weight: 700; color: var(--text); }

  /* SKILL CARDS */
  .skills-grid {
    display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px;
  }
  @media(max-width:500px){ .skills-grid { grid-template-columns: 1fr; } }
  .skill-card {
    background: var(--bg3);
    border: 1px solid var(--border);
    border-radius: 20px; padding: 24px;
    transition: all 0.35s; position: relative; overflow: hidden;
    cursor: default;
  }
  .skill-card:hover {
    transform: translateY(-6px);
    border-color: var(--skill-color);
    box-shadow: 0 20px 50px rgba(0,0,0,0.4), 0 0 0 1px rgba(255,255,255,0.03) inset;
  }
  .skill-card::before {
    content: ''; position: absolute;
    inset: 0; opacity: 0;
    background: radial-gradient(circle at top left, rgba(var(--skill-rgb),0.12), transparent 60%);
    transition: opacity 0.35s;
  }
  .skill-card:hover::before { opacity: 1; }
  .skill-card::after {
    content: ''; position: absolute; bottom: 0; left: 0;
    width: 100%; height: 2px;
    background: linear-gradient(90deg, var(--skill-color), transparent);
    transform: scaleX(0); transform-origin: left;
    transition: transform 0.4s;
  }
  .skill-card:hover::after { transform: scaleX(1); }
  .skill-card.py { --skill-color: #3b82f6; --skill-rgb: 59,130,246; }
  .skill-card.sql { --skill-color: #f59e0b; --skill-rgb: 245,158,11; }
  .skill-card.pbi { --skill-color: #f97316; --skill-rgb: 249,115,22; }
  .skill-card.xl { --skill-color: #10b981; --skill-rgb: 16,185,129; }
  .skill-emoji { font-size: 32px; margin-bottom: 12px; display: block; }
  .skill-name { font-size: 18px; font-weight: 800; margin-bottom: 4px; color: var(--skill-color); }
  .skill-desc { font-family: 'Space Mono', monospace; font-size: 11px; color: var(--muted); line-height: 1.7; }
  .skill-bar { height: 3px; background: var(--border); border-radius: 2px; margin-top: 18px; overflow: hidden; }
  .skill-fill { height: 100%; border-radius: 2px; }
  .skill-card.py .skill-fill { background: linear-gradient(90deg, #3b82f6, #818cf8); width: 80%; }
  .skill-card.sql .skill-fill { background: linear-gradient(90deg, #f59e0b, #fde68a); width: 85%; }
  .skill-card.pbi .skill-fill { background: linear-gradient(90deg, #f97316, #fdba74); width: 75%; }
  .skill-card.xl .skill-fill { background: linear-gradient(90deg, #10b981, #6ee7b7); width: 90%; }
  .skill-percent {
    font-family: 'Space Mono', monospace; font-size: 11px;
    color: var(--skill-color); text-align: right;
    margin-top: 6px; opacity: 0.8;
  }

  /* PROJECT CARDS */
  .project-card {
    background: var(--bg3); border: 1px solid var(--border);
    border-radius: 20px; padding: 28px 28px 28px 36px;
    margin-bottom: 16px; transition: all 0.35s;
    position: relative; overflow: hidden; cursor: default;
  }
  .project-card::before {
    content: ''; position: absolute; left: 0;
    top: 16%; bottom: 16%; width: 3px;
    border-radius: 0 3px 3px 0;
    background: var(--proj-grad);
    transition: all 0.35s;
  }
  .project-card:hover::before { top: 0; bottom: 0; }
  .project-card:hover { transform: translateX(6px); border-color: rgba(124,58,237,0.3); }
  .proj-sales { --proj-grad: linear-gradient(180deg, #7c3aed, #ec4899); }
  .proj-sql { --proj-grad: linear-gradient(180deg, #f59e0b, #10b981); }
  .proj-header { display: flex; align-items: flex-start; justify-content: space-between; margin-bottom: 10px; gap: 12px; }
  .proj-title { font-size: 18px; font-weight: 800; color: var(--text); }
  .proj-badge {
    display: inline-flex; align-items: center; gap: 6px;
    font-family: 'Space Mono', monospace; font-size: 10px;
    padding: 5px 12px; border-radius: 50px; white-space: nowrap;
    background: rgba(236,72,153,0.08); border: 1px solid rgba(236,72,153,0.25);
    color: #f9a8d4;
  }
  .proj-dot { width: 6px; height: 6px; border-radius: 50%; background: #ec4899; animation: ping2 1.2s infinite; }
  @keyframes ping2 { 0%,100% { opacity: 1; } 50% { opacity: 0.2; } }
  .proj-desc { font-family: 'Space Mono', monospace; font-size: 12px; color: var(--muted); line-height: 1.8; margin-bottom: 16px; }
  .proj-tags { display: flex; gap: 8px; flex-wrap: wrap; }
  .ptag {
    font-family: 'Space Mono', monospace; font-size: 10px;
    padding: 4px 12px; border-radius: 50px; font-weight: 700; letter-spacing: 0.5px;
    border: 1px solid;
  }
  .pt-v { background: rgba(124,58,237,0.1); color: #a78bfa; border-color: rgba(124,58,237,0.3); }
  .pt-p { background: rgba(192,132,252,0.1); color: #c084fc; border-color: rgba(192,132,252,0.3); }
  .pt-y { background: rgba(245,158,11,0.1); color: #fbbf24; border-color: rgba(245,158,11,0.3); }
  .pt-g { background: rgba(52,211,153,0.1); color: #34d399; border-color: rgba(52,211,153,0.3); }
  .pt-o { background: rgba(249,115,22,0.1); color: #fb923c; border-color: rgba(249,115,22,0.3); }
  .pt-b { background: rgba(59,130,246,0.1); color: #60a5fa; border-color: rgba(59,130,246,0.3); }

  /* STATS */
  .stats-grid { display: grid; grid-template-columns: repeat(3,1fr); gap: 16px; }
  @media(max-width:480px){ .stats-grid { grid-template-columns: 1fr 1fr; } }
  .stat-card {
    background: var(--bg3); border: 1px solid var(--border);
    border-radius: 18px; padding: 24px; text-align: center;
    transition: all 0.35s;
  }
  .stat-card:hover { transform: scale(1.05); border-color: rgba(124,58,237,0.5); box-shadow: 0 0 30px rgba(124,58,237,0.12); }
  .stat-num {
    font-size: 40px; font-weight: 800; line-height: 1;
    background: linear-gradient(135deg, #a78bfa, #ec4899);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
    margin-bottom: 8px;
  }
  .stat-label { font-family: 'Space Mono', monospace; font-size: 10px; color: var(--muted); letter-spacing: 2px; text-transform: uppercase; }

  /* CURRENTLY LEARNING */
  .learning-list { display: flex; flex-direction: column; gap: 14px; }
  .learn-item {
    background: var(--bg3); border: 1px solid var(--border);
    border-radius: 16px; padding: 18px 22px;
    display: flex; align-items: center; gap: 16px;
    transition: all 0.3s;
  }
  .learn-item:hover { border-color: var(--border2); transform: translateX(4px); }
  .learn-icon {
    font-size: 24px; width: 48px; height: 48px;
    background: var(--bg4); border-radius: 14px;
    display: flex; align-items: center; justify-content: center;
    border: 1px solid var(--border2); flex-shrink: 0;
  }
  .learn-name { font-size: 16px; font-weight: 700; color: var(--text); margin-bottom: 3px; }
  .learn-desc { font-family: 'Space Mono', monospace; font-size: 11px; color: var(--muted); }
  .learn-progress { margin-left: auto; text-align: right; flex-shrink: 0; }
  .lp-num { font-family: 'Space Mono', monospace; font-size: 13px; font-weight: 700; color: var(--violet); }
  .lp-bar { width: 80px; height: 3px; background: var(--border); border-radius: 2px; margin-top: 6px; overflow: hidden; }
  .lp-fill { height: 100%; border-radius: 2px; background: linear-gradient(90deg, var(--violet), var(--pink)); }

  /* CONNECT */
  .connect-card {
    background: linear-gradient(135deg, #130f2b 0%, #0e1220 100%);
    border: 1px solid var(--border2);
    border-radius: 24px; padding: 40px;
    text-align: center; position: relative; overflow: hidden;
  }
  .connect-card::before {
    content: ''; position: absolute; top: -1px; left: 20%; right: 20%; height: 2px;
    background: linear-gradient(90deg, transparent, var(--violet), var(--pink), transparent);
  }
  .connect-glow {
    position: absolute; inset: 0; pointer-events: none;
    background: radial-gradient(ellipse at 50% 100%, rgba(124,58,237,0.12), transparent 60%);
  }
  .connect-title { font-size: 32px; font-weight: 800; margin-bottom: 12px; position: relative; z-index: 1; }
  .connect-sub { font-family: 'Space Mono', monospace; font-size: 13px; color: var(--sub); margin-bottom: 28px; position: relative; z-index: 1; }
  .connect-btns { display: flex; gap: 14px; justify-content: center; flex-wrap: wrap; position: relative; z-index: 1; }
  .connect-btn {
    display: inline-flex; align-items: center; gap: 9px;
    padding: 12px 28px; border-radius: 50px;
    font-family: 'Space Mono', monospace; font-size: 13px; font-weight: 700;
    text-decoration: none; transition: all 0.3s; border: 1px solid;
  }
  .btn-primary {
    background: linear-gradient(135deg, var(--violet), var(--pink));
    color: #fff; border-color: transparent;
  }
  .btn-primary:hover { transform: translateY(-3px); box-shadow: 0 16px 40px rgba(124,58,237,0.35); }
  .btn-secondary {
    background: transparent; color: var(--text);
    border-color: var(--border2);
  }
  .btn-secondary:hover { background: var(--bg4); transform: translateY(-3px); box-shadow: 0 16px 40px rgba(0,0,0,0.3); }

  /* FOOTER */
  .footer {
    text-align: center; padding: 48px 0 0;
    font-family: 'Space Mono', monospace; font-size: 11px;
    color: #2d2a4a; letter-spacing: 3px;
  }
  .footer-wave {
    width: 100%; height: 100px; position: relative; overflow: hidden; margin-bottom: 24px;
  }

  /* DIVIDER */
  .divider {
    height: 1px; margin: 0 0 56px;
    background: linear-gradient(90deg, transparent, var(--border2), transparent);
  }

  /* ANIMATIONS */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }
  .reveal {
    opacity: 0; transform: translateY(30px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  /* SCROLLBAR */
  ::-webkit-scrollbar { width: 6px; }
  ::-webkit-scrollbar-track { background: var(--bg); }
  ::-webkit-scrollbar-thumb { background: var(--border2); border-radius: 3px; }
  ::-webkit-scrollbar-thumb:hover { background: var(--violet); }

  /* NAV */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    padding: 16px 24px;
    display: flex; align-items: center; justify-content: space-between;
    background: rgba(8,8,15,0.7);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid rgba(255,255,255,0.04);
    transition: all 0.3s;
  }
  .nav-logo {
    font-family: 'Space Mono', monospace; font-size: 14px;
    font-weight: 700; color: var(--text);
    background: linear-gradient(135deg, #a78bfa, #ec4899);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
  }
  .nav-links { display: flex; gap: 28px; }
  .nav-links a {
    font-family: 'Space Mono', monospace; font-size: 11px;
    color: var(--muted); text-decoration: none;
    letter-spacing: 2px; text-transform: uppercase;
    transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--text); }
  @media(max-width:480px){ .nav-links { display: none; } }

  /* TECH TAGS CLOUD */
  .tag-cloud { display: flex; flex-wrap: wrap; gap: 10px; }
  .tech-tag {
    font-family: 'Space Mono', monospace; font-size: 11px;
    padding: 7px 16px; border-radius: 50px;
    border: 1px solid var(--border2); color: var(--sub);
    background: var(--bg3); transition: all 0.3s; cursor: default;
  }
  .tech-tag:hover { color: var(--text); border-color: var(--violet); background: rgba(124,58,237,0.1); }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-follower" id="follower"></div>

<canvas id="bg"></canvas>

<!-- NAV -->
<nav>
  <div class="nav-logo">SN.portfolio</div>
  <div class="nav-links">
    <a href="#about">About</a>
    <a href="#skills">Skills</a>
    <a href="#projects">Projects</a>
    <a href="#connect">Connect</a>
  </div>
</nav>

<!-- HERO -->
<div class="page">
  <section class="hero">
    <div class="hero-eyebrow">⟨ Data Analyst Portfolio ⟩</div>
    <h1 class="hero-name">Sayan Naha</h1>
    <p class="hero-role">SQL &nbsp;·&nbsp; Python &nbsp;·&nbsp; Power BI &nbsp;·&nbsp; Excel</p>
    <p class="hero-tagline">Turning raw numbers into decisions that matter — one dashboard at a time.</p>
    <div class="status-pill">
      <div class="status-dot"></div>
      Open to WFH &amp; Private Sector Opportunities · India 🇮🇳
    </div>
    <div class="socials">
      <a href="https://linkedin.com/in/YOUR_USERNAME" class="social-btn" target="_blank">
        <span>🔗</span><span>LinkedIn</span>
      </a>
      <a href="mailto:youremail@gmail.com" class="social-btn">
        <span>✉️</span><span>Gmail</span>
      </a>
      <a href="https://github.com/YOUR_USERNAME" class="social-btn" target="_blank">
        <span>🐙</span><span>GitHub</span>
      </a>
    </div>
    <div class="scroll-hint">
      <span>scroll</span>
      <div class="scroll-line"></div>
    </div>
  </section>

  <div style="height: 60px;"></div>

  <!-- ABOUT -->
  <section class="section reveal" id="about">
    <div class="section-label">About</div>
    <div class="about-card">
      <div class="about-grid">
        <div class="about-item">
          <div class="about-icon">🎯</div>
          <div>
            <div class="about-label">Role</div>
            <div class="about-val">Aspiring Data Analyst</div>
          </div>
        </div>
        <div class="about-item">
          <div class="about-icon">📍</div>
          <div>
            <div class="about-label">Location</div>
            <div class="about-val">India 🇮🇳</div>
          </div>
        </div>
        <div class="about-item">
          <div class="about-icon">🚀</div>
          <div>
            <div class="about-label">Goal</div>
            <div class="about-val">WFH / Private Sector Job</div>
          </div>
        </div>
        <div class="about-item">
          <div class="about-icon">⚡</div>
          <div>
            <div class="about-label">Passion</div>
            <div class="about-val">Data → Decisions 📊</div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <div class="divider reveal"></div>

  <!-- SKILLS -->
  <section class="section reveal" id="skills">
    <div class="section-label">Tech Stack</div>
    <div class="skills-grid">
      <div class="skill-card py">
        <span class="skill-emoji">🐍</span>
        <div class="skill-name">Python</div>
        <div class="skill-desc">Pandas · NumPy · Matplotlib<br/>Seaborn · Data Wrangling</div>
        <div class="skill-bar"><div class="skill-fill" style="animation: growBar 1.2s 0.2s ease-out forwards; width:0;"></div></div>
        <div class="skill-percent">80%</div>
      </div>
      <div class="skill-card sql">
        <span class="skill-emoji">🗄️</span>
        <div class="skill-name">SQL</div>
        <div class="skill-desc">PostgreSQL · Joins · CTEs<br/>Aggregations · Subqueries</div>
        <div class="skill-bar"><div class="skill-fill" style="animation: growBar 1.2s 0.4s ease-out forwards; width:0;"></div></div>
        <div class="skill-percent">85%</div>
      </div>
      <div class="skill-card pbi">
        <span class="skill-emoji">📊</span>
        <div class="skill-name">Power BI</div>
        <div class="skill-desc">DAX · KPI Dashboards<br/>Data Modeling · Reports</div>
        <div class="skill-bar"><div class="skill-fill" style="animation: growBar 1.2s 0.6s ease-out forwards; width:0;"></div></div>
        <div class="skill-percent">75%</div>
      </div>
      <div class="skill-card xl">
        <span class="skill-emoji">📗</span>
        <div class="skill-name">Excel</div>
        <div class="skill-desc">Pivot Tables · VLOOKUP<br/>Charts · Data Cleaning</div>
        <div class="skill-bar"><div class="skill-fill" style="animation: growBar 1.2s 0.8s ease-out forwards; width:0;"></div></div>
        <div class="skill-percent">90%</div>
      </div>
    </div>

    <div style="margin-top: 24px;">
      <div class="section-label" style="margin-bottom: 16px;">Also familiar with</div>
      <div class="tag-cloud">
        <span class="tech-tag">📈 Data Visualization</span>
        <span class="tech-tag">🔍 Exploratory Analysis</span>
        <span class="tech-tag">🧹 Data Cleaning</span>
        <span class="tech-tag">📉 Statistical Analysis</span>
        <span class="tech-tag">🗂️ Data Modeling</span>
        <span class="tech-tag">📋 Reporting</span>
        <span class="tech-tag">⚙️ ETL Basics</span>
        <span class="tech-tag">🤔 Problem Solving</span>
      </div>
    </div>
  </section>

  <div class="divider reveal"></div>

  <!-- PROJECTS -->
  <section class="section reveal" id="projects">
    <div class="section-label">Projects</div>

    <div class="project-card proj-sales reveal">
      <div class="proj-header">
        <div class="proj-title">📊 Sales Dashboard</div>
        <div class="proj-badge"><div class="proj-dot"></div>In Progress</div>
      </div>
      <p class="proj-desc">
        Interactive KPI dashboard built in Power BI with advanced DAX measures,<br/>
        dynamic filters, trend analysis & multi-page report layout.
      </p>
      <div class="proj-tags">
        <span class="ptag pt-o">Power BI</span>
        <span class="ptag pt-v">DAX</span>
        <span class="ptag pt-p">KPI</span>
        <span class="ptag pt-y">Trend Analysis</span>
      </div>
    </div>

    <div class="project-card proj-sql reveal">
      <div class="proj-header">
        <div class="proj-title">🗄️ SQL Data Analysis</div>
        <div class="proj-badge"><div class="proj-dot"></div>In Progress</div>
      </div>
      <p class="proj-desc">
        End-to-end exploratory analysis on a real-world dataset using PostgreSQL<br/>
        for querying and Python (Pandas + Matplotlib) for visualization.
      </p>
      <div class="proj-tags">
        <span class="ptag pt-y">PostgreSQL</span>
        <span class="ptag pt-b">Python</span>
        <span class="ptag pt-g">EDA</span>
        <span class="ptag pt-v">Matplotlib</span>
      </div>
    </div>
  </section>

  <div class="divider reveal"></div>

  <!-- STATS -->
  <section class="section reveal">
    <div class="section-label">By the Numbers</div>
    <div class="stats-grid">
      <div class="stat-card">
        <div class="stat-num">2+</div>
        <div class="stat-label">Projects</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">4</div>
        <div class="stat-label">Tech Skills</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">∞</div>
        <div class="stat-label">Curiosity</div>
      </div>
    </div>
  </section>

  <div class="divider reveal"></div>

  <!-- LEARNING -->
  <section class="section reveal">
    <div class="section-label">Currently Learning</div>
    <div class="learning-list">
      <div class="learn-item">
        <div class="learn-icon">📊</div>
        <div>
          <div class="learn-name">Advanced Power BI</div>
          <div class="learn-desc">Complex DAX · Row-Level Security · Bookmarks</div>
        </div>
        <div class="learn-progress">
          <div class="lp-num">65%</div>
          <div class="lp-bar"><div class="lp-fill" style="width:65%"></div></div>
        </div>
      </div>
      <div class="learn-item">
        <div class="learn-icon">🐍</div>
        <div>
          <div class="learn-name">Python for Data Science</div>
          <div class="learn-desc">Scikit-learn · Statistical Modeling</div>
        </div>
        <div class="learn-progress">
          <div class="lp-num">50%</div>
          <div class="lp-bar"><div class="lp-fill" style="width:50%"></div></div>
        </div>
      </div>
      <div class="learn-item">
        <div class="learn-icon">🗄️</div>
        <div>
          <div class="learn-name">Advanced SQL</div>
          <div class="learn-desc">Window Functions · Performance Tuning</div>
        </div>
        <div class="learn-progress">
          <div class="lp-num">70%</div>
          <div class="lp-bar"><div class="lp-fill" style="width:70%"></div></div>
        </div>
      </div>
    </div>
  </section>

  <div class="divider reveal"></div>

  <!-- CONNECT -->
  <section class="section reveal" id="connect">
    <div class="connect-card">
      <div class="connect-glow"></div>
      <div class="connect-title">Let's Connect 🤝</div>
      <p class="connect-sub">Open to data analyst roles · WFH preferred · India 🇮🇳</p>
      <div class="connect-btns">
        <a href="https://linkedin.com/in/YOUR_USERNAME" class="connect-btn btn-primary" target="_blank">
          🔗 &nbsp;LinkedIn
        </a>
        <a href="mailto:youremail@gmail.com" class="connect-btn btn-secondary">
          ✉️ &nbsp;Send Email
        </a>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer class="footer reveal">
    <div>✦ SAYAN NAHA · DATA ANALYST · INDIA ✦</div>
    <div style="margin-top: 8px; font-size: 10px;">Built with passion for data</div>
  </footer>
</div>

<style>
@keyframes growBar {
  from { width: 0; }
  to { width: var(--target-w, 80%); }
}
.skill-card.py .skill-fill { --target-w: 80%; }
.skill-card.sql .skill-fill { --target-w: 85%; }
.skill-card.pbi .skill-fill { --target-w: 75%; }
.skill-card.xl .skill-fill { --target-w: 90%; }
</style>

<script>
// CURSOR
const cursor = document.getElementById('cursor');
const follower = document.getElementById('follower');
let mx = 0, my = 0, fx = 0, fy = 0;
document.addEventListener('mousemove', e => {
  mx = e.clientX; my = e.clientY;
  cursor.style.left = mx - 6 + 'px';
  cursor.style.top = my - 6 + 'px';
});
function animFollower() {
  fx += (mx - fx - 18) * 0.15;
  fy += (my - fy - 18) * 0.15;
  follower.style.left = fx + 'px';
  follower.style.top = fy + 'px';
  requestAnimationFrame(animFollower);
}
animFollower();

// CANVAS STARS + NEBULA
const canvas = document.getElementById('bg');
const ctx = canvas.getContext('2d');
let W, H, stars = [], particles = [];

function resize() {
  W = canvas.width = window.innerWidth;
  H = canvas.height = window.innerHeight;
}
resize();
window.addEventListener('resize', resize);

for(let i = 0; i < 140; i++) {
  stars.push({
    x: Math.random() * 2000,
    y: Math.random() * 2000,
    r: Math.random() * 1.5 + 0.3,
    a: Math.random(),
    speed: Math.random() * 0.008 + 0.003
  });
}

// Nebula blobs
const blobs = [
  { x: 0.2, y: 0.3, r: 250, c: '124,58,237', a: 0.04 },
  { x: 0.8, y: 0.1, r: 200, c: '236,72,153', a: 0.04 },
  { x: 0.5, y: 0.7, r: 300, c: '59,130,246', a: 0.03 },
  { x: 0.9, y: 0.8, r: 180, c: '249,115,22', a: 0.03 },
];

let t = 0;
function draw() {
  ctx.clearRect(0, 0, W, H);

  // Draw nebula
  blobs.forEach(b => {
    const gx = b.x * W + Math.sin(t * 0.0004 + b.x * 5) * 30;
    const gy = b.y * H + Math.cos(t * 0.0005 + b.y * 5) * 20;
    const g = ctx.createRadialGradient(gx, gy, 0, gx, gy, b.r);
    g.addColorStop(0, `rgba(${b.c},${b.a})`);
    g.addColorStop(1, `rgba(${b.c},0)`);
    ctx.fillStyle = g;
    ctx.beginPath();
    ctx.arc(gx, gy, b.r, 0, Math.PI * 2);
    ctx.fill();
  });

  // Draw stars
  stars.forEach(s => {
    s.a += s.speed;
    const alpha = 0.2 + Math.abs(Math.sin(s.a)) * 0.7;
    ctx.beginPath();
    ctx.arc(s.x % W, s.y % H, s.r, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(200,190,255,${alpha})`;
    ctx.fill();
  });

  t++;
  requestAnimationFrame(draw);
}
draw();

// SCROLL REVEAL
const reveals = document.querySelectorAll('.reveal');
const observer = new IntersectionObserver(entries => {
  entries.forEach((e, i) => {
    if(e.isIntersecting) {
      setTimeout(() => e.target.classList.add('visible'), i * 80);
    }
  });
}, { threshold: 0.1 });
reveals.forEach(r => observer.observe(r));

// SKILL BAR ANIMATION ON SCROLL
const skillCards = document.querySelectorAll('.skill-card');
const skillObserver = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if(e.isIntersecting) {
      const fill = e.target.querySelector('.skill-fill');
      if(fill) fill.style.animation = fill.style.animation || 'growBar 1.2s ease-out forwards';
    }
  });
}, { threshold: 0.3 });
skillCards.forEach(c => skillObserver.observe(c));

// NAV scroll effect
const nav = document.querySelector('nav');
window.addEventListener('scroll', () => {
  if(window.scrollY > 60) {
    nav.style.background = 'rgba(8,8,15,0.95)';
  } else {
    nav.style.background = 'rgba(8,8,15,0.7)';
  }
});
</script>
</body>
</html>
