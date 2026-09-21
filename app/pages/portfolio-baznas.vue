<script setup lang="ts">
import { ref, computed, onMounted, watch } from 'vue'

useHead({
  title: 'Portofolio Riset BAZNAS & Materi Paparan Pimpinan — Arva Athallah Susanto',
  meta: [
    {
      name: 'description',
      content: 'Portofolio akademik, materi presentasi eksekutif pimpinan, publikasi Google Scholar, pengelolaan OJS Journal MASEI Al-Khawarizmi, dan International Journal of Zakat (IJAZ) oleh Arva Athallah Susanto, S.EI., M.SEI.'
    },
    {
      name: 'keywords',
      content: 'BAZNAS RI, Staf Riset dan Kajian Pengembangan, MASEI Al Khawarizmi, OJS 3, IJAZ BAZNAS, Google Scholar Arva Athallah Susanto, SROI Zakat, ZCP BAZNAS, Gaya Hidup Halal'
    },
    {
      property: 'og:title',
      content: 'Portofolio Riset BAZNAS & Materi Paparan Pimpinan — Arva Athallah Susanto'
    },
    {
      property: 'og:description',
      content: 'Koleksi materi presentasi pimpinan, 22+ publikasi Google Scholar, tim redaksi OJS MASEI, dan kompetensi riset BAZNAS RI.'
    }
  ]
})

// ── PRESENTATION CAROUSEL STATE ─────────────────────────
interface Presentation {
  id: string
  title: string
  categoryBadge: string
  subtitle: string
  creator: string
  designedFor: string
  institution: string
  totalPages: number
  pdfUrl: string
  fileSize: string
  date: string
  summary: string
  keyTopics: string[]
}

const presentations: Presentation[] = [
  {
    id: 'presentation-1',
    title: 'Islamic Economics for Economic Resilience and Welfare',
    categoryBadge: 'Materi Eksekutif #01',
    subtitle: 'Kajian Fikih Muamalah, Sukuk, dan Zakat sebagai Instrumen Fiskal Negara',
    creator: 'Arva Athallah Susanto, S.EI., M.SEI',
    designedFor: 'Prof. Dr. Tika Widiastuti, S.E., M.Si',
    institution: 'Wakil Dekan I FEB Universitas Airlangga & Guru Besar Keuangan Sosial Islam',
    totalPages: 26,
    pdfUrl: '/documents/islamic-economics-resilience-welfare-arva.pdf',
    fileSize: '2.9 MB (26 Slide)',
    date: '2026',
    summary: 'Materi presentasi tingkat pimpinan yang merumuskan integrasi Fikih Muamalah sebagai solusi alternatif ekonomi konvensional. Membahas skema penerbitan dan investasi Sukuk untuk sektor riil, zakat sebagai instrumen fiskal negara (komparasi Indonesia, Malaysia, Arab Saudi, Kuwait, Turki, Singapura), model pemberdayaan berbasis potensi mustahik (Azis et al.), serta pergeseran indikator keberhasilan dari GDP konvensional menuju Falah.',
    keyTopics: [
      'Fikih-Muamalah Based Alternatives vs Conventional Instruments',
      'Sukuk Process Scheme & Real Sector Capital Circulation',
      'Zakat as Islamic Fiscal Instrument across 6 Global Countries',
      'Productive Zakat & Mustahik Potential Model (Azis et al., 2017)',
      'Zakat-Waqf Integration Framework (+12% Welfare Improvement)',
      'Paradigm Shift: From GDP to Holistic Falah Indicators'
    ]
  },
  {
    id: 'presentation-2',
    title: 'Program Pemberdayaan Terukur, Terencana, dan Berdampak',
    categoryBadge: 'Materi Eksekutif #02',
    subtitle: 'Tata Kelola ZCP BAZNAS, BMC Sentra Ternak, dan Kaji Dampak SROI',
    creator: 'Arva Athallah Susanto, S.EI., M.SEI',
    designedFor: 'Prof. Dr. Tika Widiastuti, S.E., M.Si',
    institution: 'Senior Expert Center of Islamic Social Finance (CISF) & Guru Besar FEB UNAIR',
    totalPages: 27,
    pdfUrl: '/documents/program-pemberdayaan-terukur-cisf-arva.pdf',
    fileSize: '9.0 MB (27 Slide)',
    date: '2026',
    summary: 'Materi strategis perancangan program pemberdayaan ZISWAF berbasis bukti empiris dan regulasi nasional. Membedah kinerja zakat nasional (DEKS BI), RPJPN 2025-2045, regulasi UU 23/2011 & PP 14/2014, Zakat Core Principles (ZCP 7 & ZCP 8 BAZNAS), Business Model Canvas (BMC) Zakat Sentra Ternak Puskas BAZNAS, Social Return on Investment (SROI) Value Map, Indeks Desa Zakat, Indeks Kifayah, Indeks Kesejahteraan BAZNAS, dan Model Transformasi 4 ER (Rescue, Recovery, Reinforcement, Resilience).',
    keyTopics: [
      'Kinerja Ekonomi Syariah Nasional & Arah Zakat RPJPN 2025-2045',
      'Regulasi UU 23/2011 & Standar Zakat Core Principles (ZCP 7-8)',
      '7 Tahap Perancangan Program & Business Model Canvas (BMC)',
      'Metodologi Kaji Dampak Social Return on Investment (SROI)',
      'Indeks Desa Zakat, Indeks Kifayah & Indeks Kesejahteraan BAZNAS',
      'Model 4 ER: Transformasi Mustahik Menjadi Muzakki'
    ]
  },
  {
    id: 'presentation-3',
    title: 'Gaya Hidup Halal & Ekosistem Industri Halal Nasional',
    categoryBadge: 'Materi Eksekutif #03',
    subtitle: 'Lanskap Global SGIE, Regulasi BPJPH, dan Digital Branding Produk Halal',
    creator: 'Arva Athallah Susanto, S.EI., M.SEI',
    designedFor: 'Prof. Dr. Tika Widiastuti, S.E., M.Si',
    institution: 'Masyarakat Ekonomi Syariah (MES) Jawa Timur & FEB Universitas Airlangga',
    totalPages: 21,
    pdfUrl: '/documents/gaya-hidup-halal-mes-arva.pdf',
    fileSize: '4.7 MB (21 Slide)',
    date: '2026',
    summary: 'Materi paparan eksekutif komprehensif mengenai akselerasi ekonomi dan gaya hidup halal di Indonesia. Membahas skor State of the Global Islamic Economy (SGIE), ekosistem rantai pasok industri halal (KNEKS), regulasi mandatori sertifikasi halal (UU 33/2014 & Perpres 153/2024), titik kritis halal produk dan fasilitas produksi, literasi keuangan syariah (OJK), hingga strategi digital branding dan verifikasi halal berbasis aplikasi digital.',
    keyTopics: [
      'Global Islamic Economic Indicator (SGIE) Ranking & Outlook',
      'Ruang Lingkup & Rantai Pasok Industri Halal (KNEKS Framework)',
      'Regulasi Mandatori Sertifikasi Halal BPJPH & UU No. 33/2014',
      'Analisis Titik Kritis Bahan Baku, Proses Produksi & Distribusi',
      'Tingkat Literasi & Inklusi Keuangan Syariah Nasional (OJK)',
      'Strategi Digital Halal Branding, E-Commerce, & Aplikasi Verifikasi'
    ]
  },
  {
    id: 'presentation-4',
    title: 'Pentingnya Ketenangan Hati di Tengah Kesibukan Akademik',
    categoryBadge: 'Materi Eksekutif #04',
    subtitle: 'Manajemen Stres Akademik, Produktivitas Berimbang, dan Pendekatan Spiritual',
    creator: 'Arva Athallah Susanto, S.EI., M.SEI',
    designedFor: 'Prof. Dr. Tika Widiastuti, S.E., M.Si',
    institution: 'Wakil Dekan I FEB Universitas Airlangga',
    totalPages: 25,
    pdfUrl: '/documents/pentingnya-ketenangan-hati-arva.pdf',
    fileSize: '1.5 MB (25 Slide)',
    date: '6 Agustus 2026',
    summary: 'Materi orasi dan pembinaan sivitas akademika bertema kesehatan mental dan ketenangan spiritual dalam dunia akademik. Membedah data statistik stres akademik mahasiswa, dampak psikologis dan sosial dari beban studi, strategi manajemen waktu, mindfulness & latihan pernapasan, penataan lingkungan belajar, serta kiat praktis meraih prestasi optimal melalui ketenangan batin yang berlandaskan nilai-nilai spiritualitas Islam.',
    keyTopics: [
      'Dinamika Tekanan & Statistik Stres di Lingkungan Akademik',
      'Korelasi Ketenangan Hati terhadap Fokus & Daya Ingat',
      'Strategi Manajemen Waktu Terstruktur & Skala Prioritas',
      'Praktik Mindfulness, Relaksasi & Pola Hidup Sehat Mahasiswa',
      'Studi Kasus: Transformasi Akademik melalui Ketenangan Pikiran',
      'Integrasi Keseimbangan Emosional dan Nilai Spiritualitas'
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

  window.addEventListener('keydown', (e) => {
    if (e.key === 'ArrowRight') nextPage()
    if (e.key === 'ArrowLeft') prevPage()
  })
})

// ── BAZNAS JOB REQUIREMENTS ALIGNMENT MATRIX ────────────
const jobMatrix = [
  {
    number: '01',
    roleTask: 'Melakukan riset, kajian, dan pengembangan mengenai zakat',
    evidence: 'Publikasi di International Journal of Zakat (IJAZ - BAZNAS), pemodelan ekonometrika ARDL makroekonomi zakat, dan kajian transformasi 4 ER (Rescue, Recovery, Reinforcement, Resilience).',
    link: 'https://scholar.google.com/citations?user=7gI4mGYAAAAJ&hl=id',
    linkText: 'Lihat Sitasi Scholar →',
    statusBadge: '100% Terpenuhi'
  },
  {
    number: '02',
    roleTask: 'Membuat materi untuk Pimpinan BAZNAS',
    evidence: 'Rekam jejak terbukti dalam menyusun 4 set materi presentasi strategis tingkat pimpinan sivitas akademika & pakar (Prof. Dr. Tika Widiastuti) dengan standar substansi akademik dan visual berkualitas tinggi.',
    link: '#presentation-carousel',
    linkText: 'Buka Carousel Materi Pimpinan ↓',
    statusBadge: '100% Terpenuhi'
  },
  {
    number: '03',
    roleTask: 'Melakukan administrasi yang mendukung kegiatan riset & kajian',
    evidence: 'Pengalaman sebagai Research Consultant di Center of Islamic Social Finance (CISF) dan Research Assistant Guru Besar Keuangan Sosial Islam (Prof. Dr. Tika Widiastuti).',
    link: 'https://www.cisf.or.id',
    linkText: 'Kunjungi CISF →',
    statusBadge: '100% Terpenuhi'
  },
  {
    number: '04',
    roleTask: 'Mengelola jurnal IJAZ (International Journal of Zakat) & Pengelolaan Jurnal Ilmiah OJS',
    evidence: 'Tim Redaksi (Editorial Office & IT Infrastructure) di Journal MASEI Al-Khawarizmi (journal.masei.or.id), bertanggung jawab penuh memastikan infrastruktur server, OJS 3.4.0.8, alur peer-review, submission, dan OJS berjalan dengan sempurna. Sekaligus merupakan penulis aktif di International Journal of Zakat (IJAZ - BAZNAS).',
    link: 'https://journal.masei.or.id/al-khawarizmi/about/contact',
    linkText: 'Cek SK & Kontak Redaksi OJS MASEI →',
    statusBadge: '100% Terpenuhi'
  },
  {
    number: '05',
    roleTask: 'Pengoperasian tools riset & kemampuan analisis ilmiah',
    evidence: 'Mahir mengoperasikan VOSviewer, SmartPLS (PLS-SEM), EViews/Stata (ARDL), Systematic Literature Review (PRISMA), dan analisis SROI Value Map.',
    link: '#scholar-section',
    linkText: 'Lihat Publikasi Riset ↓',
    statusBadge: '100% Terpenuhi'
  }
]

// ── GOOGLE SCHOLAR REPOSITORY (22 ARTICLES) ──────────────
interface ScholarArticle {
  title: string
  authors: string
  publication: string
  year: string
  citations: string
  link: string
  badge?: string
}

const scholarArticles: ScholarArticle[] = [
  {
    title: "How Islamic Leadership and Islamic Worldview Play a Role in Restoring a Country's Economic Glory: Bibliometrical Analysis",
    authors: "AA Susanto, A Suprayitno, S Zulaikha, AK Wardhana",
    publication: "Jurnal Transformatif (Islamic Studies) 9 (1), 40-56",
    year: "2025",
    citations: "13",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:4DMP91E08xMC",
    badge: "13 Sitasi • SINTA 2"
  },
  {
    title: "Critical assessment of blockchain applications in zakat literature: Lessons for government and future directions",
    authors: "AA Susanto",
    publication: "International Journal of Zakat (IJAZ - BAZNAS) 10 (1), 80-98",
    year: "2025",
    citations: "9",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:Wp0gIr-vW9MC",
    badge: "Publikasi IJAZ BAZNAS"
  },
  {
    title: "Digital Transformation in Zakat Management: A Bibliometric Review on the Application of Blockchain Technology",
    authors: "AA Susanto, N Asya'bani, CF Rizal, M Oktari",
    publication: "iBAF e-Proceedings 11 (1), 768-790",
    year: "2024",
    citations: "9",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:dhFuZR0502QC",
    badge: "International Proceeding"
  },
  {
    title: "Navigating the future: The impact of AI on Islamic economic policy in the digital age",
    authors: "N Asya'bani, AA Susanto, SK Indirwan, AB Robani",
    publication: "Review of Islamic Economics and Finance 8 (1), 125-150",
    year: "2025",
    citations: "6",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:mVmsd5A6BfQC",
    badge: "AI & Islamic Policy"
  },
  {
    title: "Long term nexus between digitalization and macroeconomy on zakat collection in Indonesia",
    authors: "A Suprayitno, W Hawariyuni, WA Pratomo, WS Hasibuan, M Andrasari, AA Susanto",
    publication: "Review of Islamic Social Finance and Entrepreneurship, 141-153",
    year: "2025",
    citations: "3",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:ZeXyd9-uunAC",
    badge: "Ekonometrika ARDL"
  },
  {
    title: "Pengaruh Literasi Keuangan dan Pendapatan Perkapita Terhadap Konsumsi Rumah Tangga Di Indonesia: Analisis Ekonomi Islam",
    authors: "A Wahab, A Suprayitno, AA Susanto, S Rusgianto",
    publication: "Jurnal Ekonomika dan Bisnis Islam 8 (2), 20-35",
    year: "2025",
    citations: "3",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:hFOr9nPyWt4C",
    badge: "Ekonomi Makro Islam"
  },
  {
    title: "Toward the future of the halal industry: exploring perceptions and halal awareness among poultry slaughterhouse business practitioners",
    authors: "L Hikmah, TD Pertiwi, M Cholil, AA Susanto, M Soleh, T Widiastuti",
    publication: "Journal of Halal Product and Research 8 (1), 75-89",
    year: "2025",
    citations: "3",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:7PzlFSSx8tAC",
    badge: "Halal Industry & BPJPH"
  },
  {
    title: "TWO DECADES OF ISLAMIC LEADERSHIP AND ISLAMIC WORK ETHICS IMPLEMENTATION: BIBLIOMETRIC ANALYSIS",
    authors: "A Suprayitno, AA Susanto, A Wahab",
    publication: "Jurnal EL-RIYASAH 16 (1), 40-59",
    year: "2025",
    citations: "2",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:9ZlFYXVOiuMC",
    badge: "Bibliometric VOSviewer"
  },
  {
    title: "Sustainability of Islamic Bank Financing across Macroeconomic and Internal Factors",
    authors: "A Suprayitno, AA Susanto, W Hawariyuni",
    publication: "Journal of Sustainable Economics 2 (2), 83-93",
    year: "2024",
    citations: "2",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:hqOjcs7Dif8C",
    badge: "Islamic Banking Sustainability"
  },
  {
    title: "A Bibliometric-Systematic Review of Digital Transformation in Indonesia's Economic Development",
    authors: "AA Susanto, J Lu, A Suprayitno, NH Hadi",
    publication: "Journal of Advances in Information and Industrial Technology 8 (1), 145-160",
    year: "2026",
    citations: "1",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:iH-uZ7U-co4C",
    badge: "Systematic Review (SLR)"
  },
  {
    title: "Unlocking Amil performance: Leadership, knowledge management capability, and organizational culture",
    authors: "N Asya'bani, S Rusgianto, RT Ratnasari, MNH Ryandono, AA Susanto",
    publication: "Asian Journal of Islamic Management (AJIM), 133-153",
    year: "2025",
    citations: "1",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:QIV2ME_5wuYC",
    badge: "Tata Kelola Amil OPZ"
  },
  {
    title: "The Influence of Corporate Social Responsibility on Consumer Happiness and Brand Love",
    authors: "NH Hadi, HA Al-Giffari, AA Susanto",
    publication: "IJBEG: International Journal of Business and Economic Growth 1 (01), 78-99",
    year: "2026",
    citations: "0",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:NMxIlDl6LWMC",
    badge: "CSR & Social Impact"
  },
  {
    title: "Islamic Financial Regulations, Islamic Financial Literacy and Financial Inclusion: Insights from ASEAN",
    authors: "AA Susanto, S Rusgianto, T Widiastuti",
    publication: "SAUJANA: Jurnal Perbankan Syariah dan Ekonomi Syariah 8 (3), 606-630",
    year: "2026",
    citations: "0",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:hMod-77fHWUC",
    badge: "Regulasi Finansial ASEAN"
  },
  {
    title: "The Anthropology of Modernity: Four Lessons from Surah Al-Kahf",
    authors: "AA Susanto",
    publication: "Center of Islamic Social Finance (CISF) Academic Notes",
    year: "2026",
    citations: "0",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:maZDTaKrznsC",
    badge: "Islamic Worldview"
  },
  {
    title: "Stabilitas Bank Syariah Vs Bank Konvensional: Mana Yang Lebih Tangguh?",
    authors: "AR Rafli, AF Hady, R Indrarini, AA Susanto",
    publication: "WADIAH 10 (2), 90-114",
    year: "2026",
    citations: "0",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:isC4tDSrTZIC",
    badge: "Stabilitas Perbankan"
  },
  {
    title: "Pengaruh Zakat terhadap Pertumbuhan Ekonomi di Negara-Negara OKI: Peran Moderasi Kualitas Institusi dan Tantangan Digitalisasi",
    authors: "AA Susanto, S Rusgianto, T Widiastuti",
    publication: "SAUJANA: Jurnal Perbankan Syariah dan Ekonomi Syariah 8 (1), 197-213",
    year: "2026",
    citations: "0",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:j3f4tGmQtD8C",
    badge: "Zakat Makro OKI"
  },
  {
    title: "MISSION-DRIVEN HRM IN NON-PROFIT ORGANISATION: A SYSTEMATIC REVIEW OF PLANNING PRACTICES AND CHALLENGES",
    authors: "BNM Ulum, T Widiastuti, A Prasetyo, A Athallah",
    publication: "Airlangga International Journal of Islamic Economics & Finance 9 (1), 1",
    year: "2026",
    citations: "0",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:bEWYMUwI8FkC",
    badge: "HRM Lembaga Nirlaba"
  },
  {
    title: "PENGARUH HUMAN CAPITAL, ECONOMIC FREEDOM, DAN CAPITAL FORMATION TERHADAP PEMBANGUNAN EKONOMI ISLAM DI NEGARA-NEGARA OKI",
    authors: "S Indirwan, AA Susanto, S Herianingrum, T Widiastuti, AB Robani",
    publication: "Jurnal Ekonomika dan Bisnis Islam 8 (3), 1-23",
    year: "2025",
    citations: "0",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:_Qo2XoVZTnwC",
    badge: "Pembangunan Ekonomi OKI"
  },
  {
    title: "What Islamic Economics Can Teach the West About Fiscal Trust",
    authors: "AA Susanto",
    publication: "CISF Working Paper & International Public Economics Series",
    year: "2025",
    citations: "0",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:qUcmZB5y_30C",
    badge: "Fiscal Trust & Ethics"
  },
  {
    title: "Faktor-Faktor Yang Menyebabkan Herding Behavior Di Kalangan Investor Saham Syariah Indonesia",
    authors: "AA Susanto",
    publication: "Skripsi Sarjana Ekonomi Islam, Universitas Airlangga",
    year: "2022",
    citations: "0",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:k_IJM867U9cC",
    badge: "Skripsi Cum Laude S1"
  },
  {
    title: "From Readiness to Performance: Examining Blockchain Integration in Financial Services and Its Effects on Transparency and Efficiency",
    authors: "A Alsmadi, RW Al-Smadi (Peer-Reviewed: AA Susanto)",
    publication: "Frontiers in Blockchain 9, 1891070",
    year: "2026",
    citations: "0",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:blknAaTinKkC",
    badge: "Frontiers Peer Reviewer"
  },
  {
    title: "Algorithmic Trust and the Future of Money: A Dynamic General Equilibrium Framework for AI-Governed Digital Currencies",
    authors: "AA Susanto",
    publication: "Theoretical Working Paper in Computational Economics",
    year: "2026",
    citations: "0",
    link: "https://scholar.google.com/citations?view_op=view_citation&hl=id&oe=ASCII&user=7gI4mGYAAAAJ&pagesize=100&citation_for_view=7gI4mGYAAAAJ:TQgYirikUcIC",
    badge: "AI & Computational Macro"
  }
]

const searchQuery = ref('')
const scholarCategory = ref('Semua')

const filteredScholarArticles = computed(() => {
  return scholarArticles.filter(art => {
    const matchSearch = art.title.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
                        art.authors.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
                        art.publication.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
                        art.year.includes(searchQuery.value)
    
    if (scholarCategory.value === 'Semua') return matchSearch
    if (scholarCategory.value === 'Zakat & ZISWAF') {
      return matchSearch && (art.title.toLowerCase().includes('zakat') || art.badge?.toLowerCase().includes('zakat') || art.title.toLowerCase().includes('amil'))
    }
    if (scholarCategory.value === 'Blockchain & AI') {
      return matchSearch && (art.title.toLowerCase().includes('blockchain') || art.title.toLowerCase().includes('ai') || art.title.toLowerCase().includes('digital'))
    }
    if (scholarCategory.value === 'Perbankan & Sukuk') {
      return matchSearch && (art.title.toLowerCase().includes('bank') || art.title.toLowerCase().includes('financial') || art.title.toLowerCase().includes('sustainability'))
    }
    if (scholarCategory.value === 'Halal Industry') {
      return matchSearch && (art.title.toLowerCase().includes('halal') || art.badge?.toLowerCase().includes('halal'))
    }
    return matchSearch
  })
})

const verticalCarouselRef = ref<HTMLElement | null>(null)

function scrollCarousel(direction: 'up' | 'down') {
  if (!verticalCarouselRef.value) return
  const scrollAmount = 280
  verticalCarouselRef.value.scrollBy({
    top: direction === 'down' ? scrollAmount : -scrollAmount,
    behavior: 'smooth'
  })
}
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
          Portofolio Riset &amp; Materi Paparan Pimpinan <span class="highlight-text">BAZNAS RI</span>
        </h1>

        <p class="hero-description">
          Dokumentasi karya ilmiah, <strong>22+ Publikasi Google Scholar</strong>, materi presentasi eksekutif pimpinan, 
          pengelolaan OJS <strong>Journal MASEI Al-Khawarizmi</strong>, serta pemenuhan kualifikasi 
          <strong>Staf Riset dan Kajian Pengembangan BAZNAS RI</strong> oleh 
          <strong>Arva Athallah Susanto, S.EI., M.SEI</strong>.
        </p>

        <!-- Elegant Executive Attribution Notice -->
        <div class="executive-notice-box">
          <div class="enb-icon">✨</div>
          <div class="enb-content">
            <h4>Materi Paparan Strategis Pimpinan</h4>
            <p>
              Seluruh materi presentasi eksekutif pada portofolio ini disusun dan dikembangkan secara komprehensif oleh 
              <strong>Arva Athallah Susanto, S.EI., M.SEI</strong> guna mendukung penyampaian materi, kuliah pakar, 
              serta forum kebijakan strategis <strong>Prof. Dr. Tika Widiastuti, S.E., M.Si</strong> 
              <em>(Wakil Dekan I FEB Universitas Airlangga &amp; Guru Besar Keuangan Sosial Islam)</em>.
            </p>
          </div>
        </div>

        <div class="hero-cta-group">
          <a href="#presentation-carousel" class="baznas-btn primary">
            📊 Jelajahi 4 Materi Presentasi Pimpinan ↓
          </a>
          <a href="#job-matrix" class="baznas-btn secondary">
            📋 Matriks Kualifikasi BAZNAS RI
          </a>
          <a href="#scholar-section" class="baznas-btn secondary">
            📚 22+ Publikasi Google Scholar ↓
          </a>
        </div>

        <!-- Metric Highlight Bar -->
        <div class="metric-ribbon">
          <div class="metric-item">
            <span class="metric-number">22+</span>
            <span class="metric-label">Publikasi Google Scholar</span>
          </div>
          <div class="metric-sep"></div>
          <div class="metric-item">
            <span class="metric-number">4 Set</span>
            <span class="metric-label">Materi Paparan Pimpinan</span>
          </div>
          <div class="metric-sep"></div>
          <div class="metric-item">
            <span class="metric-number">OJS 3.4</span>
            <span class="metric-label">Redaksi Journal MASEI Al-Khawarizmi</span>
          </div>
          <div class="metric-sep"></div>
          <div class="metric-item">
            <span class="metric-number">IJAZ</span>
            <span class="metric-label">Penulis Jurnal Resmi BAZNAS</span>
          </div>
        </div>
      </div>
    </section>

    <!-- ── INTERACTIVE PRESENTATION CAROUSEL (PDF SLIDE VIEWER) ── -->
    <section id="presentation-carousel" class="baznas-section">
      <div class="section-head">
        <p class="section-kicker">Executive Presentation &amp; Policy Materials</p>
        <h2>Carousel Materi Riset &amp; Paparan Pimpinan</h2>
        <p class="section-sub">
          Koleksi 4 set materi presentasi tingkat pimpinan yang dirancang untuk forum strategis, kuliah umum pakar, dan kajian kebijakan publik. 
          Dapat dijelajahi slide demi slide secara interaktif maupun diunduh dalam format PDF asli.
        </p>
      </div>

      <!-- Presentation Selector Tabs (4 Tabs) -->
      <div class="pres-tabs-wrap">
        <button
          v-for="(pres, pIdx) in presentations"
          :key="pres.id"
          class="pres-tab-btn"
          :class="{ active: selectedPresIndex === pIdx }"
          @click="selectPresentation(pIdx)"
        >
          <div class="tab-top-row">
            <span class="tab-badge">{{ pres.categoryBadge }}</span>
            <span class="tab-date">📅 {{ pres.date }}</span>
          </div>
          <span class="tab-title">{{ pres.title }}</span>
          <span class="tab-meta">{{ pres.fileSize }}</span>
        </button>
      </div>

      <!-- Carousel Viewer Main Box -->
      <div class="carousel-container">
        <!-- Presentation Header Info Bar with Elegant Attribution -->
        <div class="pres-info-bar">
          <div class="pib-left">
            <div class="pib-attribution-badge">
              <span class="badge-creator">Disusun oleh: <strong>{{ currentPresentation.creator }}</strong></span>
              <span class="badge-arrow">➔</span>
              <span class="badge-target">Untuk: <strong>{{ currentPresentation.designedFor }}</strong></span>
            </div>
            <span class="pib-role">🏛️ {{ currentPresentation.institution }}</span>
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
            <h4>Poin-Poin Pokok yang Disajikan:</h4>
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
          Pemetaan kompetensi akademik, penguasaan materi pimpinan, pengelolaan infrastruktur OJS, dan portofolio Arva Athallah Susanto terhadap 
          kebutuhan formasi <strong>Staf Riset dan Kajian Pengembangan — BAZNAS RI</strong>.
        </p>
      </div>

      <div class="matrix-grid">
        <article v-for="item in jobMatrix" :key="item.number" class="matrix-card">
          <div class="mc-top">
            <span class="mc-num">Kualifikasi Poin #{{ item.number }}</span>
            <span class="mc-badge">{{ item.statusBadge }}</span>
          </div>
          <h3 class="mc-task">"{{ item.roleTask }}"</h3>
          <div class="mc-evidence">
            <strong>Bukti Portofolio &amp; Rekam Jejak:</strong>
            <p>{{ item.evidence }}</p>
          </div>
          <div class="mc-footer">
            <a :href="item.link" target="_blank" class="mc-link">{{ item.linkText }}</a>
          </div>
        </article>
      </div>
    </section>

    <!-- ── VERTICAL SCHOLAR CAROUSEL SECTION (22+ ARTICLES) ── -->
    <section id="scholar-section" class="baznas-section">
      <div class="section-head">
        <p class="section-kicker">Google Scholar Academic Repository</p>
        <h2>Koleksi 22+ Publikasi Ilmiah Google Scholar</h2>
        <p class="section-sub">
          Daftar lengkap artikel jurnal, prosiding internasional, dan working paper karya 
          <strong>Arva Athallah Susanto</strong> yang terindeks resmi di Google Scholar.
        </p>
      </div>

      <!-- Search & Category Filters -->
      <div class="scholar-controls-wrap">
        <div class="scholar-search-box">
          <span class="search-icon">🔍</span>
          <input
            v-model="searchQuery"
            type="text"
            placeholder="Cari judul artikel, penulis, atau kata kunci..."
            class="scholar-input"
          />
          <button v-if="searchQuery" class="clear-search" @click="searchQuery = ''">✕</button>
        </div>

        <div class="scholar-filter-pills">
          <button
            v-for="cat in ['Semua', 'Zakat & ZISWAF', 'Blockchain & AI', 'Perbankan & Sukuk', 'Halal Industry']"
            :key="cat"
            class="filter-pill"
            :class="{ active: scholarCategory === cat }"
            @click="scholarCategory = cat"
          >
            {{ cat }}
          </button>
        </div>
      </div>

      <!-- Vertical Carousel Container -->
      <div class="vertical-carousel-wrapper">
        <!-- Floating Navigation Arrow Controls -->
        <div class="vc-header-bar">
          <div class="vc-stat">
            Menampilkan <strong>{{ filteredScholarArticles.length }}</strong> dari <strong>{{ scholarArticles.length }}</strong> Publikasi
          </div>
          <div class="vc-nav-btns">
            <button class="vc-nav-btn" @click="scrollCarousel('up')" title="Scroll ke Atas">▲ Atas</button>
            <button class="vc-nav-btn" @click="scrollCarousel('down')" title="Scroll ke Bawah">▼ Bawah</button>
          </div>
        </div>

        <!-- Scrollable Vertical Feed (Carousel Kebawah) -->
        <div ref="verticalCarouselRef" class="vertical-carousel-feed">
          <article
            v-for="(art, aIdx) in filteredScholarArticles"
            :key="art.link + aIdx"
            class="scholar-feed-card"
          >
            <div class="sfc-meta-row">
              <span class="sfc-index">#{{ aIdx + 1 }}</span>
              <span v-if="art.badge" class="sfc-badge">{{ art.badge }}</span>
              <span v-if="art.year" class="sfc-year">📅 {{ art.year }}</span>
              <span v-if="art.citations !== '0'" class="sfc-cites">⭐ {{ art.citations }} Sitasi</span>
            </div>

            <h3 class="sfc-title">
              <a :href="art.link" target="_blank" rel="noopener noreferrer">
                {{ art.title }}
              </a>
            </h3>

            <p class="sfc-authors">
              👥 <strong>Penulis:</strong> {{ art.authors }}
            </p>

            <p v-if="art.publication" class="sfc-pub">
              📖 <strong>Jurnal / Prosiding:</strong> {{ art.publication }}
            </p>

            <div class="sfc-footer">
              <a :href="art.link" target="_blank" rel="noopener noreferrer" class="sfc-link">
                Buka Sitasi di Google Scholar ➔
              </a>
            </div>
          </article>
        </div>

        <!-- Scholar External Link Bar -->
        <div class="vc-bottom-bar">
          <div class="vcb-text">
            <span>Profil Google Scholar Resmi Arva Athallah Susanto:</span>
            <strong>Citations: 44+ | H-Index: 4 | i10-Index: 2</strong>
          </div>
          <a
            href="https://scholar.google.com/citations?user=7gI4mGYAAAAJ&hl=id"
            target="_blank"
            rel="noopener noreferrer"
            class="btn-scholar-profile"
          >
            🎓 Buka Profil Lengkap Google Scholar →
          </a>
        </div>
      </div>
    </section>

    <!-- CALL TO ACTION -->
    <section class="baznas-cta-section">
      <div class="cta-inner">
        <span class="hero-badge live-badge">KOLABORASI &amp; REKRUTMEN BAZNAS RI</span>
        <h2>Siap Berkontribusi Nyata bagi Kemajuan Riset BAZNAS RI</h2>
        <p>
          Memiliki dedikasi tinggi untuk memperkuat tata kelola zakat nasional, pengelolaan OJS &amp; jurnal IJAZ, 
          serta penyusunan materi kebijakan pimpinan berbasis riset empiris dan teknologi mutakhir.
        </p>

        <div class="cta-actions">
          <NuxtLink to="/contact" class="baznas-btn primary">
            Hubungi Arva Athallah →
          </NuxtLink>
          <a href="https://journal.masei.or.id/al-khawarizmi/about/contact" target="_blank" class="baznas-btn secondary">
            🌐 Redaksi OJS Journal MASEI
          </a>
          <a href="https://scholar.google.com/citations?user=7gI4mGYAAAAJ&hl=id" target="_blank" class="baznas-btn secondary">
            🎓 Google Scholar Profile
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
  max-width: 960px;
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
  font-size: clamp(32px, 5.2vw, 58px);
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
  max-width: 820px;
  margin: 0 auto 30px;
}

.hero-description strong {
  color: #f8fafc;
}

/* Elegant Executive Notice Box */
.executive-notice-box {
  background: rgba(255, 255, 255, 0.07);
  border: 1px solid rgba(52, 211, 153, 0.3);
  backdrop-filter: blur(16px);
  border-radius: 18px;
  padding: 18px 24px;
  display: flex;
  align-items: flex-start;
  gap: 16px;
  text-align: left;
  max-width: 860px;
  margin: 0 auto 36px;
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.2);
}

.enb-icon {
  font-size: 26px;
  flex-shrink: 0;
  margin-top: 2px;
}

.enb-content h4 {
  font-family: var(--font-display, serif);
  font-size: 15px;
  font-weight: 700;
  color: #34d399;
  margin: 0 0 6px 0;
  letter-spacing: 0.02em;
}

.enb-content p {
  font-size: 13px;
  color: #e2e8f0;
  line-height: 1.6;
  margin: 0;
}

.enb-content strong {
  color: #ffffff;
}

.enb-content em {
  color: #a7f3d0;
  font-style: normal;
}

.hero-cta-group {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 14px;
  flex-wrap: wrap;
  margin-bottom: 48px;
}

.baznas-btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 12px 24px;
  border-radius: 12px;
  font-size: 13.5px;
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
  max-width: 820px;
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
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 16px;
  margin-bottom: 24px;
}

.pres-tab-btn {
  background: #ffffff;
  border: 2px solid #e2e8f0;
  border-radius: 16px;
  padding: 18px 20px;
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

.tab-top-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.tab-badge {
  font-family: var(--font-mono, monospace);
  font-size: 11px;
  font-weight: 800;
  color: #059669;
  text-transform: uppercase;
}

.tab-date {
  font-size: 11px;
  font-weight: 600;
  color: #64748b;
}

.tab-title {
  font-family: var(--font-display, serif);
  font-size: 15px;
  font-weight: 700;
  color: #0f172a;
  line-height: 1.35;
}

.tab-meta {
  font-size: 11px;
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
  gap: 14px;
}

.pib-left {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.pib-attribution-badge {
  display: flex;
  align-items: center;
  gap: 8px;
  background: rgba(255, 255, 255, 0.08);
  border: 1px solid rgba(52, 211, 153, 0.3);
  padding: 6px 14px;
  border-radius: 8px;
  font-size: 12px;
  flex-wrap: wrap;
}

.badge-creator {
  color: #a7f3d0;
}

.badge-creator strong {
  color: #ffffff;
}

.badge-arrow {
  color: #34d399;
  font-weight: bold;
}

.badge-target {
  color: #cbd5e1;
}

.badge-target strong {
  color: #fbbf24;
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

.mc-footer {
  margin-top: auto;
  padding-top: 10px;
}

.mc-link {
  font-size: 13px;
  font-weight: 700;
  color: #059669;
  text-decoration: none;
  transition: color 0.2s;
}

.mc-link:hover {
  color: #047857;
  text-decoration: underline;
}

/* ── VERTICAL SCHOLAR CAROUSEL SECTION ──────────────── */
.scholar-controls-wrap {
  display: flex;
  flex-direction: column;
  gap: 16px;
  align-items: center;
  max-width: 800px;
  margin: 0 auto 36px;
}

.scholar-search-box {
  position: relative;
  width: 100%;
}

.scholar-search-box .search-icon {
  position: absolute;
  left: 18px;
  top: 50%;
  transform: translateY(-50%);
  font-size: 16px;
}

.scholar-input {
  width: 100%;
  padding: 14px 44px 14px 46px;
  border-radius: 999px;
  border: 1.5px solid #cbd5e1;
  font-size: 14px;
  outline: none;
  transition: all 0.2s;
  box-shadow: 0 4px 14px rgba(15, 23, 42, 0.04);
}

.scholar-input:focus {
  border-color: #059669;
  box-shadow: 0 0 0 4px rgba(16, 185, 129, 0.15);
}

.clear-search {
  position: absolute;
  right: 18px;
  top: 50%;
  transform: translateY(-50%);
  background: none;
  border: none;
  color: #94a3b8;
  font-size: 14px;
  cursor: pointer;
}

.scholar-filter-pills {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  justify-content: center;
}

.filter-pill {
  padding: 6px 18px;
  border-radius: 999px;
  border: 1px solid #cbd5e1;
  background: #ffffff;
  color: #475569;
  font-size: 12px;
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

.vertical-carousel-wrapper {
  background: #ffffff;
  border: 1.5px solid #e2e8f0;
  border-radius: 24px;
  overflow: hidden;
  box-shadow: 0 20px 50px rgba(15, 23, 42, 0.08);
}

.vc-header-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 24px;
  background: #f8fafc;
  border-bottom: 1px solid #e2e8f0;
  font-size: 13px;
  color: #475569;
}

.vc-header-bar strong {
  color: #0f172a;
}

.vc-nav-btns {
  display: flex;
  gap: 8px;
}

.vc-nav-btn {
  background: #ffffff;
  border: 1px solid #cbd5e1;
  color: #0f172a;
  padding: 6px 14px;
  border-radius: 8px;
  font-size: 12px;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.2s;
}

.vc-nav-btn:hover {
  background: #059669;
  color: #ffffff;
  border-color: #059669;
}

/* Vertical Scrolling Feed Container */
.vertical-carousel-feed {
  max-height: 620px;
  overflow-y: auto;
  padding: 24px;
  display: flex;
  flex-direction: column;
  gap: 18px;
  background: #fafbfc;
  scroll-behavior: smooth;
}

.scholar-feed-card {
  background: #ffffff;
  border: 1px solid #e2e8f0;
  border-radius: 18px;
  padding: 22px 24px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  transition: all 0.25s cubic-bezier(0.16, 1, 0.3, 1);
  box-shadow: 0 2px 10px rgba(15, 23, 42, 0.03);
}

.scholar-feed-card:hover {
  transform: translateX(4px);
  border-color: #10b981;
  box-shadow: 0 10px 25px rgba(16, 185, 129, 0.1);
}

.sfc-meta-row {
  display: flex;
  align-items: center;
  gap: 10px;
  flex-wrap: wrap;
}

.sfc-index {
  font-family: var(--font-mono, monospace);
  font-size: 11px;
  font-weight: 800;
  color: #64748b;
  background: #f1f5f9;
  padding: 2px 8px;
  border-radius: 6px;
}

.sfc-badge {
  font-family: var(--font-mono, monospace);
  font-size: 11px;
  font-weight: 800;
  color: #047857;
  background: #d1fae5;
  padding: 3px 10px;
  border-radius: 6px;
  text-transform: uppercase;
}

.sfc-year {
  font-size: 12px;
  font-weight: 600;
  color: #64748b;
}

.sfc-cites {
  font-family: var(--font-mono, monospace);
  font-size: 11px;
  font-weight: 800;
  color: #b45309;
  background: #fef3c7;
  padding: 2px 8px;
  border-radius: 6px;
}

.sfc-title {
  font-family: var(--font-display, serif);
  font-size: 17px;
  font-weight: 700;
  line-height: 1.35;
  margin: 0;
}

.sfc-title a {
  color: #0f172a;
  text-decoration: none;
  transition: color 0.2s;
}

.sfc-title a:hover {
  color: #059669;
}

.sfc-authors {
  font-size: 13px;
  color: #475569;
  margin: 0;
  line-height: 1.5;
}

.sfc-pub {
  font-size: 12.5px;
  color: #0284c7;
  margin: 0;
  font-style: italic;
}

.sfc-footer {
  margin-top: 6px;
  padding-top: 10px;
  border-top: 1px solid #f1f5f9;
}

.sfc-link {
  font-size: 12.5px;
  font-weight: 700;
  color: #059669;
  text-decoration: none;
  transition: all 0.2s;
}

.sfc-link:hover {
  color: #047857;
  text-decoration: underline;
}

.vc-bottom-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 24px;
  background: #0f172a;
  color: #ffffff;
  flex-wrap: wrap;
  gap: 14px;
}

.vcb-text {
  display: flex;
  flex-direction: column;
  gap: 2px;
  font-size: 12px;
  color: #94a3b8;
}

.vcb-text strong {
  color: #34d399;
  font-family: var(--font-mono, monospace);
  font-size: 13px;
}

.btn-scholar-profile {
  background: linear-gradient(135deg, #10b981 0%, #059669 100%);
  color: #ffffff;
  padding: 10px 20px;
  border-radius: 10px;
  font-size: 13px;
  font-weight: 700;
  text-decoration: none;
  transition: all 0.2s;
  box-shadow: 0 4px 14px rgba(16, 185, 129, 0.4);
}

.btn-scholar-profile:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 24px rgba(16, 185, 129, 0.6);
}

/* ── CTA SECTION ────────────────────────────────────── */
.baznas-cta-section {
  background: linear-gradient(135deg, #022c22 0%, #064e3b 50%, #0f766e 100%);
  color: #ffffff;
  padding: 80px 24px;
  text-align: center;
}

.cta-inner {
  max-width: 840px;
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
  gap: 12px;
  flex-wrap: wrap;
}
</style>
