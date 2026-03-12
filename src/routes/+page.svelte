<script>
  import { onMount } from 'svelte';
  import { inject } from '@vercel/analytics';
  import trendsData from '$lib/data/trends.json';

  onMount(() => {
    inject();
  });

  let selectedRegion = trendsData.region || 'US';

  $: filteredInsights = {
    veryShort: {
      ...insights.veryShort,
      items: insights.veryShort.items.filter(item => item.region === selectedRegion)
    },
    short: {
      ...insights.short,
      items: insights.short.items.filter(item => item.region === selectedRegion)
    },
    medium: {
      ...insights.medium,
      items: insights.medium.items.filter(item => item.region === selectedRegion)
    },
    long: {
      ...insights.long,
      items: insights.long.items.filter(item => item.region === selectedRegion)
    }
  };

  const { lastUpdated, lastUpdatedTimestamp, regions, topTrends, insights } = trendsData;

  function formatTimestamp(isoString) {
    const date = new Date(isoString);
    return date.toLocaleString('id-ID', {
      day: 'numeric',
      month: 'long',
      year: 'numeric',
      hour: '2-digit',
      minute: '2-digit',
      timeZoneName: 'short'
    });
  }

  function getProfileLabel(profile) {
    const labels = {
      'safe': { text: 'Safe', color: '#10b981' },
      'medium': { text: 'Medium', color: '#f59e0b' },
      'aggressive': { text: 'Aggressive', color: '#ef4444' }
    };
    return labels[profile] || { text: profile, color: '#6b7280' };
  }

  function getTimeframeTooltip(timeframe) {
    const labels = {
      'veryShort': '1 hari',
      'short': '7 hari',
      'medium': '1 bulan',
      'long': '6-12 bulan'
    };
    return labels[timeframe] || timeframe;
  }
</script>

<svelte:head>
  <title>Investment Insights - Analisis Tren Investasi US & Indonesia</title>
  <meta name="description" content="Dapatkan analisis investasi harian berdasarkan Google Trends. Temukan peluang investasi US dan Indonesia dengan estimasi kenaikan, penurunan, dan profil risiko (Safe, Medium, Aggressive)." />
  <meta name="keywords" content="investment insight, analisis investasi, google trends investasi, Saham US, Saham Indonesia, IHSG, crypto, emas, reksa dana" />
</svelte:head>

<main class="container">
  <header>
    <h1>Investment Insights</h1>
    <p>Investment insight berdasarkan Google Trends data hari ini, {lastUpdated}</p>
    
    <div class="region-selector">
      <label for="region">Region:</label>
      <select id="region" bind:value={selectedRegion}>
        {#each regions as region}
          <option value={region}>{region === 'US' ? 'Amerika Serikat' : 'Indonesia'}</option>
        {/each}
      </select>
    </div>
    
    <div class="last-updated">Updated: {lastUpdated} pukul {formatTimestamp(lastUpdatedTimestamp).split('pukul')[1]?.trim() || ''} WIB</div>
  </header>

  <div class="card">
    <h2>Top Trending di {selectedRegion === 'US' ? 'Amerika Serikat' : 'Indonesia'}</h2>
    <div class="top-trends">
      {#each topTrends[selectedRegion] || topTrends['US'] as item}
        <a href={item.url} target="_blank" rel="noopener noreferrer" class="trend-item">
          <div class="name">{item.name}</div>
          <div class="growth">{item.growth}</div>
        </a>
      {/each}
    </div>
  </div>

  <div class="card">
    <h2>1 Hari (Very Short-term)</h2>
    <span class="timeframe very-short">{filteredInsights.veryShort.label}</span>
    <div class="table-scroll">
      <table>
        <tr>
          <th>Tren</th>
          <th>Asset/Saham</th>
          <th>Opportunity</th>
          <th title="Ini merupakan estimasi kenaikan dalam 1 hari">Estimasi Kenaikan</th>
          <th title="Ini merupakan estimasi penurunan dalam 1 hari">Estimasi Penurunan</th>
          <th>Profile</th>
        </tr>
        {#each filteredInsights.veryShort.items as item}
          <tr>
            <td><a href={item.url || '#'} target="_blank" rel="noopener noreferrer">{item.trend}</a></td>
            <td class="asset-name">{item.asset}</td>
            <td>{item.opportunity}</td>
            <td class="estimate gain">{item.gain}</td>
            <td class="estimate loss">{item.loss}</td>
            <td class="profiles">
              {#each item.profiles || [] as profile}
                <span class="profile-badge" style="background-color: {getProfileLabel(profile).color}">
                  {getProfileLabel(profile).text}
                </span>
              {/each}
            </td>
          </tr>
        {/each}
      </table>
    </div>
  </div>

  <div class="card">
    <h2>7 Hari (Short-term)</h2>
    <span class="timeframe short">{filteredInsights.short.label}</span>
    <div class="table-scroll">
      <table>
        <tr>
          <th>Tren</th>
          <th>Asset/Saham</th>
          <th>Opportunity</th>
          <th title="Ini merupakan estimasi kenaikan dalam 7 hari">Estimasi Kenaikan</th>
          <th title="Ini merupakan estimasi penurunan dalam 7 hari">Estimasi Penurunan</th>
          <th>Profile</th>
        </tr>
        {#each filteredInsights.short.items as item}
          <tr>
            <td><a href={item.url || '#'} target="_blank" rel="noopener noreferrer">{item.trend}</a></td>
            <td class="asset-name">{item.asset}</td>
            <td>{item.opportunity}</td>
            <td class="estimate gain">{item.gain}</td>
            <td class="estimate loss">{item.loss}</td>
            <td class="profiles">
              {#each item.profiles || [] as profile}
                <span class="profile-badge" style="background-color: {getProfileLabel(profile).color}">
                  {getProfileLabel(profile).text}
                </span>
              {/each}
            </td>
          </tr>
        {/each}
      </table>
    </div>
  </div>

  <div class="card">
    <h2>1 Bulan</h2>
    <span class="timeframe medium">{filteredInsights.medium.label}</span>
    <div class="table-scroll">
      <table>
        <tr>
          <th>Tren</th>
          <th>Asset/Saham</th>
          <th>Opportunity</th>
          <th title="Ini merupakan estimasi kenaikan dalam 1 bulan">Estimasi Kenaikan</th>
          <th title="Ini merupakan estimasi penurunan dalam 1 bulan">Estimasi Penurunan</th>
          <th>Profile</th>
        </tr>
        {#each filteredInsights.medium.items as item}
          <tr>
            <td><a href={item.url || '#'} target="_blank" rel="noopener noreferrer">{item.trend}</a></td>
            <td class="asset-name">{item.asset}</td>
            <td>{item.opportunity}</td>
            <td class="estimate gain">{item.gain}</td>
            <td class="estimate loss">{item.loss}</td>
            <td class="profiles">
              {#each item.profiles || [] as profile}
                <span class="profile-badge" style="background-color: {getProfileLabel(profile).color}">
                  {getProfileLabel(profile).text}
                </span>
              {/each}
            </td>
          </tr>
        {/each}
      </table>
    </div>
  </div>

  <div class="card">
    <h2>6 Bulan - 1 Tahun</h2>
    <span class="timeframe long">{filteredInsights.long.label}</span>
    <div class="table-scroll">
      <table>
        <tr>
          <th>Tren</th>
          <th>Asset/Saham</th>
          <th>Opportunity</th>
          <th title="Ini merupakan estimasi kenaikan dalam 6-12 bulan">Estimasi Kenaikan</th>
          <th title="Ini merupakan estimasi penurunan dalam 6-12 bulan">Estimasi Penurunan</th>
          <th>Profile</th>
        </tr>
        {#each filteredInsights.long.items as item}
          <tr>
            <td><a href={item.url || '#'} target="_blank" rel="noopener noreferrer">{item.trend}</a></td>
            <td class="asset-name">{item.asset}</td>
            <td>{item.opportunity}</td>
            <td class="estimate gain">{item.gain}</td>
            <td class="estimate loss">{item.loss}</td>
            <td class="profiles">
              {#each item.profiles || [] as profile}
                <span class="profile-badge" style="background-color: {getProfileLabel(profile).color}">
                  {getProfileLabel(profile).text}
                </span>
              {/each}
            </td>
          </tr>
        {/each}
      </table>
    </div>
  </div>

  <div class="profile-legend">
    <h3>Keterangan Profile Investasi:</h3>
    <div class="legend-items">
      <span class="profile-badge" style="background-color: #10b981">Safe</span> - Risiko rendah, return stabil
      <span class="profile-badge" style="background-color: #f59e0b">Medium</span> - Risiko sedang, return menengah
      <span class="profile-badge" style="background-color: #ef4444">Aggressive</span> - Risiko tinggi, return tinggi
    </div>
  </div>

  <div class="captcha-container">
    <div class="h-captcha" data-sitekey="1fa43efa-6a1c-467a-b082-ad1a6ba0302a"></div>
  </div>

  <div class="disclaimer">
    Disclaimer: Ini berdasarkan Google Trends search patterns, BUKAN financial advice. 
    Lakukan riset sendiri sebelum investasi. Risiko rugi selalu ada.
  </div>

  <footer>
    <p>&copy; 2026 Investment Insights. All rights reserved.</p>
    <p>Generated by <a href="https://github.com/wicaksana94" target="_blank" rel="noopener noreferrer">Arya</a> - {lastUpdated}</p>
  </footer>

  <div class="floating-donation">
    <a href="https://saweria.co/wicaksana94" target="_blank" rel="noopener noreferrer" title="Donasi via Saweria">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="donation-icon">
        <path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/>
      </svg>
    </a>
  </div>
</main>

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

  main.container {
    max-width: 1100px;
    margin: 0 auto;
  }

  header {
    text-align: center;
    padding: 40px 0 20px;
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

  .region-selector {
    margin: 20px 0;
  }

  .region-selector label {
    margin-right: 10px;
    color: #8892b0;
  }

  .region-selector select {
    padding: 8px 16px;
    font-size: 1rem;
    border-radius: 8px;
    border: 1px solid rgba(255,255,255,0.2);
    background: rgba(255,255,255,0.1);
    color: #fff;
    cursor: pointer;
  }

  .region-selector select option {
    background: #1a1a2e;
    color: #fff;
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

  .table-scroll {
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
    margin-top: 12px;
  }

  table {
    width: 100%;
    border-collapse: collapse;
    min-width: 600px;
  }

  th, td {
    text-align: left;
    padding: 12px 8px;
    border-bottom: 1px solid rgba(255,255,255,0.1);
  }

  th {
    color: #8892b0;
    font-weight: 500;
    font-size: 0.8rem;
    white-space: nowrap;
  }

  td {
    font-size: 0.9rem;
  }

  td:first-child a {
    color: #00d4ff;
    text-decoration: none;
    border-bottom: none;
  }

  td:first-child a:hover {
    text-decoration: underline;
  }

  .asset-name {
    color: #fbbf24 !important;
    font-weight: 600;
    white-space: nowrap;
  }

  .estimate {
    font-size: 0.85rem;
    white-space: nowrap;
  }

  .gain {
    color: #10b981;
  }

  .loss {
    color: #ef4444;
  }

  .profiles {
    display: flex;
    gap: 4px;
    flex-wrap: wrap;
  }

  .profile-badge {
    display: inline-block;
    padding: 2px 8px;
    border-radius: 12px;
    font-size: 0.7rem;
    font-weight: 600;
    color: #fff;
    text-transform: uppercase;
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
    text-decoration: none;
    color: inherit;
    display: block;
    transition: background 0.2s;
  }

  .trend-item:hover {
    background: rgba(255,255,255,0.1);
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

  footer a {
    color: #00d4ff;
    text-decoration: none;
  }

  footer a:hover {
    text-decoration: underline;
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

  .profile-legend {
    background: rgba(255,255,255,0.05);
    border-radius: 12px;
    padding: 16px;
    margin-bottom: 24px;
  }

  .profile-legend h3 {
    color: #8892b0;
    font-size: 0.9rem;
    margin-bottom: 12px;
  }

  .legend-items {
    display: flex;
    gap: 20px;
    flex-wrap: wrap;
    align-items: center;
    font-size: 0.85rem;
    color: #ccc;
  }

  .floating-donation {
    position: fixed;
    bottom: 20px;
    right: 20px;
    z-index: 1000;
  }

  .floating-donation a {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 60px;
    height: 60px;
    border-radius: 50%;
    background: linear-gradient(135deg, #FF6B6B, #FF8E8E);
    box-shadow: 0 4px 15px rgba(255, 107, 107, 0.4);
    transition: transform 0.3s, box-shadow 0.3s;
    text-decoration: none;
  }

  .floating-donation a:hover {
    transform: scale(1.1);
    box-shadow: 0 6px 20px rgba(255, 107, 107, 0.6);
  }

  .donation-icon {
    width: 30px;
    height: 30px;
    color: white;
  }

  /* Mobile Responsive */
  @media (max-width: 768px) {
    :global(body) {
      padding: 15px;
    }

    header {
      padding: 25px 0 15px;
    }

    header h1 {
      font-size: 1.8rem;
    }

    header p {
      font-size: 0.9rem;
    }

    .card {
      padding: 16px;
      margin-bottom: 16px;
      border-radius: 12px;
    }

    .card h2 {
      font-size: 1.1rem;
    }

    .top-trends {
      grid-template-columns: repeat(2, 1fr);
      gap: 8px;
    }

    .trend-item {
      padding: 10px;
    }

    .trend-item .name {
      font-size: 0.8rem;
    }

    .trend-item .growth {
      font-size: 0.7rem;
    }

    th, td {
      padding: 8px 6px;
      font-size: 0.75rem;
    }

    .asset-name {
      font-size: 0.75rem;
    }

    .estimate {
      font-size: 0.75rem;
    }

    .profile-badge {
      font-size: 0.6rem;
      padding: 2px 6px;
    }

    .region-selector select {
      font-size: 0.9rem;
      padding: 6px 12px;
    }

    .floating-donation {
      bottom: 12px;
      right: 12px;
    }

    .floating-donation a {
      width: 50px;
      height: 50px;
    }

    .legend-items {
      flex-direction: column;
      gap: 8px;
      align-items: flex-start;
    }

    .profile-legend {
      padding: 12px;
    }

    .captcha-container {
      transform: scale(0.85);
      transform-origin: center;
    }
  }

  @media (max-width: 480px) {
    :global(body) {
      padding: 10px;
    }

    header {
      padding: 20px 0 10px;
    }

    header h1 {
      font-size: 1.5rem;
    }

    .top-trends {
      grid-template-columns: 1fr;
    }

    th, td {
      padding: 6px 4px;
      font-size: 0.7rem;
    }

    .timeframe {
      font-size: 0.75rem;
      padding: 3px 8px;
    }
  }
</style>
