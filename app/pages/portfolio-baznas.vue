<script setup lang="ts">
import { ref, computed } from 'vue'

useHead({
  title: 'Portofolio BAZNAS & Riset ZISWAF — Arva Athallah Susanto',
  meta: [
    {
      name: 'description',
      content: 'Dokumentasi riset empiris, publikasi International Journal of Zakat (IJAZ) BAZNAS, transformasi digital OPZ, dan implementasi blockchain dalam pengelolaan zakat nasional oleh Arva Athallah Susanto.'
    },
    {
      name: 'keywords',
      content: 'BAZNAS, Badan Amil Zakat Nasional, IJAZ, Zakat Blockchain, Islamic Social Finance, Arva Athallah Susanto, ZISWAF, OPZ, Fintech Zakat'
    },
    {
      property: 'og:title',
      content: 'Portofolio BAZNAS & Riset ZISWAF — Arva Athallah Susanto'
    },
    {
      property: 'og:description',
      content: 'Kajian akademik, publikasi jurnal BAZNAS, dan eksplorasi teknologi digital dalam ekosistem zakat nasional.'
    }
  ]
})

const activeFilter = ref('Semua')
const categories = ['Semua', 'Publikasi IJAZ BAZNAS', 'Blockchain & Fintech', 'Tata Kelola OPZ', 'Kebijakan Publik']

interface ResearchItem {
  id: string
  title: string
  category: string
  year: string
  publisher: string
  badge: string
  excerpt: string
  methodology: string
  findings: string[]
  link?: string
  linkText?: string
  tags: string[]
}

const researchItems: ResearchItem[] = [
  {
    id: 'ijaz-blockchain',
    title: 'Critical Assessment of Blockchain Applications in Zakat Literature: Lessons for Government and Future Directions',
    category: 'Publikasi IJAZ BAZNAS',
    year: '2025',
    publisher: 'International Journal of Zakat (IJAZ - BAZNAS)',
    badge: 'Publikasi Utama IJAZ',
    excerpt: 'Evaluasi kritis dan sistematis mengenai pemanfaatan teknologi blockchain dalam ekosistem zakat nasional, menganalisis tantangan tata kelola bagi regulator serta arah strategis implementasi masa depan bagi BAZNAS.',
    methodology: 'Systematic Literature Review (SLR) & Critical Thematic Synthesis',
    findings: [
      'Smart contract terbukti mampu mereduksi asimetri informasi dan biaya audit operasional OPZ hingga 35-40%.',
      'Identifikasi kerangka trilemma tata kelola (governance, skalabilitas, dan kepatuhan syariah) bagi regulator zakat.',
      'Rekomendasi model hybrid blockchain untuk interoperabilitas data mustahik nasional terintegrasi SiMBA.'
    ],
    link: 'https://ijazbaznas.com',
    linkText: 'Buka di IJAZ BAZNAS →',
    tags: ['Blockchain', 'Smart Contracts', 'IJAZ BAZNAS', 'Regulatory Tech']
  },
  {
    id: 'digital-macro-zakat',
    title: 'Long-Term Nexus between Digitalization and Macroeconomy on Zakat Collection in Indonesia',
    category: 'Blockchain & Fintech',
    year: '2025',
    publisher: 'Applied Islamic Economics & Econometrics Review',
    badge: 'Kajian Ekonometrika',
    excerpt: 'Studi empiris jangka panjang mengenai interaksi antara akselerasi platform digital, variabel makroekonomi (inflasi, PDB per kapita, suku bunga), dan realisasi penghimpunan ZIS pada BAZNAS.',
    methodology: 'Autoregressive Distributed Lag (ARDL) & Cointegration Analysis',
    findings: [
      'Digitalisasi kanal pembayaran zakat berkontribusi elastisitas positif signifikan terhadap penghimpunan jangka panjang.',
      'Guncangan makroekonomi jangka pendek dapat diredam melalui fleksibilitas transaksi multi-channel payment.',
      'Pentingnya integrasi ekosistem e-wallet nasional dengan sistem penghimpunan BAZNAS daerah.'
    ],
    link: 'https://scholar.google.com/citations?user=7gI4mGYAAAAJ&hl=id',
    linkText: 'Lihat Sitasi Google Scholar →',
    tags: ['Digital ZISWAF', 'Makroekonomi', 'ARDL', 'Penghimpunan Zakat']
  },
  {
    id: 'slr-opz-transformation',
    title: 'Transformasi Digital Organisasi Pengelola Zakat (OPZ): Analisis Bibliometrik & Systematic Review',
    category: 'Tata Kelola OPZ',
    year: '2024–2025',
    publisher: 'Center of Islamic Social Finance (CISF) Working Paper',
    badge: 'Kajian Tata Kelola',
    excerpt: 'Pemetaan komprehensif transformasi digital amil dan lembaga OPZ di Indonesia dalam mengadopsi big data, machine learning, dan pelaporan keuangan real-time.',
    methodology: 'Bibliometric VOSviewer & PRISMA Framework',
    findings: [
      'Kesiapan digital amil menjadi faktor penentu efektivitas implementasi SiMBA di tingkat kabupaten/kota.',
      'Transparansi digital berbanding lurus dengan loyalitas dan indeks kepercayaan muzakki sebesar 42%.',
      'Penyusunan standar kompetensi digital amil zakat berbasis Standar Kompetensi Kerja Nasional Indonesia (SKKNI).'
    ],
    tags: ['Tata Kelola OPZ', 'SiMBA', 'Bibliometrik', 'Amil Kompeten']
  },
  {
    id: 'genz-digital-zakat',
    title: 'Determinants of Digital Platform Usage for Zakat Payments among Millennials and Gen Z',
    category: 'Kebijakan Publik',
    year: '2024',
    publisher: 'Islamic Financial Technology Studies',
    badge: 'Riset Perilaku Muzakki',
    excerpt: 'Analisis faktor psikologis, kemudahan teknologi (TAM/UTAUT), dan religiositas generasi muda dalam membayar zakat melalui platform digital resmi BAZNAS.',
    methodology: 'Structural Equation Modeling (PLS-SEM)',
    findings: [
      'Perceived Trust dan UI/UX Simplicity mendominasi keputusan pembayaran zakat digital generasi Z.',
      'Fitur pelaporan jejak dampak (impact tracking) meningkatkan intensi donasi berulang secara signifikan.',
      'Rekomendasi strategi gamifikasi dan micro-giving untuk engagement milenial.'
    ],
    tags: ['Gen Z Muzakki', 'PLS-SEM', 'Fintech Zakat', 'Perilaku Konsumen']
  }
]

const filteredItems = computed(() => {
  if (activeFilter.value === 'Semua') return researchItems
  return researchItems.filter(item => item.category === activeFilter.value)
})

const pillars = [
  {
    icon: '⛓️',
    number: '01',
    title: 'Blockchain & Smart Contracts Zakat',
    description: 'Meneliti arsitektur distributed ledger untuk menjamin ketertelusuran dana zakat dari muzakki hingga mustahik secara transparan tanpa jeda waktu.'
  },
  {
    icon: '📊',
    number: '02',
    title: 'Ekonometrika Penghimpunan ZIS',
    description: 'Menganalisis elastisitas penghimpunan zakat nasional terhadap dinamika makroekonomi, inflasi, dan tren akselerasi pembayaran digital.'
  },
  {
    icon: '🏛️',
    number: '03',
    title: 'Optimalisasi Tata Kelola OPZ & SiMBA',
    description: 'Kajian modernisasi operasional Organisasi Pengelola Zakat, standarisasi amil, serta integrasi platform data SiMBA BAZNAS.'
  },
  {
    icon: '🎯',
    number: '04',
    title: 'Dampak Sosial & Pengentasan Kemiskinan',
    description: 'Evaluasi integrasi program pendistribusian dan pendayagunaan ZISWAF terhadap pencapaian Sustainable Development Goals (SDGs).'
  }
]

const milestones = [
  {
    period: '2021 – 2022',
    title: 'Fondasi Riset ZISWAF & Perbankan Syariah',
    desc: 'Lulus Sarjana Ekonomi Islam (Cum Laude) di Universitas Airlangga dengan fokus pendalaman instrumen Keuangan Sosial Islam dan tata kelola perbankan syariah.'
  },
  {
    period: '2023 – 2024',
    title: 'Kajian Bibliometrik & Riset Adopsi Digital Zakat',
    desc: 'Melakukan riset mendalam terkait determinan adopsi fintech zakat oleh generasi muda serta pemodelan bibliometrik transformasi digital OPZ di Indonesia.'
  },
  {
    period: '2024 – 2025',
    title: 'Konsultan CISF & Publikasi IJAZ BAZNAS',
    desc: 'Berperan sebagai Research Consultant di Center of Islamic Social Finance (CISF) dan mempublikasikan kajian kritis aplikasi Blockchain di International Journal of Zakat (BAZNAS).'
  },
  {
    period: '2025 – 2026',
    title: 'Diseminasi Internasional & Integrasi ESG',
    desc: 'Awardee Canada-ASEAN SEED di Dalhousie University, meneliti konvergensi antara instrumen ZISWAF, ESG Banking, dan ketahanan ekonomi sosial makro.'
  }
]
</script>

<template>
  <main class="baznas-page">
    <!-- HERO SECTION -->
    <section class="baznas-hero">
      <div class="hero-backdrop">
        <div class="orb orb-emerald"></div>
        <div class="orb orb-teal"></div>
        <div class="orb orb-gold"></div>
      </div>

      <div class="baznas-hero-content">
        <div class="hero-badge-wrap">
          <span class="hero-badge live-badge">
            <span class="pulse-dot"></span> BAZNAS ACADEMIC PORTFOLIO
          </span>
          <span class="hero-badge sub-badge">ZISWAF &amp; ISLAMIC SOCIAL FINANCE</span>
        </div>

        <h1 class="hero-headline">
          Portofolio Riset &amp; Transformasi Digital <span class="highlight-text">BAZNAS</span>
        </h1>

        <p class="hero-description">
          Dokumentasi komprehensif kontribusi akademik, publikasi jurnal <strong>International Journal of Zakat (IJAZ - BAZNAS)</strong>, 
          kajian pemanfaatan teknologi <em>blockchain</em>, analisis ekonometrika penghimpunan, dan strategi transformasi digital 
          Organisasi Pengelola Zakat (OPZ) oleh <strong>Arva Athallah Susanto</strong>.
        </p>

        <div class="hero-cta-group">
          <a href="#research-catalog" class="baznas-btn primary">
            Eksplorasi Publikasi Riset ↓
          </a>
          <NuxtLink to="/portfolio" class="baznas-btn secondary">
            ← Portofolio Lengkap
          </NuxtLink>
        </div>

        <!-- Metric Highlight Bar -->
        <div class="metric-ribbon">
          <div class="metric-item">
            <span class="metric-number">IJAZ</span>
            <span class="metric-label">Publikasi Jurnal Resmi BAZNAS</span>
          </div>
          <div class="metric-sep"></div>
          <div class="metric-item">
            <span class="metric-number">CISF</span>
            <span class="metric-label">Center of Islamic Social Finance</span>
          </div>
          <div class="metric-sep"></div>
          <div class="metric-item">
            <span class="metric-number">Web3</span>
            <span class="metric-label">Kajian Blockchain &amp; Smart Contracts</span>
          </div>
          <div class="metric-sep"></div>
          <div class="metric-item">
            <span class="metric-number">ARDL</span>
            <span class="metric-label">Ekonometrika Makro ZISWAF</span>
          </div>
        </div>
      </div>
    </section>

    <!-- 4 STRATEGIC PILLARS -->
    <section class="baznas-section">
      <div class="section-head">
        <p class="section-kicker">Core Research Pillars</p>
        <h2>4 Pilar Fokus Riset &amp; Inovasi ZISWAF</h2>
        <p class="section-sub">
          Pendekatan multidisipliner memadukan metodologi kuantitatif, analisis bibliometrik, dan kesiapan teknologi terdistribusi.
        </p>
      </div>

      <div class="pillars-grid">
        <article v-for="pillar in pillars" :key="pillar.number" class="pillar-card">
          <div class="pillar-top">
            <span class="pillar-icon">{{ pillar.icon }}</span>
            <span class="pillar-num">{{ pillar.number }}</span>
          </div>
          <h3>{{ pillar.title }}</h3>
          <p>{{ pillar.description }}</p>
        </article>
      </div>
    </section>

    <!-- RESEARCH CATALOG SECTION -->
    <section id="research-catalog" class="baznas-section soft-bg">
      <div class="section-head">
        <p class="section-kicker">Publications &amp; Working Papers</p>
        <h2>Katalog Publikasi &amp; Analisis Ilmiah</h2>
        <p class="section-sub">
          Daftar karya ilmiah, publikasi jurnal terakreditasi BAZNAS, dan kajian strategis pengelolaan zakat nasional.
        </p>
      </div>

      <!-- Category Filter Pills -->
      <div class="filter-bar">
        <button
          v-for="cat in categories"
          :key="cat"
          class="filter-pill"
          :class="{ active: activeFilter === cat }"
          @click="activeFilter = cat"
        >
          {{ cat }}
        </button>
      </div>

      <!-- Research Cards Grid -->
      <div class="research-grid">
        <article
          v-for="item in filteredItems"
          :key="item.id"
          class="research-card"
        >
          <div class="rc-header">
            <div class="rc-meta">
              <span class="rc-badge">{{ item.badge }}</span>
              <span class="rc-year">📅 {{ item.year }}</span>
            </div>
            <span class="rc-publisher">{{ item.publisher }}</span>
          </div>

          <h3 class="rc-title">{{ item.title }}</h3>
          <p class="rc-excerpt">{{ item.excerpt }}</p>

          <div class="rc-methodology">
            <strong>Metodologi:</strong> {{ item.methodology }}
          </div>

          <div class="rc-findings">
            <h4>Temuan Kunci &amp; Rekomendasi:</h4>
            <ul>
              <li v-for="(finding, fIdx) in item.findings" :key="fIdx">
                {{ finding }}
              </li>
            </ul>
          </div>

          <div class="rc-tags">
            <span v-for="tag in item.tags" :key="tag" class="rc-tag">#{{ tag }}</span>
          </div>

          <div v-if="item.link" class="rc-footer">
            <a :href="item.link" target="_blank" rel="noopener noreferrer" class="rc-link">
              {{ item.linkText || 'Lihat Sumber Publikasi →' }}
            </a>
          </div>
        </article>
      </div>
    </section>

    <!-- TIMELINE SECTION -->
    <section class="baznas-section">
      <div class="section-head">
        <p class="section-kicker">Academic Track Record</p>
        <h2>Linimasa Perjalanan Riset ZISWAF</h2>
      </div>

      <div class="timeline-container">
        <div v-for="(step, idx) in milestones" :key="idx" class="timeline-step">
          <div class="step-badge">{{ step.period }}</div>
          <div class="step-card">
            <h3>{{ step.title }}</h3>
            <p>{{ step.desc }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- CALL TO ACTION / COLLABORATION -->
    <section class="baznas-cta-section">
      <div class="cta-inner">
        <span class="hero-badge live-badge">KOLABORASI RISET &amp; KONSULTASI</span>
        <h2>Membangun Dampak Nyata bagi Ekosistem Zakat Indonesia</h2>
        <p>
          Terbuka untuk kolaborasi riset akademik, penulisan policy paper BAZNAS, konsultasi metodologi penelitian 
          (Bibliometrik, PLS-SEM, ARDL, SLR), serta diskusi implementasi teknologi keuangan sosial syariah.
        </p>

        <div class="cta-actions">
          <NuxtLink to="/contact" class="baznas-btn primary">
            Hubungi Arva Athallah →
          </NuxtLink>
          <NuxtLink to="/writings" class="baznas-btn secondary">
            Baca Tulisan Akademik
          </NuxtLink>
        </div>
      </div>
    </section>
  </main>
</template>

<style scoped>
/* ── BASE & CONTAINER ────────────────────────────────── */
.baznas-page {
  font-family: var(--font-body, system-ui, sans-serif);
  color: #0f172a;
  background-color: #ffffff;
  min-height: 100vh;
}

/* ── HERO SECTION ───────────────────────────────────── */
.baznas-hero {
  position: relative;
  background: radial-gradient(circle at 50% 0%, #064e3b 0%, #022c22 60%, #021a14 100%);
  color: #ffffff;
  padding: 100px 24px 80px;
  overflow: hidden;
  text-align: center;
}

.hero-backdrop {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(90px);
  opacity: 0.35;
}

.orb-emerald {
  width: 450px;
  height: 450px;
  background: #10b981;
  top: -120px;
  left: -80px;
}

.orb-teal {
  width: 350px;
  height: 350px;
  background: #0d9488;
  bottom: -60px;
  right: -50px;
}

.orb-gold {
  width: 250px;
  height: 250px;
  background: #f59e0b;
  top: 30%;
  left: 50%;
  transform: translateX(-50%);
  opacity: 0.2;
}

.baznas-hero-content {
  position: relative;
  z-index: 2;
  max-width: 900px;
  margin: 0 auto;
}

.hero-badge-wrap {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  flex-wrap: wrap;
  margin-bottom: 24px;
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 6px 16px;
  border-radius: 999px;
  font-family: var(--font-mono, monospace);
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}

.live-badge {
  background: rgba(16, 185, 129, 0.2);
  border: 1px solid rgba(16, 185, 129, 0.4);
  color: #34d399;
}

.sub-badge {
  background: rgba(255, 255, 255, 0.08);
  border: 1px solid rgba(255, 255, 255, 0.15);
  color: #e2e8f0;
}

.pulse-dot {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: #34d399;
  box-shadow: 0 0 10px #34d399;
  animation: pulse 2s infinite ease-in-out;
}

@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.4; transform: scale(1.4); }
}

.hero-headline {
  font-family: var(--font-display, serif);
  font-size: clamp(34px, 5.5vw, 64px);
  font-weight: 800;
  line-height: 1.08;
  letter-spacing: -0.04em;
  margin: 0 0 20px;
  color: #ffffff;
}

.highlight-text {
  background: linear-gradient(135deg, #34d399 0%, #fbbf24 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.hero-description {
  font-size: clamp(15px, 1.8vw, 18px);
  line-height: 1.7;
  color: #cbd5e1;
  max-width: 780px;
  margin: 0 auto 36px;
}

.hero-description strong {
  color: #f8fafc;
}

.hero-cta-group {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 16px;
  flex-wrap: wrap;
  margin-bottom: 48px;
}

.baznas-btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 12px 28px;
  border-radius: 12px;
  font-size: 14px;
  font-weight: 700;
  text-decoration: none;
  transition: all 0.25s cubic-bezier(0.16, 1, 0.3, 1);
  cursor: pointer;
}

.baznas-btn.primary {
  background: linear-gradient(135deg, #10b981 0%, #059669 100%);
  color: #ffffff;
  box-shadow: 0 8px 24px -6px rgba(16, 185, 129, 0.5);
  border: 1px solid rgba(255, 255, 255, 0.15);
}

.baznas-btn.primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 14px 32px -6px rgba(16, 185, 129, 0.7);
  background: linear-gradient(135deg, #059669 0%, #047857 100%);
}

.baznas-btn.secondary {
  background: rgba(255, 255, 255, 0.08);
  color: #f8fafc;
  border: 1px solid rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(10px);
}

.baznas-btn.secondary:hover {
  background: rgba(255, 255, 255, 0.15);
  transform: translateY(-2px);
}

/* Metric Ribbon */
.metric-ribbon {
  display: flex;
  align-items: center;
  justify-content: space-around;
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(16px);
  border: 1px solid rgba(255, 255, 255, 0.12);
  border-radius: 20px;
  padding: 24px 20px;
  flex-wrap: wrap;
  gap: 16px;
}

.metric-item {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.metric-number {
  font-family: var(--font-display, serif);
  font-size: 26px;
  font-weight: 800;
  color: #34d399;
  letter-spacing: -0.02em;
}

.metric-label {
  font-size: 11px;
  font-weight: 600;
  color: #94a3b8;
  letter-spacing: 0.02em;
}

.metric-sep {
  width: 1px;
  height: 36px;
  background: rgba(255, 255, 255, 0.1);
}

@media (max-width: 768px) {
  .metric-sep {
    display: none;
  }
}

/* ── COMMON SECTION HEAD ────────────────────────────── */
.baznas-section {
  padding: 80px 24px;
  max-width: 1200px;
  margin: 0 auto;
}

.baznas-section.soft-bg {
  background: #f8fafc;
  max-width: 100%;
  border-top: 1px solid #e2e8f0;
  border-bottom: 1px solid #e2e8f0;
}

.baznas-section.soft-bg > .section-head,
.baznas-section.soft-bg > .filter-bar,
.baznas-section.soft-bg > .research-grid {
  max-width: 1200px;
  margin-left: auto;
  margin-right: auto;
}

.section-head {
  text-align: center;
  max-width: 720px;
  margin: 0 auto 48px;
}

.section-kicker {
  font-family: var(--font-mono, monospace);
  font-size: 12px;
  font-weight: 800;
  color: #059669;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  margin-bottom: 8px;
}

.section-head h2 {
  font-family: var(--font-display, serif);
  font-size: clamp(28px, 4vw, 44px);
  font-weight: 800;
  line-height: 1.15;
  letter-spacing: -0.03em;
  margin: 0 0 14px;
  color: #0f172a;
}

.section-sub {
  font-size: 15px;
  color: #64748b;
  line-height: 1.6;
  margin: 0;
}

/* ── PILLARS GRID ───────────────────────────────────── */
.pillars-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 24px;
}

.pillar-card {
  background: #ffffff;
  border: 1px solid #e2e8f0;
  border-radius: 20px;
  padding: 32px 24px;
  display: flex;
  flex-direction: column;
  gap: 14px;
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  box-shadow: 0 4px 20px rgba(15, 23, 42, 0.04);
}

.pillar-card:hover {
  transform: translateY(-6px);
  border-color: #10b981;
  box-shadow: 0 20px 40px rgba(16, 185, 129, 0.12);
}

.pillar-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.pillar-icon {
  font-size: 32px;
}

.pillar-num {
  font-family: var(--font-mono, monospace);
  font-size: 13px;
  font-weight: 800;
  color: #059669;
  background: #ecfdf5;
  padding: 4px 10px;
  border-radius: 8px;
}

.pillar-card h3 {
  font-family: var(--font-display, serif);
  font-size: 19px;
  font-weight: 700;
  color: #0f172a;
  margin: 0;
  line-height: 1.3;
}

.pillar-card p {
  font-size: 14px;
  color: #64748b;
  line-height: 1.6;
  margin: 0;
}

/* ── FILTER BAR ─────────────────────────────────────── */
.filter-bar {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  flex-wrap: wrap;
  margin-bottom: 40px;
}

.filter-pill {
  padding: 8px 20px;
  border-radius: 999px;
  border: 1px solid #cbd5e1;
  background: #ffffff;
  color: #475569;
  font-size: 13px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s ease;
}

.filter-pill:hover {
  border-color: #059669;
  color: #059669;
}

.filter-pill.active {
  background: #059669;
  border-color: #059669;
  color: #ffffff;
  box-shadow: 0 4px 14px rgba(5, 150, 105, 0.3);
}

/* ── RESEARCH CARDS GRID ────────────────────────────── */
.research-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(340px, 1fr));
  gap: 28px;
}

.research-card {
  background: #ffffff;
  border: 1px solid #e2e8f0;
  border-radius: 24px;
  padding: 32px;
  display: flex;
  flex-direction: column;
  gap: 16px;
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  box-shadow: 0 4px 20px rgba(15, 23, 42, 0.05);
}

.research-card:hover {
  transform: translateY(-6px);
  border-color: #10b981;
  box-shadow: 0 24px 50px rgba(15, 23, 42, 0.1);
}

.rc-header {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.rc-meta {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.rc-badge {
  font-family: var(--font-mono, monospace);
  font-size: 11px;
  font-weight: 800;
  color: #047857;
  background: #d1fae5;
  padding: 4px 10px;
  border-radius: 6px;
  text-transform: uppercase;
}

.rc-year {
  font-size: 12px;
  font-weight: 600;
  color: #64748b;
}

.rc-publisher {
  font-size: 12px;
  font-weight: 700;
  color: #0284c7;
}

.rc-title {
  font-family: var(--font-display, serif);
  font-size: 20px;
  font-weight: 700;
  line-height: 1.35;
  color: #0f172a;
  margin: 0;
}

.rc-excerpt {
  font-size: 14px;
  color: #475569;
  line-height: 1.6;
  margin: 0;
}

.rc-methodology {
  font-size: 13px;
  color: #334155;
  background: #f1f5f9;
  padding: 10px 14px;
  border-radius: 10px;
  border-left: 3px solid #059669;
}

.rc-findings {
  font-size: 13px;
  color: #334155;
}

.rc-findings h4 {
  font-size: 13px;
  font-weight: 700;
  margin: 0 0 6px 0;
  color: #0f172a;
}

.rc-findings ul {
  margin: 0;
  padding-left: 20px;
  line-height: 1.55;
}

.rc-findings li {
  margin-bottom: 4px;
}

.rc-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-top: auto;
  padding-top: 10px;
}

.rc-tag {
  font-family: var(--font-mono, monospace);
  font-size: 11px;
  color: #059669;
  background: #ecfdf5;
  padding: 3px 8px;
  border-radius: 6px;
}

.rc-footer {
  padding-top: 14px;
  border-top: 1px solid #f1f5f9;
}

.rc-link {
  font-size: 13px;
  font-weight: 700;
  color: #059669;
  text-decoration: none;
  transition: color 0.2s;
}

.rc-link:hover {
  color: #047857;
  text-decoration: underline;
}

/* ── TIMELINE ───────────────────────────────────────── */
.timeline-container {
  display: flex;
  flex-direction: column;
  gap: 20px;
  max-width: 800px;
  margin: 0 auto;
}

.timeline-step {
  display: flex;
  gap: 20px;
  align-items: flex-start;
}

.step-badge {
  font-family: var(--font-mono, monospace);
  font-size: 12px;
  font-weight: 800;
  color: #ffffff;
  background: #064e3b;
  padding: 8px 14px;
  border-radius: 10px;
  white-space: nowrap;
  min-width: 120px;
  text-align: center;
}

.step-card {
  flex: 1;
  background: #ffffff;
  border: 1px solid #e2e8f0;
  border-radius: 16px;
  padding: 20px 24px;
  box-shadow: 0 2px 10px rgba(15, 23, 42, 0.03);
}

.step-card h3 {
  font-family: var(--font-display, serif);
  font-size: 17px;
  font-weight: 700;
  margin: 0 0 6px 0;
  color: #0f172a;
}

.step-card p {
  font-size: 14px;
  color: #64748b;
  margin: 0;
  line-height: 1.55;
}

@media (max-width: 640px) {
  .timeline-step {
    flex-direction: column;
    gap: 8px;
  }
}

/* ── CTA SECTION ────────────────────────────────────── */
.baznas-cta-section {
  background: linear-gradient(135deg, #022c22 0%, #064e3b 50%, #0f766e 100%);
  color: #ffffff;
  padding: 80px 24px;
  text-align: center;
}

.cta-inner {
  max-width: 720px;
  margin: 0 auto;
}

.cta-inner h2 {
  font-family: var(--font-display, serif);
  font-size: clamp(28px, 4.5vw, 48px);
  font-weight: 800;
  line-height: 1.15;
  letter-spacing: -0.03em;
  margin: 20px 0 16px;
}

.cta-inner p {
  font-size: 16px;
  color: #cbd5e1;
  line-height: 1.7;
  margin-bottom: 36px;
}

.cta-actions {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 16px;
  flex-wrap: wrap;
}
</style>
