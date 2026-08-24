<!DOCTYPE html>
<html lang="ar" dir="rtl" id="htmlRoot">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MK Creator Hub | Next Founders Hackathon</title>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            scroll-behavior: smooth;
        }

        body {
            background-color: #0f172a;
            color: #f8fafc;
            line-height: 1.6;
        }

        /* Navbar */
        .navbar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 8%;
            background: rgba(15, 23, 42, 0.9);
            position: fixed;
            top: 0;
            width: 100%;
            backdrop-filter: blur(10px);
            z-index: 1000;
            border-bottom: 1px solid #1e293b;
        }

        .logo {
            font-size: 24px;
            font-weight: bold;
            color: #38bdf8;
        }

        .nav-links {
            display: flex;
            align-items: center;
            gap: 20px;
        }

        .navbar nav a {
            color: #cbd5e1;
            text-decoration: none;
            margin: 0 10px;
            transition: 0.3s;
        }

        .navbar nav a:hover {
            color: #38bdf8;
        }

        /* Lang Switcher Button */
        .lang-btn {
            background: #1e293b;
            color: #38bdf8;
            border: 1px solid #38bdf8;
            padding: 6px 14px;
            border-radius: 6px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.3s;
        }

        .lang-btn:hover {
            background: #38bdf8;
            color: #0f172a;
        }

        .cta-btn {
            background: #38bdf8;
            color: #0f172a;
            padding: 8px 20px;
            border-radius: 6px;
            text-decoration: none;
            font-weight: bold;
            transition: 0.3s;
        }

        .cta-btn:hover {
            background: #0ea5e9;
        }

        /* Hero Section */
        .hero {
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            padding: 0 20px;
            background: linear-gradient(rgba(15, 23, 42, 0.8), rgba(15, 23, 42, 0.9)), url('https://images.unsplash.com/photo-1518770660439-4636190af475?auto=format&fit=crop&w=1200&q=80');
            background-size: cover;
            background-position: center;
        }

        .hero-content h1 {
            font-size: 45px;
            margin-bottom: 15px;
            color: #ffffff;
        }

        .welcome-badge {
            display: inline-block;
            background: rgba(56, 189, 248, 0.1);
            color: #38bdf8;
            padding: 6px 16px;
            border-radius: 20px;
            border: 1px solid rgba(56, 189, 248, 0.3);
            font-size: 15px;
            margin-bottom: 20px;
            font-weight: 600;
        }

        .hero-content p {
            font-size: 18px;
            color: #94a3b8;
            max-width: 600px;
            margin: 0 auto 30px auto;
        }

        .hero-buttons .btn {
            padding: 12px 25px;
            border-radius: 8px;
            text-decoration: none;
            font-weight: bold;
            margin: 0 10px;
            display: inline-block;
        }

        .btn.primary {
            background: #38bdf8;
            color: #0f172a;
        }

        .btn.secondary {
            background: transparent;
            border: 2px solid #38bdf8;
            color: #38bdf8;
        }

        /* Features Section */
        .features {
            padding: 80px 10%;
            text-align: center;
        }

        .features h2, .interactive-tool h2, .business-model h2 {
            font-size: 32px;
            margin-bottom: 50px;
            color: #38bdf8;
        }

        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 30px;
        }

        .card {
            background: #1e293b;
            padding: 30px;
            border-radius: 12px;
            transition: 0.3s;
            border: 1px solid #334155;
        }

        .card:hover {
            transform: translateY(-5px);
            border-color: #38bdf8;
        }

        .card i {
            font-size: 40px;
            color: #38bdf8;
            margin-bottom: 15px;
        }

        /* Interactive Tool Section */
        .interactive-tool {
            padding: 80px 10%;
            text-align: center;
            background: #0b1120;
        }

        .tool-box {
            max-width: 800px;
            margin: 0 auto;
            background: #1e293b;
            padding: 30px;
            border-radius: 12px;
            border: 1px solid #334155;
        }

        .category-buttons {
            display: flex;
            justify-content: center;
            gap: 12px;
            flex-wrap: wrap;
            margin-bottom: 25px;
        }

        .cat-btn {
            background: #0f172a;
            color: #38bdf8;
            border: 1px solid #38bdf8;
            padding: 10px 20px;
            border-radius: 8px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.3s;
        }

        .cat-btn:hover, .cat-btn.active {
            background: #38bdf8;
            color: #0f172a;
            transform: translateY(-2px);
        }

        .result-box {
            margin-top: 20px;
            padding: 20px;
            background: #0f172a;
            border-radius: 8px;
            color: #e2e8f0;
            border: 1px dashed #38bdf8;
            text-align: inherit;
            min-height: 110px;
            font-size: 17px;
            position: relative;
        }

        /* Action Buttons Inside Result */
        .result-actions {
            display: flex;
            gap: 10px;
            justify-content: flex-end;
            margin-top: 15px;
        }

        .action-tool-btn {
            background: #1e293b;
            color: #38bdf8;
            border: 1px solid #38bdf8;
            padding: 6px 12px;
            border-radius: 6px;
            font-size: 13px;
            cursor: pointer;
            transition: 0.3s;
            font-weight: bold;
        }

        .action-tool-btn:hover {
            background: #38bdf8;
            color: #0f172a;
        }

        /* Saved Ideas Box */
        .saved-section {
            margin-top: 30px;
            text-align: inherit;
            background: #0f172a;
            padding: 15px;
            border-radius: 8px;
            border: 1px solid #334155;
        }

        .saved-section h4 {
            color: #38bdf8;
            margin-bottom: 10px;
            font-size: 16px;
        }

        .saved-list {
            list-style: none;
            max-height: 120px;
            overflow-y: auto;
            padding-left: 5px;
        }

        .saved-list li {
            background: #1e293b;
            padding: 8px 12px;
            border-radius: 6px;
            margin-bottom: 6px;
            font-size: 14px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .saved-list li button {
            background: transparent;
            border: none;
            color: #ef4444;
            cursor: pointer;
        }

        /* Loading Spinner */
        .spinner {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(56, 189, 248, 0.3);
            border-radius: 50%;
            border-top-color: #38bdf8;
            animation: spin 0.8s ease-in-out infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        /* Business Model Section */
        .business-model {
            padding: 80px 10%;
            text-align: center;
        }

        .business-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 30px;
        }

        .b-card {
            background: #1e293b;
            padding: 30px;
            border-radius: 12px;
            border: 1px solid #334155;
        }

        .b-card h3 {
            color: #38bdf8;
            margin-bottom: 10px;
        }

        /* Footer */
        footer {
            text-align: center;
            padding: 20px;
            background: #0b1120;
            color: #64748b;
            border-top: 1px solid #1e293b;
        }
    </style>
</head>
<body>

    <!-- Header / Navbar -->
    <header class="navbar">
        <div class="logo">
            <i class="fa-solid fa-rocket"></i> <span id="navLogo">MK Creator Hub</span>
        </div>
        <div class="nav-links">
            <nav>
                <a href="#features" id="navFeatures">المميزات</a>
                <a href="#tool" id="navTool">الأداة التفاعلية</a>
                <a href="#business" id="navBusiness">نموذج البيزنس</a>
            </nav>
            <!-- زر تغيير اللغة -->
            <button class="lang-btn" onclick="toggleLanguage()" id="langSwitchBtn">English 🌐</button>
            <a href="#tool" class="cta-btn" id="navCta">ابدأ الآن</a>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="hero">
        <div class="hero-content">
            <div class="welcome-badge" id="welcomeBadge">👋 أهلاً بك يا محمد في منصتك الذكية</div>
            <h1 id="heroTitle">منصتك الذكية لإدارة المحتوى وصناع المشاريع الناشئة</h1>
            <p id="heroDesc">أداة ويب متكاملة مصممة خصيصاً لمساعدة المبدعين وأصحاب الوكالات على تنظيم أفكارهم ومشاريعهم بكل سهولة واحترافية.</p>
            <div class="hero-buttons">
                <a href="#tool" class="btn primary" id="heroBtn1">جرب الأداة الآن</a>
                <a href="#features" class="btn secondary" id="heroBtn2">اكتشف المميزات</a>
            </div>
        </div>
    </section>

    <!-- Features Section -->
    <section id="features" class="features">
        <h2 id="featuresHeading">لماذا MK Creator Hub؟</h2>
        <div class="features-grid">
            <div class="card">
                <i class="fa-solid fa-bolt"></i>
                <h3 id="feat1Title">سرعة وأداء عالي</h3>
                <p id="feat1Desc">مبني بأحدث تقنيات الـ Front-End لضمان تجربة مستخدم سلسة وسريعة جداً.</p>
            </div>
            <div class="card">
                <i class="fa-solid fa-chart-line"></i>
                <h3 id="feat2Title">تتبع وتخطيط المشاريع</h3>
                <p id="feat2Desc">نظام ذكي يساعدك على متابعة مهامك ومشاريعك اليومية بدون تعقيد.</p>
            </div>
            <div class="card">
                <i class="fa-solid fa-shield-halved"></i>
                <h3 id="feat3Title">موثوق وآمن</h3>
                <p id="feat3Desc">حماية كاملة لبياناتك وأفكارك ومشاريعك الناشئة في مكان واحد.</p>
            </div>
        </div>
    </section>

    <!-- Interactive Tool Section (The Core Feature) -->
    <section id="tool" class="interactive-tool">
        <h2 id="toolHeading">مولد الأفكار السريع للمشاريع 💡</h2>
        <p id="toolSub">اختر المجال الذي تود استكشاف أفكاره:</p>
        
        <div class="tool-box">
            <!-- أزرار المجالات التفاعلية -->
            <div class="category-buttons">
                <button class="cat-btn" onclick="showIdea('code')" id="btnCode">💻 برمجة (Code)</button>
                <button class="cat-btn" onclick="showIdea('editing')" id="btnEditing">🎬 مونتاج (Editing)</button>
                <button class="cat-btn" onclick="showIdea('design')" id="btnDesign">🎨 تصميم (Design)</button>
                <button class="cat-btn" onclick="showIdea('marketing')" id="btnMarketing">📈 تسويق (Marketing)</button>
            </div>

            <!-- مربع عرض النتيجة والأفكار -->
            <div id="ideaResult" class="result-box">
                اختر أحد المجالات بالأعلى لتوليد فكرة مشروع احترافية فوراً... 🚀
            </div>

            <!-- قائمة الأفكار المحفوظة -->
            <div class="saved-section">
                <h4 id="savedHeading">📌 الأفكار المحفوظة المفضلة:</h4>
                <ul id="savedList" class="saved-list">
                    <li style="color: #64748b; text-align: center; display: block;" id="noSavedText">لا توجد أفكار محفوظة حالياً...</li>
                </ul>
            </div>
        </div>
    </section>

    <!-- Business Model Section -->
    <section id="business" class="business-model">
        <h2 id="busHeading">نموذج العمل والربح (Business Model)</h2>
        <div class="business-grid">
            <div class="b-card">
                <h3 id="bus1Title">اشتراكات شهرية (SaaS)</h3>
                <p id="bus1Desc">باقات مدفوعة للميزات المتقدمة وتخزين أكبر للمشاريع.</p>
            </div>
            <div class="b-card">
                <h3 id="bus2Title">الخدمات الاستشارية</h3>
                <p id="bus2Desc">ربط صناع المحتوى بالخبراء لتطوير أعمالهم مقابل نسبة عمولة.</p>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <p id="footerText">تم تطوير هذا المشروع خصيصاً لـ Next Founders Hackathon | تصميم وبناء فريق MK</p>
    </footer>

    <script>
        let currentLang = 'ar';
        let currentGeneratedIdea = '';
        let savedIdeas = JSON.parse(localStorage.getItem('mk_saved_ideas')) || [];

        const translations = {
            ar: {
                welcomeBadge: "👋 أهلاً بك يا محمد في منصتك الذكية",
                navFeatures: "المميزات",
                navTool: "الأداة التفاعلية",
                navBusiness: "نموذج البيزنس",
                navCta: "ابدأ الآن",
                langSwitchBtn: "English 🌐",
                heroTitle: "منصتك الذكية لإدارة المحتوى وصناع المشاريع الناشئة",
                heroDesc: "أداة ويب متكاملة مصممة خصيصاً لمساعدة المبدعين وأصحاب الوكالات على تنظيم أفكارهم ومشاريعهم بكل سهولة واحترافية.",
                heroBtn1: "جرب الأداة الآن",
                heroBtn2: "اكتشف المميزات",
                featuresHeading: "لماذا MK Creator Hub؟",
                feat1Title: "سرعة وأداء عالي",
                feat1Desc: "مبني بأحدث تقنيات الـ Front-End لضمان تجربة مستخدم سلسة وسريعة جداً.",
                feat2Title: "تتبع وتخطيط المشاريع",
                feat2Desc: "نظام ذكي يساعدك على متابعة مهامك ومشاريعك اليومية بدون تعقيد.",
                feat3Title: "موثوق وآمن",
                feat3Desc: "حماية كاملة لبياناتك وأفكارك ومشاريعك الناشئة في مكان واحد.",
                toolHeading: "مولد الأفكار السريع للمشاريع 💡",
                toolSub: "اختر المجال الذي تود استكشاف أفكاره:",
                btnCode: "💻 برمجة (Code)",
                btnEditing: "🎬 مونتاج (Editing)",
                btnDesign: "🎨 تصميم (Design)",
                btnMarketing: "📈 تسويق (Marketing)",
                defaultResult: "اختر أحد المجالات بالأعلى لتوليد فكرة مشروع احترافية فوراً... 🚀",
                savedHeading: "📌 الأفكار المحفوظة المفضلة:",
                noSavedText: "لا توجد أفكار محفوظة حالياً...",
                busHeading: "نموذج العمل والربح (Business Model)",
                bus1Title: "اشتراكات شهرية (SaaS)",
                bus1Desc: "باقات مدفوعة للميزات المتقدمة وتخزين أكبر للمشاريع.",
                bus2Title: "الخدمات الاستشارية",
                bus2Desc: "ربط صناع المحتوى بالخبراء لتطوير أعمالهم مقابل نسبة عمولة.",
                footerText: "تم تطوير هذا المشروع خصيصاً لـ Next Founders Hackathon | تصميم وبناء فريق MK"
            },
            en: {
                welcomeBadge: "👋 Welcome Mohamed to your smart platform",
                navFeatures: "Features",
                navTool: "Interactive Tool",
                navBusiness: "Business Model",
                navCta: "Get Started",
                langSwitchBtn: "العربية 🌐",
                heroTitle: "Your Smart Platform for Content & Startup Management",
                heroDesc: "A complete web tool designed specifically to help creators and agency owners organize ideas and projects smoothly and professionally.",
                heroBtn1: "Try Tool Now",
                heroBtn2: "Explore Features",
                featuresHeading: "Why MK Creator Hub?",
                feat1Title: "High Speed & Performance",
                feat1Desc: "Built with modern Front-End technologies to ensure an ultra-smooth user experience.",
                feat2Title: "Project Tracking & Planning",
                feat2Desc: "A smart system to help you track daily tasks and projects without complexity.",
                feat3Title: "Secure & Reliable",
                feat3Desc: "Complete protection for your data, ideas, and startup projects in one place.",
                toolHeading: "Quick Startup Idea Generator 💡",
                toolSub: "Choose the field you want to explore ideas for:",
                btnCode: "💻 Code",
                btnEditing: "🎬 Editing",
                btnDesign: "🎨 Design",
                btnMarketing: "📈 Marketing",
                defaultResult: "Select one of the fields above to instantly generate a professional project idea... 🚀",
                savedHeading: "📌 Saved Favorite Ideas:",
                noSavedText: "No saved ideas yet...",
                busHeading: "Business Model",
                bus1Title: "Monthly Subscriptions (SaaS)",
                bus1Desc: "Paid tiers for advanced features and higher project storage.",
                bus2Title: "Consulting Services",
                bus2Desc: "Connecting content creators with experts to grow their business for a commission.",
                footerText: "Developed exclusively for Next Founders Hackathon | Designed & Built by MK Team"
            }
        };

        const ideasDatabase = {
            ar: {
                code: [
                    "تطوير منصة ويب تفاعلية لربط المبرمجين المبتدئين بالمشاريع المصغرة.",
                    "بناء أداة سحابية لتوليد وتنسيق أكواد الـ CSS بشكل أوتوماتيكي وسريع.",
                    "إنشاء نظام لوحة تحكم (Dashboard) مفتوح المصدر لإدارة مهام مطوري الـ Front-End.",
                    "تطبيق ويب لفحص الثغرات الأمنية البسيطة في مواقع الويب الناشئة.",
                    "منصة لاختبار سرعة وأداء صفحات الويب مع تقديم تقارير تحسين تلقائية."
                ],
                editing: [
                    "نظام تتبع وإدارة أرباح الإعلانات والرعايات الخاصة بالقناة في لوحة تحكم واحدة.",
                    "تطوير أداة ويب لجدولة ومراجعة الفيديوهات القصيرة (Shorts/Reels) قبل نشرها.",
                    "منصة تواصل تربط أصحاب القنوات بمحرري الفيديو والمونيتيرز الموهوبين.",
                    "أداة ويب لاقتراح العناوين والوصف المناسب لفيديوهات اليوتيوب بناءً على المحتوى.",
                    "نظام تخزين سحابي مصغر مخصص لمشاركة ملفات الفيديو الخام الضخمة بين الفريق."
                ],
                design: [
                    "أداة توليد أنظمة ألوان متناسقة (Color Palettes) بضغطة زر واحدة.",
                    "إنشاء مكتبة مجانية على الويب لتصاميم الصور المصغرة (Thumbnails) القابلة للتعديل.",
                    "منصة لتقييم تصاميم واجهات المستخدم (UI/UX) وتقديم ملاحظات فورية.",
                    "أداة لدمج وتحويل صيغ الصور وتغيير مقاساتها لمنصات السوشيال ميديا.",
                    "معرض إلكتروني لتبادل الأفكار وإلهام التصميم (Inspiration Gallery) للمصممين."
                ],
                marketing: [
                    "منصة لتقديم استشارات تسويقية سريعة ومباشرة عبر المحادثات.",
                    "تطوير أداة ذكية لكتابة وتوليد العناوين الجذابة (SEO & Copywriting) للفيديوهات والمقالات.",
                    "إنشاء نظام تحليل متقدم لمتابعة نمو المشتركين والتفاعل على منصات السوشيال ميديا.",
                    "منصة إعلانية مصغرة تساعد أصحاب المشاريع الصغيرة في إطلاق حملاتهم الرقمية.",
                    "أداة لجدولة النشر التلقائي على منصات متعددة في نفس اللحظة."
                ]
            },
            en: {
                code: [
                    "Develop an interactive web platform connecting beginner programmers with micro-projects.",
                    "Build a cloud tool to automatically generate and format CSS code quickly.",
                    "Create an open-source Dashboard to manage tasks for Front-End developers.",
                    "A web application to scan basic security vulnerabilities in startup websites.",
                    "A platform to test website speed and performance with automated optimization reports."
                ],
                editing: [
                    "A unified dashboard to track and manage ad revenues and channel sponsorships.",
                    "Develop a web tool to schedule and review short-form videos (Shorts/Reels) before posting.",
                    "A networking platform connecting channel owners with talented video editors.",
                    "A web tool to generate optimized titles and descriptions for YouTube videos based on content.",
                    "A dedicated micro cloud storage system for sharing huge raw video files among the team."
                ],
                design: [
                    "A tool to generate harmonious color palettes with a single click.",
                    "Create a free web library of customizable thumbnail designs.",
                    "A platform to evaluate UI/UX designs and provide instant feedback.",
                    "A web tool to merge, convert image formats, and resize for social media platforms.",
                    "An inspiration gallery website for designers to share creative ideas."
                ],
                marketing: [
                    "A platform providing fast, direct marketing consultations via chat.",
                    "Develop a smart tool to write and generate catchy SEO titles and video copywriting.",
                    "Create an advanced analytics system to monitor subscriber growth and social engagement.",
                    "A micro advertising platform helping small business owners launch digital campaigns.",
                    "A tool to schedule automated publishing across multiple platforms simultaneously."
                ]
            }
        };

        function toggleLanguage() {
            currentLang = currentLang === 'ar' ? 'en' : 'ar';
            
            const htmlRoot = document.getElementById('htmlRoot');
            if (currentLang === 'en') {
                htmlRoot.setAttribute('lang', 'en');
                htmlRoot.setAttribute('dir', 'ltr');
            } else {
                htmlRoot.setAttribute('lang', 'ar');
                htmlRoot.setAttribute('dir', 'rtl');
            }

            const t = translations[currentLang];
            document.getElementById('welcomeBadge').innerText = t.welcomeBadge;
            document.getElementById('navFeatures').innerText = t.navFeatures;
            document.getElementById('navTool').innerText = t.navTool;
            document.getElementById('navBusiness').innerText = t.navBusiness;
            document.getElementById('navCta').innerText = t.navCta;
            document.getElementById('langSwitchBtn').innerText = t.langSwitchBtn;
            document.getElementById('heroTitle').innerText = t.heroTitle;
            document.getElementById('heroDesc').innerText = t.heroDesc;
            document.getElementById('heroBtn1').innerText = t.heroBtn1;
            document.getElementById('heroBtn2').innerText = t.heroBtn2;
            document.getElementById('featuresHeading').innerText = t.featuresHeading;
            document.getElementById('feat1Title').innerText = t.feat1Title;
            document.getElementById('feat1Desc').innerText = t.feat1Desc;
            document.getElementById('feat2Title').innerText = t.feat2Title;
            document.getElementById('feat2Desc').innerText = t.feat2Desc;
            document.getElementById('feat3Title').innerText = t.feat3Title;
            document.getElementById('feat3Desc').innerText = t.feat3Desc;
            document.getElementById('toolHeading').innerText = t.toolHeading;
            document.getElementById('toolSub').innerText = t.toolSub;
            document.getElementById('btnCode').innerText = t.btnCode;
            document.getElementById('btnEditing').innerText = t.btnEditing;
            document.getElementById('btnDesign').innerText = t.btnDesign;
            document.getElementById('btnMarketing').innerText = t.btnMarketing;
            document.getElementById('ideaResult').innerText = t.defaultResult;
            document.getElementById('savedHeading').innerText = t.savedHeading;
            document.getElementById('busHeading').innerText = t.busHeading;
            document.getElementById('bus1Title').innerText = t.bus1Title;
            document.getElementById('bus1Desc').innerText = t.bus1Desc;
            document.getElementById('bus2Title').innerText = t.bus2Title;
            document.getElementById('bus2Desc').innerText = t.bus2Desc;
            document.getElementById('footerText').innerText = t.footerText;
            
            renderSavedIdeas();
        }

        function showIdea(category) {
            const resultBox = document.getElementById('ideaResult');
            
            // إظهار تأثير التحميل (Loading Spinner)
            const loadingText = currentLang === 'ar' ? 'جاري توليد الفكرة بالذكاء الاصطناعي...' : 'Generating idea with AI...';
            resultBox.innerHTML = `<div style="text-align:center; padding: 20px;"><div class="spinner"></div><p style="margin-top:10px; color:#38bdf8;">${loadingText}</p></div>`;

            setTimeout(() => {
                const ideasList = ideasDatabase[currentLang][category];
                const randomIdea = ideasList[Math.floor(Math.random() * ideasList.length)];
                currentGeneratedIdea = randomIdea;
                
                const categoryNames = {
                    ar: {
                        code: "البرمجة والتطوير (Code)",
                        editing: "المونتاج وصناعة المحتوى (Editing)",
                        design: "التصميم والجرافيك (Design)",
                        marketing: "التسويق الرقمي (Marketing)"
                    },
                    en: {
                        code: "Coding & Development",
                        editing: "Video Editing & Content",
                        design: "UI/UX & Design",
                        marketing: "Digital Marketing"
                    }
                };

                const labelText = currentLang === 'ar' ? "فكرة مقترحة في مجال" : "Suggested idea in";
                const copyText = currentLang === 'ar' ? "📋 نسخ النص" : "📋 Copy";
                const saveText = currentLang === 'ar' ? "⭐ حفظ الفكرة" : "⭐ Save Idea";

                resultBox.innerHTML = `
                    <strong style="color: #38bdf8;">${labelText} ${categoryNames[currentLang][category]}:</strong><br><br>✨ ${randomIdea}
                    <div class="result-actions">
                        <button class="action-tool-btn" onclick="copyIdea()">${copyText}</button>
                        <button class="action-tool-btn" onclick="saveIdea()">${saveText}</button>
                    </div>
                `;
            }, 500);
        }

        function copyIdea() {
            if (!currentGeneratedIdea) return;
            navigator.clipboard.writeText(currentGeneratedIdea);
            const msg = currentLang === 'ar' ? '✨ تم نسخ الفكرة بنجاح!' : '✨ Idea copied successfully!';
            alert(msg);
        }

        function saveIdea() {
            if (!currentGeneratedIdea) return;
            if (!savedIdeas.includes(currentGeneratedIdea)) {
                savedIdeas.push(currentGeneratedIdea);
                localStorage.setItem('mk_saved_ideas', JSON.stringify(savedIdeas));
                renderSavedIdeas();
                const msg = currentLang === 'ar' ? '📌 تم حفظ الفكرة في المفضلة!' : '📌 Idea saved to favorites!';
                alert(msg);
            } else {
                const msg = currentLang === 'ar' ? '⚠️ هذه الفكرة محفوظة مسبقاً!' : '⚠️ Idea is already saved!';
                alert(msg);
            }
        }

        function removeSavedIdea(index) {
            savedIdeas.splice(index, 1);
            localStorage.setItem('mk_saved_ideas', JSON.stringify(savedIdeas));
            renderSavedIdeas();
        }

        function renderSavedIdeas() {
            const listEl = document.getElementById('savedList');
            if (savedIdeas.length === 0) {
                const noText = currentLang === 'ar' ? "لا توجد أفكار محفوظة حالياً..." : "No saved ideas yet...";
                listEl.innerHTML = `<li style="color: #64748b; text-align: center; display: block;">${noText}</li>`;
                return;
            }

            listEl.innerHTML = '';
            savedIdeas.forEach((idea, index) => {
                listEl.innerHTML += `
                    <li>
                        <span style="max-width: 85%; overflow: hidden; text-overflow: ellipsis; white-space: nowrap;">✨ ${idea}</span>
                        <button onclick="removeSavedIdea(${index})" title="حذف"><i class="fa-solid fa-trash"></i></button>
                    </li>
                `;
            });
        }

        // تشغيل تحميل الأفكار المحفوظة عند فتح الصفحة
        renderSavedIdeas();
    </script>
</body>
</html> 
