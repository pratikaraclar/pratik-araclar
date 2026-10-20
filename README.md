<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ücretsiz Kelime Sayacı</title>
<style>
body {
  font-family: Arial, sans-serif;
  background: #f2f5f9;
  margin: 0;
  padding: 20px;
  color: #222;
}
.container {
  max-width: 650px;
  margin: 30px auto;
  background: white;
  padding: 24px;
  border-radius: 14px;
  box-shadow: 0 4px 18px #0001;
}
h1 { text-align: center; }
textarea {
  width: 100%;
  height: 220px;
  box-sizing: border-box;
  padding: 14px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 8px;
}
.stats {
  display: flex;
  justify-content: space-around;
  gap: 10px;
  margin: 20px 0;
  text-align: center;
}
.stat {
  background: #eef3ff;
  padding: 14px;
  border-radius: 8px;
  flex: 1;
}
.number {
  display: block;
  font-size: 25px;
  font-weight: bold;
}
button {
  padding: 12px 18px;
  background: #2459d3;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
}
</style>
</head>
<body>
<div class="container">
  <h1>Ücretsiz Kelime Sayacı</h1>
  <p>Metnini aşağıya yaz veya yapıştır.</p>
  <textarea id="metin" placeholder="Metnini buraya yaz..."></textarea>
  <div class="stats">
    <div class="stat">
      <span class="number" id="kelime">0</span>
      Kelime
    </div>
    <div class="stat">
      <span class="number" id="karakter">0</span>
      Karakter
    </div>
  </div>
  <button onclick="temizle()">Metni Temizle</button>
</div>
<script>
const metin = document.getElementById("metin");
metin.addEventListener("input", () => {
  const yazi = metin.value.trim();
  document.getElementById("kelime").textContent =
    yazi ? yazi.split(/\s+/).length : 0;
  document.getElementById("karakter").textContent =
    metin.value.length;
});
function temizle() {
  metin.value = "";
  metin.dispatchEvent(new Event("input"));
}
</script>
</body>
</html>
