<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>BGS SMP — Minecraft Server</title>
  <style>
    :root{
      --accent: #2ecc71; /* green heading */
      --bg: #0b1220;
      --card: #0f1724;
      --gold: linear-gradient(180deg,#ffd54a,#f6b12e);
      font-family: Inter, system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;
    }
    body{margin:0;background:radial-gradient(ellipse at bottom,#07111a 0%, #04121a 60%, #000 100%);color:#e6eef8}
    header{display:flex;align-items:center;gap:18px;padding:28px 32px}
    .logo{width:120px;height:120px;flex:0 0 120px;border-radius:12px;overflow:hidden;box-shadow:0 8px 30px rgba(0,0,0,.6)}
    .logo img{width:100%;height:100%;object-fit:cover;display:block}
    h1{font-size:34px;margin:0;color:var(--accent);text-shadow:0 4px 18px rgba(46,204,113,0.12)}
    .sub{color:#9fb3c8;margin-top:6px}

    main{max-width:980px;margin:24px auto;padding:18px}
    .grid{display:grid;grid-template-columns:1fr 340px;gap:18px}

    .card{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));border:1px solid rgba(255,255,255,0.03);padding:18px;border-radius:12px;box-shadow:0 8px 30px rgba(2,6,23,0.6)}

    .server-info{display:flex;flex-direction:column;gap:12px}
    .ip{font-family:monospace;background:rgba(255,255,255,0.03);padding:10px;border-radius:8px;display:flex;align-items:center;justify-content:space-between}
    .btn{background:var(--accent);border:none;color:#042017;padding:10px 12px;border-radius:8px;font-weight:600;cursor:pointer}
    .btn.ghost{background:transparent;border:1px solid rgba(255,255,255,0.04);color:inherit}

    .ranks{display:flex;gap:12px;flex-wrap:wrap}
    .rank{flex:1 1 140px;padding:14px;border-radius:10px;background:linear-gradient(180deg,rgba(255,255,255,0.015),transparent);border:1px solid rgba(255,255,255,0.02)}
    .rank h3{margin:0;font-size:16px}
    .price{font-weight:700;margin-top:6px}

    .crates-list{display:flex;flex-direction:column;gap:10px}
    .crate{display:flex;align-items:center;gap:12px;padding:12px;border-radius:10px}
    .crate .icon{width:56px;height:56px;border-radius:8px;background:rgba(0,0,0,0.25);display:flex;align-items:center;justify-content:center;font-weight:700}

    footer{max-width:980px;margin:28px auto;color:#9fb3c8;padding:0 18px}

    /* modal */
    .modal{position:fixed;inset:0;display:none;align-items:center;justify-content:center;background:rgba(2,6,23,0.6);z-index:60}
    .modal.open{display:flex}
    .modal .panel{background:linear-gradient(180deg,#07121a,#081923);padding:18px;border-radius:12px;min-width:320px;border:1px solid rgba(255,255,255,0.03)}

    .success{color:#8beb9a;font-weight:700}

    @media (max-width:880px){.grid{grid-template-columns:1fr}header{padding:18px}.logo{width:84px;height:84px}}
  </style>
</head>
<body>
  <header>
    <div class="logo">
      <!-- Using image from the conversation container. If it doesn't show, replace src with your uploaded logo path -->
      <img src="/mnt/data/WhatsApp Image 2025-09-21 at 07.23.54_7940e8b9.jpg" alt="BGS SMP logo: bearded avatar holding cube earth" />
    </div>
    <div>
      <h1 id="server-name">BGS SMP</h1>
      <div class="sub">A friendly Minecraft survival server — custom ranks, crates, and more.</div>
    </div>
  </header>

  <main>
    <div class="grid">
      <section class="card">
        <h2 style="margin-top:0;color:var(--accent)">Server Details</h2>
        <div class="server-info">
          <div class="ip" title="Click to copy IP">
            <div>
              <div style="font-size:13px;color:#9fb3c8">IP &amp; Port</div>
              <div id="server-ip">BGSSMP.aternos.me:21257</div>
            </div>
            <div style="display:flex;gap:8px">
              <button class="btn" id="copy-ip">Copy</button>
              <button class="btn ghost" id="connect-btn">Launch Minecraft</button>
            </div>
          </div>

          <p style="margin:0;font-size:14px;color:#9fb3c8">Tip: Click <strong>Copy</strong> then paste into Minecraft's server address field. The "Launch Minecraft" button will try to open the minecraft protocol if the user has the desktop client installed.</p>

          <hr style="border:none;border-top:1px solid rgba(255,255,255,0.03);margin:12px 0">

          <h3 style="margin:0;color:#cfe9ff">Online Features</h3>
          <ul style="margin:8px 0 0 18px;color:#9fb3c8">
            <li>Survival, Custom Economy &amp; Shops</li>
            <li>Custom Ranks (buyable / earned)</li>
            <li>Crates / Keys mini-game</li>
            <li>Active community &amp; events</li>
          </ul>
        </div>
      </section>

      <aside class="card">
        <h2 style="margin-top:0;color:var(--accent);">Ranks &amp; Crates</h2>

        <div style="margin-top:8px">
          <div class="ranks">
            <div class="rank">
              <h3>Member</h3>
              <div class="price">Free</div>
              <div style="font-size:13px;color:#9fb3c8;margin-top:6px">Basic access to the server.</div>
              <button class="btn ghost" onclick="showDetails('Member','Free','Member rank is default for new players')">Details</button>
            </div>

            <div class="rank">
              <h3>Builder</h3>
              <div class="price">$4.99</div>
              <div style="font-size:13px;color:#9fb3c8;margin-top:6px">Extra claims &amp; building perks.</div>
              <button class="btn" onclick="openPurchase('Builder',4.99)">Buy</button>
            </div>

            <div class="rank">
              <h3>VIP</h3>
              <div class="price">$9.99</div>
              <div style="font-size:13px;color:#9fb3c8;margin-top:6px">More homes, priority queue.</div>
              <button class="btn" onclick="openPurchase('VIP',9.99)">Buy</button>
            </div>

            <div class="rank">
              <h3>Legend</h3>
              <div class="price">$19.99</div>
              <div style="font-size:13px;color:#9fb3c8;margin-top:6px">Top cosmetic perks &amp; crate boosts.</div>
              <button class="btn" onclick="openPurchase('Legend',19.99)">Buy</button>
            </div>
          </div>
        </div>

        <hr style="border:none;border-top:1px solid rgba(255,255,255,0.03);margin:12px 0">

        <h3 style="margin:0;color:#cfe9ff">Crates</h3>
        <div class="crates-list">
          <div class="crate card" style="align-items:center">
            <div class="icon">A</div>
            <div style="flex:1">
              <div style="font-weight:700">Alpha Crate</div>
              <div style="font-size:13px;color:#9fb3c8">Contains common rewards &amp; small chance of rare items.</div>
            </div>
            <button class="btn" onclick="openCrate('Alpha')">Open</button>
          </div>

          <div class="crate card" style="align-items:center">
            <div class="icon">R</div>
            <div style="flex:1">
              <div style="font-weight:700">Royal Crate</div>
              <div style="font-size:13px;color:#9fb3c8">Higher chance of rare items.</div>
            </div>
            <button class="btn" onclick="openCrate('Royal')">Open</button>
          </div>

          <div class="crate card" style="align-items:center">
            <div class="icon">L</div>
            <div style="flex:1">
              <div style="font-weight:700">Legend Crate</div>
              <div style="font-size:13px;color:#9fb3c8">Top tier rewards and cosmetics.</div>
            </div>
            <button class="btn" onclick="openCrate('Legend')">Open</button>
          </div>
        </div>

      </aside>
    </div>

    <!-- Purchase / modal dialogs -->
    <div id="modal" class="modal" role="dialog" aria-hidden="true">
      <div class="panel" id="modal-panel">
        <!-- dynamic content -->
      </div>
    </div>

  </main>

  <footer>
    <small>© <span id="year"></span> BGS SMP — Server IP: <strong>BGSSMP.aternos.me:21257</strong></small>
  </footer>

  <script>
    // basic interactive features so "all item is working"
    document.getElementById('year').textContent = new Date().getFullYear();

    // copy IP
    document.getElementById('copy-ip').addEventListener('click', async ()=>{
      const ip = document.getElementById('server-ip').textContent.trim();
      try{
        await navigator.clipboard.writeText(ip);
        showToast('IP copied to clipboard');
      }catch(e){
        // fallback
        const ta = document.createElement('textarea');ta.value = ip;document.body.appendChild(ta);ta.select();
        try{document.execCommand('copy'); showToast('IP copied to clipboard');}catch(err){alert('Copy failed, please select and copy manually: ' + ip);}ta.remove();
      }
    });

    // Launch minecraft protocol (may only work in desktop with proper handler)
    document.getElementById('connect-btn').addEventListener('click', ()=>{
      const ip = document.getElementById('server-ip').textContent.trim();
      // this uses the minecraft: URL scheme
      window.location.href = 'minecraft://' + ip;
    });

    // Modal helpers
    const modal = document.getElementById('modal');
    const panel = document.getElementById('modal-panel');
    function openModal(html){panel.innerHTML = html; modal.classList.add('open'); modal.setAttribute('aria-hidden','false');}
    function closeModal(){modal.classList.remove('open'); modal.setAttribute('aria-hidden','true');}
    modal.addEventListener('click',(e)=>{ if(e.target===modal) closeModal(); });

    function showDetails(name,price,desc){
      openModal(`<h3 style="margin-top:0">${escapeHtml(name)} — ${escapeHtml(price)}</h3><p style="color:#9fb3c8">${escapeHtml(desc)}</p><div style="margin-top:12px;display:flex;gap:8px;justify-content:flex-end"><button class=\"btn ghost\" onclick=\"closeModal()\">Close</button></div>`)
    }

    function openPurchase(name,price){
      openModal(`<h3 style=\"margin-top:0\">Purchase ${escapeHtml(name)}</h3>
        <p style=\"color:#9fb3c8\">Price: $${Number(price).toFixed(2)}</p>
        <label style=\"display:block;margin-top:8px;color:#9fb3c8;font-size:13px\">Your In-Game Name</label>
        <input id=\"buyer-name\" placeholder=\"Steve123\" style=\"width:100%;padding:10px;border-radius:8px;border:1px solid rgba(255,255,255,0.04);background:transparent;color:inherit;margin-top:6px\" />
        <div style=\"margin-top:12px;display:flex;gap:8px;justify-content:flex-end\">
          <button class=\"btn ghost\" onclick=\"closeModal()\">Cancel</button>
          <button class=\"btn\" onclick=\"confirmPurchase(\'${escapeJs(name)}\',${price})\">Pay $${Number(price).toFixed(2)}</button>
        </div>`)
    }

    function confirmPurchase(name,price){
      const buyer = document.getElementById('buyer-name').value.trim();
      if(!buyer){alert('Please enter your in-game name.');return}
      // Simulate a purchase flow: store locally and show success. In real site, connect to payment gateway.
      const purchases = JSON.parse(localStorage.getItem('bgs_purchases')||'[]');
      purchases.push({name,price,buyer,date:new Date().toISOString()});
      localStorage.setItem('bgs_purchases',JSON.stringify(purchases));
      openModal(`<h3 style=\"margin-top:0\">Purchase Complete</h3><p class=\"success\">Thanks ${escapeHtml(buyer)} — ${escapeHtml(name)} was added to your account.</p><p style=\"color:#9fb3c8;margin-top:8px\">This is a demo flow — connect your payment backend to fulfill real purchases.</p><div style=\"margin-top:12px;display:flex;gap:8px;justify-content:flex-end\"><button class=\"btn\" onclick=\"closeModal()\">Close</button></div>`)
    }

    // Crates: simple randomization demo
    function openCrate(crate){
      const items = {
        'Alpha':['5x Coal','10x Oak Sapling','Iron Ingot','Rare Dye (2%)'],
        'Royal':['Gold Ingot','Enchanted Book (Sharpness)','Diamond (5%)','Emerald (3%)'],
        'Legend':['Elytra (0.5%)','Nether Star (0.2%)','Custom Pet (0.1%)','1000 Coins']
      };
      const pool = items[crate]||['Nothing'];

      // simple rarity weighting demo (last item is rarest)
      const idx = Math.floor(Math.pow(Math.random(),2) * pool.length);
      const prize = pool[idx];
      openModal(`<h3 style=\"margin-top:0\">${escapeHtml(crate)} Crate</h3><p style=\"color:#9fb3c8\">You opened a ${escapeHtml(crate)} crate and received:</p><div style=\"margin-top:10px;padding:12px;border-radius:8px;background:rgba(255,255,255,0.02);font-weight:700\">${escapeHtml(prize)}</div><div style=\"margin-top:12px;display:flex;gap:8px;justify-content:flex-end\"><button class=\"btn ghost\" onclick=\"closeModal()\">Close</button></div>`)
    }

    function escapeHtml(s){return String(s).replace(/[&<>"']/g, c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":"&#39;"})[c])}
    function escapeJs(s){return String(s).replace(/\\/g,'\\\\').replace(/'/g,"\\'")}

    // small toast
    function showToast(msg){
      const t = document.createElement('div'); t.textContent = msg; t.style.position='fixed';t.style.right='18px';t.style.bottom='18px';t.style.padding='10px 14px';t.style.borderRadius='8px';t.style.background='rgba(0,0,0,0.6)';t.style.border='1px solid rgba(255,255,255,0.03)';t.style.color='#cfe9ff';t.style.zIndex=9999;document.body.appendChild(t);
      setTimeout(()=>t.style.opacity=0,2200);setTimeout(()=>t.remove(),2600);
    }

    // preload demo purchases (so user can inspect localStorage)
    if(!localStorage.getItem('bgs_demo')){
      localStorage.setItem('bgs_demo','1');
      localStorage.removeItem('bgs_purchases');
    }
  </script>
</body>
</html>
