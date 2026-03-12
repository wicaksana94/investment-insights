# 📊 Investment Insights

<p align="center">
  <a href="https://investment-insights-sveltekit.vercel.app">
    <img src="https://img.shields.io/badge/Visit-WebApp-6C63FF?style=for-the-badge&logo=vercel&logoColor=white" alt="Live Demo" />
  </a>
  <a href="https://github.com/wicaksana94/investment-insights/stargazers">
    <img src="https://img.shields.io/github/stars/wicaksana94/investment-insights?style=for-the-badge&color=gold" alt="Stars" />
  </a>
  <a href="https://github.com/wicaksana94/investment-insights/issues">
    <img src="https://img.shields.io/github/issues/wicaksana94/investment-insights?style=for-the-badge&color=green" alt="Issues" />
  </a>
  <a href="https://github.com/wicaksana94/investment-insights/blob/main/LICENSE">
    <img src="https://img.shields.io/github/license/wicaksana94/investment-insights?style=for-the-badge&color=blue" alt="License" />
  </a>
</p>

---

## ✨ Apa Itu Investment Insights?

**Investment Insights** adalah platform analisis tren investasi harian yang menggunakan data **Google Trends** untuk mengidentifikasi peluang investasi di pasar **US** dan **Indonesia**.

Platform ini memberikan:
- 📈 Analisis tren investasi real-time
- 🇺🇸🇮🇩 Dukungan pasar US dan Indonesia
- ⏰ Multiple timeframe (1 hari, 7 hari, 1 bulan, 6-12 bulan)
- 🎯 Rekomendasi aset dengan profil risiko (Safe, Medium, Aggressive)
- 📰 Link ke berita terkait setiap tren

---

## 🖥️ Tech Stack

| Kategori | Teknologi |
|----------|-----------|
| **Framework** | [SvelteKit](https://kit.svelte.dev/) |
| **Deployment** | [Vercel](https://vercel.com) |
| **Analytics** | [@vercel/analytics](https://vercel.com/analytics) |
| **Security** | [hCaptcha](https://www.hcaptcha.com/) |
| **Data Source** | Google Trends |
| **Automation** | GitHub Actions + OpenClaw Cron |

---

## 🚀 Fitur Utama

### 1. Analisis Multi-Region
Pilih antara pasar **US** atau **Indonesia** untuk melihat analisis yang sesuai dengan pasar lokal.

### 2. Multiple Timeframe
- ⚡ **1 Hari** (Very Short-term)
- 📅 **7 Hari** (Short-term)  
- 🗓️ **1 Bulan** (Medium-term)
- 📈 **6-12 Bulan** (Long-term)

### 3. Profil Risiko
Setiap rekomendasi dilengkapi profil risiko:
- 🟢 **Safe** - Risiko rendah, return stabil
- 🟡 **Medium** - Risiko sedang, return menengah
- 🔴 **Aggressive** - Risiko tinggi, return tinggi

### 4. SEO Optimized
- Meta tags lengkap
- Schema.org (Organization, FAQ)
- Sitemap XML
- robots.txt
- RSS Feed

### 5. Auto-Update Harian
Website diperbarui otomatis setiap jam 6 pagi WIB menggunakan GitHub Actions dan OpenClaw Cron.

---

## 📱 Preview

<p align="center">
  <img src="https://investment-insights-sveltekit.vercel.app/screenshot.png" alt="App Screenshot" width="100%" />
</p>

---

## 🛠️ Installation & Development

```bash
# Clone repository
git clone https://github.com/wicaksana94/investment-insights.git
cd investment-insights-sveltekit

# Install dependencies
npm install

# Development
npm run dev

# Build
npm run build
```

---

## 📂 Struktur Project

```
investment-insights-sveltekit/
├── src/
│   ├── lib/
│   │   └── data/
│   │       └── trends.json    # Data tren investasi
│   └── routes/
│       ├── +page.svelte      # Halaman utama
│       └── +layout.js        # Konfigurasi SvelteKit
├── static/
│   ├── robots.txt           # SEO
│   ├── sitemap.xml         # SEO
│   └── rss.xml             # RSS Feed
├── .github/
│   └── workflows/
│       └── daily-update.yml # Auto-update harian
├── svelte.config.js
├── vite.config.js
└── package.json
```

---

## 🤝 Kontribusi

Kontribusi sangat welcomed! Berikut cara kontribusi:

1. **Fork** repository ini
2. Buat **branch** baru (`git checkout -b feature/fitur-anda`)
3. **Commit** perubahan (`git commit -m 'Tambah fitur baru'`)
4. **Push** ke branch (`git push origin feature/fitur-anda`)
5. Buat **Pull Request**

---

## 📄 Lisensi

MIT License - lihat file [LICENSE](LICENSE) untuk detail.

---

## 🙏 Dukungan

Jika Anda menemukan project ini useful, dukungan Anda sangat berarti!

### 💖 Donasi via Saweria

Klik untuk donasi: [https://saweria.co/wicaksana94](https://saweria.co/wicaksana94)

<p align="center">
  <img src="https://saweria.co/widgets/qr?streamKey=80ea6ddcf71777f409051bf827faf7fc" alt="Saweria QR Code" width="200" />
</p>

---

## 📬 Kontak

- **Author**: [Arya](https://github.com/wicaksana94)
- **Website**: [investment-insights.vercel.app](https://investment-insights-sveltekit.vercel.app)
- **GitHub**: [@wicaksana94](https://github.com/wicaksana94)

---

<p align="center">
  <sub>Made with ❤️ by <a href="https://github.com/wicaksana94">Arya</a> • Updated: 13 Maret 2026</sub>
</p>
