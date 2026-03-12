<script>
  import { onMount } from 'svelte';
  import { inject } from '@vercel/analytics';

  onMount(() => {
    inject();
  });

  let verified = false;

  function onCaptchaVerify(token) {
    verified = true;
  }
</script>

<svelte:head>
  <title>Investment Insights - Arya</title>
</svelte:head>

<div class="container">
  <header>
    <h1>Investment Insights</h1>
    <p>Google Trends Analysis - 12 Maret 2026</p>
    <div class="last-updated">Updated: 12 Maret 2026</div>
  </header>

  <div class="card">
    <h2>Top Trending di US</h2>
    <div class="top-trends">
      <div class="trend-item"><div class="name">PSG vs Chelsea</div><div class="growth">+1,000%</div></div>
      <div class="trend-item"><div class="name">Vinnie Pasquantino</div><div class="growth">+1,000%</div></div>
      <div class="trend-item"><div class="name">Weather</div><div class="growth">+75%</div></div>
      <div class="trend-item"><div class="name">Iran California</div><div class="growth">+900%</div></div>
      <div class="trend-item"><div class="name">Venezuala vs DR</div><div class="growth">+900%</div></div>
      <div class="trend-item"><div class="name">Rivian R2</div><div class="growth">+100%</div></div>
      <div class="trend-item"><div class="name">Jake Paul</div><div class="growth">+1,000%</div></div>
      <div class="trend-item"><div class="name">Cyber Attacks</div><div class="growth">+1,000%</div></div>
    </div>
  </div>

  <div class="card">
    <h2>1 Hari (Very Short-term)</h2>
    <span class="timeframe very-short">1 Hari</span>
    <table>
      <tr><th>Tren</th><th>Asset/Saham</th><th>Opportunity</th><th>Estimasi Kenaikan</th><th>Estimasi Penurunan</th></tr>
      <tr>
        <td>Olahraga (PSG, NBA)</td>
        <td class="asset-name">DIS, WBD</td>
        <td>Sports media rights, streaming</td>
        <td class="estimate gain">+3-5%</td>
        <td class="estimate loss">-2-3%</td>
      </tr>
      <tr>
        <td>Winter Storm</td>
        <td class="asset-name">XLU, NEE</td>
        <td>Utility stocks, emergency supplies</td>
        <td class="estimate gain">+2-4%</td>
        <td class="estimate loss">-1-2%</td>
      </tr>
      <tr>
        <td>Iran Tensions</td>
        <td class="asset-name">LMT, RTX, PANW</td>
        <td>Defense & Cybersecurity</td>
        <td class="estimate gain">+4-8%</td>
        <td class="estimate loss">-3-5%</td>
      </tr>
    </table>
  </div>

  <div class="card">
    <h2>7 Hari (Short-term)</h2>
    <span class="timeframe short">7 Hari</span>
    <table>
      <tr><th>Tren</th><th>Asset/Saham</th><th>Opportunity</th><th>Estimasi Kenaikan</th><th>Estimasi Penurunan</th></tr>
      <tr>
        <td>Olahraga (PSG, NBA)</td>
        <td class="asset-name">DIS, PENN, DKNG</td>
        <td>Sports betting stocks, ESPN/Disney</td>
        <td class="estimate gain">+5-10%</td>
        <td class="estimate loss">-3-5%</td>
      </tr>
      <tr>
        <td>Winter Storm</td>
        <td class="asset-name">XLU, ED</td>
        <td>Utility stocks, emergency supplies</td>
        <td class="estimate gain">+3-6%</td>
        <td class="estimate loss">-2-4%</td>
      </tr>
      <tr>
        <td>Iran Tensions</td>
        <td class="asset-name">LMT, RTX, CRWD, ZS</td>
        <td>Defense (LMT, RTX), Cybersecurity (CRWD)</td>
        <td class="estimate gain">+8-15%</td>
        <td class="estimate loss">-5-8%</td>
      </tr>
    </table>
  </div>

  <div class="card">
    <h2>1 Bulan</h2>
    <span class="timeframe medium">1 Bulan</span>
    <table>
      <tr><th>Tren</th><th>Asset/Saham</th><th>Opportunity</th><th>Estimasi Kenaikan</th><th>Estimasi Penurunan</th></tr>
      <tr>
        <td>Rivian R2</td>
        <td class="asset-name">RIVN, TSLA, LCID</td>
        <td>EV stocks - RIVN preview launches</td>
        <td class="estimate gain">+10-20%</td>
        <td class="estimate loss">-8-12%</td>
      </tr>
      <tr>
        <td>Cybersecurity</td>
        <td class="asset-name">CRWD, ZS, PANW, OKTA</td>
        <td>Long-term: Enterprise security</td>
        <td class="estimate gain">+15-25%</td>
        <td class="estimate loss">-8-15%</td>
      </tr>
      <tr>
        <td>Creator Economy</td>
        <td class="asset-name">RBLX, SNAP, Pika</td>
        <td>Influencer platforms, content creation</td>
        <td class="estimate gain">+8-18%</td>
        <td class="estimate loss">-5-10%</td>
      </tr>
    </table>
  </div>

  <div class="card">
    <h2>6 Bulan - 1 Tahun</h2>
    <span class="timeframe long">6-12 Bulan</span>
    <table>
      <tr><th>Tren</th><th>Asset/Saham</th><th>Opportunity</th><th>Estimasi Kenaikan</th><th>Estimasi Penurunan</th></tr>
      <tr>
        <td>EV Overall</td>
        <td class="asset-name">TSLA, RIVN, BYD, FSR</td>
        <td>Electric vehicles - election year subsidies</td>
        <td class="estimate gain">+20-40%</td>
        <td class="estimate loss">-15-25%</td>
      </tr>
      <tr>
        <td>Sports Media</td>
        <td class="asset-name">NFLX, AMZN, DIS</td>
        <td>Netflix sports, Amazon Prime streaming</td>
        <td class="estimate gain">+15-30%</td>
        <td class="estimate loss">-10-20%</td>
      </tr>
      <tr>
        <td>Geopolitics</td>
        <td class="asset-name">LMT, BA, GD, CRWD</td>
        <td>Defense & cybersecurity - recurring theme</td>
        <td class="estimate gain">+25-50%</td>
        <td class="estimate loss">-15-30%</td>
      </tr>
      <tr>
        <td>AI/Cloud</td>
        <td class="asset-name">NVDA, MSFT, GOOGL, AMZN</td>
        <td>AI infrastructure & services</td>
        <td class="estimate gain">+30-60%</td>
        <td class="estimate loss">-20-35%</td>
      </tr>
    </table>
  </div>

  <div class="captcha-container">
    <div class="g-recaptcha" data-sitekey="6LeIxAcTAAAAAJcZVRqyHh71UMIEGNQ_MXjiZKhI"></div>
  </div>

  <div class="disclaimer">
    Disclaimer: Ini berdasarkan Google Trends search patterns, BUKAN financial advice. 
    Lakukan riset sendiri sebelum investasi. Risiko rugi selalu ada.
  </div>

  <footer>
    Generated by Arya - 12 Maret 2026
  </footer>
</div>

<style>
  :global(*) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  :global(body) {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
    background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
    color: #fff;
    min-height: 100vh;
    padding: 20px;
  }

  .container {
    max-width: 1000px;
    margin: 0 auto;
  }

  header {
    text-align: center;
    padding: 40px 0;
  }

  header h1 {
    font-size: 2.5rem;
    background: linear-gradient(90deg, #00d4ff, #7c3aed);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  header p {
    color: #8892b0;
    margin-top: 10px;
  }

  .card {
    background: rgba(255,255,255,0.05);
    border-radius: 16px;
    padding: 24px;
    margin-bottom: 24px;
    border: 1px solid rgba(255,255,255,0.1);
  }

  .card h2 {
    color: #00d4ff;
    margin-bottom: 16px;
    font-size: 1.3rem;
  }

  .timeframe {
    display: inline-block;
    padding: 4px 12px;
    border-radius: 20px;
    font-size: 0.85rem;
    margin-right: 8px;
    margin-bottom: 8px;
  }

  .very-short { background: #ef4444; color: #fff; }
  .short { background: #f59e0b; color: #000; }
  .medium { background: #3b82f6; color: #fff; }
  .long { background: #10b981; color: #fff; }

  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 12px;
  }

  th, td {
    text-align: left;
    padding: 12px;
    border-bottom: 1px solid rgba(255,255,255,0.1);
  }

  th {
    color: #8892b0;
    font-weight: 500;
    font-size: 0.85rem;
  }

  td:first-child {
    color: #00d4ff;
    font-weight: 500;
  }

  .asset-name {
    color: #fbbf24 !important;
    font-weight: 600;
  }

  .estimate {
    font-size: 0.85rem;
  }

  .gain {
    color: #10b981;
  }

  .loss {
    color: #ef4444;
  }

  .top-trends {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
    gap: 12px;
    margin-top: 12px;
  }

  .trend-item {
    background: rgba(255,255,255,0.05);
    padding: 12px;
    border-radius: 8px;
    text-align: center;
  }

  .trend-item .name {
    font-weight: 500;
    font-size: 0.9rem;
  }

  .trend-item .growth {
    color: #10b981;
    font-size: 0.8rem;
    margin-top: 4px;
  }

  .disclaimer {
    text-align: center;
    padding: 20px;
    color: #8892b0;
    font-size: 0.85rem;
  }

  footer {
    text-align: center;
    padding: 20px;
    color: #8892b0;
    font-size: 0.8rem;
  }

  .last-updated {
    text-align: center;
    color: #6b7280;
    font-size: 0.8rem;
    margin-top: 10px;
  }

  .captcha-container {
    display: flex;
    justify-content: center;
    margin: 20px 0;
  }
</style>
