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
</script>

<svelte:head>
  <title>Investment Insights - Arya</title>
</svelte:head>

<div class="container">
  <header>
    <h1>Investment Insights</h1>
    <p>Google Trends Analysis - {lastUpdated}</p>
    
    <div class="region-selector">
      <label for="region">Region:</label>
      <select id="region" bind:value={selectedRegion}>
        {#each regions as region}
          <option value={region}>{region === 'US' ? 'Amerika Serikat' : 'Indonesia'}</option>
        {/each}
      </select>
    </div>
    
    <div class="last-updated">Updated: {lastUpdated} ({formatTimestamp(lastUpdatedTimestamp)})</div>
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
    <table>
      <tr>
        <th>Tren</th>
        <th>Asset/Saham</th>
        <th>Opportunity</th>
        <th>Estimasi Kenaikan</th>
        <th>Estimasi Penurunan</th>
        <th>Profile</th>
      </tr>
      {#each filteredInsights.veryShort.items as item}
        <tr>
          <td>{item.trend}</td>
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

  <div class="card">
    <h2>7 Hari (Short-term)</h2>
    <span class="timeframe short">{filteredInsights.short.label}</span>
    <table>
      <tr>
        <th>Tren</th>
        <th>Asset/Saham</th>
        <th>Opportunity</th>
        <th>Estimasi Kenaikan</th>
        <th>Estimasi Penurunan</th>
        <th>Profile</th>
      </tr>
      {#each filteredInsights.short.items as item}
        <tr>
          <td>{item.trend}</td>
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

  <div class="card">
    <h2>1 Bulan</h2>
    <span class="timeframe medium">{filteredInsights.medium.label}</span>
    <table>
      <tr>
        <th>Tren</th>
        <th>Asset/Saham</th>
        <th>Opportunity</th>
        <th>Estimasi Kenaikan</th>
        <th>Estimasi Penurunan</th>
        <th>Profile</th>
      </tr>
      {#each filteredInsights.medium.items as item}
        <tr>
          <td>{item.trend}</td>
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

  <div class="card">
    <h2>6 Bulan - 1 Tahun</h2>
    <span class="timeframe long">{filteredInsights.long.label}</span>
    <table>
      <tr>
        <th>Tren</th>
        <th>Asset/Saham</th>
        <th>Opportunity</th>
        <th>Estimasi Kenaikan</th>
        <th>Estimasi Penurunan</th>
        <th>Profile</th>
      </tr>
      {#each filteredInsights.long.items as item}
        <tr>
          <td>{item.trend}</td>
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

  <div class="profile-legend">
    <h3>Legend Profile Investasi:</h3>
    <div class="legend-items">
      <span class="profile-badge" style="background-color: #10b981">Safe</span> - Risiko rendah, return stabil
      <span class="profile-badge" style="background-color: #f59e0b">Medium</span> - Risiko sedang, return menengah
      <span class="profile-badge" style="background-color: #ef4444">Aggressive</span> - Risiko tinggi, return tinggi
    </div>
  </div>

  <div class="captcha-container">
    <div class="g-recaptcha" data-sitekey="6LeIxAcTAAAAAJcZVRqyHh71UMIEGNQ_MXjiZKhI"></div>
  </div>

  <div class="disclaimer">
    Disclaimer: Ini berdasarkan Google Trends search patterns, BUKAN financial advice. 
    Lakukan riset sendiri sebelum investasi. Risiko rugi selalu ada.
  </div>

  <footer>
    Generated by Arya - {lastUpdated}
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
</style>
