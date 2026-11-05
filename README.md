
<!DOCTYPE html>
<html lang="uz" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mehnatkash O'quv Markazi | Kelajak Kasblari</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        darkBg: '#090d16',
                        cardBg: 'rgba(255, 255, 255, 0.05)',
                        cardBorder: 'rgba(255, 255, 255, 0.1)',
                        neonCyan: '#00f3ff',
                        neonPurple: '#b026ff',
                        neonGreen: '#00ff66'
                    }
                }
            }
        }
    </script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=Orbitron:wght@500;700;900&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: #090d16;
            color: #f8fafc;
            overflow-x: hidden;
        }
        .font-tech {
            font-family: 'Orbitron', sans-serif;
        }
        .glassmorphism {
            background: rgba(15, 23, 42, 0.75);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }
        .glass-card {
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.05) 0%, rgba(255, 255, 255, 0.01) 100%);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.08);
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }
        .glass-card:hover {
            transform: translateY(-8px);
            border-color: rgba(0, 243, 255, 0.4);
            box-shadow: 0 15px 35px -5px rgba(0, 243, 255, 0.2);
        }
        .neon-glow {
            text-shadow: 0 0 20px rgba(0, 243, 255, 0.6);
        }
        .neon-btn {
            background: linear-gradient(135deg, #00f3ff 0%, #b026ff 100%);
            transition: all 0.3s ease;
        }
        .neon-btn:hover {
            box-shadow: 0 0 25px rgba(0, 243, 255, 0.6);
            transform: scale(1.02);
        }
        #particles-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            pointer-events: none;
        }
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #090d16;
        }
        ::-webkit-scrollbar-thumb {
            background: rgba(255, 255, 255, 0.15);
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: rgba(0, 243, 255, 0.4);
        }
    </style>
</head>
<body class="relative min-h-screen flex flex-col selection:bg-cyan-500 selection:text-black">

    <!-- Particle Background Canvas -->
    <canvas id="particles-canvas"></canvas>

    <!-- Header / Navbar -->
    <header class="fixed top-0 left-0 w-full z-50 glassmorphism border-b border-white/10">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            <a href="#hero" class="flex items-center space-x-3">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-cyan-400 to-purple-600 flex items-center justify-center shadow-lg shadow-cyan-500/30">
                    <i class="fa-solid fa-graduation-cap text-black text-lg"></i>
                </div>
                <span class="font-tech text-xl sm:text-2xl font-extrabold tracking-wider bg-gradient-to-r from-white via-cyan-200 to-cyan-400 bg-clip-text text-transparent">
                    MEHNAT<span class="text-cyan-400">KASH</span>
                </span>
            </a>
            <nav class="hidden md:flex items-center space-x-8 text-sm font-medium text-slate-300">
                <a href="#hero" class="hover:text-cyan-400 transition">Bosh sahifa</a>
                <a href="#courses" class="hover:text-cyan-400 transition">Kurslar</a>
                <a href="#about" class="hover:text-cyan-400 transition">Markaz haqida</a>
                <a href="#contact" class="hover:text-cyan-400 transition">Aloqa</a>
            </nav>
            <div>
                <a href="#contact" class="neon-btn px-6 py-2.5 rounded-xl font-bold text-black text-sm shadow-md inline-block">
                    Darsga yozilish
                </a>
            </div>
        </div>
    </header>

    <!-- Main Content Wrapper -->
    <div class="relative z-10 pt-20">

        <!-- Hero Section -->
        <section id="hero" class="relative min-h-[85vh] flex items-center justify-center pt-16 pb-20 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
            <div>
                <div class="inline-flex items-center space-x-2 px-4 py-2 rounded-full glassmorphism text-xs sm:text-sm text-cyan-300 mb-8 border border-cyan-500/30">
                    <span class="w-2 h-2 rounded-full bg-cyan-400 animate-pulse"></span>
                    <span>Andijondagi zamonaviy ta'lim va innovatsiyalar markazi</span>
                </div>
                <h1 class="text-4xl sm:text-6xl lg:text-7xl font-extrabold tracking-tight leading-tight mb-8">
                    Kelajak kasblarini <br>
                    <span class="bg-gradient-to-r from-cyan-400 via-purple-400 to-pink-500 bg-clip-text text-transparent neon-glow font-tech">
                        "MEHNATKASH"
                    </span> bilan o'rganing!
                </h1>
                <p class="max-w-2xl mx-auto text-base sm:text-xl text-slate-300 mb-10 font-light leading-relaxed">
                    IT (Havaskor & Pro), Robototexnika, Ingliz tili (IELTS / CEFR) va Matematika yo'nalishlarida nazariy hamda amaliy bilimlarni egallang.
                </p>
                <div class="flex flex-col sm:flex-row items-center justify-center gap-4">
                    <a href="#courses" class="w-full sm:w-auto neon-btn px-8 py-4 rounded-xl font-bold text-black text-base shadow-xl">
                        Barcha kurslar <i class="fa-solid fa-arrow-right ml-2"></i>
                    </a>
                    <a href="#contact" class="w-full sm:w-auto px-8 py-4 rounded-xl font-semibold glassmorphism text-white hover:border-cyan-400 transition text-base">
                        Bepul sinov darsiga yozilish
                    </a>
                </div>

                <!-- Stats Counter -->
                <div class="grid grid-cols-2 md:grid-cols-4 gap-6 mt-16 max-w-4xl mx-auto">
                    <div class="glass-card p-6 rounded-2xl text-center">
                        <div class="text-3xl sm:text-4xl font-extrabold text-cyan-400 font-tech mb-1">1200+</div>
                        <div class="text-xs sm:text-sm text-slate-400">Muvaffaqiyatli o'quvchilar</div>
                    </div>
                    <div class="glass-card p-6 rounded-2xl text-center">
                        <div class="text-3xl sm:text-4xl font-extrabold text-purple-400 font-tech mb-1">15+</div>
                        <div class="text-xs sm:text-sm text-slate-400">Tajribali ustozlar</div>
                    </div>
                    <div class="glass-card p-6 rounded-2xl text-center">
                        <div class="text-3xl sm:text-4xl font-extrabold text-pink-400 font-tech mb-1">5 ta</div>
                        <div class="text-xs sm:text-sm text-slate-400">Asosiy yo'nalish</div>
                    </div>
                    <div class="glass-card p-6 rounded-2xl text-center">
                        <div class="text-3xl sm:text-4xl font-extrabold text-green-400 font-tech mb-1">98%</div>
                        <div class="text-xs sm:text-sm text-slate-400">Natijaga kafolat</div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Courses Section -->
        <section id="courses" class="py-20 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 w-full">
            <div class="text-center mb-16">
                <h2 class="text-xs font-bold text-cyan-400 uppercase tracking-widest font-tech mb-2">Yo'nalishlarimiz</h2>
                <h3 class="text-3xl sm:text-5xl font-bold mb-4">O'zingizga Mos Kursni Tanlang</h3>
                <p class="text-slate-400 max-w-xl mx-auto text-sm sm:text-base">Noldan boshlab professional darajagacha sifatli ta'lim tizimi.</p>
                
                <!-- Filters -->
                <div class="flex flex-wrap items-center justify-center gap-2 sm:gap-4 mt-8">
                    <button onclick="filterCourses('all', this)" class="filter-btn px-5 py-2.5 rounded-xl text-xs sm:text-sm font-semibold glassmorphism border-cyan-400 bg-cyan-500/20 text-cyan-300 transition">Barchasi</button>
                    <button onclick="filterCourses('it-havaskor', this)" class="filter-btn px-5 py-2.5 rounded-xl text-xs sm:text-sm font-semibold glassmorphism text-slate-300 hover:text-white transition">IT (Havaskor)</button>
                    <button onclick="filterCourses('it-pro', this)" class="filter-btn px-5 py-2.5 rounded-xl text-xs sm:text-sm font-semibold glassmorphism text-slate-300 hover:text-white transition">IT (Professional)</button>
                    <button onclick="filterCourses('robotics', this)" class="filter-btn px-5 py-2.5 rounded-xl text-xs sm:text-sm font-semibold glassmorphism text-slate-300 hover:text-white transition">Robototexnika</button>
                    <button onclick="filterCourses('english', this)" class="filter-btn px-5 py-2.5 rounded-xl text-xs sm:text-sm font-semibold glassmorphism text-slate-300 hover:text-white transition">Ingliz tili</button>
                    <button onclick="filterCourses('math', this)" class="filter-btn px-5 py-2.5 rounded-xl text-xs sm:text-sm font-semibold glassmorphism text-slate-300 hover:text-white transition">Matematika</button>
                </div>
            </div>

            <!-- Course Cards Grid -->
            <div id="courses-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                
                <!-- Card 1: IT Havaskor -->
                <div class="glass-card rounded-2xl p-6 flex flex-col justify-between course-item" data-category="it-havaskor">
                    <div>
                        <div class="flex items-center justify-between mb-4">
                            <span class="px-3 py-1 rounded-full text-xs font-semibold bg-cyan-500/10 text-cyan-300 border border-cyan-500/30">IT Havaskor</span>
                            <i class="fa-solid fa-laptop-code text-2xl text-cyan-400"></i>
                        </div>
                        <h3 class="text-xl font-bold mb-2 text-white">Kompyuter Savodxonligi & Web Asoslari</h3>
                        <p class="text-slate-400 text-sm mb-6 leading-relaxed">Kompyuterda ishlashni o'rganish, Windows/Office dasturlari, Scratch orqali mantiqiy fikrlash hamda HTML va CSS yordamida ilk saytlarni yaratish.</p>
                    </div>
                    <div class="pt-4 border-t border-white/10 flex items-center justify-between">
                        <span class="text-xs text-slate-400"><i class="fa-regular fa-clock mr-1 text-cyan-400"></i> 2-3 oy</span>
                        <button onclick="openModal('IT Havaskor', 'Kompyuter Savodxonligi va Web Asoslari', '2-3 oy', 'Boshlang\'ich', 'Kompyuter va Windows tizimida bexato ishlash, internet xavfsizligi, Microsoft Office (Word, Excel, PowerPoint) dasturlari, Scratch orqali dasturlash mantig\'ini shakllantirish hamda HTML5/CSS3 yordamida moslashuvchan veb-sahifalar yaratish.')" class="text-cyan-400 font-semibold text-sm hover:underline">Batafsil <i class="fa-solid fa-arrow-right ml-1"></i></button>
                    </div>
                </div>

                <!-- Card 2: IT Professional -->
                <div class="glass-card rounded-2xl p-6 flex flex-col justify-between course-item" data-category="it-pro">
                    <div>
                        <div class="flex items-center justify-between mb-4">
                            <span class="px-3 py-1 rounded-full text-xs font-semibold bg-purple-500/10 text-purple-300 border border-purple-500/30">IT Professional</span>
                            <i class="fa-solid fa-code text-2xl text-purple-400"></i>
                        </div>
                        <h3 class="text-xl font-bold mb-2 text-white">Full-Stack & Python Dasturlash</h3>
                        <p class="text-slate-400 text-sm mb-6 leading-relaxed">Python, Flask framework, JavaScript, REST API, ma'lumotlar bazasi (SQL) va real loyihalar yaratish bo'yicha professional kurs.</p>
                    </div>
                    <div class="pt-4 border-t border-white/10 flex items-center justify-between">
                        <span class="text-xs text-slate-400"><i class="fa-regular fa-clock mr-1 text-purple-400"></i> 6-8 oy</span>
                        <button onclick="openModal('IT Professional', 'Full-Stack & Python Dasturlash', '6-8 oy', 'O\'rta / Professional', 'Python asoslari va OOP, Flask/Django yordamida backend veb-ilovalar yaratish, JavaScript, React asoslari, APIlar bilan ishlash, ma\'lumotlar bazasi (PostgreSQL/SQLite) va GitHub tizimi.')" class="text-purple-400 font-semibold text-sm hover:underline">Batafsil <i class="fa-solid fa-arrow-right ml-1"></i></button>
                    </div>
                </div>

                <!-- Card 3: Robototexnika -->
                <div class="glass-card rounded-2xl p-6 flex flex-col justify-between course-item" data-category="robotics">
                    <div>
                        <div class="flex items-center justify-between mb-4">
                            <span class="px-3 py-1 rounded-full text-xs font-semibold bg-pink-500/10 text-pink-300 border border-pink-500/30">Robototexnika</span>
                            <i class="fa-solid fa-robot text-2xl text-pink-400"></i>
                        </div>
                        <h3 class="text-xl font-bold mb-2 text-white">Arduino & Smart Qurilmalar</h3>
                        <p class="text-slate-400 text-sm mb-6 leading-relaxed">Arduino mikrokontrollerlari, datchiklar, servo motorlar hamda Bluetooth modullari yordamida avtomatlashtirilgan aqlli loyihalar yig'ish.</p>
                    </div>
                    <div class="pt-4 border-t border-white/10 flex items-center justify-between">
                        <span class="text-xs text-slate-400"><i class="fa-regular fa-clock mr-1 text-pink-400"></i> 4-5 oy</span>
                        <button onclick="openModal('Robototexnika', 'Arduino va Aqlli Qurilmalar', '4-5 oy', 'Barcha yoshdagilar', 'Elektronika asoslari, sxemalar yig\'ish, Arduino C++ dasturlash tili, datchiklar bilan ishlash, ultratovushli robotlar va Smart Home (Aqlli Uy) loyihalarini yaratish amaliyoti.')" class="text-pink-400 font-semibold text-sm hover:underline">Batafsil <i class="fa-solid fa-arrow-right ml-1"></i></button>
                    </div>
                </div>

                <!-- Card 4: Ingliz tili - IELTS/CEFR -->
                <div class="glass-card rounded-2xl p-6 flex flex-col justify-between course-item" data-category="english">
                    <div>
                        <div class="flex items-center justify-between mb-4">
                            <span class="px-3 py-1 rounded-full text-xs font-semibold bg-blue-500/10 text-blue-300 border border-blue-500/30">Ingliz tili</span>
                            <i class="fa-solid fa-award text-2xl text-blue-400"></i>
                        </div>
                        <h3 class="text-xl font-bold mb-2 text-white">IELTS & CEFR Tayyorlov</h3>
                        <p class="text-slate-400 text-sm mb-6 leading-relaxed">Intensiv Listening, Reading, Writing hamda Speaking darslari. IELTS 7.0+ va CEFR B2/C1 darajalariga sifatli va tizimli tayyorgarlik.</p>
                    </div>
                    <div class="pt-4 border-t border-white/10 flex items-center justify-between">
                        <span class="text-xs text-slate-400"><i class="fa-regular fa-clock mr-1 text-blue-400"></i> 4-6 oy</span>
                        <button onclick="openModal('Ingliz tili', 'IELTS & CEFR Tayyorlov', '4-6 oy', 'B2 - C1 Daraja', 'Speaking, Listening, Reading va Writing ko\'nikmalarini mukammal rivojlantirish, imtihon strategiyalari, har haftalik Mock testlar va tajribali IELTS instruktorlar bilan ishlash.')" class="text-blue-400 font-semibold text-sm hover:underline">Batafsil <i class="fa-solid fa-arrow-right ml-1"></i></button>
                    </div>
                </div>

                <!-- Card 5: Ingliz tili - General -->
                <div class="glass-card rounded-2xl p-6 flex flex-col justify-between course-item" data-category="english">
                    <div>
                        <div class="flex items-center justify-between mb-4">
                            <span class="px-3 py-1 rounded-full text-xs font-semibold bg-green-500/10 text-green-300 border border-green-500/30">Ingliz tili</span>
                            <i class="fa-solid fa-comments text-2xl text-green-400"></i>
                        </div>
                        <h3 class="text-xl font-bold mb-2 text-white">General English (A1 - B2)</h3>
                        <p class="text-slate-400 text-sm mb-6 leading-relaxed">Ingliz tilida erkin so'zlashish, grammatika va lug'at boyligini oshirish bo'yicha interaktiv darslar hamda Speaking Club lar.</p>
                    </div>
                    <div class="pt-4 border-t border-white/10 flex items-center justify-between">
                        <span class="text-xs text-slate-400"><i class="fa-regular fa-clock mr-1 text-green-400"></i> 4 oy</span>
                        <button onclick="openModal('Ingliz tili', 'General English (A1-B2)', '4 oy', 'A1 - B2 Daraja', 'Grammatika, talaffuz (pronunciation), lug\'at boyligi, o\'qish va so'zlashuv ko'nikmalarini amaliy muloqot va audio-video materiallar orqali oshirish.')" class="text-green-400 font-semibold text-sm hover:underline">Batafsil <i class="fa-solid fa-arrow-right ml-1"></i></button>
                    </div>
                </div>

                <!-- Card 6: Matematika -->
                <div class="glass-card rounded-2xl p-6 flex flex-col justify-between course-item" data-category="math">
                    <div>
                        <div class="flex items-center justify-between mb-4">
                            <span class="px-3 py-1 rounded-full text-xs font-semibold bg-amber-500/10 text-amber-300 border border-amber-500/30">Matematika</span>
                            <i class="fa-solid fa-calculator text-2xl text-amber-400"></i>
                        </div>
                        <h3 class="text-xl font-bold mb-2 text-white">Mental Arifmetika & Maktab/Litsey Tayyorlov</h3>
                        <p class="text-slate-400 text-sm mb-6 leading-relaxed">Mantiqiy fikrlashni rivojlantirish, tezkor hisoblash hamda litsey va universitet imtihonlariga chuqurlashtirilgan tayyorgarlik.</p>
                    </div>
                    <div class="pt-4 border-t border-white/10 flex items-center justify-between">
                        <span class="text-xs text-slate-400"><i class="fa-regular fa-clock mr-1 text-amber-400"></i> 5-6 oy</span>
                        <button onclick="openModal('Matematika', 'Mental Arifmetika va Maktab Matematikasi', '5-6 oy', 'Maktab va Abituriyentlar', 'Tezkor miya hisob-kitoblari (Abakus), algebra, geometriya, mantiqiy masalalar yechish va Milliy Sertifikat hamda OTM imtihonlariga tayyorgarlik.')" class="text-amber-400 font-semibold text-sm hover:underline">Batafsil <i class="fa-solid fa-arrow-right ml-1"></i></button>
                    </div>
                </div>

            </div>
        </section>

        <!-- About Section -->
        <section id="about" class="py-20 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="glassmorphism rounded-3xl p-8 sm:p-12 border border-white/10 relative overflow-hidden">
                <div class="absolute -right-20 -bottom-20 w-96 h-96 bg-cyan-500/10 rounded-full blur-3xl pointer-events-none"></div>
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
                    <div>
                        <h2 class="text-xs font-bold text-cyan-400 uppercase tracking-widest font-tech mb-2">Markazimiz Afzalliklari</h2>
                        <h3 class="text-3xl sm:text-4xl font-bold mb-6 text-white">Nega Aynan <span class="text-cyan-400 font-tech">Mehnatkash</span>?</h3>
                        <ul class="space-y-4 text-slate-300 text-sm sm:text-base">
                            <li class="flex items-start space-x-3">
                                <i class="fa-solid fa-circle-check text-cyan-400 mt-1"></i>
                                <span>Amaliyotga yo'naltirilgan zamonaviy o'quv dasturlari va shaxsiy kompyuterlar.</span>
                            </li>
                            <li class="flex items-start space-x-3">
                                <i class="fa-solid fa-circle-check text-cyan-400 mt-1"></i>
                                <span>O'z sohasida ko'p yillik tajribaga ega malakali va talabchan ustozlar.</span>
                            </li>
                            <li class="flex items-start space-x-3">
                                <i class="fa-solid fa-circle-check text-cyan-400 mt-1"></i>
                                <span>Har bir o'quvchiga individual yondashuv hamda shaxsiy mentorlik yordami.</span>
                            </li>
                            <li class="flex items-start space-x-3">
                                <i class="fa-solid fa-circle-check text-cyan-400 mt-1"></i>
                                <span>Kurs yakunida sertifikat va yuqori natija ko'rsatganlarga ishga joylashishda ko'mak.</span>
                            </li>
                        </ul>
                    </div>
                    <div class="grid grid-cols-2 gap-4">
                        <div class="glass-card p-6 rounded-2xl text-center">
                            <i class="fa-solid fa-laptop text-3xl text-cyan-400 mb-3"></i>
                            <h4 class="font-bold mb-1 text-white">Zamonaviy jihozlar</h4>
                            <p class="text-xs text-slate-400">So'nggi rusumdagi kompyuterlar va robototexnika to'plamlari.</p>
                        </div>
                        <div class="glass-card p-6 rounded-2xl text-center">
                            <i class="fa-solid fa-award text-3xl text-purple-400 mb-3"></i>
                            <h4 class="font-bold mb-1 text-white">Sifat kafolati</h4>
                            <p class="text-xs text-slate-400">Muntazam bilim nazorati va qo'shimcha amaliy darslar.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Contact & Registration Form Section -->
        <section id="contact" class="py-20 max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 w-full">
            <div class="text-center mb-12">
                <h2 class="text-xs font-bold text-cyan-400 uppercase tracking-widest font-tech mb-2">Bog'lanish</h2>
                <h3 class="text-3xl sm:text-4xl font-bold mb-4 text-white">Kursga Ro'yxatdan O'ting</h3>
                <p class="text-slate-400 text-sm sm:text-base">Ma'lumotlaringizni qoldiring, bizning mas'ul xodimimiz tez orada siz bilan bog'lanadi.</p>
            </div>

            <div class="glassmorphism rounded-3xl p-8 sm:p-10 border border-white/10 shadow-2xl relative">
                <form id="contact-form" onsubmit="sendToTelegram(event)" class="space-y-6">
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
                        <div>
                            <label class="block text-sm font-medium text-slate-300 mb-2">Ism va familiyangiz</label>
                            <input type="text" id="user-name" required placeholder="Masalan: Anvar Rahimov" class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 text-white placeholder-slate-500 focus:outline-none focus:border-cyan-400 transition">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-300 mb-2">Telefon raqamingiz</label>
                            <input type="tel" id="user-phone" required placeholder="+998 90 123 45 67" class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 text-white placeholder-slate-500 focus:outline-none focus:border-cyan-400 transition">
                        </div>
                    </div>

                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
                        <div>
                            <label class="block text-sm font-medium text-slate-300 mb-2">Elektron pochtangiz (Email)</label>
                            <input type="email" id="user-email" required placeholder="example@gmail.com" class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 text-white placeholder-slate-500 focus:outline-none focus:border-cyan-400 transition">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-300 mb-2">Qaysi kursni tanlaysiz?</label>
                            <select id="user-course" required class="w-full bg-[#090d16] border border-white/10 rounded-xl px-4 py-3 text-white focus:outline-none focus:border-cyan-400 transition">
                                <option value="" disabled selected>Kursni tanlang...</option>
                                <option value="IT Havaskor">IT Havaskor (Kompyuter savodxonligi & Web)</option>
                                <option value="IT Professional">IT Professional (Full-Stack & Python)</option>
                                <option value="Robototexnika">Robototexnika (Arduino & Smart qurilmalar)</option>
                                <option value="Ingliz tili - IELTS/CEFR">Ingliz tili (IELTS & CEFR tayyorlov)</option>
                                <option value="Ingliz tili - General">Ingliz tili (General English)</option>
                                <option value="Matematika">Matematika & Mental Arifmetika</option>
                            </select>
                        </div>
                    </div>

                    <div>
                        <label class="block text-sm font-medium text-slate-300 mb-2">Qo'shimcha xabar yoki savolingiz</label>
                        <textarea id="user-message" rows="4" placeholder="Savol yoki taklifingiz bo'lsa yozib qoldiring..." class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 text-white placeholder-slate-500 focus:outline-none focus:border-cyan-400 transition"></textarea>
                    </div>

                    <button type="submit" id="submit-btn" class="w-full neon-btn py-4 rounded-xl font-bold text-black text-base shadow-xl flex items-center justify-center space-x-2">
                        <span>Arizani Yuborish</span>
                        <i class="fa-solid fa-paper-plane"></i>
                    </button>
                </form>

                <div id="form-success" class="hidden mt-6 p-4 rounded-xl bg-green-500/20 border border-green-500/40 text-green-300 text-center font-medium">
                    ✅ Arizangiz muvaffaqiyatli yuborildi! Tez orada siz bilan bog'lanamiz.
                </div>
                <div id="form-error" class="hidden mt-6 p-4 rounded-xl bg-red-500/20 border border-red-500/40 text-red-300 text-center font-medium">
                    ❌ Xatolik yuz berdi. Iltimos, qaytadan urinib ko'ring.
                </div>
            </div>
        </section>

        <!-- Footer -->
        <footer class="mt-auto border-t border-white/10 glassmorphism py-8 text-center text-slate-400 text-sm">
            <div class="max-w-7xl mx-auto px-4 flex flex-col sm:flex-row items-center justify-between gap-4">
                <div class="flex items-center space-x-2">
                    <span class="font-bold text-white font-tech">"MEHNATKASH" O'quv Markazi</span>
                </div>
                <p>&copy; 2026 Barcha huquqlar himoyalangan.</p>
                <div class="flex space-x-4 text-lg">
                    <a href="#" class="hover:text-cyan-400 transition"><i class="fa-brands fa-telegram"></i></a>
                    <a href="#" class="hover:text-cyan-400 transition"><i class="fa-brands fa-instagram"></i></a>
                    <a href="#" class="hover:text-cyan-400 transition"><i class="fa-brands fa-facebook"></i></a>
                </div>
            </div>
        </footer>

    </div>

    <!-- Course Detail Modal -->
    <div id="course-modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/80 backdrop-blur-md hidden">
        <div class="glassmorphism max-w-lg w-full rounded-3xl p-6 sm:p-8 border border-white/20 relative shadow-2xl">
            <button onclick="closeModal()" class="absolute top-5 right-5 text-slate-400 hover:text-white text-xl">
                <i class="fa-solid fa-xmark"></i>
            </button>
            <span id="modal-badge" class="px-3 py-1 rounded-full text-xs font-semibold bg-cyan-500/10 text-cyan-300 border border-cyan-500/30 inline-block mb-4"></span>
            <h3 id="modal-title" class="text-2xl font-bold mb-2 text-white"></h3>
            <div class="flex items-center space-x-4 text-sm text-slate-400 mb-6">
                <span><i class="fa-regular fa-clock mr-1 text-cyan-400"></i> <span id="modal-duration"></span></span>
                <span><i class="fa-solid fa-layer-group mr-1 text-purple-400"></i> <span id="modal-level"></span></span>
            </div>
            <p id="modal-desc" class="text-slate-300 text-sm leading-relaxed mb-8"></p>
            <div class="flex space-x-4">
                <a href="#contact" onclick="closeModal(); selectModalCourse();" class="flex-1 neon-btn py-3 rounded-xl font-bold text-black text-center text-sm">
                    Shu kursga yozilish
                </a>
                <button onclick="closeModal()" class="px-5 py-3 rounded-xl glassmorphism text-slate-300 hover:text-white text-sm">
                    Yopish
                </button>
            </div>
        </div>
    </div>

    <!-- JavaScript code -->
    <script>
        // Particle Animation Script
        const canvas = document.getElementById('particles-canvas');
        const ctx = canvas.getContext('2d');
        let particlesArray = [];

        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        class Particle {
            constructor() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.size = Math.random() * 2 + 0.5;
                this.speedX = (Math.random() - 0.5) * 0.5;
                this.speedY = (Math.random() - 0.5) * 0.5;
                this.color = Math.random() > 0.5 ? '#00f3ff' : '#b026ff';
            }
            update() {
                this.x += this.speedX;
                this.y += this.speedY;
                if (this.x < 0 || this.x > canvas.width) this.speedX = -this.speedX;
                if (this.y < 0 || this.y > canvas.height) this.speedY = -this.speedY;
            }
            draw() {
                ctx.fillStyle = this.color;
                ctx.shadowBlur = 10;
                ctx.shadowColor = this.color;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
                ctx.shadowBlur = 0;
            }
        }

        function initParticles() {
            particlesArray = [];
            let count = Math.floor((canvas.width * canvas.height) / 15000);
            for (let i = 0; i < count; i++) {
                particlesArray.push(new Particle());
            }
        }
        initParticles();

        function animateParticles() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            particlesArray.forEach(p => {
                p.update();
                p.draw();
            });
            requestAnimationFrame(animateParticles);
        }
        animateParticles();

        // Course Filtering
        function filterCourses(category, btnElement) {
            const items = document.querySelectorAll('.course-item');
            const buttons = document.querySelectorAll('.filter-btn');

            buttons.forEach(btn => {
                btn.classList.remove('border-cyan-400', 'bg-cyan-500/20', 'text-cyan-300');
                btn.classList.add('text-slate-300');
            });

            btnElement.classList.add('border-cyan-400', 'bg-cyan-500/20', 'text-cyan-300');
            btnElement.classList.remove('text-slate-300');

            items.forEach(item => {
                if (category === 'all' || item.getAttribute('data-category') === category) {
                    item.style.display = 'flex';
                } else {
                    item.style.display = 'none';
                }
            });
        }

        // Modal Functionality
        let currentCourseBadge = '';
        function openModal(badge, title, duration, level, desc) {
            currentCourseBadge = badge;
            document.getElementById('modal-badge').innerText = badge;
            document.getElementById('modal-title').innerText = title;
            document.getElementById('modal-duration').innerText = duration;
            document.getElementById('modal-level').innerText = level;
            document.getElementById('modal-desc').innerText = desc;
            document.getElementById('course-modal').classList.remove('hidden');
        }

        function closeModal() {
            document.getElementById('course-modal').classList.add('hidden');
        }

        function selectModalCourse() {
            const selectElem = document.getElementById('user-course');
            for (let i = 0; i < selectElem.options.length; i++) {
                if (selectElem.options[i].text.includes(currentCourseBadge) || selectElem.options[i].value.includes(currentCourseBadge)) {
                    selectElem.selectedIndex = i;
                    break;
                }
            }
        }

        // Telegram Bot Integration
        const BOT_TOKEN = '8528033534:AAGFprpZZFf-poDA5hCtY47o9hEXe2t26OU';
        const CHAT_ID = '8689546738';

        async function sendToTelegram(e) {
            e.preventDefault();
            const name = document.getElementById('user-name').value;
            const phone = document.getElementById('user-phone').value;
            const email = document.getElementById('user-email').value;
            const course = document.getElementById('user-course').value;
            const message = document.getElementById('user-message').value;
            const submitBtn = document.getElementById('submit-btn');

            const text = `📩 <b>"MEHNATKASH" O'QUV MARKAZIDAN YANGI ARIZA!</b>\n\n` +
                         `👤 <b>Ism:</b> ${name}\n` +
                         `📞 <b>Telefon:</b> ${phone}\n` +
                         `📧 <b>Email:</b> ${email}\n` +
                         `📚 <b>Tanlangan Kurs:</b> ${course}\n` +
                         `💬 <b>Xabar:</b> ${message || "Kiritilmagan"}\n\n` +
                         `⚡ <i>Ushbu o'quvchi bilan tezroq bog'laning!</i>`;

            submitBtn.disabled = true;
            submitBtn.innerHTML = `<span>Yuborilmoqda...</span> <i class="fa-solid fa-spinner animate-spin"></i>`;

            try {
                const response = await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        chat_id: CHAT_ID,
                        text: text,
                        parse_mode: 'HTML'
                    })
                });

                const data = await response.json();
                if (data.ok) {
                    document.getElementById('form-success').classList.remove('hidden');
                    document.getElementById('form-error').classList.add('hidden');
                    document.getElementById('contact-form').reset();
                } else {
                    throw new Error('Telegram API error');
                }
            } catch (error) {
                document.getElementById('form-error').classList.remove('hidden');
                document.getElementById('form-success').classList.add('hidden');
            } finally {
                submitBtn.disabled = false;
                submitBtn.innerHTML = `<span>Arizani Yuborish</span> <i class="fa-solid fa-paper-plane"></i>`;
            }
        }
    </script>
</body>
</html>
