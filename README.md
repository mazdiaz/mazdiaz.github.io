<!DOCTYPE html>
<html lang="id">
<head>
  
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Your Name — Portfolio</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
  /* ---------- TOKENS ---------- */
  :root {
    --bg:        #ece8df;
    --bg-soft:   #e2ddd1;
    --ink:       #1a1a1a;
    --ink-soft:  #4a4a4a;
    --muted:     #7a766f;
    --line:      #c9c3b5;
    --line-soft: #d8d3c5;
    --accent:    #c8412c;
    --accent-2:  #2d4a3a;

    --mono: 'IBM Plex Mono', ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--ink);
    font-family: var(--mono);
    font-weight: 400;
    font-size: 15px;
    line-height: 1.6;
    -webkit-font-smoothing: antialiased;
    overflow-x: hidden;
    min-height: 100vh;
    position: relative;
  }

  ::selection { background: var(--accent); color: var(--bg); }
  a { color: inherit; text-decoration: none; }

  /* ---------- BACKGROUND (subtle) ---------- */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    pointer-events: none;
    z-index: 1;
    opacity: 0.4;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='3' stitchTiles='stitch'/%3E%3CfeColorMatrix values='0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.07 0'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  }

  .blob {
    position: fixed;
    border-radius: 50%;
    filter: blur(80px);
    opacity: 0.35;
    z-index: 0;
    pointer-events: none;
  }
  .blob-1 {
    width: 480px; height: 480px;
    background: var(--accent);
    top: -120px; right: -160px;
    animation: drift1 22s ease-in-out infinite;
  }
  .blob-2 {
    width: 380px; height: 380px;
    background: var(--accent-2);
    bottom: -140px; left: -120px;
    animation: drift2 28s ease-in-out infinite;
    opacity: 0.25;
  }
  @keyframes drift1 {
    0%, 100% { transform: translate(0, 0) scale(1); }
    50%      { transform: translate(-60px, 40px) scale(1.08); }
  }
  @keyframes drift2 {
    0%, 100% { transform: translate(0, 0) scale(1); }
    50%      { transform: translate(50px, -30px) scale(0.92); }
  }

  /* ---------- MARQUEE ---------- */
  .marquee {
    position: relative;
    z-index: 3;
    border-top: 1px solid var(--line);
    border-bottom: 1px solid var(--line);
    background: var(--bg);
    overflow: hidden;
    padding: 14px 0;
    font-size: 13px;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    font-weight: 500;
  }
  .marquee-track {
    display: flex;
    gap: 48px;
    white-space: nowrap;
    width: max-content;
    animation: scroll 38s linear infinite;
  }
  .marquee-track span { display: flex; align-items: center; gap: 48px; }
  .marquee-track span::after { content: '✦'; color: var(--accent); }
  @keyframes scroll {
    from { transform: translateX(0); }
    to   { transform: translateX(-50%); }
  }

  /* ---------- LAYOUT ---------- */
  .wrap {
    position: relative;
    z-index: 2;
    max-width: 1180px;
    margin: 0 auto;
    padding: 0 32px;
  }

  /* ---------- NAV ---------- */
  nav {
    position: sticky;
    top: 0;
    z-index: 50;
    background: rgba(236, 232, 223, 0.88);
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    border-bottom: 1px solid var(--line-soft);
  }
  nav .wrap {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-top: 18px;
    padding-bottom: 18px;
  }
  .brand {
    font-weight: 600;
    letter-spacing: -0.01em;
    font-size: 15px;
  }
  .brand .dot { color: var(--accent); margin-left: 2px; }
  .nav-links {
    display: flex;
    gap: 28px;
    list-style: none;
    font-size: 13px;
    counter-reset: navc;
  }
  .nav-links li { counter-increment: navc; }
  .nav-links a {
    color: var(--ink-soft);
    transition: color 0.2s ease;
  }
  .nav-links a::before {
    content: '0' counter(navc) '.';
    color: var(--accent);
    margin-right: 6px;
    font-weight: 500;
  }
  .nav-links a:hover { color: var(--ink); }

  /* ---------- HERO ---------- */
  header.hero {
    padding: 120px 0 80px;
    border-bottom: 1px solid var(--line-soft);
  }
  .eyebrow {
    font-size: 12px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 24px;
    display: flex;
    align-items: center;
    gap: 12px;
  }
  .eyebrow::before {
    content: '';
    width: 32px;
    height: 1px;
    background: var(--accent);
  }
  h1.display {
    font-size: clamp(40px, 7vw, 84px);
    font-weight: 500;
    line-height: 1.02;
    letter-spacing: -0.035em;
    margin-bottom: 28px;
    max-width: 14ch;
  }
  h1.display em {
    font-style: italic;
    font-weight: 300;
    color: var(--accent);
  }
  .hero-meta {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 40px;
    max-width: 720px;
    margin-top: 56px;
    padding-top: 32px;
    border-top: 1px dashed var(--line);
  }
  .hero-meta p {
    font-size: 14.5px;
    color: var(--ink-soft);
    line-height: 1.7;
  }
  .hero-meta .label {
    display: block;
    font-size: 11px;
    letter-spacing: 0.16em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 10px;
  }

  /* ---------- SECTION ---------- */
  section { padding: 96px 0; border-bottom: 1px solid var(--line-soft); }
  .section-head {
    display: flex;
    align-items: baseline;
    gap: 16px;
    margin-bottom: 56px;
  }
  .section-head .num {
    color: var(--accent);
    font-size: 13px;
    font-weight: 500;
    letter-spacing: 0.1em;
  }
  .section-head h2 {
    font-size: 28px;
    font-weight: 500;
    letter-spacing: -0.02em;
  }
  .section-head .line {
    flex: 1;
    height: 1px;
    background: var(--line);
    margin-bottom: 8px;
  }

  /* ---------- WORK ---------- */
  .work-list { list-style: none; }
  .work-item {
    display: grid;
    grid-template-columns: 80px 1fr auto;
    gap: 32px;
    padding: 32px 0;
    border-top: 1px solid var(--line-soft);
    align-items: start;
    transition: padding 0.3s ease;
    position: relative;
  }
  .work-item:last-child { border-bottom: 1px solid var(--line-soft); }
  .work-item:hover {
    padding-left: 12px;
    padding-right: 12px;
  }
  .work-item::before {
    content: '';
    position: absolute;
    left: 0; right: 0; top: 0; bottom: 0;
    background: var(--bg-soft);
    z-index: -1;
    opacity: 0;
    transition: opacity 0.3s ease;
    border-radius: 4px;
  }
  .work-item:hover::before { opacity: 1; }

  .work-num {
    font-size: 13px;
    color: var(--muted);
    font-weight: 500;
    padding-top: 6px;
    letter-spacing: 0.05em;
  }
  .work-main h3 {
    font-size: 22px;
    font-weight: 500;
    letter-spacing: -0.015em;
    margin-bottom: 8px;
    transition: color 0.2s ease;
  }
  .work-item:hover .work-main h3 { color: var(--accent); }
  .work-main .summary {
    font-size: 14px;
    color: var(--ink-soft);
    line-height: 1.65;
    margin-bottom: 14px;
    max-width: 60ch;
  }
  .stack {
    display: flex;
    flex-wrap: wrap;
    gap: 6px 8px;
    margin-bottom: 16px;
  }
  .stack span {
    font-size: 11px;
    letter-spacing: 0.06em;
    color: var(--muted);
    text-transform: uppercase;
  }
  .stack span:not(:last-child)::after {
    content: '·';
    margin-left: 8px;
    color: var(--line);
  }

  .actions {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }
  .btn {
    font-family: var(--mono);
    font-size: 12px;
    font-weight: 500;
    letter-spacing: 0.04em;
    padding: 9px 16px;
    background: transparent;
    color: var(--ink);
    border: 1px solid var(--line);
    border-radius: 999px;
    cursor: pointer;
    transition: all 0.2s ease;
    display: inline-flex;
    align-items: center;
    gap: 8px;
    text-transform: lowercase;
  }
  .btn:hover {
    background: var(--ink);
    color: var(--bg);
    border-color: var(--ink);
    transform: translateY(-1px);
  }
  .btn.primary {
    background: var(--accent);
    border-color: var(--accent);
    color: var(--bg);
  }
  .btn.primary:hover {
    background: var(--ink);
    border-color: var(--ink);
  }
  .btn .arrow {
    transition: transform 0.2s ease;
    display: inline-block;
  }
  .btn:hover .arrow { transform: translate(2px, -2px); }

  .work-meta {
    text-align: right;
    font-size: 12px;
    color: var(--muted);
    padding-top: 8px;
    letter-spacing: 0.05em;
  }
  .work-meta .year {
    display: block;
    font-size: 13px;
    color: var(--ink);
    font-weight: 500;
  }

  /* ---------- ABOUT ---------- */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 56px;
    align-items: start;
  }
  .about-grid p {
    font-size: 15.5px;
    line-height: 1.75;
    color: var(--ink-soft);
    margin-bottom: 18px;
  }
  .about-grid p strong { color: var(--ink); font-weight: 600; }
  .skills-list {
    list-style: none;
    font-size: 14px;
  }
  .skills-list li {
    padding: 10px 0;
    border-bottom: 1px solid var(--line-soft);
    color: var(--ink-soft);
    display: flex;
    justify-content: space-between;
    gap: 16px;
  }
  .skills-list li::before { content: '/'; color: var(--accent); margin-right: 8px; }
  .skills-list li span:last-child { color: var(--ink); font-weight: 500; }

  /* ---------- CONTACT / FOOTER ---------- */
  footer { padding: 96px 0 48px; }
  .contact-cta {
    font-size: clamp(32px, 5vw, 56px);
    font-weight: 500;
    line-height: 1.1;
    letter-spacing: -0.025em;
    max-width: 16ch;
    margin-bottom: 40px;
  }
  .contact-cta a {
    color: var(--accent);
    border-bottom: 2px solid var(--accent);
    transition: opacity 0.2s ease;
  }
  .contact-cta a:hover { opacity: 0.7; }

  .contact-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 24px;
    padding: 32px 0;
    border-top: 1px solid var(--line);
    border-bottom: 1px solid var(--line);
    margin-bottom: 32px;
  }
  .contact-grid .label {
    font-size: 11px;
    letter-spacing: 0.16em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 8px;
    display: block;
  }
  .contact-grid a {
    font-size: 14px;
    color: var(--ink);
    border-bottom: 1px solid transparent;
    transition: border-color 0.2s ease;
  }
  .contact-grid a:hover { border-bottom-color: var(--ink); }

  .footer-bottom {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 12px;
    font-size: 12px;
    color: var(--muted);
    letter-spacing: 0.03em;
  }
  .footer-bottom .pulse {
    display: inline-block;
    width: 7px; height: 7px;
    background: var(--accent);
    border-radius: 50%;
    margin-right: 6px;
    animation: pulse 1.8s ease-in-out infinite;
  }
  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50%      { opacity: 0.4; transform: scale(0.85); }
  }

  /* ---------- RESPONSIVE ---------- */
  @media (max-width: 720px) {
    .wrap { padding: 0 20px; }
    nav .wrap { padding-top: 14px; padding-bottom: 14px; }
    .nav-links { gap: 16px; font-size: 12px; }
    .nav-links a::before { display: none; }
    header.hero { padding: 70px 0 56px; }
    .hero-meta { grid-template-columns: 1fr; gap: 24px; margin-top: 36px; }
    section { padding: 64px 0; }
    .section-head { margin-bottom: 36px; }
    .work-item {
      grid-template-columns: 1fr;
      gap: 12px;
      padding: 24px 0;
    }
    .work-num { padding-top: 0; font-size: 12px; }
    .work-meta { text-align: left; }
    .about-grid { grid-template-columns: 1fr; gap: 32px; }
    .work-item:hover { padding-left: 0; padding-right: 0; }
  }

  /* ---------- ENTRY ---------- */
  .reveal {
    opacity: 0;
    transform: translateY(16px);
    animation: reveal 0.7s cubic-bezier(0.2, 0.7, 0.2, 1) forwards;
  }
  @keyframes reveal {
    to { opacity: 1; transform: translateY(0); }
  }
</style>
</head>
<body>

<div class="blob blob-1"></div>
<div class="blob blob-2"></div>

<nav>
  <div class="wrap">
    <a href="#" class="brand">DIaz Hylmi Lutfiazka<span class="dot">.</span></a>
    <ul class="nav-links">
      <li><a href="#work">work</a></li>
      <li><a href="#about">about</a></li>
      <li><a href="#contact">contact</a></li>
    </ul>
  </div>
</nav>

<header class="hero">
  <div class="wrap">
    <div class="eyebrow reveal">Portfolio · 2026</div>
    <h1 class="display reveal" style="animation-delay:0.05s">
      Building thoughtful <em>digital things</em> for the web.
    </h1>
    <div class="hero-meta reveal" style="animation-delay:0.15s">
      <div>
        <span class="label">Currently</span>
        <p>Software engineer based in Jakarta, working on web apps and the occasional weekend experiment.</p>
      </div>
      <div>
        <span class="label">Focus</span>
        <p>Frontend craft, design systems, and building products that respect the people using them.</p>
      </div>
    </div>
  </div>
</header>

<div class="marquee" aria-hidden="true">
  <div class="marquee-track">
    <span>Available for freelance</span>
    <span>Available for freelance</span>
    <span>Available for freelance</span>
    <span>Available for freelance</span>
    <span>Available for freelance</span>
    <span>Available for freelance</span>
  </div>
</div>

<section id="work">
  <div class="wrap">
    <div class="section-head">
      <span class="num">01 /</span>
      <h2>My Projects</h2>
      <span class="line"></span>
      <span class="num">04 projects</span>
    </div>

    <ul class="work-list">

      <li class="work-item">
        <div class="work-num">001</div>
        <div class="work-main">
          <h3>Outfitly</h3>
          <p class="summary">A modern e-commerce platform for fashion enthusiasts. Based on PHP and Laravel.</p>
          <div class="stack">
            <span>PHP</span><span>Laravel</span><span>Postgres</span>
          </div>
          <div class="actions">
            <a href="https://outfitly-three.vercel.app/" class="btn primary" target="_blank" rel="noopener">live <span class="arrow">↗</span></a>
            <a href="https://github.com/mazdiaz/Laravel-Project/" class="btn" target="_blank" rel="noopener">github</a>
          </div>
        </div>
        <div class="work-meta">
          <span class="year">2025</span>
          <span>Team of 6</span>
        </div>
      </li>

      <li class="work-item">
        <div class="work-num">002</div>
        <div class="work-main">
          <h3>Project Two</h3>
          <p class="summary">Another concise description. Mention the impact: users, scale, or the interesting technical challenge you tackled.</p>
          <div class="stack">
            <span>Python</span><span>FastAPI</span><span>Redis</span>
          </div>
          <div class="actions">
            <a href="#" class="btn primary" target="_blank" rel="noopener">live <span class="arrow">↗</span></a>
            <a href="#" class="btn" target="_blank" rel="noopener">github</a>
          </div>
        </div>
        <div class="work-meta">
          <span class="year">2025</span>
          <span>team of 3</span>
        </div>
      </li>

      <li class="work-item">
        <div class="work-num">003</div>
        <div class="work-main">
          <h3>Project Three</h3>
          <p class="summary">A weekend hack or side project. These count too — they show curiosity and personality outside of work hours.</p>
          <div class="stack">
            <span>Rust</span><span>WASM</span>
          </div>
          <div class="actions">
            <a href="#" class="btn" target="_blank" rel="noopener">github</a>
            <a href="#" class="btn" target="_blank" rel="noopener">writeup</a>
          </div>
        </div>
        <div class="work-meta">
          <span class="year">2024</span>
          <span>open source</span>
        </div>
      </li>

      <li class="work-item">
        <div class="work-num">004</div>
        <div class="work-main">
          <h3>Project Four</h3>
          <p class="summary">The one you're proudest of. Lead with impact: what changed because this exists in the world.</p>
          <div class="stack">
            <span>Go</span><span>Kubernetes</span><span>gRPC</span>
          </div>
          <div class="actions">
            <a href="#" class="btn primary" target="_blank" rel="noopener">live <span class="arrow">↗</span></a>
            <a href="#" class="btn" target="_blank" rel="noopener">github</a>
          </div>
        </div>
        <div class="work-meta">
          <span class="year">2024</span>
          <span>team of 6</span>
        </div>
      </li>

    </ul>
  </div>
</section>

<section id="about">
  <div class="wrap">
    <div class="section-head">
      <span class="num">02 /</span>
      <h2>About</h2>
      <span class="line"></span>
    </div>

    <div class="about-grid">
      <div>
        <p>Hi, I'm <strong>Diaz Hylmi Lutfiakza</strong>, an Information Technology student who is passionate about cybersecurity and secure technology. I enjoy exploring how systems work, understanding <strong>vulnerabilities</strong>, and learning how to protect applications and networks from real security risks.</p>
        <p>My current learning focuses on web application security, vulnerability assessment, network scanning, Linux, SQL, threat detection, and incident response. I have worked with tools such as Kali Linux, Nmap, Burp Suite, SQLMap, Metasploit, Wireshark, DVWA, VirtualBox, and VMware through hands-on lab practice.</p>
        <p>Currently open to freelance and collaboration. If you have something interesting in mind, get in touch.</p>
      </div>
      <ul class="skills-list">
        <li><span>cybersecurity</span><span>vulnerability assessment · threat detection · incident response</span></li>
        <li><span>web security</span><span>owasp top 10 · sql injection · burp suite · sqlmap</span></li>
        <li><span>network security</span><span>nmap · service enumeration · vulnerability scanning</span></li>
        <li><span>operating system</span><span>linux · kali linux · windows</span></li>
        <li><span>security tools</span><span>nmap · burp suite · sqlmap · metasploit · wireshark</span></li>
        <li><span>programming</span><span>python · sql · c/c++ · php</span></li>
        <li><span>web development</span><span>laravel · mysql · postgresql · html/css</span></li>
        <li><span>virtualization</span><span>virtualbox · vmware · metasploitable</span></li>
        <li><span>writing</span><span>technical documentation · vulnerability reporting</span></li>
        <li><span>language</span><span>en · id</span></li>
      </ul>
    </div>
  </div>
</section>

<footer id="contact">
  <div class="wrap">
    <p class="contact-cta">
      Have a project in mind?<br>
      Let's <a href="mailto:diazhylmi27@gmail.com">talk</a>.
    </p>

    <div class="contact-grid">
      <div>
        <span class="label">Email</span>
        <a href="mailto:diazhylmi27@gmail.com">diazhylmi27@gmail.com</a>
      </div>
      <div>
        <span class="label">GitHub</span>
        <a href="https://github.com/mazdiaz" target="_blank" rel="noopener">@mazdiaz</a>
      </div>
      <div>
        <span class="label">LinkedIn</span>
        <a href="https://www.linkedin.com/in/diaz-hylmi-lutfiazka-4a34142a8/" target="_blank" rel="noopener">/in/Diaz Hylmi Lutfiazka</a>
      </div>
    </div>

    <div class="footer-bottom">
      <span><span class="pulse"></span>Available for new work</span>
      <span>© <span id="year"></span> Diaz Hylmi Lutfiazka · Made with care in Jakarta</span>
    </div>
  </div>
</footer>

<script>
  document.getElementById('year').textContent = new Date().getFullYear();

  // Tombol placeholder → flash 'soon'
  document.querySelectorAll('.btn').forEach(btn => {
    btn.addEventListener('click', e => {
      if (btn.getAttribute('href') === '#') {
        e.preventDefault();
        const original = btn.innerHTML;
        btn.innerHTML = 'soon';
        btn.style.opacity = '0.6';
        setTimeout(() => {
          btn.innerHTML = original;
          btn.style.opacity = '1';
        }, 800);
      }
    });
  });

  // Reveal animation saat work item masuk viewport
  const io = new IntersectionObserver((entries) => {
    entries.forEach((entry, i) => {
      if (entry.isIntersecting) {
        entry.target.style.animation = `reveal 0.7s cubic-bezier(0.2,0.7,0.2,1) ${i * 0.05}s forwards`;
        io.unobserve(entry.target);
      }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('.work-item').forEach(el => {
    el.style.opacity = '0';
    el.style.transform = 'translateY(16px)';
    io.observe(el);
  });
</script>

</body>
</html>
