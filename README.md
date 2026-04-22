<html lang="en" data-theme="light">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Your Name</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&family=IBM+Plex+Mono:wght@300;400;500&display=swap" rel="stylesheet" />
  <style>
    :root {
      --bg:        #f7f4ef;
      --fg:        #18160f;
      --muted:     #7a7368;
      --faint:     #b8b2a8;
      --accent:    #1a3a2a;
      --accent2:   #4e8c6a;
      --border:    #dedad2;
      --card:      #efecea;
      --mono:      'IBM Plex Mono', 'Courier New', monospace;
      --serif:     'Instrument Serif', Georgia, serif;
      --t:         0.22s ease;
    }
    [data-theme="dark"] {
      --bg:        #0d0d0b;
      --fg:        #e8e3d8;
      --muted:     #807870;
      --faint:     #2e2e28;
      --accent:    #5cad84;
      --accent2:   #3d7a5c;
      --border:    #1f1f1a;
      --card:      #141410;
    }

    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { font-size: 14.5px; scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--fg);
      font-family: var(--mono);
      line-height: 1.7;
      min-height: 100vh;
      transition: background var(--t), color var(--t);
    }

    /* subtle grain */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      pointer-events: none;
      z-index: 100;
      opacity: 0.025;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
      background-size: 140px;
    }

    .wrapper {
      max-width: 640px;
      margin: 0 auto;
      padding: 4rem 1.6rem 7rem;
    }

    /* ── Nav ── */
    nav {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 3.8rem;
      opacity: 0;
      animation: fadeUp 0.45s 0s forwards;
    }
    .nav-links { display: flex; gap: 1.4rem; }
    .nav-links a {
      font-size: 0.78rem;
      color: var(--muted);
      text-decoration: none;
      letter-spacing: 0.04em;
      transition: color var(--t);
    }
    .nav-links a:hover, .nav-links a.active { color: var(--fg); }

    .theme-toggle {
      background: none;
      border: 1px solid var(--border);
      color: var(--muted);
      font-family: var(--mono);
      font-size: 0.72rem;
      letter-spacing: 0.06em;
      padding: 0.28rem 0.65rem;
      cursor: pointer;
      border-radius: 2px;
      transition: color var(--t), border-color var(--t), background var(--t);
    }
    .theme-toggle:hover {
      color: var(--fg);
      border-color: var(--faint);
      background: var(--card);
    }

    /* ── Glyph ── */
    .glyph {
      font-size: 0.82rem;
      color: var(--faint);
      letter-spacing: 0.1em;
      margin-bottom: 1.4rem;
      user-select: none;
      opacity: 0;
      animation: fadeUp 0.45s 0.07s forwards;
    }

    /* ── Name ── */
    h1 {
      font-family: var(--serif);
      font-size: clamp(2.4rem, 7vw, 3.5rem);
      font-weight: 400;
      line-height: 1.08;
      letter-spacing: -0.015em;
      margin-bottom: 2.4rem;
      opacity: 0;
      animation: fadeUp 0.45s 0.13s forwards;
    }
    h1 em { font-style: italic; color: var(--accent2); }
    [data-theme="dark"] h1 em { color: var(--accent); }

    /* ── Bio ── */
    .bio {
      margin-bottom: 2.8rem;
      opacity: 0;
      animation: fadeUp 0.45s 0.19s forwards;
    }
    .bio-intro {
      font-size: 0.87rem;
      color: var(--fg);
      margin-bottom: 1.5rem;
    }

    .timeline {
      border-top: 1px solid var(--border);
      margin-bottom: 1.5rem;
    }
    .trow {
      display: grid;
      grid-template-columns: 7.5rem 1fr;
      gap: 1rem;
      padding: 0.62rem 0;
      border-bottom: 1px solid var(--border);
      font-size: 0.83rem;
      align-items: baseline;
    }
    .tlabel {
      color: var(--muted);
      font-size: 0.74rem;
      letter-spacing: 0.02em;
    }
    .tdesc { color: var(--fg); }
    .tdesc a {
      color: var(--fg);
      text-decoration: underline;
      text-decoration-color: var(--border);
      text-underline-offset: 3px;
      transition: color var(--t), text-decoration-color var(--t);
    }
    .tdesc a:hover {
      color: var(--accent2);
      text-decoration-color: var(--accent2);
    }
    [data-theme="dark"] .tdesc a:hover {
      color: var(--accent);
      text-decoration-color: var(--accent);
    }
    .badge {
      display: inline-block;
      font-size: 0.65rem;
      letter-spacing: 0.05em;
      padding: 0.08rem 0.4rem;
      border: 1px solid var(--accent2);
      color: var(--accent2);
      border-radius: 2px;
      margin-left: 0.5rem;
      vertical-align: middle;
    }
    [data-theme="dark"] .badge {
      border-color: var(--accent);
      color: var(--accent);
    }

    .bio-note {
      font-size: 0.83rem;
      color: var(--muted);
      line-height: 1.65;
      max-width: 500px;
    }
    .bio-note strong { color: var(--fg); font-weight: 500; }

    .location {
      display: inline-flex;
      align-items: center;
      gap: 0.4rem;
      font-size: 0.74rem;
      color: var(--muted);
      border: 1px solid var(--border);
      padding: 0.22rem 0.6rem;
      border-radius: 2px;
      margin-top: 1rem;
      letter-spacing: 0.03em;
    }
    .loc-dot {
      width: 5px; height: 5px;
      border-radius: 50%;
      background: var(--accent2);
      flex-shrink: 0;
    }
    [data-theme="dark"] .loc-dot { background: var(--accent); }

    /* ── Section heading ── */
    h3 {
      font-family: var(--mono);
      font-size: 0.69rem;
      font-weight: 400;
      text-transform: uppercase;
      letter-spacing: 0.14em;
      color: var(--muted);
      margin-top: 2.8rem;
      margin-bottom: 1rem;
      display: flex;
      align-items: center;
      gap: 0.8rem;
    }
    h3::after {
      content: '';
      flex: 1;
      height: 1px;
      background: var(--border);
    }

    /* ── Contact ── */
    .contact {
      display: flex;
      flex-wrap: wrap;
      gap: 0.5rem 1.5rem;
      opacity: 0;
      animation: fadeUp 0.45s 0.27s forwards;
    }
    .contact a {
      font-size: 0.83rem;
      color: var(--fg);
      text-decoration: none;
      position: relative;
      padding-bottom: 2px;
    }
    .contact a::after {
      content: '';
      position: absolute;
      bottom: 0; left: 0; right: 0;
      height: 1px;
      background: var(--border);
      transition: background var(--t);
    }
    .contact a:hover { color: var(--accent2); }
    .contact a:hover::after { background: var(--accent2); }
    [data-theme="dark"] .contact a:hover { color: var(--accent); }
    [data-theme="dark"] .contact a:hover::after { background: var(--accent); }

    /* ── About cards ── */
    .about-section {
      opacity: 0;
      animation: fadeUp 0.45s 0.34s forwards;
    }
    .about-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 0.75rem;
    }
    @media (max-width: 480px) {
      .about-grid { grid-template-columns: 1fr; }
      .trow { grid-template-columns: 5.5rem 1fr; gap: 0.5rem; }
      .wrapper { padding: 2.5rem 1.2rem 5rem; }
    }
    .about-card {
      background: var(--card);
      border: 1px solid var(--border);
      padding: 1rem 1.1rem;
      border-radius: 2px;
      transition: border-color var(--t);
    }
    .about-card:hover { border-color: var(--faint); }
    .card-label {
      font-size: 0.67rem;
      text-transform: uppercase;
      letter-spacing: 0.1em;
      color: var(--muted);
      margin-bottom: 0.3rem;
    }
    .card-value {
      font-size: 0.84rem;
      color: var(--fg);
      line-height: 1.55;
    }

    /* ── Footer ── */
    footer {
      margin-top: 4rem;
      padding-top: 1.4rem;
      border-top: 1px solid var(--border);
      font-size: 0.71rem;
      color: var(--faint);
      letter-spacing: 0.04em;
      opacity: 0;
      animation: fadeUp 0.45s 0.44s forwards;
    }

    /* ── Keyframes ── */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(9px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    ::selection { background: var(--accent2); color: #fff; }
    [data-theme="dark"] ::selection { background: var(--accent); color: #0d0d0b; }
    ::-webkit-scrollbar { width: 4px; }
    ::-webkit-scrollbar-thumb { background: var(--border); border-radius: 2px; }
  </style>
</head>
<body>
<div class="wrapper">

  <!-- Nav -->
  <nav>
    <div class="nav-links">
      <a href="#" class="active">Home</a>
      <a href="#">Notes</a>
    </div>
    <button class="theme-toggle" onclick="toggleTheme()">
      <span id="theme-label">Dark</span>
    </button>
  </nav>



  <!-- Name -->
  <h1>Justin <em>Ong</em></h1>

  <!-- Bio -->
  <div class="bio">
    <p class="bio-intro">I'm Justin. Some history:</p>

    <div class="timeline">
      <div class="trow">
        <span class="tlabel">Current</span>
        <span class="tdesc">
          <a href="https://apeironholdings.asia/" target="_blank" rel="noopener">Apeiron Holdings</a>
          — Developer
          <span class="badge">now</span>
        </span>
      </div>
      <div class="trow">
        <span class="tlabel">Current</span>
        <span class="tdesc">Student from <a href="https://nus.edu.sg/" target="_blank" rel="noopener">National University of Singapore</a><br/> Computer Engineering<span class="badge">now</span></span>
      </div>
    </div>

    <p class="bio-note">
      I like building things.
    </p>

    <div class="location">
      <span class="loc-dot"></span>
      Singapore
    </div>
  </div>

  <!-- Contact -->
  <h3>Get in touch</h3>
  <div class="contact">
    <a href="mailto:ongjunyin@gmail.com">ongjunyin@gmail.com</a>
    <a href="https://github.com/Jong-9999" target="_blank" rel="noopener">github</a>
    <a href="https://www.linkedin.com/in/justin-ong-a69382229/" target="_blank" rel="noopener">linkedin</a>
  </div>

  <!-- About -->
  <h3>About</h3>
  <div class="about-section">
    <div class="about-grid">
      <div class="about-card">
        <div class="card-label">Current role</div>
        <div class="card-value">Apeiron Holdings<br/>Technology</div>
      </div>
      <div class="about-card">
        <div class="card-label">Interests</div>
        <div class="card-value">Embedded engineering <br/></div>
      </div>
      <div class="about-card">
        <div class="card-label">Based in</div>
        <div class="card-value">Singapore, SG</div>
      </div>
      <div class="about-card">
        <div class="card-label">Background</div>
        <div class="card-value">Embedded engineering <br/> C,C++</div>
      </div>
    </div>
  </div>

  <!-- Footer -->
  <footer>© 2025 Justin Ong</footer>

</div>
<script>
  function toggleTheme() {
    const html = document.documentElement;
    const dark = html.getAttribute('data-theme') === 'dark';
    html.setAttribute('data-theme', dark ? 'light' : 'dark');
    document.getElementById('theme-label').textContent = dark ? 'Dark' : 'Light';
  }
</script>
</body>
</html>
