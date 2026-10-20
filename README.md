
<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="description" content="Ücretsiz kelime, karakter ve cümle sayacı, okuma süresi ve yüzde hesaplama araçları.">
<title>Pratik Araçlar - Ücretsiz Online Araçlar</title>
<style>
:root {
  --blue: #2459d3;
  --bg: #f2f5f9;
  --card: #ffffff;
  --text: #202938;
  --muted: #637083;
  --line: #dce3ed;
}
* { box-sizing: border-box; }
body {
  margin: 0;
  padding: 18px;
  background: var(--bg);
  color: var(--text);
  font-family: Arial, sans-serif;
  line-height: 1.5;
}
header {
  max-width: 850px;
  margin: 12px auto 24px;
  text-align: center;
}
header h1 { margin-bottom: 5px; }
header p { color: var(--muted); margin-top: 0; }
main { max-width: 850px; margin: auto; }
.card {
  background: var(--card);
  padding: 20px;
  margin-bottom: 18px;
  border: 1px solid var(--line);
  border-radius: 14px;
  box-shadow: 0 4px 15px #1720330a;
}
h2 { margin-top: 0; font-size: 21px; }
textarea, input {
  display: block;
  width: 100%;
  padding: 12px;
  margin: 8px 0 14px;
  border: 1px solid #cbd5e1;
  border-radius: 8px;
  font: inherit;
  background: white;
  color: #202938;
}
textarea { min-height: 180px; resize: vertical; }
label { font-weight: 600; }
button {
  padding: 11px 15px;
  border: 0;
  border-radius: 8px;
  background: var(--blue);
  color: white;
  font: inherit;
  font-weight: 600;
  cursor: pointer;
  margin: 3px 5px 3px 0;
}
button.secondary { background: #e8eefb; color: #2147a0; }
.stats {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 9px;
  margin: 15px 0;
}
.stat {
  text-align: center;
  background: #eef3ff;
  border-radius: 9px;
  padding: 12px 5px;
}
.number { display: block; font-size: 24px; font-weight: 700; }
.stat small { color: var(--muted); }
.result {
  background: #eef3ff;
  padding: 12px;
  border-radius: 8px;
  margin-top: 12px;
  overflow-wrap: anywhere;
}
.hint { color: var(--muted); font-size: 14px; }
footer {
  max-width: 850px;
  margin: 24px auto;
  text-align: center;
  color: var(--muted);
  font-size: 13px;
}
@media (max-width: 520px) {
  body { padding: 12px; }
  .card { padding: 15px; }
  .stats { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  button { padding: 11px 12px; }
}
</style>
</head>
<body>
<header>
  <h1>Pratik Araçlar</h1>
  <p>Ücretsiz, kolay ve kullanışlı çevrim içi araçlar</p>
</header>

<main>
  <section class="card">
    <h2>📝 Kelime ve Metin Sayacı</h2>
    <label for="metin">Metnini buraya yaz veya yapıştır</label>
    <textarea id="metin" placeholder="Metnini buraya yaz..."></textarea>

    <div class="stats">
      <div class="stat"><span class="number" id="kelime">0</span><small>Kelime</small></div>
      <div class="stat"><span class="number" id="karakter">0</span><small>Karakter</small></div>
      <div class="stat"><span class="number" id="cumle">0</span><small>Cümle</small></div>
      <div class="stat"><span class="number" id="sure">0</span><small>Okuma (dk.)</small></div>
    </div>

    <button id="kopyala">Metni Kopyala</button>
    <button class="secondary" id="temizle">Metni Temizle</button>
    <p class="hint">Okuma süresi dakikada yaklaşık 200 kelimeye göre hesaplanır.</p>
    <p id="kopyaMesaj" class="hint" aria-live="polite"></p>
  </section>

  <section class="card">
    <h2>🧮 Yüzde Hesaplama</h2>
    <label for="oran">Yüzde oranı (%)</label>
    <input id="oran" type="number" inputmode="decimal" placeholder="Örnek: 20">
    <label for="sayi">Sayı</label>
    <input id="sayi" type="number" inputmode="decimal" placeholder="Örnek: 500">
    <button id="hesapla">Yüzdeyi Hesapla</button>
    <div class="result" id="sonuc" aria-live="polite">Sonuç burada görünecek.</div>

    <hr style="border:0;border-top:1px solid var(--line);margin:20px 0">

    <h2>📊 Bir sayı diğerinin yüzde kaçı?</h2>
    <label for="parca">İlk sayı</label>
    <input id="parca" type="number" inputmode="decimal" placeholder="Örnek: 25">
    <label for="butun">İkinci sayı</label>
    <input id="butun" type="number" inputmode="decimal" placeholder="Örnek: 200">
    <button id="oranHesapla">Oranı Hesapla</button>
    <div class="result" id="oranSonuc" aria-live="polite">Sonuç burada görünecek.</div>
  </section>
</main>

<footer>Pratik Araçlar · Ücretsiz çevrim içi araçlar</footer>

<script>
const metin = document.getElementById("metin");
const kelime = document.getElementById("kelime");
const karakter = document.getElementById("karakter");
const cumle = document.getElementById("cumle");
const sure = document.getElementById("sure");

function say() {
  const yazi = metin.value.trim();
  const kelimeler = yazi ? yazi.split(/\s+/u) : [];
  const cumleler = yazi
    ? yazi.split(/[.!?…]+/u).filter(c => c.trim().length > 0)
    : [];

  kelime.textContent = kelimeler.length;
  karakter.textContent = metin.value.length;
  cumle.textContent = cumleler.length;
  sure.textContent = kelimeler.length
    ? Math.max(1, Math.ceil(kelimeler.length / 200))
    : 0;
}

metin.addEventListener("input", say);

document.getElementById("temizle").addEventListener("click", () => {
  metin.value = "";
  say();
  document.getElementById("kopyaMesaj").textContent = "";
  metin.focus();
});

document.getElementById("kopyala").addEventListener("click", async () => {
  const mesaj = document.getElementById("kopyaMesaj");
  if (!metin.value) {
    mesaj.textContent = "Önce kopyalanacak bir metin yaz.";
    return;
  }
  try {
    await navigator.clipboard.writeText(metin.value);
    mesaj.textContent = "Metin kopyalandı!";
  } catch (e) {
    metin.focus();
    metin.select();
    const ok = document.execCommand("copy");
    mesaj.textContent = ok
      ? "Metin kopyalandı!"
      : "Metni seçip cihazının Kopyala seçeneğini kullan.";
  }
});

function sayiOku(id) {
  const alan = document.getElementById(id);
  if (alan.value.trim() === "") return null;
  const deger = Number(alan.value);
  return Number.isFinite(deger) ? deger : null;
}

function bicimlendir(n) {
  return n.toLocaleString("tr-TR", { maximumFractionDigits: 6 });
}

document.getElementById("hesapla").addEventListener("click", () => {
  const oran = sayiOku("oran");
  const sayi = sayiOku("sayi");
  const sonuc = document.getElementById("sonuc");

  if (oran === null || sayi === null) {
    sonuc.textContent = "Lütfen iki alana da geçerli bir sayı gir.";
    return;
  }
  sonuc.textContent = bicimlendir(oran) + "% × " +
    bicimlendir(sayi) + " = " + bicimlendir(oran / 100 * sayi);
});

document.getElementById("oranHesapla").addEventListener("click", () => {
  const parca = sayiOku("parca");
  const butun = sayiOku("butun");
  const sonuc = document.getElementById("oranSonuc");

  if (parca === null || butun === null) {
    sonuc.textContent = "Lütfen iki alana da geçerli bir sayı gir.";
    return;
  }
  if (butun === 0) {
    sonuc.textContent = "İkinci sayı sıfır olamaz.";
    return;
  }
  sonuc.textContent = bicimlendir(parca) + ", " +
    bicimlendir(butun) + " sayısının %" +
    bicimlendir(parca / butun * 100) + " kadarıdır.";
});
</script>
<!-- PDF ARAÇLARI -->
<section id="pdf-araclari" style="padding:24px 12px; margin:20px auto; max-width:900px; font-family:Arial,sans-serif;">
  <h2>📄 PDF Araçları</h2>
  <p>PDF dosyalarını kolayca düzenle.</p>

  <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:14px;">

    <div style="padding:16px;border:1px solid #ddd;border-radius:12px;">
      <h3>📚 PDF Birleştir</h3>
      <input id="pdfMergeFiles" type="file" accept="application/pdf" multiple>
      <button onclick="pdfBirlestir()">PDF'leri Birleştir</button>
    </div>

    <div style="padding:16px;border:1px solid #ddd;border-radius:12px;">
      <h3>✂️ PDF Sayfalarını Ayır</h3>
      <input id="pdfSplitFile" type="file" accept="application/pdf">
      <p>Sayfa numarası (ör. 1,3,5)</p>
      <input id="pdfSplitPages" type="text" placeholder="1,3,5">
      <button onclick="pdfAyir()">Seçilen Sayfaları İndir</button>
    </div>

    <div style="padding:16px;border:1px solid #ddd;border-radius:12px;">
      <h3>🖼️ PDF'yi Görsele Dönüştür</h3>
      <input id="pdfImageFile" type="file" accept="application/pdf">
      <button onclick="pdfGorsel()">PNG Görsellerini İndir</button>
    </div>

    <div style="padding:16px;border:1px solid #ddd;border-radius:12px;">
      <h3>📦 PDF Boyutunu Optimize Et</h3>
      <input id="pdfCompressFile" type="file" accept="application/pdf">
      <button onclick="pdfOptimize()">Optimize Edilmiş PDF'yi İndir</button>
      <p style="font-size:12px;">Boyut azalması garanti değildir.</p>
    </div>

  </div>
  <p id="pdfStatus" role="status" style="margin-top:16px;"></p>
</section>

<script src="https://unpkg.com/pdf-lib@1.17.1/dist/pdf-lib.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
<script>
pdfjsLib.GlobalWorkerOptions.workerSrc =
  "https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js";

const pdfStatus = document.getElementById("pdfStatus");

async function pdfDosyaOku(inputId) {
  const f = document.getElementById(inputId).files[0];
  if (!f) throw new Error("Önce bir PDF dosyası seç.");
  return new Uint8Array(await f.arrayBuffer());
}

function pdfIndir(bytes, name, type = "application/pdf") {
  const url = URL.createObjectURL(new Blob([bytes], {type}));
  const a = document.createElement("a");
  a.href = url;
  a.download = name;
  a.click();
  setTimeout(() => URL.revokeObjectURL(url), 2000);
}

async function pdfBirlestir() {
  try {
    const files = [...document.getElementById("pdfMergeFiles").files];
    if (files.length < 2) throw new Error("En az iki PDF seç.");
    const out = await PDFLib.PDFDocument.create();
    for (const f of files) {
      const src = await PDFLib.PDFDocument.load(
        await f.arrayBuffer()
      );
      const pages = await out.copyPages(src, src.getPageIndices());
      pages.forEach(p => out.addPage(p));
    }
    pdfIndir(await out.save(), "birlesik.pdf");
    pdfStatus.textContent = "Birleştirme tamamlandı.";
  } catch (e) { pdfStatus.textContent = e.message; }
}

async function pdfAyir() {
  try {
    const bytes = await pdfDosyaOku("pdfSplitFile");
    const src = await PDFLib.PDFDocument.load(bytes);
    const text = document.getElementById("pdfSplitPages").value.trim();
    const nums = text.split(",").map(x => Number(x.trim()));
    if (!text || nums.some(n => !Number.isInteger(n) || n < 1 || n > src.getPageCount()))
      throw new Error("Geçerli sayfa numaraları yaz. Örnek: 1,3,5");
    const out = await PDFLib.PDFDocument.create();
    const pages = await out.copyPages(src, [...new Set(nums)].map(n => n - 1));
    pages.forEach(p => out.addPage(p));
    pdfIndir(await out.save(), "secili-sayfalar.pdf");
    pdfStatus.textContent = "Sayfalar hazır.";
  } catch (e) { pdfStatus.textContent = e.message; }
}

async function pdfGorsel() {
  try {
    const bytes = await pdfDosyaOku("pdfImageFile");
    const doc = await pdfjsLib.getDocument({data: bytes}).promise;
    for (let i = 1; i <= doc.numPages; i++) {
      pdfStatus.textContent = i + "/" + doc.numPages + " sayfa hazırlanıyor...";
      const page = await doc.getPage(i);
      const viewport = page.getViewport({scale: 1.5});
      const canvas = document.createElement("canvas");
      canvas.width = viewport.width;
      canvas.height = viewport.height;
      await page.render({canvasContext: canvas.getContext("2d"), viewport}).promise;
      const blob = await new Promise(resolve => canvas.toBlob(resolve, "image/png"));
      pdfIndir(await blob.arrayBuffer(), "sayfa-" + i + ".png", "image/png");
      canvas.width = 0;
      canvas.height = 0;
    }
    pdfStatus.textContent = "Görseller hazır.";
  } catch (e) { pdfStatus.textContent = "Dönüştürme başarısız. PDF'yi kontrol et."; }
}

async function pdfOptimize() {
  try {
    const bytes = await pdfDosyaOku("pdfCompressFile");
    const doc = await PDFLib.PDFDocument.load(bytes);
    const out = await doc.save({useObjectStreams: true});
    pdfIndir(out, "optimize.pdf");
    pdfStatus.textContent =
      "İşlem tamamlandı. Dosya boyutu mutlaka küçülmeyebilir.";
  } catch (e) { pdfStatus.textContent = e.message; }
}
</script>

<!-- GÖRSEL ARAÇLARI -->
<section id="gorsel-araclari" style="max-width:900px;margin:24px auto;padding:20px;font-family:Arial,sans-serif;">
  <h2>🖼️ Görsel Araçları</h2>
  <p>Fotoğraflarını ücretsiz olarak düzenle.</p>

  <label for="imgFile">Fotoğraf seç:</label>
  <input id="imgFile" type="file" accept="image/*" style="display:block;margin:12px 0;">

  <label for="imgFormat">Çıktı formatı:</label>
  <select id="imgFormat" style="display:block;margin:8px 0;padding:8px;">
    <option value="image/jpeg">JPG</option>
    <option value="image/png">PNG</option>
    <option value="image/webp">WebP</option>
  </select>

  <label for="imgQuality">Kalite / sıkıştırma:</label>
  <input id="imgQuality" type="range" min="30" max="100" value="80" style="display:block;margin:8px 0;">

  <label for="imgWidth">Yeni genişlik (piksel):</label>
  <input id="imgWidth" type="number" min="1" max="10000" placeholder="Boş bırak: orijinal" style="display:block;margin:8px 0;padding:8px;width:90%;">

  <label for="imgHeight">Yeni yükseklik (piksel):</label>
  <input id="imgHeight" type="number" min="1" max="10000" placeholder="Boş bırak: orijinal" style="display:block;margin:8px 0;padding:8px;width:90%;">

  <label style="display:block;margin:12px 0;">
    <input id="imgCrop" type="checkbox">
    Ortadan kırp (seçilen boyutlara göre)
  </label>

  <button id="imgProcess" type="button" style="padding:12px 18px;cursor:pointer;">
    Görseli işle ve indir
  </button>

  <p id="imgStatus" role="status" aria-live="polite"></p>
  <img id="imgPreview" alt="İşlenen görsel önizlemesi"
       style="display:none;max-width:100%;height:auto;margin-top:12px;">

  <script>
  (() => {
    const fileInput = document.getElementById("imgFile");
    const formatInput = document.getElementById("imgFormat");
    const qualityInput = document.getElementById("imgQuality");
    const widthInput = document.getElementById("imgWidth");
    const heightInput = document.getElementById("imgHeight");
    const cropInput = document.getElementById("imgCrop");
    const status = document.getElementById("imgStatus");
    const preview = document.getElementById("imgPreview");
    const button = document.getElementById("imgProcess");
    let previewUrl = null;

    button.addEventListener("click", async () => {
      let downloadUrl = null;
      button.disabled = true;

      try {
        const file = fileInput.files[0];
        if (!file) throw new Error("Önce bir fotoğraf seç.");

        if (!file.type.startsWith("image/"))
          throw new Error("Lütfen geçerli bir görsel seç.");

        const bitmap = await createImageBitmap(file);
        const originalW = bitmap.width;
        const originalH = bitmap.height;

        const rawW = widthInput.value.trim();
        const rawH = heightInput.value.trim();
        let w = rawW ? Number(rawW) : originalW;
        let h = rawH ? Number(rawH) : originalH;

        if (!Number.isInteger(w) || !Number.isInteger(h) ||
            w < 1 || h < 1 || w > 10000 || h > 10000)
          throw new Error("Genişlik ve yükseklik 1–10000 arasında tam sayı olmalı.");

        if (!rawW && rawH) w = Math.round(originalW * h / originalH);
        if (rawW && !rawH) h = Math.round(originalH * w / originalW);

        if (w * h > 40000000)
          throw new Error("Çıktı çok büyük. Daha küçük boyutlar seç.");

        const canvas = document.createElement("canvas");
        canvas.width = w;
        canvas.height = h;
        const ctx = canvas.getContext("2d");

        if (formatInput.value === "image/jpeg") {
          ctx.fillStyle = "#ffffff";
          ctx.fillRect(0, 0, w, h);
        }

        if (cropInput.checked) {
          const scale = Math.max(w / originalW, h / originalH);
          const sw = w / scale;
          const sh = h / scale;
          ctx.drawImage(bitmap,
            (originalW - sw) / 2, (originalH - sh) / 2, sw, sh,
            0, 0, w, h);
        } else {
          ctx.drawImage(bitmap, 0, 0, w, h);
        }

        bitmap.close();

        const blob = await new Promise(resolve =>
          canvas.toBlob(resolve, formatInput.value,
            Number(qualityInput.value) / 100)
        );

        if (!blob) throw new Error("Bu görsel dönüştürülemedi.");

        const ext = {
          "image/jpeg": "jpg",
          "image/png": "png",
          "image/webp": "webp"
        }[blob.type] || "png";

        downloadUrl = URL.createObjectURL(blob);
        const a = document.createElement("a");
        a.href = downloadUrl;
        a.download = "pratik-araclar." + ext;
        a.click();

        if (previewUrl) URL.revokeObjectURL(previewUrl);
        previewUrl = URL.createObjectURL(blob);
        preview.src = previewUrl;
        preview.style.display = "block";

        status.textContent =
          "Tamamlandı! Orijinal: " +
          Math.round(file.size / 1024) + " KB; yeni: " +
          Math.round(blob.size / 1024) + " KB.";
        canvas.width = 0;
        canvas.height = 0;
      } catch (error) {
        status.textContent = error.message || "İşlem başarısız.";
      } finally {
        if (downloadUrl) setTimeout(() => URL.revokeObjectURL(downloadUrl), 60000);
        button.disabled = false;
      }
    });
  })();
  </script>
</section>
<!-- GÖRSEL ARAÇLARI SONU -->
 
<!-- PRATİK ARAÇLAR MENÜSÜ -->
<nav id="ana-menu" style="padding:15px; margin:15px 0; border-radius:12px; background:#172554; color:white;">
  <h2 style="margin-top:0;">🛠️ Pratik Araçlar</h2>
  <p>Araç kategorisini seç:</p>
  <div style="display:flex; flex-wrap:wrap; gap:8px;">
    <a href="#pdf-araclari" style="background:#fff;color:#172554;padding:10px;border-radius:8px;text-decoration:none;">📄 PDF Araçları</a>
    <a href="#gorsel-araclari" style="background:#fff;color:#172554;padding:10px;border-radius:8px;text-decoration:none;">🖼️ Görsel Araçları</a>
    <a href="#hesaplama-araclari" style="background:#fff;color:#172554;padding:10px;border-radius:8px;text-decoration:none;">🧮 Hesaplama</a>
    <a href="#metin-araclari" style="background:#fff;color:#172554;padding:10px;border-radius:8px;text-decoration:none;">📝 Metin Araçları</a>
    <a href="#qr-araclari" style="background:#fff;color:#172554;padding:10px;border-radius:8px;text-decoration:none;">🔳 QR Kod</a>
    <a href="#web-araclari" style="background:#fff;color:#172554;padding:10px;border-radius:8px;text-decoration:none;">💻 Web Araçları</a>
  </div>
</nav>

</body>
</html>
