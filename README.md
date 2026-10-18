

<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>InventoryQu - System Management Gudang Professional</title>
    <!-- Bootstrap 5 CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <!-- FontAwesome 6 -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --sidebar-width: 260px;
            --primary: #4f46e5;
            --primary-dark: #4338ca;
            --sidebar-bg: #0f172a;
            --sidebar-hover: #1e293b;
            --body-bg: #f8fafc;
            --card-bg: #ffffff;
            --text-main: #334155;
            --text-muted: #64748b;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--body-bg);
            color: var(--text-main);
            overflow-x: hidden;
        }

        /* LOGIN SCREEN */
        #login-view {
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            background: radial-gradient(circle at top right, #312e81, #0f172a);
        }

        .login-card {
            width: 100%;
            max-width: 420px;
            background: #ffffff;
            border-radius: 16px;
            box-shadow: 0 20px 25px -5px rgba(0,0,0,0.3);
            border: none;
            overflow: hidden;
        }

        /* MAIN APP LAYOUT */
        #app-view {
            display: flex;
            min-height: 100vh;
        }

        #sidebar {
            width: var(--sidebar-width);
            background-color: var(--sidebar-bg);
            color: #f8fafc;
            flex-shrink: 0;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            transition: all 0.3s;
        }

        .sidebar-brand {
            padding: 20px;
            font-size: 1.25rem;
            font-weight: 700;
            color: #fff;
            border-bottom: 1px solid rgba(255, 255, 255, 0.08);
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .sidebar-menu {
            padding: 16px 12px;
            list-style: none;
            margin: 0;
        }

        .sidebar-menu .nav-link {
            color: #94a3b8;
            padding: 12px 16px;
            border-radius: 10px;
            margin-bottom: 4px;
            display: flex;
            align-items: center;
            gap: 14px;
            font-size: 0.9rem;
            font-weight: 500;
            transition: all 0.2s;
            text-decoration: none;
        }

        .sidebar-menu .nav-link:hover,
        .sidebar-menu .nav-link.active {
            color: #ffffff;
            background-color: var(--primary);
        }

        #content-wrapper {
            flex-grow: 1;
            display: flex;
            flex-direction: column;
            min-width: 0;
        }

        .navbar-top {
            background-color: #ffffff;
            border-bottom: 1px solid #e2e8f0;
            padding: 16px 28px;
        }

        .main-content {
            padding: 28px;
            flex-grow: 1;
        }

        /* CARDS & COMPONENTS */
        .card {
            border: 1px solid #e2e8f0;
            border-radius: 12px;
            box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.05);
            background: #ffffff;
        }

        .kpi-card {
            border: 1px solid #e2e8f0;
            border-radius: 12px;
            padding: 20px;
            transition: transform 0.2s;
        }

        .kpi-card:hover {
            transform: translateY(-2px);
        }

        .kpi-icon {
            width: 48px;
            height: 48px;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.25rem;
        }

        .badge-status {
            padding: 6px 12px;
            border-radius: 20px;
            font-weight: 600;
            font-size: 0.75rem;
        }

        /* PRINT MEDIA STYLES */
        @media print {
            body * {
                visibility: hidden;
            }
            #print-section, #print-section * {
                visibility: visible;
            }
            #print-section {
                position: absolute;
                left: 0;
                top: 0;
                width: 100%;
                background: #ffffff;
                padding: 20px;
            }
            .no-print {
                display: none !important;
            }
        }
    </style>
</head>
<body>

    <!-- ================= HALAMAN LOGIN ================= -->
    <div id="login-view">
        <div class="card login-card p-4 p-md-5">
            <div class="text-center mb-4">
                <div class="d-inline-flex align-items-center justify-content-center bg-primary text-white rounded-circle mb-3" style="width:60px; height:60px;">
                    <i class="fa-solid fa-boxes-stacked fa-2x"></i>
                </div>
                <h4 class="fw-bold text-dark mb-1">InventoryQu</h4>
                <p class="text-muted small">Enterprise Warehouse System</p>
            </div>
            <div id="login-alert" class="alert alert-danger d-none small"></div>
            <form id="login-form">
                <div class="mb-3">
                    <label class="form-label small fw-semibold">Username</label>
                    <div class="input-group">
                        <span class="input-group-text bg-light border-end-0"><i class="fa-solid fa-user text-muted"></i></span>
                        <input type="text" id="login-username" class="form-control bg-light border-start-0" placeholder="admin / staff" required>
                    </div>
                </div>
                <div class="mb-4">
                    <label class="form-label small fw-semibold">Password</label>
                    <div class="input-group">
                        <span class="input-group-text bg-light border-end-0"><i class="fa-solid fa-lock text-muted"></i></span>
                        <input type="password" id="login-password" class="form-control bg-light border-start-0" placeholder="••••••••" required>
                    </div>
                </div>
                <button type="submit" class="btn btn-primary w-100 py-2 fw-semibold shadow-sm">
                    <i class="fa-solid fa-right-to-bracket me-2"></i> Masuk ke Sistem
                </button>
            </form>
            <div class="mt-4 pt-3 border-top text-center">
                <small class="text-muted">Kredensial Demo:<br><b>admin / admin</b> atau <b>staff / staff</b></small>
            </div>
        </div>
    </div>

    <!-- ================= HALAMAN UTAMA APLIKASI ================= -->
    <div id="app-view" class="d-none">
        <!-- Sidebar Navigation -->
        <aside id="sidebar">
            <div>
                <div class="sidebar-brand">
                    <i class="fa-solid fa-boxes-stacked text-primary"></i>
                    <span>InventoryQu</span>
                </div>
                <ul class="sidebar-menu">
                    <li>
                        <a href="#" class="nav-link active" onclick="switchTab('dashboard')">
                            <i class="fa-solid fa-chart-pie"></i> Dashboard
                        </a>
                    </li>
                    <li>
                        <a href="#" class="nav-link" onclick="switchTab('master')">
                            <i class="fa-solid fa-box-archive"></i> Master Produk
                        </a>
                    </li>
                    <li>
                        <a href="#" class="nav-link" onclick="switchTab('pembelian')">
                            <i class="fa-solid fa-cart-arrow-down"></i> Pembelian (Masuk)
                        </a>
                    </li>
                    <li>
                        <a href="#" class="nav-link" onclick="switchTab('penjualan')">
                            <i class="fa-solid fa-cash-register"></i> Penjualan (POS)
                        </a>
                    </li>
                    <li>
                        <a href="#" class="nav-link" onclick="switchTab('history')">
                            <i class="fa-solid fa-receipt"></i> Riwayat Transaksi
                        </a>
                    </li>
                    <li>
                        <a href="#" class="nav-link" onclick="switchTab('laporan')">
                            <i class="fa-solid fa-file-invoice-dollar"></i> Laporan Aset
                        </a>
                    </li>
                    <li>
                        <a href="#" class="nav-link" onclick="switchTab('pengaturan')">
                            <i class="fa-solid fa-sliders"></i> Pengaturan
                        </a>
                    </li>
                </ul>
            </div>
            <div class="p-3 border-top border-secondary border-opacity-25">
                <button class="btn btn-outline-danger w-100 btn-sm fw-semibold" onclick="logout()">
                    <i class="fa-solid fa-power-off me-2"></i> Keluar
                </button>
            </div>
        </aside>

        <!-- Content Area -->
        <div id="content-wrapper">
            <!-- Navbar Top -->
            <nav class="navbar navbar-top d-flex justify-content-between align-items-center">
                <h5 class="fw-bold mb-0" id="page-title">Dashboard Overview</h5>
                <div class="d-flex align-items-center gap-3">
                    <div class="text-end">
                        <div class="fw-bold small" id="logged-user-name">Administrator</div>
                        <span class="badge bg-primary-subtle text-primary border border-primary-subtle" id="user-role-badge">ADMIN</span>
                    </div>
                    <div class="bg-primary text-white rounded-circle d-flex align-items-center justify-content-center fw-bold" style="width: 40px; height: 40px;" id="user-avatar">
                        A
                    </div>
                </div>
            </nav>

            <!-- Main Content Pane -->
            <main class="main-content">
                <!-- TAB 1: DASHBOARD -->
                <div id="tab-dashboard" class="tab-pane-content">
                    <div class="row g-3 mb-4">
                        <div class="col-md-3">
                            <div class="card kpi-card">
                                <div class="d-flex justify-content-between align-items-center">
                                    <div>
                                        <div class="text-muted small fw-medium">Total Jenis Produk</div>
                                        <h3 class="fw-bold text-dark mt-1 mb-0" id="kpi-total-produk">0</h3>
                                    </div>
                                    <div class="kpi-icon bg-primary-subtle text-primary">
                                        <i class="fa-solid fa-boxes-packing"></i>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="col-md-3">
                            <div class="card kpi-card">
                                <div class="d-flex justify-content-between align-items-center">
                                    <div>
                                        <div class="text-muted small fw-medium">Omset Penjualan</div>
                                        <h3 class="fw-bold text-success mt-1 mb-0" id="kpi-total-penjualan">Rp 0</h3>
                                    </div>
                                    <div class="kpi-icon bg-success-subtle text-success">
                                        <i class="fa-solid fa-chart-line"></i>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="col-md-3">
                            <div class="card kpi-card">
                                <div class="d-flex justify-content-between align-items-center">
                                    <div>
                                        <div class="text-muted small fw-medium">Total Pembelian</div>
                                        <h3 class="fw-bold text-warning mt-1 mb-0" id="kpi-total-pembelian">Rp 0</h3>
                                    </div>
                                    <div class="kpi-icon bg-warning-subtle text-warning">
                                        <i class="fa-solid fa-truck-ramp-box"></i>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="col-md-3">
                            <div class="card kpi-card">
                                <div class="d-flex justify-content-between align-items-center">
                                    <div>
                                        <div class="text-muted small fw-medium">Stok Menipis (<5)</div>
                                        <h3 class="fw-bold text-danger mt-1 mb-0" id="kpi-stok-menipis">0</h3>
                                    </div>
                                    <div class="kpi-icon bg-danger-subtle text-danger">
                                        <i class="fa-solid fa-triangle-exclamation"></i>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="row g-3">
                        <div class="col-md-8">
                            <div class="card p-4">
                                <h6 class="fw-bold mb-3">Tren Transaksi Masuk & Keluar</h6>
                                <canvas id="chart-transaksi" height="110"></canvas>
                            </div>
                        </div>
                        <div class="col-md-4">
                            <div class="card p-4">
                                <h6 class="fw-bold mb-3">Status Aset Stok</h6>
                                <div id="stock-summary-list" class="d-flex flex-column gap-3"></div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- TAB 2: MASTER PRODUK -->
                <div id="tab-master" class="tab-pane-content d-none">
                    <div class="card p-3">
                        <div class="d-flex justify-content-between align-items-center mb-3">
                            <h6 class="fw-bold mb-0">Master Data Produk Gudang</h6>
                            <button class="btn btn-primary btn-sm fw-semibold" onclick="showModalProduk()">
                                <i class="fa-solid fa-plus me-1"></i> Tambah Produk Baru
                            </button>
                        </div>
                        <div class="table-responsive">
                            <table class="table table-hover align-middle">
                                <thead class="table-light">
                                    <tr>
                                        <th>SKU</th>
                                        <th>Nama Barang</th>
                                        <th>Kategori</th>
                                        <th>Harga Beli</th>
                                        <th>Harga Jual</th>
                                        <th>Stok</th>
                                        <th class="text-center">Aksi</th>
                                    </tr>
                                </thead>
                                <tbody id="tbody-produk"></tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <!-- TAB 3: PEMBELIAN -->
                <div id="tab-pembelian" class="tab-pane-content d-none">
                    <div class="card p-4">
                        <h6 class="fw-bold mb-3">Form Input Pembelian Barang (Stok Masuk)</h6>
                        <form id="form-pembelian">
                            <div class="row g-3">
                                <div class="col-md-4">
                                    <label class="form-label small fw-semibold">Pilih Produk Master</label>
                                    <select id="pembelian-produk" class="form-select" required></select>
                                </div>
                                <div class="col-md-3">
                                    <label class="form-label small fw-semibold">Jumlah Masuk (Qty)</label>
                                    <input type="number" id="pembelian-qty" class="form-control" min="1" value="1" required>
                                </div>
                                <div class="col-md-3">
                                    <label class="form-label small fw-semibold">Harga Beli Per Unit (Rp)</label>
                                    <input type="number" id="pembelian-harga" class="form-control" required>
                                </div>
                                <div class="col-md-2 d-flex align-items-end">
                                    <button type="submit" class="btn btn-success w-100 fw-semibold">
                                        <i class="fa-solid fa-cart-plus me-1"></i> Simpan
                                    </button>
                                </div>
                            </div>
                        </form>
                    </div>
                </div>

                <!-- TAB 4: PENJUALAN (POS) -->
                <div id="tab-penjualan" class="tab-pane-content d-none">
                    <div class="row g-3">
                        <div class="col-md-7">
                            <div class="card p-3">
                                <h6 class="fw-bold mb-3">Katalog Produk</h6>
                                <div class="row g-2" id="pos-product-grid"></div>
                            </div>
                        </div>
                        <div class="col-md-5">
                            <div class="card p-3">
                                <h6 class="fw-bold mb-3">Keranjang Kasir</h6>
                                <div class="table-responsive" style="max-height: 280px;">
                                    <table class="table table-sm align-middle">
                                        <thead>
                                            <tr>
                                                <th>Item</th>
                                                <th>Qty</th>
                                                <th>Subtotal</th>
                                                <th></th>
                                            </tr>
                                        </thead>
                                        <tbody id="pos-cart-tbody"></tbody>
                                    </table>
                                </div>
                                <hr>
                                <div class="d-flex justify-content-between fw-bold h5 my-2">
                                    <span>Total Bayar:</span>
                                    <span id="pos-total-amount" class="text-primary">Rp 0</span>
                                </div>
                                <button class="btn btn-success w-100 py-2 fw-bold" onclick="prosesPenjualan()">
                                    <i class="fa-solid fa-circle-check me-1"></i> Selesaikan Transaksi
                                </button>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- TAB 5: HISTORY -->
                <div id="tab-history" class="tab-pane-content d-none">
                    <div class="card p-3">
                        <h6 class="fw-bold mb-3">Riwayat Log Transaksi</h6>
                        <div class="table-responsive">
                            <table class="table table-striped align-middle">
                                <thead>
                                    <tr>
                                        <th>Waktu Transaksi</th>
                                        <th>Tipe</th>
                                        <th>ID Transaksi</th>
                                        <th>Rincian Barang</th>
                                        <th>Total Value</th>
                                    </tr>
                                </thead>
                                <tbody id="tbody-history"></tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <!-- TAB 6: LAPORAN -->
                <div id="tab-laporan" class="tab-pane-content d-none">
                    <div class="card p-4">
                        <div class="d-flex justify-content-between align-items-center mb-3">
                            <h6 class="fw-bold mb-0">Laporan Rekapitulasi Inventaris</h6>
                            <button class="btn btn-dark btn-sm fw-semibold" onclick="printLaporan()">
                                <i class="fa-solid fa-print me-1"></i> Print / Cetak PDF
                            </button>
                        </div>
                        <div id="report-print-area">
                            <div class="text-center mb-4 border-bottom pb-3">
                                <h3 class="fw-bold mb-0">INVENTORYQU ENTERPRISE</h3>
                                <small class="text-muted">Laporan Nilai Stok & Aset Gudang - Tanggal: <span id="report-date"></span></small>
                            </div>
                            <table class="table table-bordered align-middle">
                                <thead>
                                    <tr>
                                        <th>SKU</th>
                                        <th>Nama Produk</th>
                                        <th>Stok Gudang</th>
                                        <th>Harga Jual</th>
                                        <th>Perkiraan Nilai Aset</th>
                                    </tr>
                                </thead>
                                <tbody id="report-tbody"></tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <!-- TAB 7: PENGATURAN & RESET -->
                <div id="tab-pengaturan" class="tab-pane-content d-none">
                    <div class="card p-4 border-danger border-opacity-25 mb-4">
                        <h6 class="fw-bold text-danger mb-2"><i class="fa-solid fa-triangle-exclamation me-2"></i>Zona Bahaya (Danger Zone)</h6>
                        <p class="text-muted small">Tindakan di bawah ini akan menghapus data di memori browser Anda. Harap berhati-hati.</p>
                        <div class="d-flex gap-2">
                            <button class="btn btn-danger fw-semibold" onclick="triggerResetModal()">
                                <i class="fa-solid fa-trash-can me-2"></i> Reset All Data (Kosongkan Total)
                            </button>
                            <button class="btn btn-outline-secondary fw-semibold" onclick="resetToSample()">
                                <i class="fa-solid fa-rotate-left me-2"></i> Reset ke Data Demo
                            </button>
                        </div>
                    </div>
                </div>
            </main>
        </div>
    </div>

    <!-- MODAL RESET ALL DATA -->
    <div class="modal fade" id="modalReset" tabindex="-1">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header bg-danger text-white">
                    <h5 class="modal-header-title mb-0 fw-bold"><i class="fa-solid fa-triangle-exclamation me-2"></i>Konfirmasi Reset All</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body">
                    <p class="text-dark fw-medium mb-2">Apakah Anda yakin ingin menghapus <b>SELURUH DATA SYSTEM</b>?</p>
                    <p class="text-muted small">Semua data master produk, transaksi pembelian, penjualan, dan riwayat akan di-nol-kan secara permanen.</p>
                    <div class="mb-3">
                        <label class="form-label small fw-semibold">Ketik kata <span class="text-danger">RESET</span> di bawah untuk melanjutkan:</label>
                        <input type="text" id="reset-confirm-input" class="form-control" placeholder="RESET">
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-light" data-bs-dismiss="modal">Batal</button>
                    <button type="button" class="btn btn-danger fw-semibold" onclick="executeResetAll()">Eksekusi Reset All</button>
                </div>
            </div>
        </div>
    </div>

    <!-- PRINT SECTION CONTAINER -->
    <div id="print-section"></div>

    <!-- Bootstrap 5 JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

    <!-- JS Logic Application -->
    <script>
        const DB_KEY = 'INVENTORYQU_ENTERPRISE_DB';
        
        let db = {
            users: [
                { id: 1, name: 'Administrator', username: 'admin', password: 'admin', role: 'admin' },
                { id: 2, name: 'Staff Gudang', username: 'staff', password: 'staff', role: 'staff' }
            ],
            products: [
                { id: 1, sku: 'PRD-001', name: 'Laptop Pro 14 Inch', category: 'Elektronik', buyPrice: 12000000, sellPrice: 15000000, stock: 12 },
                { id: 2, sku: 'PRD-002', name: 'Mouse Wireless Ergonomis', category: 'Aksesoris', buyPrice: 150000, sellPrice: 250000, stock: 3 },
                { id: 3, sku: 'PRD-003', name: 'Keyboard Mechanical RGB', category: 'Aksesoris', buyPrice: 450000, sellPrice: 750000, stock: 8 }
            ],
            transactions: [],
            currentUser: null
        };

        let posCart = [];
        let chartInstance = null;
        let resetModalObj = null;

        document.addEventListener('DOMContentLoaded', () => {
            loadDatabase();
            initLoginForm();
            initChart();
            resetModalObj = new bootstrap.Modal(document.getElementById('modalReset'));
        });

        function loadDatabase() {
            const saved = localStorage.getItem(DB_KEY);
            if (saved) {
                try {
                    db = JSON.parse(saved);
                } catch (e) {
                    console.error("Gagal parse data localStorage", e);
                }
            } else {
                saveDatabase();
            }
        }

        function saveDatabase() {
            localStorage.setItem(DB_KEY, JSON.stringify(db));
        }

        function initLoginForm() {
            document.getElementById('login-form').addEventListener('submit', (e) => {
                e.preventDefault();
                const u = document.getElementById('login-username').value.trim();
                const p = document.getElementById('login-password').value.trim();
                const alertEl = document.getElementById('login-alert');

                const user = db.users.find(x => x.username === u && x.password === p);

                if (user) {
                    db.currentUser = user;
                    alertEl.classList.add('d-none');
                    document.getElementById('login-view').classList.add('d-none');
                    document.getElementById('app-view').classList.remove('d-none');
                    
                    document.getElementById('logged-user-name').innerText = user.name;
                    document.getElementById('user-role-badge').innerText = user.role.toUpperCase();
                    document.getElementById('user-avatar').innerText = user.name.charAt(0);

                    renderAll();
                } else {
                    alertEl.innerText = 'Username atau Password salah!';
                    alertEl.classList.remove('d-none');
                }
            });
        }

        function logout() {
            db.currentUser = null;
            document.getElementById('app-view').classList.add('d-none');
            document.getElementById('login-view').classList.remove('d-none');
        }

        function switchTab(tabName) {
            document.querySelectorAll('#sidebar .nav-link').forEach(el => el.classList.remove('active'));
            document.querySelectorAll('.tab-pane-content').forEach(el => el.classList.add('d-none'));

            event.currentTarget.classList.add('active');
            document.getElementById(`tab-${tabName}`).classList.remove('d-none');
            document.getElementById('page-title').innerText = tabName.toUpperCase();

            renderAll();
        }

        function formatRp(num) {
            return 'Rp ' + Number(num || 0).toLocaleString('id-ID');
        }

        function renderAll() {
            renderKPI();
            renderMasterTable();
            renderPOS();
            renderHistory();
            renderLaporan();
            updateChart();
        }

        function renderKPI() {
            document.getElementById('kpi-total-produk').innerText = db.products.length;
            const totalOmset = db.transactions.filter(t => t.type === 'SELL').reduce((acc, c) => acc + c.total, 0);
            const totalBuy = db.transactions.filter(t => t.type === 'BUY').reduce((acc, c) => acc + c.total, 0);
            const lowStock = db.products.filter(p => p.stock < 5).length;

            document.getElementById('kpi-total-penjualan').innerText = formatRp(totalOmset);
            document.getElementById('kpi-total-pembelian').innerText = formatRp(totalBuy);
            document.getElementById('kpi-stok-menipis').innerText = lowStock;

            // Summary Side
            const summaryBox = document.getElementById('stock-summary-list');
            summaryBox.innerHTML = '';
            db.products.slice(0, 4).forEach(p => {
                summaryBox.innerHTML += `
                    <div class="d-flex justify-content-between align-items-center">
                        <div>
                            <div class="fw-semibold small">${p.name}</div>
                            <small class="text-muted">${p.sku}</small>
                        </div>
                        <span class="badge ${p.stock < 5 ? 'bg-danger' : 'bg-success'}">${p.stock} Unit</span>
                    </div>
                `;
            });
        }

        function renderMasterTable() {
            const tbody = document.getElementById('tbody-produk');
            const selectPem = document.getElementById('pembelian-produk');
            tbody.innerHTML = '';
            selectPem.innerHTML = '';

            db.products.forEach(p => {
                tbody.innerHTML += `
                    <tr>
                        <td><code>${p.sku}</code></td>
                        <td class="fw-semibold">${p.name}</td>
                        <td><span class="badge bg-light text-dark border">${p.category}</span></td>
                        <td>${formatRp(p.buyPrice)}</td>
                        <td>${formatRp(p.sellPrice)}</td>
                        <td><span class="badge ${p.stock < 5 ? 'bg-danger' : 'bg-success'}">${p.stock}</span></td>
                        <td class="text-center">
                            <button class="btn btn-sm btn-outline-danger" onclick="hapusProduk(${p.id})"><i class="fa-solid fa-trash"></i></button>
                        </td>
                    </tr>
                `;

                selectPem.innerHTML += `<option value="${p.id}">${p.name} (Stok: ${p.stock})</option>`;
            });
        }

        function renderPOS() {
            const grid = document.getElementById('pos-product-grid');
            grid.innerHTML = '';
            db.products.forEach(p => {
                grid.innerHTML += `
                    <div class="col-md-4">
                        <div class="card p-3 text-center h-100 shadow-sm" onclick="addToCart(${p.id})" style="cursor:pointer">
                            <div class="fw-bold small mb-1">${p.name}</div>
                            <small class="text-primary fw-bold d-block">${formatRp(p.sellPrice)}</small>
                            <small class="text-muted">Stok: ${p.stock}</small>
                        </div>
                    </div>
                `;
            });
            renderCart();
        }

        function addToCart(pId) {
            const prod = db.products.find(x => x.id === pId);
            if (!prod || prod.stock <= 0) return alert('Stok produk habis!');

            const inCart = posCart.find(x => x.id === pId);
            if (inCart) {
                if (inCart.qty + 1 > prod.stock) return alert('Stok terbatas!');
                inCart.qty++;
            } else {
                posCart.push({ id: prod.id, name: prod.name, price: prod.sellPrice, qty: 1 });
            }
            renderCart();
        }

        function renderCart() {
            const tbody = document.getElementById('pos-cart-tbody');
            tbody.innerHTML = '';
            let total = 0;
            posCart.forEach((item, index) => {
                const sub = item.price * item.qty;
                total += sub;
                tbody.innerHTML += `
                    <tr>
                        <td class="small fw-semibold">${item.name}</td>
                        <td>${item.qty}</td>
                        <td class="small">${formatRp(sub)}</td>
                        <td><button class="btn btn-sm text-danger p-0" onclick="posCart.splice(${index},1);renderCart()">&times;</button></td>
                    </tr>
                `;
            });
            document.getElementById('pos-total-amount').innerText = formatRp(total);
        }

        function prosesPenjualan() {
            if (posCart.length === 0) return alert('Keranjang masih kosong!');
            const total = posCart.reduce((a, c) => a + (c.price * c.qty), 0);

            posCart.forEach(item => {
                const prod = db.products.find(x => x.id === item.id);
                if (prod) prod.stock -= item.qty;
            });

            db.transactions.push({
                id: Date.now(),
                type: 'SELL',
                date: new Date().toLocaleString('id-ID'),
                items: [...posCart],
                total: total
            });

            saveDatabase();
            alert('Transaksi Penjualan Berhasil!');
            posCart = [];
            renderAll();
        }

        function renderHistory() {
            const tbody = document.getElementById('tbody-history');
            tbody.innerHTML = '';
            db.transactions.slice().reverse().forEach(t => {
                tbody.innerHTML += `
                    <tr>
                        <td>${t.date}</td>
                        <td><span class="badge ${t.type === 'SELL' ? 'bg-success' : 'bg-warning'}">${t.type}</span></td>
                        <td>#${t.id}</td>
                        <td>${t.items ? t.items.map(i => i.name + ' (' + i.qty + ')').join(', ') : '-'}</td>
                        <td class="fw-bold">${formatRp(t.total)}</td>
                    </tr>
                `;
            });
        }

        function renderLaporan() {
            document.getElementById('report-date').innerText = new Date().toLocaleDateString('id-ID');
            const tbody = document.getElementById('report-tbody');
            tbody.innerHTML = '';
            db.products.forEach(p => {
                tbody.innerHTML += `
                    <tr>
                        <td>${p.sku}</td>
                        <td>${p.name}</td>
                        <td>${p.stock}</td>
                        <td>${formatRp(p.sellPrice)}</td>
                        <td>${formatRp(p.stock * p.sellPrice)}</td>
                    </tr>
                `;
            });
        }

        function printLaporan() {
            const printContent = document.getElementById('report-print-area').innerHTML;
            const printSec = document.getElementById('print-section');
            printSec.innerHTML = printContent;
            window.print();
        }

        function initChart() {
            const ctx = document.getElementById('chart-transaksi').getContext('2d');
            chartInstance = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['Jan', 'Feb', 'Mar', 'Apr', 'Mei', 'Jun'],
                    datasets: [{
                        label: 'Penjualan (Rp)',
                        data: [12000000, 19000000, 28000000, 22000000, 31000000, 45000000],
                        backgroundColor: '#4f46e5'
                    }]
                },
                options: { responsive: true }
            });
        }

        function updateChart() {
            if (chartInstance) chartInstance.update();
        }

        // RESET ALL DATA FUNCTIONS
        function triggerResetModal() {
            document.getElementById('reset-confirm-input').value = '';
            resetModalObj.show();
        }

        function executeResetAll() {
            const inputVal = document.getElementById('reset-confirm-input').value.trim();
            if (inputVal !== 'RESET') {
                return alert('Konfirmasi gagal! Silakan ketik kata RESET dengan benar.');
            }

            db.products = [];
            db.transactions = [];
            saveDatabase();
            resetModalObj.hide();
            alert('Seluruh data system berhasil di-reset menjadi kosong (0)!');
            renderAll();
        }

        function resetToSample() {
            if (confirm('Kembalikan ke data demo awal?')) {
                localStorage.removeItem(DB_KEY);
                location.reload();
            }
        }
    </script>
</body>
</html>

