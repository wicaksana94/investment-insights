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
  <title>Investment Insights - Analisis Tren Investasi US & Indonesia</title>
  <meta name="description" content="Dapatkan analisis investasi harian berdasarkan Google Trends. Temukan peluang investasi US dan Indonesia dengan estimasi kenaikan, penurunan, dan profil risiko (Safe, Medium, Aggressive)." />
  <meta name="keywords" content="investment insight, analisis investasi, google trends investasi, Saham US, Saham Indonesia, IHSG, crypto, emas, reksa dana" />
</svelte:head>

<main class="max-w-6xl mx-auto px-4 py-6">
  <!-- Header -->
  <header class="text-center py-8">
    <h1 class="text-4xl md:text-5xl font-bold bg-gradient-to-r from-cyan-400 to-purple-500 bg-clip-text text-transparent">
      Investment Insights
    </h1>
    <p class="text-gray-400 mt-3">Investment insight berdasarkan Google Trends data hari ini, {lastUpdated}</p>
    
    <div class="mt-5">
      <label for="region" class="text-gray-400 mr-3">Region:</label>
      <select id="region" bind:value={selectedRegion} class="px-4 py-2 rounded-lg bg-white/10 border border-white/20 text-white cursor-pointer">
        {#each regions as region}
          <option value={region}>{region === 'US' ? 'Amerika Serikat' : 'Indonesia'}</option>
        {/each}
      </select>
    </div>
    
    <p class="text-gray-500 text-sm mt-3">Updated: {lastUpdated}</p>
  </header>

  <!-- Top Trends -->
  <section class="bg-white/5 rounded-2xl p-6 mb-6 border border-white/10">
    <h2 class="text-xl text-cyan-400 mb-4">Top Trending di {selectedRegion === 'US' ? 'Amerika Serikat' : 'Indonesia'}</h2>
    <div class="grid grid-cols-2 md:grid-cols-4 gap-3">
      {#each topTrends[selectedRegion] || topTrends['US'] as item}
        <a href={item.url} target="_blank" rel="noopener noreferrer" class="bg-white/5 hover:bg-white/10 rounded-lg p-3 text-center transition">
          <div class="font-medium text-sm">{item.name}</div>
          <div class="text-green-400 text-xs mt-1">{item.growth}</div>
        </a>
      {/each}
    </div>
  </section>

  <!-- Very Short Term -->
  <section class="bg-white/5 rounded-2xl p-6 mb-6 border border-white/10">
    <h2 class="text-xl text-cyan-400 mb-4">1 Hari (Very Short-term)</h2>
    <div class="overflow-x-auto">
      <table class="w-full text-left text-sm">
        <thead>
          <tr class="border-b border-white/10">
            <th class="py-3 px-3 text-gray-400 font-medium">Tren</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Asset/Saham</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Opportunity</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Estimasi Kenaikan</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Estimasi Penurunan</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Profile</th>
          </tr>
        </thead>
        <tbody>
          {#each filteredInsights.veryShort.items as item}
            <tr class="border-b border-white/5">
              <td class="py-3 px-3"><a href={item.url || '#'} target="_blank" class="text-cyan-400 hover:underline">{item.trend}</a></td>
              <td class="py-3 px-3 text-yellow-400 font-semibold">{item.asset}</td>
              <td class="py-3 px-3">{item.opportunity}</td>
              <td class="py-3 px-3 text-green-400">{item.gain}</td>
              <td class="py-3 px-3 text-red-400">{item.loss}</td>
              <td class="py-3 px-3">
                <div class="flex gap-1">
                  {#each item.profiles || [] as profile}
                    <span class="text-xs px-2 py-0.5 rounded-full text-white" style="background-color: {getProfileLabel(profile).color}">
                      {getProfileLabel(profile).text}
                    </span>
                  {/each}
                </div>
              </td>
            </tr>
          {/each}
        </tbody>
      </table>
    </div>
  </section>

  <!-- Short Term -->
  <section class="bg-white/5 rounded-2xl p-6 mb-6 border border-white/10">
    <h2 class="text-xl text-cyan-400 mb-4">7 Hari (Short-term)</h2>
    <div class="overflow-x-auto">
      <table class="w-full text-left text-sm">
        <thead>
          <tr class="border-b border-white/10">
            <th class="py-3 px-3 text-gray-400 font-medium">Tren</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Asset/Saham</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Opportunity</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Estimasi Kenaikan</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Estimasi Penurunan</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Profile</th>
          </tr>
        </thead>
        <tbody>
          {#each filteredInsights.short.items as item}
            <tr class="border-b border-white/5">
              <td class="py-3 px-3"><a href={item.url || '#'} target="_blank" class="text-cyan-400 hover:underline">{item.trend}</a></td>
              <td class="py-3 px-3 text-yellow-400 font-semibold">{item.asset}</td>
              <td class="py-3 px-3">{item.opportunity}</td>
              <td class="py-3 px-3 text-green-400">{item.gain}</td>
              <td class="py-3 px-3 text-red-400">{item.loss}</td>
              <td class="py-3 px-3">
                <div class="flex gap-1">
                  {#each item.profiles || [] as profile}
                    <span class="text-xs px-2 py-0.5 rounded-full text-white" style="background-color: {getProfileLabel(profile).color}">
                      {getProfileLabel(profile).text}
                    </span>
                  {/each}
                </div>
              </td>
            </tr>
          {/each}
        </tbody>
      </table>
    </div>
  </section>

  <!-- Medium Term -->
  <section class="bg-white/5 rounded-2xl p-6 mb-6 border border-white/10">
    <h2 class="text-xl text-cyan-400 mb-4">1 Bulan</h2>
    <div class="overflow-x-auto">
      <table class="w-full text-left text-sm">
        <thead>
          <tr class="border-b border-white/10">
            <th class="py-3 px-3 text-gray-400 font-medium">Tren</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Asset/Saham</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Opportunity</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Estimasi Kenaikan</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Estimasi Penurunan</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Profile</th>
          </tr>
        </thead>
        <tbody>
          {#each filteredInsights.medium.items as item}
            <tr class="border-b border-white/5">
              <td class="py-3 px-3"><a href={item.url || '#'} target="_blank" class="text-cyan-400 hover:underline">{item.trend}</a></td>
              <td class="py-3 px-3 text-yellow-400 font-semibold">{item.asset}</td>
              <td class="py-3 px-3">{item.opportunity}</td>
              <td class="py-3 px-3 text-green-400">{item.gain}</td>
              <td class="py-3 px-3 text-red-400">{item.loss}</td>
              <td class="py-3 px-3">
                <div class="flex gap-1">
                  {#each item.profiles || [] as profile}
                    <span class="text-xs px-2 py-0.5 rounded-full text-white" style="background-color: {getProfileLabel(profile).color}">
                      {getProfileLabel(profile).text}
                    </span>
                  {/each}
                </div>
              </td>
            </tr>
          {/each}
        </tbody>
      </table>
    </div>
  </section>

  <!-- Long Term -->
  <section class="bg-white/5 rounded-2xl p-6 mb-6 border border-white/10">
    <h2 class="text-xl text-cyan-400 mb-4">6 Bulan - 1 Tahun</h2>
    <div class="overflow-x-auto">
      <table class="w-full text-left text-sm">
        <thead>
          <tr class="border-b border-white/10">
            <th class="py-3 px-3 text-gray-400 font-medium">Tren</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Asset/Saham</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Opportunity</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Estimasi Kenaikan</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Estimasi Penurunan</th>
            <th class="py-3 px-3 text-gray-400 font-medium">Profile</th>
          </tr>
        </thead>
        <tbody>
          {#each filteredInsights.long.items as item}
            <tr class="border-b border-white/5">
              <td class="py-3 px-3"><a href={item.url || '#'} target="_blank" class="text-cyan-400 hover:underline">{item.trend}</a></td>
              <td class="py-3 px-3 text-yellow-400 font-semibold">{item.asset}</td>
              <td class="py-3 px-3">{item.opportunity}</td>
              <td class="py-3 px-3 text-green-400">{item.gain}</td>
              <td class="py-3 px-3 text-red-400">{item.loss}</td>
              <td class="py-3 px-3">
                <div class="flex gap-1">
                  {#each item.profiles || [] as profile}
                    <span class="text-xs px-2 py-0.5 rounded-full text-white" style="background-color: {getProfileLabel(profile).color}">
                      {getProfileLabel(profile).text}
                    </span>
                  {/each}
                </div>
              </td>
            </tr>
          {/each}
        </tbody>
      </table>
    </div>
  </section>

  <!-- Legend -->
  <section class="bg-white/5 rounded-xl p-4 mb-6">
    <h3 class="text-gray-400 text-sm mb-3">Keterangan Profile Investasi:</h3>
    <div class="flex flex-wrap gap-4 text-sm text-gray-300">
      <span class="flex items-center gap-2"><span class="bg-green-500 text-white text-xs px-2 py-0.5 rounded-full">Safe</span> - Risiko rendah, return stabil</span>
      <span class="flex items-center gap-2"><span class="bg-amber-500 text-black text-xs px-2 py-0.5 rounded-full">Medium</span> - Risiko sedang, return menengah</span>
      <span class="flex items-center gap-2"><span class="bg-red-500 text-white text-xs px-2 py-0.5 rounded-full">Aggressive</span> - Risiko tinggi, return tinggi</span>
    </div>
  </section>

  <!-- hCaptcha -->
  <div class="flex justify-center my-5">
    <div class="h-captcha" data-sitekey="1fa43efa-6a1c-467a-b082-ad1a6ba0302a"></div>
  </div>

  <!-- Disclaimer -->
  <p class="text-center text-gray-400 text-sm py-4">
    Disclaimer: Ini berdasarkan Google Trends search patterns, BUKAN financial advice. 
    Lakukan riset sendiri sebelum investasi. Risiko rugi selalu ada.
  </p>

  <!-- Footer -->
  <footer class="text-center text-gray-500 text-sm py-4">
    <p>&copy; 2026 Investment Insights. All rights reserved.</p>
    <p>Generated by <a href="https://github.com/wicaksana94" target="_blank" class="text-cyan-400 hover:underline">Arya</a> - {lastUpdated}</p>
  </footer>

  <!-- Floating Donation -->
  <a href="https://saweria.co/wicaksana94" target="_blank" rel="noopener noreferrer" 
     class="fixed bottom-5 right-5 z-50 bg-gradient-to-br from-red-400 to-red-500 rounded-full w-12 h-12 flex items-center justify-center shadow-lg hover:scale-110 transition-transform"
     title="Donasi via Saweria">
    <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 text-white" fill="currentColor" viewBox="0 0 24 24">
      <path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/>
    </svg>
  </a>
</main>
