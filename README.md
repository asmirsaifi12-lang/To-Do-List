<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>CODESOFT Python Mini Projects</title>
  <link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;600;800&display=swap" rel="stylesheet"/>
  <style>
    :root {
      --bg: #0a0a0f;
      --surface: #111118;
      --border: #1e1e2e;
      --accent: #f7c948;
      --accent2: #4fffb0;
      --accent3: #ff6b6b;
      --text: #e8e8f0;
      --muted: #6b6b8a;
      --card-bg: #13131c;
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: 'Syne', sans-serif;
      min-height: 100vh;
      overflow-x: hidden;
    }

    /* Animated grid background */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image:
        linear-gradient(rgba(247,201,72,0.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(247,201,72,0.03) 1px, transparent 1px);
      background-size: 40px 40px;
      pointer-events: none;
      z-index: 0;
    }

    .wrapper {
      max-width: 860px;
      margin: 0 auto;
      padding: 60px 24px;
      position: relative;
      z-index: 1;
    }

    /* ── HEADER ── */
    .header {
      text-align: center;
      margin-bottom: 56px;
      animation: fadeDown 0.7s ease both;
    }

    .badge-row {
      display: flex;
      justify-content: center;
      gap: 10px;
      flex-wrap: wrap;
      margin-bottom: 24px;
    }

    .badge {
      font-family: 'Space Mono', monospace;
      font-size: 11px;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      padding: 5px 14px;
      border-radius: 4px;
      border: 1px solid;
    }
    .badge-yellow { color: var(--accent); border-color: var(--accent); background: rgba(247,201,72,0.08); }
    .badge-green  { color: var(--accent2); border-color: var(--accent2); background: rgba(79,255,176,0.08); }
    .badge-red    { color: var(--accent3); border-color: var(--accent3); background: rgba(255,107,107,0.08); }

    h1 {
      font-size: clamp(2.2rem, 6vw, 3.8rem);
      font-weight: 800;
      line-height: 1.05;
      letter-spacing: -0.02em;
    }
    h1 span.hl { color: var(--accent); }

    .sub {
      margin-top: 16px;
      color: var(--muted);
      font-size: 1rem;
      font-weight: 400;
      max-width: 520px;
      margin-inline: auto;
      line-height: 1.6;
    }

    .divider {
      height: 1px;
      background: linear-gradient(90deg, transparent, var(--accent), transparent);
      margin: 48px 0;
      opacity: 0.4;
    }

    /* ── SECTION TITLE ── */
    .section-title {
      font-family: 'Space Mono', monospace;
      font-size: 11px;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      color: var(--muted);
      margin-bottom: 24px;
      display: flex;
      align-items: center;
      gap: 12px;
    }
    .section-title::after {
      content: '';
      flex: 1;
      height: 1px;
      background: var(--border);
    }

    /* ── PROJECT CARDS ── */
    .projects {
      display: flex;
      flex-direction: column;
      gap: 16px;
    }

    .card {
      background: var(--card-bg);
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 24px 28px;
      display: grid;
      grid-template-columns: auto 1fr auto;
      align-items: center;
      gap: 20px;
      position: relative;
      overflow: hidden;
      transition: border-color 0.25s, transform 0.25s, box-shadow 0.25s;
      animation: fadeUp 0.5s ease both;
    }
    .card:nth-child(1) { animation-delay: 0.1s; }
    .card:nth-child(2) { animation-delay: 0.18s; }
    .card:nth-child(3) { animation-delay: 0.26s; }
    .card:nth-child(4) { animation-delay: 0.34s; }
    .card:nth-child(5) { animation-delay: 0.42s; }

    .card::before {
      content: '';
      position: absolute;
      left: 0; top: 0; bottom: 0;
      width: 3px;
      background: var(--accent);
      transform: scaleY(0);
      transform-origin: bottom;
      transition: transform 0.3s ease;
    }
    .card:hover::before { transform: scaleY(1); }
    .card:hover {
      border-color: rgba(247,201,72,0.3);
      transform: translateX(4px);
      box-shadow: 0 8px 32px rgba(0,0,0,0.4);
    }

    .card-num {
      font-family: 'Space Mono', monospace;
      font-size: 1.6rem;
      font-weight: 700;
      color: var(--border);
      min-width: 44px;
      transition: color 0.25s;
    }
    .card:hover .card-num { color: var(--accent); }

    .card-body { flex: 1; }
    .card-title {
      font-size: 1.1rem;
      font-weight: 600;
      margin-bottom: 6px;
    }
    .card-desc {
      font-size: 0.875rem;
      color: var(--muted);
      line-height: 1.55;
      font-weight: 400;
    }

    .card-icon {
      font-size: 1.6rem;
      opacity: 0.5;
      transition: opacity 0.25s, transform 0.25s;
    }
    .card:hover .card-icon { opacity: 1; transform: scale(1.15) rotate(-5deg); }

    /* ── FOOTER STATS ── */
    .stats {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 16px;
      margin-top: 48px;
      animation: fadeUp 0.6s 0.5s ease both;
    }

    .stat-box {
      background: var(--card-bg);
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: 20px;
      text-align: center;
    }
    .stat-num {
      font-family: 'Space Mono', monospace;
      font-size: 2rem;
      font-weight: 700;
      color: var(--accent);
    }
    .stat-label {
      font-size: 0.75rem;
      color: var(--muted);
      letter-spacing: 0.08em;
      text-transform: uppercase;
      margin-top: 4px;
    }

    /* ── FOOTER ── */
    .footer {
      margin-top: 52px;
      text-align: center;
      font-family: 'Space Mono', monospace;
      font-size: 0.75rem;
      color: var(--muted);
      animation: fadeUp 0.6s 0.6s ease both;
    }
    .footer span { color: var(--accent); }

    /* ── ANIMATIONS ── */
    @keyframes fadeDown {
      from { opacity: 0; transform: translateY(-20px); }
      to   { opacity: 1; transform: translateY(0); }
    }
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(20px); }
      to   { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body>
<div class="wrapper">

  <!-- HEADER -->
  <div class="header">
    <div class="badge-row">
      <span class="badge badge-yellow">#CODESOFT</span>
      <span class="badge badge-green">Python</span>
      <span class="badge badge-red">Mini Projects</span>
    </div>
    <h1>Python <span class="hl">Mini</span><br>Projects</h1>
    <p class="sub">
      A collection of 5 simple Python projects built for practice and learning — from CLI utilities to fun games.
    </p>
  </div>

  <div class="divider"></div>

  <!-- PROJECTS -->
  <p class="section-title">Projects</p>

  <div class="projects">

    <div class="card">
      <div class="card-num">01</div>
      <div class="card-body">
        <div class="card-title">To-Do List</div>
        <div class="card-desc">A simple command-line app to add, view and remove tasks efficiently.</div>
      </div>
      <div class="card-icon">✅</div>
    </div>

    <div class="card">
      <div class="card-num">02</div>
      <div class="card-body">
        <div class="card-title">Simple Calculator</div>
        <div class="card-desc">Performs basic arithmetic operations — addition, subtraction, multiplication, and division.</div>
      </div>
      <div class="card-icon">🧮</div>
    </div>

    <div class="card">
      <div class="card-num">03</div>
      <div class="card-body">
        <div class="card-title">Password Generator</div>
        <div class="card-desc">Generates a strong random password using a mix of letters, numbers, and symbols.</div>
      </div>
      <div class="card-icon">🔐</div>
    </div>

    <div class="card">
      <div class="card-num">04</div>
      <div class="card-body">
        <div class="card-title">Rock-Paper-Scissors Game</div>
        <div class="card-desc">Play the classic Rock-Paper-Scissors game against the computer in your terminal.</div>
      </div>
      <div class="card-icon">✊</div>
    </div>

    <div class="card">
      <div class="card-num">05</div>
      <div class="card-body">
        <div class="card-title">Contact Book</div>
        <div class="card-desc">A command-line contact book app to add, view, search, update and delete contacts.</div>
      </div>
      <div class="card-icon">📒</div>
    </div>

  </div>

  <!-- STATS -->
  <div class="stats">
    <div class="stat-box">
      <div class="stat-num">5</div>
      <div class="stat-label">Projects</div>
    </div>
    <div class="stat-box">
      <div class="stat-num">100%</div>
      <div class="stat-label">Python</div>
    </div>
    <div class="stat-box">
      <div class="stat-num">CLI</div>
      <div class="stat-label">Interface</div>
    </div>
  </div>

  <!-- FOOTER -->
  <div class="footer">
    Made with <span>♥</span> for learning &nbsp;·&nbsp; <span>#CODESOFT</span>
  </div>

</div>
</body>
</html>




