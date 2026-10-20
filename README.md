
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
</body>
</html>
