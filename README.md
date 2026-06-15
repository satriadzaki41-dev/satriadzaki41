<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Kay – UI/UX Designer</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet"/>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --accent-blue: #3b82f6;
      --accent-cyan: #22d3ee;
      --text-primary: #f1f5f9;
      --text-muted: #94a3b8;
      --sidebar-bg: #0f172a;
      --bar-track: #1e293b;
    }

    html { scroll-behavior: smooth; }

    body {
      font-family: 'Inter', sans-serif;
      background: #a8c5f5;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      padding: 30px 16px;
    }

    /* ── SHELL: sidebar fixed + content scrollable ── */
    .shell {
      width: 100%;
      max-width: 720px;
      display: flex;
      background: #0d1224;
      border-radius: 20px;
      overflow: hidden;
      box-shadow: 0 24px 60px rgba(0,0,0,.5);
      height: fit-content;
      min-height: calc(100vh - 60px);
    }

    /* ── SIDEBAR ── */
    .sidebar {
      width: 56px;
      background: var(--sidebar-bg);
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 28px 0;
      gap: 26px;
      flex-shrink: 0;
      border-right: 1px solid #1e293b;
      position: sticky;
      top: 30px;
      height: fit-content;
    }

    .sidebar-icon {
      width: 36px; height: 36px;
      border-radius: 10px;
      display: flex; align-items: center; justify-content: center;
      cursor: pointer;
      transition: background .2s, color .2s;
      color: #475569;
      background: transparent;
      border: none;
      position: relative;
    }

    .sidebar-icon svg { width: 18px; height: 18px; }

    .sidebar-icon:hover { background: #1e293b; color: var(--accent-blue); }
    .sidebar-icon.active { background: #1e3a5f; color: var(--accent-blue); }

    /* tooltip */
    .sidebar-icon::after {
      content: attr(data-tip);
      position: absolute;
      left: 46px;
      background: #1e293b;
      color: var(--text-primary);
      font-size: .7rem;
      font-family: 'Inter', sans-serif;
      white-space: nowrap;
      padding: 4px 10px;
      border-radius: 6px;
      pointer-events: none;
      opacity: 0;
      transition: opacity .15s;
      z-index: 99;
    }

    .sidebar-icon:hover::after { opacity: 1; }

    /* ── CONTENT ── */
    .content { flex: 1; overflow: hidden; }

    /* ── SECTIONS ── */
    section {
      padding: 42px 40px;
      border-bottom: 1px solid #1a2236;
    }
    section:last-child { border-bottom: none; }

    /* ══ HERO ══ */
    #home { text-align: center; background: #0d1224; }

    .avatar-wrap {
      width: 96px; height: 96px;
      border-radius: 50%;
      margin: 0 auto 22px;
      background: linear-gradient(135deg, #6366f1, #22d3ee);
      padding: 3px;
    }
    .avatar-inner {
      width: 100%; height: 100%;
      border-radius: 50%;
      background: linear-gradient(135deg, #1e1b4b 30%, #0c4a6e);
      display: flex; align-items: center; justify-content: center;
      overflow: hidden;
    }
    .avatar-inner svg { width: 54px; height: 54px; }

    #home h1 {
      font-size: 2.1rem; font-weight: 800;
      color: var(--text-primary); margin-bottom: 8px;
    }
    #home h1 span { color: var(--accent-blue); }

    .subtitle {
      font-size: 1rem; font-weight: 600;
      color: var(--accent-cyan);
      margin-bottom: 14px;
      display: flex; align-items: center; justify-content: center; gap: 6px;
    }

    .cursor {
      display: inline-block;
      width: 2px; height: 1.1em;
      background: var(--accent-cyan);
      animation: blink .8s step-end infinite;
      vertical-align: middle;
    }

    @keyframes blink { 50% { opacity: 0; } }

    .desc {
      font-size: .84rem; color: var(--text-muted);
      line-height: 1.75; max-width: 380px; margin: 0 auto 28px;
    }

    .btn-row { display: flex; gap: 12px; justify-content: center; flex-wrap: wrap; }

    .btn-primary {
      background: var(--accent-blue);
      color: #fff; border: none;
      padding: 11px 26px; border-radius: 9px;
      font-size: .84rem; font-weight: 600;
      cursor: pointer;
      transition: background .2s, transform .15s;
      font-family: inherit;
    }
    .btn-primary:hover { background: #2563eb; transform: translateY(-1px); }
    .btn-primary:active { transform: translateY(0); }

    .btn-outline {
      background: transparent;
      color: var(--text-primary);
      border: 1.5px solid #334155;
      padding: 11px 26px; border-radius: 9px;
      font-size: .84rem; font-weight: 600;
      cursor: pointer;
      transition: border-color .2s, background .2s, transform .15s;
      font-family: inherit;
      display: flex; align-items: center; gap: 7px;
      text-decoration: none;
    }
    .btn-outline:hover { border-color: var(--accent-blue); background: #1e293b; transform: translateY(-1px); }
    .btn-outline:active { transform: translateY(0); }

    /* ══ ABOUT ══ */
    #about { background: #0e1525; }

    .about-grid {
      display: grid;
      grid-template-columns: auto 1fr;
      gap: 28px;
      align-items: start;
    }

    .about-avatar {
      width: 110px; height: 110px;
      border-radius: 16px;
      background: linear-gradient(135deg, #1e3a8a, #6d28d9);
      display: flex; align-items: center; justify-content: center;
      flex-shrink: 0;
    }
    .about-avatar svg { width: 60px; height: 60px; }

    .about-text h2 { font-size: 1.4rem; font-weight: 700; color: var(--text-primary); margin-bottom: 10px; }
    .about-text h2 span { color: var(--accent-blue); }
    .about-text p { font-size: .82rem; color: var(--text-muted); line-height: 1.75; margin-bottom: 12px; }

    .info-chips { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 4px; }
    .chip {
      font-size: .72rem; background: #1e293b;
      color: var(--text-muted); padding: 5px 12px;
      border-radius: 99px; display: flex; align-items: center; gap: 5px;
    }
    .chip span { color: var(--accent-cyan); font-weight: 600; }

    /* ══ SKILLS ══ */
    #skills { background: #0d1224; }

    .skills-header { display: flex; align-items: center; gap: 28px; margin-bottom: 28px; }

    .orb-wrap {
      flex-shrink: 0;
      width: 120px; height: 120px;
      position: relative;
      display: flex; align-items: center; justify-content: center;
    }

    .orb {
      width: 100px; height: 100px;
      border-radius: 50%;
      background: radial-gradient(circle at 35% 35%, #6366f1 0%, #0f172a 70%);
      box-shadow: 0 0 36px #6366f180;
      display: flex; align-items: center; justify-content: center;
    }

    .badge {
      position: absolute;
      border-radius: 50%;
      width: 30px; height: 30px;
      display: flex; align-items: center; justify-content: center;
      font-size: .55rem; font-weight: 700;
      border: 1.5px solid #334155;
      color: #fff;
    }
    .badge.b1 { top: 2px;   left: 8px;  background: #1d4ed8; }
    .badge.b2 { top: 2px;   right: 8px; background: #065f46; }
    .badge.b3 { bottom: 2px; left: 8px; background: #7c3aed; }
    .badge.b4 { bottom: 2px; right: 8px; background: #92400e; }

    .skills-intro h2 { font-size: 1.4rem; font-weight: 700; color: var(--text-primary); margin-bottom: 6px; }
    .skills-intro h2 span { color: var(--accent-blue); }
    .skills-intro p { font-size: .8rem; color: var(--text-muted); line-height: 1.7; }

    .skill-bar-wrap { margin-bottom: 12px; }
    .skill-label {
      display: flex; justify-content: space-between;
      font-size: .76rem; color: var(--text-muted); margin-bottom: 5px;
    }
    .skill-label .name { display: flex; align-items: center; gap: 6px; }
    .skill-label .name svg { width: 13px; height: 13px; }
    .track { height: 5px; background: var(--bar-track); border-radius: 99px; overflow: hidden; }
    .fill {
      height: 100%; border-radius: 99px;
      background: linear-gradient(90deg, #3b82f6, #22d3ee);
      width: 0;
      transition: width 1s cubic-bezier(.4,0,.2,1);
    }

    /* ══ PORTFOLIO ══ */
    #portfolio { background: #0e1525; }

    #portfolio h2 { font-size: 1.4rem; font-weight: 700; color: var(--text-primary); margin-bottom: 4px; }
    #portfolio h2 span { color: var(--accent-blue); }
    #portfolio .sub { font-size: .8rem; color: var(--text-muted); margin-bottom: 22px; }

    .projects-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 14px;
    }

    .project-card {
      background: #0f172a;
      border-radius: 12px;
      overflow: hidden;
      text-align: left;
      border: 1px solid #1e293b;
      cursor: pointer;
      transition: border-color .2s, transform .2s, box-shadow .2s;
    }
    .project-card:hover {
      border-color: var(--accent-blue);
      transform: translateY(-3px);
      box-shadow: 0 8px 28px rgba(59,130,246,.18);
    }

    .project-thumb { height: 110px; display: block; position: relative; overflow: hidden; }
    .project-thumb svg { display: block; width: 100%; height: 100%; }

    /* hover overlay */
    .project-thumb::after {
      content: '🔗  View Project';
      position: absolute; inset: 0;
      background: rgba(15,23,42,.85);
      display: flex; align-items: center; justify-content: center;
      font-size: .75rem; font-weight: 700; color: var(--accent-cyan);
      opacity: 0;
      transition: opacity .2s;
    }
    .project-card:hover .project-thumb::after { opacity: 1; }

    .project-info { padding: 10px; }
    .project-info h4 { font-size: .74rem; font-weight: 700; color: var(--text-primary); margin-bottom: 3px; }
    .project-info p { font-size: .63rem; color: var(--text-muted); line-height: 1.5; margin-bottom: 7px; }
    .tag-row { display: flex; flex-wrap: wrap; gap: 4px; }
    .tag { font-size: .56rem; background: #1e293b; color: var(--accent-cyan); padding: 2px 7px; border-radius: 4px; font-weight: 600; }

    /* ══ CONTACT ══ */
    #contact { background: #0d1224; }

    #contact h2 { font-size: 1.4rem; font-weight: 700; color: var(--text-primary); margin-bottom: 4px; }
    #contact h2 span { color: var(--accent-blue); }
    #contact .sub { font-size: .8rem; color: var(--text-muted); margin-bottom: 24px; }

    .contact-form { display: flex; flex-direction: column; gap: 14px; }

    .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }

    .form-group { display: flex; flex-direction: column; gap: 6px; }
    .form-group label { font-size: .74rem; font-weight: 600; color: var(--text-muted); }
    .form-group input,
    .form-group textarea {
      background: #1e293b;
      border: 1.5px solid #334155;
      border-radius: 8px;
      padding: 10px 14px;
      color: var(--text-primary);
      font-size: .82rem;
      font-family: inherit;
      outline: none;
      transition: border-color .2s;
      resize: vertical;
    }
    .form-group input:focus,
    .form-group textarea:focus { border-color: var(--accent-blue); }
    .form-group input::placeholder,
    .form-group textarea::placeholder { color: #475569; }

    .send-btn {
      background: var(--accent-blue);
      color: #fff; border: none;
      padding: 12px 28px; border-radius: 9px;
      font-size: .84rem; font-weight: 700;
      cursor: pointer;
      font-family: inherit;
      display: flex; align-items: center; gap: 8px;
      justify-content: center;
      transition: background .2s, transform .15s;
      align-self: flex-start;
    }
    .send-btn:hover { background: #2563eb; transform: translateY(-1px); }
    .send-btn:active { transform: translateY(0); }

    .toast {
      display: none;
      align-items: center; gap: 8px;
      background: #064e3b;
      border: 1px solid #059669;
      color: #6ee7b7;
      padding: 10px 16px;
      border-radius: 9px;
      font-size: .8rem; font-weight: 600;
      margin-top: 4px;
    }
    .toast.show { display: flex; }

    /* modal overlay */
    .modal-overlay {
      display: none;
      position: fixed; inset: 0;
      background: rgba(0,0,0,.7);
      z-index: 200;
      align-items: center; justify-content: center;
      padding: 20px;
    }
    .modal-overlay.open { display: flex; }

    .modal {
      background: #0f172a;
      border: 1px solid #1e293b;
      border-radius: 16px;
      padding: 28px;
      max-width: 460px; width: 100%;
      position: relative;
      animation: popIn .2s ease;
    }
    @keyframes popIn { from { transform: scale(.92); opacity: 0; } to { transform: scale(1); opacity: 1; } }

    .modal-close {
      position: absolute; top: 14px; right: 14px;
      background: #1e293b; border: none;
      color: var(--text-muted);
      width: 28px; height: 28px;
      border-radius: 50%;
      cursor: pointer; font-size: 1rem;
      display: flex; align-items: center; justify-content: center;
      transition: background .2s;
    }
    .modal-close:hover { background: #334155; color: var(--text-primary); }

    .modal h3 { font-size: 1.1rem; font-weight: 700; color: var(--text-primary); margin-bottom: 8px; }
    .modal .modal-sub { font-size: .78rem; color: var(--text-muted); margin-bottom: 18px; }
    .modal-thumb { width: 100%; height: 150px; border-radius: 10px; overflow: hidden; margin-bottom: 16px; }
    .modal-thumb svg { width: 100%; height: 100%; }
    .modal-desc { font-size: .8rem; color: var(--text-muted); line-height: 1.7; margin-bottom: 16px; }
    .modal-tags { display: flex; flex-wrap: wrap; gap: 6px; margin-bottom: 20px; }
    .modal-tag { font-size: .7rem; background: #1e293b; color: var(--accent-cyan); padding: 3px 10px; border-radius: 4px; font-weight: 600; }
    .modal-actions { display: flex; gap: 10px; }
    .modal-btn-primary {
      background: var(--accent-blue); color: #fff; border: none;
      padding: 9px 20px; border-radius: 8px;
      font-size: .8rem; font-weight: 600; cursor: pointer; font-family: inherit;
      transition: background .2s;
    }
    .modal-btn-primary:hover { background: #2563eb; }
    .modal-btn-outline {
      background: transparent; color: var(--text-muted);
      border: 1.5px solid #334155;
      padding: 9px 20px; border-radius: 8px;
      font-size: .8rem; font-weight: 600; cursor: pointer; font-family: inherit;
      transition: border-color .2s;
    }
    .modal-btn-outline:hover { border-color: #475569; color: var(--text-primary); }

    /* FAB scroll-to-top */
    .fab {
      position: fixed; bottom: 28px; right: 28px;
      width: 38px; height: 38px;
      border-radius: 50%;
      background: var(--accent-blue);
      display: flex; align-items: center; justify-content: center;
      cursor: pointer;
      box-shadow: 0 4px 16px #3b82f670;
      border: none;
      opacity: 0; pointer-events: none;
      transition: opacity .3s;
      z-index: 100;
    }
    .fab.visible { opacity: 1; pointer-events: all; }
    .fab svg { width: 16px; height: 16px; color: #fff; }
  </style>
</head>
<body>

<!-- ══ MODAL ══ -->
<div class="modal-overlay" id="modal" onclick="if(event.target===this)closeModal()">
  <div class="modal">
    <button class="modal-close" onclick="closeModal()">✕</button>
    <div id="modal-thumb" class="modal-thumb"></div>
    <h3 id="modal-title"></h3>
    <p class="modal-sub" id="modal-sub"></p>
    <p class="modal-desc" id="modal-desc"></p>
    <div class="modal-tags" id="modal-tags"></div>
    <div class="modal-actions">
      <button class="modal-btn-primary" onclick="closeModal()">Live Demo ↗</button>
      <button class="modal-btn-outline" onclick="closeModal()">View Code</button>
    </div>
  </div>
</div>

<!-- ══ SHELL ══ -->
<div class="shell">

  <!-- SIDEBAR -->
  <nav class="sidebar" id="sidebar">
    <button class="sidebar-icon active" data-section="home" data-tip="Home" onclick="scrollTo('home')">
      <svg fill="currentColor" viewBox="0 0 20 20"><path d="M10.707 2.293a1 1 0 00-1.414 0l-7 7A1 1 0 003 11h1v6a1 1 0 001 1h4v-4h2v4h4a1 1 0 001-1v-6h1a1 1 0 00.707-1.707l-7-7z"/></svg>
    </button>
    <button class="sidebar-icon" data-section="about" data-tip="About" onclick="scrollTo('about')">
      <svg fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"/></svg>
    </button>
    <button class="sidebar-icon" data-section="skills" data-tip="Skills" onclick="scrollTo('skills')">
      <svg fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/></svg>
    </button>
    <button class="sidebar-icon" data-section="portfolio" data-tip="Portfolio" onclick="scrollTo('portfolio')">
      <svg fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M3 7v10a2 2 0 002 2h14a2 2 0 002-2V9a2 2 0 00-2-2h-6l-2-2H5a2 2 0 00-2 2z"/></svg>
    </button>
    <button class="sidebar-icon" data-section="contact" data-tip="Contact" onclick="scrollTo('contact')">
      <svg fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/></svg>
    </button>
  </nav>

  <!-- CONTENT -->
  <div class="content" id="main-content">

    <!-- ══ HOME ══ -->
    <section id="home">
      <div class="avatar-wrap">
        <div class="avatar-inner">
          <svg viewBox="0 0 64 64" fill="none">
            <ellipse cx="32" cy="36" rx="22" ry="14" fill="#4f46e5"/>
            <rect x="14" y="30" width="36" height="16" rx="8" fill="#6366f1"/>
            <ellipse cx="24" cy="38" rx="6" ry="6" fill="#0ea5e9" opacity=".8"/>
            <ellipse cx="40" cy="38" rx="6" ry="6" fill="#0ea5e9" opacity=".8"/>
            <rect x="10" y="33" width="4" height="8" rx="2" fill="#818cf8"/>
            <rect x="50" y="33" width="4" height="8" rx="2" fill="#818cf8"/>
            <ellipse cx="32" cy="22" rx="10" ry="12" fill="#c4b5fd" opacity=".3"/>
          </svg>
        </div>
      </div>
      <h1>Hi, I'm <span>Kay</span></h1>
      <p class="subtitle">I'm a <span id="typed-text">UI/UX Designer</span><span class="cursor"></span></p>
      <p class="desc">I create beautiful, responsive web experiences using modern technologies. Passionate about clean code and user-centered design.</p>
      <div class="btn-row">
        <button class="btn-primary" onclick="scrollTo('portfolio')">View My Work</button>
        <a class="btn-outline" onclick="downloadCV()" href="#" id="cv-btn">
          <svg width="14" height="14" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M12 10v6m0 0l-3-3m3 3l3-3M3 17V7a2 2 0 012-2h6l2 2h6a2 2 0 012 2v8a2 2 0 01-2 2H5a2 2 0 01-2-2z"/></svg>
          Download CV
        </a>
      </div>
    </section>

    <!-- ══ ABOUT ══ -->
    <section id="about">
      <div class="about-grid">
        <div class="about-avatar">
          <svg viewBox="0 0 64 64" fill="none">
            <circle cx="32" cy="22" r="12" fill="#818cf8" opacity=".6"/>
            <ellipse cx="32" cy="50" rx="18" ry="12" fill="#6366f1" opacity=".5"/>
            <circle cx="32" cy="22" r="8" fill="#c4b5fd" opacity=".7"/>
          </svg>
        </div>
        <div class="about-text">
          <h2>About <span>Me</span></h2>
          <p>I'm Kay, a UI/UX Designer & Frontend Developer based in Indonesia with 3+ years of experience crafting modern digital experiences. I love turning complex problems into clean, intuitive interfaces.</p>
          <p>When I'm not pushing pixels, I'm exploring new technologies and contributing to open-source projects.</p>
          <div class="info-chips">
            <div class="chip">📍 <span>Indonesia</span></div>
            <div class="chip">🎓 <span>Computer Science</span></div>
            <div class="chip">💼 <span>Open to Work</span></div>
            <div class="chip">🌐 <span>kay.dev</span></div>
          </div>
        </div>
      </div>
    </section>

    <!-- ══ SKILLS ══ -->
    <section id="skills">
      <div class="skills-header">
        <div class="orb-wrap">
          <div class="badge b1">R</div>
          <div class="badge b2">Py</div>
          <div class="orb">
            <svg width="44" height="44" viewBox="0 0 50 50" fill="none">
              <path d="M25 5 C15 5 8 15 8 25 S15 45 25 45 42 35 42 25 35 5 25 5Z" fill="#4f46e5" opacity=".7"/>
              <path d="M25 12 C18 12 13 18 13 25 S18 38 25 38 37 32 37 25 32 12 25 12Z" fill="#6366f1" opacity=".5"/>
            </svg>
          </div>
          <div class="badge b3">V</div>
          <div class="badge b4">Tw</div>
        </div>
        <div class="skills-intro">
          <h2>My <span>Skills</span></h2>
          <p>Passionate web developer with 3+ years building modern, responsive applications using cutting-edge technologies.</p>
        </div>
      </div>

      <div class="skill-bar-wrap">
        <div class="skill-label">
          <span class="name"><svg viewBox="0 0 24 24" fill="#61dafb"><circle cx="12" cy="12" r="2"/><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2z" fill="none" stroke="#61dafb" stroke-width="1.5"/></svg>React</span>
          <span>90%</span>
        </div>
        <div class="track"><div class="fill" data-width="90"></div></div>
      </div>
      <div class="skill-bar-wrap">
        <div class="skill-label">
          <span class="name"><svg viewBox="0 0 24 24" fill="#38bdf8"><path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/></svg>Tailwind</span>
          <span>85%</span>
        </div>
        <div class="track"><div class="fill" data-width="85"></div></div>
      </div>
      <div class="skill-bar-wrap">
        <div class="skill-label">
          <span class="name"><svg viewBox="0 0 24 24" fill="#fbbf24"><path d="M12 2a10 10 0 100 20A10 10 0 0012 2z"/></svg>Python</span>
          <span>80%</span>
        </div>
        <div class="track"><div class="fill" data-width="80"></div></div>
      </div>
      <div class="skill-bar-wrap">
        <div class="skill-label">
          <span class="name"><svg viewBox="0 0 24 24" fill="#4ade80"><path d="M12 2L2 19h20L12 2z"/></svg>Vue</span>
          <span>95%</span>
        </div>
        <div class="track"><div class="fill" data-width="95"></div></div>
      </div>
    </section>

    <!-- ══ PORTFOLIO ══ -->
    <section id="portfolio">
      <h2>My <span>Portfolio</span></h2>
      <p class="sub">A collection of my recent projects — click to explore</p>

      <div class="projects-grid">

        <!-- P1: E-Commerce -->
        <div class="project-card" onclick="openModal(0)">
          <div class="project-thumb" style="background:#0d1b3e">
            <svg viewBox="0 0 220 110" xmlns="http://www.w3.org/2000/svg">
              <rect width="220" height="14" fill="#0a1628"/>
              <rect x="6" y="4" width="28" height="6" rx="2" fill="#3b82f6"/>
              <rect x="120" y="5" width="16" height="4" rx="1" fill="#334155"/>
              <rect x="140" y="5" width="16" height="4" rx="1" fill="#334155"/>
              <rect x="160" y="5" width="16" height="4" rx="1" fill="#334155"/>
              <rect x="196" y="4" width="18" height="6" rx="3" fill="#22d3ee"/>
              <rect y="14" width="220" height="28" fill="#1e3a6e"/>
              <rect x="8" y="19" width="40" height="5" rx="2" fill="#fff" opacity=".9"/>
              <rect x="8" y="27" width="28" height="3" rx="1" fill="#94a3b8"/>
              <rect x="8" y="33" width="18" height="5" rx="2" fill="#3b82f6"/>
              <rect x="148" y="16" width="66" height="24" rx="4" fill="#1e40af" opacity=".5"/>
              <circle cx="181" cy="28" r="8" fill="#3b82f6" opacity=".4"/>
              <rect y="46" width="220" height="64" fill="#0f172a"/>
              <rect x="6" y="52" width="60" height="50" rx="4" fill="#1e293b"/>
              <rect x="6" y="52" width="60" height="28" rx="4" fill="#1d4ed8" opacity=".5"/>
              <circle cx="36" cy="66" r="6" fill="#60a5fa" opacity=".5"/>
              <rect x="10" y="83" width="30" height="3" rx="1" fill="#cbd5e1" opacity=".8"/>
              <rect x="10" y="88" width="20" height="3" rx="1" fill="#22d3ee" opacity=".8"/>
              <rect x="42" y="85" width="18" height="8" rx="2" fill="#3b82f6"/>
              <rect x="80" y="52" width="60" height="50" rx="4" fill="#1e293b"/>
              <rect x="80" y="52" width="60" height="28" rx="4" fill="#7c3aed" opacity=".5"/>
              <circle cx="110" cy="66" r="6" fill="#a78bfa" opacity=".5"/>
              <rect x="84" y="83" width="30" height="3" rx="1" fill="#cbd5e1" opacity=".8"/>
              <rect x="84" y="88" width="20" height="3" rx="1" fill="#22d3ee" opacity=".8"/>
              <rect x="116" y="85" width="18" height="8" rx="2" fill="#7c3aed"/>
              <rect x="154" y="52" width="60" height="50" rx="4" fill="#1e293b"/>
              <rect x="154" y="52" width="60" height="28" rx="4" fill="#065f46" opacity=".5"/>
              <circle cx="184" cy="66" r="6" fill="#34d399" opacity=".5"/>
              <rect x="158" y="83" width="30" height="3" rx="1" fill="#cbd5e1" opacity=".8"/>
              <rect x="158" y="88" width="20" height="3" rx="1" fill="#22d3ee" opacity=".8"/>
              <rect x="190" y="85" width="18" height="8" rx="2" fill="#059669"/>
              <circle cx="207" cy="6" r="5" fill="#ef4444"/>
              <text x="207" y="8.5" text-anchor="middle" fill="#fff" font-size="5" font-family="sans-serif" font-weight="bold">3</text>
            </svg>
          </div>
          <div class="project-info">
            <h4>Modern E-Commerce Platform</h4>
            <p>Full-stack e-commerce solution with React and Node.js</p>
            <div class="tag-row">
              <span class="tag">React</span><span class="tag">Node.js</span><span class="tag">MongoDB</span><span class="tag">Tailwind</span>
            </div>
          </div>
        </div>

        <!-- P2: Task App -->
        <div class="project-card" onclick="openModal(1)">
          <div class="project-thumb" style="background:#160428">
            <svg viewBox="0 0 220 110" xmlns="http://www.w3.org/2000/svg">
              <rect width="220" height="110" fill="#160428"/>
              <rect width="38" height="110" fill="#1e0a3c"/>
              <rect x="6" y="10" width="26" height="6" rx="3" fill="#7c3aed"/>
              <rect x="9" y="22" width="20" height="3" rx="1" fill="#6d28d9" opacity=".6"/>
              <rect x="9" y="29" width="20" height="3" rx="1" fill="#6d28d9" opacity=".4"/>
              <rect x="9" y="36" width="20" height="3" rx="1" fill="#6d28d9" opacity=".4"/>
              <rect x="42" y="6" width="44" height="6" rx="2" fill="#7c3aed" opacity=".8"/>
              <rect x="42" y="18" width="52" height="86" rx="4" fill="#1e0a3c"/>
              <rect x="45" y="21" width="28" height="4" rx="1" fill="#a78bfa" opacity=".9"/>
              <rect x="45" y="28" width="46" height="14" rx="3" fill="#2e1065"/>
              <rect x="47" y="31" width="30" height="2.5" rx="1" fill="#c4b5fd" opacity=".8"/>
              <rect x="45" y="45" width="46" height="14" rx="3" fill="#2e1065"/>
              <rect x="47" y="48" width="26" height="2.5" rx="1" fill="#c4b5fd" opacity=".8"/>
              <rect x="47" y="52" width="18" height="2" rx="1" fill="#ec4899" opacity=".6"/>
              <rect x="98" y="18" width="52" height="86" rx="4" fill="#1e0a3c"/>
              <rect x="101" y="21" width="36" height="4" rx="1" fill="#f59e0b" opacity=".9"/>
              <rect x="101" y="28" width="46" height="14" rx="3" fill="#451a03" opacity=".7"/>
              <rect x="103" y="31" width="28" height="2.5" rx="1" fill="#fcd34d" opacity=".8"/>
              <rect x="103" y="38" width="40" height="2" rx="1" fill="#292524"/>
              <rect x="103" y="38" width="26" height="2" rx="1" fill="#f59e0b"/>
              <rect x="154" y="18" width="60" height="86" rx="4" fill="#1e0a3c"/>
              <rect x="157" y="21" width="22" height="4" rx="1" fill="#34d399" opacity=".9"/>
              <rect x="157" y="28" width="52" height="14" rx="3" fill="#064e3b" opacity=".5"/>
              <rect x="159" y="31" width="28" height="2.5" rx="1" fill="#6ee7b7" opacity=".8"/>
              <circle cx="200" cy="35" r="4" fill="#059669"/>
              <path d="M198 35 L200 37 L203 33" stroke="#fff" stroke-width="1" fill="none" stroke-linecap="round"/>
            </svg>
          </div>
          <div class="project-info">
            <h4>Task Management App</h4>
            <p>Productive kanban app with real-time updates</p>
            <div class="tag-row">
              <span class="tag">Vue.js</span><span class="tag">Firebase</span><span class="tag">CSS3</span>
            </div>
          </div>
        </div>

        <!-- P3: Weather -->
        <div class="project-card" onclick="openModal(2)">
          <div class="project-thumb" style="background:#021c28">
            <svg viewBox="0 0 220 110" xmlns="http://www.w3.org/2000/svg">
              <rect width="220" height="110" fill="#021c28"/>
              <rect width="220" height="12" fill="#031f2e"/>
              <rect x="6" y="3.5" width="40" height="5" rx="2" fill="#0ea5e9" opacity=".8"/>
              <rect x="6" y="16" width="80" height="50" rx="6" fill="#0c3547"/>
              <circle cx="30" cy="35" r="10" fill="#fbbf24" opacity=".9"/>
              <text x="50" y="31" fill="#fff" font-size="14" font-family="sans-serif" font-weight="bold" opacity=".95">28°</text>
              <rect x="46" y="34" width="30" height="2.5" rx="1" fill="#7dd3fc" opacity=".7"/>
              <rect x="6" y="70" width="80" height="34" rx="5" fill="#0c3547"/>
              <polyline points="10,96 28,88 46,92 64,84 82,86" stroke="#0ea5e9" stroke-width="1.5" fill="none" stroke-linecap="round"/>
              <circle cx="64" cy="84" r="2" fill="#22d3ee"/>
              <rect x="92" y="16" width="122" height="88" rx="6" fill="#0c3547"/>
              <rect x="100" y="64" width="10" height="31" rx="2" fill="#0ea5e9" opacity=".7"/>
              <rect x="115" y="52" width="10" height="43" rx="2" fill="#22d3ee" opacity=".7"/>
              <rect x="130" y="68" width="10" height="27" rx="2" fill="#0ea5e9" opacity=".7"/>
              <rect x="145" y="46" width="10" height="49" rx="2" fill="#38bdf8" opacity=".8"/>
              <rect x="160" y="56" width="10" height="39" rx="2" fill="#0ea5e9" opacity=".7"/>
              <rect x="175" y="65" width="10" height="30" rx="2" fill="#0ea5e9" opacity=".6"/>
              <rect x="190" y="48" width="10" height="47" rx="2" fill="#22d3ee" opacity=".75"/>
              <line x1="96" y1="95" x2="206" y2="95" stroke="#1e3a4f" stroke-width="1"/>
            </svg>
          </div>
          <div class="project-info">
            <h4>Weather Dashboard</h4>
            <p>Real-time weather monitoring with charts</p>
            <div class="tag-row">
              <span class="tag">React</span><span class="tag">API</span><span class="tag">Chart.js</span>
            </div>
          </div>
        </div>

        <!-- P4: Portfolio -->
        <div class="project-card" onclick="openModal(3)">
          <div class="project-thumb" style="background:#080818">
            <svg viewBox="0 0 220 110" xmlns="http://www.w3.org/2000/svg">
              <rect width="220" height="110" fill="#080818"/>
              <ellipse cx="110" cy="55" rx="90" ry="50" fill="#1e1b4b" opacity=".4"/>
              <rect width="220" height="13" fill="#0f0f1f"/>
              <rect x="6" y="4" width="22" height="5" rx="2" fill="#818cf8"/>
              <rect x="196" y="3.5" width="18" height="6" rx="3" fill="#6366f1"/>
              <circle cx="110" cy="44" r="16" fill="#1e1b4b" stroke="#6366f1" stroke-width="1.5"/>
              <circle cx="110" cy="40" r="6" fill="#a5b4fc" opacity=".6"/>
              <ellipse cx="110" cy="52" rx="10" ry="5" fill="#a5b4fc" opacity=".4"/>
              <rect x="72" y="62" width="76" height="6" rx="2" fill="#e0e7ff" opacity=".85"/>
              <rect x="82" y="70" width="56" height="3.5" rx="1" fill="#818cf8" opacity=".8"/>
              <rect x="82" y="81" width="24" height="8" rx="4" fill="#6366f1"/>
              <rect x="110" y="81" width="28" height="8" rx="4" fill="none" stroke="#475569" stroke-width="1"/>
              <rect x="20" y="95" width="180" height="12" rx="3" fill="#0f0f1f"/>
              <circle cx="38" cy="101" r="4" fill="#61dafb" opacity=".7"/>
              <circle cx="56" cy="101" r="4" fill="#4ade80" opacity=".7"/>
              <circle cx="74" cy="101" r="4" fill="#f59e0b" opacity=".7"/>
              <circle cx="92" cy="101" r="4" fill="#818cf8" opacity=".7"/>
              <circle cx="110" cy="101" r="4" fill="#f472b6" opacity=".7"/>
              <circle cx="128" cy="101" r="4" fill="#34d399" opacity=".7"/>
            </svg>
          </div>
          <div class="project-info">
            <h4>Portfolio Website</h4>
            <p>Sleek personal portfolio with animations</p>
            <div class="tag-row">
              <span class="tag">Vue.js</span><span class="tag">GSAP</span><span class="tag">CSS3</span>
            </div>
          </div>
        </div>

        <!-- P5: Dark/Light -->
        <div class="project-card" onclick="openModal(4)">
          <div class="project-thumb" style="padding:0">
            <svg viewBox="0 0 220 110" xmlns="http://www.w3.org/2000/svg">
              <rect width="110" height="110" fill="#0f172a"/>
              <rect x="4" y="6" width="102" height="8" rx="2" fill="#1e293b"/>
              <rect x="6" y="7.5" width="20" height="5" rx="1.5" fill="#3b82f6"/>
              <rect x="4" y="18" width="102" height="36" rx="4" fill="#1e293b"/>
              <circle cx="20" cy="32" r="9" fill="#312e81" opacity=".6"/>
              <rect x="32" y="25" width="42" height="4" rx="1.5" fill="#e2e8f0" opacity=".7"/>
              <rect x="32" y="42" width="22" height="6" rx="3" fill="#3b82f6"/>
              <rect x="4" y="58" width="48" height="28" rx="4" fill="#1e293b"/>
              <rect x="56" y="58" width="50" height="28" rx="4" fill="#1e293b"/>
              <line x1="110" y1="0" x2="110" y2="110" stroke="#334155" stroke-width="1.5" stroke-dasharray="4,3"/>
              <rect x="110" y="0" width="110" height="110" fill="#f1f5f9"/>
              <rect x="110" y="6" width="106" height="8" rx="2" fill="#fff"/>
              <rect x="114" y="7.5" width="20" height="5" rx="1.5" fill="#3b82f6"/>
              <rect x="114" y="18" width="102" height="36" rx="4" fill="#fff"/>
              <circle cx="130" cy="32" r="9" fill="#ede9fe" opacity=".9"/>
              <rect x="142" y="25" width="42" height="4" rx="1.5" fill="#1e293b" opacity=".8"/>
              <rect x="142" y="42" width="22" height="6" rx="3" fill="#3b82f6"/>
              <rect x="114" y="58" width="48" height="28" rx="4" fill="#fff"/>
              <rect x="166" y="58" width="50" height="28" rx="4" fill="#fff"/>
            </svg>
          </div>
          <div class="project-info">
            <h4>Dark / Light Mode UI</h4>
            <p>Adaptive UI system with theme switching</p>
            <div class="tag-row">
              <span class="tag">React</span><span class="tag">Tailwind</span>
            </div>
          </div>
        </div>

        <!-- P6: Chat App -->
        <div class="project-card" onclick="openModal(5)">
          <div class="project-thumb" style="background:#020c18">
            <svg viewBox="0 0 220 110" xmlns="http://www.w3.org/2000/svg">
              <rect width="220" height="110" fill="#020c18"/>
              <rect width="55" height="110" fill="#031525"/>
              <circle cx="13" cy="24" r="7" fill="#1d4ed8" opacity=".8"/>
              <rect x="23" y="21" width="26" height="2.5" rx="1" fill="#cbd5e1" opacity=".8"/>
              <rect x="23" y="25.5" width="18" height="2" rx="1" fill="#475569"/>
              <circle cx="50" cy="21" r="3" fill="#22c55e"/>
              <circle cx="13" cy="42" r="7" fill="#7c3aed" opacity=".8"/>
              <rect x="23" y="39" width="22" height="2.5" rx="1" fill="#cbd5e1" opacity=".7"/>
              <circle cx="13" cy="60" r="7" fill="#0f766e" opacity=".8"/>
              <rect x="23" y="57" width="24" height="2.5" rx="1" fill="#cbd5e1" opacity=".6"/>
              <circle cx="50" cy="57" r="4" fill="#ef4444"/>
              <text x="50" y="59" text-anchor="middle" fill="#fff" font-size="4.5" font-family="sans-serif" font-weight="bold">2</text>
              <rect x="57" y="0" width="163" height="14" fill="#031525"/>
              <circle cx="70" cy="7" r="5" fill="#1d4ed8" opacity=".9"/>
              <rect x="78" y="4" width="30" height="3" rx="1" fill="#e2e8f0" opacity=".8"/>
              <rect x="60" y="20" width="80" height="14" rx="4" fill="#0c2d45"/>
              <rect x="63" y="23" width="60" height="2.5" rx="1" fill="#cbd5e1" opacity=".8"/>
              <rect x="120" y="40" width="96" height="14" rx="4" fill="#1d4ed8"/>
              <rect x="123" y="43" width="70" height="2.5" rx="1" fill="#fff" opacity=".9"/>
              <rect x="60" y="58" width="96" height="14" rx="4" fill="#0c2d45"/>
              <rect x="63" y="61" width="60" height="2.5" rx="1" fill="#cbd5e1" opacity=".7"/>
              <rect x="150" y="76" width="66" height="10" rx="4" fill="#1d4ed8" opacity=".8"/>
              <rect x="60" y="88" width="36" height="12" rx="6" fill="#0c2d45"/>
              <circle cx="70" cy="94" r="2" fill="#64748b"/>
              <circle cx="78" cy="94" r="2" fill="#64748b" opacity=".7"/>
              <circle cx="86" cy="94" r="2" fill="#64748b" opacity=".5"/>
              <rect x="57" y="99" width="163" height="11" fill="#031525"/>
              <rect x="60" y="101" width="110" height="7" rx="3.5" fill="#0c2d45"/>
              <rect x="178" y="101" width="18" height="7" rx="3.5" fill="#0ea5e9"/>
            </svg>
          </div>
          <div class="project-info">
            <h4>Real-time Chat App</h4>
            <p>Messaging app with live updates & media sharing</p>
            <div class="tag-row">
              <span class="tag">React</span><span class="tag">Socket.io</span><span class="tag">Node.js</span>
            </div>
          </div>
        </div>

      </div>
    </section>

    <!-- ══ CONTACT ══ -->
    <section id="contact">
      <h2>Get In <span>Touch</span></h2>
      <p class="sub">Have a project in mind? Let's work together!</p>

      <div class="contact-form">
        <div class="form-row">
          <div class="form-group">
            <label>Your Name</label>
            <input type="text" id="f-name" placeholder="John Doe" />
          </div>
          <div class="form-group">
            <label>Email Address</label>
            <input type="email" id="f-email" placeholder="john@example.com" />
          </div>
        </div>
        <div class="form-group">
          <label>Subject</label>
          <input type="text" id="f-subject" placeholder="Project Collaboration" />
        </div>
        <div class="form-group">
          <label>Message</label>
          <textarea id="f-msg" rows="4" placeholder="Tell me about your project..."></textarea>
        </div>
        <button class="send-btn" onclick="sendMessage()">
          <svg width="15" height="15" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M12 19l9 2-9-18-9 18 9-2zm0 0v-8"/></svg>
          Send Message
        </button>
        <div class="toast" id="toast">
          <svg width="16" height="16" fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7"/></svg>
          Message sent! I'll get back to you soon.
        </div>
      </div>
    </section>

  </div><!-- /content -->
</div><!-- /shell -->

<!-- FAB scroll to top -->
<button class="fab" id="fab" onclick="window.scrollTo({top:0,behavior:'smooth'})">
  <svg fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M14.707 12.707a1 1 0 01-1.414 0L10 9.414l-3.293 3.293a1 1 0 01-1.414-1.414l4-4a1 1 0 011.414 0l4 4a1 1 0 010 1.414z" clip-rule="evenodd"/></svg>
</button>

<script>
/* ── Typing effect ── */
const roles = ['UI/UX Designer', 'Frontend Developer', 'Creative Coder', 'Vue Enthusiast'];
let ri = 0, ci = 0, deleting = false;
const el = document.getElementById('typed-text');
function type() {
  const word = roles[ri];
  el.textContent = deleting ? word.slice(0, ci--) : word.slice(0, ci++);
  if (!deleting && ci > word.length) { deleting = true; setTimeout(type, 1400); return; }
  if (deleting && ci < 0) { deleting = false; ri = (ri + 1) % roles.length; ci = 0; }
  setTimeout(type, deleting ? 50 : 90);
}
setTimeout(type, 1000);

/* ── Smooth scroll + sidebar active ── */
function scrollTo(id) {
  document.getElementById(id).scrollIntoView({ behavior: 'smooth', block: 'start' });
}

const sections = ['home','about','skills','portfolio','contact'];
const icons = document.querySelectorAll('.sidebar-icon');

const obs = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      const id = e.target.id;
      icons.forEach(i => i.classList.toggle('active', i.dataset.section === id));
      if (e.target.id === 'skills') animateBars();
    }
  });
}, { threshold: 0.4 });

sections.forEach(id => { const el = document.getElementById(id); if(el) obs.observe(el); });

/* ── FAB show/hide ── */
window.addEventListener('scroll', () => {
  document.getElementById('fab').classList.toggle('visible', window.scrollY > 300);
});

/* ── Skill bar animation ── */
let barsAnimated = false;
function animateBars() {
  if (barsAnimated) return;
  barsAnimated = true;
  document.querySelectorAll('.fill[data-width]').forEach(bar => {
    bar.style.width = bar.dataset.width + '%';
  });
}

/* ── Download CV ── */
function downloadCV() {
  event.preventDefault();
  const btn = document.getElementById('cv-btn');
  const orig = btn.innerHTML;
  btn.innerHTML = `<svg width="14" height="14" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7"/></svg> Downloaded!`;
  btn.style.borderColor = '#22d3ee';
  btn.style.color = '#22d3ee';

  // Generate a simple text CV and download it
  const cv = `KAY – UI/UX Designer & Frontend Developer
===========================================
Email   : kay@design.dev
Website : kay.dev
Location: Indonesia

ABOUT
-----
Passionate UI/UX Designer & Frontend Developer with 3+ years of experience
crafting modern, responsive web applications.

SKILLS
------
React     90%
Tailwind  85%
Python    80%
Vue       95%

PROJECTS
--------
• Modern E-Commerce Platform (React, Node.js, MongoDB, Tailwind)
• Task Management App (Vue.js, Firebase, CSS3)
• Weather Dashboard (React, API, Chart.js)
• Portfolio Website (Vue.js, GSAP, CSS3)
• Dark/Light Mode UI (React, Tailwind)
• Real-time Chat App (React, Socket.io, Node.js)
`;
  const blob = new Blob([cv], { type: 'text/plain' });
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'Kay_CV.txt';
  a.click();

  setTimeout(() => {
    btn.innerHTML = orig;
    btn.style.borderColor = '';
    btn.style.color = '';
  }, 2500);
}

/* ── Project modal ── */
const projects = [
  {
    title: 'Modern E-Commerce Platform',
    sub: 'React · Node.js · MongoDB · Tailwind',
    desc: 'A full-stack e-commerce solution featuring product listings, cart management, user authentication, order tracking, and a clean admin dashboard. Built with React for the frontend and Node.js + MongoDB for the backend.',
    tags: ['React', 'Node.js', 'MongoDB', 'Tailwind', 'REST API'],
    thumb: 0
  },
  {
    title: 'Task Management App',
    sub: 'Vue.js · Firebase · CSS3',
    desc: 'A Kanban-style productivity app with drag-and-drop columns, real-time sync via Firebase, progress bars, due dates, priority labels, and team collaboration features.',
    tags: ['Vue.js', 'Firebase', 'CSS3', 'Vuex', 'Drag & Drop'],
    thumb: 1
  },
  {
    title: 'Weather Dashboard',
    sub: 'React · OpenWeather API · Chart.js',
    desc: 'Real-time weather monitoring dashboard with 7-day forecasts, interactive bar charts, humidity/wind data, city search, and geolocation support.',
    tags: ['React', 'OpenWeather API', 'Chart.js', 'Geolocation'],
    thumb: 2
  },
  {
    title: 'Portfolio Website',
    sub: 'Vue.js · GSAP · CSS3',
    desc: 'A sleek, animated personal portfolio featuring scroll-triggered reveals, smooth page transitions via GSAP, dark theme, and a responsive layout showcasing projects and skills.',
    tags: ['Vue.js', 'GSAP', 'CSS3', 'Animations'],
    thumb: 3
  },
  {
    title: 'Dark / Light Mode UI',
    sub: 'React · Tailwind',
    desc: 'A comprehensive UI component library supporting seamless dark/light theme switching with persistent user preference via localStorage, smooth transitions, and a full component showcase.',
    tags: ['React', 'Tailwind', 'Context API', 'Accessibility'],
    thumb: 4
  },
  {
    title: 'Real-time Chat App',
    sub: 'React · Socket.io · Node.js',
    desc: 'A full-featured messaging app with real-time communication via WebSockets, typing indicators, online presence, media sharing, emoji support, and contact management.',
    tags: ['React', 'Socket.io', 'Node.js', 'WebSocket'],
    thumb: 5
  }
];

const thumbSVGs = [
  // reuse same SVGs as cards
];

function openModal(i) {
  const p = projects[i];
  document.getElementById('modal-title').textContent = p.title;
  document.getElementById('modal-sub').textContent = p.sub;
  document.getElementById('modal-desc').textContent = p.desc;
  const tagsEl = document.getElementById('modal-tags');
  tagsEl.innerHTML = p.tags.map(t => `<span class="modal-tag">${t}</span>`).join('');
  // clone thumb SVG from card
  const cards = document.querySelectorAll('.project-thumb');
  const clone = cards[i].cloneNode(true);
  clone.style.width = '100%';
  clone.style.height = '150px';
  document.getElementById('modal-thumb').innerHTML = clone.innerHTML;
  document.getElementById('modal').classList.add('open');
  document.body.style.overflow = 'hidden';
}

function closeModal() {
  document.getElementById('modal').classList.remove('open');
  document.body.style.overflow = '';
}

document.addEventListener('keydown', e => { if (e.key === 'Escape') closeModal(); });

/* ── Contact form ── */
function sendMessage() {
  const name = document.getElementById('f-name').value.trim();
  const email = document.getElementById('f-email').value.trim();
  const msg = document.getElementById('f-msg').value.trim();
  if (!name || !email || !msg) {
    alert('Please fill in your name, email, and message.');
    return;
  }
  const toast = document.getElementById('toast');
  toast.classList.add('show');
  document.getElementById('f-name').value = '';
  document.getElementById('f-email').value = '';
  document.getElementById('f-subject').value = '';
  document.getElementById('f-msg').value = '';
  setTimeout(() => toast.classList.remove('show'), 4000);
}
</script>
</body>
</html>
