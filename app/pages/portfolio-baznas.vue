<script setup lang="ts">
import { ref, computed, onMounted, watch } from 'vue'

useHead({
  title: 'Portofolio BAZNAS & Materi Riset Pimpinan — Arva Athallah Susanto',
  meta: [
    {
      name: 'description',
      content: 'Portofolio akademik, materi presentasi pimpinan BAZNAS, publikasi International Journal of Zakat (IJAZ), dan kajian transformasi digital ZISWAF oleh Arva Athallah Susanto.'
    },
    {
      name: 'keywords',
      content: 'BAZNAS RI, Staf Riset dan Kajian Pengembangan, IJAZ BAZNAS, Materi Pimpinan BAZNAS, SROI Zakat, ZISWAF, Arva Athallah Susanto, Islamic Social Finance'
    },
    {
      property: 'og:title',
      content: 'Portofolio BAZNAS & Materi Riset Pimpinan — Arva Athallah Susanto'
    },
    {
      property: 'og:description',
      content: 'Carousel presentasi materi pimpinan, publikasi IJAZ, dan kompetensi riset BAZNAS RI.'
    }
  ]
})

// ── PRESENTATION CAROUSEL STATE ─────────────────────────
interface Presentation {
  id: string
  title: string
  subtitle: string
  presenter: string
  role: string
  totalPages: number
  pdfUrl: string
  fileSize: string
  summary: string
  keyTopics: string[]
}

const presentations: Presentation[] = [
  {
    id: 'presentation-1',
    title: 'Islamic Economics for Economic Resilience and Welfare',
    subtitle: 'Materi Kajian Fikih Muamalah, Sukuk, dan Peran Zakat sebagai Instrumen Fiskal Islam',
    presenter: 'Prof. Dr. Tika Widiastuti, S.E., M.Si (with Arva Athallah Susanto)',
    role: 'Vice Dean 1 FEB UNAIR & Professor of Islamic Social Finance',
    totalPages: 26,
    pdfUrl: '/documents/islamic-economics-resilience-welfare-arva.pdf',
    fileSize: '2.9 MB (26 Slides)',
    summary: 'Materi komprehensif tingkat pimpinan yang mengkaji integrasi Fikih Muamalah, instrumen Sukuk, penjaminan sirkulasi modal ke sektor riil, zakat sebagai instrumen fiskal negara, model pemberdayaan berbasis potensi mustahik (Azis et al.), serta perbandingan tata kelola zakat lintas negara (Indonesia, Malaysia, Saudi Arabia, Kuwait, Turki, Singapura).',
    keyTopics: [
      'Fikih-Muamalah Based Alternatives',
      'Sukuk Process Scheme & Real Sector Circulation',
      'Zakat as Islamic Fiscal Instrument in Global Countries',
      'Productive Zakat & Mustahik Potential Model',
      'Zakat-Waqf Integration (12% Welfare Improvement)',
      'Shift from GDP to Falah'
    ]
  },
  {
    id: 'presentation-2',
    title: 'Program Pemberdayaan Terukur, Terencana, dan Berdampak',
    subtitle: 'Standarisasi Tata Kelola ZCP BAZNAS, BMC Zakat Sentra Ternak, dan Kaji Dampak SROI',
    presenter: 'Center of Islamic Social Finance (CISF) / Prof. Dr. Tika Widiastuti, S.E., M.Si',
    role: 'Senior Expert CISF & Guru Besar Keuangan Sosial Islam',
    totalPages: 27,
    pdfUrl: '/documents/program-pemberdayaan-terukur-cisf-arva.pdf',
    fileSize: '9.0 MB (27 Slides)',
    summary: 'Materi strategis perancangan program pemberdayaan ZISWAF berbasis data dan bukti empiris. Membedah kinerja zakat nasional (DEKS BI), RPJPN 2025-2045, regulasi UU 23/2011 & PP 14/2014, Zakat Core Principles (ZCP 7 & 8), Business Model Canvas (BMC) Sentra Ternak Puskas BAZNAS, Resource Leveling SDM, Social Return on Investment (SROI) Value Map, Indeks Desa Zakat, Indeks Kifayah, Indeks Kesejahteraan BAZNAS, dan Model 4 ER (Rescue, Recovery, Reinforcement, Resilience).',
    keyTopics: [
      'Kinerja Ekonomi Syariah Nasional & RPJPN 2025-2045',
      'Tata Kelola Regulasi & Zakat Core Principles (ZCP 7-8)',
      '7 Tahap Perancangan Program & Business Model Canvas (BMC)',
      'Pengukuran Dampak Berbasis SROI Value Map',
      'Indeks Desa Zakat & Indeks Kesejahteraan BAZNAS',
      'Transformasi Mustahik ke Muzakki (Model 4 ER)'
    ]
  }
]

const selectedPresIndex = ref(0)
const currentPresentation = computed(() => presentations[selectedPresIndex.value])
const currentPage = ref(1)
const isRendering = ref(false)
const zoomScale = ref(1.3)
const viewMode = ref<'canvas' | 'embed'>('canvas')

const pdfCanvas = ref<HTMLCanvasElement | null>(null)
let pdfDocInstance: any = null

function loadPdfJsScript(): Promise<void> {
  return new Promise((resolve, reject) => {
    if (typeof window === 'undefined') return resolve()
    if ((window as any).pdfjsLib) return resolve()

    const script = document.createElement('script')
    script.src = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js'
    script.onload = () => {
      if ((window as any).pdfjsLib) {
        (window as any).pdfjsLib.GlobalWorkerOptions.workerSrc =
          'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js'
      }
      resolve()
    }
    script.onerror = () => reject(new Error('Gagal memuat pdf.js'))
    document.head.appendChild(script)
  })
}

async function renderCurrentPage() {
  if (!pdfDocInstance || !pdfCanvas.value) return
  isRendering.value = true

  try {
    const page = await pdfDocInstance.getPage(currentPage.value)
    const canvas = pdfCanvas.value
    const ctx = canvas.getContext('2d')
    if (!ctx) return

    // Responsif viewport berdasarkan lebar layar
    let scale = zoomScale.value
    if (window.innerWidth < 768) {
      scale = 0.85
    }

    const viewport = page.getViewport({ scale })
    canvas.height = viewport.height
    canvas.width = viewport.width

    await page.render({
      canvasContext: ctx,
      viewport
    }).promise
  } catch (err) {
    console.error('Error rendering page:', err)
  } finally {
    isRendering.value = false
  }
}

async function loadPresentationDoc() {
  if (typeof window === 'undefined') return
  isRendering.value = true

  try {
    await loadPdfJsScript()
    const pdfjsLib = (window as any).pdfjsLib
    if (!pdfjsLib) return

    const loadingTask = pdfjsLib.getDocument(currentPresentation.value.pdfUrl)
    pdfDocInstance = await loadingTask.promise
    currentPage.value = 1
    await renderCurrentPage()
  } catch (err) {
    console.error('Error loading PDF document:', err)
    // Fallback otomatis ke mode embed iframe jika canvas terhalang
    viewMode.value = 'embed'
  } finally {
    isRendering.value = false
  }
}

function nextPage() {
  if (currentPage.value < currentPresentation.value.totalPages) {
    currentPage.value++
    renderCurrentPage()
  }
}

function prevPage() {
  if (currentPage.value > 1) {
    currentPage.value--
    renderCurrentPage()
  }
}

function goToPage(p: number) {
  if (p >= 1 && p <= currentPresentation.value.totalPages) {
    currentPage.value = p
    renderCurrentPage()
  }
}

function selectPresentation(index: number) {
  selectedPresIndex.value = index
  currentPage.value = 1
  loadPresentationDoc()
}

watch(zoomScale, () => {
  renderCurrentPage()
})

onMounted(() => {
  loadPresentationDoc()

  // Navigasi keyboard (Arrow Left / Arrow Right)
  window.addEventListener('keydown', (e) => {
    if (e.key === 'ArrowRight') nextPage()
    if (e.key === 'ArrowLeft') prevPage()
  })
})

// ── RESEARCH CATALOG FILTER STATE ───────────────────────
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

// ── BAZNAS JOB REQUIREMENTS ALIGNMENT MATRIX ────────────
const jobMatrix = [
  {
    number: '01',
    roleTask: 'Melakukan riset, kajian, dan pengembangan mengenai zakat',
    evidence: 'Publikasi di International Journal of Zakat (IJAZ - BAZNAS), pemodelan ekonometrika ARDL makroekonomi zakat, dan kajian transformasi 4 ER (Rescue, Recovery, Reinforcement, Resilience).',
    statusBadge: '100% Terpenuhi'
  },
  {
    number: '02',
    roleTask: 'Membuat materi untuk Pimpinan BAZNAS',
    evidence: 'Penyusunan 2 set deck materi pimpinan FEB UNAIR & CISF mencakup kebijakan fiskal zakat, SROI, ZCP BAZNAS, dan Business Model Canvas (BMC) Zakat Sentra Ternak.',
    statusBadge: '100% Terpenuhi'
  },
  {
    number: '03',
    roleTask: 'Melakukan administrasi yang mendukung kegiatan riset & kajian',
    evidence: 'Pengalaman sebagai Research Consultant di Center of Islamic Social Finance (CISF) dan Research Assistant Guru Besar Keuangan Sosial Islam (Prof. Dr. Tika Widiastuti).',
    statusBadge: '100% Terpenuhi'
  },
  {
    number: '04',
    roleTask: 'Mengelola jurnal IJAZ (International Journal of Zakat)',
    evidence: 'Penulis aktif di IJAZ BAZNAS, menguasai workflow publikasi ilmiah Open Journal Systems (OJS), peer-review, dan standar bibliometrik internasional.',
    statusBadge: '100% Terpenuhi'
  },
  {
    number: '05',
    roleTask: 'Pengoperasian tools riset & kemampuan analisis ilmiah',
    evidence: 'Mahir mengoperasikan VOSviewer, SmartPLS (PLS-SEM), EViews/Stata (ARDL), Systematic Literature Review (PRISMA), dan analisis SROI Value Map.',
    statusBadge: '100% Terpenuhi'
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
            <span class="pulse-dot"></span> BAZNAS RI RECRUITMENT PORTFOLIO
          </span>
          <span class="hero-badge sub-badge">STAF RISET &amp; KAJIAN PENGEMBANGAN</span>
        </div>

        <h1 class="hero-headline">
          Portofolio Riset &amp; Materi Pimpinan <span class="highlight-text">BAZNAS RI</span>
        </h1>

        <p class="hero-description">
          Dokumentasi karya ilmiah, publikasi <strong>International Journal of Zakat (IJAZ)</strong>, 
          materi presentasi tingkat pimpinan, serta matriks pemenuhan kualifikasi 
          <strong>Staf Riset dan Kajian Pengembangan BAZNAS RI</strong> oleh 
          <strong>Arva Athallah Susanto, S.EI., M.SEI</strong>.
        </p>

        <div class="hero-cta-group">
          <a href="#presentation-carousel" class="baznas-btn primary">
            📊 Tampilkan Carousel Materi Pimpinan ↓
          </a>
          <a href="#job-matrix" class="baznas-btn secondary">
            📋 Matriks Kualifikasi BAZNAS
          </a>
        </div>

        <!-- Metric Highlight Bar -->
        <div class="metric-ribbon">
          <div class="metric-item">
            <span class="metric-number">IJAZ</span>
            <span class="metric-label">Publikasi Terindeks BAZNAS</span>
          </div>
          <div class="metric-sep"></div>
          <div class="metric-item">
            <span class="metric-number">2 Set</span>
            <span class="metric-label">Materi Presentasi Pimpinan</span>
          </div>
          <div class="metric-sep"></div>
          <div class="metric-item">
            <span class="metric-number">CISF</span>
            <span class="metric-label">Center of Islamic Social Finance</span>
          </div>
          <div class="metric-sep"></div>
          <div class="metric-item">
            <span class="metric-number">SROI &amp; ZCP</span>
            <span class="metric-label">Metodologi Kaji Dampak ZISWAF</span>
          </div>
        </div>
      </div>
    </section>

    <!-- ── INTERACTIVE PRESENTATION CAROUSEL (PDF SLIDE VIEWER) ── -->
    <section id="presentation-carousel" class="baznas-section">
      <div class="section-head">
        <p class="section-kicker">Executive Presentation &amp; Research Materials</p>
        <h2>Carousel Materi Riset &amp; Presentasi Pimpinan</h2>
        <p class="section-sub">
          Materi presentasi komprehensif tingkat pimpinan yang dapat dijelajahi slide demi slide secara interaktif maupun diunduh dalam format PDF asli.
        </p>
      </div>

      <!-- Presentation Selector Tabs -->
      <div class="pres-tabs-wrap">
        <button
          v-for="(pres, pIdx) in presentations"
          :key="pres.id"
          class="pres-tab-btn"
          :class="{ active: selectedPresIndex === pIdx }"
          @click="selectPresentation(pIdx)"
        >
          <span class="tab-badge">Materi #0{{ pIdx + 1 }}</span>
          <span class="tab-title">{{ pres.title }}</span>
          <span class="tab-meta">{{ pres.fileSize }}</span>
        </button>
      </div>

      <!-- Carousel Viewer Main Box -->
      <div class="carousel-container">
        <!-- Presentation Header Info Bar -->
        <div class="pres-info-bar">
          <div class="pib-left">
            <span class="pib-presenter">👤 {{ currentPresentation.presenter }}</span>
            <span class="pib-role">🏛️ {{ currentPresentation.role }}</span>
          </div>
          <div class="pib-actions">
            <!-- Download Button -->
            <a
              :href="currentPresentation.pdfUrl"
              download
              class="btn-download"
              target="_blank"
            >
              📥 Download PDF ({{ currentPresentation.fileSize }})
            </a>
            <!-- View Mode Switch -->
            <button
              class="btn-toggle-view"
              @click="viewMode = viewMode === 'canvas' ? 'embed' : 'canvas'"
            >
              {{ viewMode === 'canvas' ? '🖥️ Buka PDF Reader' : '🖼️ Mode Carousel Slide' }}
            </button>
          </div>
        </div>

        <!-- SLIDE DISPLAY AREA -->
        <div class="slide-display-stage">
          <!-- Canvas Interactive Slide View -->
          <div v-show="viewMode === 'canvas'" class="canvas-wrapper">
            <div v-if="isRendering" class="rendering-overlay">
              <div class="render-spinner"></div>
              <span>Memuat Slide {{ currentPage }} / {{ currentPresentation.totalPages }}...</span>
            </div>
            <canvas ref="pdfCanvas" class="slide-canvas"></canvas>
          </div>

          <!-- Embed PDF Viewer Fallback / Alternate View -->
          <div v-if="viewMode === 'embed'" class="embed-wrapper">
            <iframe
              :src="currentPresentation.pdfUrl + '#page=' + currentPage"
              class="pdf-iframe"
              title="PDF Viewer"
            ></iframe>
          </div>

          <!-- Floating Navigation Controls -->
          <div class="carousel-nav-controls">
            <button
              class="nav-btn prev"
              :disabled="currentPage <= 1"
              @click="prevPage"
              aria-label="Slide Sebelumnya"
            >
              ❮ Prev
            </button>

            <div class="page-indicator">
              <span>Slide</span>
              <strong>{{ currentPage }}</strong>
              <span>/ {{ currentPresentation.totalPages }}</span>
            </div>

            <button
              class="nav-btn next"
              :disabled="currentPage >= currentPresentation.totalPages"
              @click="nextPage"
              aria-label="Slide Berikutnya"
            >
              Next ❯
            </button>
          </div>
        </div>

        <!-- Slide Thumbnails Grid / Quick Jumper -->
        <div class="thumbnails-bar">
          <span class="thumb-label">Lompat ke Slide:</span>
          <div class="thumb-chips">
            <button
              v-for="p in currentPresentation.totalPages"
              :key="p"
              class="thumb-chip"
              :class="{ active: currentPage === p }"
              @click="goToPage(p)"
            >
              {{ p }}
            </button>
          </div>
        </div>

        <!-- Slide Content Summary & Highlights -->
        <div class="pres-summary-box">
          <div class="ps-header">
            <h3>📑 Ringkasan Materi &amp; Ruang Lingkup Kajian:</h3>
            <p>{{ currentPresentation.summary }}</p>
          </div>

          <div class="ps-topics">
            <h4>Poin-Poin Pokok yang Dibahas:</h4>
            <div class="topic-tags">
              <span v-for="t in currentPresentation.keyTopics" :key="t" class="topic-tag">
                ✓ {{ t }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ── JOB ALIGNMENT MATRIX SECTION ── -->
    <section id="job-matrix" class="baznas-section soft-bg">
      <div class="section-head">
        <p class="section-kicker">Position Competency Match</p>
        <h2>Matriks Kesesuaian Kualifikasi BAZNAS RI</h2>
        <p class="section-sub">
          Pemetaan kompetensi akademik dan portofolio Arva Athallah Susanto terhadap kebutuhan formasi 
          <strong>Staf Riset dan Kajian Pengembangan — BAZNAS RI</strong>.
        </p>
      </div>

      <div class="matrix-grid">
        <article v-for="item in jobMatrix" :key="item.number" class="matrix-card">
          <div class="mc-top">
            <span class="mc-num">Poin #{{ item.number }}</span>
            <span class="mc-badge">{{ item.statusBadge }}</span>
          </div>
          <h3 class="mc-task">"{{ item.roleTask }}"</h3>
          <div class="mc-evidence">
            <strong>Bukti Portofolio &amp; Rekam Jejak:</strong>
            <p>{{ item.evidence }}</p>
          </div>
        </article>
      </div>
    </section>

    <!-- ── RESEARCH PUBLICATIONS SECTION ── -->
    <section id="research-catalog" class="baznas-section">
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

    <!-- CALL TO ACTION -->
    <section class="baznas-cta-section">
      <div class="cta-inner">
        <span class="hero-badge live-badge">KOLABORASI &amp; REKRUTMEN BAZNAS RI</span>
        <h2>Siap Berkontribusi Nyata bagi Kemajuan Riset BAZNAS RI</h2>
        <p>
          Memiliki dedikasi tinggi untuk memperkuat tata kelola zakat nasional, pengelolaan jurnal IJAZ, 
          serta penyusunan materi kebijakan pimpinan berbasis riset empiris dan teknologi mutakhir.
        </p>

        <div class="cta-actions">
          <NuxtLink to="/contact" class="baznas-btn primary">
            Hubungi Arva Athallah →
          </NuxtLink>
          <a href="/documents/islamic-economics-resilience-welfare-arva.pdf" download class="baznas-btn secondary">
            📥 Download Materi 1 PDF
          </a>
          <a href="/documents/program-pemberdayaan-terukur-cisf-arva.pdf" download class="baznas-btn secondary">
            📥 Download Materi 2 PDF
          </a>
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
  font-size: clamp(32px, 5.2vw, 60px);
  font-weight: 800;
  line-height: 1.1;
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
  font-size: clamp(15px, 1.8vw, 17px);
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
  font-size: 24px;
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
.baznas-section.soft-bg > .matrix-grid {
  max-width: 1200px;
  margin-left: auto;
  margin-right: auto;
}

.section-head {
  text-align: center;
  max-width: 780px;
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

/* ── CAROUSEL PRESENTATION SECTION ─────────────────── */
.pres-tabs-wrap {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
  margin-bottom: 24px;
}

@media (max-width: 768px) {
  .pres-tabs-wrap {
    grid-template-columns: 1fr;
  }
}

.pres-tab-btn {
  background: #ffffff;
  border: 2px solid #e2e8f0;
  border-radius: 16px;
  padding: 20px 24px;
  text-align: left;
  cursor: pointer;
  transition: all 0.25s ease;
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.pres-tab-btn:hover {
  border-color: #059669;
  transform: translateY(-2px);
}

.pres-tab-btn.active {
  border-color: #059669;
  background: #f0fdf4;
  box-shadow: 0 10px 25px -5px rgba(5, 150, 105, 0.15);
}

.tab-badge {
  font-family: var(--font-mono, monospace);
  font-size: 11px;
  font-weight: 800;
  color: #059669;
  text-transform: uppercase;
}

.tab-title {
  font-family: var(--font-display, serif);
  font-size: 17px;
  font-weight: 700;
  color: #0f172a;
  line-height: 1.3;
}

.tab-meta {
  font-size: 12px;
  color: #64748b;
  font-weight: 500;
}

.carousel-container {
  background: #ffffff;
  border: 1px solid #e2e8f0;
  border-radius: 24px;
  overflow: hidden;
  box-shadow: 0 20px 50px rgba(15, 23, 42, 0.08);
}

.pres-info-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 18px 24px;
  background: #0f172a;
  color: #ffffff;
  flex-wrap: wrap;
  gap: 12px;
}

.pib-left {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.pib-presenter {
  font-size: 14px;
  font-weight: 700;
  color: #f8fafc;
}

.pib-role {
  font-size: 12px;
  color: #94a3b8;
}

.pib-actions {
  display: flex;
  gap: 10px;
  align-items: center;
  flex-wrap: wrap;
}

.btn-download {
  background: linear-gradient(135deg, #10b981 0%, #059669 100%);
  color: #ffffff;
  padding: 8px 18px;
  border-radius: 8px;
  font-size: 13px;
  font-weight: 700;
  text-decoration: none;
  transition: all 0.2s ease;
  box-shadow: 0 4px 12px rgba(16, 185, 129, 0.4);
}

.btn-download:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(16, 185, 129, 0.6);
}

.btn-toggle-view {
  background: rgba(255, 255, 255, 0.1);
  color: #e2e8f0;
  border: 1px solid rgba(255, 255, 255, 0.2);
  padding: 8px 14px;
  border-radius: 8px;
  font-size: 12px;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.2s;
}

.btn-toggle-view:hover {
  background: rgba(255, 255, 255, 0.2);
}

.slide-display-stage {
  position: relative;
  background: #090d16;
  padding: 30px 20px 80px;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 480px;
}

.canvas-wrapper {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.slide-canvas {
  max-width: 100%;
  height: auto;
  border-radius: 12px;
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.6);
  background: #ffffff;
}

.rendering-overlay {
  position: absolute;
  inset: 0;
  background: rgba(9, 13, 22, 0.7);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 12px;
  color: #ffffff;
  font-size: 14px;
  font-weight: 600;
  z-index: 5;
  border-radius: 12px;
}

.render-spinner {
  width: 36px;
  height: 36px;
  border: 3px solid rgba(16, 185, 129, 0.2);
  border-top-color: #10b981;
  border-radius: 50%;
  animation: spin 0.8s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

.embed-wrapper {
  width: 100%;
  height: 600px;
}

.pdf-iframe {
  width: 100%;
  height: 100%;
  border: none;
  border-radius: 12px;
}

.carousel-nav-controls {
  position: absolute;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  align-items: center;
  gap: 14px;
  background: rgba(15, 23, 42, 0.9);
  backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 999px;
  padding: 8px 18px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
  z-index: 10;
}

.nav-btn {
  background: #10b981;
  color: #ffffff;
  border: none;
  padding: 8px 16px;
  border-radius: 999px;
  font-size: 13px;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.2s ease;
}

.nav-btn:hover:not(:disabled) {
  background: #059669;
  transform: scale(1.05);
}

.nav-btn:disabled {
  opacity: 0.4;
  cursor: not-allowed;
}

.page-indicator {
  color: #e2e8f0;
  font-size: 13px;
  display: flex;
  gap: 4px;
  align-items: center;
}

.page-indicator strong {
  color: #34d399;
  font-family: var(--font-mono, monospace);
  font-size: 15px;
}

.thumbnails-bar {
  background: #f1f5f9;
  padding: 14px 20px;
  display: flex;
  align-items: center;
  gap: 12px;
  overflow-x: auto;
  border-bottom: 1px solid #e2e8f0;
}

.thumb-label {
  font-size: 12px;
  font-weight: 700;
  color: #475569;
  white-space: nowrap;
}

.thumb-chips {
  display: flex;
  gap: 6px;
  overflow-x: auto;
  padding-bottom: 4px;
}

.thumb-chip {
  width: 32px;
  height: 32px;
  flex-shrink: 0;
  border-radius: 8px;
  border: 1px solid #cbd5e1;
  background: #ffffff;
  color: #334155;
  font-size: 12px;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.2s ease;
}

.thumb-chip:hover {
  border-color: #059669;
  color: #059669;
}

.thumb-chip.active {
  background: #059669;
  color: #ffffff;
  border-color: #059669;
  box-shadow: 0 2px 8px rgba(5, 150, 105, 0.3);
}

.pres-summary-box {
  padding: 28px;
  background: #ffffff;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.ps-header h3 {
  font-family: var(--font-display, serif);
  font-size: 18px;
  font-weight: 700;
  color: #0f172a;
  margin: 0 0 8px 0;
}

.ps-header p {
  font-size: 14px;
  color: #475569;
  line-height: 1.65;
  margin: 0;
}

.ps-topics h4 {
  font-size: 13px;
  font-weight: 700;
  color: #0f172a;
  margin: 0 0 10px 0;
}

.topic-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.topic-tag {
  background: #ecfdf5;
  color: #065f46;
  border: 1px solid #a7f3d0;
  font-size: 12px;
  font-weight: 600;
  padding: 5px 12px;
  border-radius: 8px;
}

/* ── MATRIX SECTION ─────────────────────────────────── */
.matrix-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 24px;
}

.matrix-card {
  background: #ffffff;
  border: 1px solid #e2e8f0;
  border-radius: 20px;
  padding: 28px;
  display: flex;
  flex-direction: column;
  gap: 14px;
  box-shadow: 0 4px 18px rgba(15, 23, 42, 0.04);
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}

.matrix-card:hover {
  transform: translateY(-5px);
  border-color: #10b981;
  box-shadow: 0 18px 40px rgba(16, 185, 129, 0.1);
}

.mc-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.mc-num {
  font-family: var(--font-mono, monospace);
  font-size: 11px;
  font-weight: 800;
  color: #059669;
  text-transform: uppercase;
}

.mc-badge {
  background: #dcfce7;
  color: #15803d;
  font-family: var(--font-mono, monospace);
  font-size: 11px;
  font-weight: 700;
  padding: 3px 10px;
  border-radius: 999px;
}

.mc-task {
  font-family: var(--font-display, serif);
  font-size: 17px;
  font-weight: 700;
  color: #0f172a;
  line-height: 1.35;
  margin: 0;
}

.mc-evidence {
  font-size: 13px;
  color: #475569;
  line-height: 1.6;
  background: #f8fafc;
  padding: 12px 16px;
  border-radius: 12px;
  border-left: 3px solid #059669;
}

.mc-evidence strong {
  display: block;
  color: #0f172a;
  margin-bottom: 4px;
}

.mc-evidence p {
  margin: 0;
}

/* ── FILTER & RESEARCH SECTION ──────────────────────── */
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

/* ── CTA SECTION ────────────────────────────────────── */
.baznas-cta-section {
  background: linear-gradient(135deg, #022c22 0%, #064e3b 50%, #0f766e 100%);
  color: #ffffff;
  padding: 80px 24px;
  text-align: center;
}

.cta-inner {
  max-width: 760px;
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
  gap: 14px;
  flex-wrap: wrap;
}
</style>
