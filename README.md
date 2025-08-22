<DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
<!  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Skyline Softworks</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">
  <style>
    :root { 
      --primary-grad: linear-gradient(90deg, #8A2BE2, #FF00FF);
      --primary-color: #C07DF4;
      --bg: #050505; 
      --card-bg: #111111;
      --text: #EAEAEA; 
      --text-muted: #A0A0A0;
      --border-color: rgba(255, 255, 255, 0.1);
    }
    body.light-mode {
      --bg: #f0f2f5;
      --card-bg: #ffffff;
      --text: #111827;
      --text-muted: #6B7280;
      --border-color: rgba(0, 0, 0, 0.1);
    }
    * { box-sizing: border-box; scroll-behavior: smooth; }
    body { 
      margin: 0; 
      padding-top: 70px; /* Nav bar ki height ke liye space */
      font-family: 'Poppins', sans-serif; 
      background:var(--bg); 
      color:var(--text); 
      transition: background-color 0.3s, color 0.3s;
    }
    a { color: inherit; text-decoration: none; }

    /* Navigation Bar */
    nav.top {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      padding: 15px 30px;
      background: rgba(5, 5, 5, 0.7);
      backdrop-filter: blur(10px);
      -webkit-backdrop-filter: blur(10px);
      border-bottom: 1px solid var(--border-color);
      display: flex;
      justify-content: space-between;
      align-items: center;
      z-index: 1000;
      transition: background-color 0.3s, border-color 0.3s;
    }
    body.light-mode nav.top {
        background: rgba(255, 255, 255, 0.7);
    }
    nav .logo {
      font-weight: 700;
      font-size: 1.4rem;
      background: var(--primary-grad);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }
    nav .nav-links {
      display: flex;
      gap: 25px;
      align-items: center;
    }
     nav .nav-links a {
      font-weight: 600;
      transition: color 0.3s ease;
    }
    nav .nav-links a:hover, nav .nav-links a.active {
      color: var(--primary-color);
    }
    /* Mobile Menu */
    .menu-toggle { display: none; cursor: pointer; }
    .menu-toggle div { width: 25px; height: 3px; background-color: var(--text); margin: 5px 0; transition: 0.4s; }
    body.light-mode .menu-toggle div { background-color: var(--text); }

    /* Header */
    header { position:relative; overflow:hidden; height: calc(100vh - 70px); }
    header video { 
      width:100%; height:100%; object-fit:cover; 
      position:absolute; inset:0; z-index:-1; 
      filter: brightness(0.4);
    }
    header .overlay { 
      display:flex; flex-direction:column; align-items:center; justify-content:center; 
      gap:18px; text-align:center; height:100%; 
      background:rgba(5, 5, 5, 0.3); 
      padding: 0 20px;
    }
    header h1 { 
      font-size: clamp(2.5rem, 10vw, 5rem); 
      margin:0;
      font-weight: 700;
      line-height: 1.2;
      background: var(--primary-grad);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      text-shadow: 0 0 25px rgba(255, 0, 255, 0.3);
    }
    header p { 
      font-size: clamp(1rem, 2.5vw, 1.3rem); 
      color: #EAEAEA; margin:0; max-width: 600px;
    }
    .cta-wrap { margin-top: 20px; display:flex; gap:14px; flex-wrap:wrap; justify-content:center; }
    .btn { 
      display:inline-block; padding:12px 28px; border-radius:8px; 
      color: var(--text); 
      font-weight:600;
      transition: all .3s ease;
      border: 2px solid var(--text);
      cursor: pointer;
    }
    .btn.primary {
      background: var(--primary-grad);
      color: white;
      border: none;
      padding: 14px 30px;
    }
    .btn:hover { 
      transform: translateY(-4px); 
      box-shadow:0 0 20px rgba(255, 0, 255, 0.4); 
    }

    /* Sections */
    section.page { 
      padding: 100px 20px; 
      max-width:1200px; 
      margin:auto; 
      min-height: 60vh;
      border-bottom: 1px solid var(--border-color);
    }
    section.page:last-of-type { border-bottom: none; }

    h2 { 
      text-align:center; margin:0 0 50px; 
      font-size: clamp(2.2rem, 5vw, 3rem); 
      color: var(--text);
      font-weight: 700;
    }
    h2 span { 
      background: var(--primary-grad);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }

    /* Cards */
    .grid { display:grid; grid-template-columns:repeat(auto-fit, minmax(280px, 1fr)); gap:28px; }
    .card { 
      background: var(--card-bg);
      border-radius:12px; padding:28px; 
      border: 1px solid var(--border-color);
      transition: all .3s ease; 
    }
    .card:hover { 
      transform: translateY(-10px); 
      box-shadow:0 10px 30px rgba(0,0,0,0.5);
      border-color: var(--primary-color);
    }
    .card h3 { color:var(--primary-color); margin:0 0 10px; font-weight: 600; font-size: 1.4rem; }
    .card p { color: var(--text-muted); margin:0; line-height: 1.6; }
    .card .more { display:block; margin-top:20px; font-weight:600; color:var(--primary-color); }

    /* Common Elements */
    .thumb { width:100%; height: 200px; object-fit: cover; border-radius:10px; display:block; margin-bottom:16px; }
    .video { position:relative; padding-top:56.25%; border-radius:12px; overflow:hidden; background: #000; }
    .video iframe, .video video { position:absolute; inset:0; width:100%; height:100%; border:0; object-fit: cover;}
    
    /* Stats Counter */
    .stats-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
        gap: 30px;
        text-align: center;
    }
    .stat-item .stat-number {
        font-size: 3rem;
        font-weight: 700;
        background: var(--primary-grad);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
    }
    .stat-item .stat-label {
        font-size: 1.1rem;
        color: var(--text-muted);
    }
    
    /* Client Logos */
    .clients-grid {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;
        gap: 40px;
    }
    .client-logo {
        height: 50px;
        opacity: 0.7;
        transition: opacity 0.3s ease;
        filter: grayscale(1) brightness(1.5);
    }
    .client-logo:hover {
        opacity: 1;
        filter: grayscale(0) brightness(1);
    }
    body.light-mode .client-logo {
        filter: grayscale(1) brightness(0.5);
    }
    body.light-mode .client-logo:hover {
        filter: grayscale(0) brightness(1);
    }


    /* Testimonials */
    .testimonial-card { text-align: center; }
    .testimonial-card p { font-style: italic; font-size: 1.1rem; }
    .testimonial-card .author { margin-top: 20px; font-weight: 700; color: var(--primary-color); }

    /* Process Timeline */
    .timeline {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      position: relative;
      margin-top: 40px;
    }
    .timeline::before {
      content: '';
      position: absolute;
      top: 25px;
      left: 10%;
      right: 10%;
      height: 2px;
      background: var(--border-color);
    }
    .timeline-item {
      flex: 1;
      min-width: 200px;
      max-width: 250px;
      text-align: center;
      position: relative;
      padding: 0 20px;
    }
    .timeline-icon {
      width: 50px;
      height: 50px;
      background: var(--bg);
      border: 2px solid var(--primary-color);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0 auto 20px;
      font-size: 1.5rem;
      color: var(--primary-color);
      box-shadow: 0 0 15px rgba(192, 125, 244, 0.5);
    }
    .timeline-item h4 {
      font-size: 1.2rem;
      margin-bottom: 10px;
      color: var(--text);
    }
    .timeline-item p {
      font-size: 0.9rem;
      color: var(--text-muted);
    }
    
    /* Technology Showcase */
    .tech-grid {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
        gap: 25px;
        max-width: 800px;
        margin: auto;
    }
    .tech-item {
        background: var(--card-bg);
        border: 1px solid var(--border-color);
        border-radius: 12px;
        padding: 20px;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        transition: all 0.3s ease;
    }
    .tech-item:hover {
        transform: translateY(-5px);
        border-color: var(--primary-color);
    }
    .tech-item svg {
        width: 48px;
        height: 48px;
        fill: var(--text);
    }
    .tech-item p {
        margin: 10px 0 0;
        font-weight: 600;
    }

    /* Team Section */
    .team-member { text-align: center; }
    .team-member img {
        width: 150px;
        height: 150px;
        border-radius: 50%;
        object-fit: cover;
        border: 3px solid var(--primary-color);
        margin-bottom: 15px;
    }
    .team-member h4 {
        font-size: 1.3rem;
        margin: 10px 0 5px;
        color: var(--text);
    }
    .team-member p {
        color: var(--primary-color);
        font-weight: 600;
        margin: 0;
    }


    /* FAQ Accordion */
    .faq-item {
      background: var(--card-bg);
      border: 1px solid var(--border-color);
      border-radius: 8px;
      margin-bottom: 15px;
      overflow: hidden;
    }
    .faq-question {
      padding: 20px;
      font-weight: 600;
      cursor: pointer;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .faq-question::after {
      content: '+';
      font-size: 1.5rem;
      transition: transform 0.3s ease;
    }
    .faq-item.active .faq-question::after {
      transform: rotate(45deg);
    }
    .faq-answer {
      max-height: 0;
      overflow: hidden;
      transition: max-height 0.3s ease, padding 0.3s ease;
      padding: 0 20px;
      color: var(--text-muted);
      line-height: 1.7;
    }
    .faq-item.active .faq-answer {
      max-height: 200px; /* Adjust as needed */
      padding: 0 20px 20px;
    }
    
    /* Modals */
    .modal {
        display: none; position: fixed; z-index: 1001; left: 0; top: 0;
        width: 100%; height: 100%; overflow: auto;
        background-color: rgba(0,0,0,0.8); backdrop-filter: blur(5px);
        align-items: center; justify-content: center;
    }
    .modal-content {
        background: var(--card-bg); margin: auto; padding: 30px;
        border: 1px solid var(--border-color); width: 90%; max-width: 700px;
        border-radius: 12px; position: relative;
    }
    .close-btn {
        color: #aaa; float: right; font-size: 28px; font-weight: bold;
        position: absolute; top: 10px; right: 20px;
    }
    .close-btn:hover, .close-btn:focus { color: white; text-decoration: none; cursor: pointer; }
    #modal-tags span { background: #333; padding: 5px 10px; border-radius: 5px; margin-right: 10px; font-size: 0.9rem;}


    /* Gemini Features */
    .gemini-feature .card { padding: 32px; }
    .gemini-feature label { display:block; margin:12px 0 8px; color: var(--text-muted); }
    .gemini-feature input, .gemini-feature textarea, .gemini-feature select { width:100%; padding:14px; border-radius:8px; border:1px solid var(--border-color); background:#050505; color:#eee; font-family: 'Poppins', sans-serif; font-size: 1rem; }
    body.light-mode .gemini-feature input, body.light-mode .gemini-feature textarea, body.light-mode .gemini-feature select { background: #e9ecef; color: #333; }
    .gemini-feature input:focus, .gemini-feature textarea:focus, .gemini-feature select:focus { border-color: var(--primary-color); outline: none; }
    #ad-copy-result, #idea-result, #branding-result, #cost-result { margin-top: 24px; padding: 20px; border-radius: 12px; background: #050505; min-height: 50px; white-space: pre-wrap; line-height: 1.7; border: 1px solid var(--border-color); }
    body.light-mode #ad-copy-result, body.light-mode #idea-result, body.light-mode #branding-result, body.light-mode #cost-result { background: #e9ecef; }
    #ad-copy-loading, #idea-loading, #branding-loading, #cost-loading { text-align: center; padding: 20px; display: none; }
    
    /* Live Chat Feature */
    .chat-fab {
        position: fixed;
        bottom: 30px;
        right: 30px;
        width: 60px;
        height: 60px;
        background: var(--primary-grad);
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        box-shadow: 0 5px 20px rgba(255, 0, 255, 0.4);
        z-index: 998;
        transition: transform 0.3s ease;
    }
    .chat-fab:hover { transform: scale(1.1); }
    .chat-fab svg { width: 32px; height: 32px; fill: white; }

    .chat-window {
        position: fixed;
        bottom: 100px;
        right: 30px;
        width: 90%;
        max-width: 370px;
        height: 500px;
        background: var(--card-bg);
        border: 1px solid var(--border-color);
        border-radius: 12px;
        overflow: hidden;
        display: flex;
        flex-direction: column;
        z-index: 999;
        transform: scale(0.5) translateY(100px);
        opacity: 0;
        pointer-events: none;
        transition: all 0.3s ease;
    }
    .chat-window.open {
        transform: scale(1) translateY(0);
        opacity: 1;
        pointer-events: auto;
    }
    .chat-header {
        padding: 15px;
        background: linear-gradient(90deg, #1a1a1a, #222);
        border-bottom: 1px solid var(--border-color);
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    .chat-header h4 { margin: 0; }
    .chat-header .close-chat { cursor: pointer; font-size: 1.5rem; }
    .chat-body { flex-grow: 1; padding: 15px; overflow-y: auto; }
    .chat-message { margin-bottom: 15px; display: flex; }
    .chat-message p { padding: 10px 15px; border-radius: 18px; max-width: 80%; line-height: 1.5; }
    .user-message { justify-content: flex-end; }
    .user-message p { background: var(--primary-color); color: var(--bg); border-bottom-right-radius: 4px; }
    .bot-message { justify-content: flex-start; }
    .bot-message p { background: #333; color: var(--text); border-bottom-left-radius: 4px; }
    .chat-footer { padding: 10px; border-top: 1px solid var(--border-color); }
    #chat-form { display: flex; gap: 10px; }
    #chat-input { flex-grow: 1; background: #050505; border: 1px solid var(--border-color); border-radius: 8px; padding: 10px; color: var(--text); }
    #chat-send { background: var(--primary-color); border: none; border-radius: 8px; color: var(--bg); padding: 0 15px; font-weight: 600; cursor: pointer; }


    /* Footer */
    footer { background: #000; color: var(--text-muted); padding: 50px 20px 20px; border-top: 1px solid var(--border-color); }
    .footer-grid { max-width: 1200px; margin: 0 auto 30px; display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 30px; text-align: left; }
    footer h3 { color: var(--text); margin: 0 0 15px; font-weight: 600; }
    footer p, footer ul { margin: 0; padding: 0; list-style: none; }
    footer li { margin-bottom: 10px; }
    footer a:hover { color: var(--primary-color); }
    .copyright { text-align: center; border-top: 1px solid #333; padding-top: 20px; margin-top: 30px; font-size: 0.9rem; }
    
    /* Scroll Animations */
    .reveal {
        opacity: 0;
        transform: translateY(30px);
        transition: opacity 0.6s ease-out, transform 0.6s ease-out;
    }
    .reveal.visible {
        opacity: 1;
        transform: translateY(0);
    }

    /* Responsive Styles */
    @media (max-width: 850px) {
      nav .nav-links {
        display: none;
        flex-direction: column;
        align-items: center;
        position: absolute;
        top: 70px;
        left: 0;
        width: 100%;
        background: rgba(5, 5, 5, 0.95);
        padding: 20px 0;
      }
      nav .nav-links.active {
        display: flex;
      }
      .menu-toggle {
        display: block;
      }
    }
  </style>
</head>
<body>

<nav class="top">
  <a href="#home" class="logo">Skyline Softworks</a>
  <div class="nav-links">
    <a href="#services">Services</a>
    <a href="#process">Process</a>
    <a href="#tech">Technologies</a>
    <a href="#portfolio">Portfolio</a>
    <a href="#team">Team</a>
    <a href="#testimonials">Testimonials</a>
    <a href="#pricing">Pricing</a>
    <a href="#faq">FAQ</a>
    <a href="#contact">Contact</a>
  </div>
   <div class="menu-toggle" id="menu-toggle">
    <div></div>
    <div></div>
    <div></div>
  </div>
</nav>

<!-- Home Section -->
<header id="home">
  <video autoplay muted loop playsinline poster="https://placehold.co/1920x1080/050505/C07DF4?text=Loading...">
    <source src="https://cdn.coverr.co/videos/coverr-purple-and-pink-ink-in-motion-5693/1080p.mp4" type="video/mp4" />
  </video>
  <div class="overlay">
    <h1>Skyline Softworks</h1>
    <p>Naye Web, App aur Creative Editing Solutions jo aapke business ko aage badhaye.</p>
    <div class="cta-wrap">
      <a class="btn primary" href="#services">Hamari Services Dekhein</a>
      <a class="btn" href="https://wa.me/917726870877" target="_blank">WhatsApp Now</a>
    </div>
  </div>
</header>

<main>
  <!-- Services Section -->
  <section id="services" class="page">
    <h2 class="reveal">Hamari <span>Services</span></h2>
    <div class="grid">
      <div class="card reveal">
        <h3>Web Development</h3>
        <p>Modern, responsive websites aur online stores jo premium UI/UX ke saath aate hain.</p>
      </div>
      <div class="card reveal">
        <h3>App Development</h3>
        <p>Android & iOS apps. Tez, scalable, aur user-friendly design.</p>
      </div>
      <div class="card reveal">
        <h3>Creative Editing</h3>
        <p>Branding, posters, banners, aur ad creatives jo results dete hain.</p>
      </div>
    </div>
  </section>

  <!-- Process Section -->
  <section id="process" class="page">
      <h2 class="reveal">Hum Kaise Kaam <span>Karte Hain</span></h2>
      <div class="timeline">
          <div class="timeline-item reveal">
              <div class="timeline-icon">1</div>
              <h4>Requirement</h4>
              <p>Hum aapse aapke project ki saari zarooratein samajhte hain.</p>
          </div>
          <div class="timeline-item reveal">
              <div class="timeline-icon">2</div>
              <h4>Design</h4>
              <p>Aapke idea ke anusaar ek modern aur user-friendly design taiyar karte hain.</p>
          </div>
          <div class="timeline-item reveal">
              <div class="timeline-icon">3</div>
              <h4>Development</h4>
              <p>Clean aur efficient code likhkar aapke project ko banate hain.</p>
          </div>
          <div class="timeline-item reveal">
              <div class="timeline-icon">4</div>
              <h4>Launch & Support</h4>
              <p>Project ko live karke 3 mahine ka free support dete hain.</p>
          </div>
      </div>
  </section>
  
  <!-- Technology Section -->
  <section id="tech" class="page">
      <h2 class="reveal">Technology We <span>Use</span></h2>
      <div class="tech-grid">
          <div class="tech-item reveal" data-tech="React">
              <svg viewBox="0 0 24 24"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm0 18c-4.41 0-8-3.59-8-8s3.59-8 8-8 8 3.59 8 8-3.59 8-8 8zm-1-13h2v2h-2zm0 4h2v6h-2z"/></svg>
              <p>React</p>
          </div>
          <div class="tech-item reveal" data-tech="Node.js">
              <svg viewBox="0 0 24 24"><path d="M9 3h6v2H9zM4 11h16v2H4zm5 8h6v2H9z"/></svg>
              <p>Node.js</p>
          </div>
          <div class="tech-item reveal" data-tech="Python">
              <svg viewBox="0 0 24 24"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-1 15v-2h2v2zm0-4v-6h2v6z"/></svg>
              <p>Python</p>
          </div>
          <div class="tech-item reveal" data-tech="Firebase">
              <svg viewBox="0 0 24 24"><path d="M6.78 4.31 4.53 5.25l7.47 13.5 2.25-.94zM5 15.47V9.53l-3.37 1.4L5 15.47zm13.37-9.53L15 4.53v5.94l3.37-1.4z"/></svg>
              <p>Firebase</p>
          </div>
          <div class="tech-item reveal" data-tech="Figma">
             <svg viewBox="0 0 24 24"><path d="M12 2a10 10 0 1 0 0 20 10 10 0 0 0 0-20zm0 18a8 8 0 1 1 0-16 8 8 0 0 1 0 16zm-1-5h2v2h-2zm0-6h2v4h-2z"/></svg>
             <p>Figma</p>
          </div>
          <div class="tech-item reveal" data-tech="Photoshop">
              <svg viewBox="0 0 24 24"><path d="M21 4H3c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h18c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm-2 14H5V6h14v12zM8 11h8v2H8z"/></svg>
              <p>Photoshop</p>
          </div>
      </div>
  </section>

  <!-- Portfolio Section -->
  <section id="portfolio" class="page">
    <h2 class="reveal">Featured <span>Projects</span></h2>
    <div class="grid">
      <div class="card reveal">
        <img class="thumb" src="https://images.unsplash.com/photo-1517694712202-14dd9538aa97?q=80&w=2070&auto=format&fit=crop" alt="Corporate Website" />
        <h3>Corporate Website</h3>
        <p>Ek shaandar, responsive site CMS aur SEO setup ke saath.</p>
        <button class="btn more case-study-btn" data-project="corp">Case Study</button>
      </div>
      <div class="card reveal">
        <img class="thumb" src="https://images.unsplash.com/photo-1551650975-87deedd944c3?q=80&w=1974&auto=format&fit=crop" alt="Finance App" />
        <h3>Finance App</h3>
        <p>Clean UI, analytics aur secure authentication startups ke liye.</p>
        <button class="btn more case-study-btn" data-project="finance">Case Study</button>
      </div>
      <div class="card reveal">
        <img class="thumb" src="https://images.unsplash.com/photo-1557862921-37829c790f19?q=80&w=2071&auto=format&fit=crop" alt="Branding Campaign" />
        <h3>Branding Campaign</h3>
        <p>Posters & video ads jisse 3x se zyada engagement mila.</p>
        <button class="btn more case-study-btn" data-project="branding">Case Study</button>
      </div>
    </div>
  </section>

  <!-- Team Section -->
  <section id="team" class="page">
      <h2 class="reveal">Meet Our <span>Team</span></h2>
      <div class="grid">
          <div class="card team-member reveal">
              <img src="https://placehold.co/150x150/111827/FBBF24?text=HV" alt="Team Member 1">
              <h4>Hemant Verma</h4>
              <p>Founder & CEO</p>
          </div>
          <div class="card team-member reveal">
              <img src="https://placehold.co/150x150/111827/EAEAEA?text=AV" alt="Team Member 2">
              <h4>Aarav Sharma</h4>
              <p>Lead Developer</p>
          </div>
          <div class="card team-member reveal">
              <img src="https://placehold.co/150x150/111827/EAEAEA?text=IS" alt="Team Member 3">
              <h4>Isha Singh</h4>
              <p>UI/UX Designer</p>
          </div>
      </div>
  </section>

  <!-- Testimonials Section -->
  <section id="testimonials" class="page">
    <h2 class="reveal">Hamare Clients <span>Kya Kehte Hain</span></h2>
    <div class="grid">
        <div class="card testimonial-card reveal">
            <p>"Skyline Softworks ne hamare vision ko ek behtareen website mein badal diya. Unka kaam professional aur time par tha. Highly recommended!"</p>
            <div class="author">- Priya Sharma, CEO of InnovateTech</div>
        </div>
        <div class="card testimonial-card reveal">
            <p>"Hamari mobile app unhone itni user-friendly banayi ki hamare user engagement double ho gaye. Unki team bahut supportive hai."</p>
            <div class="author">- Rahul Verma, Founder of ConnectApp</div>
        </div>
        <div class="card testimonial-card reveal">
            <p>"Creative editing ke liye inse behtar koi nahi. Hamare social media campaigns ko ek nayi pehchaan mili hai. Thank you, Skyline!"</p>
            <div class="author">- Anjali Mehta, Marketing Head</div>
        </div>
    </div>
  </section>

  <!-- Pricing Section -->
  <section id="pricing" class="page">
      <h2 class="reveal">Pricing & <span>Plans</span></h2>
      <p style="text-align:center; max-width: 600px; margin: -30px auto 50px; color: var(--text-muted);">Simple, transparent pricing. Custom quotes ke liye WhatsApp karein.</p>
      <div class="grid">
        <div class="plan card reveal">
          <h3>Landing Page</h3>
          <div class="price" style="font-size: 2.5rem;">₹9,999</div>
          <ul>
            <li>1 page modern design</li>
            <li>Responsive aur fast loading</li>
            <li>WhatsApp CTA setup</li>
          </ul>
          <a class="btn primary" href="https://wa.me/917726870877" target="_blank">Starter Plan Lein</a>
        </div>
        <div class="plan card reveal" style="border-color: var(--primary-color);">
          <span class="badge" style="background: var(--primary-grad); color: white;">Best Value</span>
          <h3>Business Website</h3>
          <div class="price" style="font-size: 2.5rem;">₹24,999</div>
          <ul>
            <li>5–7 pages + CMS</li>
            <li>On-page SEO</li>
            <li>Basic branding kit</li>
          </ul>
          <a class="btn primary" href="https://wa.me/917726870877" target="_blank">Business Plan Lein</a>
        </div>
        <div class="plan card reveal">
          <h3>E‑commerce / App</h3>
          <div class="price" style="font-size: 2.5rem;">Custom</div>
          <ul>
            <li>Payments, auth, analytics</li>
            <li>API & cloud deployment</li>
            <li>3 mahine ka support</li>
          </ul>
          <a class="btn primary" href="https://wa.me/917726870877" target="_blank">Custom Quote Lein</a>
        </div>
      </div>
  </section>
  
  <!-- FAQ Section -->
  <section id="faq" class="page">
    <h2 class="reveal">Aksar Puche Jane Wale <span>Sawal</span></h2>
    <div class="faq-container reveal" style="max-width: 800px; margin: auto;">
        <div class="faq-item">
            <div class="faq-question">Ek website banane mein kitna time lagta hai?</div>
            <div class="faq-answer"><p>Ek basic website 1-2 hafte mein taiyar ho jaati hai. Agar website badi hai ya usmein custom features hain, to usmein 4-6 hafte ya usse zyada bhi lag sakte hain.</p></div>
        </div>
        <div class="faq-item">
            <div class="faq-question">Kya aap website banane ke baad support dete hain?</div>
            <div class="faq-answer"><p>Haan, hum 3 mahine ka free technical support dete hain. Iske baad aap hamara annual maintenance plan bhi le sakte hain.</p></div>
        </div>
        <div class="faq-item">
            <div class="faq-question">Aapka payment process kya hai?</div>
            <div class="faq-answer"><p>Hum project shuru hone par 50% advance lete hain aur baaki 50% project complete hokar aapke paas live hone ke baad.</p></div>
        </div>
        <div class="faq-item">
            <div class="faq-question">Kya aap SEO services bhi dete hain?</div>
            <div class="faq-answer"><p>Haan, hum on-page SEO services dete hain jisse aapki website Google par behtar rank kar sake.</p></div>
        </div>
    </div>
  </section>

  <!-- About Section -->
  <section id="about" class="page">
    <h2 class="reveal">Hamari <span>Kahani</span></h2>
    <div class="grid">
      <div class="card reveal"><h3>Hum Kaun Hain</h3><p>Hum developers, designers, aur editors ka ek on-demand network hain jo tezi se high-quality kaam deliver karte hain.</p></div>
      <div class="card reveal"><h3>Hum Kya Karte Hain</h3><p>Websites, mobile apps, creative editing, brand kits, aur conversion-focused landing pages.</p></div>
      <div class="card reveal"><h3>Founder</h3><p>Skyline Softworks was founded by Hemant Verma with a passion for creating beautiful and functional digital experiences.</p></div>
    </div>
  </section>

  <!-- Contact Section -->
  <section id="contact" class="page">
    <h2 class="reveal">Humse <span>Sampark Karein</span></h2>
    <div class="gemini-feature reveal" style="margin-bottom: 60px;">
        <div class="card">
            <h3 style="text-align: center; font-size: 1.8rem;">AI Project Idea <span>Generator</span></h3>
            <p style="text-align: center; color: var(--text-muted); margin-top: -5px; margin-bottom: 25px;">Aapke paas ek idea hai? Use ek poore brief mein badlein.</p>
            <div>
                <label for="idea-input">Apna idea yahan likhein (kam se kam 10 shabdon mein)</label>
                <textarea id="idea-input" rows="3" placeholder="Jaise: 'Ek aisi mobile app jo aas paas ke street food vendors ko list kare aur real-time reviews de'"></textarea>
            </div>
            <button id="generate-idea-btn" class="btn primary">Generate Project Brief</button>
            <div id="idea-loading">Generating...</div>
            <div id="idea-result"></div>
        </div>
    </div>
    <div class="grid">
      <div class="card reveal">
        <h3>Message <span>Bhejein</span></h3>
        <form onsubmit="event.preventDefault(); alert('Thanks! Hum jald hi WhatsApp par reply karenge.');">
          <label for="name">Naam</label>
          <input id="name" required placeholder="Aapka Naam" />
          <label for="email">Email</label>
          <input id="email" type="email" required placeholder="name@email.com" />
          <label for="message">Message</label>
          <textarea id="message" rows="5" required placeholder="Aapne project ke baare mein batayein..."></textarea>
          <button class="btn primary" type="submit">Bhejein</button>
        </form>
      </div>
      <div class="card reveal">
        <h3>Intro <span>Video</span></h3>
        <div class="video">
           <video autoplay muted loop playsinline>
              <source src="https://cdn.coverr.co/videos/coverr-a-futuristic-hud-display-5732/1080p.mp4" type="video/mp4">
          </video>
        </div>
      </div>
    </div>
  </section>
</main>

<footer>
  <div class="footer-grid">
    <div>
      <h3>Skyline Softworks</h3>
      <p>Naye Web, App aur Creative Editing Solutions.</p>
      <p><strong>Founded by:</strong> Hemant Verma</p>
      <p><strong>Contact:</strong> +91 7726870877</p>
    </div>
    <div>
      <h3>Quick Links</h3>
      <ul>
        <li><a href="#home">Home</a></li>
        <li><a href="#about">Humare Baare Mein</a></li>
        <li><a href="#portfolio">Portfolio</a></li>
        <li><a href="#pricing">Pricing</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </div>
    <div class="reveal">
      <h3>Newsletter</h3>
      <p>Hamare latest projects aur offers ke liye subscribe karein.</p>
      <form onsubmit="event.preventDefault(); alert('Thank you for subscribing!'); this.reset();" style="margin-top: 15px; display: flex;">
          <input type="email" placeholder="Aapka email" required style="flex-grow: 1; border-radius: 8px 0 0 8px; border: 1px solid var(--border-color); background: var(--card-bg); padding: 10px;">
          <button type="submit" style="border: none; background: var(--primary-grad); color: white; padding: 0 15px; border-radius: 0 8px 8px 0; cursor: pointer; font-weight: 600;">Subscribe</button>
      </form>
    </div>
  </div>
  <div class="copyright">
    <p>© 2025 Skyline Softworks | All Rights Reserved</p>
  </div>
</footer>

<!-- Portfolio & Tech Modal -->
<div id="portfolio-modal" class="modal">
  <div class="modal-content">
    <span class="close-btn">&times;</span>
    <h2 id="modal-title" style="text-align: left; margin-bottom: 20px;"><span>Project</span> Details</h2>
    <p id="modal-description"></p>
    <h3 style="margin-top: 20px;" id="modal-tags-title">Technology Stack</h3>
    <div id="modal-tags"></div>
  </div>
</div>

<!-- Live Chat Feature -->
<div class="chat-fab" id="chat-fab">
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M20 2H4c-1.1 0-2 .9-2 2v18l4-4h14c1.1 0 2-.9 2-2V4c0-1.1-.9-2-2-2z"></path></svg>
</div>
<div class="chat-window" id="chat-window">
    <div class="chat-header">
        <h4>Humse Chat Karein</h4>
        <span class="close-chat" id="close-chat">&times;</span>
    </div>
    <div class="chat-body" id="chat-body">
        <div class="chat-message bot-message"><p>Hello! Main Skyline AI assistant hoon. Aapki kaise madad kar sakta hoon?</p></div>
    </div>
    <div class="chat-footer">
        <form id="chat-form">
            <input type="text" id="chat-input" placeholder="Message likhein..." autocomplete="off">
            <button type="submit" id="chat-send">Send</button>
        </form>
    </div>
</div>


<script>
  // --- Universal API Call Function ---
  const GEMINI_API_KEY = ""; // Leave this empty
  async function callGeminiWithBackoff(prompt, maxRetries = 3) {
    let delay = 1000;
    for (let i = 0; i < maxRetries; i++) {
      try {
        const payload = { contents: [{ role: "user", parts: [{ text: prompt }] }] };
        const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${GEMINI_API_KEY}`;
        
        const response = await fetch(apiUrl, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(payload)
        });

        if (!response.ok) {
          if (response.status !== 429) throw new Error(`HTTP error! status: ${response.status}`);
        } else {
          const result = await response.json();
          if (result.candidates && result.candidates[0]?.content?.parts?.[0]?.text) {
            return result.candidates[0].content.parts[0].text;
          } else {
            throw new Error("Invalid response structure from API.");
          }
        }
      } catch (error) {
         if (i === maxRetries - 1) throw error;
      }
      await new Promise(resolve => setTimeout(resolve, delay));
      delay *= 2;
    }
    throw new Error("API request failed after multiple retries.");
  }

  // Mobile Menu Toggle
  const menuToggle = document.getElementById('menu-toggle');
  const navLinks = document.querySelector('.nav-links');
  menuToggle.addEventListener('click', () => navLinks.classList.toggle('active'));
  document.querySelectorAll('.nav-links a').forEach(link => {
    link.addEventListener('click', () => {
      if (navLinks.classList.contains('active')) {
        navLinks.classList.remove('active');
      }
    });
  });

  // FAQ Accordion
  document.querySelectorAll('.faq-item').forEach(item => {
    item.querySelector('.faq-question').addEventListener('click', () => {
      const currentlyActive = document.querySelector('.faq-item.active');
      if (currentlyActive && currentlyActive !== item) {
        currentlyActive.classList.remove('active');
      }
      item.classList.toggle('active');
    });
  });

  // Portfolio & Tech Modal Logic
  const modal = document.getElementById('portfolio-modal');
  const modalTitle = document.getElementById('modal-title');
  const modalDesc = document.getElementById('modal-description');
  const modalTags = document.getElementById('modal-tags');
  const modalTagsTitle = document.getElementById('modal-tags-title');
  const closeBtn = document.querySelector('.close-btn');

  const caseStudies = {
    corp: { title: "Corporate Website", description: "Humne InnovateTech ke liye ek professional aur modern corporate website banayi...", tags: ["HTML5", "CSS3", "JavaScript", "PHP", "MySQL"] },
    finance: { title: "Finance App", description: "ConnectApp ke liye humne ek cross-platform mobile application banayi...", tags: ["React Native", "Firebase", "Chart.js"] },
    branding: { title: "Branding Campaign", description: "Ek naye fashion brand ke liye humne ek complete digital branding campaign design kiya...", tags: ["Photoshop", "Illustrator", "After Effects"] }
  };

  document.querySelectorAll('.case-study-btn').forEach(button => {
    button.addEventListener('click', () => {
      const projectKey = button.dataset.project;
      const projectData = caseStudies[projectKey];
      
      modalTitle.querySelector('span').textContent = projectData.title;
      modalDesc.textContent = projectData.description;
      modalTagsTitle.style.display = 'block';
      modalTags.innerHTML = '';
      projectData.tags.forEach(tag => {
        const tagElement = document.createElement('span');
        tagElement.textContent = tag;
        modalTags.appendChild(tagElement);
      });
      
      modal.style.display = 'flex';
    });
  });
  
  document.querySelectorAll('.tech-item').forEach(item => {
      item.addEventListener('click', async () => {
          const techName = item.dataset.tech;
          modalTitle.querySelector('span').textContent = techName;
          modalDesc.textContent = 'Loading...';
          modalTagsTitle.style.display = 'none';
          modalTags.innerHTML = '';
          modal.style.display = 'flex';

          const prompt = `Explain what ${techName} is in simple terms for a business owner in Hindi (Latin script). Keep it short and easy to understand (2-3 sentences).`;
          try {
              const responseText = await callGeminiWithBackoff(prompt);
              modalDesc.textContent = responseText;
          } catch (error) {
              modalDesc.textContent = 'Sorry, abhi jaankari nahi mil pa rahi hai.';
              console.error("Tech explain error:", error);
          }
      });
  });

  closeBtn.onclick = () => { modal.style.display = "none"; }
  window.onclick = (event) => {
    if (event.target == modal) {
      modal.style.display = "none";
    }
  }

  // Live Chat Logic
  const chatFab = document.getElementById('chat-fab');
  const chatWindow = document.getElementById('chat-window');
  const closeChat = document.getElementById('close-chat');
  const chatForm = document.getElementById('chat-form');
  const chatInput = document.getElementById('chat-input');
  const chatBody = document.getElementById('chat-body');
  let chatHistory = [];

  chatFab.addEventListener('click', () => chatWindow.classList.toggle('open'));
  closeChat.addEventListener('click', () => chatWindow.classList.remove('open'));

  chatForm.addEventListener('submit', async (e) => {
    e.preventDefault();
    const userMessage = chatInput.value.trim();
    if (!userMessage) return;

    appendMessage(userMessage, 'user');
    chatInput.value = '';
    chatHistory.push({role: "user", parts: [{text: userMessage}]});

    const prompt = `You are a helpful and friendly AI assistant for Skyline Softworks, a company founded by Hemant Verma that provides web development, app development, and creative editing services. Your name is Skyline AI. Keep your answers short, conversational, and in Hindi (Latin script). Current conversation history is: ${JSON.stringify(chatHistory)}`;

    try {
        const responseText = await callGeminiWithBackoff(prompt);
        appendMessage(responseText, 'bot');
        chatHistory.push({role: "model", parts: [{text: responseText}]});
    } catch (error) {
        console.error('Chatbot error:', error);
        appendMessage('Sorry, kuch takniki samasya aa gayi hai. Aap humein direct WhatsApp kar sakte hain.', 'bot');
    }
  });

  function appendMessage(text, type) {
      const messageContainer = document.createElement('div');
      messageContainer.classList.add('chat-message', `${type}-message`);
      const messageBubble = document.createElement('p');
      messageBubble.textContent = text;
      messageContainer.appendChild(messageBubble);
      chatBody.appendChild(messageContainer);
      chatBody.scrollTop = chatBody.scrollHeight;
  }

  // --- Gemini API Call Logic for Project Idea Generator ---
  const generateIdeaBtn = document.getElementById('generate-idea-btn');
  const ideaInput = document.getElementById('idea-input');
  const ideaResultDiv = document.getElementById('idea-result');
  const ideaLoadingDiv = document.getElementById('idea-loading');

  function formatResponse(text) {
      let html = text;
      html = html.replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>');
      html = html.replace(/^\s*\*\s*(.*)/gm, '<li>$1</li>');
      html = html.replace(/(<li>.*<\/li>)/s, '<ul>$1</ul>');
      html = html.replace(/^###\s*(.*)/gm, '<h3>$1</h3>');
      return html;
  }

  generateIdeaBtn.addEventListener('click', async () => {
    const idea = ideaInput.value.trim();
    if (idea.length < 10) {
      ideaResultDiv.textContent = 'Kripya apna idea kam se kam 10 shabdon mein likhein.';
      return;
    }

    ideaLoadingDiv.style.display = 'block';
    ideaResultDiv.innerHTML = '';
    generateIdeaBtn.disabled = true;

    const prompt = `Ek user ke app/website idea ke liye ek project brief generate karein. User ka idea hai: "${idea}".
    
    Brief mein yeh cheezein shaamil honi chahiye:
    ### Project ka Naam
    Ek catchy aur yaadgaar naam.
    
    ### Tagline
    Ek short, one-line description.
    
    ### Mukhya Features
    5-7 zaroori features ki bulleted list.
    
    ### Target Audience
    Kaun is product ko istemal karega.
    
    ### Technology Suggestion
    App ke liye (jaise React Native) ya Web ke liye (jaise MERN stack) technology ka sujhav.
    
    Output ko aache se format karein headings (###) aur bullet points (*) ka istemal karke.`;

    try {
      const responseText = await callGeminiWithBackoff(prompt);
      ideaResultDiv.innerHTML = formatResponse(responseText);
    } catch (error) {
      console.error('Gemini API Error:', error);
      ideaResultDiv.textContent = 'Ek error aa gaya. Kripya thodi der baad dobara try karein.';
    } finally {
      ideaLoadingDiv.style.display = 'none';
      generateIdeaBtn.disabled = false;
    }
  });
  
  // Scroll Animation
  const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
          if (entry.isIntersecting) {
              entry.target.classList.add('visible');
          }
      });
  }, { threshold: 0.1 });

  document.querySelectorAll('.reveal').forEach(el => {
      observer.observe(el);
  });
</script>

</body>
</html>
