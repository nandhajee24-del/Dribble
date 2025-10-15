# Project Responsive Web Design using Bootstrap
## Date:14/10/2025

## AIM:
To create a simplified clone of Dribbble (https://dribbble.com/) landing page.


## DESIGN STEPS:

### Step 1:
Clone the repository from GitHub.

### Step 2:
Create Django Admin project.

### Step 3:
Create a New App under the Django Admin project.

### Step 4:
Insert the necessary CSS and JavaScript files as external in order to use Bootstrap.

### Step 5:
Create a HTML file and include the needed Bootstrap components.

### Step 6:
Publish the website in the LocalHost.

## PROGRAM :
```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Dynamic Picture — High Level Web Page</title>
  <meta name="description" content="Single-file demo: dynamic hero picture, responsive layout, gallery, and subtle interactions." />

  <!-- Simple reset + modern type -->
  <style>
    :root{
      --bg:#0f1724; --card:#0b1220; --muted:#9aa4b2; --accent:#6ee7b7; --glass: rgba(255,255,255,0.05);
      --radius:16px; --max-width:1100px;
      --ease: cubic-bezier(.2,.9,.3,1);
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0; font-family:Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial; background:linear-gradient(180deg,var(--bg), #071026 120%); color:#e6eef6; -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;
      display:flex; align-items:center; justify-content:center; padding:40px 20px;
    }
    .site{width:100%; max-width:var(--max-width);}

    /* Header */
    header{display:flex; align-items:center; justify-content:space-between; gap:16px; margin-bottom:28px}
    .brand{display:flex; align-items:center; gap:12px}
    .logo{width:48px; height:48px; border-radius:12px; background:linear-gradient(135deg,#6ee7b7,#60a5fa); display:flex; align-items:center; justify-content:center; font-weight:700; color:#05233a}
    nav a{color:var(--muted); text-decoration:none; margin-left:18px}
    nav a:hover{color:var(--accent)}

    /* Hero */
    .hero{display:grid; grid-template-columns: 1fr 420px; gap:28px; align-items:center;}
    @media (max-width:980px){ .hero{grid-template-columns:1fr;}
      .hero-right{order:-1}
    }
    .hero-left h1{font-size:clamp(28px,4vw,44px); margin:0 0 12px}
    .hero-left p{color:var(--muted); margin:0 0 18px}
    .cta{display:flex; gap:12px}
    .btn{background:linear-gradient(90deg,var(--accent),#60a5fa); color:#05233a; border:none; padding:12px 18px; border-radius:12px; cursor:pointer; font-weight:600; transition:transform .18s var(--ease)}
    .btn:active{transform:scale(.98)}
    .ghost{background:transparent; border:1px solid rgba(255,255,255,0.06); color:var(--muted)}

    /* Dynamic picture card */
    .card{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); border-radius:var(--radius); padding:14px; backdrop-filter: blur(6px); box-shadow: 0 10px 30px rgba(2,6,23,0.7)}
    .hero-right{position:relative;}
    .viewport{width:100%; height:320px; border-radius:12px; overflow:hidden; position:relative}
    .slides{position:absolute; inset:0; display:flex; transition:transform .6s var(--ease)}
    .slide{min-width:100%; height:100%; display:flex; align-items:center; justify-content:center; position:relative}
    .slide img{width:100%; height:100%; object-fit:cover; display:block}
    .meta{position:absolute; left:14px; bottom:14px; background:var(--glass); padding:8px 12px; border-radius:10px; color:var(--muted); font-size:13px}
    .dots{display:flex; gap:8px; position:absolute; right:12px; bottom:14px}
    .dot{width:10px; height:10px; border-radius:999px; background:rgba(255,255,255,0.15); cursor:pointer}
    .dot.active{transform:scale(1.4); background:var(--accent)}

    /* Gallery */
    .gallery{display:grid; grid-template-columns: repeat(3,1fr); gap:12px; margin-top:26px}
    @media (max-width:800px){ .gallery{grid-template-columns:repeat(2,1fr)} }
    .thumb{border-radius:12px; overflow:hidden; cursor:pointer; height:140px; position:relative}
    .thumb img{width:100%; height:100%; object-fit:cover; display:block; transition:transform .35s var(--ease)}
    .thumb:hover img{transform:scale(1.06)}

    /* Modal */
    .modal{position:fixed; inset:0; display:flex; align-items:center; justify-content:center; background:rgba(3,6,12,0.6); visibility:hidden; opacity:0; transition:opacity .2s}
    .modal.open{visibility:visible; opacity:1}
    .modal .modal-card{width:min(92vw,1000px); border-radius:12px; overflow:hidden; background:#061122}
    .modal img{width:100%; height:auto; display:block}
    .close{position:absolute; right:18px; top:18px; background:rgba(255,255,255,0.03); border-radius:10px; padding:8px; cursor:pointer}

    /* Footer */
    footer{margin-top:28px; color:var(--muted); font-size:13px; text-align:center}

    /* subtle animated background (CSS particles) */
    .bg-particles{position:fixed; inset:0; z-index:-1; pointer-events:none; opacity:0.12}
    .particle{position:absolute; border-radius:50%; background:linear-gradient(90deg,#60a5fa,#6ee7b7); mix-blend-mode:screen; filter:blur(10px);}
  </style>
</head>
<body>
  <div class="bg-particles" id="particles"></div>
  <div class="site">
    <header>
      <div class="brand">
        <div class="logo">DP</div>
        <div>
          <div style="font-weight:700">Dynamic Picture</div>
          <div style="font-size:12px;color:var(--muted)">High-level single-file demo</div>
        </div>
      </div>
      <nav>
        <a href="#features">Features</a>
        <a href="#gallery">Gallery</a>
        <a href="#contact">Contact</a>
      </nav>
    </header>

    <main class="card hero">
      <div class="hero-left">
        <h1>Stunning, interactive hero with dynamic pictures</h1>
        <p>Single-page template showing: auto-play slideshow, parallax-like particles, responsive gallery with lightbox, and a small scriptable API to swap images dynamically.</p>
        <div class="cta">
          <button class="btn" id="swapBtn">Randomize Pictures</button>
          <button class="btn ghost" id="pauseBtn">Pause</button>
        </div>
        <section id="features" style="margin-top:18px">
          <h3 style="margin:6px 0 8px">Core features</h3>
          <ul style="color:var(--muted);margin:0;padding-left:18px">
            <li>Auto-play + manual controls for hero slideshow</li>
            <li>Lightbox gallery, keyboard navigation</li>
            <li>JavaScript API: replaceImages(array), pause(), play()</li>
          </ul>
        </section>
      </div>

      <div class="hero-right card">
        <div class="viewport" id="viewport">
          <div class="slides" id="slides">
            <div class="slide"><img alt="slide-1" src="https://images.unsplash.com/photo-1506744038136-46273834b3fb?q=80&w=1600&auto=format&fit=crop&ixlib=rb-4.0.3&s=1"><div class="meta">Ocean Vista — auto</div></div>
            <div class="slide"><img alt="slide-2" src="https://images.unsplash.com/photo-1500530855697-b586d89ba3ee?q=80&w=1600&auto=format&fit=crop&ixlib=rb-4.0.3&s=2"><div class="meta">Mountain Light</div></div>
            <div class="slide"><img alt="slide-3" src="https://images.unsplash.com/photo-1501785888041-af3ef285b470?q=80&w=1600&auto=format&fit=crop&ixlib=rb-4.0.3&s=3"><div class="meta">City Nights</div></div>
          </div>
          <div class="dots" id="dots"></div>
        </div>
      </div>
    </main>

    <section id="gallery" class="gallery">
      <div class="thumb card"><img src="https://images.unsplash.com/photo-1519681393784-d120267933ba?q=80&w=1200&auto=format&fit=crop" alt="thumb1" data-caption="Forest Path"></div>
      <div class="thumb card"><img src="https://images.unsplash.com/photo-1470770903676-69b98201ea1c?q=80&w=1200&auto=format&fit=crop" alt="thumb2" data-caption="Desert Road"></div>
      <div class="thumb card"><img src="https://images.unsplash.com/photo-1441974231531-c6227db76b6e?q=80&w=1200&auto=format&fit=crop" alt="thumb3" data-caption="Cozy Cabin"></div>
      <div class="thumb card"><img src="https://images.unsplash.com/photo-1519682337058-a94d519337bc?q=80&w=1200&auto=format&fit=crop" alt="thumb4" data-caption="Aurora"></div>
      <div class="thumb card"><img src="https://images.unsplash.com/photo-1482192596544-9eb780fc7f66?q=80&w=1200&auto=format&fit=crop" alt="thumb5" data-caption="River Bend"></div>
      <div class="thumb card"><img src="https://images.unsplash.com/photo-1441716844725-09cedc13a4e7?q=80&w=1200&auto=format&fit=crop" alt="thumb6" data-caption="Golden Field"></div>
    </section>

    <div class="modal" id="modal">
      <div class="modal-card">
        <div style="position:relative">
          <button class="close" id="closeModal">✕</button>
          <img id="modalImg" src="" alt="modal">
        </div>
        <div style="padding:12px;color:var(--muted)" id="modalCaption"></div>
      </div>
    </div>

    <footer id="contact">Built with ❤️ — tweak images or the script to fit your project</footer>
  </div>

  <script>
    // ----- Simple particle background -----
    const particlesEl = document.getElementById('particles');
    for(let i=0;i<12;i++){
      const p=document.createElement('div'); p.className='particle';
      const size=20+Math.random()*160; p.style.width=size+'px'; p.style.height=size+'px';
      p.style.left=(Math.random()*100)+'%'; p.style.top=(Math.random()*100)+'%';
      p.style.opacity=0.6*Math.random()+0.1; p.style.transform='translate(-50%,-50%)';
      p.style.animation = `float ${20+Math.random()*25}s linear ${-Math.random()*20}s infinite`;
      particlesEl.appendChild(p);
    }
    const style = document.createElement('style'); style.innerHTML = `@keyframes float{0%{transform:translateY(0)}50%{transform:translateY(-40px)}100%{transform:translateY(0)}}`; document.head.appendChild(style);

    // ----- Hero slideshow logic -----
    const slidesEl = document.getElementById('slides');
    const slides = [...slidesEl.children];
    const dotsEl = document.getElementById('dots');
    let idx=0; let interval=null; let playing=true;

    function renderDots(){
      dotsEl.innerHTML='';
      slides.forEach((_,i)=>{
        const d=document.createElement('div'); d.className='dot'+(i===idx?' active':''); d.onclick=()=>go(i);
        dotsEl.appendChild(d);
      });
    }
    function update(){ slidesEl.style.transform = `translateX(${-idx*100}%)`; renderDots(); }
    function go(i){ idx = (i+slides.length)%slides.length; update(); }
    function next(){ go(idx+1); }
    function play(){ if(interval) clearInterval(interval); interval=setInterval(next,3500); playing=true; document.getElementById('pauseBtn').textContent='Pause'; }
    function pause(){ if(interval) clearInterval(interval); interval=null; playing=false; document.getElementById('pauseBtn').textContent='Play'; }

    document.getElementById('pauseBtn').addEventListener('click', ()=>{ if(playing) pause(); else play(); });

    renderDots(); play();

    // Expose a small API: replaceImages(arrayOfUrls)
    function replaceImages(arr){
      // only replace as many as provided, preserve count
      slides.forEach((slide,i)=>{
        const img = slide.querySelector('img');
        img.src = arr[i % arr.length] || img.src;
      });
    }
    document.getElementById('swapBtn').addEventListener('click', ()=>{
      // pick random unsplash themes
      const themes=['mountain','ocean','city','forest','desert','aurora','river','cabin'];
      const picks = Array.from({length:slides.length},()=>`https://images.unsplash.com/photo-` + (Date.now()%999999999) + `?q=80&w=1600&auto=format&fit=crop`);
      replaceImages(picks);
    });

    // ----- Gallery lightbox -----
    const modal = document.getElementById('modal'); const modalImg = document.getElementById('modalImg'); const caption = document.getElementById('modalCaption');
    document.querySelectorAll('.thumb img').forEach(img=>{
      img.addEventListener('click',()=>{
        modalImg.src = img.src.replace('q=80&w=1200','q=80&w=1600');
        caption.textContent = img.getAttribute('data-caption') || img.alt || '';
        openModal();
      });
    });
    function openModal(){ modal.classList.add('open'); pause(); }
    function closeModal(){ modal.classList.remove('open'); play(); }
    document.getElementById('closeModal').addEventListener('click', closeModal);
    modal.addEventListener('click', (e)=>{ if(e.target===modal) closeModal(); });
    document.addEventListener('keydown', (e)=>{
      if(modal.classList.contains('open')){
        if(e.key==='Escape') closeModal();
      }
      if(e.key==='ArrowRight') next();
      if(e.key==='ArrowLeft') go(idx-1);
    });

    // Expose globally for quick tinkering
    window.DP = { replaceImages, pause, play };
  </script>
</body>
</html>


```

## OUTPUT:
![alt text](<Screenshot 2025-10-15 114156.png>)
![alt text](<Screenshot 2025-10-15 114316.png>)
## RESULT:
The Project for responsive web design using Bootstrap is completed successfully.
