<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Evil Bar - إيفل بار | Luxury Cafe & Bar</title>
    
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.rtl.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;900&family=Playfair+Display:wght@700;900&display=swap" rel="stylesheet">

    <style>
        :root {
            --bg: #050505; --bg2: #0d0d0d; --bg3: #1a1a1a;
            --gold: #D4AF37; --gold-light: #FFD700; --gold-dark: #B8960C;
            --brown: #4E342E; --white: #ffffff; --gray: #999999;
            --red: #e74c3c; --green: #2ecc71; --blue: #4285f4;
            --glass: rgba(20,20,20,0.8); --glass-border: rgba(212,175,55,0.2);
            --shadow-gold: 0 0 30px rgba(212,175,55,0.3);
            --shadow-gold-big: 0 0 60px rgba(212,175,55,0.5);
            --visa-blue: #1a1f71; --visa-gold: #f7b600;
            --vodafone-red: #e60000;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }
        html { scroll-behavior: smooth; }
        
        body {
            background: var(--bg); color: var(--white);
            font-family: 'Cairo', 'Segoe UI', Tahoma, sans-serif;
            overflow-x: hidden; min-height: 100vh;
        }

        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: var(--bg); }
        ::-webkit-scrollbar-thumb { background: var(--gold); border-radius: 10px; }

        /* Particles */
        #particlesCanvas { position: fixed; top: 0; left: 0; width: 100%; height: 100%; z-index: 0; pointer-events: none; }

        /* Preloader */
        #preloader {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: var(--bg); z-index: 99999;
            display: flex; align-items: center; justify-content: center;
            transition: opacity 0.5s, visibility 0.5s;
        }
        #preloader.hide { opacity: 0; visibility: hidden; }
        .preloader-logo {
            font-family: 'Playfair Display', serif; font-size: 50px; font-weight: 900;
            color: var(--gold); letter-spacing: 8px; animation: pulse 1.5s infinite;
            text-shadow: 0 0 30px rgba(212,175,55,0.6);
        }
        @keyframes pulse { 0%,100%{opacity:1;transform:scale(1);} 50%{opacity:0.7;transform:scale(1.05);} }

        /* Glass */
        .glass {
            background: var(--glass); backdrop-filter: blur(20px);
            border: 1px solid var(--glass-border); border-radius: 20px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.3);
        }

        /* Auth */
        .auth-wrapper { min-height: 100vh; display: flex; align-items: center; justify-content: center; position: relative; z-index: 1; padding: 20px; }
        .auth-card { width: 100%; max-width: 480px; padding: 35px 30px; animation: slideUp 0.6s ease; }
        @keyframes slideUp { from{opacity:0;transform:translateY(30px);} to{opacity:1;transform:translateY(0);} }

        .auth-logo h1 {
            font-family: 'Playfair Display', serif; font-size: 42px; font-weight: 900;
            background: linear-gradient(135deg, var(--gold-dark), var(--gold), var(--gold-light));
            -webkit-background-clip: text; -webkit-text-fill-color: transparent; letter-spacing: 6px;
        }

        .auth-tabs { display: flex; gap: 8px; margin-bottom: 25px; background: rgba(255,255,255,0.03); border-radius: 15px; padding: 5px; }
        .auth-tab {
            flex: 1; padding: 12px; text-align: center; border: none; background: transparent;
            color: var(--gray); border-radius: 12px; cursor: pointer; font-size: 14px;
            transition: all 0.3s; font-weight: 600;
        }
        .auth-tab.active { background: linear-gradient(135deg, var(--gold-dark), var(--gold)); color: #000; font-weight: 700; box-shadow: var(--shadow-gold); }

        .form-group { margin-bottom: 18px; }
        .form-group label { display: block; margin-bottom: 6px; color: var(--gray); font-size: 13px; font-weight: 600; }
        .form-input {
            width: 100%; padding: 14px 18px; background: rgba(255,255,255,0.04);
            border: 1px solid rgba(255,255,255,0.12); border-radius: 14px;
            color: var(--white); font-size: 15px; transition: all 0.3s; font-family: 'Cairo', sans-serif;
        }
        .form-input:focus { outline: none; border-color: var(--gold); box-shadow: 0 0 20px rgba(212,175,55,0.15); background: rgba(255,255,255,0.07); }

        .btn {
            width: 100%; padding: 15px; border: none; border-radius: 14px;
            font-size: 16px; font-weight: 700; cursor: pointer; transition: all 0.3s;
            display: flex; align-items: center; justify-content: center; gap: 10px;
            font-family: 'Cairo', sans-serif;
        }
        .btn-gold {
            background: linear-gradient(135deg, #8B7500, var(--gold), #FFE44D);
            color: #000; position: relative; overflow: hidden;
        }
        .btn-gold:hover { transform: translateY(-3px); box-shadow: 0 10px 30px rgba(212,175,55,0.4); }
        .btn-outline { background: transparent; border: 2px solid rgba(255,255,255,0.2); color: var(--white); }
        .btn-outline:hover { border-color: var(--gold); color: var(--gold); }
        .btn-danger { background: var(--red); color: #fff; width: auto; display: inline-flex; }
        .btn-success { background: var(--green); color: #fff; width: auto; display: inline-flex; }
        .btn-google { background: #fff; color: #333; font-weight: 600; }
        .btn-visa { background: linear-gradient(135deg, #1a1f71, #2a3f91); color: #fff; }
        .btn-vodafone { background: linear-gradient(135deg, #e60000, #cc0000); color: #fff; }

        .divider-text {
            text-align: center; margin: 20px 0; position: relative;
            color: var(--gray); font-size: 13px;
        }
        .divider-text::before, .divider-text::after {
            content: ''; position: absolute; top: 50%; width: 35%;
            height: 1px; background: rgba(255,255,255,0.15);
        }
        .divider-text::before { left: 0; } .divider-text::after { right: 0; }

        /* OTP */
        .otp-section { display: none; animation: fadeIn 0.4s ease; }
        .otp-section.show { display: block; }
        .otp-inputs { display: flex; gap: 10px; justify-content: center; margin: 20px 0; }
        .otp-inputs input {
            width: 50px; height: 55px; text-align: center; font-size: 22px; font-weight: 700;
            background: rgba(255,255,255,0.05); border: 2px solid rgba(255,255,255,0.15);
            border-radius: 12px; color: var(--gold);
        }
        .otp-inputs input:focus { outline: none; border-color: var(--gold); box-shadow: 0 0 15px rgba(212,175,55,0.3); }
        @keyframes fadeIn { from{opacity:0;transform:translateY(-10px);} to{opacity:1;transform:translateY(0);} }

        /* Main App */
        #mainApp { display: none; position: relative; z-index: 1; }
        #mainApp.show { display: block; }

        /* Navbar */
        .navbar-evil {
            position: sticky; top: 0; z-index: 1000;
            background: rgba(5,5,5,0.9); backdrop-filter: blur(25px);
            border-bottom: 1px solid rgba(212,175,55,0.15); padding: 12px 0;
        }
        .brand-logo {
            font-family: 'Playfair Display', serif; font-size: 26px; font-weight: 900;
            color: var(--gold); text-decoration: none; letter-spacing: 4px;
        }
        .nav-link-evil {
            color: var(--white) !important; margin: 0 5px; padding: 8px 15px !important;
            border-radius: 10px; cursor: pointer; font-weight: 600; font-size: 14px;
        }
        .nav-link-evil:hover, .nav-link-evil.active { color: var(--gold) !important; background: rgba(212,175,55,0.1); }
        .user-btn {
            background: rgba(212,175,55,0.1); border: 1px solid rgba(212,175,55,0.3);
            color: var(--gold); padding: 8px 16px; border-radius: 50px; cursor: pointer;
            font-weight: 600; font-size: 14px;
        }
        .cart-btn {
            position: relative; background: transparent; border: 1px solid rgba(255,255,255,0.2);
            color: var(--white); padding: 8px 16px; border-radius: 50px; cursor: pointer;
        }
        .cart-badge {
            position: absolute; top: -8px; right: -8px; background: var(--gold);
            color: #000; border-radius: 50%; width: 22px; height: 22px;
            font-size: 11px; display: flex; align-items: center; justify-content: center; font-weight: 900;
        }

        /* Hero */
        .hero-section {
            min-height: 100vh; display: flex; align-items: center; justify-content: center;
            text-align: center; position: relative; padding: 100px 20px;
        }
        .hero-title {
            font-family: 'Playfair Display', serif;
            font-size: clamp(50px, 10vw, 100px); font-weight: 900;
            background: linear-gradient(135deg, #8B7500, var(--gold), #FFE44D, var(--gold));
            background-size: 300% 300%; -webkit-background-clip: text;
            -webkit-text-fill-color: transparent; animation: gradientShift 4s infinite;
            letter-spacing: 10px;
        }
        @keyframes gradientShift { 0%,100%{background-position:0% 50%;} 50%{background-position:100% 50%;} }
        .hero-subtitle { font-size: clamp(16px, 3vw, 22px); color: var(--gray); margin: 20px 0 30px; }
        .hero-btn {
            padding: 16px 35px; border-radius: 50px; font-size: 16px; font-weight: 700;
            cursor: pointer; transition: all 0.4s; text-decoration: none;
            display: inline-flex; align-items: center; gap: 10px; margin: 5px;
        }
        .hero-btn-primary { background: linear-gradient(135deg, #8B7500, var(--gold)); color: #000; border: none; }
        .hero-btn-primary:hover { transform: translateY(-5px); box-shadow: 0 15px 40px rgba(212,175,55,0.5); }
        .hero-btn-outline { background: transparent; border: 2px solid var(--gold); color: var(--gold); }
        .hero-btn-outline:hover { background: var(--gold); color: #000; transform: translateY(-5px); }

        /* Sections */
        .section { padding: 80px 0; position: relative; }
        .section-dark { background: var(--bg2); }
        .section-title { text-align: center; font-size: clamp(28px, 5vw, 42px); font-weight: 900; margin-bottom: 50px; }
        .gold-text { color: var(--gold); }

        /* Product Grid */
        .product-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 25px; }
        .product-card {
            background: rgba(20,20,20,0.8); border: 1px solid rgba(255,255,255,0.08);
            border-radius: 20px; overflow: hidden; transition: all 0.4s;
        }
        .product-card:hover { transform: translateY(-10px); border-color: rgba(212,175,55,0.4); box-shadow: 0 20px 50px rgba(0,0,0,0.5), 0 0 30px rgba(212,175,55,0.15); }
        .product-card-img { height: 240px; overflow: hidden; position: relative; }
        .product-card-img img { width: 100%; height: 100%; object-fit: cover; transition: transform 0.6s; }
        .product-card:hover .product-card-img img { transform: scale(1.12); }
        .product-badge { position: absolute; top: 15px; left: 15px; background: var(--red); color: #fff; padding: 5px 12px; border-radius: 20px; font-size: 12px; font-weight: 700; }
        .product-card-actions { position: absolute; top: 15px; right: 15px; display: flex; flex-direction: column; gap: 8px; opacity: 0; transform: translateX(15px); transition: all 0.3s; }
        .product-card:hover .product-card-actions { opacity: 1; transform: translateX(0); }
        .product-action-btn { width: 38px; height: 38px; border-radius: 50%; border: none; background: rgba(0,0,0,0.7); color: var(--gold); cursor: pointer; transition: all 0.3s; display: flex; align-items: center; justify-content: center; }
        .product-action-btn:hover { background: var(--gold); color: #000; }
        .product-card-body { padding: 20px; }
        .product-card-body h5 { font-size: 18px; margin-bottom: 5px; font-weight: 700; }
        .product-card-body .desc { color: var(--gray); font-size: 13px; margin-bottom: 12px; }
        .price-row { display: flex; align-items: center; gap: 12px; margin-bottom: 10px; }
        .price-old { text-decoration: line-through; color: var(--gray); font-size: 14px; }
        .price-current { color: var(--gold); font-size: 24px; font-weight: 900; }
        .stars { color: var(--gold); margin-bottom: 15px; font-size: 13px; }
        .btn-add-cart { width: 100%; padding: 12px; background: linear-gradient(135deg, #8B7500, var(--gold)); color: #000; border: none; border-radius: 12px; font-weight: 700; cursor: pointer; transition: all 0.3s; }

        /* Payment Modal */
        .payment-modal-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.9); z-index: 3000; display: none;
            align-items: center; justify-content: center; backdrop-filter: blur(10px);
        }
        .payment-modal-overlay.open { display: flex; }
        .payment-modal {
            background: #111; border: 2px solid var(--gold); border-radius: 20px;
            padding: 30px; width: 90%; max-width: 500px; animation: modalIn 0.4s ease;
            max-height: 90vh; overflow-y: auto;
        }
        @keyframes modalIn { from{opacity:0;transform:scale(0.9);} to{opacity:1;transform:scale(1);} }

        .payment-tabs { display: flex; gap: 10px; margin-bottom: 25px; }
        .payment-tab {
            flex: 1; padding: 15px; text-align: center; border: 2px solid rgba(255,255,255,0.1);
            border-radius: 15px; cursor: pointer; transition: all 0.3s; font-weight: 700;
        }
        .payment-tab.active { border-color: var(--gold); background: rgba(212,175,55,0.1); }
        .payment-tab.visa-tab.active { border-color: #1a1f71; background: rgba(26,31,113,0.2); }
        .payment-tab.vodafone-tab.active { border-color: #e60000; background: rgba(230,0,0,0.1); }

        .visa-card-preview {
            background: linear-gradient(135deg, #1a1f71, #2a3f91);
            border-radius: 16px; padding: 25px; margin-bottom: 20px;
            color: #fff; position: relative; overflow: hidden;
        }
        .visa-card-preview::before {
            content: ''; position: absolute; top: -50px; right: -50px;
            width: 150px; height: 150px; background: rgba(255,255,255,0.05); border-radius: 50%;
        }
        .visa-card-preview .chip { font-size: 30px; margin-bottom: 20px; }
        .visa-card-preview .card-number { font-size: 22px; letter-spacing: 4px; margin-bottom: 15px; font-family: monospace; }
        .visa-card-preview .card-info { display: flex; justify-content: space-between; font-size: 13px; }
        .visa-logo { position: absolute; top: 20px; left: 20px; font-size: 40px; font-weight: 900; color: #fff; font-style: italic; }

        .vodafone-info {
            background: linear-gradient(135deg, #e60000, #cc0000);
            border-radius: 16px; padding: 25px; margin-bottom: 20px;
            color: #fff; text-align: center;
        }
        .vodafone-info .vodafone-number {
            font-size: 28px; font-weight: 900; letter-spacing: 3px;
            margin: 15px 0; background: rgba(255,255,255,0.2);
            padding: 15px; border-radius: 10px;
        }
        .copy-btn {
            background: rgba(255,255,255,0.2); border: none; color: #fff;
            padding: 8px 16px; border-radius: 8px; cursor: pointer; font-weight: 700;
        }

        .upload-area {
            border: 2px dashed rgba(212,175,55,0.4); border-radius: 15px;
            padding: 30px; text-align: center; cursor: pointer;
            transition: all 0.3s; margin-bottom: 20px;
        }
        .upload-area:hover { border-color: var(--gold); background: rgba(212,175,55,0.05); }
        .upload-area i { font-size: 40px; color: var(--gold); margin-bottom: 10px; }
        .upload-preview { max-width: 100%; max-height: 200px; border-radius: 10px; margin-top: 10px; display: none; }

        /* Cart Sidebar */
        .cart-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.8); z-index: 2000; display: none; }
        .cart-overlay.open { display: block; }
        .cart-sidebar { position: fixed; top: 0; right: -450px; width: 420px; height: 100%; background: #111; z-index: 2001; transition: right 0.4s; border-left: 1px solid rgba(212,175,55,0.2); padding: 25px; overflow-y: auto; }
        .cart-sidebar.open { right: 0; }

        /* Dashboard */
        .stat-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(250px, 1fr)); gap: 20px; }
        .stat-card { background: rgba(20,20,20,0.8); border: 1px solid rgba(255,255,255,0.1); border-radius: 20px; padding: 30px; text-align: center; transition: all 0.3s; }
        .stat-card:hover { border-color: var(--gold); transform: translateY(-5px); }
        .stat-card h2 { font-size: 40px; font-weight: 900; color: var(--gold); }
        .table-evil { width: 100%; border-collapse: collapse; }
        .table-evil th { background: rgba(212,175,55,0.1); color: var(--gold); padding: 15px; text-align: right; font-weight: 700; }
        .table-evil td { padding: 15px; border-bottom: 1px solid rgba(255,255,255,0.05); }

        /* Toast */
        .toast-container { position: fixed; bottom: 30px; right: 30px; z-index: 9999; display: flex; flex-direction: column; gap: 10px; }
        .toast-item { background: #1a1a1a; border: 1px solid rgba(212,175,55,0.3); padding: 16px 24px; border-radius: 14px; color: #fff; font-weight: 600; animation: toastIn 0.4s ease; box-shadow: 0 10px 30px rgba(0,0,0,0.5); display: flex; align-items: center; gap: 10px; min-width: 300px; }
        .toast-item.success { border-right: 4px solid var(--green); }
        .toast-item.error { border-right: 4px solid var(--red); }
        @keyframes toastIn { from{opacity:0;transform:translateX(100px);} to{opacity:1;transform:translateX(0);} }

        footer { background: #050505; border-top: 1px solid rgba(212,175,55,0.15); padding: 40px 0 20px; text-align: center; }
        footer a { color: var(--gray); text-decoration: none; margin: 0 10px; }
        footer a:hover { color: var(--gold); }

        @media (max-width: 768px) {
            .hero-title { font-size: 40px; }
            .cart-sidebar { width: 100%; right: -100%; }
            .product-grid { grid-template-columns: repeat(auto-fill, minmax(160px, 1fr)); gap: 15px; }
        }
    </style>
</head>
<body>

    <canvas id="particlesCanvas"></canvas>

    <div id="preloader">
        <div class="preloader-logo">EVIL BAR</div>
    </div>

    <div class="toast-container" id="toastContainer"></div>

    <!-- ==================== AUTH PAGE ==================== -->
    <div id="authPage" class="auth-wrapper">
        <div class="auth-card glass">
            <div class="auth-logo" style="text-align:center;margin-bottom:30px;">
                <h1>EVIL BAR</h1>
                <p style="color:var(--gray);font-size:14px;">✦ أفخم كافيه وبار في المدينة ✦</p>
            </div>

            <div class="auth-tabs">
                <button class="auth-tab active" onclick="switchAuthTab('email')"><i class="fas fa-envelope"></i> البريد</button>
                <button class="auth-tab" onclick="switchAuthTab('phone')"><i class="fas fa-mobile-alt"></i> الهاتف</button>
                <button class="auth-tab" onclick="switchAuthTab('google')"><i class="fab fa-google"></i> Google</button>
            </div>

            <div id="tabEmail">
                <div class="form-group"><label>البريد الإلكتروني أو رقم الهاتف</label><input type="text" class="form-input" id="loginEmail" placeholder="example@email.com أو 01xxxxxxxxx" dir="ltr"></div>
                <div class="form-group"><label>كلمة المرور</label><input type="password" class="form-input" id="loginPassword" placeholder="••••••••"></div>
                <button class="btn btn-gold" onclick="loginEmail()"><i class="fas fa-sign-in-alt"></i> تسجيل الدخول</button>
            </div>

            <div id="tabPhone" style="display:none;">
                <div class="form-group"><label>رقم الهاتف</label><input type="tel" class="form-input" id="phoneNumber" placeholder="01xxxxxxxxx" dir="ltr"><small style="color:var(--gray);">سيتم إرسال رمز تحقق</small></div>
                <button class="btn btn-gold" id="btnSendOTP" onclick="sendOTP()"><i class="fas fa-paper-plane"></i> إرسال رمز التحقق</button>
                <div class="otp-section" id="otpSection">
                    <div class="otp-inputs" id="otpInputs">
                        <input type="text" maxlength="1" oninput="otpNext(this)" id="otp1">
                        <input type="text" maxlength="1" oninput="otpNext(this)" id="otp2">
                        <input type="text" maxlength="1" oninput="otpNext(this)" id="otp3">
                        <input type="text" maxlength="1" oninput="otpNext(this)" id="otp4">
                        <input type="text" maxlength="1" oninput="otpNext(this)" id="otp5">
                        <input type="text" maxlength="1" oninput="otpNext(this)" id="otp6">
                    </div>
                    <div class="timer-text" id="timerText" style="text-align:center;color:var(--gold);">02:00</div>
                    <button class="btn btn-gold" onclick="verifyOTP()"><i class="fas fa-check"></i> تأكيد</button>
                    <button class="btn btn-outline mt-2" id="btnResendOTP" onclick="sendOTP()" disabled>إعادة الإرسال</button>
                </div>
            </div>

            <div id="tabGoogle" style="display:none;">
                <p style="text-align:center;color:var(--gray);margin-bottom:20px;">اختر حساب Google</p>
                <button class="btn btn-google" onclick="loginGoogle()"><i class="fab fa-google"></i> Google تسجيل الدخول بـ</button>
            </div>

            <div class="divider-text">أو</div>
            <p style="text-align:center;"><a href="#" onclick="showRegister()" style="color:var(--gold);">إنشاء حساب جديد</a></p>

            <div id="registerSection" style="display:none;">
                <div class="form-group"><label>الاسم</label><input type="text" class="form-input" id="regName"></div>
                <div class="form-group"><label>البريد</label><input type="email" class="form-input" id="regEmail" dir="ltr"></div>
                <div class="form-group"><label>الهاتف</label><input type="tel" class="form-input" id="regPhone" dir="ltr"></div>
                <div class="form-group"><label>كلمة المرور</label><input type="password" class="form-input" id="regPassword"></div>
                <button class="btn btn-gold" onclick="registerUser()">إنشاء حساب</button>
                <button class="btn btn-outline mt-2" onclick="hideRegister()">العودة</button>
            </div>
        </div>
    </div>

    <!-- ==================== MAIN APP ==================== -->
    <div id="mainApp">
        <nav class="navbar-evil" id="navbarEvil">
            <div class="container">
                <div class="d-flex justify-content-between align-items-center flex-wrap">
                    <a class="brand-logo" href="#" onclick="navigateTo('home')">EVIL BAR</a>
                    <div class="d-flex align-items-center gap-2 flex-wrap">
                        <a class="nav-link-evil active" href="#" onclick="navigateTo('home')">الرئيسية</a>
                        <a class="nav-link-evil" href="#" onclick="navigateTo('menu')">المنيو</a>
                        <a class="nav-link-evil" href="#" onclick="navigateTo('drinks')">المشروبات</a>
                        <a class="nav-link-evil" href="#" onclick="navigateTo('food')">المأكولات</a>
                        <a class="nav-link-evil" href="#" onclick="navigateTo('reservation')">حجز</a>
                        <a class="nav-link-evil" href="#" id="dashboardNav" style="display:none;" onclick="navigateTo('dashboard')">لوحة التحكم</a>
                        <button class="cart-btn" onclick="toggleCart()"><i class="fas fa-shopping-cart"></i> <span class="cart-badge" id="cartBadge">0</span></button>
                        <button class="user-btn" onclick="navigateTo('profile')"><i class="fas fa-user"></i> <span id="userNameNav">حسابي</span></button>
                        <button class="btn btn-sm" style="background:var(--red);color:#fff;width:auto;padding:8px 12px;" onclick="logout()">🚪</button>
                    </div>
                </div>
            </div>
        </nav>

        <div id="pageContent"></div>

        <footer>
            <div class="container">
                <h3 style="color:var(--gold);">EVIL BAR</h3>
                <p style="color:var(--gray);">أفخم كافيه وبار | منذ 2020</p>
                <p style="color:var(--gray);margin-top:10px;">&copy; 2024 Evil Bar. Developed by <span style="color:var(--gold);">The Developer</span></p>
            </div>
        </footer>
    </div>

    <!-- Cart Sidebar -->
    <div class="cart-overlay" id="cartOverlay" onclick="toggleCart()"></div>
    <div class="cart-sidebar" id="cartSidebar">
        <div class="d-flex justify-content-between mb-3">
            <h5 style="color:var(--gold);">🛒 السلة</h5>
            <button class="btn-close btn-close-white" onclick="toggleCart()"></button>
        </div>
        <div id="cartItemsList"></div>
        <hr style="border-color:rgba(255,255,255,0.1);">
        <div class="d-flex justify-content-between mb-3">
            <span>الإجمالي:</span>
            <span style="color:var(--gold);font-size:24px;font-weight:900;" id="cartTotal">0 ج.م</span>
        </div>
        <button class="btn btn-gold mb-2" onclick="openPaymentModal()"><i class="fas fa-credit-card"></i> ادفع الآن</button>
        <button class="btn btn-outline mb-2" onclick="clearCart()">تفريغ السلة</button>
    </div>

    <!-- Payment Modal -->
    <div class="payment-modal-overlay" id="paymentModal">
        <div class="payment-modal">
            <div class="d-flex justify-content-between mb-3">
                <h4 style="color:var(--gold);">💳 إتمام الدفع</h4>
                <button class="btn-close btn-close-white" onclick="closePaymentModal()"></button>
            </div>

            <div class="payment-tabs">
                <button class="payment-tab visa-tab active" onclick="switchPaymentTab('visa')">
                    <i class="fab fa-cc-visa"></i> فيزا
                </button>
                <button class="payment-tab vodafone-tab" onclick="switchPaymentTab('vodafone')">
                    <i class="fas fa-mobile-alt"></i> فودافون كاش
                </button>
            </div>

            <!-- Visa Payment -->
            <div id="visaPayment">
                <div class="visa-card-preview">
                    <div class="visa-logo">VISA</div>
                    <div class="chip">💳</div>
                    <div class="card-number" id="cardPreview">•••• •••• •••• ••••</div>
                    <div class="card-info">
                        <span id="namePreview">الاسم على البطاقة</span>
                        <span id="expiryPreview">MM/YY</span>
                    </div>
                </div>
                <div class="form-group"><label>الاسم على البطاقة</label><input type="text" class="form-input" id="cardName" placeholder="مثال: AHMED MOHAMED" oninput="updateCardPreview()"></div>
                <div class="form-group"><label>رقم البطاقة</label><input type="text" class="form-input" id="cardNumber" placeholder="0000 0000 0000 0000" maxlength="19" oninput="formatCardNumber(this);updateCardPreview();"></div>
                <div class="row">
                    <div class="col-6"><div class="form-group"><label>تاريخ الانتهاء</label><input type="text" class="form-input" id="cardExpiry" placeholder="MM/YY" maxlength="5" oninput="formatExpiry(this);updateCardPreview();"></div></div>
                    <div class="col-6"><div class="form-group"><label>رمز CVV</label><input type="text" class="form-input" id="cardCVV" placeholder="***" maxlength="3" type="password"></div></div>
                </div>
                <p style="color:var(--gray);font-size:12px;margin-bottom:15px;">المبلغ: <span id="visaAmount" style="color:var(--gold);font-weight:700;"></span></p>
                <button class="btn btn-visa" onclick="processVisaPayment()"><i class="fab fa-cc-visa"></i> ادفع بالفيزا</button>
            </div>

            <!-- Vodafone Cash Payment -->
            <div id="vodafonePayment" style="display:none;">
                <div class="vodafone-info">
                    <h3><i class="fas fa-mobile-alt"></i> فودافون كاش</h3>
                    <p>حول المبلغ إلى الرقم التالي:</p>
                    <div class="vodafone-number">
                        <span id="vodafoneDisplayNumber">01026966717</span>
                        <button class="copy-btn" onclick="copyVodafoneNumber()"><i class="fas fa-copy"></i> نسخ</button>
                    </div>
                    <p style="font-size:13px;margin-top:10px;">الاسم: <strong>Evil Bar</strong></p>
                </div>
                <div class="upload-area" onclick="document.getElementById('screenshotInput').click()">
                    <i class="fas fa-cloud-upload-alt"></i>
                    <p>اضغط هنا لرفع صورة إشعار التحويل (سكرين شوت)</p>
                    <input type="file" id="screenshotInput" accept="image/*" style="display:none;" onchange="previewScreenshot(event)">
                    <img id="screenshotPreview" class="upload-preview">
                </div>
                <p style="color:var(--gray);font-size:12px;margin-bottom:15px;">المبلغ: <span id="vodafoneAmount" style="color:var(--gold);font-weight:700;"></span></p>
                <button class="btn btn-vodafone" onclick="processVodafonePayment()"><i class="fas fa-paper-plane"></i> إرسال إشعار التحويل</button>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>

    <script>
        // ==================== ADMIN ACCOUNT ====================
        const ADMIN = {
            name: 'المدير',
            phone: '01026966717',
            password: '308191',
            role: 'super_admin'
        };

        // ==================== DATA ====================
        const PRODUCTS = [
            { id:1, name:'إسبرسو', cat:'hot', price:35, disc:null, rating:4.8, img:'https://images.unsplash.com/photo-1510707577719-ae7c14805e3a?w=500&q=80', desc:'إسبرسو إيطالي أصيل' },
            { id:2, name:'كابتشينو', cat:'hot', price:45, disc:38, rating:4.9, img:'https://images.unsplash.com/photo-1534778101976-62847782c213?w=500&q=80', desc:'كابتشينو برغوة كثيفة' },
            { id:3, name:'لاتيه', cat:'hot', price:45, disc:null, rating:4.7, img:'https://images.unsplash.com/photo-1461023058943-07fcbe16d735?w=500&q=80', desc:'لاتيه كريمي ناعم' },
            { id:4, name:'قهوة تركي', cat:'hot', price:30, disc:null, rating:4.9, img:'https://images.unsplash.com/photo-1509042239860-f550ce710b93?w=500&q=80', desc:'قهوة تركية تقليدية' },
            { id:5, name:'آيس لاتيه', cat:'cold', price:50, disc:null, rating:4.6, img:'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=500&q=80', desc:'آيس لاتيه منعش' },
            { id:6, name:'ليمون نعناع', cat:'cold', price:35, disc:30, rating:4.8, img:'https://images.unsplash.com/photo-1621263764928-df1444c5e859?w=500&q=80', desc:'ليمونادة طازجة' },
            { id:7, name:'تشيز كيك', cat:'food', price:60, disc:50, rating:4.9, img:'https://images.unsplash.com/photo-1533134242443-d4fd215305ad?w=500&q=80', desc:'تشيز كيك نيويورك' },
            { id:8, name:'براوني', cat:'food', price:45, disc:null, rating:4.8, img:'https://images.unsplash.com/photo-1606313564200-e75d5e30476c?w=500&q=80', desc:'براوني شوكولاتة' },
            { id:9, name:'موهيتو', cat:'alcohol', price:75, disc:null, rating:4.9, img:'https://images.unsplash.com/photo-1551538827-9c037cb4f32a?w=500&q=80', desc:'موهيتو منعش' },
            { id:10, name:'ويسكي', cat:'alcohol', price:120, disc:100, rating:4.8, img:'https://images.unsplash.com/photo-1527281400683-1aae777175f0?w=500&q=80', desc:'ويسكي 12 سنة' },
        ];

        // ==================== STATE ====================
        let cart = JSON.parse(localStorage.getItem('evilCart') || '[]');
        let currentUser = JSON.parse(localStorage.getItem('evilCurrentUser') || 'null');
        let otpCode = '';
        let otpTimer = null;
        let otpSeconds = 120;
        let screenshotFile = null;

        // ==================== INIT ====================
        window.addEventListener('DOMContentLoaded', () => {
            setTimeout(() => document.getElementById('preloader').classList.add('hide'), 1500);
            
            // Ensure admin exists
            let users = JSON.parse(localStorage.getItem('evilUsers') || '[]');
            if (!users.find(u => u.phone === ADMIN.phone)) {
                users.push(ADMIN);
                localStorage.setItem('evilUsers', JSON.stringify(users));
            }
            
            initParticles();
            AOS.init({ duration: 800, once: false });
            
            if (currentUser) showMainApp();
        });

        function initParticles() {
            const canvas = document.getElementById('particlesCanvas');
            const ctx = canvas.getContext('2d');
            canvas.width = window.innerWidth; canvas.height = window.innerHeight;
            const particles = [];
            for (let i = 0; i < 50; i++) {
                particles.push({
                    x: Math.random()*canvas.width, y: Math.random()*canvas.height,
                    size: Math.random()*2+0.5, sx: (Math.random()-0.5)*0.5, sy: (Math.random()-0.5)*0.5,
                    o: Math.random()*0.5+0.1
                });
            }
            function animate() {
                ctx.clearRect(0,0,canvas.width,canvas.height);
                particles.forEach(p => {
                    p.x+=p.sx; p.y+=p.sy;
                    if(p.x<0)p.x=canvas.width; if(p.x>canvas.width)p.x=0;
                    if(p.y<0)p.y=canvas.height; if(p.y>canvas.height)p.y=0;
                    ctx.beginPath(); ctx.arc(p.x,p.y,p.size,0,Math.PI*2);
                    ctx.fillStyle=`rgba(212,175,55,${p.o})`; ctx.fill();
                });
                requestAnimationFrame(animate);
            }
            animate();
        }

        // ==================== AUTH ====================
        function switchAuthTab(tab) {
            document.querySelectorAll('.auth-tab').forEach(t => t.classList.remove('active'));
            event.target.classList.add('active');
            document.getElementById('tabEmail').style.display = tab==='email'?'block':'none';
            document.getElementById('tabPhone').style.display = tab==='phone'?'block':'none';
            document.getElementById('tabGoogle').style.display = tab==='google'?'block':'none';
        }

        function loginEmail() {
            const email = document.getElementById('loginEmail').value.trim();
            const password = document.getElementById('loginPassword').value.trim();
            if(!email||!password) return showToast('املأ جميع الحقول','error');
            
            const users = JSON.parse(localStorage.getItem('evilUsers')||'[]');
            const user = users.find(u => (u.email===email||u.phone===email) && u.password===password);
            if(user) loginSuccess(user);
            else showToast('بيانات غير صحيحة','error');
        }

        function sendOTP() {
            const phone = document.getElementById('phoneNumber').value.trim();
            if(!phone) return showToast('أدخل رقم الهاتف','error');
            otpCode = String(Math.floor(100000+Math.random()*900000));
            localStorage.setItem('evilOTP', otpCode);
            localStorage.setItem('evilOTPPhone', phone);
            document.getElementById('otpSection').classList.add('show');
            document.getElementById('btnSendOTP').style.display='none';
            document.getElementById('otp1').focus();
            otpSeconds=120; updateTimer();
            if(otpTimer)clearInterval(otpTimer);
            otpTimer=setInterval(()=>{otpSeconds--;updateTimer();if(otpSeconds<=0){clearInterval(otpTimer);document.getElementById('btnResendOTP').disabled=false;document.getElementById('timerText').textContent='انتهت';}},1000);
            document.getElementById('btnResendOTP').disabled=true;
            console.log('OTP:', otpCode);
            showToast('تم إرسال الرمز (تحقق من console)');
        }

        function updateTimer() {
            document.getElementById('timerText').textContent = `${String(Math.floor(otpSeconds/60)).padStart(2,'0')}:${String(otpSeconds%60).padStart(2,'0')}`;
        }

        function otpNext(input) { if(input.value.length===1){ const n=input.nextElementSibling; if(n)n.focus(); } }
        function verifyOTP() {
            const code = Array.from(document.querySelectorAll('#otpInputs input')).map(i=>i.value).join('');
            if(code===localStorage.getItem('evilOTP')) {
                clearInterval(otpTimer);
                const phone=localStorage.getItem('evilOTPPhone');
                let users=JSON.parse(localStorage.getItem('evilUsers')||'[]');
                let user=users.find(u=>u.phone===phone);
                if(!user){user={name:'مستخدم',email:'',phone,password:'',role:'user'};users.push(user);localStorage.setItem('evilUsers',JSON.stringify(users));}
                loginSuccess(user);
            } else showToast('رمز غير صحيح','error');
        }

        function loginGoogle() {
            const accounts=['user1@gmail.com','user2@gmail.com','work@company.com'];
            const sel=prompt('اختر حساب Google:\n'+accounts.map((a,i)=>`${i+1}. ${a}`).join('\n')+'\nأدخل الرقم:');
            if(sel&&accounts[parseInt(sel)-1]){
                let users=JSON.parse(localStorage.getItem('evilUsers')||'[]');
                let user=users.find(u=>u.email===accounts[parseInt(sel)-1]);
                if(!user){user={name:accounts[parseInt(sel)-1].split('@')[0],email:accounts[parseInt(sel)-1],phone:'',password:'',role:'user',googleAuth:true};users.push(user);localStorage.setItem('evilUsers',JSON.stringify(users));}
                loginSuccess(user);
            }
        }

        function showRegister() {
            document.getElementById('registerSection').style.display='block';
            document.getElementById('tabEmail').style.display='none';
            document.getElementById('tabPhone').style.display='none';
            document.getElementById('tabGoogle').style.display='none';
            document.querySelector('.auth-tabs').style.display='none';
            document.querySelector('.divider-text').style.display='none';
        }

        function hideRegister() {
            document.getElementById('registerSection').style.display='none';
            document.getElementById('tabEmail').style.display='block';
            document.querySelector('.auth-tabs').style.display='flex';
            document.querySelector('.divider-text').style.display='block';
        }

        function registerUser() {
            const n=document.getElementById('regName').value.trim();
            const e=document.getElementById('regEmail').value.trim();
            const p=document.getElementById('regPhone').value.trim();
            const pw=document.getElementById('regPassword').value.trim();
            if(!n||!e||!pw) return showToast('املأ الحقول','error');
            let users=JSON.parse(localStorage.getItem('evilUsers')||'[]');
            if(users.find(u=>u.email===e)) return showToast('البريد مستخدم','error');
            // Prevent creating another admin
            if(e===ADMIN.email||p===ADMIN.phone) return showToast('لا يمكن إنشاء حساب مدير','error');
            const user={name:n,email:e,phone:p,password:pw,role:'user'};
            users.push(user); localStorage.setItem('evilUsers',JSON.stringify(users));
            loginSuccess(user);
        }

        function loginSuccess(user) {
            currentUser=user; localStorage.setItem('evilCurrentUser',JSON.stringify(user));
            showMainApp(); showToast(`👋 ${user.name}!`);
        }

        function logout() {
            currentUser=null; localStorage.removeItem('evilCurrentUser');
            document.getElementById('mainApp').classList.remove('show');
            document.getElementById('authPage').style.display='flex';
            document.getElementById('registerSection').style.display='none';
            document.getElementById('tabEmail').style.display='block';
            document.querySelector('.auth-tabs').style.display='flex';
            document.querySelector('.divider-text').style.display='block';
            showToast('تم تسجيل الخروج');
        }

        // ==================== MAIN APP ====================
        function showMainApp() {
            document.getElementById('authPage').style.display='none';
            document.getElementById('mainApp').classList.add('show');
            document.getElementById('userNameNav').textContent=currentUser.name;
            if(currentUser.role==='super_admin') document.getElementById('dashboardNav').style.display='inline';
            updateCartUI(); navigateTo('home');
        }

        function navigateTo(page) {
            const c=document.getElementById('pageContent');
            switch(page) {
                case 'home': c.innerHTML=renderHome(); break;
                case 'menu': c.innerHTML=renderMenu('all'); break;
                case 'drinks': c.innerHTML=renderMenu('drinks'); break;
                case 'food': c.innerHTML=renderMenu('food'); break;
                case 'reservation': c.innerHTML=renderReservation(); break;
                case 'profile': c.innerHTML=renderProfile(); break;
                case 'orders': c.innerHTML=renderOrders(); break;
                case 'dashboard': c.innerHTML=currentUser.role==='super_admin'?renderDashboard():renderHome(); break;
            }
            document.querySelectorAll('.nav-link-evil').forEach(l=>l.classList.remove('active'));
            window.scrollTo({top:0,behavior:'smooth'}); AOS.refresh();
        }

        function renderHome() {
            return `
                <div class="hero-section">
                    <div>
                        <h1 class="hero-title">EVIL BAR</h1>
                        <p class="hero-subtitle">✦ أفخم تجربة قهوة وبار ✦</p>
                        <a href="#" class="hero-btn hero-btn-primary" onclick="navigateTo('menu')">📋 المنيو</a>
                        <a href="#" class="hero-btn hero-btn-outline" onclick="navigateTo('reservation')">🍽 حجز</a>
                    </div>
                </div>
                <div class="section"><div class="container">
                    <h2 class="section-title"><span class="gold-text">منتجاتنا</span> المميزة</h2>
                    <div class="product-grid">${PRODUCTS.filter(p=>[1,3,5,7,9].includes(p.id)).map(p=>productCard(p)).join('')}</div>
                </div></div>
            `;
        }

        function renderMenu(filter) {
            let items=PRODUCTS;
            if(filter==='drinks') items=PRODUCTS.filter(p=>p.cat==='hot'||p.cat==='cold'||p.cat==='alcohol');
            if(filter==='food') items=PRODUCTS.filter(p=>p.cat==='food');
            return `
                <div class="section"><div class="container">
                    <h1 class="section-title"><span class="gold-text">المنيو</span></h1>
                    <div class="product-grid">${items.map(p=>productCard(p)).join('')}</div>
                </div></div>
            `;
        }

        function productCard(p) {
            const price=p.disc||p.price;
            return `
                <div class="product-card" data-aos="fade-up">
                    <div class="product-card-img">
                        <img src="${p.img}" alt="${p.name}" onerror="this.src='https://via.placeholder.com/500x300/1a1a1a/d4af37?text=${p.name}'">
                        ${p.disc?`<span class="product-badge">-${Math.round((1-p.disc/p.price)*100)}%</span>`:''}
                        <div class="product-card-actions">
                            <button class="product-action-btn" onclick="event.stopPropagation();addToCart(${p.id})"><i class="fas fa-cart-plus"></i></button>
                        </div>
                    </div>
                    <div class="product-card-body">
                        <h5>${p.name}</h5><p class="desc">${p.desc}</p>
                        <div class="price-row">${p.disc?`<span class="price-old">${p.price}ج.م</span>`:''}<span class="price-current">${price} ج.م</span></div>
                        <div class="stars">${'★'.repeat(Math.floor(p.rating))} ${p.rating}</div>
                        <button class="btn-add-cart" onclick="addToCart(${p.id})">أضف للسلة</button>
                    </div>
                </div>
            `;
        }

        function renderReservation() {
            return `
                <div class="section"><div class="container"><div class="glass" style="max-width:500px;margin:0 auto;padding:30px;">
                    <h2 style="color:var(--gold);text-align:center;">🍽 حجز</h2>
                    <div class="form-group"><label>عدد الأشخاص</label><select class="form-input">${[1,2,3,4,5,6].map(n=>`<option>${n}</option>`).join('')}</select></div>
                    <div class="form-group"><label>التاريخ</label><input type="date" class="form-input"></div>
                    <div class="form-group"><label>الوقت</label><input type="time" class="form-input"></div>
                    <button class="btn btn-gold" onclick="showToast('✅ تم الحجز')">تأكيد</button>
                </div></div></div>
            `;
        }

        function renderProfile() {
            if(!currentUser)return'';
            return `
                <div class="section"><div class="container"><div class="glass" style="max-width:500px;margin:0 auto;padding:30px;">
                    <h2 style="color:var(--gold);">👤 الملف</h2>
                    <p>الاسم: ${currentUser.name}</p>
                    <p>الهاتف: ${currentUser.phone||'-'}</p>
                    <p>البريد: ${currentUser.email||'-'}</p>
                    <p>الدور: ${currentUser.role==='super_admin'?'👑 مدير':'👤 مستخدم'}</p>
                </div></div></div>
            `;
        }

        function renderOrders() {
            const orders=JSON.parse(localStorage.getItem('evilOrders')||'[]').filter(o=>o.userPhone===currentUser.phone||o.userEmail===currentUser.email);
            return `
                <div class="section"><div class="container">
                    <h2 class="section-title">📦 طلباتي</h2>
                    ${orders.length===0?'<p style="color:var(--gray);text-align:center;">لا توجد طلبات</p>':orders.reverse().map(o=>`
                        <div class="glass p-3 mb-3">
                            <div class="d-flex justify-content-between"><strong>#${o.id}</strong><span style="color:var(--gold);">${o.total}ج.م</span></div>
                            <small>${o.date} | ${o.paymentMethod}</small><br><span class="badge" style="background:var(--gold);color:#000;">${o.status}</span>
                        </div>
                    `).join('')}
                </div></div>
            `;
        }

        function renderDashboard() {
            const users=JSON.parse(localStorage.getItem('evilUsers')||'[]');
            const orders=JSON.parse(localStorage.getItem('evilOrders')||'[]');
            const payments=JSON.parse(localStorage.getItem('evilPayments')||'[]');
            const total=orders.reduce((s,o)=>s+o.total,0);
            return `
                <div class="section"><div class="container">
                    <h1 class="section-title">📊 <span class="gold-text">لوحة التحكم</span></h1>
                    <p style="text-align:center;color:var(--gold);">👑 ${currentUser.name} - المدير</p>
                    <div class="stat-grid mb-4">
                        <div class="stat-card"><h2>${users.length}</h2><p>👥 مستخدمين</p></div>
                        <div class="stat-card"><h2>${orders.length}</h2><p>📦 طلبات</p></div>
                        <div class="stat-card"><h2>${payments.length}</h2><p>💳 مدفوعات</p></div>
                        <div class="stat-card"><h2>${total}ج.م</h2><p>💰 إيرادات</p></div>
                    </div>
                    <h3 class="gold-text">💳 المدفوعات</h3>
                    <div class="table-responsive"><table class="table-evil glass">
                        <thead><tr><th>#</th><th>العميل</th><th>الطريقة</th><th>المبلغ</th><th>الحالة</th><th>التاريخ</th></tr></thead>
                        <tbody>${payments.length===0?'<tr><td colspan="6">لا توجد مدفوعات</td></tr>':payments.reverse().slice(0,20).map(p=>`
                            <tr><td>${p.id}</td><td>${p.userName}</td><td>${p.method}</td><td style="color:var(--gold);">${p.amount}ج.م</td><td>${p.status}</td><td>${p.date}</td></tr>
                        `).join('')}</tbody>
                    </table></div>
                    <h3 class="gold-text mt-4">👥 المستخدمين</h3>
                    <div class="table-responsive"><table class="table-evil glass">
                        <thead><tr><th>الاسم</th><th>الهاتف</th><th>البريد</th>
