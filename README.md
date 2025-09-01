# DanshPedia-Payment
<!doctype html>
<html lang="id">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Payment Dans4you</title>
  <style>
    :root{
      --blue-900:#0a2540;
      --blue-700:#144a8a;
      --blue-600:#1b5fb8;
      --blue-500:#2b7be4;
      --blue-100:#e7f0ff;
      --ink:#0b1324;
      --muted:#5b6b8a;
      --card:#ffffff;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family:sans-serif;
      background: linear-gradient(135deg,var(--blue-100),#f7fbff);
      color:var(--ink);
    }
    .wrap{max-width:900px;margin:auto;padding:24px;}
    header{display:flex;justify-content:space-between;align-items:center;margin-bottom:20px;}
    h1{margin:0;font-size:24px;color:var(--blue-900);}
    .subtitle{color:var(--muted);font-size:14px}
    .grid{display:grid;gap:16px;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));}
    .card{background:#fff;border:1px solid #cfe1ff;padding:16px;border-radius:16px;box-shadow:0 4px 10px rgba(0,0,0,.1);}
    .badge{font-weight:bold;color:var(--blue-900);}
    .tag{font-size:12px;background:var(--blue-100);padding:4px 8px;border-radius:12px;color:var(--blue-700);}
    .qr{width:100%;aspect-ratio:1/1;border-radius:12px;background:#f3f6ff;margin:10px 0;}
    .row{display:flex;gap:8px;align-items:center;}
    .num{flex:1;padding:8px;border:1px solid #cfe1ff;border-radius:8px;background:#f6f9ff;font-weight:bold;}
    button{background:linear-gradient(180deg,var(--blue-500),var(--blue-600));color:#fff;border:none;border-radius:8px;padding:8px 12px;font-weight:bold;cursor:pointer;}
    footer{margin-top:20px;font-size:13px;color:var(--muted);text-align:center;}
    .toast{position:fixed;bottom:20px;left:50%;transform:translateX(-50%);background:#0f1729;color:#fff;padding:8px 12px;border-radius:20px;opacity:0;transition:.3s;}
    .toast.show{opacity:1;}
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div>
        <h1>Payment Dans4you</h1>
        <div class="subtitle">Metode pembayaran: DANA • GoPay • OVO</div>
      </div>
      <button id="btnShare">Bagikan Link</button>
    </header>

    <main class="grid">

      <!-- DANA -->
      <section class="card">
        <div class="badge">DANA <span class="tag">E-Wallet</span></div>
        <img class="qr" src="dana-qr.png" alt="QR DANA">
        <div class="row">
          <div class="num" id="num-dana" data-number="NO DANA">0881011892305</div>
          <button onclick="copyNumber('num-dana')">Copy</button>
        </div>
      </section>

      <!-- GoPay -->
      <section class="card">
        <div class="badge">GoPay <span class="tag">E-Wallet</span></div>
        <img class="qr" src="gopay-qr.png" alt="QR GoPay">
        <div class="row">
          <div class="num" id="num-gopay" data-number="NO GOPAY">083872735426</div>
          <button onclick="copyNumber('num-gopay')">Copy</button>
        </div>
      </section>

      <!-- OVO -->
      <section class="card">
        <div class="badge">OVO <span class="tag">E-Wallet</span></div>
        <img class="qr" src="ovo-qr.png" alt="QR OVO">
        <div class="row">
          <div class="num" id="num-ovo" data-number="NOMER OVO">083872735426</div>
          <button onclick="copyNumber('num-ovo')">Copy</button>
        </div>
      </section>

    </main>

    <footer>
      © <span id="year"></span> Payment Dans4you • Pastikan nama penerima sesuai sebelum transfer.
    </footer>
  </div>

  <div class="toast" id="toast"></div>

  <script>
    document.getElementById("year").textContent = new Date().getFullYear();

    function copyNumber(id){
      const el = document.getElementById(id);
      const text = el.dataset.number;
      navigator.clipboard.writeText(text).then(()=>{
        showToast("Nomor disalin: " + text);
      });
    }

    const toast = document.getElementById("toast");
    let timer;
    function showToast(msg){
      toast.textContent = msg;
      toast.classList.add("show");
      clearTimeout(timer);
      timer = setTimeout(()=>toast.classList.remove("show"),1500);
    }

    document.getElementById("btnShare").addEventListener("click", async ()=>{
      const data = {title: document.title, text:"Link Payment Dans4you", url:location.href};
      if(navigator.share){ await navigator.share(data); }
      else{ await navigator.clipboard.writeText(location.href); showToast("Link disalin"); }
    });
  </script>
</body>
</html>
