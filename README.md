# my-workspace
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WORKSPACE - Khoa Hóa Lý</title>
    <!-- Chart.js để vẽ biểu đồ -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- FontAwesome Icon -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --primary: #1e40af;
            --primary-hover: #1d4ed8;
            --sidebar-bg: #0f172a;
            --bg-light: #f1f5f9;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--bg-light);
            height: 100vh;
            overflow: hidden;
        }

        /* --- 1. GIAO DIỆN ĐĂNG NHẬP --- */
        #login-screen {
            position: fixed;
            top: 0; left: 0; width: 100vw; height: 100vh;
            background: linear-gradient(135deg, #1e3a8a, #3b82f6);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 9999;
        }

        .login-card {
            background: #fff;
            padding: 40px 30px;
            border-radius: 12px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
            width: 380px;
            text-align: center;
        }

        .login-card .icon {
            font-size: 48px;
            color: #2563eb;
            margin-bottom: 15px;
        }

        .login-card h2 {
            color: #1e293b;
            margin-bottom: 5px;
            text-transform: uppercase;
        }

        .login-card p {
            color: #64748b;
            font-size: 13px;
            margin-bottom: 25px;
        }

        .form-group {
            text-align: left;
            margin-bottom: 18px;
        }

        .form-group label {
            display: block;
            font-size: 13px;
            font-weight: 600;
            color: #334155;
            margin-bottom: 5px;
        }

        .form-group input {
            width: 100%;
            padding: 10px 12px;
            border: 1px solid #cbd5e1;
            border-radius: 6px;
            outline: none;
            font-size: 14px;
        }

        .form-group input:focus {
            border-color: #2563eb;
        }

        .btn-login {
            width: 100%;
            padding: 12px;
            background-color: #2563eb;
            color: #fff;
            border: none;
            border-radius: 6px;
            font-weight: bold;
            font-size: 15px;
            cursor: pointer;
            transition: 0.2s;
        }

        .btn-login:hover {
            background-color: #1d4ed8;
        }

        /* --- 2. GIAO DIỆN CHÍNH (APP MAIN) --- */
        #app-screen {
            display: none;
            height: 100vh;
        }

        /* Sidebar */
        .sidebar {
            width: 240px;
            background-color: var(--sidebar-bg);
            color: #fff;
            display: flex;
            flex-direction: column;
            flex-shrink: 0;
        }

        .sidebar-brand {
            padding: 20px;
            font-size: 20px;
            font-weight: bold;
            display: flex;
            align-items: center;
            gap: 10px;
            border-bottom: 1px solid #334155;
        }

        .user-profile {
            padding: 15px 20px;
            border-bottom: 1px solid #334155;
        }

        .user-profile .name {
            font-weight: 600;
            font-size: 15px;
        }

        .user-profile .badge {
            display: inline-block;
            background-color: #ef4444;
            color: #fff;
            font-size: 10px;
            padding: 2px 8px;
            border-radius: 10px;
            margin-top: 4px;
        }

        .nav-list {
            list-style: none;
            padding: 15px 0;
        }

        .nav-item {
            padding: 12px 20px;
            display: flex;
            align-items: center;
            gap: 12px;
            cursor: pointer;
            color: #94a3b8;
            transition: 0.2s;
            font-size: 14px;
        }

        .nav-item:hover, .nav-item.active {
            background-color: #2563eb;
            color: #fff;
        }

        /* Main Content */
        .main-content {
            flex: 1;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }

        .top-bar {
            background-color: #fff;
            padding: 15px 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid #e2e8f0;
        }

        .top-bar h2 {
            font-size: 18px;
            color: #1e293b;
        }

        .top-actions {
            display: flex;
            gap: 10px;
            align-items: center;
        }

        .admin-select-box {
            background: #f8fafc;
            border: 1px solid #cbd5e1;
            padding: 6px 12px;
            border-radius: 6px;
            font-size: 13px;
            display: none;
            align-items: center;
            gap: 8px;
        }

        .admin-select-box select {
            padding: 4px 8px;
            border-radius: 4px;
            border: 1px solid #cbd5e1;
            outline: none;
            font-weight: bold;
            color: #1e40af;
        }

        .btn-action {
            padding: 8px 14px;
            border-radius: 6px;
            border: 1px solid #cbd5e1;
            background: #fff;
            cursor: pointer;
            font-size: 13px;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .btn-action.btn-danger {
            background-color: #ef4444;
            color: white;
            border: none;
        }

        .tab-content {
            flex: 1;
            padding: 20px;
            overflow-y: auto;
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        /* --- STYLES CHO CÁC TAB --- */
        .dashboard-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
            gap: 20px;
            padding: 10px;
        }

        .card {
            background: #ffffff;
            border-radius: 12px;
            padding: 24px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
            border: 1px solid #f1f5f9;
            margin-bottom: 20px;
        }

        .card h3 {
            font-size: 18px;
            font-weight: 700;
            color: #334155;
            margin-bottom: 20px;
        }

        .chart-container {
            position: relative;
            height: 300px;
            width: 100%;
        }

        /* Tab Danh sách */
        .table-container {
            background: #fff;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 1px 3px rgba(0,0,0,0.1);
        }

        table {
            width: 100%;
            border-collapse: collapse;
            text-align: left;
            font-size: 14px;
        }

        th, td {
            padding: 12px 16px;
            border-bottom: 1px solid #e2e8f0;
        }

        th {
            background-color: #f8fafc;
            color: #475569;
        }

        .status-tag {
            padding: 4px 8px;
            border-radius: 4px;
            font-size: 12px;
            font-weight: 500;
        }

        .status-doing { background: #dbeafe; color: #1d4ed8; }
        .status-todo { background: #f3e8ff; color: #6b21a8; }
        .status-done { background: #dcfce7; color: #15803d; }

        /* Tab Kanban */
        .kanban-board {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
            height: 100%;
        }

        .kanban-col {
            background: #e2e8f0;
            border-radius: 8px;
            padding: 15px;
            min-height: 400px;
        }

        .kanban-col-header {
            font-weight: bold;
            margin-bottom: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .kanban-card {
            background: #fff;
            padding: 15px;
            border-radius: 6px;
            margin-bottom: 10px;
            box-shadow: 0 1px 2px rgba(0,0,0,0.1);
            cursor: grab;
        }

        .kanban-card:active {
            cursor: grabbing;
        }

        .kanban-card .id { color: #2563eb; font-size: 12px; font-weight: bold; }
        .kanban-card .title { font-size: 14px; font-weight: 600; margin: 5px 0 10px; }
        .kanban-card .meta { font-size: 12px; color: #64748b; display: flex; justify-content: space-between; }

        /* Tab KPI */
        .kpi-table input {
            width: 60px;
            padding: 4px;
            border: 1px solid #cbd5e1;
            border-radius: 4px;
            text-align: center;
        }

        /* Dynamic Action Buttons for Admin Table */
        .btn-sm {
            padding: 4px 8px;
            font-size: 12px;
            border-radius: 4px;
            border: none;
            cursor: pointer;
        }
        .btn-edit { background-color: #f59e0b; color: white; }
        .btn-delete { background-color: #ef4444; color: white; }
    </style>
</head>
<body>

    <!-- 1. MÀN HÌNH ĐĂNG NHẬP -->
    <div id="login-screen">
        <div class="login-card">
            <div class="icon"><i class="fa-solid fa-flask"></i></div>
            <h2>KHOA HÓA LÝ</h2>
            <p id="form-sub-title">Đăng nhập hệ thống quản trị công việc</p>
            
            <div style="display: flex; gap: 10px; margin-bottom: 20px; border-bottom: 2px solid #e2e8f0; padding-bottom: 10px;">
                <button type="button" id="tab-login-btn" onclick="toggleAuthTab('login')" style="flex: 1; padding: 8px; border: none; background: none; font-weight: bold; color: #2563eb; border-bottom: 2px solid #2563eb; cursor: pointer;">ĐĂNG NHẬP</button>
                <button type="button" id="tab-register-btn" onclick="toggleAuthTab('register')" style="flex: 1; padding: 8px; border: none; background: none; font-weight: bold; color: #64748b; cursor: pointer;">ĐĂNG KÝ</button>
            </div>

            <form id="login-form" onsubmit="handleLogin(event)">
                <div class="form-group">
                    <label>Tên đăng nhập</label>
                    <input type="text" id="login-username" placeholder="Nhập tên đăng nhập..." required>
                </div>
                <div class="form-group">
                    <label>Mật khẩu</label>
                    <input type="password" id="login-password" placeholder="Nhập mật khẩu..." required>
                </div>
                <button type="submit" class="btn-login">ĐĂNG NHẬP</button>
            </form>

            <form id="register-form" onsubmit="handleRegister(event)" style="display: none;">
                <div class="form-group">
                    <label>Gmail</label>
                    <input type="email" id="reg-email" placeholder="example@gmail.com" required>
                </div>
                <div class="form-group">
                    <label>Tên đăng nhập</label>
                    <input type="text" id="reg-username" placeholder="Tạo tên đăng nhập..." required>
                </div>
                <div class="form-group">
                    <label>Mật khẩu</label>
                    <input type="password" id="reg-password" placeholder="Nhập mật khẩu..." required>
                </div>
                <div class="form-group">
                    <label>Xác nhận mật khẩu</label>
                    <input type="password" id="reg-confirm-password" placeholder="Nhập lại mật khẩu..." required>
                </div>
                <button type="submit" class="btn-login" style="background-color: #10b981;">ĐĂNG KÝ TÀI KHOẢN</button>
            </form>
        </div>
    </div>

    <!-- 2. MÀN HÌNH CHÍNH WEB APP -->
    <div id="app-screen">
        <!-- Sidebar -->
        <div class="sidebar">
            <div class="sidebar-brand">
                <i class="fa-solid fa-shapes"></i> WORKSPACE
            </div>
            <div class="user-profile">
                <div class="name" id="user-display-name">Cán bộ</div>
                <span class="badge" id="user-role-badge">User</span>
            </div>
            <ul class="nav-list">
                <li class="nav-item active" onclick="switchTab('tong-quan', this)">
                    <i class="fa-solid fa-chart-pie"></i> Tổng quan
                </li>
                <li class="nav-item" onclick="switchTab('danh-sach', this)">
                    <i class="fa-solid fa-list-check"></i> Danh sách
                </li>
                <li class="nav-item" onclick="switchTab('kanban', this)">
                    <i class="fa-solid fa-table-columns"></i> Kanban
                </li>
                <li class="nav-item" onclick="switchTab('gantt', this)">
                    <i class="fa-solid fa-bars-progress"></i> Sơ đồ Gantt
                </li>
                <li class="nav-item" onclick="switchTab('kpi', this)">
                    <i class="fa-solid fa-award"></i> Đánh giá KPI
                </li>
                <li class="nav-item" id="nav-admin-users" style="display: none;" onclick="switchTab('admin-users', this)">
                    <i class="fa-solid fa-users-gear"></i> Quản lý Users
                </li>
            </ul>
        </div>

        <!-- Main Content -->
        <div class="main-content">
            <!-- Top Bar -->
            <div class="top-bar">
                <h2 id="page-title">Dashboard Thống Kê</h2>
                <div class="top-actions">
                    <!-- Dropdown dành cho Admin chọn User để xem / chỉnh sửa -->
                    <div class="admin-select-box" id="admin-user-selector">
                        <span><i class="fa-solid fa-user-pen"></i> Đang xem data của:</span>
                        <select id="select-target-user" onchange="changeTargetUser(this.value)"></select>
                    </div>

                    <button class="btn-action" onclick="reloadData()"><i class="fa-solid fa-rotate"></i> Tải dữ liệu</button>
                    <button class="btn-action btn-danger" onclick="logout()"><i class="fa-solid fa-power-off"></i></button>
                </div>
            </div>

            <!-- Tab 1: Tổng quan -->
            <div id="tab-tong-quan" class="tab-content active">
                <div class="dashboard-grid">
                    <div class="card">
                        <h3>Tỷ lệ Trạng thái</h3>
                        <div class="chart-container">
                            <canvas id="statusChart"></canvas>
                        </div>
                    </div>
                    <div class="card">
                        <h3>Mức độ Ưu tiên</h3>
                        <div class="chart-container">
                            <canvas id="priorityChart"></canvas>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Tab 2: Danh sách -->
            <div id="tab-danh-sach" class="tab-content">
                <div style="margin-bottom: 15px; display: flex; justify-content: space-between; align-items: center;">
                    <h3 style="font-size: 16px; color: #334155;">Quản lý Công Việc</h3>
                    <button class="btn-login" style="width: auto; padding: 8px 16px;" onclick="addNewTask()">+ Thêm công việc mới</button>
                </div>
                <div class="table-container">
                    <table>
                        <thead>
                            <tr>
                                <th>Mã</th>
                                <th>Tên công việc</th>
                                <th>Người nhận</th>
                                <th>Trạng thái</th>
                                <th>Hạn chót</th>
                                <th>Thao tác</th>
                            </tr>
                        </thead>
                        <tbody id="task-table-body">
                            <!-- Dữ liệu JS tự render -->
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Tab 3: Kanban -->
            <div id="tab-kanban" class="tab-content">
                <div class="kanban-board">
                    <div class="kanban-col" id="col-todo" ondragover="allowDrop(event)" ondrop="drop(event, 'Chưa làm')">
                        <div class="kanban-col-header">🌙 Chưa làm <span id="count-todo">0</span></div>
                        <div class="kanban-cards" id="cards-todo"></div>
                    </div>
                    <div class="kanban-col" id="col-doing" ondragover="allowDrop(event)" ondrop="drop(event, 'Đang làm')">
                        <div class="kanban-col-header">⌛ Đang làm <span id="count-doing">0</span></div>
                        <div class="kanban-cards" id="cards-doing"></div>
                    </div>
                    <div class="kanban-col" id="col-done" ondragover="allowDrop(event)" ondrop="drop(event, 'Hoàn thành')">
                        <div class="kanban-col-header">✔️ Hoàn thành <span id="count-done">0</span></div>
                        <div class="kanban-cards" id="cards-done"></div>
                    </div>
                </div>
            </div>

            <!-- Tab 4: Gantt -->
            <div id="tab-gantt" class="tab-content">
                <div class="card">
                    <h3>Lộ trình triển khai</h3>
                    <p style="color: #64748b; font-size: 14px;">(Sơ đồ tiến độ công việc trong tháng 08/2026)</p>
                </div>
            </div>

            <!-- Tab 5: Đánh giá KPI -->
            <div id="tab-kpi" class="tab-content">
                <div class="card">
                    <h3 style="text-align: center; font-size: 18px; margin-bottom: 20px;">BẢNG TỰ ĐÁNH GIÁ KPI CÔNG VIỆC</h3>
                    <div class="table-container">
                        <table class="kpi-table">
                            <thead>
                                <tr>
                                    <th>STT</th>
                                    <th>Tiêu chí đánh giá</th>
                                    <th>Điểm tối đa</th>
                                    <th>Điểm tự chấm</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td>1</td>
                                    <td>Phẩm chất chính trị, đạo đức, văn hóa công sở</td>
                                    <td>10</td>
                                    <td><input type="number" id="kpi-1" value="10" max="10" min="0" onchange="calcKPI()"></td>
                                </tr>
                                <tr>
                                    <td>2</td>
                                    <td>Năng lực chuyên môn, nghiệp vụ</td>
                                    <td>10</td>
                                    <td><input type="number" id="kpi-2" value="8" max="10" min="0" onchange="calcKPI()"></td>
                                </tr>
                                <tr>
                                    <td>3</td>
                                    <td>Năng lực đổi mới, sáng tạo, đảm làm, đảm chịu trách nhiệm</td>
                                    <td>10</td>
                                    <td><input type="number" id="kpi-3" value="8" max="10" min="0" onchange="calcKPI()"></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                    <div style="margin-top: 20px; font-weight: bold; text-align: right; font-size: 16px;">
                        TỔNG ĐIỂM: <span id="kpi-total" style="color: #2563eb;">26.0</span> / 30
                    </div>
                    <div style="text-align: center; margin-top: 20px;">
                        <button class="btn-login" style="width: auto; padding: 10px 30px;" onclick="exportKPI()">LƯU ĐIỂM & XUẤT PHIẾU</button>
                    </div>
                </div>
            </div>

            <!-- Tab 6: Quản lý Users (Chỉ Admin thấy) -->
            <div id="tab-admin-users" class="tab-content">
                <div class="card">
                    <h3>Danh Sách Tài Khoản Trong Hệ Thống</h3>
                    <p style="color: #64748b; font-size: 13px; margin-bottom: 15px;">* Tên đăng nhập và Mật khẩu được bảo mật (Không được phép chỉnh sửa).</p>
                    <div class="table-container">
                        <table>
                            <thead>
                                <tr>
                                    <th>STT</th>
                                    <th>Tên đăng nhập</th>
                                    <th>Email</th>
                                    <th>Mật khẩu</th>
                                    <th>Thao tác</th>
                                </tr>
                            </thead>
                            <tbody id="user-management-body">
                                <!-- JS render danh sách user -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

        </div>
    </div>

    <!-- JAVASCRIPT XỬ LÝ -->
    <script>
        // Cấu hình Admin hệ thống
        const ADMIN_USERNAME = 'linhnguyenxuan';
        const ADMIN_PASSWORD = '051214';

        // Biến toàn cục
        let currentUser = '';       // Tài khoản đang đăng nhập
        let targetUser = '';        // Tài khoản đang được thao tác/xem dữ liệu (Admin có thể đổi)
        let isAdmin = false;

        // Danh sách công việc mặc định cho user mới
        const defaultTasks = [
            { id: 'T001', name: 'Lên kế hoạch', user: 'Cán bộ', status: 'Đang làm', date: '30/08/2026', priority: 'Bình thường' },
            { id: 'T002', name: 'Thiết kế UI', user: 'Cán bộ', status: 'Đang làm', date: '05/09/2026', priority: 'Cao' },
            { id: 'T003', name: 'Phân tích mẫu thực phẩm', user: 'Cán bộ', status: 'Đang làm', date: '30/08/2026', priority: 'Cao' },
            { id: 'T004', name: 'Phân tích mẫu nước', user: 'Cán bộ', status: 'Đang làm', date: '28/08/2026', priority: 'Bình thường' }
        ];

        let tasks = [];
        let statusChartInstance = null;
        let priorityChartInstance = null;

        // Tải danh sách User đã đăng ký
        function getRegisteredUsers() {
            return JSON.parse(localStorage.getItem('registeredUsers')) || [];
        }

        // Tải dữ liệu ĐỘC LẬP theo targetUser
        function loadUserData() {
            if (!targetUser) return;

            // 1. Load Tasks của targetUser
            const savedTasks = localStorage.getItem(`tasks_${targetUser}`);
            if (savedTasks) {
                tasks = JSON.parse(savedTasks);
            } else {
                tasks = defaultTasks.map(t => ({ ...t, user: targetUser }));
                saveUserData();
            }

            // 2. Load KPI của targetUser
            const savedKPI = localStorage.getItem(`kpi_${targetUser}`);
            if (savedKPI) {
                const kpiScores = JSON.parse(savedKPI);
                document.getElementById('kpi-1').value = kpiScores.k1 || 10;
                document.getElementById('kpi-2').value = kpiScores.k2 || 8;
                document.getElementById('kpi-3').value = kpiScores.k3 || 8;
            } else {
                document.getElementById('kpi-1').value = 10;
                document.getElementById('kpi-2').value = 8;
                document.getElementById('kpi-3').value = 8;
            }

            calcKPI();
        }

        // Lưu dữ liệu vào localStorage cho targetUser
        function saveUserData() {
            if (!targetUser) return;
            
            // Lưu Tasks
            localStorage.setItem(`tasks_${targetUser}`, JSON.stringify(tasks));

            // Lưu KPI
            const kpiScores = {
                k1: Number(document.getElementById('kpi-1').value),
                k2: Number(document.getElementById('kpi-2').value),
                k3: Number(document.getElementById('kpi-3').value)
            };
            localStorage.setItem(`kpi_${targetUser}`, JSON.stringify(kpiScores));
        }

        // Chuyển đổi giữa Form Đăng nhập và Form Đăng ký
        function toggleAuthTab(tab) {
            const loginForm = document.getElementById('login-form');
            const registerForm = document.getElementById('register-form');
            const loginBtn = document.getElementById('tab-login-btn');
            const regBtn = document.getElementById('tab-register-btn');
            const subTitle = document.getElementById('form-sub-title');

            if (tab === 'login') {
                loginForm.style.display = 'block';
                registerForm.style.display = 'none';
                loginBtn.style.color = '#2563eb';
                loginBtn.style.borderBottom = '2px solid #2563eb';
                regBtn.style.color = '#64748b';
                regBtn.style.borderBottom = 'none';
                subTitle.innerText = 'Đăng nhập hệ thống quản trị công việc';
            } else {
                loginForm.style.display = 'none';
                registerForm.style.display = 'block';
                regBtn.style.color = '#10b981';
                regBtn.style.borderBottom = '2px solid #10b981';
                loginBtn.style.color = '#64748b';
                loginBtn.style.borderBottom = 'none';
                subTitle.innerText = 'Tạo tài khoản mới cho cán bộ';
            }
        }

        // Xử lý ĐĂNG KÝ
        function handleRegister(e) {
            e.preventDefault();

            const email = document.getElementById('reg-email').value.trim();
            const username = document.getElementById('reg-username').value.trim();
            const password = document.getElementById('reg-password').value;
            const confirmPassword = document.getElementById('reg-confirm-password').value;

            if (username === ADMIN_USERNAME) {
                alert('Tên đăng nhập này thuộc quyền Admin hệ thống. Vui lòng chọn tên khác!');
                return;
            }

            if (password !== confirmPassword) {
                alert('Lỗi: Mật khẩu và Xác nhận mật khẩu không trùng khớp!');
                return;
            }

            let users = getRegisteredUsers();

            if (users.some(u => u.username === username)) {
                alert('Tên đăng nhập này đã tồn tại. Vui lòng chọn tên khác!');
                return;
            }

            users.push({ email, username, password });
            localStorage.setItem('registeredUsers', JSON.stringify(users));

            alert('Đăng ký tài khoản thành công! Bạn có thể Đăng nhập ngay bây giờ.');

            document.getElementById('register-form').reset();
            toggleAuthTab('login');
            document.getElementById('login-username').value = username;
        }

        // Xử lý ĐĂNG NHẬP
        function handleLogin(e) {
            e.preventDefault();

            const usernameInput = document.getElementById('login-username').value.trim();
            const passwordInput = document.getElementById('login-password').value;

            let users = getRegisteredUsers();
            const validUser = users.find(u => u.username === usernameInput && u.password === passwordInput);

            // Kiểm tra Admin chủ hoặc User thường
            if (usernameInput === ADMIN_USERNAME && passwordInput === ADMIN_PASSWORD) {
                currentUser = ADMIN_USERNAME;
                targetUser = ADMIN_USERNAME;
                isAdmin = true;
            } else if (validUser) {
                currentUser = usernameInput;
                targetUser = usernameInput;
                isAdmin = false;
            } else {
                alert('Sai Tên đăng nhập hoặc Mật khẩu. Vui lòng kiểm tra lại!');
                return;
            }

            // Cập nhật giao diện theo quyền
            document.getElementById('login-screen').style.display = 'none';
            document.getElementById('app-screen').style.display = 'flex';

            document.getElementById('user-display-name').innerText = currentUser;
            const badge = document.getElementById('user-role-badge');
            
            if (isAdmin) {
                badge.innerText = 'ADMIN';
                badge.style.backgroundColor = '#10b981';
                document.getElementById('nav-admin-users').style.display = 'flex';
                document.getElementById('admin-user-selector').style.display = 'flex';
                populateAdminUserSelector();
            } else {
                badge.innerText = 'User';
                badge.style.backgroundColor = '#ef4444';
                document.getElementById('nav-admin-users').style.display = 'none';
                document.getElementById('admin-user-selector').style.display = 'none';
            }

            loadUserData();
            initApp();
        }

        // Đổ danh sách người dùng vào dropdown của Admin
        function populateAdminUserSelector() {
            const select = document.getElementById('select-target-user');
            select.innerHTML = `<option value="${ADMIN_USERNAME}">Chính mình (Admin)</option>`;
            
            const users = getRegisteredUsers();
            users.forEach(u => {
                select.innerHTML += `<option value="${u.username}">${u.username}</option>`;
            });
            select.value = targetUser;
        }

        // Admin chuyển đổi tài khoản muốn xem/sửa
        function changeTargetUser(newTarget) {
            saveUserData(); // Lưu lại dữ liệu user cũ trước khi chuyển
            targetUser = newTarget;
            loadUserData();
            initApp();
        }

        // ĐĂNG XUẤT
        function logout() {
            saveUserData();
            currentUser = '';
            targetUser = '';
            isAdmin = false;
            document.getElementById('app-screen').style.display = 'none';
            document.getElementById('login-screen').style.display = 'flex';
            document.getElementById('login-password').value = '';
        }

        // Khởi tạo ứng dụng
        function initApp() {
            renderTable();
            renderKanban();
            initCharts();
            if (isAdmin) renderUserManagementTable();
        }

        // Chuyển Tab
        function switchTab(tabId, element) {
            document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(el => el.classList.remove('active'));

            element.classList.add('active');
            document.getElementById(`tab-${tabId}`).classList.add('active');

            const titles = {
                'tong-quan': 'Dashboard Thống Kê',
                'danh-sach': 'Danh Sách Công Việc',
                'kanban': 'Bảng Kéo Thả (Kanban)',
                'gantt': 'Sơ đồ Tiến Độ (Gantt)',
                'kpi': 'Xuất Phiếu Đánh Giá',
                'admin-users': 'Quản Lý Tài Khoản Hệ Thống'
            };
            document.getElementById('page-title').innerText = titles[tabId];
        }

        // Render Table Danh Sách Công Việc
        function renderTable() {
            const tbody = document.getElementById('task-table-body');
            tbody.innerHTML = '';
            tasks.forEach((task, index) => {
                let statusClass = 'status-doing';
                if(task.status === 'Chưa làm') statusClass = 'status-todo';
                if(task.status === 'Hoàn thành') statusClass = 'status-done';

                tbody.innerHTML += `
                    <tr>
                        <td style="color: #2563eb; font-weight: bold;">${task.id}</td>
                        <td><b>${task.name}</b></td>
                        <td>${task.user}</td>
                        <td><span class="status-tag ${statusClass}">${task.status}</span></td>
                        <td>${task.date}</td>
                        <td>
                            <button class="btn-sm btn-edit" onclick="editTask(${index})"><i class="fa-solid fa-pen"></i> Sửa</button>
                            <button class="btn-sm btn-delete" onclick="deleteTask(${index})"><i class="fa-solid fa-trash"></i> Xóa</button>
                        </td>
                    </tr>
                `;
            });
        }

        // Thêm công việc mới
        function addNewTask() {
            const taskName = prompt("Nhập tên công việc mới:");
            if (!taskName) return;

            const newTask = {
                id: 'T' + String(tasks.length + 1).padStart(3, '0'),
                name: taskName,
                user: targetUser,
                status: 'Chưa làm',
                date: '31/08/2026',
                priority: 'Bình thường'
            };

            tasks.push(newTask);
            saveUserData();
            initApp();
        }

        // Chỉnh sửa công việc
        function editTask(index) {
            const task = tasks[index];
            const newName = prompt("Sửa tên công việc:", task.name);
            if (newName !== null) {
                task.name = newName;
                const newStatus = prompt("Nhập trạng thái (Chưa làm / Đang làm / Hoàn thành):", task.status);
                if (['Chưa làm', 'Đang làm', 'Hoàn thành'].includes(newStatus)) {
                    task.status = newStatus;
                }
                saveUserData();
                initApp();
            }
        }

        // Xóa công việc
        function deleteTask(index) {
            if (confirm("Bạn có chắc muốn xóa công việc này?")) {
                tasks.splice(index, 1);
                saveUserData();
                initApp();
            }
        }

        // Render Bảng Kanban
        function renderKanban() {
            const todoBox = document.getElementById('cards-todo');
            const doingBox = document.getElementById('cards-doing');
            const doneBox = document.getElementById('cards-done');

            todoBox.innerHTML = ''; doingBox.innerHTML = ''; doneBox.innerHTML = '';

            let countTodo = 0, countDoing = 0, countDone = 0;

            tasks.forEach(task => {
                const cardHTML = `
                    <div class="kanban-card" draggable="true" ondragstart="drag(event, '${task.id}')">
                        <div class="id">${task.id}</div>
                        <div class="title">${task.name}</div>
                        <div class="meta">
                            <span><i class="fa-regular fa-user"></i> ${task.user}</span>
                            <span><i class="fa-regular fa-calendar"></i> ${task.date}</span>
                        </div>
                    </div>
                `;

                if (task.status === 'Chưa làm') {
                    todoBox.innerHTML += cardHTML;
                    countTodo++;
                } else if (task.status === 'Đang làm') {
                    doingBox.innerHTML += cardHTML;
                    countDoing++;
                } else if (task.status === 'Hoàn thành') {
                    doneBox.innerHTML += cardHTML;
                    countDone++;
                }
            });

            document.getElementById('count-todo').innerText = countTodo;
            document.getElementById('count-doing').innerText = countDoing;
            document.getElementById('count-done').innerText = countDone;
        }

        // Kéo thả Kanban
        function allowDrop(ev) { ev.preventDefault(); }
        function drag(ev, id) { ev.dataTransfer.setData("text", id); }
        function drop(ev, newStatus) {
            ev.preventDefault();
            const id = ev.dataTransfer.getData("text");
            const task = tasks.find(t => t.id === id);
            if (task) {
                task.status = newStatus;
                saveUserData();
                renderKanban();
                renderTable();
                updateCharts();
            }
        }

        // Cập nhật biểu đồ
        function updateCharts() {
            if (!statusChartInstance || !priorityChartInstance) return;

            let todo = tasks.filter(t => t.status === 'Chưa làm').length;
            let doing = tasks.filter(t => t.status === 'Đang làm').length;
            let done = tasks.filter(t => t.status === 'Hoàn thành').length;

            statusChartInstance.data.labels = [`Chưa làm (${todo})`, `Đang làm (${doing})`, `Hoàn thành (${done})`];
            statusChartInstance.data.datasets[0].data = [todo, doing, done];
            statusChartInstance.update();

            let high = tasks.filter(t => t.priority === 'Cao').length;
            let normal = tasks.filter(t => t.priority === 'Bình thường').length;
            let low = tasks.filter(t => t.priority === 'Thấp').length;

            priorityChartInstance.data.datasets[0].data = [high, normal, low];
            priorityChartInstance.update();
        }

        // Khởi tạo Chart.js
        function initCharts() {
            const ctx1 = document.getElementById('statusChart').getContext('2d');
            const ctx2 = document.getElementById('priorityChart').getContext('2d');

            if (statusChartInstance) statusChartInstance.destroy();
            if (priorityChartInstance) priorityChartInstance.destroy();

            let todo = tasks.filter(t => t.status === 'Chưa làm').length;
            let doing = tasks.filter(t => t.status === 'Đang làm').length;
            let done = tasks.filter(t => t.status === 'Hoàn thành').length;

            statusChartInstance = new Chart(ctx1, {
                type: 'doughnut',
                data: {
                    labels: [`Chưa làm (${todo})`, `Đang làm (${doing})`, `Hoàn thành (${done})`],
                    datasets: [{
                        data: [todo, doing, done],
                        backgroundColor: ['#a5a6f6', '#2563eb', '#06b6d4'],
                        borderWidth: 2,
                        borderColor: '#ffffff',
                        cutout: '65%'
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { position: 'top', labels: { usePointStyle: true, boxWidth: 12, padding: 15, font: { size: 13 } } }
                    }
                }
            });

            let high = tasks.filter(t => t.priority === 'Cao').length;
            let normal = tasks.filter(t => t.priority === 'Bình thường').length;
            let low = tasks.filter(t => t.priority === 'Thấp').length;

            priorityChartInstance = new Chart(ctx2, {
                type: 'bar',
                data: {
                    labels: ['Cao', 'Bình thường', 'Thấp'],
                    datasets: [{
                        label: 'Số lượng',
                        data: [high, normal, low],
                        backgroundColor: ['#ff4d6d', '#e69100', '#10b981'],
                        borderRadius: 4,
                        barThickness: 60
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: { beginAtZero: true, ticks: { stepSize: 1, precision: 0 }, grid: { color: '#f1f5f9' } },
                        x: { grid: { display: false } }
                    }
                }
            });
        }

        // Tính điểm KPI
        function calcKPI() {
            const inputs = document.querySelectorAll('#tab-kpi input');
            let total = 0;
            inputs.forEach(input => total += Number(input.value || 0));
            document.getElementById('kpi-total').innerText = total.toFixed(1);
        }

        function exportKPI() {
            saveUserData();
            alert(`Đã lưu dữ liệu KPI cho tài khoản [${targetUser}] thành công!`);
        }

        // Quản lý Users (Chỉ Admin)
        function renderUserManagementTable() {
            const tbody = document.getElementById('user-management-body');
            tbody.innerHTML = '';

            const users = getRegisteredUsers();
            users.forEach((u, i) => {
                tbody.innerHTML += `
                    <tr>
                        <td>${i + 1}</td>
                        <td><b>${u.username}</b> (Không thể chỉnh sửa)</td>
                        <td>${u.email}</td>
                        <td>•••••••• (Bảo mật)</td>
                        <td>
                            <button class="btn-sm btn-edit" onclick="adminEditUserTasks('${u.username}')"><i class="fa-solid fa-pen-to-square"></i> Sửa Dữ Liệu</button>
                        </td>
                    </tr>
                `;
            });
        }

        function adminEditUserTasks(username) {
            document.getElementById('select-target-user').value = username;
            changeTargetUser(username);
            switchTab('danh-sach', document.querySelectorAll('.nav-item')[1]);
        }

        function reloadData() {
            loadUserData();
            initApp();
        }
    </script>
</body>
</html>
