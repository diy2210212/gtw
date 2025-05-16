<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Halaman Pembayaran FAHRUL STORE</title>
  <style>
    :root {
      --primary-color: #0a74da;
      --primary-dark: #095ab0;
      --bg-light: #ffffff;
      --bg-dark: #1e1e1e;
      --text-light: #333;
      --text-dark: #eee;
    }

    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(45deg, rgb(255, 0, 150), rgb(0, 204, 255), rgb(102, 255, 0), rgb(255, 255, 0));
      background-size: 400% 400%;
      animation: gradient 10s ease infinite;
      color: var(--text-light);
      padding: 20px;
      margin: 0;
      min-height: 100vh;
      box-sizing: border-box;
    }

    .main-container {
      max-width: 500px;
      margin: 0 auto;
    }

    @keyframes gradient {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    .container {
      background: var(--bg-light);
      border-radius: 10px;
      padding: 25px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.1);
      margin-bottom: 20px;
    }

    @media (prefers-color-scheme: dark) {
      body {
        color: var(--text-dark);
      }

      .container {
        background: #2a2a2a;
        box-shadow: 0 0 10px rgba(255, 255, 255, 0.05);
      }

      .copy-box {
        background: #333;
      }

      .copy-box:hover {
        background: #444;
      }
      
      #confirmationMessage {
        background: #333;
        border-left-color: var(--primary-dark);
      }
    }

    h2 {
      text-align: center;
      color: var(--primary-color);
      font-weight: bold;
      margin-top: 0;
    }

    .payment-info {
      margin: 20px 0;
    }

    .label {
      font-weight: bold;
      margin-bottom: 6px;
      display: block;
    }

    .copy-box {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: #eee;
      padding: 10px 15px;
      border-radius: 6px;
      cursor: pointer;
      margin: 10px 0;
    }

    .copy-box:hover {
      background: #ddd;
    }

    .qris {
      text-align: center;
      margin: 20px 0;
    }

    .qris img {
      max-width: 100%;
      height: auto;
      border: 10px solid #ccc;
      border-radius: 6px;
      box-sizing: border-box;
    }

    button {
      padding: 10px 20px;
      background: var(--primary-color);
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      transition: background 0.2s;
      font-weight: bold;
    }

    button:hover {
      background: var(--primary-dark);
    }

    input[type="text"],
    input[type="number"] {
      width: 100%;
      padding: 10px;
      margin: 8px 0 16px;
      border: 1px solid #ccc;
      border-radius: 6px;
      box-sizing: border-box;
      font-size: 16px;
    }

    ol {
      padding-left: 20px;
      line-height: 1.6;
    }

    ol li {
      margin-bottom: 8px;
    }

    #confirmationMessage {
      margin-top: 20px;
      padding: 15px;
      border-left: 4px solid var(--primary-color);
      background: #f0f8ff;
      border-radius: 6px;
      line-height: 1.6;
    }
    
    hr {
      border: none;
      height: 1px;
      background-color: #ccc;
      margin: 20px 0;
    }
    
    .copy-box button {
      margin: 0;
      padding: 5px 10px;
      font-size: 14px;
    }
  </style>
</head>
<body>
  <div class="main-container">
    <div class="container">
      <h2>Pembayaran FAHRUL STORE</h2>
      <hr>

      <div class="payment-info">
        <div class="label">Konfirmasi Pembayaran:</div>
        <form id="paymentForm">
          <label for="name">Nama Anda:</label>
          <input type="text" id="name" name="name" required>

          <label for="amount">Jumlah Pembayaran (Rp):</label>
          <input type="number" id="amount" name="amount" required>

          <button type="submit">Kirim Pembayaran</button>
        </form>

        <div id="confirmationMessage"></div>
      </div>

      <div class="payment-info">
        <div class="label">Nomor DANA:</div>
        <div class="copy-box" onclick="copyDana()">
          <span id="danaNumber">083159206263</span>
          <button>Salin</button>
        </div>
      </div>

      <div class="payment-info">
        <div class="label">Cara Transfer DANA:</div>
        <ol>
          <li>Buka aplikasi DANA.</li>
          <li>Pilih menu <strong>"Kirim"</strong>.</li>
          <li>Masukkan nomor di atas.</li>
          <li>Pastikan atas nama: <strong>Adi Nxx</strong>.</li>
          <li>Masukkan jumlah dana dan lanjutkan pembayaran.</li>
        </ol>
      </div>

      <div class="qris">
        <div class="label">Atau Scan QRIS:</div>
        <img src="https://files.catbox.moe/f1ybjf.jpg" alt="QRIS Pembayaran">
      </div>
    </div>
  </div>

  <script>
    function copyDana() {
      const danaNumber = document.getElementById("danaNumber").textContent;
      navigator.clipboard.writeText(danaNumber).then(() => {
        alert("Nomor DANA berhasil disalin!");
      }).catch(err => {
        console.error('Gagal menyalin teks: ', err);
      });
    }

    document.getElementById("paymentForm").addEventListener("submit", function (e) {
      e.preventDefault();

      const name = document.getElementById("name").value.trim();
      const amount = document.getElementById("amount").value.trim();

      if (!name || !amount) {
        alert("Harap isi semua field yang diperlukan!");
        return;
      }

      const message = ` 
        <strong>Terima kasih, ${name}!</strong><br>
        Kami telah menerima konfirmasi pembayaran sebesar <strong>Rp ${parseInt(amount).toLocaleString('id-ID')}</strong>.<br>
        Tolong kirim bukti transfer ke Fahrul Store.`;

      document.getElementById("confirmationMessage").innerHTML = message;

      // Simpan data ke localStorage
      const paymentData = { 
        name: name, 
        amount: amount,
        date: new Date().toLocaleString()
      };
      localStorage.setItem("paymentData", JSON.stringify(paymentData));
      
      // Reset form
      document.getElementById("paymentForm").reset();
    });
  </script>
</body>
</html>
