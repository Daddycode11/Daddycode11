<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Jowel Dionisio Paña — Developer Profile</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Syne:wght@400;600;800&family=JetBrains+Mono:wght@300;400;700&display=swap" rel="stylesheet"/>
<style>
  :root {
    --neon: #00FFC8;
    --pink: #FF4D7E;
    --yellow: #FFD600;
    --bg: #050A12;
    --bg2: #0B1120;
    --card: #0E1A2E;
    --border: rgba(0,255,200,0.15);
    --text: #C8D8E8;
    --muted: #5A7A9A;
    --font-display: 'Orbitron', monospace;
    --font-body: 'Syne', sans-serif;
    --font-mono: 'JetBrains Mono', monospace;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--font-body);
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom Cursor */
  .cursor {
    width: 12px; height: 12px;
    background: var(--neon);
    border-radius: 50%;
    position: fixed; pointer-events: none;
    z-index: 9999;
    transform: translate(-50%,-50%);
    transition: transform 0.1s, width 0.2s, height 0.2s;
    mix-blend-mode: difference;
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1.5px solid var(--neon);
    border-radius: 50%;
    position: fixed; pointer-events: none;
    z-index: 9998;
    transform: translate(-50%,-50%);
    transition: transform 0.15s ease, width 0.3s, height 0.3s;
    opacity: 0.5;
  }

  /* Noise Overlay */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='300' height='300'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='300' height='300' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none; z-index: 0; opacity: 0.4;
  }

  /* Animated Grid Background */
  .grid-bg {
    position: fixed; inset: 0; z-index: 0;
    background-image:
      linear-gradient(rgba(0,255,200,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,255,200,0.03) 1px, transparent 1px);
    background-size: 50px 50px;
    animation: gridShift 20s linear infinite;
  }
  @keyframes gridShift {
    0% { background-position: 0 0; }
    100% { background-position: 50px 50px; }
  }

  /* Glow Blobs */
  .blob {
    position: fixed; border-radius: 50%;
    filter: blur(120px); pointer-events: none; z-index: 0;
    animation: blobDrift 15s ease-in-out infinite alternate;
  }
  .blob1 { width: 500px; height: 500px; background: rgba(0,255,200,0.06); top: -100px; left: -100px; }
  .blob2 { width: 400px; height: 400px; background: rgba(255,77,126,0.06); bottom: 10%; right: -50px; animation-delay: -7s; }
  .blob3 { width: 300px; height: 300px; background: rgba(255,214,0,0.04); top: 50%; left: 40%; animation-delay: -3s; }
  @keyframes blobDrift {
    0% { transform: translate(0,0) scale(1); }
    100% { transform: translate(30px,40px) scale(1.1); }
  }

  /* Layout */
  .container { max-width: 1000px; margin: 0 auto; padding: 0 24px; position: relative; z-index: 1; }

  /* ─── HERO ─── */
  .hero {
    min-height: 100vh;
    display: flex; align-items: center; justify-content: center;
    text-align: center; position: relative; padding: 80px 24px 60px;
  }
  .hero-inner { position: relative; z-index: 1; }

  .status-badge {
    display: inline-flex; align-items: center; gap: 8px;
    background: rgba(0,255,200,0.08);
    border: 1px solid rgba(0,255,200,0.25);
    border-radius: 100px;
    padding: 6px 16px;
    font-family: var(--font-mono);
    font-size: 12px; color: var(--neon);
    margin-bottom: 32px;
    animation: fadeSlideUp 0.6s ease both;
  }
  .status-dot {
    width: 7px; height: 7px; border-radius: 50%;
    background: var(--neon);
    animation: pulse 1.5s ease infinite;
  }
  @keyframes pulse {
    0%,100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.4; transform: scale(0.7); }
  }

  .hero-name {
    font-family: var(--font-display);
    font-size: clamp(2.4rem, 7vw, 5.5rem);
    font-weight: 900;
    line-height: 1.0;
    letter-spacing: -0.02em;
    background: linear-gradient(135deg, #fff 0%, var(--neon) 60%, #00A882 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
    animation: fadeSlideUp 0.7s 0.1s ease both;
    position: relative;
  }

  /* Glitch Effect */
  .hero-name::before, .hero-name::after {
    content: attr(data-text);
    position: absolute; inset: 0;
    background: linear-gradient(135deg, #fff 0%, var(--neon) 60%, #00A882 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
    animation: glitch 4s infinite;
  }
  .hero-name::before { left: 2px; animation-delay: 0.5s; clip-path: polygon(0 20%, 100% 20%, 100% 35%, 0 35%); }
  .hero-name::after  { left: -2px; animation-delay: 1s;  clip-path: polygon(0 65%, 100% 65%, 100% 80%, 0 80%); }
  @keyframes glitch {
    0%,90%,100% { transform: translate(0); opacity: 0; }
    92% { transform: translate(-3px, 1px); opacity: 0.7; }
    94% { transform: translate(3px, -1px); opacity: 0.7; }
    96% { transform: translate(0); opacity: 0; }
  }

  .hero-role {
    font-family: var(--font-mono);
    font-size: clamp(0.85rem, 2vw, 1.1rem);
    color: var(--muted);
    margin-top: 16px;
    letter-spacing: 0.12em;
    animation: fadeSlideUp 0.7s 0.2s ease both;
  }
  .hero-role span { color: var(--pink); }

  .hero-desc {
    font-size: clamp(0.95rem, 2vw, 1.1rem);
    color: var(--text); line-height: 1.75;
    max-width: 640px; margin: 28px auto 0;
    animation: fadeSlideUp 0.7s 0.3s ease both;
    opacity: 0.85;
  }
  .hero-desc strong { color: var(--neon); font-weight: 600; }

  .hero-cta {
    display: flex; gap: 14px; justify-content: center; flex-wrap: wrap;
    margin-top: 40px;
    animation: fadeSlideUp 0.7s 0.4s ease both;
  }
  .btn {
    display: inline-flex; align-items: center; gap: 8px;
    padding: 12px 28px; border-radius: 8px;
    font-family: var(--font-mono); font-size: 13px; font-weight: 700;
    letter-spacing: 0.05em; text-decoration: none;
    transition: all 0.25s ease; cursor: none;
  }
  .btn-primary {
    background: var(--neon); color: #000;
    box-shadow: 0 0 20px rgba(0,255,200,0.3);
  }
  .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 0 35px rgba(0,255,200,0.55); }
  .btn-ghost {
    border: 1.5px solid rgba(0,255,200,0.3); color: var(--neon);
    background: transparent;
  }
  .btn-ghost:hover { background: rgba(0,255,200,0.08); transform: translateY(-2px); }

  .hero-gif {
    margin-top: 56px;
    display: flex; justify-content: center;
    animation: fadeSlideUp 0.8s 0.5s ease both;
  }
  .hero-gif img {
    width: 360px; border-radius: 16px;
    border: 1px solid var(--border);
    box-shadow: 0 0 60px rgba(0,255,200,0.12);
  }

  @keyframes fadeSlideUp {
    from { opacity: 0; transform: translateY(24px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  /* ─── SECTION COMMON ─── */
  section { padding: 100px 0; }
  .section-label {
    font-family: var(--font-mono); font-size: 11px;
    color: var(--neon); letter-spacing: 0.25em;
    text-transform: uppercase; margin-bottom: 12px;
    display: flex; align-items: center; gap: 12px;
  }
  .section-label::after {
    content: ''; flex: 1; height: 1px;
    background: linear-gradient(90deg, rgba(0,255,200,0.4), transparent);
    max-width: 80px;
  }
  .section-title {
    font-family: var(--font-display);
    font-size: clamp(1.8rem, 4vw, 2.8rem);
    font-weight: 700; line-height: 1.1;
    color: #fff; margin-bottom: 48px;
  }

  /* ─── ABOUT ─── */
  .about-grid {
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 24px;
  }
  @media(max-width:640px) { .about-grid { grid-template-columns: 1fr; } }

  .about-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px; padding: 28px;
    position: relative; overflow: hidden;
    transition: transform 0.3s, border-color 0.3s, box-shadow 0.3s;
  }
  .about-card::before {
    content: ''; position: absolute;
    top: 0; left: 0; right: 0; height: 2px;
    background: linear-gradient(90deg, var(--neon), var(--pink));
    opacity: 0; transition: opacity 0.3s;
  }
  .about-card:hover { transform: translateY(-4px); border-color: rgba(0,255,200,0.3); box-shadow: 0 12px 40px rgba(0,0,0,0.4); }
  .about-card:hover::before { opacity: 1; }
  .about-card .icon { font-size: 2rem; margin-bottom: 14px; }
  .about-card h4 { font-family: var(--font-display); font-size: 0.85rem; color: var(--neon); letter-spacing: 0.08em; margin-bottom: 8px; }
  .about-card p { font-size: 0.9rem; color: var(--text); line-height: 1.65; opacity: 0.85; }

  .about-facts {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 16px; padding: 32px; margin-top: 24px;
    display: grid; grid-template-columns: repeat(auto-fill, minmax(260px, 1fr)); gap: 16px;
  }
  .fact {
    display: flex; align-items: flex-start; gap: 12px;
    font-family: var(--font-mono); font-size: 13px; color: var(--text);
  }
  .fact .emoji { font-size: 1.1rem; margin-top: 1px; flex-shrink: 0; }
  .fact strong { color: var(--neon); }

  /* ─── SKILLS ─── */
  .skills-section { background: linear-gradient(180deg, var(--bg) 0%, var(--bg2) 50%, var(--bg) 100%); }

  .skills-grid {
    display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 16px;
  }
  .skill-group {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 14px; padding: 22px;
    transition: transform 0.3s, box-shadow 0.3s;
  }
  .skill-group:hover { transform: translateY(-4px); box-shadow: 0 16px 40px rgba(0,0,0,0.5); }
  .skill-group-title {
    font-family: var(--font-mono); font-size: 10px;
    letter-spacing: 0.2em; color: var(--neon); text-transform: uppercase;
    margin-bottom: 16px; display: flex; align-items: center; gap: 8px;
  }
  .skill-pills { display: flex; flex-wrap: wrap; gap: 8px; }
  .skill-pill {
    background: rgba(0,255,200,0.06);
    border: 1px solid rgba(0,255,200,0.15);
    border-radius: 6px; padding: 5px 10px;
    font-family: var(--font-mono); font-size: 11px;
    color: var(--text); transition: all 0.2s;
    cursor: none;
  }
  .skill-pill:hover { background: rgba(0,255,200,0.15); border-color: var(--neon); color: var(--neon); transform: scale(1.05); }

  /* tech icons row */
  .tech-icons { margin-top: 40px; text-align: center; }
  .tech-icons img { border-radius: 12px; max-width: 100%; }

  /* ─── PROJECTS / FOCUS ─── */
  .focus-grid {
    display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 20px;
  }
  .focus-card {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 16px; padding: 28px 28px 24px;
    position: relative; overflow: hidden;
    transition: all 0.3s;
  }
  .focus-card::after {
    content: '';
    position: absolute; bottom: 0; left: 0; right: 0; height: 100%;
    background: linear-gradient(180deg, transparent 60%, rgba(0,255,200,0.04));
    pointer-events: none;
  }
  .focus-card:hover { transform: translateY(-6px); box-shadow: 0 20px 50px rgba(0,0,0,0.5); border-color: rgba(0,255,200,0.3); }
  .focus-tag {
    display: inline-block;
    font-family: var(--font-mono); font-size: 10px;
    padding: 3px 10px; border-radius: 100px;
    margin-bottom: 16px; letter-spacing: 0.1em; text-transform: uppercase;
  }
  .tag-web { background: rgba(0,255,200,0.1); color: var(--neon); border: 1px solid rgba(0,255,200,0.2); }
  .tag-game { background: rgba(255,77,126,0.1); color: var(--pink); border: 1px solid rgba(255,77,126,0.2); }
  .tag-mobile { background: rgba(255,214,0,0.1); color: var(--yellow); border: 1px solid rgba(255,214,0,0.2); }
  .focus-card h3 { font-family: var(--font-display); font-size: 1rem; color: #fff; margin-bottom: 10px; letter-spacing: 0.02em; }
  .focus-card p { font-size: 0.875rem; color: var(--text); line-height: 1.7; opacity: 0.8; }
  .focus-stack {
    display: flex; flex-wrap: wrap; gap: 6px; margin-top: 18px;
  }
  .stack-chip {
    font-family: var(--font-mono); font-size: 10px;
    padding: 3px 8px; border-radius: 4px;
    background: rgba(255,255,255,0.05);
    color: var(--muted); border: 1px solid rgba(255,255,255,0.07);
  }

  /* ─── STATS ─── */
  .stats-section { position: relative; }
  .stats-grid {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 16px; margin-bottom: 32px;
  }
  .stat-card {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 16px; padding: 28px;
    text-align: center; position: relative; overflow: hidden;
    transition: all 0.3s;
  }
  .stat-card:hover { border-color: rgba(0,255,200,0.35); transform: translateY(-3px); }
  .stat-card::before {
    content: ''; position: absolute; inset: 0;
    background: radial-gradient(ellipse at top, rgba(0,255,200,0.05), transparent 70%);
  }
  .stat-num {
    font-family: var(--font-display); font-size: 2.5rem;
    font-weight: 900; color: var(--neon);
    line-height: 1; margin-bottom: 6px;
  }
  .stat-label { font-size: 0.8rem; color: var(--muted); letter-spacing: 0.08em; font-family: var(--font-mono); }

  .github-images {
    display: grid; grid-template-columns: 1fr 1fr; gap: 16px;
    margin-top: 16px;
  }
  @media(max-width:640px) { .github-images { grid-template-columns: 1fr; } }
  .github-images img { width: 100%; border-radius: 12px; border: 1px solid var(--border); }
  .github-wide { grid-column: 1 / -1; }
  .trophy-img { width: 100%; border-radius: 12px; border: 1px solid var(--border); margin-top: 16px; }

  /* ─── CONNECT ─── */
  .connect-section { text-align: center; }
  .social-links { display: flex; justify-content: center; gap: 16px; flex-wrap: wrap; margin-top: 0; }
  .social-btn {
    display: inline-flex; align-items: center; gap: 10px;
    padding: 14px 26px; border-radius: 10px;
    border: 1px solid var(--border);
    background: var(--card);
    text-decoration: none; color: var(--text);
    font-family: var(--font-mono); font-size: 13px;
    transition: all 0.25s; cursor: none;
  }
  .social-btn:hover { transform: translateY(-4px); box-shadow: 0 12px 30px rgba(0,0,0,0.4); }
  .social-btn.li:hover { border-color: #0A66C2; color: #0A66C2; }
  .social-btn.fb:hover { border-color: #1877F2; color: #1877F2; }
  .social-btn.gh:hover { border-color: var(--neon); color: var(--neon); }
  .social-btn.em:hover { border-color: var(--pink); color: var(--pink); }
  .social-icon { font-size: 1.1rem; }

  /* ─── SUPPORT ─── */
  .support-section { text-align: center; }
  .support-btns { display: flex; gap: 20px; justify-content: center; flex-wrap: wrap; margin-top: 16px; }
  .support-btns img { height: 52px; border-radius: 10px; transition: transform 0.2s; }
  .support-btns img:hover { transform: translateY(-3px); }

  /* ─── FOOTER ─── */
  footer {
    border-top: 1px solid var(--border);
    padding: 40px 24px;
    text-align: center;
    position: relative; z-index: 1;
  }
  .footer-text { font-family: var(--font-mono); font-size: 12px; color: var(--muted); }
  .footer-text span { color: var(--neon); }
  .views-badge { margin-top: 16px; }
  .views-badge img { border-radius: 6px; }

  /* Scroll Reveal */
  .reveal { opacity: 0; transform: translateY(30px); transition: opacity 0.6s ease, transform 0.6s ease; }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  /* Nav */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    display: flex; justify-content: space-between; align-items: center;
    padding: 16px 40px;
    background: rgba(5,10,18,0.8);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid rgba(0,255,200,0.07);
  }
  .nav-logo {
    font-family: var(--font-display); font-size: 0.85rem;
    color: var(--neon); letter-spacing: 0.1em;
  }
  .nav-links { display: flex; gap: 24px; }
  .nav-links a {
    font-family: var(--font-mono); font-size: 11px;
    color: var(--muted); text-decoration: none;
    letter-spacing: 0.1em; transition: color 0.2s;
    cursor: none;
  }
  .nav-links a:hover { color: var(--neon); }

  @media(max-width:500px) { nav { padding: 12px 20px; } .nav-links { display: none; } }

  /* Terminal Card */
  .terminal {
    background: #070D1A; border: 1px solid rgba(0,255,200,0.15);
    border-radius: 12px; padding: 24px;
    font-family: var(--font-mono); font-size: 13px;
    margin-top: 40px; position: relative; overflow: hidden;
  }
  .terminal::before {
    content: '● ● ●';
    font-size: 10px; color: var(--muted);
    letter-spacing: 4px;
    display: block; margin-bottom: 16px;
  }
  .terminal-line { line-height: 2; }
  .t-prompt { color: var(--neon); }
  .t-cmd { color: #fff; }
  .t-comment { color: var(--muted); }
  .t-string { color: var(--pink); }
  .t-bool { color: var(--yellow); }
  .blink { animation: blink 1s step-end infinite; }
  @keyframes blink { 0%,100% { opacity: 1; } 50% { opacity: 0; } }

  /* Mood section */
  .mood-section { text-align: center; }
  .mood-img { border-radius: 16px; border: 1px solid var(--border); box-shadow: 0 0 50px rgba(0,0,0,0.6); max-width: 380px; width: 100%; }
  .mood-quote {
    font-family: var(--font-mono); font-size: 14px;
    color: var(--muted); margin-top: 24px;
    border-left: 3px solid var(--neon); padding-left: 16px;
    text-align: left; display: inline-block; line-height: 1.8;
  }
  .mood-quote span { color: var(--neon); }
</style>
</head>
<body>

<!-- Custom Cursor -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- Background Effects -->
<div class="grid-bg"></div>
<div class="blob blob1"></div>
<div class="blob blob2"></div>
<div class="blob blob3"></div>

<!-- Nav -->
<nav>
  <div class="nav-logo">JDP.DEV</div>
  <div class="nav-links">
    <a href="#about">ABOUT</a>
    <a href="#skills">SKILLS</a>
    <a href="#projects">FOCUS</a>
    <a href="#stats">STATS</a>
    <a href="#connect">CONNECT</a>
  </div>
</nav>

<!-- ─── HERO ─── -->
<section class="hero">
  <div class="hero-inner">
    <div class="status-badge">
      <div class="status-dot"></div>
      AVAILABLE FOR COLLAB · PHILIPPINES
    </div>
    <h1 class="hero-name" data-text="Jowel Dionisio Paña">Jowel Dionisio Paña</h1>
    <p class="hero-role">
      🎮 2D Game Developer &nbsp;·&nbsp; 💻 Software Developer &nbsp;·&nbsp; <span>🚀 Tech Innovator</span>
    </p>
    <p class="hero-desc">
      Transforming ideas into interactive experiences — from <strong>fun 2D games</strong> to 
      <strong>modern web & mobile apps</strong>. Clean design, smooth UX, and functional creativity 
      powered by Angular, Flutter, Laravel, and Unity.
    </p>
    <div class="hero-cta">
      <a href="mailto:mr.techdeveloper2019@gmail.com" class="btn btn-primary">📫 Get In Touch</a>
      <a href="https://github.com/daddycode11" class="btn btn-ghost" target="_blank">⚡ View GitHub</a>
    </div>
    <div class="hero-gif">
      <img src="https://media.giphy.com/media/qgQUggAC3Pfv687qPC/giphy.gif" alt="Developer at work"/>
    </div>
  </div>
</section>

<!-- ─── ABOUT ─── -->
<section id="about">
  <div class="container">
    <div class="reveal">
      <div class="section-label">01 &nbsp; WHO I AM</div>
      <h2 class="section-title">About Me</h2>
    </div>
    <div class="about-grid reveal">
      <div class="about-card">
        <div class="icon">🎮</div>
        <h4>GAME DEVELOPER</h4>
        <p>Passionate about crafting immersive 2D experiences in Unity. I love building game mechanics, creative systems, and interactive storytelling that keeps players engaged.</p>
      </div>
      <div class="about-card">
        <div class="icon">💻</div>
        <h4>SOFTWARE DEVELOPER</h4>
        <p>Building modern web and mobile applications using Angular, Flutter, and Laravel. I focus on clean architecture, scalable code, and seamless user experiences.</p>
      </div>
      <div class="about-card">
        <div class="icon">🎨</div>
        <h4>CREATIVE THINKER</h4>
        <p>Design-minded developer who bridges the gap between aesthetics and functionality. Every pixel matters — from UI polish to smooth micro-interactions.</p>
      </div>
      <div class="about-card">
        <div class="icon">🌱</div>
        <h4>LIFELONG LEARNER</h4>
        <p>Currently leveling up in Angular, Java, Laravel, and Unity. Always exploring new technologies and methodologies to stay ahead of the curve.</p>
      </div>
    </div>
    <div class="about-facts reveal">
      <div class="fact"><span class="emoji">🔭</span><span>Currently building: <strong>Angular Web-Based Booking App</strong></span></div>
      <div class="fact"><span class="emoji">🤝</span><span>Open to: <strong>Mobile & Web Collaborations</strong></span></div>
      <div class="fact"><span class="emoji">📫</span><span>Email: <strong>mr.techdeveloper2019@gmail.com</strong></span></div>
      <div class="fact"><span class="emoji">🎧</span><span>Debug mode: <strong>Always with background music</strong></span></div>
      <div class="fact"><span class="emoji">📍</span><span>Based in: <strong>Philippines</strong></span></div>
      <div class="fact"><span class="emoji">⚡</span><span>Specialty: <strong>Game Dev + Creative Systems</strong></span></div>
    </div>

    <!-- Terminal Card -->
    <div class="terminal reveal">
      <div class="terminal-line"><span class="t-prompt">~</span> <span class="t-cmd">node developer.js</span></div>
      <div class="terminal-line"><span class="t-comment">// Loading Jowel's profile...</span></div>
      <div class="terminal-line"><span class="t-prompt">›</span> name: <span class="t-string">"Jowel Dionisio Paña"</span></div>
      <div class="terminal-line"><span class="t-prompt">›</span> role: <span class="t-string">["Game Dev", "Web Dev", "Mobile Dev"]</span></div>
      <div class="terminal-line"><span class="t-prompt">›</span> open_to_work: <span class="t-bool">true</span></div>
      <div class="terminal-line"><span class="t-prompt">›</span> coffee_dependent: <span class="t-bool">true</span></div>
      <div class="terminal-line"><span class="t-prompt">›</span> music_while_coding: <span class="t-bool">always</span> <span class="blink">█</span></div>
    </div>
  </div>
</section>

<!-- ─── SKILLS ─── -->
<section id="skills" class="skills-section">
  <div class="container">
    <div class="reveal">
      <div class="section-label">02 &nbsp; TOOLKIT</div>
      <h2 class="section-title">Languages & Tools</h2>
    </div>
    <div class="skills-grid reveal">
      <div class="skill-group">
        <div class="skill-group-title">🌐 Frontend</div>
        <div class="skill-pills">
          <span class="skill-pill">HTML</span>
          <span class="skill-pill">CSS</span>
          <span class="skill-pill">JavaScript</span>
          <span class="skill-pill">TypeScript</span>
          <span class="skill-pill">Angular</span>
          <span class="skill-pill">React</span>
          <span class="skill-pill">Vue</span>
        </div>
      </div>
      <div class="skill-group">
        <div class="skill-group-title">📱 Mobile</div>
        <div class="skill-pills">
          <span class="skill-pill">Flutter</span>
          <span class="skill-pill">Dart</span>
          <span class="skill-pill">Firebase</span>
        </div>
      </div>
      <div class="skill-group">
        <div class="skill-group-title">⚙️ Backend</div>
        <div class="skill-pills">
          <span class="skill-pill">Laravel</span>
          <span class="skill-pill">PHP</span>
          <span class="skill-pill">Java</span>
          <span class="skill-pill">Python</span>
          <span class="skill-pill">MySQL</span>
        </div>
      </div>
      <div class="skill-group">
        <div class="skill-group-title">🎮 Game Dev</div>
        <div class="skill-pills">
          <span class="skill-pill">Unity</span>
          <span class="skill-pill">C#</span>
          <span class="skill-pill">Blender</span>
          <span class="skill-pill">2D Design</span>
        </div>
      </div>
      <div class="skill-group">
        <div class="skill-group-title">🛠 DevTools</div>
        <div class="skill-pills">
          <span class="skill-pill">Git</span>
          <span class="skill-pill">GitHub</span>
          <span class="skill-pill">Figma</span>
          <span class="skill-pill">VS Code</span>
        </div>
      </div>
    </div>
    <div class="tech-icons reveal">
      <img src="https://skillicons.dev/icons?i=html,css,js,ts,angular,flutter,java,laravel,php,python,mysql,firebase,unity,git,figma,react,vue,blender&theme=dark" alt="Tech stack icons"/>
    </div>
  </div>
</section>

<!-- ─── FOCUS AREAS ─── -->
<section id="projects">
  <div class="container">
    <div class="reveal">
      <div class="section-label">03 &nbsp; WHAT I BUILD</div>
      <h2 class="section-title">Focus Areas</h2>
    </div>
    <div class="focus-grid reveal">
      <div class="focus-card">
        <span class="focus-tag tag-web">WEB</span>
        <h3>Angular Web Apps</h3>
        <p>Building scalable, component-driven web applications with clean architecture, reactive state management, and polished UI interactions.</p>
        <div class="focus-stack">
          <span class="stack-chip">Angular</span>
          <span class="stack-chip">TypeScript</span>
          <span class="stack-chip">Laravel API</span>
          <span class="stack-chip">MySQL</span>
        </div>
      </div>
      <div class="focus-card">
        <span class="focus-tag tag-game">GAME</span>
        <h3>2D Game Development</h3>
        <p>Crafting engaging 2D games in Unity with creative mechanics, pixel art aesthetics, and satisfying game loops that keep players coming back.</p>
        <div class="focus-stack">
          <span class="stack-chip">Unity</span>
          <span class="stack-chip">C#</span>
          <span class="stack-chip">Blender</span>
          <span class="stack-chip">2D Physics</span>
        </div>
      </div>
      <div class="focus-card">
        <span class="focus-tag tag-mobile">MOBILE</span>
        <h3>Flutter Applications</h3>
        <p>Cross-platform mobile apps with beautiful, native-feeling UIs built with Flutter — one codebase, every device, flawless performance.</p>
        <div class="focus-stack">
          <span class="stack-chip">Flutter</span>
          <span class="stack-chip">Dart</span>
          <span class="stack-chip">Firebase</span>
          <span class="stack-chip">REST API</span>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ─── STATS ─── -->
<section id="stats" class="stats-section">
  <div class="container">
    <div class="reveal">
      <div class="section-label">04 &nbsp; BY THE NUMBERS</div>
      <h2 class="section-title">GitHub Stats</h2>
    </div>

    <div class="stats-grid reveal">
      <div class="stat-card">
        <div class="stat-num">∞</div>
        <div class="stat-label">COMMITS & COUNTING</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">5+</div>
        <div class="stat-label">TECH STACKS</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">2D</div>
        <div class="stat-label">GAME SPECIALIZATION</div>
      </div>
    </div>

    <div class="github-images reveal">
      <img src="https://github-readme-stats.vercel.app/api?username=daddycode11&show_icons=true&theme=react&hide_border=true&bg_color=0B1120&title_color=00FFC8&icon_color=FF4D7E&text_color=C8D8E8" alt="GitHub Stats"/>
      <img src="https://github-readme-streak-stats.herokuapp.com/?user=daddycode11&theme=react&hide_border=true&background=0B1120&ring=00FFC8&fire=FF4D7E&currStreakLabel=00FFC8" alt="Streak Stats"/>
      <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=daddycode11&layout=compact&theme=react&hide_border=true&bg_color=0B1120&title_color=00FFC8&text_color=C8D8E8" class="github-wide" alt="Top Languages"/>
    </div>

    <!-- Trophies -->
    <div class="reveal">
      <img src="https://github-profile-trophy.vercel.app/?username=daddycode11&theme=darkhub&no-frame=true&margin-w=10&column=7" class="trophy-img" alt="Trophies"/>
    </div>
  </div>
</section>

<!-- ─── MOOD ─── -->
<section class="mood-section">
  <div class="container">
    <div class="reveal">
      <div class="section-label">05 &nbsp; DEVELOPER LIFE</div>
      <h2 class="section-title">Current Mood</h2>
    </div>
    <div class="reveal">
      <img class="mood-img" src="https://i.pinimg.com/originals/23/9b/4f/239b4f0b4b89f99b3d460e0ed5e0a77b.gif" alt="Coding Mood"/>
      <div style="display:flex;justify-content:center;margin-top:28px;">
        <div class="mood-quote">
          "It's not a bug, it's an <span>undocumented feature</span>."<br/>
          Debugging status: <span>headphones on 🎧 · laser focused</span>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ─── CONNECT ─── -->
<section id="connect" class="connect-section">
  <div class="container">
    <div class="reveal">
      <div class="section-label" style="justify-content:center;">06 &nbsp; LET'S TALK</div>
      <h2 class="section-title">Connect With Me</h2>
      <p style="color:var(--muted);font-size:0.95rem;margin-bottom:36px;font-family:var(--font-mono);">
        Open to collaborations, freelance projects, and cool ideas. Let's build something great.
      </p>
    </div>
    <div class="social-links reveal">
      <a href="https://www.linkedin.com/in/jowel-pa%c3%b1a-bab72331a" target="_blank" class="social-btn li">
        <span class="social-icon">🔗</span> LinkedIn
      </a>
      <a href="https://www.facebook.com/jowjow.dionisio/" target="_blank" class="social-btn fb">
        <span class="social-icon">👤</span> Facebook
      </a>
      <a href="https://github.com/daddycode11" target="_blank" class="social-btn gh">
        <span class="social-icon">⚡</span> GitHub
      </a>
      <a href="mailto:mr.techdeveloper2019@gmail.com" class="social-btn em">
        <span class="social-icon">📫</span> Email Me
      </a>
    </div>
  </div>
</section>

<!-- ─── SUPPORT ─── -->
<section class="support-section">
  <div class="container">
    <div class="reveal">
      <div class="section-label" style="justify-content:center;">07 &nbsp; FUEL THE GRIND</div>
      <h2 class="section-title">Support My Work</h2>
      <p style="color:var(--muted);font-size:0.9rem;margin-bottom:28px;font-family:var(--font-mono);">
        If my projects have helped you or just made you smile, consider buying me a coffee ☕
      </p>
    </div>
    <div class="support-btns reveal">
      <a href="https://www.buymeacoffee.com/Daddycode11" target="_blank">
        <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee"/>
      </a>
      <a href="https://ko-fi.com/Daddycode11" target="_blank">
        <img src="https://cdn.ko-fi.com/cdn/kofi3.png?v=3" alt="Ko-fi"/>
      </a>
    </div>
  </div>
</section>

<!-- ─── FOOTER ─── -->
<footer>
  <div class="footer-text">
    Crafted with <span>❤️</span> & a lot of ☕ by <span>Jowel Dionisio Paña</span> · Philippines
  </div>
  <div class="footer-text" style="margin-top:8px;">
    <span>© 2025</span> · Always learning · Always building
  </div>
  <div class="views-badge" style="margin-top:16px;">
    <img src="https://komarev.com/ghpvc/?username=daddycode11&label=Profile+Views&color=00FFC8&style=flat-square" alt="Profile views"/>
  </div>
</footer>

<script>
  // Custom Cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;
  document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; cursor.style.left = mx+'px'; cursor.style.top = my+'px'; });
  function animateRing() {
    rx += (mx - rx) * 0.12;
    ry += (my - ry) *.12;
    ring.style.left = rx+'px';
    ring.style.top = ry+'px';
    requestAnimationFrame(animateRing);
  }
  animateRing();

  // Scroll Reveal
  const reveals = document.querySelectorAll('.reveal');
  const io = new IntersectionObserver(entries => {
    entries.forEach(e => { if(e.isIntersecting) { e.target.classList.add('visible'); io.unobserve(e.target); } });
  }, { threshold: 0.08 });
  reveals.forEach(el => io.observe(el));
</script>
</body>
</html>
