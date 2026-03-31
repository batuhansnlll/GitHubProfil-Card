<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Batuhan Şanlı</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      min-height: 100vh;
      background: #0d0d1a;
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: 'Segoe UI', sans-serif;
      overflow: hidden;
    }

    /* Partikel arka plan */
    canvas {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      z-index: 0;
    }

    .sahne {
      perspective: 1000px;
      z-index: 1;
    }

    .kart {
      width: 380px;
      background: linear-gradient(135deg, #13132a 0%, #1a1a35 100%);
      border-radius: 24px;
      padding: 36px 32px;
      border: 1px solid rgba(83, 52, 131, 0.4);
      box-shadow: 0 0 40px rgba(83, 52, 131, 0.2), 0 20px 60px rgba(0,0,0,0.5);
      transform-style: preserve-3d;
      transition: box-shadow 0.1s;
      position: relative;
      overflow: hidden;
    }

    /* Parlayan köşe efekti */
    .kart::before {
      content: '';
      position: absolute;
      top: -1px; left: -1px; right: -1px; bottom: -1px;
      border-radius: 24px;
      background: linear-gradient(135deg, rgba(83,52,131,0.6), transparent 40%, transparent 60%, rgba(233,69,96,0.3));
      z-index: 0;
      opacity: 0;
      transition: opacity 0.3s;
    }
    .kart:hover::before { opacity: 1; }

    /* Işık yansıması */
    .parlak {
      position: absolute;
      top: 0; left: 0; right: 0; bottom: 0;
      border-radius: 24px;
      background: radial-gradient(circle at 50% 50%, rgba(255,255,255,0.04) 0%, transparent 60%);
      pointer-events: none;
      z-index: 0;
      transition: background 0.05s;
    }

    .icerik { position: relative; z-index: 1; }

    /* Avatar */
    .avatar-alan {
      display: flex;
      align-items: center;
      gap: 18px;
      margin-bottom: 24px;
    }
    .avatar {
      width: 72px;
      height: 72px;
      border-radius: 50%;
      background: linear-gradient(135deg, #533483, #e94560);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 28px;
      font-weight: 700;
      color: #fff;
      flex-shrink: 0;
      box-shadow: 0 0 20px rgba(83,52,131,0.5);
      animation: nabiz 3s ease-in-out infinite;
    }
    @keyframes nabiz {
      0%, 100% { box-shadow: 0 0 20px rgba(83,52,131,0.5); }
      50%       { box-shadow: 0 0 35px rgba(83,52,131,0.9), 0 0 60px rgba(233,69,96,0.3); }
    }

    .isim-alan h1 {
      color: #fff;
      font-size: 20px;
      font-weight: 700;
      letter-spacing: -0.3px;
    }
    .isim-alan p {
      color: #7b6fa0;
      font-size: 13px;
      margin-top: 3px;
    }
    .durum {
      display: flex;
      align-items: center;
      gap: 6px;
      margin-top: 6px;
    }
    .durum-nokta {
      width: 7px; height: 7px;
      border-radius: 50%;
      background: #68d391;
      animation: yanip 2s ease-in-out infinite;
    }
    @keyframes yanip {
      0%, 100% { opacity: 1; }
      50%       { opacity: 0.3; }
    }
    .durum span { color: #68d391; font-size: 12px; }

    /* Bölücü */
    .bolucü {
      height: 1px;
      background: linear-gradient(to right, transparent, rgba(83,52,131,0.5), transparent);
      margin: 20px 0;
    }

    /* Hakkında */
    .hakkinda {
      color: #9990b8;
      font-size: 13.5px;
      line-height: 1.7;
      margin-bottom: 22px;
    }

    /* Teknolojiler */
    .baslik {
      color: #555577;
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 1px;
      margin-bottom: 10px;
    }
    .teknolojiler {
      display: flex;
      flex-wrap: wrap;
      gap: 7px;
      margin-bottom: 22px;
    }
    .tech-pill {
      padding: 5px 12px;
      border-radius: 20px;
      font-size: 12px;
      font-weight: 600;
      border: 1px solid;
      transition: transform 0.2s, box-shadow 0.2s;
      cursor: default;
    }
    .tech-pill:hover {
      transform: translateY(-2px);
      box-shadow: 0 4px 12px rgba(0,0,0,0.3);
    }
    .tc { background: rgba(0,89,192,0.15); border-color: rgba(0,89,192,0.4); color: #5b9bd5; }
    .cs { background: rgba(35,145,32,0.15); border-color: rgba(35,145,32,0.4); color: #68d391; }
    .js { background: rgba(247,223,30,0.12); border-color: rgba(247,223,30,0.35); color: #f6e05e; }
    .ht { background: rgba(227,79,38,0.15); border-color: rgba(227,79,38,0.4); color: #fc8181; }
    .css{ background: rgba(21,114,182,0.15); border-color: rgba(21,114,182,0.4); color: #63b3ed; }
    .cpp{ background: rgba(83,52,131,0.2); border-color: rgba(83,52,131,0.5); color: #b794f4; }

    /* İstatistikler */
    .istatistikler {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 10px;
      margin-bottom: 22px;
    }
    .stat {
      background: rgba(83,52,131,0.1);
      border: 1px solid rgba(83,52,131,0.2);
      border-radius: 10px;
      padding: 10px;
      text-align: center;
    }
    .stat .sayi { color: #fff; font-size: 20px; font-weight: 700; }
    .stat .etiket { color: #555577; font-size: 10px; margin-top: 2px; }

    /* Linkler */
    .linkler {
      display: flex;
      gap: 10px;
    }
    .link-btn {
      flex: 1;
      padding: 10px;
      border-radius: 10px;
      border: 1px solid rgba(83,52,131,0.3);
      background: rgba(83,52,131,0.1);
      color: #9980c8;
      font-size: 12px;
      font-weight: 600;
      text-align: center;
      cursor: pointer;
      transition: all 0.2s;
      text-decoration: none;
      display: block;
    }
    .link-btn:hover {
      background: rgba(83,52,131,0.3);
      border-color: #533483;
      color: #fff;
      transform: translateY(-2px);
    }
    .link-btn.mail {
      background: rgba(233,69,96,0.1);
      border-color: rgba(233,69,96,0.3);
      color: #fc8181;
    }
    .link-btn.mail:hover {
      background: rgba(233,69,96,0.25);
      border-color: #e94560;
      color: #fff;
    }

    /* Alt yazı */
    .alt-yazi {
      text-align: center;
      color: #2a2a4a;
      font-size: 11px;
      margin-top: 16px;
    }
  </style>
</head>
<body>

<canvas id="canvas"></canvas>

<div class="sahne">
  <div class="kart" id="kart">
    <div class="parlak" id="parlak"></div>
    <div class="icerik">

      <div class="avatar-alan">
        <div class="avatar">BS</div>
        <div class="isim-alan">
          <h1>Batuhan Şanlı</h1>
          <p>Bilgisayar Programcısı</p>
          <div class="durum">
            <div class="durum-nokta"></div>
            <span>Öğrenmeye devam ediyor</span>
          </div>
        </div>
      </div>

      <div class="bolucü"></div>

      <p class="hakkinda">
        Yazılım dünyasına yeni adım atan, kendini sürekli geliştirmeye odaklanmış heyecanlı bir geliştirici. Her gün yeni şeyler öğrenmekten keyif alıyorum.
      </p>

      <div class="baslik">Teknolojiler</div>
      <div class="teknolojiler">
        <span class="tech-pill tc">C</span>
        <span class="tech-pill cs">C#</span>
        <span class="tech-pill cpp">C++</span>
        <span class="tech-pill js">JavaScript</span>
        <span class="tech-pill ht">HTML5</span>
        <span class="tech-pill css">CSS3</span>
      </div>

      <div class="baslik">GitHub</div>
      <div class="istatistikler">
        <div class="stat">
          <div class="sayi" id="proje-sayi">0</div>
          <div class="etiket">Proje</div>
        </div>
        <div class="stat">
          <div class="sayi" id="commit-sayi">0</div>
          <div class="etiket">Commit</div>
        </div>
        <div class="stat">
          <div class="sayi">29</div>
          <div class="etiket">Gün önce</div>
        </div>
      </div>

      <div class="linkler">
        <a class="link-btn" href="https://github.com/batuhansnlll" target="_blank">⌥ GitHub</a>
        <a class="link-btn mail" href="mailto:batuhansanli3131@gmail.com">✉ E-posta</a>
      </div>

    </div>
  </div>
</div>

<p class="alt-yazi" style="position:fixed;bottom:20px;left:0;right:0;z-index:2;">Kartı fareyle hareket ettir ✦</p>

<script>
  // 3D kart efekti
  const kart = document.getElementById('kart');
  const parlak = document.getElementById('parlak');

  kart.addEventListener('mousemove', e => {
    const r = kart.getBoundingClientRect();
    const x = e.clientX - r.left;
    const y = e.clientY - r.top;
    const cx = r.width / 2;
    const cy = r.height / 2;
    const rotY =  ((x - cx) / cx) * 14;
    const rotX = -((y - cy) / cy) * 10;
    kart.style.transform = `rotateX(${rotX}deg) rotateY(${rotY}deg) scale(1.02)`;
    parlak.style.background = `radial-gradient(circle at ${x}px ${y}px, rgba(255,255,255,0.07) 0%, transparent 60%)`;
  });

  kart.addEventListener('mouseleave', () => {
    kart.style.transform = 'rotateX(0deg) rotateY(0deg) scale(1)';
    kart.style.transition = 'transform 0.5s cubic-bezier(.4,0,.2,1)';
    parlak.style.background = 'radial-gradient(circle at 50% 50%, rgba(255,255,255,0.04) 0%, transparent 60%)';
    setTimeout(() => kart.style.transition = '', 500);
  });

  // Sayaç animasyonu
  function sayacAnimasyonu(id, hedef, sure) {
    const el = document.getElementById(id);
    let baslangic = 0;
    const adim = hedef / (sure / 16);
    const timer = setInterval(() => {
      baslangic += adim;
      if (baslangic >= hedef) { el.textContent = hedef; clearInterval(timer); }
      else el.textContent = Math.floor(baslangic);
    }, 16);
  }
  sayacAnimasyonu('proje-sayi', 2, 1200);
  sayacAnimasyonu('commit-sayi', 7, 1000);

  // Partikel arka plan
  const canvas = document.getElementById('canvas');
  const ctx = canvas.getContext('2d');
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;

  const partikeller = Array.from({ length: 80 }, () => ({
    x: Math.random() * canvas.width,
    y: Math.random() * canvas.height,
    r: Math.random() * 1.5 + 0.3,
    dx: (Math.random() - 0.5) * 0.3,
    dy: (Math.random() - 0.5) * 0.3,
    a: Math.random()
  }));

  function ciz() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    partikeller.forEach(p => {
      ctx.beginPath();
      ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
      ctx.fillStyle = `rgba(83,52,131,${p.a * 0.6})`;
      ctx.fill();
      p.x += p.dx; p.y += p.dy;
      if (p.x < 0 || p.x > canvas.width)  p.dx *= -1;
      if (p.y < 0 || p.y > canvas.height) p.dy *= -1;
    });
    requestAnimationFrame(ciz);
  }
  ciz();

  window.addEventListener('resize', () => {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  });
</script>
</body>
</html>
