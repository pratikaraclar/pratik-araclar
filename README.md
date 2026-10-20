
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
  <!-- Diğer araç bölümleri sonraki parçalarda eklenecek -->
</main>

<footer>
  © 2026 Pratik Araçlar
</footer>
</body>
</html>
