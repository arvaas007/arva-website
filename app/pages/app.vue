<script setup lang="ts">
useHead({
  title: 'App Dashboard — ARVA-AS',
  meta: [
    { name: 'description', content: 'Dashboard aplikasi dan website digital buatan Arva Athallah Susanto. Eksplorasi ekosistem karya digital dari Arverse, Podge, Game Zeta, dan lainnya.' }
  ]
})

onMounted(() => {
  const animatedEls = document.querySelectorAll('[data-animate]')
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('is-visible')
          observer.unobserve(entry.target)
        }
      })
    },
    { threshold: 0.1 }
  )
  animatedEls.forEach((el) => observer.observe(el))
})

const apps = [
  {
    id: 'arverse',
    number: '01',
    emoji: '🌌',
    label: 'Qur\'an App',
    name: 'Arverse',
    fullName: 'Augmented Reality Quranic Verse',
    tagline: 'Digital Qur\'an with Gamification',
    description: 'Aplikasi Qur\'an digital dengan fitur gamifikasi setor murojaah harian. Kartu dipilih secara acak dan menampilkan ayat tujuan secara interaktif.',
    url: 'https://arverse.vercel.app/',
    internalRoute: '/arverse',
    color: '#3b82f6',
    colorDark: '#1d4ed8',
    featured: true,
    tags: ['Quran', 'Gamification', 'Daily Habit'],
  },
  {
    id: 'podge',
    number: '02',
    emoji: '🧩',
    label: 'Ecosystem',
    name: 'Podge',
    fullName: 'Podge-Ecosystem',
    tagline: 'Centralized App Portal',
    description: 'Portal aplikasi digital Arva — menyediakan akses terpusat ke berbagai layanan dan platform ekosistem Podge.',
    url: 'https://podge-ecosystem.vercel.app',
    internalRoute: '/podge',
    color: '#8b5cf6',
    colorDark: '#6d28d9',
    featured: false,
    tags: ['Portal', 'Ecosystem', 'Multi-platform'],
  },
  {
    id: 'gmae',
    number: '03',
    emoji: '⚙️',
    label: 'Algorithm',
    name: 'GMAE',
    fullName: 'General Model Algorithmic Equilibrium',
    tagline: 'Algorithmic Equilibrium Model',
    description: 'Proyek model algoritmik berbasis web buatan Arva — eksplorasi keseimbangan sistem, logika komputasional, dan pengembangan model digital.',
    url: 'https://gmae-zeta.vercel.app',
    internalRoute: null,
    color: '#10b981',
    colorDark: '#059669',
    featured: false,
    tags: ['Algorithm', 'Model', 'Equilibrium'],
  },
  {
    id: 'kopdes-ai-backend',
    number: '04',
    emoji: '🤖',
    label: 'Backend API',
    name: 'Kopdes AI Backend',
    fullName: 'Kopdes AI Backend Server',
    tagline: 'Backend API for Kopdes AI',
    description: 'Layanan backend API berbasis Express dan Supabase untuk mendukung operasional kecerdasan buatan (AI) pada aplikasi Kopdes.',
    url: 'https://www.arva-as.my.id/kopdes-ai-backend',
    internalRoute: null,
    color: '#ec4899',
    colorDark: '#be185d',
    featured: false,
    tags: ['Backend', 'API', 'AI', 'Express', 'Supabase'],
  },
  {
    id: 'aksa-brin',
    number: '05',
    emoji: '💼',
    label: 'Finance & Research',
    name: 'Aksa BRIN',
    fullName: 'AKSARA — Aplikasi Keuangan Syariah',
    tagline: 'Islamic Financial App & Research',
    description: 'Aplikasi Keuangan Syariah (AKSARA) hasil riset kolaborasi, dikembangkan untuk membantu pencatatan keuangan dan manajemen transaksi secara syariah.',
    url: 'https://www.arva-as.my.id/aksa-brin',
    internalRoute: null,
    color: '#f59e0b',
    colorDark: '#b45309',
    featured: false,
    tags: ['Finance', 'Research', 'Sharia', 'BRIN'],
  },
  {
    id: 'edutwin-lms',
    number: '06',
    emoji: '🎓',
    label: 'Education Platform',
    name: 'Edutwin LMS',
    fullName: 'Edutwin Learning Management System',
    tagline: 'Interactive Learning Platform',
    description: 'Sistem manajemen pembelajaran digital interaktif yang dirancang untuk mendukung kolaborasi akademis dan proses belajar-mengajar modern.',
    url: 'https://www.arva-as.my.id/edutwin-lms',
    internalRoute: null,
    color: '#0284c7',
    colorDark: '#0369a1',
    featured: false,
    tags: ['LMS', 'Education', 'Interactive', 'Nuxt'],
  },
  {
    id: 'agavera-labs',
    number: '07',
    emoji: '🧪',
    label: 'Research Lab',
    name: 'Agavera Labs',
    fullName: 'Agavera Labs Studio',
    tagline: 'Research & Innovation Studio',
    description: 'Laboratorium riset dan inkubasi teknologi digital untuk eksplorasi AI, web terdistribusi, dan ekosistem komputasi canggih.',
    url: 'https://www.arva-as.my.id/agavera-labs',
    internalRoute: null,
    color: '#6366f1',
    colorDark: '#4f46e5',
    featured: false,
    tags: ['Research', 'AI', 'Innovation', 'Vercel'],
  },
  {
    id: 'vij-journal',
    number: '08',
    emoji: '📓',
    label: 'Academic Journal',
    name: 'VIJ Journal',
    fullName: 'VIJ Journal Platform',
    tagline: 'Academic & Research Journal',
    description: 'Platform jurnal akademik digital untuk publikasi riset, artikel ilmiah, dan dokumentasi kajian akademis secara terstruktur.',
    url: 'https://www.arva-as.my.id/vij-journal',
    internalRoute: null,
    color: '#14b8a6',
    colorDark: '#0f766e',
    featured: false,
    tags: ['Journal', 'Academic', 'Publication', 'Research'],
  },
  {
    id: 'baznas-portfolio',
    number: '09',
    emoji: '🏛️',
    label: 'ZISWAF Portfolio',
    name: 'BAZNAS Portfolio',
    fullName: 'Portofolio Riset & Transformasi Digital BAZNAS',
    tagline: 'ZISWAF, Blockchain & Empirical Research',
    description: 'Dokumentasi riset empiris, publikasi IJAZ BAZNAS, pemodelan ekonometrika zakat makro, dan integrasi blockchain dalam pengelolaan zakat nasional.',
    url: 'https://www.arva-as.my.id/portfolio-baznas',
    internalRoute: '/portfolio-baznas',
    color: '#059669',
    colorDark: '#047857',
    featured: true,
    tags: ['BAZNAS', 'IJAZ', 'Blockchain', 'ZISWAF', 'Economics'],
  },
]

// Ticker items — duplicated for infinite loop
const tickerItems = [
  { abbr: 'ARVERSE', full: 'Augmented Reality Quranic Verse', emoji: '🌌', color: '#3b82f6', url: 'https://arverse.vercel.app/' },
  { abbr: 'PODGE', full: 'Podge-Ecosystem', emoji: '🧩', color: '#8b5cf6', url: 'https://podge-ecosystem.vercel.app' },
  { abbr: 'BAZNAS RISIL', full: 'Portofolio Riset BAZNAS & IJAZ', emoji: '🏛️', color: '#059669', url: 'https://www.arva-as.my.id/portfolio-baznas' },
  { abbr: 'GMAE', full: 'General Model Algorithmic Equilibrium', emoji: '⚙️', color: '#10b981', url: 'https://gmae-zeta.vercel.app' },
  { abbr: 'KOPDES API', full: 'Kopdes AI Backend Server', emoji: '🤖', color: '#ec4899', url: 'https://www.arva-as.my.id/kopdes-ai-backend' },
  { abbr: 'AKSA BRIN', full: 'AKSARA Keuangan Syariah', emoji: '💼', color: '#f59e0b', url: 'https://www.arva-as.my.id/aksa-brin' },
  { abbr: 'EDUTWIN LMS', full: 'Edutwin Learning Management System', emoji: '🎓', color: '#0284c7', url: 'https://www.arva-as.my.id/edutwin-lms' },
  { abbr: 'AGAVERA LABS', full: 'Agavera Labs Studio', emoji: '🧪', color: '#6366f1', url: 'https://www.arva-as.my.id/agavera-labs' },
  { abbr: 'VIJ JOURNAL', full: 'VIJ Journal Platform', emoji: '📓', color: '#14b8a6', url: 'https://www.arva-as.my.id/vij-journal' },
  { abbr: 'ARVERSE', full: 'Augmented Reality Quranic Verse', emoji: '🌌', color: '#3b82f6', url: 'https://arverse.vercel.app/' },
  { abbr: 'PODGE', full: 'Podge-Ecosystem', emoji: '🧩', color: '#8b5cf6', url: 'https://podge-ecosystem.vercel.app' },
  { abbr: 'BAZNAS RISIL', full: 'Portofolio Riset BAZNAS & IJAZ', emoji: '🏛️', color: '#059669', url: 'https://www.arva-as.my.id/portfolio-baznas' },
  { abbr: 'GMAE', full: 'General Model Algorithmic Equilibrium', emoji: '⚙️', color: '#10b981', url: 'https://gmae-zeta.vercel.app' },
  { abbr: 'KOPDES API', full: 'Kopdes AI Backend Server', emoji: '🤖', color: '#ec4899', url: 'https://www.arva-as.my.id/kopdes-ai-backend' },
  { abbr: 'AKSA BRIN', full: 'AKSARA Keuangan Syariah', emoji: '💼', color: '#f59e0b', url: 'https://www.arva-as.my.id/aksa-brin' },
  { abbr: 'EDUTWIN LMS', full: 'Edutwin Learning Management System', emoji: '🎓', color: '#0284c7', url: 'https://www.arva-as.my.id/edutwin-lms' },
  { abbr: 'AGAVERA LABS', full: 'Agavera Labs Studio', emoji: '🧪', color: '#6366f1', url: 'https://www.arva-as.my.id/agavera-labs' },
  { abbr: 'VIJ JOURNAL', full: 'VIJ Journal Platform', emoji: '📓', color: '#14b8a6', url: 'https://www.arva-as.my.id/vij-journal' },
]
</script>

<template>
  <div class="app-dashboard">
    <!-- Hero Header -->
    <section class="app-dashboard-hero">
      <div class="app-hero-bg">
        <div class="app-hero-orb orb-1"></div>
        <div class="app-hero-orb orb-2"></div>
        <div class="app-hero-orb orb-3"></div>
      </div>
      <div class="app-hero-inner">
        <p class="arva-kicker">Digital Works</p>
        <h1 class="app-hero-title">App Dashboard</h1>
        <p class="app-hero-subtitle">
          Koleksi aplikasi &amp; website digital buatan<br />
          <strong>Arva Athallah Susanto</strong>
        </p>
        <div class="app-hero-meta">
          <span class="app-meta-badge">{{ apps.length }} Projects</span>
          <span class="app-meta-badge">Live &amp; Active</span>
        </div>
      </div>
    </section>

    <!-- ── LIVE TICKER / MARQUEE ────────────── -->
    <div class="ticker-wrapper">
      <div class="ticker-label">LIVE PROJECTS</div>
      <div class="ticker-track-outer">
        <div class="ticker-track">
          <a
            v-for="(item, i) in tickerItems"
            :key="`tick-${i}`"
            :href="item.url"
            target="_blank"
            rel="noopener"
            class="ticker-item"
            :style="`--tc: ${item.color}`"
          >
            <span class="ticker-dot" :style="`background: ${item.color}`"></span>
            <span class="ticker-abbr">{{ item.abbr }}</span>
            <span class="ticker-sep">—</span>
            <span class="ticker-full">{{ item.full }}</span>
            <span class="ticker-emoji">{{ item.emoji }}</span>
            <span class="ticker-divider">◆</span>
          </a>
        </div>
      </div>
    </div>

    <!-- ── WEB3 PROJECT SHOWCASE ─────────────── -->
    <section class="showcase-section">
      <div class="showcase-header" data-animate="fade-up">
        <p class="arva-kicker">Digital Portfolio</p>
        <h2 class="showcase-title">{{ apps.length }} Active Projects</h2>
        <p class="showcase-sub">Semua platform berjalan live dan terus dikembangkan.</p>
      </div>

      <div class="showcase-grid">
        <a
          v-for="(item, i) in tickerItems.slice(0, 8)"
          :key="item.abbr + i"
          :href="item.url"
          target="_blank"
          rel="noopener"
          class="showcase-card"
          :style="`--sc: ${item.color}; --delay: ${i * 120}ms`"
          data-animate="fade-up"
        >
          <div class="sc-top">
            <div class="sc-logo" :style="`background: linear-gradient(135deg, ${item.color}22, ${item.color}44); border-color: ${item.color}55`">
              <span class="sc-emoji">{{ item.emoji }}</span>
            </div>
            <div class="sc-live">
              <span class="sc-live-dot"></span>
              LIVE
            </div>
          </div>
          <div class="sc-body">
            <h3 class="sc-abbr" :style="`color: ${item.color}`">{{ item.abbr }}</h3>
            <p class="sc-full">{{ item.full }}</p>
          </div>
          <div class="sc-footer">
            <span class="sc-link">Visit →</span>
            <span class="sc-url">{{ item.url.replace('https://', '') }}</span>
          </div>
          <div class="sc-glow" :style="`background: radial-gradient(circle at 0% 0%, ${item.color}18, transparent 70%)`"></div>
        </a>
      </div>
    </section>

    <!-- App Grid (full detail cards) -->
    <section class="app-grid-section">
      <div class="section-heading-center" data-animate="fade-up">
        <p class="arva-kicker">Deep Dive</p>
        <h2>Detail Setiap Aplikasi</h2>
      </div>
      <div class="app-grid">
        <article
          v-for="(app, i) in apps"
          :key="app.id"
          class="app-card"
          :class="{ 'app-card--featured': app.featured }"
          :style="`--app-color: ${app.color}; --app-color-dark: ${app.colorDark}; --delay: ${i * 100}ms`"
          data-animate="fade-up"
        >
          <!-- Card Top -->
          <div class="app-card-top">
            <div class="app-icon-wrap">
              <span class="app-icon">{{ app.emoji }}</span>
            </div>
            <div class="app-card-meta">
              <span class="app-number">{{ app.number }}</span>
              <span class="app-label-badge">{{ app.label }}</span>
            </div>
          </div>

          <!-- Card Body -->
          <div class="app-card-body">
            <h2 class="app-name">{{ app.name }}</h2>
            <p class="app-fullname">{{ app.fullName }}</p>
            <p class="app-tagline">{{ app.tagline }}</p>
            <p class="app-desc">{{ app.description }}</p>

            <!-- Tags -->
            <div class="app-tags">
              <span v-for="tag in app.tags" :key="tag" class="app-tag">{{ tag }}</span>
            </div>
          </div>

          <!-- Card Footer -->
          <div class="app-card-footer">
            <a
              :href="app.url"
              target="_blank"
              rel="noopener noreferrer"
              class="app-open-btn"
            >
              <span>Open {{ app.name }}</span>
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
                <path d="M18 13v6a2 2 0 01-2 2H5a2 2 0 01-2-2V8a2 2 0 012-2h6"/>
                <polyline points="15,3 21,3 21,9"/>
                <line x1="10" y1="14" x2="21" y2="3"/>
              </svg>
            </a>
            <NuxtLink
              v-if="app.internalRoute"
              :to="app.internalRoute"
              class="app-internal-link"
            >
              Info →
            </NuxtLink>
          </div>

          <!-- Decorative glow -->
          <div class="app-card-glow"></div>
        </article>
      </div>
    </section>

    <!-- Footer CTA -->
    <section class="app-cta-section">
      <div class="app-cta-inner">
        <p class="arva-kicker">More Coming Soon</p>
        <h2>Ekosistem digital yang terus berkembang.</h2>
        <p>Setiap aplikasi mencerminkan eksplorasi dan pertumbuhan Arva dalam pengembangan digital, riset, dan identitas akademik.</p>
        <NuxtLink to="/portfolio" class="arva-btn primary">View Full Portfolio →</NuxtLink>
      </div>
    </section>
  </div>
</template>

<style scoped>
/* ── LAYOUT ─────────────────────────────── */
.app-dashboard {
  min-height: 100vh;
  background: #f8fafc;
  font-family: 'Inter', system-ui, sans-serif;
}

/* ── HERO ───────────────────────────────── */
.app-dashboard-hero {
  position: relative;
  background: #0f172a;
  overflow: hidden;
  padding: 100px 24px 80px;
  text-align: center;
}

.app-hero-bg {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.app-hero-orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0.25;
}

.orb-1 {
  width: 400px;
  height: 400px;
  background: #3b82f6;
  top: -100px;
  left: -80px;
}

.orb-2 {
  width: 300px;
  height: 300px;
  background: #8b5cf6;
  bottom: -60px;
  right: -40px;
}

.orb-3 {
  width: 200px;
  height: 200px;
  background: #10b981;
  top: 40%;
  left: 50%;
  transform: translateX(-50%);
}

.app-hero-inner {
  position: relative;
  z-index: 2;
  max-width: 700px;
  margin: 0 auto;
}

.app-hero-title {
  margin: 12px 0 0;
  font-family: Georgia, 'Times New Roman', serif;
  font-size: clamp(48px, 8vw, 96px);
  letter-spacing: -0.06em;
  line-height: 0.95;
  color: #ffffff;
}

.app-hero-subtitle {
  margin: 20px 0 0;
  color: #94a3b8;
  font-size: 17px;
  line-height: 1.6;
}

.app-hero-subtitle strong {
  color: #e2e8f0;
}

.app-hero-meta {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  margin-top: 28px;
}

.app-meta-badge {
  display: inline-flex;
  align-items: center;
  padding: 6px 16px;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.07);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: #94a3b8;
  font-size: 13px;
  font-weight: 600;
  letter-spacing: 0.02em;
}

/* ── TICKER / MARQUEE ───────────────────── */
.ticker-wrapper {
  position: relative;
  background: #ffffff;
  border-bottom: 1px solid #e2e8f0;
  display: flex;
  align-items: center;
  height: 52px;
  overflow: hidden;
}

.ticker-label {
  flex-shrink: 0;
  padding: 0 20px;
  font-size: 10px;
  font-weight: 900;
  letter-spacing: 0.15em;
  color: #0f172a;
  background: #0f172a;
  color: #ffffff;
  height: 100%;
  display: flex;
  align-items: center;
  z-index: 2;
  white-space: nowrap;
}

.ticker-track-outer {
  flex: 1;
  overflow: hidden;
  mask-image: linear-gradient(90deg, transparent 0%, #000 5%, #000 95%, transparent 100%);
  -webkit-mask-image: linear-gradient(90deg, transparent 0%, #000 5%, #000 95%, transparent 100%);
}

.ticker-track {
  display: flex;
  align-items: center;
  gap: 0;
  animation: ticker-scroll 18s linear infinite;
  width: max-content;
}

.ticker-item {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 0 28px;
  text-decoration: none;
  transition: background 0.2s ease;
  height: 52px;
  cursor: pointer;
}

.ticker-item:hover {
  background: #f8fafc;
}

.ticker-dot {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  flex-shrink: 0;
  animation: pulse-dot 2s ease-in-out infinite;
}

.ticker-abbr {
  font-size: 13px;
  font-weight: 900;
  color: var(--tc);
  letter-spacing: 0.06em;
}

.ticker-sep {
  color: #cbd5e1;
  font-size: 12px;
}

.ticker-full {
  font-size: 12px;
  font-weight: 500;
  color: #64748b;
  white-space: nowrap;
}

.ticker-emoji {
  font-size: 14px;
}

.ticker-divider {
  color: #e2e8f0;
  font-size: 8px;
  margin-left: 10px;
}

@keyframes ticker-scroll {
  0%   { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}

@keyframes pulse-dot {
  0%, 100% { opacity: 1; transform: scale(1); }
  50%       { opacity: 0.5; transform: scale(1.4); }
}

/* ── WEB3 SHOWCASE ──────────────────────── */
.showcase-section {
  background: #ffffff;
  padding: 72px 24px 80px;
  border-bottom: 1px solid #e2e8f0;
}

.showcase-header {
  text-align: center;
  max-width: 600px;
  margin: 0 auto 48px;
}

.showcase-title {
  margin: 8px 0 0;
  font-family: Georgia, serif;
  font-size: clamp(36px, 5vw, 60px);
  letter-spacing: -0.05em;
  color: #0f172a;
  line-height: 1;
}

.showcase-sub {
  margin: 12px 0 0;
  color: #64748b;
  font-size: 15px;
}

.showcase-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  max-width: 1100px;
  margin: 0 auto;
}

.showcase-card {
  position: relative;
  background: #ffffff;
  border: 1.5px solid #e2e8f0;
  border-radius: 24px;
  padding: 28px;
  display: flex;
  flex-direction: column;
  gap: 16px;
  text-decoration: none;
  overflow: hidden;
  transition: transform 0.3s cubic-bezier(0.16, 1, 0.3, 1),
              box-shadow 0.3s cubic-bezier(0.16, 1, 0.3, 1),
              border-color 0.3s ease;
  box-shadow: 0 2px 16px rgba(15, 23, 42, 0.05);
  transition-delay: var(--delay, 0ms);
}

.showcase-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 20px 56px rgba(15, 23, 42, 0.12);
  border-color: var(--sc);
}

.sc-glow {
  position: absolute;
  inset: 0;
  border-radius: 24px;
  pointer-events: none;
  opacity: 0;
  transition: opacity 0.4s ease;
}

.showcase-card:hover .sc-glow {
  opacity: 1;
}

.sc-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.sc-logo {
  width: 52px;
  height: 52px;
  border-radius: 14px;
  border: 1.5px solid;
  display: grid;
  place-items: center;
}

.sc-emoji {
  font-size: 22px;
}

.sc-live {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 4px 12px;
  border-radius: 999px;
  background: #dcfce7;
  color: #16a34a;
  font-size: 10px;
  font-weight: 900;
  letter-spacing: 0.08em;
}

.sc-live-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #16a34a;
  animation: pulse-dot 1.5s ease-in-out infinite;
}

.sc-body {
  flex: 1;
}

.sc-abbr {
  margin: 0;
  font-size: 22px;
  font-weight: 900;
  letter-spacing: -0.02em;
  line-height: 1;
}

.sc-full {
  margin: 6px 0 0;
  font-size: 12px;
  color: #94a3b8;
  line-height: 1.5;
  font-weight: 500;
}

.sc-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-top: 14px;
  border-top: 1px solid #f1f5f9;
}

.sc-link {
  font-size: 12px;
  font-weight: 700;
  color: var(--sc);
}

.sc-url {
  font-size: 10px;
  color: #cbd5e1;
  font-family: monospace;
}

/* ── GRID ───────────────────────────────── */
.app-grid-section {
  max-width: 1200px;
  margin: 0 auto;
  padding: 64px 24px 80px;
}

.section-heading-center {
  text-align: center;
  max-width: 600px;
  margin: 0 auto 48px;
}

.section-heading-center h2 {
  margin: 8px 0 0;
  font-family: Georgia, serif;
  font-size: clamp(32px, 4vw, 52px);
  letter-spacing: -0.05em;
  color: #0f172a;
}

.app-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}

/* ── CARD ───────────────────────────────── */
.app-card {
  position: relative;
  background: #ffffff;
  border: 1px solid #e2e8f0;
  border-radius: 28px;
  padding: 32px;
  display: flex;
  flex-direction: column;
  gap: 20px;
  overflow: hidden;
  transition: transform 0.35s cubic-bezier(0.16, 1, 0.3, 1),
              box-shadow 0.35s cubic-bezier(0.16, 1, 0.3, 1),
              border-color 0.3s ease;
  box-shadow: 0 4px 24px rgba(15, 23, 42, 0.06);
}

.app-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 24px 64px rgba(15, 23, 42, 0.14);
  border-color: var(--app-color);
}

.app-card:hover .app-card-glow {
  opacity: 1;
}

.app-card--featured {
  background: #0f172a;
  border-color: rgba(255, 255, 255, 0.08);
}

.app-card--featured:hover {
  border-color: var(--app-color);
}

.app-card-glow {
  position: absolute;
  inset: 0;
  border-radius: 28px;
  background: radial-gradient(circle at top left, var(--app-color), transparent 60%);
  opacity: 0;
  transition: opacity 0.4s ease;
  pointer-events: none;
  mix-blend-mode: soft-light;
}

/* ── CARD TOP ───────────────────────────── */
.app-card-top {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
}

.app-icon-wrap {
  width: 56px;
  height: 56px;
  border-radius: 16px;
  display: grid;
  place-items: center;
  background: linear-gradient(135deg, var(--app-color), var(--app-color-dark));
  box-shadow: 0 8px 24px -4px color-mix(in srgb, var(--app-color) 40%, transparent);
}

.app-icon {
  font-size: 26px;
  line-height: 1;
}

.app-card-meta {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 6px;
}

.app-number {
  font-size: 28px;
  font-family: Georgia, serif;
  font-weight: 700;
  letter-spacing: -0.04em;
  color: #cbd5e1;
  line-height: 1;
}

.app-card--featured .app-number {
  color: rgba(255, 255, 255, 0.2);
}

.app-label-badge {
  display: inline-flex;
  padding: 4px 10px;
  border-radius: 999px;
  background: color-mix(in srgb, var(--app-color) 12%, transparent);
  color: var(--app-color);
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 0.04em;
  text-transform: uppercase;
}

.app-card--featured .app-label-badge {
  background: color-mix(in srgb, var(--app-color) 20%, transparent);
}

/* ── CARD BODY ──────────────────────────── */
.app-card-body {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.app-name {
  margin: 0;
  font-size: 26px;
  letter-spacing: -0.04em;
  color: #0f172a;
  font-family: Georgia, serif;
}

.app-card--featured .app-name {
  color: #f8fafc;
}

.app-fullname {
  margin: 0;
  font-size: 11px;
  font-weight: 600;
  color: #94a3b8;
  letter-spacing: 0.02em;
}

.app-card--featured .app-fullname {
  color: #475569;
}

.app-tagline {
  margin: 4px 0 0;
  font-size: 13px;
  font-weight: 600;
  color: var(--app-color);
  text-transform: uppercase;
  letter-spacing: 0.06em;
}

.app-desc {
  margin: 6px 0 0;
  color: #64748b;
  font-size: 14px;
  line-height: 1.7;
}

.app-card--featured .app-desc {
  color: #94a3b8;
}

.app-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-top: 10px;
}

.app-tag {
  padding: 3px 10px;
  border-radius: 999px;
  background: #f1f5f9;
  color: #475569;
  font-size: 11px;
  font-weight: 600;
}

.app-card--featured .app-tag {
  background: rgba(255, 255, 255, 0.07);
  color: #94a3b8;
}

/* ── CARD FOOTER ────────────────────────── */
.app-card-footer {
  display: flex;
  align-items: center;
  gap: 16px;
  padding-top: 16px;
  border-top: 1px solid #f1f5f9;
}

.app-card--featured .app-card-footer {
  border-top-color: rgba(255, 255, 255, 0.07);
}

.app-open-btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 10px 20px;
  border-radius: 12px;
  background: linear-gradient(135deg, var(--app-color), var(--app-color-dark));
  color: #ffffff;
  text-decoration: none;
  font-size: 13px;
  font-weight: 700;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  box-shadow: 0 4px 16px -4px color-mix(in srgb, var(--app-color) 60%, transparent);
}

.app-open-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 24px -4px color-mix(in srgb, var(--app-color) 70%, transparent);
}

.app-internal-link {
  color: #94a3b8;
  font-size: 13px;
  font-weight: 600;
  text-decoration: none;
  transition: color 0.2s ease;
}

.app-internal-link:hover {
  color: var(--app-color);
}

/* ── CTA SECTION ────────────────────────── */
.app-cta-section {
  background: #0f172a;
  padding: 100px 24px;
  text-align: center;
}

.app-cta-inner {
  max-width: 640px;
  margin: 0 auto;
}

.app-cta-inner h2 {
  margin: 12px 0 0;
  font-family: Georgia, serif;
  font-size: clamp(32px, 5vw, 52px);
  letter-spacing: -0.05em;
  line-height: 1.1;
  color: #f8fafc;
}

.app-cta-inner p {
  margin: 16px 0 32px;
  color: #64748b;
  font-size: 16px;
  line-height: 1.75;
}

/* ── SCROLL ANIMATIONS ──────────────────── */
[data-animate="fade-up"] {
  opacity: 0;
  transform: translateY(40px);
  transition: opacity 0.6s cubic-bezier(0.16, 1, 0.3, 1),
              transform 0.6s cubic-bezier(0.16, 1, 0.3, 1);
  transition-delay: var(--delay, 0ms);
}

[data-animate="fade-up"].is-visible {
  opacity: 1;
  transform: translateY(0);
}

/* ── RESPONSIVE ─────────────────────────── */
@media (max-width: 900px) {
  .app-grid,
  .showcase-grid {
    grid-template-columns: 1fr;
  }

  .app-dashboard-hero {
    padding: 80px 20px 60px;
  }
}

@media (max-width: 600px) {
  .app-card {
    padding: 24px 20px;
  }

  .app-icon-wrap {
    width: 48px;
    height: 48px;
  }

  .app-name {
    font-size: 22px;
  }

  .ticker-full {
    display: none;
  }
}
</style>
