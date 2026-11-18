<!DOCTYPE html>
<html lang="id" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AgriRawit Pro | Sistem Manajemen & Kalkulator Budidaya Cabai Rawit (Pot & Lahan)</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Plus Jakarta Sans & Inter -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Plus+Jakarta+Sans:wght@600;700;800&display=swap" rel="stylesheet">
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <!-- Chart.js for Agronomic & Financial Visualizations -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        display: ['Plus Jakarta Sans', 'sans-serif'],
                    },
                    colors: {
                        emerald: {
                            50: '#ecfdf5',
                            100: '#d1fae5',
                            200: '#a7f3d0',
                            300: '#6ee7b7',
                            400: '#34d399',
                            500: '#10b981',
                            600: '#059669',
                            700: '#047857',
                            800: '#065f46',
                            900: '#064e3b',
                            950: '#022c22',
                        },
                        chili: {
                            500: '#ef4444',
                            600: '#dc2626',
                            700: '#b91c1c',
                        }
                    }
                }
            }
        }
    </script>

    <style>
        body {
            background-color: #f8fafc;
            color: #0f172a;
        }
        .tab-content {
            display: none;
            animation: fadeIn 0.35s ease-out forwards;
        }
        .tab-content.active {
            display: block;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(8px); }
            to { opacity: 1; transform: translateY(0); }
        }
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 9999px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
    </style>
</head>
<body class="antialiased min-h-screen flex flex-col">

    <!-- Toast Notification Container -->
    <div id="toast-container" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2 pointer-events-none"></div>

    <!-- Modal Pustaka Ilmiah & Jurnal Pendukung -->
    <div id="modal-pustaka" class="fixed inset-0 z-50 hidden bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4">
        <div class="bg-white rounded-2xl max-w-3xl w-full max-h-[85vh] overflow-hidden shadow-2xl border border-slate-200 flex flex-col">
            <div class="p-5 bg-emerald-900 text-white flex items-center justify-between">
                <div class="flex items-center gap-2.5">
                    <i data-lucide="book-open-check" class="w-6 h-6 text-emerald-300"></i>
                    <h3 class="font-display font-bold text-lg">Pustaka Ilmiah, Buku Panduan & Jurnal Pendukung</h3>
                </div>
                <button onclick="toggleModal('modal-pustaka', false)" class="p-1.5 rounded-lg hover:bg-emerald-800 text-emerald-100 transition">
                    <i data-lucide="x" class="w-5 h-5"></i>
                </button>
            </div>
            <div class="p-6 overflow-y-auto space-y-4 text-sm text-slate-700 leading-relaxed">
                <p class="bg-emerald-50 border-l-4 border-emerald-600 p-3.5 rounded-r-xl text-emerald-900 font-medium">
                    Seluruh formulasi dosis kocor per 100 liter air, prosedur budidaya cabai rawit (baik di lahan terbuka maupun dalam pot/polybag), serta pengendalian hama dan penyakit (PHT) dalam sistem ini merujuk pada standar ilmiah resmi berikut:
                </p>
                <div class="space-y-3">
                    <div class="p-4 rounded-xl border border-slate-200 bg-slate-50">
                        <span class="text-xs font-bold uppercase tracking-wider text-emerald-700">Buku Referensi Utama Pemuliaan & Budidaya</span>
                        <h4 class="font-bold text-slate-900 mt-0.5">Syukur, M., Sujiprihati, S., & Yunianti, R. (2015). <em>Teknik Pemuliaan & Budidaya Cabai Unggul</em>. Penebar Swadaya.</h4>
                        <p class="text-xs text-slate-600 mt-1">Acuan genetika varietas cabai rawit (<em>Capsicum frutescens</em> L.), manajemen pembentukan cabang Y, dan takaran hara vegetatif & generatif.</p>
                    </div>
                    <div class="p-4 rounded-xl border border-slate-200 bg-slate-50">
                        <span class="text-xs font-bold uppercase tracking-wider text-emerald-700">Standar Operasional Prosedur (SOP) Kementan RI</span>
                        <h4 class="font-bold text-slate-900 mt-0.5">Balai Penelitian Tanaman Sayuran (Balitsa) - Kementerian Pertanian. <em>SOP Budidaya Cabai Rawit & Cabai Merah Ramah Lingkungan</em>.</h4>
                        <p class="text-xs text-slate-600 mt-1">Acuan pengapuran dolomit, komposisi media tanam pot (topsoil:kompos:sekam 2:1:1), interval pemupukan kocor 7 hari sekali, serta volume siram 200 ml per tanaman.</p>
                    </div>
                    <div class="p-4 rounded-xl border border-slate-200 bg-slate-50">
                        <span class="text-xs font-bold uppercase tracking-wider text-emerald-700">Jurnal Perlindungan Tanaman & Pengendalian Hama Terpadu (PHT)</span>
                        <h4 class="font-bold text-slate-900 mt-0.5">Setiawati, W., Udiarto, B. K., & Muharam, A. (2013). <em>Pengendalian Hama dan Penyakit Utama Cabai Merah dan Cabai Rawit</em>. Jurnal Hortikultura & Balitsa.</h4>
                        <p class="text-xs text-slate-600 mt-1">Acuan ambang ekonomi serangan <em>Thrips parvispinus</em>, vektor virus Gemini (kutu kebul), antraknosa (<em>Colletotrichum</em>), layu fusarium, serta rotasi bahan aktif fungisida/insektisida.</p>
                    </div>
                    <div class="p-4 rounded-xl border border-slate-200 bg-slate-50">
                        <span class="text-xs font-bold uppercase tracking-wider text-emerald-700">Panduan Budidaya Tanaman dalam Pot / Polybag</span>
                        <h4 class="font-bold text-slate-900 mt-0.5">Cahyono, B. (2012). <em>Cabai Rawit: Teknik Budidaya dan Analisis Usaha Tani</em>. Kanisius.</h4>
                        <p class="text-xs text-slate-600 mt-1">Acuan ukuran pot minimal diameter 30-40 cm, aerasi media tanam wadah, pemupukan susulan berkala, dan penyiraman terkontrol.</p>
                    </div>
                </div>
            </div>
            <div class="p-4 border-t border-slate-200 bg-slate-50 flex justify-end">
                <button onclick="toggleModal('modal-pustaka', false)" class="px-5 py-2.5 bg-emerald-700 hover:bg-emerald-800 text-white font-semibold rounded-xl text-sm transition">
                    Tutup Pustaka
                </button>
            </div>
        </div>
    </div>

    <!-- Top Navigation Bar -->
    <header class="sticky top-0 z-40 bg-emerald-950 text-white shadow-lg border-b border-emerald-800/60">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <!-- Brand Logo -->
                <div class="flex items-center gap-3">
                    <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-chili-500 to-amber-500 flex items-center justify-center shadow-md">
                        <svg class="w-6 h-6 text-white" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                            <path d="M17 3c1.5 1.5 2 3.5 1.5 5.5"/>
                            <path d="M18.5 8.5c-1.5-1-3.5-1-5 0-3 2-5.5 6.5-6.5 10.5-.3 1.2.8 2.2 2 1.8 4.2-1.4 8.5-4.3 10.2-7.8.8-1.6.5-3.4-.7-4.5Z"/>
                            <path d="M15.5 6.5c.5-1.5 2-2.5 3.5-2.5"/>
                        </svg>
                    </div>
                    <div>
                        <div class="flex items-center gap-2">
                            <span class="font-display font-extrabold text-lg tracking-tight text-white">AgriRawit<span class="text-emerald-400">Pro</span></span>
                            <span class="hidden sm:inline-block text-[10px] font-bold uppercase tracking-wider px-2 py-0.5 rounded-full bg-emerald-800 text-emerald-200 border border-emerald-700">v3.0 Ultimate</span>
                        </div>
                        <p class="text-[11px] text-emerald-300/90 hidden sm:block">Sistem Manajemen & Kalkulator Cabai Rawit (Pot & Lahan Terbuka)</p>
                    </div>
                </div>

                <!-- Right Actions -->
                <div class="flex items-center gap-2.5">
                    <button onclick="toggleModal('modal-pustaka', true)" class="flex items-center gap-1.5 px-3 py-2 rounded-xl bg-emerald-900/90 hover:bg-emerald-800 text-emerald-100 text-xs font-semibold border border-emerald-700/70 transition">
                        <i data-lucide="library" class="w-4 h-4 text-amber-400"></i>
                        <span class="hidden md:inline">Pustaka & Jurnal</span>
                    </button>
                    <button onclick="switchTab('tab-kalender')" class="flex items-center gap-1.5 px-3.5 py-2 rounded-xl bg-chili-600 hover:bg-chili-700 text-white text-xs font-bold shadow-sm transition">
                        <i data-lucide="calendar-check" class="w-4 h-4"></i>
                        <span>Jadwal Tanam</span>
                    </button>
                </div>
            </div>

            <!-- Navigation Tabs -->
            <nav class="flex items-center gap-1 overflow-x-auto pb-2.5 pt-1 no-scrollbar">
                <button onclick="switchTab('tab-sop')" data-tab="tab-sop" class="nav-btn active flex items-center gap-2 px-3.5 py-2 rounded-xl text-xs font-semibold whitespace-nowrap bg-emerald-600 text-white shadow-sm transition">
                    <i data-lucide="sprout" class="w-4 h-4"></i> 1. SOP Lengkap & Pot/Polybag
                </button>
                <button onclick="switchTab('tab-kalender')" data-tab="tab-kalender" class="nav-btn flex items-center gap-2 px-3.5 py-2 rounded-xl text-xs font-semibold whitespace-nowrap text-emerald-200 hover:bg-emerald-900/70 transition">
                    <i data-lucide="calendar-days" class="w-4 h-4"></i> 2. Kalender & Tgl Tanam
                </button>
                <button onclick="switchTab('tab-kalkulator')" data-tab="tab-kalkulator" class="nav-btn flex items-center gap-2 px-3.5 py-2 rounded-xl text-xs font-semibold whitespace-nowrap text-emerald-200 hover:bg-emerald-900/70 transition">
                    <i data-lucide="calculator" class="w-4 h-4"></i> 3. Kalkulator Dosis 100L Air
                </button>
                <button onclick="switchTab('tab-opt')" data-tab="tab-opt" class="nav-btn flex items-center gap-2 px-3.5 py-2 rounded-xl text-xs font-semibold whitespace-nowrap text-emerald-200 hover:bg-emerald-900/70 transition">
                    <i data-lucide="bug" class="w-4 h-4"></i> 4. Klinik Hama & Penyakit PHT
                </button>
                <button onclick="switchTab('tab-ekonomi')" data-tab="tab-ekonomi" class="nav-btn flex items-center gap-2 px-3.5 py-2 rounded-xl text-xs font-semibold whitespace-nowrap text-emerald-200 hover:bg-emerald-900/70 transition">
                    <i data-lucide="trending-up" class="w-4 h-4"></i> 5. Analisis Usaha & BEP
                </button>
                <button onclick="switchTab('tab-jurnal')" data-tab="tab-jurnal" class="nav-btn flex items-center gap-2 px-3.5 py-2 rounded-xl text-xs font-semibold whitespace-nowrap text-emerald-200 hover:bg-emerald-900/70 transition">
                    <i data-lucide="clipboard-list" class="w-4 h-4"></i> 6. Logbook Lahan
                </button>
            </nav>
        </div>
    </header>

    <!-- Main Content Container -->
    <main class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 space-y-6">

        <!-- Global Status & Live HST Banner -->
        <section class="bg-gradient-to-r from-emerald-900 via-emerald-800 to-teal-900 rounded-2xl p-5 sm:p-6 text-white shadow-md border border-emerald-700/50">
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-5 items-center">
                <div class="lg:col-span-7 space-y-2">
                    <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-emerald-950/60 border border-emerald-600/40 text-emerald-200 text-xs font-medium">
                        <span id="global-hst-badge" class="font-bold text-amber-300">HST: 0 (Hari Pindah Tanam)</span>
                    </div>
                    <h1 class="font-display text-xl sm:text-2xl font-extrabold tracking-tight text-white">
                        Pusat Kendali Budidaya Cabai Rawit (Pot, Polybag & Lahan)
                    </h1>
                    <p class="text-xs sm:text-sm text-emerald-100/90 leading-relaxed">
                        Platform berbasis referensi resmi Kementan RI dan buku panduan budidaya terpercaya untuk mengoptimalkan hasil panen Anda.
                    </p>
                </div>
                <!-- Quick Info Cards -->
                <div class="lg:col-span-5 grid grid-cols-2 gap-2.5">
                    <div class="bg-white/10 backdrop-blur-sm rounded-xl p-3 border border-white/15">
                        <div class="text-[11px] text-emerald-200 font-medium">Tanggal Tanam Aktif</div>
                        <div id="banner-tgl-tanam" class="font-display font-bold text-sm sm:text-base text-amber-300 mt-0.5">-</div>
                    </div>
                    <div class="bg-white/10 backdrop-blur-sm rounded-xl p-3 border border-white/15">
                        <div class="text-[11px] text-emerald-200 font-medium">Fase Pertumbuhan Saat Ini</div>
                        <div id="banner-fase-aktif" class="font-display font-bold text-sm sm:text-base text-white mt-0.5">-</div>
                    </div>
                </div>
            </div>
        </section>

        <!-- ===================================================================== -->
        <!-- TAB 1: SOP TERPADU & KHUSUS POT / POLYBAG                             -->
        <!-- ===================================================================== -->
        <section id="tab-sop" class="tab-content active space-y-6">
            <div class="bg-white rounded-2xl p-4 shadow-sm border border-slate-200">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3 mb-4">
                    <div>
                        <h2 class="font-display font-bold text-lg text-slate-900">Tahapan SOP Budidaya Cabai Rawit (Lengkap & Terperinci)</h2>
                        <p class="text-xs text-slate-500">Pilih fase pertumbuhan untuk melihat penjelasan teknis mendalam dan panduan khusus tanam dalam pot/polybag.</p>
                    </div>
                    <span class="text-xs font-semibold px-3 py-1.5 rounded-lg bg-emerald-50 text-emerald-700 border border-emerald-200 self-start">6 Fase Kritis Kementan & Buku Panduan</span>
                </div>
                <div class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-6 gap-2" id="sop-phase-buttons">
                    <button onclick="selectSopPhase(0)" class="sop-btn active text-left p-3 rounded-xl border-2 border-emerald-600 bg-emerald-50/80 transition">
                        <div class="text-[11px] font-bold text-emerald-700">FASE 1 • -25 s/d 0 HST</div>
                        <div class="font-bold text-xs sm:text-sm text-slate-900 mt-0.5">Persemaian Benih</div>
                    </button>
                    <button onclick="selectSopPhase(1)" class="sop-btn text-left p-3 rounded-xl border border-slate-200 hover:border-emerald-400 bg-white transition">
                        <div class="text-[11px] font-bold text-slate-500">FASE 2 • -14 s/d -1 HST</div>
                        <div class="font-bold text-xs sm:text-sm text-slate-900 mt-0.5">Media Pot & Lahan</div>
                    </button>
                    <button onclick="selectSopPhase(2)" class="sop-btn text-left p-3 rounded-xl border border-slate-200 hover:border-emerald-400 bg-white transition">
                        <div class="text-[11px] font-bold text-slate-500">FASE 3 • 0 s/d 7 HST</div>
                        <div class="font-bold text-xs sm:text-sm text-slate-900 mt-0.5">Pindah Tanam & Ajir</div>
                    </button>
                    <button onclick="selectSopPhase(3)" class="sop-btn text-left p-3 rounded-xl border border-slate-200 hover:border-emerald-400 bg-white transition">
                        <div class="text-[11px] font-bold text-slate-500">FASE 4 • 14 s/d 45 HST</div>
                        <div class="font-bold text-xs sm:text-sm text-slate-900 mt-0.5">Pewiwilan & Kocor</div>
                    </button>
                    <button onclick="selectSopPhase(4)" class="sop-btn text-left p-3 rounded-xl border border-slate-200 hover:border-emerald-400 bg-white transition">
                        <div class="text-[11px] font-bold text-slate-500">FASE 5 • 35 s/d 75 HST</div>
                        <div class="font-bold text-xs sm:text-sm text-slate-900 mt-0.5">Generatif & Buah</div>
                    </button>
                    <button onclick="selectSopPhase(5)" class="sop-btn text-left p-3 rounded-xl border border-slate-200 hover:border-emerald-400 bg-white transition">
                        <div class="text-[11px] font-bold text-slate-500">FASE 6 • 75+ HST</div>
                        <div class="font-bold text-xs sm:text-sm text-slate-900 mt-0.5">Panen & Pemulihan</div>
                    </button>
                </div>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                <div class="lg:col-span-7 bg-white rounded-2xl p-6 shadow-sm border border-slate-200 space-y-5" id="sop-detail-container"></div>
                <div class="lg:col-span-5 space-y-6">
                    <div class="bg-white rounded-2xl p-5 shadow-sm border border-slate-200">
                        <div class="flex items-center justify-between mb-3">
                            <h3 class="font-display font-bold text-sm text-slate-900 flex items-center gap-2">
                                <i data-lucide="layers" class="w-4 h-4 text-emerald-600"></i>
                                <span id="svg-diagram-title">Diagram Teknis Agronomi</span>
                            </h3>
                            <span class="text-[11px] font-semibold px-2 py-0.5 rounded bg-slate-100 text-slate-600">Ilustrasi Skala</span>
                        </div>
                        <div id="sop-svg-container" class="w-full bg-slate-50 rounded-xl border border-slate-200/80 p-3 flex items-center justify-center overflow-hidden"></div>
                        <p id="svg-diagram-caption" class="text-xs text-slate-500 mt-3 leading-relaxed"></p>
                    </div>
                    <div class="bg-white rounded-2xl p-5 shadow-sm border border-slate-200">
                        <div class="flex items-center justify-between mb-2">
                            <h3 class="font-display font-bold text-sm text-slate-900 flex items-center gap-2">
                                <i data-lucide="bar-chart-3" class="w-4 h-4 text-amber-500"></i> Kurva Kebutuhan Hara N - P - K (%)
                            </h3>
                        </div>
                        <div class="h-52 w-full"><canvas id="npkChart"></canvas></div>
                    </div>
                </div>
            </div>
        </section>

        <!-- ===================================================================== -->
        <!-- TAB 2: KALENDER TANAM & PENJADWALAN OTOMATIS                          -->
        <!-- ===================================================================== -->
        <section id="tab-kalender" class="tab-content space-y-6">
            <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-200">
                <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 pb-5 border-b border-slate-200">
                    <div>
                        <h2 class="font-display font-bold text-lg text-slate-900">Custom Tanggal Tanam & Generator Kalender Otomatis</h2>
                        <p class="text-xs text-slate-500 mt-0.5">Ubah tanggal pindah tanam (0 HST) di bawah ini untuk memperbarui seluruh jadwal harian secara otomatis.</p>
                    </div>
                    <div class="flex items-center gap-2">
                        <button onclick="resetChecklist()" class="px-3.5 py-2 rounded-xl border border-slate-300 hover:bg-slate-50 text-xs font-semibold text-slate-700 transition">
                            Reset Checklist
                        </button>
                    </div>
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4 mt-5">
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 mb-1.5">Tanggal Pindah Tanam (0 HST)</label>
                        <input type="date" id="input-tgl-tanam" class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm focus:ring-2 focus:ring-emerald-500 font-bold text-emerald-900 bg-emerald-50/55 outline-none" onchange="generateSchedule()">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 mb-1.5">Varietas Cabai Rawit</label>
                        <select id="input-varietas" class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm focus:ring-2 focus:ring-emerald-500 outline-none bg-white" onchange="generateSchedule()">
                            <option value="ori212">Ori 212 (Panen ~80 HST)</option>
                            <option value="dewata43">Dewata 43 F1 (Panen ~75 HST)</option>
                            <option value="bara">Bara (Panen ~85 HST)</option>
                            <option value="pelita8">Pelita 8 F1 (Panen ~80 HST)</option>
                            <option value="lokal">Rawit Putih / Lokal (Panen ~90 HST)</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 mb-1.5">Nama Blok / Kebun Pot</label>
                        <input type="text" id="input-nama-blok" value="Kebun Pot / Polybag Rumah" class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm outline-none" oninput="generateSchedule(false)">
                    </div>
                    <div class="flex items-end">
                        <button onclick="generateSchedule()" class="w-full py-2.5 px-4 bg-emerald-600 hover:bg-emerald-700 text-white font-bold rounded-xl text-sm shadow-sm flex items-center justify-center gap-2 transition">
                            <i data-lucide="refresh-cw" class="w-4 h-4"></i> Perbarui Jadwal
                        </button>
                    </div>
                </div>

                <div class="grid grid-cols-2 lg:grid-cols-4 gap-3 mt-6" id="schedule-summary-cards"></div>
            </div>

            <div class="bg-white rounded-2xl shadow-sm border border-slate-200 overflow-hidden">
                <div class="p-4 sm:p-5 bg-slate-50 border-b border-slate-200 flex flex-col sm:flex-row sm:items-center justify-between gap-2">
                    <div class="flex items-center gap-2">
                        <i data-lucide="list-checks" class="w-5 h-5 text-emerald-600"></i>
                        <h3 class="font-display font-bold text-sm sm:text-base text-slate-900">Agenda Perawatan Berbasis HST & Tanggal Aktual</h3>
                    </div>
                    <div class="text-xs font-semibold text-emerald-700 bg-emerald-100 px-3 py-1 rounded-full" id="checklist-progress-badge">Progres: 0 / 0 Selesai</div>
                </div>
                <div class="divide-y divide-slate-200" id="schedule-timeline-list"></div>
            </div>
        </section>

        <!-- ===================================================================== -->
        <!-- TAB 3: KALKULATOR DOSIS PEMUPUKAN BERDASARKAN POPULASI TANAMAN POT    -->
        <!-- ===================================================================== -->
        <section id="tab-kalkulator" class="tab-content space-y-6">
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                <!-- Populasi Tanaman (Dapat Diubah Sendiri untuk Pot/Polybag) -->
                <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-200 space-y-5">
                    <div class="flex items-start gap-3 pb-4 border-b border-slate-100">
                        <div class="w-10 h-10 rounded-xl bg-emerald-100 text-emerald-700 flex items-center justify-center shrink-0">
                            <i data-lucide="flower-2" class="w-5 h-5"></i>
                        </div>
                        <div>
                            <h3 class="font-display font-bold text-base text-slate-900">Kalkulator Populasi Pot / Polybag</h3>
                            <p class="text-xs text-slate-500 mt-0.5">Ubah jumlah tanaman di bawah ini sesuai jumlah pot Anda. Dosis pupuk kebun akan dihitung secara otomatis.</p>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-xs font-semibold text-slate-700 mb-1">Jumlah Tanaman Anda (Pot/Polybag)</label>
                            <input type="number" id="calc-jml-tanaman" value="25" min="1" max="10000" class="w-full px-3.5 py-2.5 rounded-xl border-2 border-emerald-500 bg-emerald-50/50 font-bold text-emerald-900 text-sm outline-none" oninput="renderFertilizerTable()">
                            <p class="text-[11px] text-slate-500 mt-1">Contoh: Jika punya 25 pot, masukkan angka 25.</p>
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-slate-700 mb-1">Volume Kocor per Pohon</label>
                            <input type="text" value="200 ml (1 Gelas Standar)" disabled class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 bg-slate-100 text-xs font-medium text-slate-600">
                            <p class="text-[11px] text-slate-500 mt-1">Standar Balitsa & Buku Budidaya.</p>
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-slate-700 mb-1">pH Media Pot Aktual</label>
                            <input type="number" id="calc-ph" value="6.0" step="0.1" min="4.0" max="7.5" class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm outline-none" oninput="calculateAgronomyPot()">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-slate-700 mb-1">Ukuran Pot / Polybag</label>
                            <select id="calc-ukuran-pot" class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm bg-white outline-none">
                                <option value="30">Diameter 30 cm (Kecil)</option>
                                <option value="40" selected>Diameter 40 cm (Ideal / Rekomendasi)</option>
                                <option value="50">Diameter 50 cm+ (Jumbo)</option>
                            </select>
                        </div>
                    </div>

                    <div class="bg-slate-50 rounded-xl p-4 border border-slate-200/80 grid grid-cols-2 gap-3" id="calc-pot-output"></div>
                </div>

                <!-- Petunjuk Pencampuran Larutan Berdasarkan 100 Liter Air -->
                <div class="bg-gradient-to-br from-emerald-900 to-teal-900 rounded-2xl p-6 text-white shadow-sm border border-emerald-700 space-y-4 flex flex-col justify-between">
                    <div>
                        <div class="flex items-center gap-2 text-amber-300 font-bold text-sm mb-2">
                            <i data-lucide="info" class="w-5 h-5"></i>
                            Petunjuk Pencampuran Larutan Kocor (Basis 100 Liter Air)
                        </div>
                        <ol class="list-decimal list-inside space-y-2 text-xs sm:text-sm text-emerald-100 leading-relaxed">
                            <li>Formulasi standar di tabel merujuk pada takaran per <strong>100 Liter Air</strong>. Sistem mengonversinya secara proporsional sesuai jumlah pot Anda.</li>
                            <li>Larutkan terlebih dahulu pupuk kristal (NPK, MKP, KNO3, Kalsium, Humat) ke dalam ember kecil berisi air hangat kuku hingga larut sempurna.</li>
                            <li>Campurkan larutan pekat tersebut ke dalam wadah utama sesuai total air yang dibutuhkan untuk pot Anda.</li>
                            <li>Kocorkan tepat pada perakaran sebanyak <strong class="text-amber-300">200 ml</strong> per pot pada pagi hari (07.00–09.00) saat media lembab.</li>
                        </ol>
                    </div>
                    <div class="p-3.5 rounded-xl bg-white/10 border border-white/15 text-xs text-emerald-200">
                        * Total Air Kocor Kebun Anda saat ini: <strong id="total-air-badge" class="text-amber-300">5.0 Liter</strong> (untuk <span id="badge-pop-count">25</span> pot).
                    </div>
                </div>
            </div>

            <!-- Tabel Pemupukan Kocor Diperluas (12 Fase Berdasarkan Kementan & Buku Panduan) -->
            <div class="bg-white rounded-2xl shadow-sm border border-slate-200 overflow-hidden">
                <div class="p-5 bg-slate-50 border-b border-slate-200 flex flex-col sm:flex-row sm:items-center justify-between gap-3">
                    <div>
                        <h3 class="font-display font-bold text-base text-slate-900">Tabel Rujukan Pemupukan Kocor Lengkap (12 Fase Kritis)</h3>
                        <p class="text-xs text-slate-500">Formulasi Standar per 100 Liter Air vs Kebutuhan Aktual untuk <span id="table-populasi-label" class="font-bold text-emerald-700">25</span> Pot Anda.</p>
                    </div>
                    <span class="text-xs font-semibold px-3 py-1 rounded-full bg-emerald-100 text-emerald-800 self-start">Sumber: Balitsa Kementan & Buku Syukur et al. (2015)</span>
                </div>
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse text-xs">
                        <thead>
                            <tr class="bg-slate-100/80 border-b border-slate-200 text-slate-700 font-bold uppercase tracking-wider">
                                <th class="py-3.5 px-4">Umur Tanaman</th>
                                <th class="py-3.5 px-4">Formulasi Standar (per 100 Liter Air)</th>
                                <th class="py-3.5 px-4 bg-emerald-50/70 text-emerald-900">Kebutuhan Pupuk Pot Anda</th>
                                <th class="py-3.5 px-4">Tujuan & Efek Agronomis</th>
                            </tr>
                        </thead>
                        <tbody id="fertilizer-table-body" class="divide-y divide-slate-200 text-slate-700">
                            <!-- Populated via JS -->
                        </tbody>
                    </table>
                </div>
            </div>
        </section>

        <!-- ===================================================================== -->
        <!-- TAB 4: KLINIK DIAGNOSA HAMA & PENYAKIT (PHT BERDASARKAN JURNAL)       -->
        <!-- ===================================================================== -->
        <section id="tab-opt" class="tab-content space-y-6">
            <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-200">
                <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
                    <div>
                        <h2 class="font-display font-bold text-lg text-slate-900">Klinik Diagnosa Hama & Penyakit Tanaman Cabai Rawit</h2>
                        <p class="text-xs text-slate-500 mt-0.5">Referensi lengkap penanganan Organisme Pengganggu Tumbuhan (OPT) merujuk pada Jurnal Balitsa & Buku PHT.</p>
                    </div>
                    <div class="flex flex-wrap gap-1.5" id="opt-filter-group">
                        <button onclick="filterOpt('all')" data-filter="all" class="opt-filter-btn active px-3 py-1.5 rounded-lg text-xs font-bold bg-emerald-600 text-white transition">Semua OPT</button>
                        <button onclick="filterOpt('hama')" data-filter="hama" class="opt-filter-btn px-3 py-1.5 rounded-lg text-xs font-semibold bg-slate-100 text-slate-700 transition">Hama Utama</button>
                        <button onclick="filterOpt('penyakit')" data-filter="penyakit" class="opt-filter-btn px-3 py-1.5 rounded-lg text-xs font-semibold bg-slate-100 text-slate-700 transition">Penyakit Jamur/Bakteri</button>
                        <button onclick="filterOpt('virus')" data-filter="virus" class="opt-filter-btn px-3 py-1.5 rounded-lg text-xs font-semibold bg-slate-100 text-slate-700 transition">Penyakit Virus</button>
                        <button onclick="filterOpt('fisiologis')" data-filter="fisiologis" class="opt-filter-btn px-3 py-1.5 rounded-lg text-xs font-semibold bg-slate-100 text-slate-700 transition">Gangguan Fisiologis</button>
                    </div>
                </div>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-5" id="opt-cards-container"></div>
        </section>

        <!-- ===================================================================== -->
        <!-- TAB 5: ANALISIS USAHA TANI                                            -->
        <!-- ===================================================================== -->
        <section id="tab-ekonomi" class="tab-content space-y-6">
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                <div class="lg:col-span-5 bg-white rounded-2xl p-6 shadow-sm border border-slate-200 space-y-4">
                    <div class="pb-3 border-b border-slate-100">
                        <h2 class="font-display font-bold text-base text-slate-900">Parameter Biaya & Proyeksi Panen</h2>
                        <p class="text-xs text-slate-500">Sesuaikan komponen RAB untuk skala pot/polybag atau skala kebun.</p>
                    </div>
                    <div class="space-y-3 text-xs">
                        <div class="grid grid-cols-2 gap-3">
                            <div>
                                <label class="font-semibold text-slate-700 block mb-1">Jumlah Tanaman</label>
                                <input type="number" id="eco-populasi" value="25" class="w-full px-3 py-2 rounded-xl border border-slate-300 font-semibold" oninput="calculateEconomics()">
                            </div>
                            <div>
                                <label class="font-semibold text-slate-700 block mb-1">Hasil / Pohon (Kg)</label>
                                <input type="number" id="eco-hasil-pohon" value="0.75" step="0.05" class="w-full px-3 py-2 rounded-xl border border-slate-300 font-semibold" oninput="calculateEconomics()">
                            </div>
                        </div>
                        <div>
                            <label class="font-semibold text-slate-700 block mb-1">Harga Jual Cabai Rawit (Rp / Kg)</label>
                            <input type="number" id="eco-harga-jual" value="30000" step="1000" class="w-full px-3 py-2 rounded-xl border border-emerald-400 bg-emerald-50/40 font-bold text-emerald-900" oninput="calculateEconomics()">
                        </div>
                        <div class="pt-2 border-t border-slate-100 font-bold text-slate-800 uppercase tracking-wider text-[11px]">Komponen Biaya Modal (Rp)</div>
                        <div class="grid grid-cols-2 gap-3">
                            <div>
                                <label class="font-medium text-slate-600 block mb-1">Pot / Polybag & Media</label>
                                <input type="number" id="eco-biaya-lahan" value="150000" step="10000" class="w-full px-3 py-2 rounded-xl border border-slate-300" oninput="calculateEconomics()">
                            </div>
                            <div>
                                <label class="font-medium text-slate-600 block mb-1">Benih & Ajir</label>
                                <input type="number" id="eco-biaya-saprotan" value="50000" step="10000" class="w-full px-3 py-2 rounded-xl border border-slate-300" oninput="calculateEconomics()">
                            </div>
                            <div>
                                <label class="font-medium text-slate-600 block mb-1">Pupuk & Nutrisi</label>
                                <input type="number" id="eco-biaya-pupuk" value="75000" step="10000" class="w-full px-3 py-2 rounded-xl border border-slate-300" oninput="calculateEconomics()">
                            </div>
                            <div>
                                <label class="font-medium text-slate-600 block mb-1">Pestisida Nabati / Kimia</label>
                                <input type="number" id="eco-biaya-pestisida" value="40000" step="10000" class="w-full px-3 py-2 rounded-xl border border-slate-300" oninput="calculateEconomics()">
                            </div>
                        </div>
                    </div>
                </div>
                <div class="lg:col-span-7 space-y-6">
                    <div class="grid grid-cols-2 sm:grid-cols-3 gap-3" id="eco-kpi-container"></div>
                    <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-200 space-y-4">
                        <h3 class="font-display font-bold text-base text-slate-900">Analisis Titik Impas (BEP) & Kelayakan Usaha</h3>
                        <div class="grid grid-cols-1 sm:grid-cols-3 gap-4" id="eco-bep-container"></div>
                        <div class="h-56 w-full pt-2"><canvas id="ecoChart"></canvas></div>
                    </div>
                </div>
            </div>
        </section>

        <!-- ===================================================================== -->
        <!-- TAB 6: LOGBOOK LAHAN DIGITAL                                          -->
        <!-- ===================================================================== -->
        <section id="tab-jurnal" class="tab-content space-y-6">
            <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-200">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 pb-4 border-b border-slate-200">
                    <div>
                        <h2 class="font-display font-bold text-lg text-slate-900">Logbook Digital & Monitoring Tanaman Pot</h2>
                        <p class="text-xs text-slate-500">Catat perkembangan tinggi tanaman, aplikasi pupuk/pestisida, dan hasil petikan panen.</p>
                    </div>
                    <button onclick="exportJournalCSV()" class="flex items-center gap-2 px-4 py-2 rounded-xl bg-slate-900 hover:bg-slate-800 text-white text-xs font-bold transition self-start">
                        <i data-lucide="download" class="w-4 h-4"></i> Ekspor Data (.CSV)
                    </button>
                </div>
                <form id="journal-form" onsubmit="addJournalEntry(event)" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-6 gap-3 mt-5">
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 mb-1">Tanggal</label>
                        <input type="date" id="j-tanggal" required class="w-full px-3 py-2 rounded-xl border border-slate-300 text-xs">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 mb-1">Umur (HST)</label>
                        <input type="number" id="j-hst" placeholder="Misal: 21" required class="w-full px-3 py-2 rounded-xl border border-slate-300 text-xs">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 mb-1">Tinggi (cm)</label>
                        <input type="number" id="j-tinggi" placeholder="Misal: 35" required class="w-full px-3 py-2 rounded-xl border border-slate-300 text-xs">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-slate-700 mb-1">Kategori</label>
                        <select id="j-kategori" class="w-full px-3 py-2 rounded-xl border border-slate-300 text-xs bg-white">
                            <option value="Pemupukan Kocor">Pemupukan Kocor</option>
                            <option value="Penyemprotan OPT">Penyemprotan OPT</option>
                            <option value="Pewiwilan & Ajir">Pewiwilan & Ajir</option>
                            <option value="Panen / Petik">Panen / Petik</option>
                            <option value="Pengamatan Rutin">Pengamatan Rutin</option>
                        </select>
                    </div>
                    <div class="lg:col-span-2">
                        <label class="block text-xs font-semibold text-slate-700 mb-1">Catatan Teknis / Dosis</label>
                        <div class="flex gap-2">
                            <input type="text" id="j-catatan" placeholder="Contoh: Kocor NPK sesuai jadwal" required class="w-full px-3 py-2 rounded-xl border border-slate-300 text-xs">
                            <button type="submit" class="px-4 py-2 bg-emerald-600 hover:bg-emerald-700 text-white font-bold rounded-xl text-xs shrink-0 transition">Simpan</button>
                        </div>
                    </div>
                </form>
            </div>
            <div class="bg-white rounded-2xl shadow-sm border border-slate-200 overflow-hidden">
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="bg-slate-50 border-b border-slate-200 text-[11px] font-bold uppercase tracking-wider text-slate-600">
                                <th class="py-3.5 px-4">Tanggal</th>
                                <th class="py-3.5 px-4">Umur</th>
                                <th class="py-3.5 px-4">Tinggi</th>
                                <th class="py-3.5 px-4">Aktivitas</th>
                                <th class="py-3.5 px-4">Catatan Teknis & Dosis</th>
                                <th class="py-3.5 px-4 text-right">Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="journal-table-body" class="divide-y divide-slate-200 text-xs text-slate-700"></tbody>
                    </table>
                </div>
            </div>
        </section>

    </main>

    <!-- Footer -->
    <footer class="bg-slate-900 text-slate-400 border-t border-slate-800 mt-12">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 flex flex-col sm:flex-row items-center justify-between gap-4 text-xs">
            <div><span class="font-display font-bold text-white">AgriRawit Pro</span> • Sistem Pendukung Keputusan Budidaya <em>Capsicum frutescens</em> L.</div>
            <div class="text-slate-500">Disusun berdasarkan SOP Balitsa Kementan RI, Buku Syukur et al. (2015), & Cahyono (2012).</div>
        </div>
    </footer>

    <!-- ========================================================================= -->
    <!-- JAVASCRIPT LOGIC & DATABASES                                              -->
    <!-- ========================================================================= -->
    <script>
        const sopData = [
            {
                badge: "FASE 1 • -25 s/d 0 HST",
                title: "Persiapan Benih, Persemaian & Media Pot",
                reference: "Ref: SOP Balitsa Kementan RI & Syukur et al. (2015)",
                objective: "Menghasilkan bibit seragam, perakaran kuat, dan bebas patogen tular benih maupun virus awal.",
                steps: [
                    { head: "Seleksi & Perlakuan Benih", desc: "Gunakan benih bermutu berlabel. Rendam air hangat 50°C selama 30 menit atau fungisida Propamokarb (1 ml/L) selama 15 menit untuk mengeliminasi patogen permukaan." },
                    { head: "Komposisi Media Semai & Pot", desc: "Untuk tanam dalam pot/polybag, gunakan media campuran Topsoil : Kompos Matang : Arang Sekam dengan perbandingan 2 : 1 : 1. Tambahkan 50 gram Trichoderma harzianum per 10 kg media untuk mencegah busuk akar." },
                    { head: "Sungkup & Perawatan Bibit", desc: "Semai di tray 72 lubang atau polybag kecil. Berikan naungan atau sungkup kelambu kasa 50 mesh untuk melindungi dari serangan kutu kebul vektor virus." }
                ],
                svgTitle: "Anatomi Persemaian & Media Pot",
                svgCaption: "Rasio media 2:1:1 memastikan aerasi optimal dan mencegah genangan air pada akar muda.",
                svgCode: `<svg viewBox="0 0 400 220" class="w-full h-auto"><rect width="400" height="220" fill="#f8fafc" rx="10"/><path d="M40 160 Q200 20 360 160" fill="none" stroke="#10b981" stroke-width="2.5" stroke-dasharray="5,4"/><text x="200" y="42" text-anchor="middle" font-size="11" font-weight="bold" fill="#047857">Sungkup Kelambu Kasa (50 Mesh)</text><polygon points="80,160 320,160 305,195 95,195" fill="#334155"/><text x="200" y="182" text-anchor="middle" font-size="11" fill="#f8fafc" font-weight="bold">Media 2:1:1 + Trichoderma</text><g transform="translate(200,160)"><line x1="0" y1="0" x2="0" y2="-36" stroke="#15803d" stroke-width="3"/><ellipse cx="-11" cy="-24" rx="11" ry="5" fill="#22c55e"/><ellipse cx="11" cy="-24" rx="11" ry="5" fill="#22c55e"/></g><text x="200" y="108" text-anchor="middle" font-size="10" fill="#475569">Siap Pindah Tanam: Umur 21–25 HSS</text></svg>`
            },
            {
                badge: "FASE 2 • -14 s/d -1 HST",
                title: "Persiapan Wadah Pot/Polybag & Pengapuran",
                reference: "Ref: Cahyono (2012) & SOP Balitsa",
                objective: "Menciptakan media tumbuh gembur, pH stabil (6,0–6,8), dan kaya unsur hara.",
                steps: [
                    { head: "Pemilihan Ukuran Pot", desc: "Gunakan pot atau polybag dengan diameter minimal 40 cm agar ruang perakaran cabai rawit berkembang maksimal dan mampu menopang produksi buah lebat." },
                    { head: "Aplikasi Dolomit", desc: "Jika pH media pot < 6,0, campurkan 1–2 sendok makan kapur pertanian (Dolomit) ke dalam setiap pot dan biarkan selama 7 hari sebelum bibit ditanam." },
                    { head: "Pupuk Dasar Pot", desc: "Campurkan 1-2 kg pupuk kandang matang dan 5 gram NPK 16-16-16 ke dalam setiap pot sebagai cadangan hara awal." }
                ],
                svgTitle: "Penampang Pot / Polybag 40 cm",
                svgCaption: "Lapisan dasar pot diberi pecahan genteng/batu bata agar drainase air lancar.",
                svgCode: `<svg viewBox="0 0 400 220" class="w-full h-auto"><rect width="400" height="220" fill="#f8fafc" rx="10"/><path d="M120 50 L140 180 Q200 195 260 180 L280 50 Z" fill="#92400e" stroke="#78350f" stroke-width="3"/><rect x="135" y="165" width="130" height="15" fill="#334155"/><text x="200" y="115" text-anchor="middle" font-size="11" font-weight="bold" fill="#fef3c7">Media Pot 2:1:1 + Dolomit</text><text x="200" y="180" text-anchor="middle" font-size="9" fill="#fff">Lapisan Drainase</text></svg>`
            },
            {
                badge: "FASE 3 • 0 s/d 7 HST",
                title: "Pindah Tanam (Transplanting) & Pemasangan Ajir",
                reference: "Ref: Syukur et al. (2015)",
                objective: "Menjamin adaptasi bibit di pot tanpa stres berlebihan.",
                steps: [
                    { head: "Waktu Tanam Sore Hari", desc: "Lakukan pemindahan bibit ke pot pada sore hari (pukul 15.30–17.30) untuk menghindari sengatan terik matahari langsung." },
                    { head: "Penyiraman Awal", desc: "Siram media pot secukupnya dan berikan larutan fungisida hayati untuk mencegah rebah batang (damping-off)." },
                    { head: "Pemasangan Ajir Bambu", desc: "Pasang ajir bambu setinggi 100-120 cm di samping tanaman pada umur 7 HST untuk menyangga pertumbuhan tajuk." }
                ],
                svgTitle: "Bibit di Pot & Penyangga Ajir",
                svgCaption: "Ajir dipasang miring menjauhi pangkal batang agar tidak merusak perakaran utama.",
                svgCode: `<svg viewBox="0 0 400 220" class="w-full h-auto"><rect width="400" height="220" fill="#f8fafc" rx="10"/><path d="M130 70 L150 190 Q200 205 250 190 L270 70 Z" fill="#b45309"/><line x1="200" y1="200" x2="240" y2="25" stroke="#64748b" stroke-width="4"/><g transform="translate(200,85)"><line x1="0" y1="30" x2="0" y2="-15" stroke="#15803d" stroke-width="5"/><circle cx="0" cy="-20" r="14" fill="#22c55e"/></g><text x="200" y="215" text-anchor="middle" font-size="10" fill="#475569">Pot Diameter 40 cm</text></svg>`
            },
            {
                badge: "FASE 4 • 14 s/d 45 HST",
                title: "Pewiwilan Tunas Air & Pemupukan Kocor Vegetatif",
                reference: "Ref: Jurnal Agronomi & Kementan",
                objective: "Membentuk percabangan Y yang kokoh dan mempercepat pertumbuhan vegetatif.",
                steps: [
                    { head: "Pewiwilan Tunas Air", desc: "Buang seluruh tunas air atau cabang yang tumbuh di bawah titik percabangan Y pada pagi hari agar nutrisi terfokus ke tajuk utama." },
                    { head: "Pemupukan Kocor Berkala", desc: "Berikan pupuk kocor NPK dan zat humat sesuai jadwal untuk merangsang pembentukan daun dan penguatan batang." }
                ],
                svgTitle: "Anatomi Cabang Y & Titik Wiwil",
                svgCaption: "Pewiwilan rutin di bawah cabang Y mencegah tanaman tumbuh terlalu rimbun dan lembab.",
                svgCode: `<svg viewBox="0 0 400 220" class="w-full h-auto"><rect width="400" height="220" fill="#f8fafc" rx="10"/><line x1="200" y1="190" x2="200" y2="105" stroke="#15803d" stroke-width="6"/><path d="M200 108 L145 45 M200 108 L255 45" stroke="#16a34a" stroke-width="5"/><text x="200" y="92" text-anchor="middle" font-size="11" font-weight="bold" fill="#b45309">Titik Cabang Y (Pusat Produksi)</text></svg>`
            },
            {
                badge: "FASE 5 • 35 s/d 75 HST",
                title: "Fase Generatif, Pembungaan & Pencegahan Rontok",
                reference: "Ref: Jurnal Hortikultura",
                objective: "Meningkatkan persentase jadi buah dan mencegah kerontokan bunga.",
                steps: [
                    { head: "Transisi Pupuk P & K Tinggi", desc: "Ganti atau kombinasikan pupuk NPK dengan MKP dan KNO3 untuk merangsang pembentukan bunga lebat." },
                    { head: "Aplikasi Kalsium & Boron", desc: "Semprotkan pupuk kalsium daun untuk mencegah busuk ujung buah (blossom-end rot) yang sering terjadi pada tanaman dalam pot." }
                ],
                svgTitle: "Fase Pembungaan & Pengisian Buah",
                svgCaption: "Kecukupan Kalium dan Kalsium menjamin buah cabai rawit pedas, keras, dan mengkilap.",
                svgCode: `<svg viewBox="0 0 400 220" class="w-full h-auto"><rect width="400" height="220" fill="#f8fafc" rx="10"/><rect x="90" y="70" width="220" height="80" rx="12" fill="#fef2f2" stroke="#dc2626" stroke-width="1.5"/><text x="200" y="115" text-anchor="middle" font-size="12" font-weight="bold" fill="#991b1b">Optimasi Fosfat, Kalium & Kalsium</text></svg>`
            },
            {
                badge: "FASE 6 • 75+ HST",
                title: "Panen Bertahap & Pemulihan Tanaman",
                reference: "Ref: SNI & Buku Budidaya",
                objective: "Menjaga kontinuitas produksi cabai rawit hingga puluhan petikan.",
                steps: [
                    { head: "Waktu Panen Pagi Hari", desc: "Petik buah cabai rawit saat tingkat kemasakan mencapai 85-90% (merah/oranye mengkilap) beserta tangkainya agar tidak melukai cabang." },
                    { head: "Pemulihan Pasca Petik", desc: "Berikan kocor susulan NPK + KNO3 setiap selesai 2 kali petikan untuk memulihkan tenaga tanaman dan merangsang flush bunga baru." }
                ],
                svgTitle: "Siklus Panen & Flushing",
                svgCaption: "Puncak produktivitas pot terjaga dengan pemupukan susulan rutin.",
                svgCode: `<svg viewBox="0 0 400 220" class="w-full h-auto"><rect width="400" height="220" fill="#f8fafc" rx="10"/><line x1="40" y1="110" x2="360" y2="110" stroke="#cbd5e1" stroke-width="4"/><circle cx="70" cy="110" r="14" fill="#dc2626"/><text x="70" y="114" text-anchor="middle" font-size="9" fill="#fff" font-weight="bold">P1</text><circle cx="200" cy="110" r="15" fill="#059669"/><text x="200" y="114" text-anchor="middle" font-size="9" fill="#fff" font-weight="bold">Kocor</text></svg>`
            }
        ];

        // 12 FASE PEMUPUKAN KOCOR BERDASARKAN KEMENTAN & BUKU PANDUAN (BASIS 100 LITER AIR)
        const fertilizerScheduleMaster = [
            { hst: 7, label: "7 HST", std: "NPK 1kg + Humat 100g", nPkVal: 1, humatVal: 100, mkpVal: 0, pocVal: 0, caVal: 0, kno3Val: 0, desc: "Memacu pertumbuhan akar & vegetatif awal." },
            { hst: 14, label: "14 HST", std: "NPK 1.5kg", nPkVal: 1.5, humatVal: 0, mkpVal: 0, pocVal: 0, caVal: 0, kno3Val: 0, desc: "Memperkuat batang dan percepatan jumlah daun." },
            { hst: 21, label: "21 HST", std: "NPK 2kg + POC 0.5L", nPkVal: 2, humatVal: 0, mkpVal: 0, pocVal: 0.5, caVal: 0, kno3Val: 0, desc: "Nutrisi seimbang saat pembentukan cabang Y." },
            { hst: 28, label: "28 HST", std: "NPK 2kg", nPkVal: 2, humatVal: 0, mkpVal: 0, pocVal: 0, caVal: 0, kno3Val: 0, desc: "Mempersiapkan tanaman memasuki fase pembungaan." },
            { hst: 35, label: "35 HST", std: "NPK 1.5kg + MKP 1kg", nPkVal: 1.5, humatVal: 0, mkpVal: 1, pocVal: 0, caVal: 0, kno3Val: 0, desc: "Phosphat & Kalium tinggi penahan gugur bunga." },
            { hst: 42, label: "42 HST", std: "NPK 1kg + MKP 1.5kg + Ca 0.5kg", nPkVal: 1, humatVal: 0, mkpVal: 1.5, pocVal: 0, caVal: 0.5, kno3Val: 0, desc: "Penguatan dinding sel & pembentukan calon buah." },
            { hst: 50, label: "50 HST", std: "NPK 1kg + KNO3 1.5kg", nPkVal: 1, humatVal: 0, mkpVal: 0, pocVal: 0, caVal: 0, kno3Val: 1.5, desc: "Optimasi pengisian bobot, ukuran, dan rasa pedas." },
            { hst: 60, label: "60 HST", std: "NPK 1.5kg + KNO3 1kg + Ca 0.5kg", nPkVal: 1.5, humatVal: 0, mkpVal: 0, pocVal: 0, caVal: 0.5, kno3Val: 1, desc: "Kontinuitas produktivitas buah fase panen awal." },
            { hst: 70, label: "70 HST", std: "MKP 1.5kg + KNO3 1.5kg", nPkVal: 0, humatVal: 0, mkpVal: 1.5, pocVal: 0, caVal: 0, kno3Val: 1.5, desc: "Puncak pemupukan generatif masa panen raya." },
            { hst: 80, label: "80 HST", std: "NPK 1.5kg + KNO3 1kg", nPkVal: 1.5, humatVal: 0, mkpVal: 0, pocVal: 0, caVal: 0, kno3Val: 1, desc: "Pemulihan nutrisi pasca petikan ke-3 dan ke-4." },
            { hst: 90, label: "90 HST", std: "NPK 1kg + MKP 1kg + Ca 0.5kg", nPkVal: 1, humatVal: 0, mkpVal: 1, pocVal: 0, caVal: 0.5, kno3Val: 0, desc: "Menjaga kualitas buah susulan & ketahanan fisik." },
            { hst: 100, label: "100+ HST", std: "NPK 2kg + KNO3 1kg", nPkVal: 2, humatVal: 0, mkpVal: 0, pocVal: 0, caVal: 0, kno3Val: 1, desc: "Suplai hara lanjutan untuk flushes buah berikutnya." }
        ];

        // KLINIK OPT LENGKAP BERDASARKAN JURNAL BALITSA & BUKU PHT
        const optDatabase = [
            { id: "thrips", name: "Thrips (Thrips parvispinus)", category: "hama", tagBadge: "Hama Utama", severity: "Tinggi", symptom: "Daun muda mengeriting ke atas, berwarna keperakan atau perunggu di permukaan bawah daun.", kulturTeknis: "Pemasangan perangkap warna kuning/biru (yellow/blue sticky trap), sanitasi gulma.", hayati: "Penyemprotan jamur entomopatogen Beauveria bassiana.", kimiawi: "Insektisida berbahan aktif Abamektin atau Spinetoram dengan rotasi ketat." },
            { id: "kutukebul", name: "Kutu Kebul (Bemisia tabaci) & Virus Gemini", category: "virus", tagBadge: "Vektor Virus Kuning", severity: "Sangat Kritis", symptom: "Daun pucuk menguning cerah (klorosis mosaik), tulang daun menebal dan menggulung ke bawah.", kulturTeknis: "Penggunaan sungkup kasa pada fase bibit, cabut dan bakar tanaman yang terinfeksi dini.", hayati: "Aplikasi minyak mimba (neem oil) atau ekstrak bawang putih.", kimiawi: "Insektisida sistemik berbahan aktif Pimetrozin atau Buprofezin." },
            { id: "antraknosa", name: "Antraknosa / Patek (Colletotrichum spp.)", category: "penyakit", tagBadge: "Penyakit Jamur Buah", severity: "Sangat Tinggi", symptom: "Bercak bulat cekung pada buah cabai, bagian tengahnya berwarna gelap/hitam dan berair, mudah busuk.", kulturTeknis: "Menjaga jarak tanam, pemangkasan daun bawah yang terlalu rimbun, petik dan musnahkan buah sakit.", hayati: "Aplikasi agens hayati Bacillus subtilis.", kimiawi: "Fungisida kontak berbahan aktif Mankozeb atau sistemik Azoksistrobin + Difenokonazol." },
            { id: "fusarium", name: "Layu Fusarium (Fusarium oxysporum)", category: "penyakit", tagBadge: "Penyakit Tanah", severity: "Tinggi", symptom: "Tanaman layu mendadak pada siang hari dan tampak segar kembali pada malam hari, pangkal batang membusuk kecokelatan.", kulturTeknis: "Pengapuran dolomit untuk menaikkan pH, sterilisasi media tanam pot dengan Trichoderma.", hayati: "Penyiraman Trichoderma harzianum di sekitar perakaran.", kimiawi: "Fungisida sistemik berbahan aktif Benomil atau Karbendazim." },
            { id: "gemini", name: "Kutu Daun (Aphis gossypii)", category: "hama", tagBadge: "Hama Pengisap", severity: "Sedang", symptom: "Koloni kutu bergerombol di pucuk tanaman, mengeluarkan cairan embun madu yang memicu jamur jelaga.", kulturTeknis: "Penyemprotan air bertekanan untuk merontokkan koloni, musnahkan semut penjaga.", hayati: "Pelepasan kumbang koksi (Coccinella septempunctata) sebagai predator alami.", kimiawi: "Insektisida Imidakloprid atau Asetamiprid dosis rendah." },
            { id: "bppot", name: "Busuk Ujung Buah (Blossom-End Rot)", category: "fisiologis", tagBadge: "Gangguan Fisiologis Pot", severity: "Sedang", symptom: "Bagian pantat atau ujung buah cabai berwarna hitam, kering, dan cekung saat menjelang masak.", kulturTeknis: "Ketersediaan air penyiraman pot yang stabil, hindari kekeringan ekstrem.", hayati: "Pemberian kompos matang kaya kalsium.", kimiawi: "Aplikasi pupuk daun kalsium nitrat secara teratur." }
        ];

        let npkChartInstance = null;
        let ecoChartInstance = null;
        const varietasConfig = {
            ori212: { name: "Ori 212", harvestHst: 80, yieldEst: "0.8 - 1.2 kg/pohon" },
            dewata43: { name: "Dewata 43 F1", harvestHst: 75, yieldEst: "0.7 - 1.0 kg/pohon" },
            bara: { name: "Bara", harvestHst: 85, yieldEst: "0.8 - 1.1 kg/pohon" },
            pelita8: { name: "Pelita 8 F1", harvestHst: 80, yieldEst: "0.8 - 1.2 kg/pohon" },
            lokal: { name: "Rawit Lokal", harvestHst: 90, yieldEst: "0.6 - 0.9 kg/pohon" }
        };

        window.addEventListener('DOMContentLoaded', () => {
            lucide.createIcons();
            const todayStr = new Date().toISOString().split('T')[0];
            document.getElementById('input-tgl-tanam').value = todayStr;
            document.getElementById('j-tanggal').value = todayStr;

            selectSopPhase(0);
            initNpkChart();
            generateSchedule(false);
            calculateAgronomyPot();
            renderFertilizerTable();
            filterOpt('all');
            calculateEconomics();
            renderJournalTable();
        });

        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.remove('active'));
            document.getElementById(tabId).classList.add('active');
            document.querySelectorAll('.nav-btn').forEach(btn => {
                if (btn.dataset.tab === tabId) {
                    btn.classList.add('active', 'bg-emerald-600', 'text-white', 'shadow-sm');
                    btn.classList.remove('text-emerald-200', 'hover:bg-emerald-900/70');
                } else {
                    btn.classList.remove('active', 'bg-emerald-600', 'text-white', 'shadow-sm');
                    btn.classList.add('text-emerald-200', 'hover:bg-emerald-900/70');
                }
            });
            if (tabId === 'tab-ekonomi' && ecoChartInstance) ecoChartInstance.resize();
            if (tabId === 'tab-sop' && npkChartInstance) npkChartInstance.resize();
        }

        function toggleModal(modalId, show) {
            const modal = document.getElementById(modalId);
            if (show) modal.classList.remove('hidden'); else modal.classList.add('hidden');
        }

        function showToast(message, type = 'success') {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            toast.className = `pointer-events-auto flex items-center gap-2.5 px-4 py-3 rounded-xl border shadow-lg text-xs font-semibold bg-emerald-900 border-emerald-700 text-white`;
            toast.innerHTML = `<i data-lucide="check-circle-2" class="w-4 h-4 text-emerald-400 shrink-0"></i><span>${message}</span>`;
            container.appendChild(toast);
            lucide.createIcons();
            setTimeout(() => { toast.remove(); }, 3000);
        }

        function selectSopPhase(index) {
            const data = sopData[index];
            document.querySelectorAll('.sop-btn').forEach((btn, idx) => {
                if (idx === index) {
                    btn.classList.add('active', 'border-2', 'border-emerald-600', 'bg-emerald-50/80');
                    btn.classList.remove('border', 'border-slate-200', 'bg-white');
                } else {
                    btn.classList.remove('active', 'border-2', 'border-emerald-600', 'bg-emerald-50/80');
                    btn.classList.add('border', 'border-slate-200', 'bg-white');
                }
            });
            document.getElementById('sop-detail-container').innerHTML = `
                <div class="flex flex-wrap items-center justify-between gap-2 pb-3 border-b border-slate-100">
                    <span class="px-3 py-1 rounded-full bg-emerald-100 text-emerald-800 text-xs font-bold">${data.badge}</span>
                    <span class="text-[11px] font-medium text-slate-500">${data.reference}</span>
                </div>
                <div>
                    <h3 class="font-display font-extrabold text-xl text-slate-900">${data.title}</h3>
                    <p class="text-xs sm:text-sm text-emerald-800 bg-emerald-50/70 p-3 rounded-xl border border-emerald-200/60 mt-2.5">
                        <strong>Target Agronomi:</strong> ${data.objective}
                    </p>
                </div>
                <div class="space-y-3.5">
                    ${data.steps.map((step, i) => `
                        <div class="p-4 rounded-xl bg-slate-50 border border-slate-200/80">
                            <div class="flex items-center gap-2.5">
                                <span class="w-6 h-6 rounded-lg bg-emerald-700 text-white font-bold text-xs flex items-center justify-center shrink-0">${i + 1}</span>
                                <h4 class="font-bold text-sm text-slate-900">${step.head}</h4>
                            </div>
                            <p class="text-xs sm:text-sm text-slate-600 mt-2 pl-8">${step.desc}</p>
                        </div>
                    `).join('')}
                </div>
            `;
            document.getElementById('svg-diagram-title').textContent = data.svgTitle;
            document.getElementById('sop-svg-container').innerHTML = data.svgCode;
            document.getElementById('svg-diagram-caption').textContent = data.svgCaption;
            lucide.createIcons();
        }

        function initNpkChart() {
            const ctx = document.getElementById('npkChart').getContext('2d');
            npkChartInstance = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['0-14 HST', '21-35 HST', '42-56 HST', '63-75 HST', '80+ HST'],
                    datasets: [
                        { label: 'Nitrogen (N)', data: [55, 65, 35, 25, 25], borderColor: '#10b981', backgroundColor: 'rgba(16, 185, 129, 0.1)', tension: 0.35, fill: true },
                        { label: 'Fosfat (P)', data: [30, 20, 35, 25, 20], borderColor: '#f59e0b', backgroundColor: 'transparent', tension: 0.35 },
                        { label: 'Kalium (K)', data: [15, 15, 30, 50, 55], borderColor: '#ef4444', backgroundColor: 'rgba(239, 68, 68, 0.08)', tension: 0.35, fill: true }
                    ]
                },
                options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { position: 'bottom', labels: { boxWidth: 12 } } }, scales: { y: { beginAtZero: true, max: 80 } } }
            });
        }

        // KALENDER TANAM OTOMATIS
        function addDays(dateStr, days) {
            const d = new Date(dateStr);
            d.setDate(d.getDate() + days);
            return d;
        }
        function formatIndoDate(dateObj) {
            return dateObj.toLocaleDateString('id-ID', { day: 'numeric', month: 'short', year: 'numeric' });
        }

        function generateSchedule(notify = true) {
            const plantDateStr = document.getElementById('input-tgl-tanam').value;
            const variety = document.getElementById('input-varietas').value;
            const vInfo = varietasConfig[variety];
            const harvestHst = vInfo.harvestHst;

            const today = new Date();
            today.setHours(0,0,0,0);
            const pDate = new Date(plantDateStr);
            pDate.setHours(0,0,0,0);
            const diffTime = today - pDate;
            const currentHst = Math.floor(diffTime / (1000 * 60 * 60 * 24));

            document.getElementById('global-hst-badge').textContent = `HST Aktif: ${currentHst >= 0 ? currentHst + ' Hari Setelah Tanam' : Math.abs(currentHst) + ' Hari Menuju Pindah Tanam'}`;
            document.getElementById('banner-tgl-tanam').textContent = formatIndoDate(pDate);
            
            let faseStr = "Persiapan Persemaian";
            if (currentHst >= 0 && currentHst <= 14) faseStr = "Fase Vegetatif Awal";
            else if (currentHst > 14 && currentHst <= 35) faseStr = "Fase Vegetatif Aktif & Cabang Y";
            else if (currentHst > 35 && currentHst <= 74) faseStr = "Fase Generatif & Pembungaan";
            else if (currentHst >= 75) faseStr = "Fase Panen & Pascapanen";
            document.getElementById('banner-fase-aktif').textContent = faseStr;

            const tasks = [
                { id: 't1', hst: -21, title: "Persemaian Benih & Trichoderma", desc: "Semai benih di tray/polybag kecil dengan sungkup kasa pelindung.", tag: "Persemaian" },
                { id: 't2', hst: -14, title: "Persiapan Media Pot & Dolomit", desc: "Campur media 2:1:1 + dolomit ke dalam pot ukuran 40 cm.", tag: "Media" },
                { id: 't3', hst: -3, title: "Penyiraman Awal Media Pot", desc: "Pastikan kelembapan media pot stabil sebelum pindah tanam.", tag: "Media" },
                { id: 't4', hst: 0, title: "Pindah Tanam (Transplanting) Sore Hari", desc: "Tanam bibit umur 21 HSS ke pot utama + siram Trichoderma.", tag: "Tanam" },
                { id: 't5', hst: 7, title: "Penyulaman & Kocor Pemupukan 1", desc: "Pasang ajir bambu 120 cm, kocor NPK 1kg + Humat 100g (skala pot).", tag: "Pemupukan" },
                { id: 't6', hst: 14, title: "Pewiwilan Tunas Air 1 & Kocor 2", desc: "Rempel tunas di bawah cabang Y, kocor NPK 1.5kg.", tag: "Perawatan" },
                { id: 't7', hst: 21, title: "Pewiwilan Tunas Air 2 & Kocor 3", desc: "Lanjutkan pembersihan tunas bawah cabang Y, kocor NPK 2kg + POC 0.5L.", tag: "Perawatan" },
                { id: 't8', hst: 28, title: "Kocor Vegetatif Lanjut 4", desc: "Kocor NPK 2kg per 100L air.", tag: "Pemupukan" },
                { id: 't9', hst: 35, title: "Pengikatan Batang ke Ajir & Kocor 5", desc: "Kocor NPK 1.5kg + MKP 1kg penahan gugur bunga.", tag: "Proteksi" },
                { id: 't10', hst: 42, title: "Kocor Transisi Generatif 6", desc: "Kocor NPK 1kg + MKP 1.5kg + Kalsium 0.5kg.", tag: "Generatif" },
                { id: 't11', hst: 50, title: "Kocor Pengisian Buah 7", desc: "Kocor NPK 1kg + KNO3 1.5kg (optimasi bobot & rasa pedas).", tag: "Generatif" },
                { id: 't12', hst: 60, title: "Kocor Kontinuitas Panen 8", desc: "Kocor NPK 1.5kg + KNO3 1kg + Kalsium 0.5kg.", tag: "Panen" },
                { id: 't13', hst: harvestHst, title: `Estimasi Panen Perdana (${vInfo.name})`, desc: "Petik buah masak fisiologis beserta tangkainya pada pagi hari.", tag: "Panen" }
            ];

            const savedState = JSON.parse(localStorage.getItem('agrirawit_schedule_v3') || '{"completed":[]}');
            
            document.getElementById('schedule-summary-cards').innerHTML = `
                <div class="p-3.5 rounded-xl bg-slate-50 border border-slate-200">
                    <div class="text-[11px] font-semibold text-slate-500">Mulai Semai (-21 HST)</div>
                    <div class="font-display font-bold text-sm text-slate-900 mt-0.5">${formatIndoDate(addDays(plantDateStr, -21))}</div>
                </div>
                <div class="p-3.5 rounded-xl bg-emerald-50 border border-emerald-200">
                    <div class="text-[11px] font-semibold text-emerald-700">Pindah Tanam (0 HST)</div>
                    <div class="font-display font-bold text-sm text-emerald-900 mt-0.5">${formatIndoDate(pDate)}</div>
                </div>
                <div class="p-3.5 rounded-xl bg-amber-50 border border-amber-200">
                    <div class="text-[11px] font-semibold text-amber-700">Estimasi Panen</div>
                    <div class="font-display font-bold text-sm text-amber-900 mt-0.5">${formatIndoDate(addDays(plantDateStr, harvestHst))}</div>
                </div>
                <div class="p-3.5 rounded-xl bg-slate-50 border border-slate-200">
                    <div class="text-[11px] font-semibold text-slate-500">Potensi Hasil / Pohon</div>
                    <div class="font-display font-bold text-sm text-slate-900 mt-0.5">${vInfo.yieldEst}</div>
                </div>
            `;

            const doneCount = savedState.completed.length;
            document.getElementById('checklist-progress-badge').textContent = `Progres: ${doneCount} / ${tasks.length} Selesai`;

            document.getElementById('schedule-timeline-list').innerHTML = tasks.map(t => {
                const isDone = savedState.completed.includes(t.id);
                const taskDate = formatIndoDate(addDays(plantDateStr, t.hst));
                const hstLabel = t.hst === 0 ? "0 HST" : (t.hst > 0 ? `+${t.hst} HST` : `${t.hst} HST`);
                return `
                    <label class="flex items-start gap-3.5 p-4 hover:bg-slate-50 cursor-pointer transition ${isDone ? 'bg-emerald-50/40' : ''}">
                        <input type="checkbox" ${isDone ? 'checked' : ''} onchange="toggleTask('${t.id}')" class="mt-1 w-4 h-4 rounded text-emerald-600 border-slate-300">
                        <div class="flex-1 min-w-0">
                            <div class="flex items-center justify-between">
                                <div class="flex items-center gap-2">
                                    <span class="px-2 py-0.5 rounded text-[11px] font-bold ${t.hst >= harvestHst ? 'bg-chili-600 text-white' : 'bg-slate-200 text-slate-800'}">${hstLabel}</span>
                                    <span class="text-xs font-bold text-emerald-700">${taskDate}</span>
                                </div>
                                <span class="text-[10px] font-semibold uppercase px-2 py-0.5 rounded bg-slate-100 text-slate-600">${t.tag}</span>
                            </div>
                            <h4 class="font-bold text-sm mt-1 ${isDone ? 'line-through text-slate-400' : 'text-slate-900'}">${t.title}</h4>
                            <p class="text-xs text-slate-500 mt-0.5">${t.desc}</p>
                        </div>
                    </label>
                `;
            }).join('');

            if(notify) showToast("Jadwal kalender diperbarui!");
        }

        function toggleTask(id) {
            let state = JSON.parse(localStorage.getItem('agrirawit_schedule_v3') || '{"completed":[]}');
            if(state.completed.includes(id)) {
                state.completed = state.completed.filter(item => item !== id);
            } else {
                state.completed.push(id);
            }
            localStorage.setItem('agrirawit_schedule_v3', JSON.stringify(state));
            generateSchedule(false);
        }

        function resetChecklist() {
            localStorage.setItem('agrirawit_schedule_v3', JSON.stringify({"completed":[]}));
            generateSchedule(false);
            showToast("Checklist direset.");
        }

        // KALKULATOR DOSIS PEMUPUKAN BERDASARKAN POPULASI POT & 100L AIR
        function calculateAgronomyPot() {
            const populasi = parseFloat(document.getElementById('calc-jml-tanaman').value) || 25;
            const ph = parseFloat(document.getElementById('calc-ph').value) || 6.0;

            const totalAirLiter = populasi * 0.2; // 200 ml per tanaman
            document.getElementById('total-air-badge').textContent = `${totalAirLiter.toFixed(1)} Liter`;
            document.getElementById('badge-pop-count').textContent = populasi;
            document.getElementById('table-populasi-label').textContent = populasi;

            const deltaPh = Math.max(0, 6.2 - ph);
            const dolomitSendok = Math.round((deltaPh / 0.5) * 1.5 * populasi);

            document.getElementById('calc-pot-output').innerHTML = `
                <div class="bg-white p-3 rounded-lg border border-slate-200">
                    <div class="text-[11px] text-slate-500">Total Air Kocor Sekali Aplikasi</div>
                    <div class="font-display font-extrabold text-base text-emerald-700">${totalAirLiter.toFixed(1)} Liter</div>
                </div>
                <div class="bg-white p-3 rounded-lg border border-slate-200">
                    <div class="text-[11px] text-slate-500">Dolomit Total untuk ${populasi} Pot</div>
                    <div class="font-display font-extrabold text-base text-amber-700">${dolomitSendok} sendok makan</div>
                </div>
            `;
            renderFertilizerTable();
        }

        function renderFertilizerTable() {
            const populasi = parseFloat(document.getElementById('calc-jml-tanaman').value) || 25;
            const totalAirLiter = populasi * 0.2;
            const pengali = totalAirLiter / 100;

            const tbody = document.getElementById('fertilizer-table-body');
            tbody.innerHTML = fertilizerScheduleMaster.map(item => {
                let rArray = [];
                if(item.nPkVal > 0) {
                    let val = (item.nPkVal * pengali).toFixed(2);
                    rArray.push(`NPK: <strong>${val} kg</strong>`);
                }
                if(item.humatVal > 0) {
                    let val = Math.round(item.humatVal * pengali);
                    rArray.push(`Humat: <strong>${val} gram</strong>`);
                }
                if(item.mkpVal > 0) {
                    let val = (item.mkpVal * pengali).toFixed(2);
                    rArray.push(`MKP: <strong>${val} kg</strong>`);
                }
                if(item.pocVal > 0) {
                    let val = (item.pocVal * pengali).toFixed(2);
                    rArray.push(`POC: <strong>${val} Liter</strong>`);
                }
                if(item.caVal > 0) {
                    let val = (item.caVal * pengali).toFixed(2);
                    rArray.push(`Kalsium: <strong>${val} kg</strong>`);
                }
                if(item.kno3Val > 0) {
                    let val = (item.kno3Val * pengali).toFixed(2);
                    rArray.push(`KNO3: <strong>${val} kg</strong>`);
                }
                const rumusPotStr = rArray.join(' + ');

                return `
                    <tr class="hover:bg-slate-50 transition">
                        <td class="py-3 px-4 font-bold text-emerald-800 whitespace-nowrap">${item.label}</td>
                        <td class="py-3 px-4 font-medium text-slate-700">${item.std}</td>
                        <td class="py-3 px-4 bg-emerald-50/40 text-slate-900 font-semibold">${rumusPotStr} <br><span class="text-[10px] text-slate-500">(${totalAirLiter.toFixed(1)} L air total)</span></td>
                        <td class="py-3 px-4 text-slate-600">${item.desc}</td>
                    </tr>
                `;
            }).join('');
        }

        // KLINIK OPT FILTER
        function filterOpt(tag) {
            document.querySelectorAll('.opt-filter-btn').forEach(btn => {
                if (btn.dataset.filter === tag) {
                    btn.classList.add('active', 'bg-emerald-600', 'text-white');
                    btn.classList.remove('bg-slate-100', 'text-slate-700');
                } else {
                    btn.classList.remove('active', 'bg-emerald-600', 'text-white');
                    btn.classList.add('bg-slate-100', 'text-slate-700');
                }
            });
            const filtered = tag === 'all' ? optDatabase : optDatabase.filter(i => i.category === tag);
            document.getElementById('opt-cards-container').innerHTML = filtered.map(opt => `
                <div class="bg-white rounded-2xl p-5 shadow-sm border border-slate-200 space-y-3">
                    <div class="flex justify-between items-start">
                        <div>
                            <span class="text-[10px] font-bold uppercase px-2 py-0.5 rounded bg-slate-100 text-slate-700">${opt.tagBadge}</span>
                            <h3 class="font-display font-bold text-base text-slate-900 mt-1">${opt.name}</h3>
                        </div>
                        <span class="text-[11px] font-bold px-2.5 py-1 rounded bg-red-50 text-red-700 border border-red-200">Risiko: ${opt.severity}</span>
                    </div>
                    <div class="p-3 rounded-xl bg-amber-50 border border-amber-200 text-xs text-slate-700"><strong>Gejala Serangan:</strong> ${opt.symptom}</div>
                    <div class="text-xs space-y-1.5 pt-2 border-t border-slate-100">
                        <div><strong class="text-emerald-700">1. Kultur Teknis:</strong> ${opt.kulturTeknis}</div>
                        <div><strong class="text-teal-700">2. Pengendalian Hayati:</strong> ${opt.hayati}</div>
                        <div><strong class="text-chili-600">3. Pengendalian Kimiawi:</strong> ${opt.kimiawi}</div>
                    </div>
                </div>
            `).join('');
        }

        // EKONOMI
        function formatRupiah(num) {
            return new Intl.NumberFormat('id-ID', { style: 'currency', currency: 'IDR', maximumFractionDigits: 0 }).format(num);
        }
        function calculateEconomics() {
            const populasi = parseFloat(document.getElementById('eco-populasi').value) || 0;
            const hasilPohon = parseFloat(document.getElementById('eco-hasil-pohon').value) || 0;
            const hargaJual = parseFloat(document.getElementById('eco-harga-jual').value) || 0;
            const bLahan = parseFloat(document.getElementById('eco-biaya-lahan').value) || 0;
            const bSaprotan = parseFloat(document.getElementById('eco-biaya-saprotan').value) || 0;
            const bPupuk = parseFloat(document.getElementById('eco-biaya-pupuk').value) || 0;
            const bPestisida = parseFloat(document.getElementById('eco-biaya-pestisida').value) || 0;

            const totalBiaya = bLahan + bSaprotan + bPupuk + bPestisida;
            const totalProduksiKg = populasi * hasilPohon;
            const totalPenerimaan = totalProduksiKg * hargaJual;
            const keuntungan = totalPenerimaan - totalBiaya;
            const rcRatio = totalBiaya > 0 ? (totalPenerimaan / totalBiaya).toFixed(2) : 0;
            const bepHarga = totalProduksiKg > 0 ? Math.round(totalBiaya / totalProduksiKg) : 0;
            const bepProd = hargaJual > 0 ? Math.round(totalBiaya / hargaJual) : 0;

            document.getElementById('eco-kpi-container').innerHTML = `
                <div class="bg-white p-4 rounded-2xl border border-slate-200">
                    <div class="text-[11px] text-slate-500">Total Modal</div>
                    <div class="font-display font-extrabold text-sm sm:text-base text-slate-900 mt-1">${formatRupiah(totalBiaya)}</div>
                </div>
                <div class="bg-white p-4 rounded-2xl border border-slate-200">
                    <div class="text-[11px] text-slate-500">Pendapatan Kotor</div>
                    <div class="font-display font-extrabold text-sm sm:text-base text-emerald-700 mt-1">${formatRupiah(totalPenerimaan)}</div>
                </div>
                <div class="col-span-2 sm:col-span-1 p-4 rounded-2xl border ${keuntungan >= 0 ? 'bg-emerald-900 text-white' : 'bg-red-900 text-white'}">
                    <div class="text-[11px] opacity-80">Keuntungan Bersih</div>
                    <div class="font-display font-extrabold text-sm sm:text-base mt-1">${formatRupiah(keuntungan)}</div>
                </div>
            `;
            document.getElementById('eco-bep-container').innerHTML = `
                <div class="p-3 rounded-xl bg-slate-50 border border-slate-200">
                    <div class="text-[11px] text-slate-500 font-semibold">BEP Harga / Kg</div>
                    <div class="font-display font-extrabold text-base text-slate-900 mt-0.5">${formatRupiah(bepHarga)}</div>
                </div>
                <div class="p-3 rounded-xl bg-slate-50 border border-slate-200">
                    <div class="text-[11px] text-slate-500 font-semibold">BEP Produksi</div>
                    <div class="font-display font-extrabold text-base text-slate-900 mt-0.5">${bepProd.toLocaleString('id-ID')} kg</div>
                </div>
                <div class="p-3 rounded-xl bg-emerald-50 border border-emerald-200">
                    <div class="text-[11px] font-semibold text-emerald-700">R/C Ratio</div>
                    <div class="font-display font-extrabold text-base text-emerald-900 mt-0.5">${rcRatio} (Layak >1.0)</div>
                </div>
            `;
            renderEcoChart([bLahan, bSaprotan, bPupuk, bPestisida]);
        }

        function renderEcoChart(arr) {
            const ctx = document.getElementById('ecoChart').getContext('2d');
            if(ecoChartInstance) ecoChartInstance.destroy();
            ecoChartInstance = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['Pot/Media', 'Benih/Ajir', 'Pupuk', 'Pestisida'],
                    datasets: [{ data: arr, backgroundColor: ['#065f46', '#059669', '#10b981', '#f59e0b'], borderRadius: 6 }]
                },
                options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false } } }
            });
        }

        // LOGBOOK
        function getJournal() {
            return JSON.parse(localStorage.getItem('agrirawit_journal_v3') || '[{"tanggal":"2026-11-01","hst":0,"tinggi":15,"kategori":"Pengamatan","catatan":"Pindah tanam bibit ke pot 40 cm"}]');
        }
        function addJournalEntry(e) {
            e.preventDefault();
            const list = getJournal();
            list.unshift({
                tanggal: document.getElementById('j-tanggal').value,
                hst: document.getElementById('j-hst').value,
                tinggi: document.getElementById('j-tinggi').value,
                kategori: document.getElementById('j-kategori').value,
                catatan: document.getElementById('j-catatan').value
            });
            localStorage.setItem('agrirawit_journal_v3', JSON.stringify(list));
            document.getElementById('j-catatan').value = '';
            renderJournalTable();
            showToast("Logbook berhasil disimpan!");
        }
        function renderJournalTable() {
            const list = getJournal();
            document.getElementById('journal-table-body').innerHTML = list.map((r, i) => `
                <tr class="hover:bg-slate-50">
                    <td class="py-3 px-4 font-medium">${r.tanggal}</td>
                    <td class="py-3 px-4"><span class="px-2 py-0.5 rounded bg-emerald-100 text-emerald-800 font-bold">${r.hst} HST</span></td>
                    <td class="py-3 px-4">${r.tinggi} cm</td>
                    <td class="py-3 px-4"><span class="px-2 py-0.5 rounded bg-slate-100 text-slate-700 text-[11px]">${r.kategori}</span></td>
                    <td class="py-3 px-4">${r.catatan}</td>
                    <td class="py-3 px-4 text-right"><button onclick="deleteJournal(${i})" class="text-slate-400 hover:text-red-600"><i data-lucide="trash-2" class="w-4 h-4"></i></button></td>
                </tr>
            `).join('');
            lucide.createIcons();
        }
        function deleteJournal(idx) {
            let list = getJournal();
            list.splice(idx, 1);
            localStorage.setItem('agrirawit_journal_v3', JSON.stringify(list));
            renderJournalTable();
            showToast("Catatan dihapus.");
        }
        function exportJournalCSV() {
            const list = getJournal();
            let csv = "Tanggal,HST,Tinggi,Kategori,Catatan\n";
            list.forEach(r => { csv += `${r.tanggal},${r.hst},${r.tinggi},"${r.kategori}","${r.catatan}"\n`; });
            const blob = new Blob([csv], { type: 'text/csv' });
            const link = document.createElement("a");
            link.href = URL.createObjectURL(blob);
            link.download = "Logbook_AgriRawit.csv";
            link.click();
            showToast("CSV diunduh.");
        }
    </script>
</body>
</html>
