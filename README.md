
<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Pratik Araçlar</title>
  <meta name="description" content="Ücretsiz çevrim içi PDF, metin, görsel ve hesaplama araçları.">
  <style>
    * {
      box-sizing: border-box;
    }

    html {
      scroll-behavior: smooth;
    }

    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #f1f5f9;
      color: #172033;
      line-height: 1.6;
    }

    header {
      background: #172554;
      color: white;
      text-align: center;
      padding: 28px 16px;
    }

    header h1 {
      margin: 0 0 8px;
      font-size: 30px;
    }

    header p {
      margin: 0;
    }

    nav {
      background: white;
      padding: 14px;
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      gap: 8px;
      box-shadow: 0 2px 8px #00000010;
    }

    nav a {
      display: inline-block;
      background: #e0e7ff;
      color: #172554;
      padding: 9px 12px;
      border-radius: 9px;
      text-decoration: none;
      font-size: 14px;
      font-weight: bold;
    }

    nav a:hover {
      background: #c7d2fe;
    }

    main {
      width: 100%;
      max-width: 900px;
      margin: 20px auto;
      padding: 0 14px;
    }

    .card {
      background: white;
      padding: 20px;
      margin-bottom: 18px;
      border-radius: 14px;
      box-shadow: 0 3px 12px #0000000a;
      scroll-margin-top: 15px;
    }

    h2 {
      color: #172554;
      margin-top: 0;
    }

    input, textarea, select, button {
      font: inherit;
      max-width: 100%;
    }

    input, textarea, select {
      width: 100%;
      padding: 11px;
      margin: 6px 0 12px;
      border: 1px solid #cbd5e1;
      border-radius: 8px;
    }

    button, .file-label {
      display: inline-block;
      border: 0;
      border-radius: 8px;
      padding: 11px 15px;
      background: #1d4ed8;
      color: white;
      cursor: pointer;
      font-weight: bold;
    }

    button:hover, .file-label:hover {
      background: #1e40af;
    }

    .result {
      margin-top: 12px;
      padding: 12px;
      background: #eff6ff;
      border-radius: 8px;
      overflow-wrap: anywhere;
    }

    .tool-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 14px;
    }

    .tool-grid .card {
      margin-bottom: 0;
    }

    .muted {
      color: #64748b;
      font-size: 14px;
    }

    footer {
      text-align: center;
      padding: 22px 12px;
      color: #64748b;
    }

    @media (max-width: 480px) {
      header h1 {
        font-size: 25px;
      }

      .card {
        padding: 15px;
      }

      nav a {
        flex: 1 1 42%;
        text-align: center;
      }
    }
  </style>
</head>
<body>

<header>
  <h1>🛠️ Pratik Araçlar</h1>
  <p>Ücretsiz, kolay ve kullanışlı çevrim içi araçlar</p>
</header>

<nav aria-label="Araç kategorileri">
  <a href="#metin-araclari">📝 Metin</a>
  <a href="#hesaplama-araclari">🧮 Hesaplama</a>
  <a href="#pdf-araclari">📄 PDF</a>
  <a href="#gorsel-araclari">🖼️ Görsel</a>
</nav>

<main>
  
<section class="card" id="metin-araclari">
  <h2>📝 Kelime ve Metin Sayacı</h2>
  <p>Metnini yaz veya yapıştır; sonuçlar otomatik hesaplanır.</p>

  <textarea id="metinSayaci" rows="6"
    placeholder="Metnini buraya yaz..."></textarea>

  <div class="result" id="metinSayaciSonuc">
    Kelime: 0 | Karakter: 0 | Boşluksuz karakter: 0
  </div>

  <button type="button" onclick="metinSayaciTemizle()">Temizle</button>
  <button type="button" onclick="metinSayaciKopyala()">Metni kopyala</button>
</section>

<script>
(function () {
  const alan = document.getElementById("metinSayaci");
  const sonuc = document.getElementById("metinSayaciSonuc");

  function guncelle() {
    const metin = alan.value;
    const temiz = metin.trim();
    const kelime = temiz ? temiz.split(/\s+/u).length : 0;

    sonuc.textContent =
      "Kelime: " + kelime +
      " | Karakter: " + metin.length +
      " | Boşluksuz karakter: " + metin.replace(/\s/g, "").length;
  }

  alan.addEventListener("input", guncelle);

  window.metinSayaciTemizle = function () {
    alan.value = "";
    guncelle();
  };

  window.metinSayaciKopyala = async function () {
    if (!alan.value) {
      alert("Önce bir metin yaz.");
      return;
    }

    try {
      await navigator.clipboard.writeText(alan.value);
      alert("Metin kopyalandı!");
    } catch (e) {
      alan.focus();
      alan.select();
      alert("Metni seçtim. Kopyalamak için Kopyala seçeneğine dokun.");
    }
  };

  guncelle();
})();
</script>

  
<section class="card" id="hesaplama-araclari">
  <h2>🧮 Hesaplama Araçları</h2>

  <h3>Yüzde Hesaplama</h3>
  <label for="hesapYuzde">Yüzde oranı (%)</label>
  <input type="number" id="hesapYuzde" placeholder="Örn. 20">

  <label for="hesapSayi">Sayı</label>
  <input type="number" id="hesapSayi" placeholder="Örn. 500">

  <button type="button" onclick="yuzdeHesaplaYeni()">Hesapla</button>
  <div class="result" id="yuzdeSonucYeni">Sonuç burada görünecek.</div>

  <hr>

  <h3>Dört İşlem</h3>
  <label for="hesapSayi1">Birinci sayı</label>
  <input type="number" id="hesapSayi1" placeholder="Örn. 100">

  <label for="hesapIslem">İşlem seç</label>
  <select id="hesapIslem">
    <option value="+">Toplama (+)</option>
    <option value="-">Çıkarma (-)</option>
    <option value="*">Çarpma (×)</option>
    <option value="/">Bölme (÷)</option>
  </select>

  <label for="hesapSayi2">İkinci sayı</label>
  <input type="number" id="hesapSayi2" placeholder="Örn. 20">

  <button type="button" onclick="dortIslemYeni()">Hesapla</button>
  <div class="result" id="dortIslemSonucYeni">Sonuç burada görünecek.</div>

  <hr>

  <h3>İndirim Hesaplama</h3>
  <label for="indirimFiyatYeni">Ürün fiyatı (TL)</label>
  <input type="number" id="indirimFiyatYeni" min="0" step="any" placeholder="Örn. 1000">

  <label for="indirimOranYeni">İndirim oranı (%)</label>
  <input type="number" id="indirimOranYeni" min="0" max="100" step="any" placeholder="Örn. 15">

  <button type="button" onclick="indirimHesaplaYeni()">Hesapla</button>
  <div class="result" id="indirimSonucYeni">Sonuç burada görünecek.</div>
</section>

<script>
function yuzdeHesaplaYeni() {
  const o = document.getElementById("hesapYuzde").value;
  const s = document.getElementById("hesapSayi").value;
  const r = document.getElementById("yuzdeSonucYeni");

  if (o === "" || s === "") {
    r.textContent = "İki alanı da doldur.";
    return;
  }

  r.textContent = "Sonuç: " + (Number(o) * Number(s) / 100);
}

function dortIslemYeni() {
  const a = document.getElementById("hesapSayi1").value;
  const b = document.getElementById("hesapSayi2").value;
  const i = document.getElementById("hesapIslem").value;
  const r = document.getElementById("dortIslemSonucYeni");

  if (a === "" || b === "") {
    r.textContent = "İki sayıyı da gir.";
    return;
  }

  if (i === "/" && Number(b) === 0) {
    r.textContent = "Sıfıra bölme yapılamaz.";
    return;
  }

  let sonuc;
  if (i === "+") sonuc = Number(a) + Number(b);
  if (i === "-") sonuc = Number(a) - Number(b);
  if (i === "*") sonuc = Number(a) * Number(b);
  if (i === "/") sonuc = Number(a) / Number(b);

  r.textContent = "Sonuç: " + sonuc;
}

function indirimHesaplaYeni() {
  const f = document.getElementById("indirimFiyatYeni").value;
  const o = document.getElementById("indirimOranYeni").value;
  const r = document.getElementById("indirimSonucYeni");

  if (f === "" || o === "" || Number(f) < 0 ||
      Number(o) < 0 || Number(o) > 100) {
    r.textContent = "Fiyatı ve %0–100 arasındaki indirim oranını kontrol et.";
    return;
  }

  const indirim = Number(f) * Number(o) / 100;
  const sonFiyat = Number(f) - indirim;

  r.textContent =
    "İndirim tutarı: " + indirim.toFixed(2) +
    " TL | İndirimli fiyat: " + sonFiyat.toFixed(2) + " TL";
}
</script>

</main>

<footer>
  © 2026 Pratik Araçlar
</footer>
</body>
</html>
