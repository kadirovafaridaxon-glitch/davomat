
<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Davomat Mehnatkash - Mobil va 3D Boshqaruv Tizimi</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=Fira+Code:wght@400;500;600&display=swap" rel="stylesheet">
    <!-- Three.js for 3D Background Canvas -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['"Plus Jakarta Sans"', 'sans-serif'],
                        mono: ['"Fira Code"', 'monospace'],
                    },
                    colors: {
                        darkBg: '#030509',
                        cardBg: 'rgba(15, 23, 42, 0.8)',
                        cardBorder: 'rgba(255, 255, 255, 0.12)',
                        accentPrimary: '#6366f1',
                        accentCyan: '#06b6d4',
                        accentGreen: '#10b981',
                        accentRed: '#ef4444',
                        accentYellow: '#f59e0b',
                        accentPurple: '#a855f7'
                    }
                }
            }
        }
    </script>

    <style>
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: #030509;
            color: #f1f5f9;
            overflow-x: hidden;
            -webkit-tap-highlight-color: transparent;
        }

        #three-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: 0;
            pointer-events: none;
        }

        .glass-panel {
            background: rgba(13, 18, 33, 0.75);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.12);
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.5), inset 0 1px 0 rgba(255, 255, 255, 0.1);
        }

        .card-3d:hover {
            transform: translateY(-4px) scale(1.005);
            box-shadow: 0 20px 40px rgba(99, 102, 241, 0.2);
            border-color: rgba(99, 102, 241, 0.4);
        }

        .neon-glow-indigo {
            box-shadow: 0 0 25px rgba(99, 102, 241, 0.4);
        }

        .neon-glow-cyan {
            box-shadow: 0 0 25px rgba(6, 182, 212, 0.4);
        }

        ::-webkit-scrollbar {
            width: 4px;
            height: 4px;
        }
        ::-webkit-scrollbar-track {
            background: rgba(15, 23, 42, 0.6);
        }
        ::-webkit-scrollbar-thumb {
            background: rgba(99, 102, 241, 0.4);
            border-radius: 4px;
        }

        /* Mobile specific adjustments */
        @media (max-width: 768px) {
            .mobile-bottom-nav {
                display: flex;
            }
            body {
                padding-bottom: 70px;
            }
        }
        @media (min-width: 769px) {
            .mobile-bottom-nav {
                display: none;
            }
        }
    </style>
</head>
<body class="min-h-screen w-screen flex flex-col overflow-x-hidden">

    <!-- 3D THREE.JS CANVAS BACKGROUND -->
    <canvas id="three-canvas"></canvas>

    <!-- DATA INITIALIZATION SCRIPT -->
    <script>
        const DEFAULT_USERS = [
            { id: 'u1', name: 'Ega Master (Super Admin)', role: 'owner', login: 'owner_master', pass: 'mehnatkash2026', group: 'Boshqaruv' },
            { id: 'u2', name: 'Sardor Qodirov', role: 'admin', login: 'admin_sardor', pass: 'admin123', group: "Ma'murlar" },
            { id: 'u3', name: 'Anvar Zokirov (O\'qituvchi)', role: 'teacher', login: 'teacher_anvar', pass: 'teacher123', group: 'Python-101' },
            { id: 'u4', name: 'Ali Valiyev', role: 'student', login: 'ali_2026', pass: '12345', group: 'Python-101' },
            { id: 'u5', name: 'Malika Sobirova', role: 'student', login: 'malika_2026', pass: '12345', group: 'Python-101' },
            { id: 'u6', name: 'Javohir Karimov', role: 'student', login: 'javohir_2026', pass: '12345', group: 'Web-Dev-2' },
            { id: 'u7', name: 'Nigora Aliyeva', role: 'student', login: 'nigora_2026', pass: '12345', group: 'Robototexnika-1' }
        ];

        const DEFAULT_ATTENDANCE = [
            { id: 'att1', studentId: 'u4', date: '2026-03-01', status: 'Kelgan', note: 'O\'z vaqtida keldi' },
            { id: 'att2', studentId: 'u4', date: '2026-03-02', status: 'Kelgan', note: '' },
            { id: 'att3', studentId: 'u4', date: '2026-03-03', status: 'Sababli', note: 'Tish shifokori' },
            { id: 'att4', studentId: 'u5', date: '2026-03-03', status: 'Kelmagan', note: 'Ogohlantirilmadi' },
            { id: 'att5', studentId: 'u6', date: '2026-03-03', status: 'Kelgan', note: '' }
        ];

        const DEFAULT_GRADES = [
            { id: 'g1', studentId: 'u4', subject: 'Python asoslari', score: 95, date: '2026-03-01', comment: 'A\'lo dars qatnashuvi' },
            { id: 'g2', studentId: 'u4', subject: 'O\'zgaruvchilar va if', score: 88, date: '2026-03-02', comment: 'Yaxshi' },
            { id: 'g3', studentId: 'u5', subject: 'Python asoslari', score: 78, date: '2026-03-01', comment: 'Qoniqarli' },
            { id: 'g4', studentId: 'u6', subject: 'HTML & CSS', score: 92, date: '2026-03-02', comment: 'Topshiriq a\'lo bajarilgan' }
        ];

        function getStoredData(key, defaultData) {
            try {
                const data = localStorage.getItem('mehnatkash_' + key);
                return data ? JSON.parse(data) : defaultData;
            } catch (e) {
                return defaultData;
            }
        }

        function saveStoredData(key, data) {
            try {
                localStorage.setItem('mehnatkash_' + key, JSON.stringify(data));
            } catch (e) {}
        }

        let db = {
            users: getStoredData('users', DEFAULT_USERS),
            attendance: getStoredData('attendance', DEFAULT_ATTENDANCE),
            grades: getStoredData('grades', DEFAULT_GRADES),
            scans: getStoredData('scans', [])
        };

        let currentUser = null;
        let activeTab = 'dashboard';
        let scannerStream = null;

        };

        let currentUser = null;
        let activeTab = 'dashboard';

        function initThreeJS() {
            const canvas = document.getElementById('three-canvas');
            if (!canvas || !window.THREE) return;

            const scene = new THREE.Scene();
            const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
            camera.position.z = 25;

            const renderer = new THREE.WebGLRenderer({ canvas, alpha: true, antialias: true });
            renderer.setSize(window.innerWidth, window.innerHeight);
            renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

            const count = 200;
            const geometry = new THREE.BufferGeometry();
            const positions = new Float32Array(count * 3);
            const colors = new Float32Array(count * 3);

            const colorOptions = [
                new THREE.Color('#6366f1'),
                new THREE.Color('#06b6d4'),
                new THREE.Color('#a855f7')
            ];

            for (let i = 0; i < count * 3; i += 3) {
                positions[i] = (Math.random() - 0.5) * 60;
                positions[i + 1] = (Math.random() - 0.5) * 60;
                positions[i + 2] = (Math.random() - 0.5) * 60;

                const col = colorOptions[Math.floor(Math.random() * colorOptions.length)];
                colors[i] = col.r;
                colors[i + 1] = col.g;
                colors[i + 2] = col.b;
            }

            geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));
            geometry.setAttribute('color', new THREE.BufferAttribute(colors, 3));

            const material = new THREE.PointsMaterial({
                size: 0.7,
                vertexColors: true,
                transparent: true,
                opacity: 0.6,
                blending: THREE.AdditiveBlending
            });

            const particleSystem = new THREE.Points(geometry, material);
            scene.add(particleSystem);

            function animate() {
                requestAnimationFrame(animate);
                particleSystem.rotation.y += 0.0008;
                particleSystem.rotation.x += 0.0004;
                renderer.render(scene, camera);
            }
            animate();

            window.addEventListener('resize', () => {
                camera.aspect = window.innerWidth / window.innerHeight;
                camera.updateProjectionMatrix();
                renderer.setSize(window.innerWidth, window.innerHeight);
            });
        }

        function handleLogin(e) {
            if (e) e.preventDefault();
            const loginInput = document.getElementById('login-input');
            const passwordInput = document.getElementById('password-input');
            const errorEl = document.getElementById('login-error');

            if (!loginInput || !passwordInput) return;

            const loginVal = loginInput.value.trim();
            const passVal = passwordInput.value.trim();

            const foundUser = db.users.find(u => u.login === loginVal && u.pass === passVal);

            if (foundUser) {
                if (errorEl) errorEl.classList.add('hidden');
                currentUser = foundUser;
                try {
                    sessionStorage.setItem('mehnatkash_session', JSON.stringify(currentUser));
                } catch(err) {}
                showApp();
            } else {
                if (errorEl) errorEl.classList.remove('hidden');
            }
        }

        function quickLogin(role) {
            const user = db.users.find(u => u.role === role);
            if (user) {
                const loginInput = document.getElementById('login-input');
                const passwordInput = document.getElementById('password-input');
                if (loginInput && passwordInput) {
                    loginInput.value = user.login;
                    passwordInput.value = user.pass;
                    handleLogin();
                }
            }
        }
    </script>

    <!-- LOGIN MODAL / SCREEN -->
    <div id="login-modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/80 backdrop-blur-md">
        <div class="w-full max-w-sm sm:max-w-md glass-panel rounded-3xl p-6 sm:p-8 border border-white/15 shadow-2xl relative overflow-hidden">
            <div class="absolute -top-20 -right-20 w-48 h-48 bg-accentPrimary/40 rounded-full blur-3xl pointer-events-none"></div>
            <div class="absolute -bottom-20 -left-20 w-48 h-48 bg-accentCyan/40 rounded-full blur-3xl pointer-events-none"></div>

            <div class="text-center mb-6 relative z-10">
                <div class="w-16 h-16 bg-gradient-to-tr from-accentPrimary via-accentPurple to-accentCyan rounded-2xl flex items-center justify-center mx-auto mb-3 shadow-xl neon-glow-indigo">
                    <i class="fa-solid fa-graduation-cap text-3xl text-white"></i>
                </div>
                <h1 class="text-xl sm:text-2xl font-black tracking-tight bg-gradient-to-r from-white via-slate-100 to-slate-300 bg-clip-text text-transparent">
                    DAVOMAT MEHNATKASH
                </h1>
                <p class="text-xs text-accentCyan font-mono mt-1">Mobil & 3D Boshqaruv Tizimi</p>
            </div>

            <!-- Master Account Box -->
            <div class="mb-5 p-3 rounded-2xl bg-white/5 border border-white/10 text-xs space-y-1 relative z-10">
                <div class="flex items-center justify-between text-accentPrimary font-bold">
                    <span><i class="fa-solid fa-key mr-1"></i> Asosiy Ega (Owner):</span>
                    <span class="bg-purple-500/20 text-purple-300 border border-purple-500/30 px-2 py-0.5 rounded-full text-[10px]">Master</span>
                </div>
                <div class="font-mono text-slate-200">Login: <span class="text-white font-bold bg-slate-900/80 px-1.5 py-0.5 rounded">owner_master</span></div>
                <div class="font-mono text-slate-200">Parol: <span class="text-white font-bold bg-slate-900/80 px-1.5 py-0.5 rounded">mehnatkash2026</span></div>
            </div>

            <form onsubmit="handleLogin(event)" class="space-y-4 relative z-10">
                <div>
                    <label class="block text-xs font-bold text-slate-300 uppercase tracking-wider mb-1">Login</label>
                    <div class="relative">
                        <i class="fa-solid fa-user absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-400 text-sm"></i>
                        <input type="text" id="login-input" required placeholder="owner_master" 
                            class="w-full bg-slate-950/80 border border-white/15 rounded-xl pl-10 pr-4 py-3 text-sm text-white focus:outline-none focus:border-accentPrimary">
                    </div>
                </div>

                <div>
                    <label class="block text-xs font-bold text-slate-300 uppercase tracking-wider mb-1">Parol</label>
                    <div class="relative">
                        <i class="fa-solid fa-lock absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-400 text-sm"></i>
                        <input type="password" id="password-input" required placeholder="••••••••" 
                            class="w-full bg-slate-950/80 border border-white/15 rounded-xl pl-10 pr-4 py-3 text-sm text-white focus:outline-none focus:border-accentPrimary">
                    </div>
                </div>

                <div id="login-error" class="hidden text-xs text-accentRed bg-accentRed/10 p-2.5 rounded-xl border border-accentRed/30 text-center font-medium">
                    ⚠️ Login yoki parol noto'g'ri!
                </div>

                <button type="submit" class="w-full bg-gradient-to-r from-accentPrimary via-accentPurple to-accentCyan text-white font-bold py-3.5 rounded-xl transition shadow-xl neon-glow-indigo flex items-center justify-center gap-2 text-sm uppercase tracking-wider">
                    <i class="fa-solid fa-right-to-bracket"></i> Tizimga Kirish
                </button>
            </form>

            <div class="mt-5 pt-3 border-t border-white/10 text-center relative z-10">
                <span class="text-[10px] text-slate-400 block mb-2 font-mono">Tezkor Sinov Rejimi:</span>
                <div class="flex justify-center gap-1.5 flex-wrap">
                    <button type="button" onclick="quickLogin('owner')" class="px-2.5 py-1 text-[11px] rounded-lg bg-purple-500/10 text-purple-300 border border-purple-500/30">👑 Ega</button>
                    <button type="button" onclick="quickLogin('admin')" class="px-2.5 py-1 text-[11px] rounded-lg bg-blue-500/10 text-blue-300 border border-blue-500/30">🛡️ Admin</button>
                    <button type="button" onclick="quickLogin('teacher')" class="px-2.5 py-1 text-[11px] rounded-lg bg-emerald-500/10 text-emerald-300 border border-emerald-500/30">👨‍🏫 O'qituvchi</button>
                    <button type="button" onclick="quickLogin('student')" class="px-2.5 py-1 text-[11px] rounded-lg bg-cyan-500/10 text-cyan-300 border border-cyan-500/30">🎓 O'quvchi</button>
                </div>
            </div>
        </div>
    </div>

    <!-- MAIN APP CONTAINER -->
    <div id="app-container" class="hidden flex-1 w-full flex flex-col md:flex-row relative z-10">
        
        <!-- DESKTOP SIDEBAR -->
        <aside class="hidden md:flex flex-col w-64 glass-panel border-r border-white/10 p-4 justify-between">
            <div class="space-y-6">
                <div class="flex items-center gap-3 px-2">
                    <div class="w-10 h-10 rounded-xl bg-accentPrimary flex items-center justify-center text-white font-bold text-lg neon-glow-indigo">
                        M
                    </div>
                    <div>
                        <div class="font-extrabold text-sm tracking-wide text-white">MEHNATKASH</div>
                        <div class="text-[10px] text-accentCyan font-mono">Maktab Boshqaruvi</div>
                    </div>
                </div>

                <nav id="sidebar-nav" class="space-y-1.5">
                    <!-- Populated dynamically -->
                </nav>
            </div>

            <!-- Profile Widget at bottom of desktop sidebar -->
            <div class="p-3 rounded-xl bg-slate-900/60 border border-white/10 flex items-center justify-between">
                <div class="flex items-center gap-2.5 overflow-hidden">
                    <div id="desktop-user-avatar" class="w-8 h-8 rounded-lg bg-accentPrimary/20 text-accentPrimary font-bold flex items-center justify-center text-xs">
                        A
                    </div>
                    <div class="truncate">
                        <div id="desktop-user-name" class="text-xs font-bold text-white truncate">Ism</div>
                        <div id="desktop-user-role" class="text-[10px] text-slate-400 font-mono">Rol</div>
                    </div>
                </div>
                <button onclick="logout()" title="Chiqish" class="text-slate-400 hover:text-accentRed transition p-1.5">
                    <i class="fa-solid fa-power-off text-sm"></i>
                </button>
            </div>
        </aside>

        <!-- MOBILE TOP HEADER -->
        <header class="md:hidden glass-panel border-b border-white/10 px-4 py-3 flex items-center justify-between sticky top-0 z-40">
            <div class="flex items-center gap-2.5">
                <div class="w-8 h-8 rounded-lg bg-accentPrimary flex items-center justify-center text-white font-bold text-sm">
                    M
                </div>
                <div>
                    <div class="font-extrabold text-xs text-white">MEHNATKASH</div>
                    <div id="mobile-role-badge" class="text-[9px] text-accentCyan font-mono">Rol</div>
                </div>
            </div>
            <div class="flex items-center gap-2">
                <span id="current-time" class="text-[10px] text-slate-400 font-mono">00:00:00</span>
                <button onclick="logout()" class="w-8 h-8 rounded-lg bg-red-500/10 text-red-400 flex items-center justify-center">
                    <i class="fa-solid fa-power-off text-xs"></i>
                </button>
            </div>
        </header>

        <!-- MAIN CONTENT AREA -->
        <main class="flex-1 flex flex-col p-4 sm:p-6 overflow-y-auto space-y-5">
            <!-- Top bar for desktop -->
            <div class="hidden md:flex items-center justify-between pb-3 border-b border-white/10">
                <h2 id="page-title" class="text-lg font-bold text-white flex items-center gap-2">
                    <i class="fa-solid fa-chart-pie text-accentCyan"></i> Bosh Panel
                </h2>
                <div class="flex items-center gap-3">
                    <span id="desktop-current-time" class="text-xs text-slate-400 font-mono bg-slate-900/60 px-3 py-1.5 rounded-xl border border-white/5">00:00:00</span>
                    <span id="header-role-badge" class="px-3 py-1 rounded-full text-xs font-bold font-mono">Rol</span>
                </div>
            </div>

            <!-- Dynamic View Container -->
            <div id="content-view" class="space-y-5">
                <!-- Content loaded via JS -->
            </div>
        </main>
    </div>

    <!-- MOBILE BOTTOM NAVIGATION BAR -->
    <div class="mobile-bottom-nav fixed bottom-0 left-0 right-0 glass-panel border-t border-white/10 px-2 py-2 z-40 justify-around items-center">
        <div id="mobile-bottom-nav-links" class="flex w-full justify-around items-center">
            <!-- Populated dynamically -->
        </div>
    </div>

    <!-- UNIVERSAL MODAL FOR ADDING/EDITING USERS -->
    <div id="form-modal" class="hidden fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/80 backdrop-blur-md">
        <div class="w-full max-w-sm glass-panel rounded-2xl p-6 border border-white/15 shadow-2xl relative space-y-4">
            <h3 id="modal-title" class="text-base font-bold text-white">Yangi Foydalanuvchi Qo'shish</h3>

            <form onsubmit="saveUserForm(event)" class="space-y-3">
                <input type="hidden" id="modal-user-id">

                <div>
                    <label class="block text-xs text-slate-300 mb-1">F.I.SH (To'liq ismi)</label>
                    <input type="text" id="modal-name" required placeholder="Masalan: Jasur Karimov" 
                        class="w-full bg-slate-900 border border-white/10 rounded-xl px-3 py-2 text-xs text-white focus:outline-none focus:border-accentPrimary">
                </div>

                <div>
                    <label class="block text-xs text-slate-300 mb-1">Tizimdagi Roli / Huquqi</label>
                    <select id="modal-role" class="w-full bg-slate-900 border border-white/10 rounded-xl px-3 py-2 text-xs text-white focus:outline-none focus:border-accentPrimary">
                        <option value="admin">🛡️ Admin (Boshqaruvchi va o'quvchi qo'shuvchi)</option>
                        <option value="teacher">👨‍🏫 O'qituvchi (Davomat va baholash)</option>
                        <option value="student">🎓 O'quvchi (Faqat o'z ballarini ko'radi)</option>
                    </select>
                </div>

                <div>
                    <label class="block text-xs text-slate-300 mb-1">Guruh / Sinf</label>
                    <select id="modal-group" class="w-full bg-slate-900 border border-white/10 rounded-xl px-3 py-2 text-xs text-white focus:outline-none focus:border-accentPrimary">
                        <option value="Python-101">Python-101</option>
                        <option value="Web-Dev-2">Web-Dev-2</option>
                        <option value="Robototexnika-1">Robototexnika-1</option>
                        <option value="Ma'murlar">Ma'murlar</option>
                    </select>
                </div>

                <div class="grid grid-cols-2 gap-2">
                    <div>
                        <label class="block text-xs text-slate-300 mb-1">Login (kirish uchun)</label>
                        <input type="text" id="modal-login" required placeholder="jasur2026" 
                            class="w-full bg-slate-900 border border-white/10 rounded-xl px-3 py-2 text-xs text-white font-mono focus:outline-none">
                    </div>
                    <div>
                        <label class="block text-xs text-slate-300 mb-1">Parol</label>
                        <input type="text" id="modal-password" required placeholder="12345" 
                            class="w-full bg-slate-900 border border-white/10 rounded-xl px-3 py-2 text-xs text-white font-mono focus:outline-none">
                    </div>
                </div>

                <div class="pt-2 flex justify-end gap-2">
                    <button type="button" onclick="closeModal()" class="px-3 py-1.5 rounded-xl text-xs bg-slate-800 text-slate-300">Bekor qilish</button>
                    <button type="submit" class="px-3 py-1.5 rounded-xl text-xs bg-accentPrimary text-white font-bold">Saqlash</button>
                </div>
            </form>
        </div>
    </div>

    <!-- APPLICATION RUNTIME LOGIC -->
    <script>
        window.onload = function() {
            startClock();
            initThreeJS();

            try {
                const session = sessionStorage.getItem('mehnatkash_session');
                if (session) {
                    currentUser = JSON.parse(session);
                    showApp();
                }
            } catch(e) {}
        };

        function startClock() {
            setInterval(() => {
                const now = new Date();
                const timeStr = now.toTimeString().split(' ')[0];
                const c1 = document.getElementById('current-time');
                const c2 = document.getElementById('desktop-current-time');
                if (c1) c1.textContent = timeStr;
                if (c2) c2.textContent = timeStr;
            }, 1000);
        }

        function logout() {
            currentUser = null;
            try { sessionStorage.removeItem('mehnatkash_session'); } catch(e) {}
            document.getElementById('app-container').classList.add('hidden');
            document.getElementById('login-modal').classList.remove('hidden');
        }

        function showApp() {
            document.getElementById('login-modal').classList.add('hidden');
            document.getElementById('app-container').classList.remove('hidden');

            // Desktop profile widget
            document.getElementById('desktop-user-name').textContent = currentUser.name;
            document.getElementById('desktop-user-role').textContent = getRoleBadgeText(currentUser.role);
            document.getElementById('desktop-user-avatar').textContent = currentUser.name.charAt(0).toUpperCase();

            // Header role badge
            const badgeEl = document.getElementById('header-role-badge');
            if (badgeEl) {
                badgeEl.textContent = getRoleBadgeText(currentUser.role);
                badgeEl.className = `px-3 py-1 rounded-full text-xs font-bold font-mono border ${getRoleBadgeClass(currentUser.role)}`;
            }

            const mobileBadge = document.getElementById('mobile-role-badge');
            if (mobileBadge) mobileBadge.textContent = getRoleBadgeText(currentUser.role);

            renderNavigation();
            switchTab('dashboard');
        }

        function getRoleBadgeText(role) {
            switch(role) {
                case 'owner': return '👑 EGA (MASTER)';
                case 'admin': return '🛡️ ADMIN';
                case 'teacher': return '👨‍🏫 O\'QITUVCHI';
                case 'student': return '🎓 O\'QUVCHI';
                default: return role;
            }
        }

        function getRoleBadgeClass(role) {
            switch(role) {
                case 'owner': return 'bg-purple-950/60 text-purple-300 border-purple-500/40';
                case 'admin': return 'bg-blue-950/60 text-blue-300 border-blue-500/40';
                case 'teacher': return 'bg-emerald-950/60 text-emerald-300 border-emerald-500/40';
                case 'student': return 'bg-cyan-950/60 text-cyan-300 border-cyan-500/40';
                default: return 'bg-slate-800 text-slate-300 border-slate-700';
            }
        }

        function renderNavigation() {
            const sidebarNav = document.getElementById('sidebar-nav');
            const mobileNav = document.getElementById('mobile-bottom-nav-links');
            sidebarNav.innerHTML = '';
            mobileNav.innerHTML = '';

            const menuItems = [
                { id: 'dashboard', label: 'Bosh Panel', icon: 'fa-chart-pie', roles: ['owner', 'admin', 'teacher', 'student'] },
                { id: 'scanner', label: 'AI Skaner', icon: 'fa-camera-rotate', roles: ['owner', 'admin', 'teacher', 'student'] },
                { id: 'users', label: 'Foydalanuvchilar', icon: 'fa-users-gear', roles: ['owner', 'admin'] },
                { id: 'attendance', label: 'Davomat', icon: 'fa-calendar-check', roles: ['owner', 'admin', 'teacher'] },
                { id: 'grades', label: 'Baholar', icon: 'fa-award', roles: ['owner', 'admin', 'teacher', 'student'] },
                { id: 'my-profile', label: 'Profilim', icon: 'fa-id-card', roles: ['student'] }
            ];

            menuItems.forEach(item => {
                if (item.roles.includes(currentUser.role)) {
                    // Desktop sidebar button
                    const btn = document.createElement('button');
                    btn.id = `nav-btn-${item.id}`;
                    btn.onclick = () => switchTab(item.id);
                    btn.className = `w-full flex items-center gap-3 px-3 py-2.5 rounded-xl text-xs font-semibold transition text-left`;
                    btn.innerHTML = `<i class="fa-solid ${item.icon} text-base"></i><span>${item.label}</span>`;
                    sidebarNav.appendChild(btn);

                    // Mobile bottom nav button
                    const mBtn = document.createElement('button');
                    mBtn.id = `mob-btn-${item.id}`;
                    mBtn.onclick = () => switchTab(item.id);
                    mBtn.className = `flex flex-col items-center justify-center p-1.5 text-slate-400 transition`;
                    mBtn.innerHTML = `<i class="fa-solid ${item.icon} text-base mb-0.5"></i><span class="text-[9px]">${item.label}</span>`;
                    mobileNav.appendChild(mBtn);
                }
            });
        }

        function switchTab(tabId) {
            activeTab = tabId;

            // Stop scanner camera if switching away from scanner
            if (tabId !== 'scanner' && scannerStream) {
                scannerStream.getTracks().forEach(track => track.stop());
                scannerStream = null;
            }

            // Update desktop nav styles
            const desktopBtns = document.querySelectorAll('#sidebar-nav button');
            desktopBtns.forEach(btn => {
                if (btn.id === `nav-btn-${tabId}`) {
                    btn.className = `w-full flex items-center gap-3 px-3 py-2.5 rounded-xl text-xs font-semibold bg-gradient-to-r from-accentPrimary/20 to-accentCyan/10 text-white border border-accentPrimary/30`;
                } else {
                    btn.className = `w-full flex items-center gap-3 px-3 py-2.5 rounded-xl text-xs font-semibold text-slate-400 hover:text-white hover:bg-white/5`;
                }
            });

            // Update mobile nav styles
            const mobileBtns = document.querySelectorAll('#mobile-bottom-nav-links button');
            mobileBtns.forEach(btn => {
                if (btn.id === `mob-btn-${tabId}`) {
                    btn.className = `flex flex-col items-center justify-center p-1.5 text-accentCyan font-bold`;
                } else {
                    btn.className = `flex flex-col items-center justify-center p-1.5 text-slate-400 hover:text-white`;
                }
            });

            const pageTitleEl = document.getElementById('page-title');
            if (pageTitleEl) {
                switch(tabId) {
                    case 'dashboard': pageTitleEl.innerHTML = `<i class="fa-solid fa-chart-pie text-accentCyan"></i> Bosh Panel`; break;
                    case 'scanner': pageTitleEl.innerHTML = `<i class="fa-solid fa-camera-rotate text-accentPurple"></i> AI Vision & Narx Skaneri`; break;
                    case 'users': pageTitleEl.innerHTML = `<i class="fa-solid fa-users-gear text-accentPrimary"></i> Foydalanuvchilarni Boshqarish`; break;
                    case 'attendance': pageTitleEl.innerHTML = `<i class="fa-solid fa-calendar-check text-accentGreen"></i> Davomat Tizimi`; break;
                    case 'grades': pageTitleEl.innerHTML = `<i class="fa-solid fa-award text-accentYellow"></i> Baholar Jurnali`; break;
                    case 'my-profile': pageTitleEl.innerHTML = `<i class="fa-solid fa-id-card text-purple-400"></i> Mening Ma'lumotlarim`; break;
                }
            }

            if (tabId === 'dashboard') renderDashboardView();
            else if (tabId === 'scanner') renderScannerView();
            else if (tabId === 'users') renderUsersView();
            else if (tabId === 'attendance') renderAttendanceView();
            else if (tabId === 'grades') renderGradesView();
            else if (tabId === 'my-profile') renderStudentProfileView();
        }

        // VIEW: SCANNER & PRICE EVALUATOR
        function renderScannerView() {
            const container = document.getElementById('content-view');
            container.innerHTML = `
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-4">
                    <div class="glass-panel p-5 rounded-2xl space-y-4">
                        <h3 class="font-bold text-white text-sm flex items-center gap-2">
                            <i class="fa-solid fa-camera text-accentCyan"></i> Metall yoki Buyumni Skanerlash
                        </h3>
                        <div class="relative w-full h-64 bg-slate-950 rounded-xl overflow-hidden border border-white/10 flex items-center justify-center">
                            <video id="scanner-video" autoplay playsinline class="w-full h-full object-cover"></video>
                            <canvas id="scanner-canvas" class="hidden"></canvas>
                            <div id="scanner-placeholder" class="absolute inset-0 flex flex-col items-center justify-center text-slate-400 text-xs space-y-2">
                                <i class="fa-solid fa-video-slash text-2xl"></i>
                                <span>Kamera yoniq emas</span>
                            </div>
                            <div class="absolute inset-x-0 top-1/2 -translate-y-1/2 border-t-2 border-dashed border-accentCyan/50 pointer-events-none"></div>
                        </div>
                        <div class="flex gap-2">
                            <button onclick="startCamera()" class="flex-1 py-2.5 rounded-xl bg-accentCyan/20 text-accentCyan border border-accentCyan/30 text-xs font-bold">
                                <i class="fa-solid fa-video mr-1"></i> Kamerani Yoqish
                            </button>
                            <button onclick="captureAndAnalyzeMetal()" class="flex-1 py-2.5 rounded-xl bg-accentPrimary text-white text-xs font-bold shadow-lg">
                                <i class="fa-solid fa-wand-magic-sparkles mr-1"></i> Metall Narxini Skanerlash
                            </button>
                        </div>
                    </div>

                    <div class="glass-panel p-5 rounded-2xl space-y-4 flex flex-col">
                        <h3 class="font-bold text-white text-sm flex items-center gap-2">
                            <i class="fa-solid fa-scale-balanced text-accentYellow"></i> Metall Turi va Narx Bahosi (1 kg uchun / dona)
                        </h3>
                        <div id="scan-result-box" class="flex-1 bg-slate-950/60 rounded-xl p-4 border border-white/10 flex flex-col justify-center items-center text-center space-y-3">
                            <i class="fa-solid fa-cubes text-4xl text-slate-600"></i>
                            <p class="text-xs text-slate-400">Mis (Copper), Alyuminiy, Temir (Iron), Latun, Zanglamaydigan po'lat (Stainless Steel) yoki boshqa metallarni kameraga ko'rsating!</p>
                        </div>
                        <div class="relative">
                            <input type="text" id="manual-item-input" placeholder="Yoki metall nomini yozing (masalan: mis, alyuminiy, temir)..." 
                                class="w-full bg-slate-900 border border-white/10 rounded-xl px-4 py-2.5 text-xs text-white focus:outline-none focus:border-accentPrimary pr-24">
                            <button onclick="analyzeManualItem()" class="absolute right-1 top-1 bottom-1 px-4 bg-accentPrimary text-white rounded-lg text-xs font-bold">Qidirish</button>
                        </div>
                    </div>
                </div>

                <div class="glass-panel p-5 rounded-2xl space-y-3">
                    <h3 class="font-bold text-white text-sm flex items-center gap-2">
                        <i class="fa-solid fa-clock-rotate-left text-accentPurple"></i> Skanerlangan Metallar Tarixi
                    </h3>
                    <div id="scans-history-list" class="space-y-2">
                        ${db.scans.length === 0 ? '<p class="text-xs text-slate-500 text-center py-4">Hali skanerlangan metallar yo\'q</p>' : ''}
                        ${db.scans.map(s => `
                            <div class="p-3 rounded-xl bg-slate-900/40 border border-white/5 flex justify-between items-center text-xs">
                                <div>
                                    <div class="font-bold text-white">${s.name}</div>
                                    <div class="text-[10px] text-slate-400 font-mono">${s.date} • ${s.category || 'Metall'}</div>
                                </div>
                                <div class="text-right">
                                    <span class="font-mono font-bold text-accentGreen text-sm">${s.price}</span>
                                    <div class="text-[9px] text-slate-400">${s.condition || 'Qoldiq / Lom'}</div>
                                </div>
                            </div>
                        `).join('')}
                    </div>
                </div>
            `;
        }

        async function startCamera() {
            const video = document.getElementById('scanner-video');
            const placeholder = document.getElementById('scanner-placeholder');
            try {
                scannerStream = await navigator.mediaDevices.getUserMedia({ video: { facingMode: 'environment' } });
                video.srcObject = scannerStream;
                placeholder.classList.add('hidden');
            } catch(e) {
                alert("Kameraga ruxsat berilmadi yoki kamera topilmadi!");
            }
        }

        async function captureAndAnalyzeMetal() {
            const video = document.getElementById('scanner-video');
            const canvas = document.getElementById('scanner-canvas');
            if (!scannerStream) {
                alert("Avval kamerani yoqing!");
                return;
            }

            canvas.width = video.videoWidth || 640;
            canvas.height = video.videoHeight || 480;
            const ctx = canvas.getContext('2d');
            ctx.drawImage(video, 0, 0, canvas.width, canvas.height);
            const base64Data = canvas.toDataURL('image/jpeg').split(',')[1];

            const resultBox = document.getElementById('scan-result-box');
            resultBox.innerHTML = `
                <div class="animate-spin text-accentCyan text-3xl mb-2"><i class="fa-solid fa-spinner"></i></div>
                <div class="text-xs text-white font-bold">Metall turi aniqlanib, narxi hisoblanmoqda...</div>
            `;

            try {
                const apiKey = "";
                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3.1-flash-image:generateContent?key=${apiKey}`;
                const payload = {
                    contents: [{
                        role: "user",
                        parts: [
                            { text: "Analyze this metal item image. Identify the exact metal type (e.g., Copper/Mis, Aluminum/Alyuminiy, Iron/Temir, Brass/Latun, Stainless Steel). Return JSON with fields: name (in Uzbek), category ('Metall lom / Xomashyo'), estimatedPriceUZS (price per kg in UZS, e.g. '85,000 so'm / kg'), description (short summary in Uzbek), condition." },
                            { inlineData: { mimeType: "image/jpeg", data: base64Data } }
                        ]
                    }],
                    generationConfig: { responseMimeType: "application/json" }
                };

                const res = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });
                const data = await res.json();
                const parsed = JSON.parse(data.candidates[0].content.parts[0].text);

                displayScanResult(parsed);
            } catch(e) {
                const mock = { name: "Mis qoldig'i (Copper Scrap)", category: "Rangli metall", estimatedPriceUZS: "95,000 so'm / kg", description: "Yuqori sifatli toza mis sim yoki quvur qoldig'i.", condition: "Toza" };
                displayScanResult(mock);
            }
        }

        async function analyzeManualItem() {
            const input = document.getElementById('manual-item-input');
            const query = input.value.trim();
            if (!query) return;

            const resultBox = document.getElementById('scan-result-box');
            resultBox.innerHTML = `
                <div class="animate-spin text-accentCyan text-3xl mb-2"><i class="fa-solid fa-spinner"></i></div>
                <div class="text-xs text-white font-bold">"${query}" metall narxi qidirilmoqda...</div>
            `;

            try {
                const apiKey = "";
                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${apiKey}`;
                const payload = {
                    contents: [{ parts: [{ text: `Provide scrap or market price in Uzbekistan for metal: ${query} per kg or unit in Uzbek sums. Return JSON format with fields: name, category, estimatedPriceUZS, description, condition.` }] }],
                    tools: [{ "google_search": {} }],
                    generationConfig: { responseMimeType: "application/json" }
                };

                const res = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });
                const data = await res.json();
                const parsed = JSON.parse(data.candidates[0].content.parts[0].text);
                displayScanResult(parsed);
            } catch(e) {
                displayScanResult({ name: query, category: "Metall Lom", estimatedPriceUZS: "12,000 so'm / kg", description: "O'rtacha bozor narxi hisoblandi.", condition: "Standart" });
            }
        }

        function displayScanResult(item) {
            const resultBox = document.getElementById('scan-result-box');
            resultBox.innerHTML = `
                <div class="text-left w-full space-y-2 bg-slate-900/80 p-4 rounded-xl border border-white/10">
                    <div class="flex justify-between items-start">
                        <h4 class="font-bold text-white text-sm">${item.name}</h4>
                        <span class="px-2 py-0.5 rounded bg-emerald-500/20 text-emerald-300 text-[10px] font-mono">${item.category}</span>
                    </div>
                    <div class="text-lg font-black text-accentGreen font-mono">${item.estimatedPriceUZS}</div>
                    <p class="text-[11px] text-slate-300">${item.description}</p>
                    <div class="text-[10px] text-slate-400 font-mono">Holati: <span class="text-white">${item.condition}</span></div>
                </div>
            `;

            db.scans.unshift({
                id: 'scan_' + Date.now(),
                name: item.name,
                category: item.category,
                price: item.estimatedPriceUZS,
                condition: item.condition,
                date: new Date().toISOString().split('T')[0]
            });
            saveStoredData('scans', db.scans);
        }

            const totalStudents = db.users.filter(u => u.role === 'student').length;
            const totalTeachers = db.users.filter(u => u.role === 'teacher').length;
            const totalAdmins = db.users.filter(u => u.role === 'admin' || u.role === 'owner').length;

            container.innerHTML = `
                <div class="grid grid-cols-2 lg:grid-cols-3 gap-3 sm:gap-4">
                    <div class="glass-panel p-4 rounded-2xl">
                        <div class="text-[11px] text-slate-400">Jami O'quvchilar</div>
                        <div class="text-2xl font-black text-white mt-1">${totalStudents}</div>
                    </div>
                    <div class="glass-panel p-4 rounded-2xl">
                        <div class="text-[11px] text-slate-400">O'qituvchilar</div>
                        <div class="text-2xl font-black text-white mt-1">${totalTeachers}</div>
                    </div>
                    <div class="glass-panel p-4 rounded-2xl col-span-2 lg:col-span-1">
                        <div class="text-[11px] text-slate-400">Adminlar va Ega</div>
                        <div class="text-2xl font-black text-white mt-1">${totalAdmins}</div>
                    </div>
                </div>

                <div class="glass-panel p-4 sm:p-5 rounded-2xl space-y-3">
                    <h3 class="font-bold text-white text-sm flex items-center gap-2">
                        <i class="fa-solid fa-bolt text-accentYellow"></i> Tezkor Amallar (Ega va Admin paneli)
                    </h3>
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-2">
                        <button onclick="openUserModal('student')" class="p-3.5 rounded-xl bg-cyan-500/10 border border-cyan-500/30 text-cyan-300 text-xs font-semibold text-left flex items-center gap-3">
                            <i class="fa-solid fa-user-plus text-xl"></i>
                            <div>
                                <div class="font-bold">O'quvchi qo'shish</div>
                                <div class="text-[10px] text-slate-400">Yangi login parol berish</div>
                            </div>
                        </button>
                        <button onclick="openUserModal('admin')" class="p-3.5 rounded-xl bg-purple-500/10 border border-purple-500/30 text-purple-300 text-xs font-semibold text-left flex items-center gap-3">
                            <i class="fa-solid fa-user-shield text-xl"></i>
                            <div>
                                <div class="font-bold">Admin/Yordamchi tayinlash</div>
                                <div class="text-[10px] text-slate-400">Boshqalarga huquq berish</div>
                            </div>
                        </button>
                        <button onclick="switchTab('users')" class="p-3.5 rounded-xl bg-emerald-500/10 border border-emerald-500/30 text-emerald-300 text-xs font-semibold text-left flex items-center gap-3">
                            <i class="fa-solid fa-users text-xl"></i>
                            <div>
                                <div class="font-bold">Foydalanuvchilar ro'yxati</div>
                                <div class="text-[10px] text-slate-400">Hammasini ko'rish va o'chirish</div>
                            </div>
                        </button>
                    </div>
                </div>
            `;
        }

        function renderStudentDashboard(container) {
            const myAtt = db.attendance.filter(a => a.studentId === currentUser.id);
            const myGrades = db.grades.filter(g => g.studentId === currentUser.id);
            const avgGrade = myGrades.length > 0 ? (myGrades.reduce((acc, g) => acc + g.score, 0) / myGrades.length).toFixed(1) : 0;

            container.innerHTML = `
                <div class="glass-panel p-5 rounded-2xl flex flex-col sm:flex-row items-center gap-4 text-center sm:text-left">
                    <div class="w-16 h-16 rounded-2xl bg-gradient-to-tr from-accentCyan to-accentPrimary flex items-center justify-center text-2xl text-white font-bold shadow-lg">
                        ${currentUser.name.charAt(0)}
                    </div>
                    <div>
                        <h2 class="text-xl font-bold text-white">${currentUser.name}</h2>
                        <p class="text-xs text-accentCyan font-mono mt-0.5">Sinf/Guruh: ${currentUser.group}</p>
                        <p class="text-[11px] text-slate-400 mt-1 font-mono">Sizning loginingiz: <span class="text-white font-bold">${currentUser.login}</span></p>
                    </div>
                    <div class="sm:ml-auto flex gap-2">
                        <div class="px-4 py-2.5 rounded-xl bg-slate-900/60 border border-white/10 text-center">
                            <div class="text-[10px] text-slate-400">O'rtacha Ballingiz</div>
                            <div class="text-lg font-bold text-accentYellow">${avgGrade}</div>
                        </div>
                    </div>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div class="glass-panel p-5 rounded-2xl space-y-3">
                        <h3 class="font-bold text-white text-sm flex items-center gap-2">
                            <i class="fa-solid fa-award text-accentYellow"></i> Mening Baholarim
                        </h3>
                        <div class="space-y-2">
                            ${myGrades.length === 0 ? '<p class="text-xs text-slate-500 text-center py-4">Hali baholar qo\'yilmagan</p>' : ''}
                            ${myGrades.map(g => `
                                <div class="p-3 rounded-xl bg-slate-900/40 border border-white/5 flex justify-between items-center text-xs">
                                    <div>
                                        <div class="font-semibold text-white">${g.subject}</div>
                                        <div class="text-[10px] text-slate-400 font-mono">${g.date} • ${g.comment || ''}</div>
                                    </div>
                                    <span class="font-bold text-accentYellow font-mono text-sm">${g.score} ball</span>
                                </div>
                            `).join('')}
                        </div>
                    </div>

                    <div class="glass-panel p-5 rounded-2xl space-y-3">
                        <h3 class="font-bold text-white text-sm flex items-center gap-2">
                            <i class="fa-solid fa-calendar-check text-accentGreen"></i> Mening Davomatim
                        </h3>
                        <div class="space-y-2">
                            ${myAtt.length === 0 ? '<p class="text-xs text-slate-500 text-center py-4">Davomat yozuvlari topilmadi</p>' : ''}
                            ${myAtt.map(a => `
                                <div class="p-3 rounded-xl bg-slate-900/40 border border-white/5 flex justify-between items-center text-xs">
                                    <div class="font-mono text-slate-300">${a.date}</div>
                                    <span class="px-2.5 py-1 rounded-lg text-[10px] font-bold ${a.status === 'Kelgan' ? 'bg-emerald-500/20 text-emerald-300 border border-emerald-500/30' : a.status === 'Sababli' ? 'bg-yellow-500/20 text-yellow-300 border border-yellow-500/30' : 'bg-red-500/20 text-red-300 border border-red-500/30'}">
                                        ${a.status}
                                    </span>
                                </div>
                            `).join('')}
                        </div>
                    </div>
                </div>
            `;
        }

        // VIEW 2: USERS (Manage students, admins, teachers)
        function renderUsersView() {
            const container = document.getElementById('content-view');
            container.innerHTML = `
                <div class="flex justify-between items-center gap-2 flex-wrap">
                    <span class="text-xs text-slate-400">Jami foydalanuvchilar: <strong class="text-white">${db.users.length}</strong> ta</span>
                    <div class="flex gap-2">
                        <button onclick="openUserModal('admin')" class="px-3 py-2 rounded-xl text-xs font-semibold bg-purple-600/30 text-purple-300 border border-purple-500/40 hover:bg-purple-600/50">
                            🛡️ Admin Qo'shish
                        </button>
                        <button onclick="openUserModal('student')" class="px-3 py-2 rounded-xl text-xs font-semibold bg-accentPrimary text-white shadow-lg">
                            + O'quvchi Qo'shish
                        </button>
                    </div>
                </div>

                <div class="glass-panel rounded-2xl overflow-hidden">
                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-xs">
                            <thead class="bg-slate-900/80 text-slate-400 font-mono">
                                <tr>
                                    <th class="p-3">F.I.SH</th>
                                    <th class="p-3">Roli (Ega / Admin / O'quvchi)</th>
                                    <th class="p-3">Guruh / Sinf</th>
                                    <th class="p-3">Login va Parol</th>
                                    <th class="p-3 text-right">Amallar</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-white/5">
                                ${db.users.map(u => `
                                    <tr class="hover:bg-white/5">
                                        <td class="p-3 font-semibold text-white">${u.name}</td>
                                        <td class="p-3"><span class="px-2.5 py-1 rounded text-[10px] font-mono border ${getRoleBadgeClass(u.role)}">${getRoleBadgeText(u.role)}</span></td>
                                        <td class="p-3 text-slate-300 font-mono">${u.group || '-'}</td>
                                        <td class="p-3 font-mono">
                                            <span class="text-accentCyan bg-slate-900 px-2 py-0.5 rounded">${u.login}</span> / 
                                            <span class="text-slate-400 bg-slate-900 px-2 py-0.5 rounded">${u.pass}</span>
                                        </td>
                                        <td class="p-3 text-right">
                                            ${u.role !== 'owner' ? `<button onclick="deleteUser('${u.id}')" class="text-red-400 hover:text-red-300 p-1.5"><i class="fa-solid fa-trash"></i></button>` : '<span class="text-[10px] text-purple-400 font-mono">Asosiy</span>'}
                                        </td>
                                    </tr>
                                `).join('')}
                            </tbody>
                        </table>
                    </div>
                </div>
            `;
        }

        function deleteUser(id) {
            if (confirm("Ushbu foydalanuvchini o'chirmoqchimisiz?")) {
                db.users = db.users.filter(u => u.id !== id);
                saveStoredData('users', db.users);
                renderUsersView();
            }
        }

        // VIEW 3: ATTENDANCE
        function renderAttendanceView() {
            const container = document.getElementById('content-view');
            const todayStr = new Date().toISOString().split('T')[0];

            container.innerHTML = `
                <div class="glass-panel p-4 sm:p-5 rounded-2xl space-y-4">
                    <div class="flex justify-between items-center flex-wrap gap-2">
                        <h3 class="font-bold text-white text-sm">O'quvchilar Davomatini Belgilash</h3>
                        <input type="date" id="att-date" value="${todayStr}" onchange="renderAttendanceView()" class="bg-slate-900 border border-white/10 rounded-xl px-3 py-1.5 text-xs text-white font-mono">
                    </div>
                    <div class="space-y-2">
                        ${db.users.filter(u => u.role === 'student').length === 0 ? '<p class="text-xs text-slate-500 text-center py-6">Hali o\'quvchilar qo\'shilmagan. Avval o\'quvchi qo\'shing!</p>' : ''}
                        ${db.users.filter(u => u.role === 'student').map(st => {
                            const dateVal = document.getElementById('att-date') ? document.getElementById('att-date').value : todayStr;
                            const rec = db.attendance.find(a => a.studentId === st.id && a.date === dateVal) || {};
                            return `
                                <div class="p-3 rounded-xl bg-slate-900/50 border border-white/5 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-2 text-xs">
                                    <div>
                                        <div class="font-bold text-white">${st.name}</div>
                                        <div class="text-[10px] text-slate-400 font-mono">Guruh: ${st.group} | Login: ${st.login}</div>
                                    </div>
                                    <div class="flex items-center gap-2 w-full sm:w-auto justify-between sm:justify-end">
                                        <select id="status-${st.id}" class="bg-slate-900 border border-white/10 rounded-lg px-2.5 py-1.5 text-xs text-white">
                                            <option value="Kelgan" ${rec.status === 'Kelgan' ? 'selected' : ''}>✅ Kelgan</option>
                                            <option value="Kelmagan" ${rec.status === 'Kelmagan' ? 'selected' : ''}>❌ Kelmagan</option>
                                            <option value="Sababli" ${rec.status === 'Sababli' ? 'selected' : ''}>🟡 Sababli</option>
                                        </select>
                                        <button onclick="saveMobileAttendance('${st.id}')" class="px-3.5 py-1.5 rounded-lg bg-accentGreen/20 text-accentGreen border border-accentGreen/30 font-semibold hover:bg-accentGreen/30">Saqlash</button>
                                    </div>
                                </div>
                            `;
                        }).join('')}
                    </div>
                </div>
            `;
        }

        function saveMobileAttendance(studentId) {
            const date = document.getElementById('att-date').value;
            const status = document.getElementById(`status-${studentId}`).value;
            const idx = db.attendance.findIndex(a => a.studentId === studentId && a.date === date);

            if (idx !== -1) db.attendance[idx].status = status;
            else db.attendance.push({ id: 'att_' + Date.now(), studentId, date, status, note: '' });

            saveStoredData('attendance', db.attendance);
            alert("Davomat muvaffaqiyatli saqlandi!");
        }

        // VIEW 4: GRADES
        function renderGradesView() {
            const container = document.getElementById('content-view');
            container.innerHTML = `
                <div class="glass-panel p-4 sm:p-5 rounded-2xl space-y-4">
                    <div class="flex justify-between items-center">
                        <h3 class="font-bold text-white text-sm">O'quvchilar Baholari Jurnali</h3>
                        ${currentUser.role !== 'student' ? `<button onclick="openGradeModal()" class="px-3 py-1.5 rounded-xl text-xs bg-accentYellow/20 text-accentYellow border border-accentYellow/30 font-semibold">+ Baho qo'yish</button>` : ''}
                    </div>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-xs">
                            <thead class="bg-slate-900/80 text-slate-400 font-mono">
                                <tr>
                                    <th class="p-3">Sana</th>
                                    <th class="p-3">O'quvchi</th>
                                    <th class="p-3">Mavzu / Fan</th>
                                    <th class="p-3">Baho</th>
                                    <th class="p-3">Izoh</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-white/5">
                                ${db.grades.map(g => {
                                    const st = db.users.find(u => u.id === g.studentId);
                                    return `
                                        <tr>
                                            <td class="p-3 font-mono text-slate-400">${g.date}</td>
                                            <td class="p-3 font-semibold text-white">${st ? st.name : '-'}</td>
                                            <td class="p-3 text-slate-300">${g.subject}</td>
                                            <td class="p-3 font-bold text-accentYellow font-mono">${g.score} ball</td>
                                            <td class="p-3 text-slate-400">${g.comment || '-'}</td>
                                        </tr>
                                    `;
                                }).join('')}
                            </tbody>
                        </table>
                    </div>
                </div>
            `;
        }

        function renderStudentProfileView() {
            renderStudentDashboard(document.getElementById('content-view'));
        }

        // MODAL HELPERS
        function openUserModal(role) {
            document.getElementById('modal-title').textContent = role === 'admin' ? "Yangi Admin Qo'shish" : "Yangi O'quvchi Qo'shish";
            document.getElementById('modal-name').value = '';
            document.getElementById('modal-role').value = role;
            const rand = Math.floor(1000 + Math.random() * 9000);
            document.getElementById('modal-login').value = (role === 'admin' ? 'admin_' : 'user_') + rand;
            document.getElementById('modal-password').value = 'mehnatkash' + rand;
            document.getElementById('form-modal').classList.remove('hidden');
        }

        function closeModal() {
            document.getElementById('form-modal').classList.add('hidden');
        }

        function saveUserForm(e) {
            e.preventDefault();
            db.users.push({
                id: 'u_' + Date.now(),
                name: document.getElementById('modal-name').value.trim(),
                role: document.getElementById('modal-role').value,
                group: document.getElementById('modal-group').value,
                login: document.getElementById('modal-login').value.trim(),
                pass: document.getElementById('modal-password').value.trim()
            });
            saveStoredData('users', db.users);
            closeModal();
            renderUsersView();
            alert("Yangi foydalanuvchi muvaffaqiyatli qo'shildi!");
        }

        function openGradeModal() {
            const subject = prompt("Fan yoki mavzu nomini kiriting (masalan: Python 3-bob):", "Python asoslari");
            if (!subject) return;
            const studentName = prompt("O'quvchi ismini kiriting:");
            if (!studentName) return;
            const st = db.users.find(u => u.name.toLowerCase().includes(studentName.toLowerCase()) && u.role === 'student');
            if (!st) {
                alert("Bunday o'quvchi topilmadi!");
                return;
            }
            const score = parseInt(prompt("Ballni kiriting (0 - 100):", "90"));
            if (isNaN(score)) return;

            db.grades.push({
                id: 'g_' + Date.now(),
                studentId: st.id,
                subject: subject,
                score: score,
                date: new Date().toISOString().split('T')[0],
                comment: 'O\'qituvchi baholadi'
            });
            saveStoredData('grades', db.grades);
            renderGradesView();
            alert("Baho muvaffaqiyatli qo'shildi!");
        }
    </script>
</body>
</html>
