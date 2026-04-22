<html lang="en" data-theme="light">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
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
    .wrapper { max-width: 640px; margin: 0 auto; padding: 4rem 1.6rem 7rem; }

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
      cursor: pointer;
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
    .theme-toggle:hover { color: var(--fg); border-color: var(--faint); background: var(--card); }

    /* ── Typography ── */
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
    h3::after { content: ''; flex: 1; height: 1px; background: var(--border); }

    /* ── Bio / Home ── */
    .bio { margin-bottom: 2.8rem; opacity: 0; animation: fadeUp 0.45s 0.19s forwards; }
    .bio-intro { font-size: 0.87rem; color: var(--fg); margin-bottom: 1.5rem; }
    .timeline { border-top: 1px solid var(--border); margin-bottom: 1.5rem; }
    .trow {
      display: grid;
      grid-template-columns: 7.5rem 1fr;
      gap: 1rem;
      padding: 0.62rem 0;
      border-bottom: 1px solid var(--border);
      font-size: 0.83rem;
      align-items: baseline;
    }
    .tlabel { color: var(--muted); font-size: 0.74rem; letter-spacing: 0.02em; }
    .tdesc { color: var(--fg); }
    .tdesc a {
      color: var(--fg);
      text-decoration: underline;
      text-decoration-color: var(--border);
      text-underline-offset: 3px;
      transition: color var(--t), text-decoration-color var(--t);
    }
    .tdesc a:hover { color: var(--accent2); text-decoration-color: var(--accent2); }
    [data-theme="dark"] .tdesc a:hover { color: var(--accent); text-decoration-color: var(--accent); }
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
    [data-theme="dark"] .badge { border-color: var(--accent); color: var(--accent); }
    .bio-note { font-size: 0.83rem; color: var(--muted); line-height: 1.65; max-width: 500px; }
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
    .loc-dot { width: 5px; height: 5px; border-radius: 50%; background: var(--accent2); flex-shrink: 0; }
    [data-theme="dark"] .loc-dot { background: var(--accent); }
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
    .about-section { opacity: 0; animation: fadeUp 0.45s 0.34s forwards; }
    .about-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 0.75rem; }
    .about-card {
      background: var(--card);
      border: 1px solid var(--border);
      padding: 1rem 1.1rem;
      border-radius: 2px;
      transition: border-color var(--t);
    }
    .about-card:hover { border-color: var(--faint); }
    .card-label { font-size: 0.67rem; text-transform: uppercase; letter-spacing: 0.1em; color: var(--muted); margin-bottom: 0.3rem; }
    .card-value { font-size: 0.84rem; color: var(--fg); line-height: 1.55; }

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

    /* ── Page views ── */
    .page { display: none; }
    .page.active { display: block; }

    /* ── Notes list ── */
    .notes-header {
      opacity: 0;
      animation: fadeUp 0.45s 0.07s forwards;
    }
    .notes-title {
      font-family: var(--serif);
      font-size: clamp(1.8rem, 5vw, 2.6rem);
      font-weight: 400;
      line-height: 1.1;
      letter-spacing: -0.01em;
      margin-bottom: 0.6rem;
    }
    .notes-title em { font-style: italic; color: var(--accent2); }
    [data-theme="dark"] .notes-title em { color: var(--accent); }
    .notes-subtitle {
      font-size: 0.8rem;
      color: var(--muted);
      margin-bottom: 2.8rem;
    }

    .notes-list {
      border-top: 1px solid var(--border);
      opacity: 0;
      animation: fadeUp 0.45s 0.18s forwards;
    }
    .note-row {
      display: grid;
      grid-template-columns: 6.5rem 1fr auto;
      gap: 1rem;
      padding: 0.9rem 0;
      border-bottom: 1px solid var(--border);
      align-items: baseline;
      cursor: pointer;
      transition: background var(--t);
      border-radius: 2px;
    }
    .note-row:hover .note-row-title { color: var(--accent2); }
    [data-theme="dark"] .note-row:hover .note-row-title { color: var(--accent); }
    .note-row-date { font-size: 0.72rem; color: var(--muted); letter-spacing: 0.02em; white-space: nowrap; }
    .note-row-title { font-size: 0.87rem; color: var(--fg); transition: color var(--t); }
    .note-row-tag {
      font-size: 0.62rem;
      letter-spacing: 0.06em;
      padding: 0.06rem 0.38rem;
      border: 1px solid var(--border);
      color: var(--muted);
      border-radius: 2px;
      white-space: nowrap;
    }
    .notes-empty {
      padding: 2.5rem 0;
      font-size: 0.82rem;
      color: var(--muted);
    }

    /* ── Single note view ── */
    #page-note { display: none; }
    #page-note.active { display: block; }

    .note-back {
      display: inline-flex;
      align-items: center;
      gap: 0.4rem;
      font-size: 0.74rem;
      color: var(--muted);
      cursor: pointer;
      margin-bottom: 2.4rem;
      transition: color var(--t);
      opacity: 0;
      animation: fadeUp 0.35s 0s forwards;
      text-decoration: none;
      letter-spacing: 0.03em;
    }
    .note-back:hover { color: var(--fg); }
    .note-back::before { content: '←'; }

    .note-meta {
      opacity: 0;
      animation: fadeUp 0.35s 0.08s forwards;
      margin-bottom: 0.5rem;
    }
    .note-meta-row {
      display: flex;
      align-items: center;
      gap: 1rem;
      margin-bottom: 0.5rem;
    }
    .note-meta-date { font-size: 0.72rem; color: var(--muted); letter-spacing: 0.02em; }
    .note-meta-tag {
      font-size: 0.62rem;
      letter-spacing: 0.06em;
      padding: 0.06rem 0.38rem;
      border: 1px solid var(--border);
      color: var(--muted);
      border-radius: 2px;
    }

    .note-view-title {
      font-family: var(--serif);
      font-size: clamp(1.7rem, 5vw, 2.4rem);
      font-weight: 400;
      line-height: 1.12;
      letter-spacing: -0.01em;
      margin-bottom: 2rem;
      opacity: 0;
      animation: fadeUp 0.35s 0.13s forwards;
    }

    .note-body {
      font-size: 0.88rem;
      line-height: 1.85;
      color: var(--fg);
      opacity: 0;
      animation: fadeUp 0.35s 0.2s forwards;
      max-width: 560px;
    }
    .note-body p { margin-bottom: 1.2rem; }
    .note-body p:last-child { margin-bottom: 0; }
    .note-body h2 {
      font-family: var(--serif);
      font-size: 1.15rem;
      font-weight: 400;
      margin: 1.8rem 0 0.5rem;
      color: var(--fg);
    }
    .note-body code {
      font-family: var(--mono);
      font-size: 0.82rem;
      background: var(--card);
      border: 1px solid var(--border);
      padding: 0.1rem 0.35rem;
      border-radius: 2px;
    }
    .note-body pre {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 2px;
      padding: 1rem 1.2rem;
      margin: 1.2rem 0;
      overflow-x: auto;
      font-size: 0.8rem;
      line-height: 1.6;
    }
    .note-body pre code { background: none; border: none; padding: 0; }
    .note-body a {
      color: var(--fg);
      text-underline-offset: 3px;
      text-decoration-color: var(--border);
    }
    .note-body a:hover { color: var(--accent2); }
    [data-theme="dark"] .note-body a:hover { color: var(--accent); }
    .note-body blockquote {
      border-left: 2px solid var(--border);
      padding-left: 1rem;
      color: var(--muted);
      margin: 1.2rem 0;
    }
    .note-divider {
      border: none;
      border-top: 1px solid var(--border);
      margin: 2.4rem 0;
      opacity: 0;
      animation: fadeUp 0.35s 0.25s forwards;
    }

    /* ── Animations ── */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(9px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    /* ── Responsive ── */
    @media (max-width: 480px) {
      .about-grid { grid-template-columns: 1fr; }
      .trow { grid-template-columns: 5.5rem 1fr; gap: 0.5rem; }
      .wrapper { padding: 2.5rem 1.2rem 5rem; }
      .note-row { grid-template-columns: 5.5rem 1fr; }
      .note-row-tag { display: none; }
    }

    ::selection { background: var(--accent2); color: #fff; }
    [data-theme="dark"] ::selection { background: var(--accent); color: #0d0d0b; }
    ::-webkit-scrollbar { width: 4px; }
    ::-webkit-scrollbar-thumb { background: var(--border); border-radius: 2px; }

    /* ── Konami overlay ── */
    #konami-overlay {
      display: none;
      position: fixed;
      inset: 0;
      z-index: 999;
      background: var(--bg);
      justify-content: center;
      align-items: center;
      flex-direction: column;
    }
    #konami-overlay.active { display: flex; animation: konamiFadeIn 0.3s ease forwards; }
    @keyframes konamiFadeIn { from { opacity: 0; } to { opacity: 1; } }
    .konami-terminal {
      border: 1px solid var(--border);
      background: var(--card);
      padding: 2rem 2.4rem;
      border-radius: 2px;
      max-width: 380px;
      width: 90%;
    }
    .konami-header {
      font-size: 0.67rem;
      text-transform: uppercase;
      letter-spacing: 0.14em;
      color: var(--muted);
      margin-bottom: 1.2rem;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }
    .konami-header::before { content: '//'; color: var(--accent2); }
    [data-theme="dark"] .konami-header::before { color: var(--accent); }
    .konami-code-display { font-size: 1.05rem; letter-spacing: 0.16em; color: var(--accent2); margin-bottom: 1.4rem; line-height: 2; }
    [data-theme="dark"] .konami-code-display { color: var(--accent); }
    .konami-msg { font-size: 0.8rem; color: var(--fg); line-height: 1.8; margin-bottom: 1.4rem; }
    .konami-msg .prompt { color: var(--muted); margin-right: 0.45rem; }
    .konami-close {
      background: none; border: 1px solid var(--border); color: var(--muted);
      font-family: var(--mono); font-size: 0.72rem; letter-spacing: 0.06em;
      padding: 0.28rem 0.65rem; cursor: pointer; border-radius: 2px;
      transition: color var(--t), border-color var(--t), background var(--t);
    }
    .konami-close:hover { color: var(--fg); border-color: var(--faint); background: var(--bg); }
    #konami-progress {
      position: fixed; bottom: 1.6rem; left: 50%; transform: translateX(-50%);
      display: flex; gap: 6px; opacity: 0; transition: opacity 0.3s ease;
      pointer-events: none; z-index: 200;
    }
    #konami-progress.visible { opacity: 1; }
    .kp-dot { width: 5px; height: 5px; border-radius: 50%; border: 1px solid var(--border); transition: background 0.15s ease, border-color 0.15s ease; }
    .kp-dot.lit { background: var(--accent2); border-color: var(--accent2); }
    [data-theme="dark"] .kp-dot.lit { background: var(--accent); border-color: var(--accent); }
    #konami-hint {
      position: fixed; bottom: 1.4rem; right: 1.6rem; font-size: 0.63rem;
      letter-spacing: 0.08em; color: var(--faint); opacity: 0; transition: opacity 0.5s ease;
      pointer-events: none; z-index: 200; font-family: var(--mono);
    }
    #konami-hint.visible { opacity: 1; }
  </style>
</head>
<body>
<div class="wrapper">

  <nav>
    <div class="nav-links">
      <a id="nav-home" class="active" onclick="showPage('home')">Home</a>
      <a id="nav-notes" onclick="showPage('notes')">Notes</a>
    </div>
    <button class="theme-toggle" onclick="toggleTheme()">
      <span id="theme-label">Dark</span>
    </button>
  </nav>

  <!-- ══ HOME PAGE ══ -->
  <div id="page-home" class="page active">
    <h1>Justin <em>Ong</em></h1>
    <div class="bio">
      <p class="bio-intro">I'm Justin. Some history:</p>
      <div class="timeline">
        <div class="trow">
          <span class="tlabel">Current</span>
          <span class="tdesc">
            <a href="https://apeironholdings.asia/" target="_blank" rel="noopener">Apeiron Holdings</a>
            — Developer <span class="badge">now</span>
          </span>
        </div>
        <div class="trow">
          <span class="tlabel">Current</span>
          <span class="tdesc">Student from <a href="https://nus.edu.sg/" target="_blank" rel="noopener">National University of Singapore</a><br/>Computer Engineering<span class="badge">now</span></span>
        </div>
      </div>
      <p class="bio-note">I like building things.</p>
      <div class="location"><span class="loc-dot"></span>Singapore</div>
    </div>

    <h3>Get in touch</h3>
    <div class="contact">
      <a href="mailto:ongjunyin@gmail.com">ongjunyin@gmail.com</a>
      <a href="https://github.com/Jong-9999" target="_blank" rel="noopener">github</a>
      <a href="https://www.linkedin.com/in/justin-ong-a69382229/" target="_blank" rel="noopener">linkedin</a>
    </div>

    <h3>About</h3>
    <div class="about-section">
      <div class="about-grid">
        <div class="about-card">
          <div class="card-label">Current role</div>
          <div class="card-value">Apeiron Holdings<br/>Technology</div>
        </div>
        <div class="about-card">
          <div class="card-label">Interests</div>
          <div class="card-value">Embedded engineering</div>
        </div>
        <div class="about-card">
          <div class="card-label">Based in</div>
          <div class="card-value">Singapore, SG</div>
        </div>
        <div class="about-card">
          <div class="card-label">Background</div>
          <div class="card-value">Embedded engineering<br/>C, C++</div>
        </div>
      </div>
    </div>
    <footer>© 2025 Justin Ong</footer>
  </div>

  <!-- ══ NOTES LIST PAGE ══ -->
  <div id="page-notes" class="page">
    <div class="notes-header">
      <div class="notes-title">Notes <em>&</em> writing</div>
      <div class="notes-subtitle">Occasional thoughts on building things.</div>
    </div>
    <div class="notes-list" id="notes-list-container"></div>
    <footer style="margin-top:4rem;padding-top:1.4rem;border-top:1px solid var(--border);font-size:0.71rem;color:var(--faint);letter-spacing:0.04em;">© 2025 Justin Ong</footer>
  </div>

  <!-- ══ SINGLE NOTE PAGE ══ -->
  <div id="page-note" class="page">
    <a class="note-back" onclick="showPage('notes')">back to notes</a>
    <div class="note-meta">
      <div class="note-meta-row">
        <span class="note-meta-date" id="note-view-date"></span>
        <span class="note-meta-tag" id="note-view-tag"></span>
      </div>
    </div>
    <h2 class="note-view-title" id="note-view-title"></h2>
    <div class="note-body" id="note-view-body"></div>
    <hr class="note-divider"/>
    <footer style="font-size:0.71rem;color:var(--faint);letter-spacing:0.04em;opacity:0;animation:fadeUp 0.35s 0.3s forwards;">© 2025 Justin Ong</footer>
  </div>

</div><!-- /wrapper -->

<!-- Konami overlay -->
<div id="konami-overlay">
  <div class="konami-terminal">
    <div class="konami-header">cheat code detected</div>
    <div class="konami-code-display">↑ ↑ ↓ ↓ ← → ← → B A</div>
    <div class="konami-msg">
      <span class="prompt">$</span>you found it.<br/>
      <span class="prompt">$</span>not sure what you expected,<br/>
      <span class="prompt">$</span>but here we are.
    </div>
    <button class="konami-close" onclick="closeKonami()">[ close ]</button>
  </div>
</div>
<div id="konami-progress">
  <div class="kp-dot" id="kp0"></div><div class="kp-dot" id="kp1"></div>
  <div class="kp-dot" id="kp2"></div><div class="kp-dot" id="kp3"></div>
  <div class="kp-dot" id="kp4"></div><div class="kp-dot" id="kp5"></div>
  <div class="kp-dot" id="kp6"></div><div class="kp-dot" id="kp7"></div>
  <div class="kp-dot" id="kp8"></div><div class="kp-dot" id="kp9"></div>
</div>
<div id="konami-hint">↑↑↓↓←→←→BA</div>

<script>
// ══════════════════════════════════════════
//  NOTES DATA — edit this array to add notes
// ══════════════════════════════════════════
const NOTES = [
  {
    id: 'bare-metal-uart',
    date: '2025-04-10',
    tag: 'embedded',
    title: 'Bare-metal UART on STM32 without HAL',
    body: `
      <p>Most tutorials reach straight for the HAL and call it a day. That works, but I wanted to understand what was actually happening at the register level. Here's what I learned setting up UART on an STM32F4 from scratch.</p>
      <h2>Clock setup</h2>
      <p>Before touching the USART peripheral you need to enable its clock in the RCC register. For USART2 on APB1 that means setting bit 17 of <code>RCC->APB1ENR</code>. Miss this step and nothing works — no error, just silence.</p>
      <pre><code>RCC->APB1ENR |= (1 &lt;&lt; 17); // enable USART2 clock
RCC->AHB1ENR |= (1 &lt;&lt; 0);  // enable GPIOA clock</code></pre>
      <h2>GPIO alternate function</h2>
      <p>PA2 and PA3 are USART2 TX/RX. Set them to alternate function mode (10 in MODER), push-pull output, and assign AF7 in the AFR register.</p>
      <h2>Baud rate</h2>
      <p>The USART BRR register takes a divisor, not the raw baud rate. Calculate it as <code>f_CK / baud</code> where <code>f_CK</code> is the peripheral clock. At 16 MHz system clock with APB1 not divided, a 9600 baud rate gives a BRR value of 1667.</p>
      <blockquote>The HAL hides this calculation inside <code>HAL_UART_Init()</code>. Once you see it you'll never forget why baud rates need to match on both ends.</blockquote>
      <p>Once you get bytes flying across without a single HAL call, the abstraction layers start feeling a lot less magical and a lot more legible.</p>
    `
  },
  {
    id: 'why-c-still',
    date: '2025-03-02',
    tag: 'thoughts',
    title: 'Why I still reach for C first',
    body: `
      <p>People ask why I still write C when there are memory-safe alternatives. My answer is usually: because it's honest.</p>
      <p>C doesn't hide what's happening. Every malloc is visible. Every pointer dereference is deliberate. When something breaks, the bug is usually exactly where you think it is — you just have to look.</p>
      <h2>The embedded argument</h2>
      <p>On constrained hardware, C is still the lingua franca. Rust is gaining ground and I think that's genuinely good. But for now, if you want to talk to a peripheral without arguing with a toolchain, C is the path of least resistance.</p>
      <h2>What it teaches you</h2>
      <p>Writing C forces you to think about memory layout, alignment, and the actual cost of abstractions. That mental model transfers. When I read higher-level code now I have a better sense of what's expensive and what isn't.</p>
      <p>None of this is an argument against other languages. It's an argument for spending time close to the metal before you float too far above it.</p>
    `
  },
  {
    id: 'first-pcb',
    date: '2025-01-18',
    tag: 'hardware',
    title: 'First PCB spin: what I got wrong',
    body: `
      <p>Got my first PCB back from the fab last month. It mostly worked, which felt like a miracle. Here's a list of things I'll do differently next time.</p>
      <h2>Decoupling caps too far from the IC</h2>
      <p>I put the 100nF bypass caps a centimeter away from the power pins. They're supposed to be as close as physically possible — the trace inductance between the cap and the pin defeats the whole purpose. Move them first, route everything else around them.</p>
      <h2>No test points</h2>
      <p>When the board came back and one subsystem wasn't responding, I had nowhere to probe. Add test points on every supply rail and on signals you'll actually want to observe. They cost nothing and save hours.</p>
      <h2>Silkscreen over pads</h2>
      <p>Some of my reference designators overlapped with solderable pads. The fab stripped those silkscreen areas, which made the board look sloppy. Keep silkscreen off pads — most DRC rules catch this but mine was misconfigured.</p>
      <p>Overall: more fun than I expected, more humbling than I expected. Spin two is in progress.</p>
    `
  }
];

// ══════════════════════════════════════════
//  ROUTING
// ══════════════════════════════════════════
let currentPage = 'home';

function showPage(page, noteId) {
  // Hide all pages
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));

  // Update nav active state
  document.getElementById('nav-home').classList.toggle('active', page === 'home');
  document.getElementById('nav-notes').classList.toggle('active', page === 'notes' || page === 'note');

  if (page === 'home') {
    document.getElementById('page-home').classList.add('active');
  } else if (page === 'notes') {
    renderNotesList();
    document.getElementById('page-notes').classList.add('active');
  } else if (page === 'note' && noteId) {
    renderNote(noteId);
    document.getElementById('page-note').classList.add('active');
  }

  currentPage = page;
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

// ══════════════════════════════════════════
//  RENDER NOTES LIST
// ══════════════════════════════════════════
function renderNotesList() {
  const container = document.getElementById('notes-list-container');
  if (!NOTES.length) {
    container.innerHTML = '<div class="notes-empty">nothing here yet.</div>';
    return;
  }
  container.innerHTML = NOTES.map(n => `
    <div class="note-row" onclick="showPage('note', '${n.id}')">
      <span class="note-row-date">${formatDate(n.date)}</span>
      <span class="note-row-title">${n.title}</span>
      <span class="note-row-tag">${n.tag}</span>
    </div>
  `).join('');

  // Re-trigger animation
  container.style.animation = 'none';
  container.offsetHeight; // reflow
  container.style.animation = '';
}

// ══════════════════════════════════════════
//  RENDER SINGLE NOTE
// ══════════════════════════════════════════
function renderNote(id) {
  const note = NOTES.find(n => n.id === id);
  if (!note) { showPage('notes'); return; }

  document.getElementById('note-view-date').textContent = formatDate(note.date);
  document.getElementById('note-view-tag').textContent = note.tag;
  document.getElementById('note-view-title').textContent = note.title;
  document.getElementById('note-view-body').innerHTML = note.body;

  // Reset animations by re-cloning children
  ['note-view-title', 'note-view-body', 'note-view-date'].forEach(id => {
    const el = document.getElementById(id);
    if (el) { el.style.animation = 'none'; el.offsetHeight; el.style.animation = ''; }
  });
}

function formatDate(iso) {
  const [y, m, d] = iso.split('-');
  const months = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
  return `${months[+m-1]} ${+d}, ${y}`;
}

// ══════════════════════════════════════════
//  THEME
// ══════════════════════════════════════════
function toggleTheme() {
  const html = document.documentElement;
  const dark = html.getAttribute('data-theme') === 'dark';
  html.setAttribute('data-theme', dark ? 'light' : 'dark');
  document.getElementById('theme-label').textContent = dark ? 'Dark' : 'Light';
}

// ══════════════════════════════════════════
//  KONAMI
// ══════════════════════════════════════════
const KONAMI = ['ArrowUp','ArrowUp','ArrowDown','ArrowDown','ArrowLeft','ArrowRight','ArrowLeft','ArrowRight','b','a'];
let kidx = 0, kTimer = null;

setTimeout(() => {
  const hint = document.getElementById('konami-hint');
  hint.classList.add('visible');
  setTimeout(() => hint.classList.remove('visible'), 3500);
}, 10000);

document.addEventListener('keydown', (e) => {
  if (e.key === KONAMI[kidx]) {
    clearTimeout(kTimer);
    document.getElementById('konami-progress').classList.add('visible');
    document.getElementById(`kp${kidx}`).classList.add('lit');
    kidx++;
    if (kidx === KONAMI.length) { setTimeout(triggerKonami, 150); return; }
    kTimer = setTimeout(resetKonami, 2500);
  } else {
    resetKonami();
    if (e.key === KONAMI[0]) {
      kidx = 1;
      document.getElementById('konami-progress').classList.add('visible');
      document.getElementById('kp0').classList.add('lit');
      kTimer = setTimeout(resetKonami, 2500);
    }
  }
});

function resetKonami() {
  kidx = 0;
  document.getElementById('konami-progress').classList.remove('visible');
  for (let i = 0; i < 10; i++) document.getElementById(`kp${i}`).classList.remove('lit');
}
function triggerKonami() {
  resetKonami();
  document.getElementById('konami-overlay').classList.add('active');
  document.body.style.overflow = 'hidden';
}
function closeKonami() {
  document.getElementById('konami-overlay').classList.remove('active');
  document.body.style.overflow = '';
}
document.getElementById('konami-overlay').addEventListener('click', (e) => {
  if (e.target === document.getElementById('konami-overlay')) closeKonami();
});
document.addEventListener('keydown', (e) => { if (e.key === 'Escape') closeKonami(); });
</script>
</body>
</html>
