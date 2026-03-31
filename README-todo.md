<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Yapılacaklar</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      min-height: 100vh;
      background: #0d0d1a;
      font-family: 'Segoe UI', sans-serif;
      display: flex;
      align-items: flex-start;
      justify-content: center;
      padding: 40px 20px;
    }

    .kapsayici { width: 100%; max-width: 560px; }

    /* BAŞLIK */
    .baslik-alan {
      margin-bottom: 32px;
    }
    .baslik-alan h1 {
      color: #fff;
      font-size: 30px;
      font-weight: 700;
      letter-spacing: -0.5px;
    }
    .baslik-alan p {
      color: #555577;
      font-size: 13px;
      margin-top: 4px;
    }

    /* ÖZET KARTLAR */
    .ozet-kartlar {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 12px;
      margin-bottom: 28px;
    }
    .ozet-kart {
      background: #13132a;
      border: 1px solid #1e1e3a;
      border-radius: 14px;
      padding: 16px;
      text-align: center;
    }
    .ozet-kart .sayi {
      font-size: 28px;
      font-weight: 700;
      color: #fff;
    }
    .ozet-kart .etiket {
      font-size: 11px;
      color: #555577;
      margin-top: 2px;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }
    .ozet-kart.yuksek .sayi { color: #e94560; }
    .ozet-kart.orta .sayi  { color: #f6ad55; }
    .ozet-kart.dusuk .sayi { color: #68d391; }

    /* GİRİŞ KARTI */
    .giris-karti {
      background: #13132a;
      border: 1px solid #1e1e3a;
      border-radius: 16px;
      padding: 20px;
      margin-bottom: 20px;
    }
    .giris-karti input[type="text"] {
      width: 100%;
      background: #0d0d1a;
      border: 1px solid #1e1e3a;
      border-radius: 10px;
      padding: 12px 16px;
      color: #fff;
      font-size: 14px;
      outline: none;
      margin-bottom: 12px;
      transition: border-color 0.2s;
    }
    .giris-karti input[type="text"]:focus { border-color: #533483; }
    .giris-karti input[type="text"]::placeholder { color: #333355; }

    .giris-alt {
      display: flex;
      gap: 10px;
      align-items: center;
    }

    .oncelik-sec {
      display: flex;
      gap: 6px;
    }
    .oncelik-btn {
      padding: 7px 14px;
      border-radius: 8px;
      border: 1px solid #1e1e3a;
      background: #0d0d1a;
      color: #555577;
      font-size: 12px;
      cursor: pointer;
      transition: all 0.2s;
    }
    .oncelik-btn.secili-yuksek { background: rgba(233,69,96,0.15); border-color: #e94560; color: #e94560; }
    .oncelik-btn.secili-orta  { background: rgba(246,173,85,0.15); border-color: #f6ad55; color: #f6ad55; }
    .oncelik-btn.secili-dusuk { background: rgba(104,211,145,0.15); border-color: #68d391; color: #68d391; }

    input[type="date"] {
      background: #0d0d1a;
      border: 1px solid #1e1e3a;
      border-radius: 8px;
      padding: 7px 12px;
      color: #888;
      font-size: 12px;
      outline: none;
      cursor: pointer;
      transition: border-color 0.2s;
    }
    input[type="date"]:focus { border-color: #533483; }

    .ekle-btn {
      margin-left: auto;
      padding: 8px 20px;
      background: #533483;
      color: #fff;
      border: none;
      border-radius: 10px;
      font-size: 14px;
      font-weight: 600;
      cursor: pointer;
      transition: background 0.2s;
      white-space: nowrap;
    }
    .ekle-btn:hover { background: #6b45a8; }

    /* FİLTRELER */
    .filtre-alan {
      display: flex;
      gap: 0;
      background: #13132a;
      border: 1px solid #1e1e3a;
      border-radius: 12px;
      padding: 4px;
      margin-bottom: 16px;
      position: relative;
    }
    .filtre-kaydirici {
      position: absolute;
      top: 4px;
      height: calc(100% - 8px);
      background: #533483;
      border-radius: 9px;
      transition: left 0.25s cubic-bezier(.4,0,.2,1), width 0.25s cubic-bezier(.4,0,.2,1);
      z-index: 0;
    }
    .filtre-btn {
      flex: 1;
      padding: 8px;
      border: none;
      background: transparent;
      color: #555577;
      font-size: 13px;
      cursor: pointer;
      border-radius: 9px;
      transition: color 0.2s;
      position: relative;
      z-index: 1;
    }
    .filtre-btn.aktif { color: #fff; font-weight: 600; }

    /* SIRALAMA */
    .siralama-alan {
      display: flex;
      align-items: center;
      gap: 8px;
      margin-bottom: 16px;
    }
    .siralama-alan span { color: #555577; font-size: 12px; }
    .siralama-sec {
      background: #13132a;
      border: 1px solid #1e1e3a;
      border-radius: 8px;
      padding: 6px 10px;
      color: #aaa;
      font-size: 12px;
      outline: none;
      cursor: pointer;
    }

    /* GÖREV LİSTESİ */
    .liste { display: flex; flex-direction: column; gap: 8px; }

    .gorev {
      display: flex;
      align-items: center;
      gap: 12px;
      background: #13132a;
      border: 1px solid #1e1e3a;
      border-radius: 13px;
      padding: 14px 16px;
      transition: border-color 0.2s, opacity 0.3s;
      animation: giris 0.2s ease;
      cursor: grab;
    }
    .gorev:active { cursor: grabbing; }
    .gorev.surukle-uzerine { border-color: #533483; background: #1a1a3a; }
    @keyframes giris {
      from { opacity: 0; transform: translateY(-6px); }
      to   { opacity: 1; transform: translateY(0); }
    }
    .gorev.tamamlandi { opacity: 0.45; }
    .gorev.tamamlandi .gorev-metin { text-decoration: line-through; color: #333355; }

    .oncelik-cubuk {
      width: 3px;
      height: 36px;
      border-radius: 4px;
      flex-shrink: 0;
    }
    .oncelik-cubuk.yuksek { background: #e94560; }
    .oncelik-cubuk.orta  { background: #f6ad55; }
    .oncelik-cubuk.dusuk { background: #68d391; }

    .checkbox {
      width: 20px;
      height: 20px;
      border-radius: 6px;
      border: 2px solid #2a2a4a;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-shrink: 0;
      transition: all 0.2s;
    }
    .checkbox.isaretli { background: #533483; border-color: #533483; }
    .checkbox.isaretli::after { content: '✓'; color: #fff; font-size: 11px; font-weight: 700; }

    .gorev-icerik { flex: 1; min-width: 0; }
    .gorev-metin { color: #ddd; font-size: 14px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
    .gorev-tarih {
      font-size: 11px;
      margin-top: 3px;
    }
    .gorev-tarih.gecmis { color: #e94560; }
    .gorev-tarih.yakin  { color: #f6ad55; }
    .gorev-tarih.normal { color: #555577; }

    .sil-btn {
      background: none;
      border: none;
      color: #2a2a4a;
      font-size: 16px;
      cursor: pointer;
      padding: 4px 6px;
      border-radius: 6px;
      transition: all 0.2s;
      flex-shrink: 0;
    }
    .sil-btn:hover { color: #e94560; background: rgba(233,69,96,0.1); }

    .bos-mesaj { text-align: center; color: #333355; font-size: 14px; padding: 50px 0; }
  </style>
</head>
<body>
<div class="kapsayici">

  <div class="baslik-alan">
    <h1>Yapılacaklar</h1>
    <p>Görevlerini önceliklendir, zamanını yönet.</p>
  </div>

  <div class="ozet-kartlar">
    <div class="ozet-kart yuksek">
      <div class="sayi" id="sayi-yuksek">0</div>
      <div class="etiket">Yüksek</div>
    </div>
    <div class="ozet-kart orta">
      <div class="sayi" id="sayi-orta">0</div>
      <div class="etiket">Orta</div>
    </div>
    <div class="ozet-kart dusuk">
      <div class="sayi" id="sayi-dusuk">0</div>
      <div class="etiket">Düşük</div>
    </div>
  </div>

  <div class="giris-karti">
    <input type="text" id="gorevGiris" placeholder="Yeni görev yaz..." maxlength="100">
    <div class="giris-alt">
      <div class="oncelik-sec">
        <button class="oncelik-btn secili-yuksek" data-oncelik="yuksek" onclick="oncelikSec('yuksek')">● Yüksek</button>
        <button class="oncelik-btn" data-oncelik="orta"   onclick="oncelikSec('orta')">● Orta</button>
        <button class="oncelik-btn" data-oncelik="dusuk"  onclick="oncelikSec('dusuk')">● Düşük</button>
      </div>
      <input type="date" id="tarihGiris">
      <button class="ekle-btn" onclick="gorevEkle()">+ Ekle</button>
    </div>
  </div>

  <div class="filtre-alan" id="filtreAlan">
    <div class="filtre-kaydirici" id="kaydirici"></div>
    <button class="filtre-btn aktif" onclick="filtrele('hepsi', this)">Hepsi</button>
    <button class="filtre-btn" onclick="filtrele('aktif', this)">Aktif</button>
    <button class="filtre-btn" onclick="filtrele('tamamlandi', this)">Tamamlandı</button>
  </div>

  <div class="siralama-alan">
    <span>Sırala:</span>
    <select class="siralama-sec" onchange="siralamaGuncelle(this.value)">
      <option value="eklenme">Eklenme sırası</option>
      <option value="oncelik">Öncelik</option>
      <option value="tarih">Son tarih</option>
    </select>
  </div>

  <div class="liste" id="liste"></div>
</div>

<script>
  let gorevler = JSON.parse(localStorage.getItem('gorevler') || '[]');
  let mevcutFiltre = 'hepsi';
  let mevcutSiralama = 'eklenme';
  let seciliOncelik = 'yuksek';
  let surukleIndex = null;

  document.getElementById('gorevGiris').addEventListener('keypress', e => {
    if (e.key === 'Enter') gorevEkle();
  });

  function oncelikSec(oncelik) {
    seciliOncelik = oncelik;
    document.querySelectorAll('.oncelik-btn').forEach(b => {
      b.className = 'oncelik-btn';
      if (b.dataset.oncelik === oncelik) b.classList.add('secili-' + oncelik);
    });
  }

  function gorevEkle() {
    const input = document.getElementById('gorevGiris');
    const metin = input.value.trim();
    if (!metin) return;
    const tarih = document.getElementById('tarihGiris').value;
    gorevler.push({ id: Date.now(), metin, oncelik: seciliOncelik, tarih, tamamlandi: false });
    input.value = '';
    kaydet();
    listeyiGuncelle();
  }

  function tamamlandiToggle(id) {
    const g = gorevler.find(g => g.id === id);
    if (g) g.tamamlandi = !g.tamamlandi;
    kaydet();
    listeyiGuncelle();
  }

  function gorevSil(id) {
    gorevler = gorevler.filter(g => g.id !== id);
    kaydet();
    listeyiGuncelle();
  }

  function filtrele(filtre, btn) {
    mevcutFiltre = filtre;
    document.querySelectorAll('.filtre-btn').forEach(b => b.classList.remove('aktif'));
    btn.classList.add('aktif');
    kaydiriciGuncelle(btn);
    listeyiGuncelle();
  }

  function kaydiriciGuncelle(aktifBtn) {
    const alan = document.getElementById('filtreAlan');
    const k = document.getElementById('kaydirici');
    const alanRect = alan.getBoundingClientRect();
    const btnRect = aktifBtn.getBoundingClientRect();
    k.style.left = (btnRect.left - alanRect.left) + 'px';
    k.style.width = btnRect.width + 'px';
  }

  function siralamaGuncelle(deger) {
    mevcutSiralama = deger;
    listeyiGuncelle();
  }

  function tarihRengi(tarih) {
    if (!tarih) return '';
    const bugun = new Date(); bugun.setHours(0,0,0,0);
    const hedef = new Date(tarih);
    const fark = (hedef - bugun) / 86400000;
    if (fark < 0)  return 'gecmis';
    if (fark <= 2) return 'yakin';
    return 'normal';
  }

  function tarihMetni(tarih) {
    if (!tarih) return '';
    const bugun = new Date(); bugun.setHours(0,0,0,0);
    const hedef = new Date(tarih);
    const fark = Math.round((hedef - bugun) / 86400000);
    if (fark < 0)  return '⚠ ' + Math.abs(fark) + ' gün geçti';
    if (fark === 0) return '⏰ Bugün son gün!';
    if (fark === 1) return '⏰ Yarın son gün';
    return '📅 ' + hedef.toLocaleDateString('tr-TR');
  }

  function sirala(liste) {
    if (mevcutSiralama === 'oncelik') {
      const sira = { yuksek: 0, orta: 1, dusuk: 2 };
      return [...liste].sort((a, b) => sira[a.oncelik] - sira[b.oncelik]);
    }
    if (mevcutSiralama === 'tarih') {
      return [...liste].sort((a, b) => {
        if (!a.tarih && !b.tarih) return 0;
        if (!a.tarih) return 1;
        if (!b.tarih) return -1;
        return new Date(a.tarih) - new Date(b.tarih);
      });
    }
    return liste;
  }

  function listeyiGuncelle() {
    const liste = document.getElementById('liste');

    let gosterilen = gorevler;
    if (mevcutFiltre === 'aktif')      gosterilen = gorevler.filter(g => !g.tamamlandi);
    if (mevcutFiltre === 'tamamlandi') gosterilen = gorevler.filter(g => g.tamamlandi);
    gosterilen = sirala(gosterilen);

    document.getElementById('sayi-yuksek').textContent = gorevler.filter(g => g.oncelik === 'yuksek' && !g.tamamlandi).length;
    document.getElementById('sayi-orta').textContent   = gorevler.filter(g => g.oncelik === 'orta'   && !g.tamamlandi).length;
    document.getElementById('sayi-dusuk').textContent  = gorevler.filter(g => g.oncelik === 'dusuk'  && !g.tamamlandi).length;

    if (gosterilen.length === 0) {
      liste.innerHTML = '<p class="bos-mesaj">Görev yok 🎯</p>';
      return;
    }

    liste.innerHTML = gosterilen.map((g, i) => `
      <div class="gorev ${g.tamamlandi ? 'tamamlandi' : ''}"
           draggable="true"
           ondragstart="surukleBasla(${g.id})"
           ondragover="surukleUzeri(event, ${i})"
           ondrop="birak(${i})"
           ondragleave="this.classList.remove('surukle-uzerine')">
        <div class="oncelik-cubuk ${g.oncelik}"></div>
        <div class="checkbox ${g.tamamlandi ? 'isaretli' : ''}" onclick="tamamlandiToggle(${g.id})"></div>
        <div class="gorev-icerik">
          <div class="gorev-metin">${g.metin}</div>
          ${g.tarih ? `<div class="gorev-tarih ${tarihRengi(g.tarih)}">${tarihMetni(g.tarih)}</div>` : ''}
        </div>
        <button class="sil-btn" onclick="gorevSil(${g.id})">✕</button>
      </div>
    `).join('');

    // Kaydırıcıyı güncelle
    const aktifBtn = document.querySelector('.filtre-btn.aktif');
    if (aktifBtn) kaydiriciGuncelle(aktifBtn);
  }

  function surukleBasla(id) { surukleIndex = gorevler.findIndex(g => g.id === id); }

  function surukleUzeri(e, i) {
    e.preventDefault();
    document.querySelectorAll('.gorev').forEach(el => el.classList.remove('surukle-uzerine'));
    document.querySelectorAll('.gorev')[i]?.classList.add('surukle-uzerine');
  }

  function birak(hedefIndex) {
    document.querySelectorAll('.gorev').forEach(el => el.classList.remove('surukle-uzerine'));
    if (surukleIndex === null || surukleIndex === hedefIndex) return;
    const [gorev] = gorevler.splice(surukleIndex, 1);
    gorevler.splice(hedefIndex, 0, gorev);
    surukleIndex = null;
    kaydet();
    listeyiGuncelle();
  }

  function kaydet() { localStorage.setItem('gorevler', JSON.stringify(gorevler)); }

  // Başlangıç kaydırıcı
  window.addEventListener('load', () => {
    const aktif = document.querySelector('.filtre-btn.aktif');
    if (aktif) setTimeout(() => kaydiriciGuncelle(aktif), 50);
    listeyiGuncelle();
  });
</script>
</body>
</html>
