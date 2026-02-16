# noosphere
Awaken the global mindstorm. Join visionaries—students, economists, scientists, rebels—from every corner to dissect world's wounds: crumbling climates, social rifts, tech tempests. Bare your truths, clash perspectives, craft audacious fixes. No echo chambers; pure, unfiltered alchemy of ideas into action. Together, we don't debate—we transform.
<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>StudentThinkers - Free Global Platform</title>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-auth-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore-compat.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Devanagari:wght@400;600;700&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        
        :root {
            --primary: #6366f1;
            --primary-dark: #4f46e5;
            --secondary: #ec4899;
            --bg: #0f172a;
            --surface: #1e293b;
            --text: #f1f5f9;
            --text-muted: #94a3b8;
        }
        
        body {
            font-family: 'Inter', 'Noto Sans Devanagari', sans-serif;
            background: var(--bg);
            color: var(--text);
            line-height: 1.6;
        }
        
        .container { max-width: 1200px; margin: 0 auto; padding: 0 20px; }
        
        /* Header */
        header {
            background: rgba(30, 41, 59, 0.95);
            backdrop-filter: blur(10px);
            position: sticky;
            top: 0;
            z-index: 100;
            border-bottom: 1px solid #334155;
        }
        
        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem 0;
        }
        
        .logo {
            font-size: 1.5rem;
            font-weight: 700;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }
        
        /* Buttons */
        .btn {
            padding: 0.625rem 1.25rem;
            border-radius: 0.5rem;
            border: none;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s;
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            font-size: 0.875rem;
        }
        
        .btn-primary {
            background: var(--primary);
            color: white;
        }
        
        .btn-primary:hover {
            background: var(--primary-dark);
            transform: translateY(-1px);
        }
        
        .btn-outline {
            background: transparent;
            border: 1px solid #475569;
            color: var(--text);
        }
        
        .btn-outline:hover {
            border-color: var(--primary);
            color: var(--primary);
        }
        
        .btn-ghost {
            background: transparent;
            color: var(--text-muted);
        }
        
        .btn-ghost:hover {
            color: var(--text);
        }
        
        /* Hero */
        .hero {
            padding: 4rem 0;
            text-align: center;
            background: radial-gradient(ellipse at top, rgba(99, 102, 241, 0.15), transparent);
        }
        
        .hero h1 {
            font-size: 3rem;
            margin-bottom: 1rem;
            line-height: 1.2;
        }
        
        .hero p {
            color: var(--text-muted);
            font-size: 1.125rem;
            max-width: 600px;
            margin: 0 auto 2rem;
        }
        
        .cta-group {
            display: flex;
            gap: 1rem;
            justify-content: center;
            flex-wrap: wrap;
        }
        
        /* Features Grid */
        .features {
            padding: 4rem 0;
        }
        
        .section-title {
            text-align: center;
            font-size: 2rem;
            margin-bottom: 3rem;
        }
        
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 1.5rem;
        }
        
        .card {
            background: var(--surface);
            border-radius: 1rem;
            padding: 1.5rem;
            border: 1px solid #334155;
            transition: all 0.3s;
        }
        
        .card:hover {
            border-color: var(--primary);
            transform: translateY(-2px);
        }
        
        .card-icon {
            width: 48px;
            height: 48px;
            background: rgba(99, 102, 241, 0.1);
            border-radius: 0.75rem;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--primary);
            font-size: 1.25rem;
            margin-bottom: 1rem;
        }
        
        .card h3 {
            margin-bottom: 0.5rem;
            font-size: 1.125rem;
        }
        
        .card p {
            color: var(--text-muted);
            font-size: 0.875rem;
        }
        
        /* Auth Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            padding: 1rem;
        }
        
        .modal.active { display: flex; }
        
        .modal-content {
            background: var(--surface);
            border-radius: 1rem;
            padding: 2rem;
            width: 100%;
            max-width: 400px;
            border: 1px solid #334155;
        }
        
        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
        }
        
        .modal-header h2 {
            font-size: 1.5rem;
        }
        
        .close-btn {
            background: none;
            border: none;
            color: var(--text-muted);
            font-size: 1.5rem;
            cursor: pointer;
        }
        
        .form-group {
            margin-bottom: 1rem;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            font-size: 0.875rem;
            font-weight: 500;
        }
        
        .form-group input, .form-group select {
            width: 100%;
            padding: 0.75rem;
            border-radius: 0.5rem;
            border: 1px solid #475569;
            background: var(--bg);
            color: var(--text);
            font-size: 0.875rem;
        }
        
        .form-group input:focus {
            outline: none;
            border-color: var(--primary);
        }
        
        .divider {
            text-align: center;
            margin: 1.5rem 0;
            position: relative;
            color: var(--text-muted);
            font-size: 0.875rem;
        }
        
        .divider::before, .divider::after {
            content: '';
            position: absolute;
            top: 50%;
            width: 45%;
            height: 1px;
            background: #334155;
        }
        
        .divider::before { left: 0; }
        .divider::after { right: 0; }
        
        /* Dashboard */
        .dashboard {
            display: none;
            padding: 2rem 0;
        }
        
        .dashboard.active { display: block; }
        
        .dashboard-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 2rem;
        }
        
        .user-info {
            display: flex;
            align-items: center;
            gap: 1rem;
        }
        
        .avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 600;
        }
        
        /* Post Creator */
        .post-creator {
            background: var(--surface);
            border-radius: 1rem;
            padding: 1.5rem;
            margin-bottom: 2rem;
            border: 1px solid #334155;
        }
        
        .post-input {
            width: 100%;
            background: var(--bg);
            border: 1px solid #475569;
            border-radius: 0.75rem;
            padding: 1rem;
            color: var(--text);
            font-family: inherit;
            resize: vertical;
            min-height: 120px;
            margin-bottom: 1rem;
        }
        
        .post-input:focus {
            outline: none;
            border-color: var(--primary);
        }
        
        .post-actions {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .post-tools {
            display: flex;
            gap: 0.5rem;
        }
        
        .tool-btn {
            background: transparent;
            border: none;
            color: var(--text-muted);
            cursor: pointer;
            padding: 0.5rem;
            border-radius: 0.5rem;
            transition: all 0.3s;
        }
        
        .tool-btn:hover {
            color: var(--primary);
            background: rgba(99, 102, 241, 0.1);
        }
        
        /* Posts Feed */
        .posts-container {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }
        
        .post {
            background: var(--surface);
            border-radius: 1rem;
            padding: 1.5rem;
            border: 1px solid #334155;
            animation: slideIn 0.3s ease;
        }
        
        @keyframes slideIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .post-header {
            display: flex;
            justify-content: space-between;
            align-items: start;
            margin-bottom: 1rem;
        }
        
        .post-author {
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }
        
        .post-meta {
            color: var(--text-muted);
            font-size: 0.875rem;
        }
        
        .post-content {
            margin-bottom: 1rem;
            line-height: 1.6;
        }
        
        .post-tags {
            display: flex;
            gap: 0.5rem;
            margin-bottom: 1rem;
            flex-wrap: wrap;
        }
        
        .tag {
            background: rgba(99, 102, 241, 0.1);
            color: var(--primary);
            padding: 0.25rem 0.75rem;
            border-radius: 9999px;
            font-size: 0.75rem;
            font-weight: 500;
        }
        
        .post-footer {
            display: flex;
            gap: 1.5rem;
            padding-top: 1rem;
            border-top: 1px solid #334155;
        }
        
        .action-btn {
            background: transparent;
            border: none;
            color: var(--text-muted);
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            font-size: 0.875rem;
            transition: color 0.3s;
        }
        
        .action-btn:hover {
            color: var(--primary);
        }
        
        .action-btn.liked {
            color: var(--secondary);
        }
        
        /* Toast */
        .toast {
            position: fixed;
            bottom: 2rem;
            right: 2rem;
            background: var(--surface);
            border: 1px solid #334155;
            padding: 1rem 1.5rem;
            border-radius: 0.75rem;
            display: none;
            align-items: center;
            gap: 0.75rem;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            z-index: 2000;
            animation: slideUp 0.3s;
        }
        
        @keyframes slideUp {
            from { transform: translateY(100px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }
        
        .toast.show { display: flex; }
        
        .toast.success { border-left: 4px solid #10b981; }
        .toast.error { border-left: 4px solid #ef4444; }
        
        /* Loading */
        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(255,255,255,.3);
            border-radius: 50%;
            border-top-color: white;
            animation: spin 1s linear infinite;
        }
        
        @keyframes spin { to { transform: rotate(360deg); } }
        
        /* Responsive */
        @media (max-width: 768px) {
            .hero h1 { font-size: 2rem; }
            .grid { grid-template-columns: 1fr; }
            .post-actions { flex-direction: column; gap: 1rem; align-items: stretch; }
        }
        
        /* Hidden */
        .hidden { display: none !important; }
    </style>
</head>
<body>

    <!-- Header -->
    <header>
        <div class="container">
            <div class="header-content">
                <div class="logo">
                    <i class="fas fa-graduation-cap"></i>
                    StudentThinkers
                </div>
                <div id="authButtons">
                    <button class="btn btn-outline" onclick="showModal('login')">लॉग इन</button>
                    <button class="btn btn-primary" onclick="showModal('signup')">मुफ्त जुड़ें</button>
                </div>
                <div id="userMenu" class="hidden">
                    <button class="btn btn-ghost" onclick="logout()">
                        <i class="fas fa-sign-out-alt"></i> लॉग आउट
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- Landing Page -->
    <div id="landingPage">
        <section class="hero">
            <div class="container">
                <h1>विद्यार्थियों और विचारकों का <br>ग्लोबल नेटवर्क</h1>
                <p>दुनिया भर के छात्रों से जुड़ें, आर्थिक, सामाजिक और शैक्षिक विषयों पर चर्चा करें, अपने विचार साझा करें। 100% मुफ्त!</p>
                <div class="cta-group">
                    <button class="btn btn-primary btn-lg" onclick="showModal('signup')">
                        <i class="fas fa-rocket"></i> अभी शुरू करें
                    </button>
                    <button class="btn btn-outline" onclick="showModal('login')">
                        <i class="fas fa-play"></i> डेमो देखें
                    </button>
                </div>
            </div>
        </section>

        <section class="features">
            <div class="container">
                <h2 class="section-title">आपको क्या मिलेगा</h2>
                <div class="grid">
                    <div class="card">
                        <div class="card-icon"><i class="fas fa-globe"></i></div>
                        <h3>ग्लोबल कनेक्शन</h3>
                        <p>120+ देशों के छात्रों और विचारकों से सीधे जुड़ें। भाषा की कोई बाधा नहीं।</p>
                    </div>
                    <div class="card">
                        <div class="card-icon"><i class="fas fa-comments"></i></div>
                        <h3>विचार-विमर्श</h3>
                        <p>अर्थशास्त्र, राजनीति, दर्शन पर गहन चर्चाएँ। अपने विचार रखें।</p>
                    </div>
                    <div class="card">
                        <div class="card-icon"><i class="fas fa-shield-alt"></i></div>
                        <h3>सुरक्षित माहौल</h3>
                        <p>कोई ट्रोलिंग नहीं, कोई घृणा नहीं। केवल सम्मानजनक बातचीत।</p>
                    </div>
                    <div class="card">
                        <div class="card-icon"><i class="fas fa-mobile-alt"></i></div>
                        <h3>हर जगह उपलब्ध</h3>
                        <p>मोबाइल, टैबलेट, लैपटॉप - कहीं से भी एक्सेस करें।</p>
                    </div>
                    <div class="card">
                        <div class="card-icon"><i class="fas fa-language"></i></div>
                        <h3>मल्टी-लैंग्वेज</h3>
                        <p>हिंदी, English, Spanish, Arabic और अन्य भाषाओं में।</p>
                    </div>
                    <div class="card">
                        <div class="card-icon"><i class="fas fa-wallet"></i></div>
                        <h3>100% मुफ्त</h3>
                        <p>कोई शुल्क नहीं, कोई विज्ञापन नहीं, कोई छिपी लागत नहीं।</p>
                    </div>
                </div>
            </div>
        </section>
    </div>

    <!-- Dashboard -->
    <div id="dashboard" class="dashboard">
        <div class="container">
            <div class="dashboard-header">
                <div class="user-info">
                    <div class="avatar" id="userAvatar">U</div>
                    <div>
                        <div style="font-weight: 600;" id="userName">User</div>
                        <div style="font-size: 0.875rem; color: var(--text-muted);">ऑनलाइन</div>
                    </div>
                </div>
                <div style="display: flex; gap: 0.5rem;">
                    <select class="btn btn-outline" style="padding: 0.5rem;" onchange="changeLang(this.value)">
                        <option value="hi">🇮🇳 हिंदी</option>
                        <option value="en">🇬🇧 English</option>
                        <option value="es">🇪🇸 Español</option>
                        <option value="ar">🇸🇦 العربية</option>
                    </select>
                </div>
            </div>

            <div class="post-creator">
                <textarea class="post-input" id="postContent" placeholder="अपने विचार साझा करें... क्या चल रहा है आपके दिमाग में?"></textarea>
                <div class="post-actions">
                    <div class="post-tools">
                        <button class="tool-btn" title="Topic"><i class="fas fa-hashtag"></i></button>
                        <button class="tool-btn" title="Image"><i class="fas fa-image"></i></button>
                        <button class="tool-btn" title="Poll"><i class="fas fa-poll"></i></button>
                    </div>
                    <button class="btn btn-primary" onclick="createPost()">
                        <i class="fas fa-paper-plane"></i> पोस्ट करें
                    </button>
                </div>
            </div>

            <div class="posts-container" id="postsContainer">
                <!-- Posts will load here -->
            </div>
        </div>
    </div>

    <!-- Auth Modal -->
    <div class="modal" id="authModal" onclick="closeModal(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2 id="modalTitle">जुड़ें</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            
            <form id="authForm" onsubmit="handleAuth(event)">
                <div class="form-group">
                    <label>ईमेल</label>
                    <input type="email" id="email" required placeholder="your@email.com">
                </div>
                <div class="form-group">
                    <label>पासवर्ड</label>
                    <input type="password" id="password" required placeholder="••••••••">
                </div>
                <div class="form-group" id="nameGroup" style="display: none;">
                    <label>आपका नाम</label>
                    <input type="text" id="displayName" placeholder="राहुल शर्मा">
                </div>
                <button type="submit" class="btn btn-primary" style="width: 100%;" id="submitBtn">
                    जारी रखें
                </button>
            </form>

            <div class="divider">या</div>

            <button class="btn btn-outline" style="width: 100%;" onclick="googleLogin()">
                <i class="fab fa-google"></i> Google से जुड़ें
            </button>

            <p style="text-align: center; margin-top: 1rem; font-size: 0.875rem; color: var(--text-muted);">
                <span id="switchText">पहले से अकाउंट है?</span>
                <a href="#" onclick="toggleAuthMode()" style="color: var(--primary); text-decoration: none;">
                    <span id="switchLink">लॉग इन करें</span>
                </a>
            </p>
        </div>
    </div>

    <!-- Toast -->
    <div class="toast" id="toast">
        <i class="fas fa-check-circle"></i>
        <span id="toastMsg">Success!</span>
    </div>

    <script>
        // Firebase Configuration - Aapko yeh apna banana hoga
        const firebaseConfig = {
            apiKey: "YOUR_API_KEY",
            authDomain: "YOUR_PROJECT.firebaseapp.com",
            projectId: "YOUR_PROJECT",
            storageBucket: "YOUR_PROJECT.appspot.com",
            messagingSenderId: "123456789",
            appId: "YOUR_APP_ID"
        };

        // Initialize Firebase (jab aap apna config dalenge)
        // firebase.initializeApp(firebaseConfig);
        // const auth = firebase.auth();
        // const db = firebase.firestore();

        let currentUser = null;
        let authMode = 'login';

        // Demo Data (jab tak real database nahi lagti)
        const demoPosts = [
            {
                id: 1,
                author: "Priya Patel",
                country: "🇮🇳",
                content: "भारत की अर्थव्यवस्था में startups का बढ़ता प्रभाव। क्या यह sustainable है?",
                tags: ["#economy", "#startup", "#india"],
                likes: 45,
                comments: 12,
                time: "2 घंटे पहले"
            },
            {
                id: 2,
                author: "John Smith",
                country: "🇺🇸",
                content: "The future of education is not in classrooms but in communities like this. What do you think?",
                tags: ["#education", "#future", "#community"],
                likes: 89,
                comments: 34,
                time: "5 घंटे पहले"
            },
            {
                id: 3,
                author: "Wei Chen",
                country: "🇨🇳",
                content: "全球化与本地化的平衡。我们需要更多的跨文化对话。",
                tags: ["#globalization", "#culture", "#dialogue"],
                likes: 67,
                comments: 23,
                time: "8 घंटे पहले"
            }
        ];

        function showModal(mode) {
            authMode = mode;
            document.getElementById('authModal').classList.add('active');
            updateModalUI();
        }

        function closeModal(e) {
            if (!e || e.target.id === 'authModal') {
                document.getElementById('authModal').classList.remove('active');
            }
        }

        function toggleAuthMode() {
            authMode = authMode === 'login' ? 'signup' : 'login';
            updateModalUI();
        }

        function updateModalUI() {
            const isLogin = authMode === 'login';
            document.getElementById('modalTitle').textContent = isLogin ? 'लॉग इन' : 'अकाउंट बनाएं';
            document.getElementById('submitBtn').innerHTML = isLogin ? 
                '<i class="fas fa-sign-in-alt"></i> लॉग इन' : 
                '<i class="fas fa-user-plus"></i> साइन अप';
            document.getElementById('nameGroup').style.display = isLogin ? 'none' : 'block';
            document.getElementById('switchText').textContent = isLogin ? 'अकाउंट नहीं है?' : 'पहले से अकाउंट है?';
            document.getElementById('switchLink').textContent = isLogin ? 'साइन अप' : 'लॉग इन';
        }

        function handleAuth(e) {
            e.preventDefault();
            const email = document.getElementById('email').value;
            const password = document.getElementById('password').value;
            const name = document.getElementById('displayName').value || email.split('@')[0];
            
            // Demo login (jab tak Firebase connect nahi hota)
            simulateLogin(name);
        }

        function googleLogin() {
            // Demo Google login
            simulateLogin("Google User");
        }

        function simulateLogin(name) {
            const btn = document.getElementById('submitBtn');
            btn.innerHTML = '<div class="loading"></div>';
            
            setTimeout(() => {
                currentUser = { name: name, email: "user@example.com" };
                showToast('स्वागत है, ' + name + '!', 'success');
                closeModal();
                showDashboard();
                btn.innerHTML = authMode === 'login' ? 'लॉग इन' : 'साइन अप';
            }, 1500);
        }

        function showDashboard() {
            document.getElementById('landingPage').style.display = 'none';
            document.getElementById('dashboard').classList.add('active');
            document.getElementById('authButtons').classList.add('hidden');
            document.getElementById('userMenu').classList.remove('hidden');
            document.getElementById('userName').textContent = currentUser.name;
            document.getElementById('userAvatar').textContent = currentUser.name[0].toUpperCase();
            
            loadPosts();
        }

        function logout() {
            currentUser = null;
            document.getElementById('landingPage').style.display = 'block';
            document.getElementById('dashboard').classList.remove('active');
            document.getElementById('authButtons').classList.remove('hidden');
            document.getElementById('userMenu').classList.add('hidden');
            showToast('लॉग आउट सफल', 'success');
        }

        function createPost() {
            const content = document.getElementById('postContent').value;
            if (!content.trim()) {
                showToast('कृपया कुछ लिखें', 'error');
                return;
            }

            const newPost = {
                id: Date.now(),
                author: currentUser.name,
                country: "🇮🇳",
                content: content,
                tags: ["#new", "#thoughts"],
                likes: 0,
                comments: 0,
                time: "अभी"
            };

            demoPosts.unshift(newPost);
            document.getElementById('postContent').value = '';
            loadPosts();
            showToast('पोस्ट सफलतापूर्वक प्रकाशित!', 'success');
        }

        function loadPosts() {
            const container = document.getElementById('postsContainer');
            container.innerHTML = demoPosts.map(post => `
                <div class="post">
                    <div class="post-header">
                        <div class="post-author">
                            <div class="avatar">${post.author[0]}</div>
                            <div>
                                <div style="font-weight: 600;">${post.author} ${post.country}</div>
                                <div class="post-meta">${post.time}</div>
                            </div>
                        </div>
                    </div>
                    <div class="post-content">${post.content}</div>
                    <div class="post-tags">
                        ${post.tags.map(tag => `<span class="tag">${tag}</span>`).join('')}
                    </div>
                    <div class="post-footer">
                        <button class="action-btn" onclick="toggleLike(this, ${post.id})">
                            <i class="far fa-heart"></i>
                            <span>${post.likes}</span>
                        </button>
                        <button class="action-btn">
                            <i class="far fa-comment"></i>
                            <span>${post.comments}</span>
                        </button>
                        <button class="action-btn">
                            <i class="fas fa-share"></i>
                            <span>शेयर</span>
                        </button>
                    </div>
                </div>
            `).join('');
        }

        function toggleLike(btn, postId) {
            btn.classList.toggle('liked');
            const icon = btn.querySelector('i');
            const count = btn.querySelector('span');
            let num = parseInt(count.textContent);
            
            if (btn.classList.contains('liked')) {
                icon.classList.remove('far');
                icon.classList.add('fas');
                count.textContent = num + 1;
            } else {
                icon.classList.remove('fas');
                icon.classList.add('far');
                count.textContent = num - 1;
            }
        }

        function changeLang(lang) {
            showToast('भाषा बदली गई: ' + lang, 'success');
        }

        function showToast(msg, type = 'success') {
            const toast = document.getElementById('toast');
            document.getElementById('toastMsg').textContent = msg;
            toast.className = 'toast show ' + type;
            
            setTimeout(() => {
                toast.classList.remove('show');
            }, 3000);
        }

        // Initialize
        document.addEventListener('DOMContentLoaded', () => {
            // Auto-load demo posts on landing for preview
            console.log('StudentThinkers loaded!');
        });
    </script>
</body>
</html>
