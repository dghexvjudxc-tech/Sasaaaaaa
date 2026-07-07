<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>☕ كافيه Evil Bar  - الطلب أونلاين</title>
    <style>
        :root {
            --gold: #d4a853;
            --gold-light: #f0d78c;
            --gold-dark: #b8922e;
            --bg: #0a0a0a;
            --bg2: #141414;
            --bg3: #1e1e1e;
            --text: #f0e6d2;
            --text2: #a89070;
            --border: #2a2a2a;
            --red: #ff4757;
            --green: #2ed573;
            --purple: #a55eea;
            --shadow: 0 10px 40px rgba(0,0,0,0.5);
            --transition: all 0.3s ease;
        }

        * { margin:0; padding:0; box-sizing:border-box; }

        body {
            font-family: 'Cairo', 'Segoe UI', Tahoma, sans-serif;
            background: var(--bg);
            color: var(--text);
            min-height: 100vh;
            overflow-x: hidden;
            scroll-behavior: smooth;
        }

        /* ============ جسيمات ============ */
        #particlesCanvas {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        /* ============ شاشة البداية ============ */
        .welcome-screen {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: #000;
            z-index: 99999;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            animation: welcomeOut 0.8s 2.5s forwards;
        }
        .welcome-screen .coffee-anim {
            font-size: 5em;
            animation: coffeeBounce 0.6s infinite alternate;
        }
        @keyframes coffeeBounce {
            from { transform: translateY(0) rotate(-5deg); }
            to { transform: translateY(-20px) rotate(5deg); }
        }
        .welcome-screen h1 {
            font-size: 2.5em;
            color: var(--gold);
            margin-top: 20px;
            letter-spacing: 5px;
            animation: textGlow 1.5s infinite;
        }
        @keyframes textGlow {
            0%,100% { text-shadow: 0 0 10px rgba(212,168,83,0.5); }
            50% { text-shadow: 0 0 40px rgba(212,168,83,1), 0 0 80px rgba(212,168,83,0.5); }
        }
        .welcome-screen .loading-dots {
            display: flex; gap: 10px; margin-top: 30px;
        }
        .welcome-screen .dot {
            width: 12px; height: 12px;
            background: var(--gold);
            border-radius: 50%;
            animation: dotBounce 0.6s infinite alternate;
        }
        .dot:nth-child(2) { animation-delay: 0.2s; }
        .dot:nth-child(3) { animation-delay: 0.4s; }
        @keyframes dotBounce {
            to { transform: translateY(-20px); opacity: 0.3; }
        }
        @keyframes welcomeOut {
            0% { opacity:1; }
            90% { opacity:1; }
            100% { opacity:0; pointer-events:none; }
        }

        /* ============ النافبار ============ */
        .navbar {
            background: rgba(10,10,10,0.9);
            backdrop-filter: blur(30px);
            border-bottom: 1px solid rgba(212,168,83,0.3);
            padding: 12px 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 1000;
            box-shadow: 0 5px 30px rgba(0,0,0,0.6);
        }
        .logo-box {
            display: flex;
            align-items: center;
            gap: 10px;
            cursor: pointer;
        }
        .logo-box .logo-icon {
            font-size: 2.2em;
            animation: floatIcon 3s ease-in-out infinite;
            filter: drop-shadow(0 0 15px rgba(212,168,83,0.6));
        }
        @keyframes floatIcon {
            0%,100% { transform: translateY(0); }
            50% { transform: translateY(-8px); }
        }
        .logo-box .logo-text {
            font-size: 1.6em;
            font-weight: 900;
            background: linear-gradient(135deg, var(--gold), var(--gold-light), var(--gold));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            letter-spacing: 2px;
        }
        .nav-btns {
            display: flex;
            gap: 10px;
            align-items: center;
            flex-wrap: wrap;
        }
        .nav-btn {
            background: transparent;
            border: 1px solid rgba(212,168,83,0.4);
            color: var(--gold);
            padding: 10px 18px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            font-size: 0.9em;
            transition: var(--transition);
            white-space: nowrap;
        }
        .nav-btn:hover {
            background: var(--gold);
            color: #1a1a1a;
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(212,168,83,0.3);
        }
        .cart-nav-btn {
            background: var(--gold);
            color: #1a1a1a;
            border: none;
            padding: 12px 24px;
            border-radius: 50px;
            font-weight: 900;
            cursor: pointer;
            position: relative;
            transition: var(--transition);
            font-size: 1em;
        }
        .cart-nav-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(212,168,83,0.5);
        }
        .cart-count {
            position: absolute;
            top: -8px; right: -8px;
            background: var(--red);
            color: #fff;
            border-radius: 50%;
            width: 25px; height: 25px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.75em;
            font-weight: 900;
            display: none;
        }
        .user-btn {
            background: transparent;
            border: 1px solid var(--purple);
            color: var(--purple);
            padding: 10px 18px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            font-size: 0.9em;
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: 6px;
        }
        .user-btn:hover { background: rgba(165,94,234,0.2); }
        .user-btn.logged-in { background: var(--purple); color: #fff; }

        /* ============ المحتوى ============ */
        .container {
            max-width: 1300px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 1;
        }

        /* ============ الهيرو ============ */
        .hero {
            text-align: center;
            padding: 50px 20px 30px;
        }
        .hero h1 {
            font-size: clamp(2em, 5vw, 3.5em);
            font-weight: 900;
            background: linear-gradient(135deg, var(--gold), var(--gold-light), #fff, var(--gold));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 10px;
            animation: glowText 2s infinite;
        }
        @keyframes glowText {
            0%,100% { filter: brightness(1); }
            50% { filter: brightness(1.4); }
        }
        .hero p {
            color: var(--text2);
            font-size: 1.1em;
            max-width: 600px;
            margin: 0 auto;
        }

        /* ============ عنوان القسم ============ */
        .section-title {
            text-align: center;
            font-size: 2em;
            font-weight: 900;
            color: var(--gold);
            margin: 50px 0 20px;
        }
        .section-title::after {
            content: '';
            display: block;
            width: 60px; height: 3px;
            background: linear-gradient(90deg, transparent, var(--gold), transparent);
            margin: 10px auto;
            border-radius: 10px;
        }

        /* ============ شبكة المنتجات ============ */
        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(290px, 1fr));
            gap: 22px;
            padding: 10px;
        }
        .product-card {
            background: linear-gradient(160deg, #1a1a1a, #0d0d0d);
            border-radius: 20px;
            overflow: hidden;
            border: 1px solid var(--border);
            transition: var(--transition);
            cursor: pointer;
            box-shadow: 0 8px 25px rgba(0,0,0,0.4);
        }
        .product-card:hover {
            transform: translateY(-12px);
            border-color: var(--gold);
            box-shadow: 0 20px 50px rgba(212,168,83,0.25);
        }
        .product-card .badge {
            position: absolute;
            top: 12px; left: 12px;
            background: var(--red);
            color: #fff;
            padding: 5px 14px;
            border-radius: 20px;
            font-size: 0.75em;
            font-weight: 900;
            z-index: 2;
            animation: pulseBadge 1.5s infinite;
        }
        @keyframes pulseBadge {
            0%,100% { box-shadow: 0 0 0 0 rgba(255,71,87,0.5); }
            50% { box-shadow: 0 0 0 15px rgba(255,71,87,0); }
        }
        .img-wrap {
            width: 100%; height: 230px;
            position: relative;
            overflow: hidden;
        }
        .img-wrap img {
            width: 100%; height: 100%;
            object-fit: cover;
            transition: transform 0.6s;
        }
        .product-card:hover .img-wrap img {
            transform: scale(1.1);
        }
        .img-fallback {
            width: 100%; height: 230px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 6em;
            background: linear-gradient(135deg, #1a1008, #2a1a10);
        }
        .info-wrap {
            padding: 18px;
        }
        .info-wrap h3 {
            font-size: 1.15em;
            margin-bottom: 5px;
        }
        .info-wrap .desc {
            color: #7a6a55;
            font-size: 0.85em;
            margin-bottom: 12px;
        }
        .price-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .old-price {
            font-size: 0.8em;
            color: #555;
            text-decoration: line-through;
            margin-left: 6px;
        }
        .current-price {
            font-size: 1.4em;
            font-weight: 900;
            color: var(--gold);
        }
        .add-btn {
            background: linear-gradient(135deg, var(--gold-dark), var(--gold));
            color: #1a1a1a;
            border: none;
            padding: 10px 20px;
            border-radius: 12px;
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
        }
        .add-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 5px 20px rgba(212,168,83,0.4);
        }
        .qty-row {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .qty-btn {
            background: var(--bg3);
            border: 2px solid var(--gold);
            color: var(--gold);
            width: 32px; height: 32px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 1.1em;
            transition: var(--transition);
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .qty-btn:hover {
            background: var(--gold);
            color: #1a1a1a;
        }
        .qty-val {
            font-weight: 900;
            min-width: 25px;
            text-align: center;
        }

        /* ============ مودال السلة ============ */
        .modal-overlay {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(0,0,0,0.9);
            backdrop-filter: blur(10px);
            z-index: 5000;
            display: none;
            justify-content: center;
            align-items: center;
        }
        .modal-overlay.active { display: flex; animation: fadeIn 0.3s; }
        @keyframes fadeIn { from { opacity:0; } to { opacity:1; } }
        .modal-box {
            background: linear-gradient(160deg, #1a1a1a, #0d0d0d);
            border: 2px solid rgba(212,168,83,0.5);
            border-radius: 25px;
            padding: 30px;
            width: 92%;
            max-width: 650px;
            max-height: 85vh;
            overflow-y: auto;
            position: relative;
            animation: popIn 0.4s ease-out;
            box-shadow: 0 0 80px rgba(212,168,83,0.2);
        }
        @keyframes popIn {
            from { transform: scale(0.5) translateY(50px); opacity:0; }
            to { transform: scale(1) translateY(0); opacity:1; }
        }
        .modal-close {
            position: absolute;
            top: 15px; left: 20px;
            background: none;
            border: none;
            color: var(--gold);
            font-size: 2em;
            cursor: pointer;
            transition: var(--transition);
        }
        .modal-close:hover { color: var(--red); transform: rotate(90deg); }
        .modal-box h2 {
            text-align: center;
            color: var(--gold);
            margin-bottom: 20px;
        }
        .cart-item {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 14px;
            border-bottom: 1px solid #222;
        }
        .cart-item-info { flex: 1; }
        .cart-item-name { font-weight: bold; }
        .cart-item-price { color: var(--gold); font-size: 0.9em; }
        .cart-remove {
            background: var(--red);
            color: #fff;
            border: none;
            padding: 7px 14px;
            border-radius: 8px;
            cursor: pointer;
            transition: var(--transition);
        }
        .cart-remove:hover { background: #d63031; transform: scale(1.1); }
        .cart-total {
            text-align: center;
            font-size: 1.6em;
            font-weight: 900;
            color: var(--gold);
            margin: 20px 0;
        }
        .payment-options {
            display: flex;
            gap: 10px;
            justify-content: center;
            flex-wrap: wrap;
            margin: 15px 0;
        }
        .pay-opt {
            background: var(--bg3);
            border: 2px solid transparent;
            padding: 15px;
            border-radius: 12px;
            cursor: pointer;
            text-align: center;
            font-size: 1.8em;
            transition: var(--transition);
            flex: 1;
            min-width: 90px;
        }
        .pay-opt.selected {
            border-color: var(--gold);
            background: #1a1008;
            box-shadow: 0 0 20px rgba(212,168,83,0.3);
        }
        .pay-opt span {
            display: block;
            font-size: 0.3em;
            margin-top: 4px;
        }
        .checkout-btn {
            width: 100%;
            padding: 16px;
            background: linear-gradient(135deg, #2ed573, #1dd1a1);
            color: #000;
            border: none;
            border-radius: 12px;
            font-size: 1.2em;
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
        }
        .checkout-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(46,213,115,0.4);
        }

        /* ============ مودال تسجيل الدخول ============ */
        .auth-overlay {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(0,0,0,0.95);
            backdrop-filter: blur(15px);
            z-index: 6000;
            display: none;
            justify-content: center;
            align-items: center;
        }
        .auth-overlay.active { display: flex; }
        .auth-box {
            background: linear-gradient(160deg, #1a1a1a, #0d0d0d);
            border: 2px solid rgba(212,168,83,0.5);
            border-radius: 25px;
            padding: 35px;
            width: 92%;
            max-width: 460px;
            animation: popIn 0.4s ease-out;
            box-shadow: 0 0 80px rgba(212,168,83,0.2);
        }
        .auth-box h2 {
            text-align: center;
            color: var(--gold);
            margin-bottom: 20px;
        }
        .auth-tabs {
            display: flex;
            gap: 8px;
            margin-bottom: 20px;
        }
        .auth-tab {
            flex: 1;
            padding: 10px;
            background: transparent;
            border: 2px solid rgba(212,168,83,0.3);
            color: var(--gold);
            border-radius: 10px;
            cursor: pointer;
            font-weight: bold;
            transition: var(--transition);
        }
        .auth-tab.active {
            background: var(--gold);
            color: #1a1a1a;
            border-color: var(--gold);
        }
        .form-group {
            margin-bottom: 14px;
        }
        .form-group label {
            display: block;
            color: var(--gold);
            margin-bottom: 5px;
            font-weight: bold;
            font-size: 0.9em;
        }
        .form-group input {
            width: 100%;
            padding: 12px 16px;
            background: var(--bg3);
            border: 2px solid #2a2a2a;
            border-radius: 10px;
            color: var(--text);
            font-size: 1em;
            font-family: inherit;
            transition: var(--transition);
        }
        .form-group input:focus {
            outline: none;
            border-color: var(--gold);
            box-shadow: 0 0 15px rgba(212,168,83,0.15);
        }
        .btn-submit {
            width: 100%;
            padding: 14px;
            background: linear-gradient(135deg, var(--gold-dark), var(--gold));
            color: #1a1a1a;
            border: none;
            border-radius: 10px;
            font-size: 1.1em;
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
        }
        .btn-submit:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(212,168,83,0.3);
        }
        .error-msg {
            color: var(--red);
            text-align: center;
            margin-top: 8px;
            display: none;
            font-size: 0.9em;
        }
        .success-msg {
            color: var(--green);
            text-align: center;
            margin-top: 8px;
            display: none;
            font-size: 0.9em;
        }

        /* ============ لوحة الأدمن ============ */
        .admin-panel {
            display: none;
            background: linear-gradient(160deg, #0d0d0d, #1a1a1a);
            border: 2px solid var(--purple);
            border-radius: 22px;
            padding: 25px;
            margin: 30px 0;
        }
        .admin-panel.active { display: block; animation: fadeIn 0.5s; }
        .admin-panel h2 {
            color: var(--purple);
            text-align: center;
            margin-bottom: 20px;
        }
        .admin-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 18px;
        }
        .admin-card {
            background: #141414;
            border: 1px solid #222;
            border-radius: 15px;
            padding: 18px;
        }
        .admin-card h3 {
            color: var(--gold);
            text-align: center;
            margin-bottom: 12px;
        }
        .admin-card input,
        .admin-card select {
            width: 100%;
            padding: 10px;
            margin-bottom: 8px;
            background: #0a0a0a;
            border: 1px solid #222;
            border-radius: 8px;
            color: var(--text);
            font-family: inherit;
        }
        .admin-card button {
            width: 100%;
            padding: 11px;
            border: none;
            border-radius: 8px;
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
            margin-top: 4px;
        }
        .btn-add { background: var(--green); color: #000; }
        .btn-del { background: var(--red); color: #fff; width: auto; padding: 6px 12px; font-size: 0.8em; }
        .btn-reset { background: #ffa502; color: #000; }
        .btn-export { background: var(--purple); color: #fff; }
        .admin-list {
            max-height: 350px;
            overflow-y: auto;
        }
        .admin-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 9px;
            border-bottom: 1px solid #1a1a1a;
            font-size: 0.85em;
        }

        /* ============ أزرار عائمة ============ */
        .float-btns {
            position: fixed;
            bottom: 25px;
            left: 25px;
            display: flex;
            flex-direction: column;
            gap: 10px;
            z-index: 100;
        }
        .float-btn {
            width: 50px; height: 50px;
            border-radius: 50%;
            border: none;
            cursor: pointer;
            font-size: 1.3em;
            transition: var(--transition);
            box-shadow: 0 8px 25px rgba(0,0,0,0.4);
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .float-btn:hover { transform: scale(1.15); }
        .float-wa { background: #25D366; color: #fff; animation: waPulse 2s infinite; }
        @keyframes waPulse {
            0%,100% { box-shadow: 0 0 0 0 rgba(37,211,102,0.5); }
            50% { box-shadow: 0 0 0 18px rgba(37,211,102,0); }
        }
        .float-admin { background: linear-gradient(135deg, #6c5ce7, #a55eea); color: #fff; font-weight: 900; }
        .float-cart { background: var(--gold); color: #1a1a1a; display: none; }
        .float-cart.show { display: flex; animation: bounceIn 0.5s; }
        @keyframes bounceIn {
            0% { transform: scale(0); }
            60% { transform: scale(1.2); }
            100% { transform: scale(1); }
        }

        /* ============ توست ============ */
        .toast-container {
            position: fixed;
            top: 80px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 9999;
            display: flex;
            flex-direction: column;
            gap: 8px;
            align-items: center;
            pointer-events: none;
        }
        .toast {
            background: #1a1a1a;
            border: 1px solid var(--gold);
            color: var(--text);
            padding: 14px 28px;
            border-radius: 50px;
            font-weight: bold;
            animation: toastIn 0.4s, toastOut 0.4s 2.5s forwards;
            box-shadow: 0 8px 25px rgba(0,0,0,0.5);
            pointer-events: auto;
        }
        @keyframes toastIn { from { transform: translateY(-40px); opacity:0; } to { transform: translateY(0); opacity:1; } }
        @keyframes toastOut { from { opacity:1; } to { opacity:0; transform: translateY(-30px); } }

        /* ============ فوتر ============ */
        .footer {
            text-align: center;
            padding: 40px 20px;
            background: #050505;
            border-top: 1px solid rgba(212,168,83,0.15);
            margin-top: 50px;
            position: relative;
            z-index: 1;
        }
        .footer h3 { color: var(--gold); font-size: 1.8em; }
        .footer .phone { color: var(--gold); font-size: 1.2em; margin: 8px 0; direction: ltr; display: inline-block; font-weight: bold; }
        .footer .social { display: flex; justify-content: center; gap: 12px; margin: 18px 0; }
        .footer .social-icon {
            width: 42px; height: 42px;
            border-radius: 50%;
            background: #1a1a1a;
            border: 1px solid #2a2a2a;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2em;
            cursor: pointer;
            transition: var(--transition);
        }
        .footer .social-icon:hover {
            border-color: var(--gold);
            background: var(--gold);
            color: #1a1a1a;
            transform: translateY(-5px);
        }

        @media (max-width: 768px) {
            .navbar { flex-wrap: wrap; gap: 8px; justify-content: center; padding: 8px; }
            .nav-btn { padding: 7px 12px; font-size: 0.75em; }
            .products-grid { grid-template-columns: 1fr 1fr; gap: 12px; }
            .img-wrap, .img-fallback { height: 160px; }
            .img-fallback { font-size: 4em; }
            .section-title { font-size: 1.4em; }
            .hero h1 { font-size: 1.8em; }
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700;900&display=swap" rel="stylesheet">
</head>
<body>

    <!-- جسيمات -->
    <canvas id="particlesCanvas"></canvas>

    <!-- شاشة البداية -->
    <div class="welcome-screen">
        <div class="coffee-anim">☕</div>
        <h1>كافيه مصطفى</h1>
        <div class="loading-dots">
            <div class="dot"></div><div class="dot"></div><div class="dot"></div>
        </div>
    </div>

    <!-- النافبار -->
    <nav class="navbar">
        <div class="logo-box" onclick="window.scrollTo({top:0,behavior:'smooth'})">
            <span class="logo-icon">☕</span>
            <span class="logo-text">كافيه مصطفى</span>
        </div>
        <div class="nav-btns">
            <button class="nav-btn" onclick="scrollToSection('drinks')">🥤 مشروبات</button>
            <button class="nav-btn" onclick="scrollToSection('food')">🍽️ مأكولات</button>
            <button class="nav-btn" onclick="scrollToSection('drinks2')">🍷 مشروبات خاصة</button>
            <button class="nav-btn" onclick="scrollToSection('payment')">💳 الدفع</button>
            <button class="user-btn" id="userBtn" onclick="toggleAuth()">👤 دخول</button>
            <button class="cart-nav-btn" onclick="openCart()">
                🛒 السلة <span class="cart-count" id="cartBadge">0</span>
            </button>
        </div>
    </nav>

    <!-- المحتوى -->
    <div class="container">
        <!-- هيرو -->
        <div class="hero">
            <h1>☕ كافيه مصطفى</h1>
            <p>أجود المشروبات والمأكولات - اطلب أونلاين واستمتع</p>
        </div>

        <!-- المشروبات -->
        <div id="drinks">
            <h2 class="section-title">🥤 المشروبات الساخنة والباردة</h2>
            <div class="products-grid" id="drinksGrid"></div>
        </div>

        <!-- المأكولات -->
        <div id="food">
            <h2 class="section-title">🍽️ المأكولات والحلويات</h2>
            <div class="products-grid" id="foodGrid"></div>
        </div>

        <!-- مشروبات خاصة -->
        <div id="drinks2">
            <h2 class="section-title">🍷 مشروبات خاصة</h2>
            <div class="products-grid" id="drinks2Grid"></div>
        </div>

        <!-- طرق الدفع -->
        <div id="payment">
            <h2 class="section-title">💳 طرق الدفع</h2>
            <p style="text-align:center;color:var(--text2);">الدفع عند الاستلام أو عن طريق فودافون كاش</p>
            <div style="display:flex;flex-wrap:wrap;gap:15px;justify-content:center;padding:25px;">
                <div style="background:#1a1a1a;border:2px solid var(--gold);border-radius:18px;padding:30px;text-align:center;font-size:3em;flex:1;min-width:150px;">💵<br><span style="font-size:0.3em;">نقداً عند الاستلام</span></div>
                <div style="background:#1a1a1a;border:2px solid var(--gold);border-radius:18px;padding:30px;text-align:center;font-size:3em;flex:1;min-width:150px;">📱<br><span style="font-size:0.3em;">فودافون كاش<br><span dir="ltr" style="color:var(--gold);">01026966717</span></span></div>
            </div>
        </div>

        <!-- لوحة الأدمن -->
        <div class="admin-panel" id="adminPanel">
            <h2>👑 لوحة تحكم الأدمن</h2>
            <div class="admin-grid">
                <div class="admin-card">
                    <h3>➕ إضافة منتج</h3>
                    <select id="adminCat">
                        <option value="drinks">🥤 مشروبات</option>
                        <option value="food">🍽️ مأكولات</option>
                        <option value="drinks2">🍷 مشروبات خاصة</option>
                    </select>
                    <input type="text" id="adminName" placeholder="اسم المنتج">
                    <input type="text" id="adminDesc" placeholder="الوصف">
                    <input type="number" id="adminPrice" placeholder="السعر">
                    <input type="number" id="adminOldPrice" placeholder="السعر قبل الخصم (اختياري)">
                    <input type="text" id="adminEmoji" placeholder="إيموجي">
                    <input type="text" id="adminImg" placeholder="رابط الصورة">
                    <button class="btn-add" onclick="adminAddProduct()">✅ إضافة</button>
                </div>
                <div class="admin-card">
                    <h3>📋 المنتجات الحالية</h3>
                    <div class="admin-list" id="adminList"></div>
                </div>
                <div class="admin-card">
                    <h3>⚙️ أدوات</h3>
                    <p style="color:var(--gold);">🥤 مشروبات: <b id="s1">0</b></p>
                    <p style="color:var(--gold);">🍽️ مأكولات: <b id="s2">0</b></p>
                    <p style="color:var(--gold);">🍷 خاصة: <b id="s3">0</b></p>
                    <button class="btn-reset" onclick="adminReset()" style="margin-top:10px;">🔄 إعادة ضبط</button>
                    <button class="btn-export" onclick="adminExport()">📤 تصدير</button>
                </div>
            </div>
        </div>
    </div>

    <!-- مودال السلة -->
    <div class="modal-overlay" id="cartModal">
        <div class="modal-box">
            <button class="modal-close" onclick="closeCart()">✕</button>
            <h2>🛒 سلة المشتريات</h2>
            <div id="cartItems"></div>
            <div class="cart-total" id="cartTotal">الإجمالي: 0 ج.م</div>
            <p style="text-align:center;color:var(--gold);">اختر طريقة الدفع:</p>
            <div class="payment-options" id="payOpts">
                <div class="pay-opt selected" onclick="selectPay('cash',this)">💵<span>نقداً</span></div>
                <div class="pay-opt" onclick="selectPay('vodafone',this)">📱<span>فودافون كاش</span></div>
            </div>
            <button class="checkout-btn" onclick="checkout()">✅ تأكيد الطلب واتساب</button>
        </div>
    </div>

    <!-- مودال الدخول -->
    <div class="auth-overlay" id="authOverlay">
        <div class="auth-box">
            <h2>🔐 تسجيل الدخول / إنشاء حساب</h2>
            <div class="auth-tabs">
                <button class="auth-tab active" onclick="switchTab('login')">تسجيل الدخول</button>
                <button class="auth-tab" onclick="switchTab('register')">إنشاء حساب</button>
            </div>
            <div id="loginForm">
                <div class="form-group"><label>👤 اسم المستخدم</label><input type="text" id="loginUser" placeholder="اسم المستخدم"></div>
                <div class="form-group"><label>🔒 كلمة المرور</label><input type="password" id="loginPass" placeholder="كلمة المرور"></div>
                <div class="error-msg" id="loginErr"></div>
                <button class="btn-submit" onclick="doLogin()">🚪 دخول</button>
            </div>
            <div id="registerForm" style="display:none;">
                <div class="form-group"><label>👤 اسم المستخدم</label><input type="text" id="regUser" placeholder="اختر اسم مستخدم"></div>
                <div class="form-group"><label>📧 البريد الإلكتروني</label><input type="email" id="regEmail" placeholder="بريدك الإلكتروني"></div>
                <div class="form-group"><label>🔒 كلمة المرور</label><input type="password" id="regPass" placeholder="كلمة مرور (6+ أحرف)"></div>
                <div class="form-group"><label>🔒 تأكيد كلمة المرور</label><input type="password" id="regPass2" placeholder="أعد كتابة كلمة المرور"></div>
                <div class="error-msg" id="regErr"></div>
                <div class="success-msg" id="regOk"></div>
                <button class="btn-submit" onclick="doRegister()">📝 إنشاء حساب</button>
            </div>
            <button style="width:100%;margin-top:12px;padding:10px;background:transparent;border:1px solid #333;color:#888;border-radius:8px;cursor:pointer;" onclick="closeAuth()">✕ إغلاق</button>
        </div>
    </div>

    <!-- أزرار عائمة -->
    <div class="float-btns">
        <button class="float-btn float-wa" onclick="openWa()" title="واتساب">💬</button>
        <button class="float-btn float-admin" id="floatAdmin" onclick="toggleAdmin()" title="لوحة الأدمن">👑</button>
        <button class="float-btn float-cart" id="floatCart" onclick="openCart()" title="السلة">🛒</button>
    </div>

    <!-- توست -->
    <div class="toast-container" id="toastContainer"></div>

    <!-- فوتر -->
    <div class="footer">
        <h3>☕ كافيه مصطفى</h3>
        <p style="color:var(--text2);">📍 شارع النخيل، مدينة القهوة</p>
        <p class="phone">📞 01026966717</p>
        <div class="social">
            <div class="social-icon">📘</div><div class="social-icon">📷</div><div class="social-icon">🐦</div>
        </div>
        <p style="color:#555;margin-top:15px;">© 2026 كافيه مصطفى - Developed by Mustafa 👑</p>
    </div>

    <script>
        // ==================== البيانات ====================
        const ADMIN_USERNAME = 'Mustafa';
        const ADMIN_PASSWORD = '123456';
        const WA_NUMBER = '201026966717';
        const PHONE = '01026966717';

        function getDefaultData() {
            return {
                drinks: [
                    { id:1, name:'قهوة تركية', desc:'قهوة تركية أصلية على الرمل', price:25, oldPrice:0, emoji:'☕', img:'https://images.unsplash.com/photo-1572442388796-11668a67e53d?w=400&h=300&fit=crop' },
                    { id:2, name:'لاتيه كريمي', desc:'لاتيه بحليب طازج وفن اللاتيه', price:35, oldPrice:42, emoji:'🥛', img:'https://images.unsplash.com/photo-1570968915860-54d5c301fa9f?w=400&h=300&fit=crop' },
                    { id:3, name:'كابتشينو', desc:'كابتشينو إيطالي برغوة كثيفة', price:30, oldPrice:0, emoji:'☕', img:'https://images.unsplash.com/photo-1534778101976-62847782c213?w=400&h=300&fit=crop' },
                    { id:4, name:'شاي كرك', desc:'شاي كرك هندي أصلي', price:20, oldPrice:25, emoji:'🍵', img:'https://images.unsplash.com/photo-1564890369478-c89ca6d9cde9?w=400&h=300&fit=crop' },
                    { id:5, name:'موكا مثلجة', desc:'موكا باردة بصوص الشوكولاتة', price:40, oldPrice:0, emoji:'🧊', img:'https://images.unsplash.com/photo-1461023058943-07fcbe16d735?w=400&h=300&fit=crop' },
                    { id:6, name:'عصير مانجو', desc:'مانجو طبيعي 100%', price:30, oldPrice:0, emoji:'🥭', img:'https://images.unsplash.com/photo-1546173159-315724a31696?w=400&h=300&fit=crop' },
                    { id:7, name:'ليمون بالنعناع', desc:'عصير ليمون طازج', price:22, oldPrice:0, emoji:'🍋', img:'https://images.unsplash.com/photo-1621263764928-df1444c5e859?w=400&h=300&fit=crop' },
                    { id:8, name:'سحلب', desc:'سحلب ساخن بالمكسرات', price:28, oldPrice:35, emoji:'🥜', img:'https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=400&h=300&fit=crop' },
                ],
                food: [
                    { id:101, name:'كرواسون زبدة', desc:'كرواسون فرنسي طازج', price:30, oldPrice:0, emoji:'🥐', img:'https://images.unsplash.com/photo-1555507036-ab1f4038024a?w=400&h=300&fit=crop' },
                    { id:102, name:'تشيز كيك', desc:'تشيز كيك بالتوت الطازج', price:45, oldPrice:55, emoji:'🍰', img:'https://images.unsplash.com/photo-1533134242443-d4fd215305ad?w=400&h=300&fit=crop' },
                    { id:103, name:'وافل شوكولاتة', desc:'وافل بلجيكي بصوص الشوكولاتة', price:40, oldPrice:0, emoji:'🧇', img:'https://images.unsplash.com/photo-1558584724-0e4d32ca55a6?w=400&h=300&fit=crop' },
                    { id:104, name:'بان كيك', desc:'بان كيك أمريكي بالعسل', price:35, oldPrice:0, emoji:'🥞', img:'https://images.unsplash.com/photo-1567620905732-2d1ec7ab7445?w=400&h=300&fit=crop' },
                    { id:105, name:'ساندوتش دجاج', desc:'دجاج مشوي طازج', price:50, oldPrice:60, emoji:'🥪', img:'https://images.unsplash.com/photo-1528735602780-2552fd46c7af?w=400&h=300&fit=crop' },
                    { id:106, name:'بيتزا مارجريتا', desc:'بيتزا إيطالية أصلية', price:45, oldPrice:0, emoji:'🍕', img:'https://images.unsplash.com/photo-1574071318508-1cdbab80d002?w=400&h=300&fit=crop' },
                ],
                drinks2: [
                    { id:201, name:'مشروب خاص 1', desc:'مشروب مميز بنكهة خاصة', price:50, oldPrice:0, emoji:'🍷', img:'https://images.unsplash.com/photo-1474722883777-792e7990302f?w=400&h=300&fit=crop' },
                    { id:202, name:'مشروب خاص 2', desc:'مشروب فاخر للمناسبات', price:65, oldPrice:80, emoji:'🥂', img:'https://images.unsplash.com/photo-1514362545857-3bc16c4c7d1b?w=400&h=300&fit=crop' },
                    { id:203, name:'مشروب خاص 3', desc:'مشروب بارد منعش', price:45, oldPrice:0, emoji:'🍸', img:'https://images.unsplash.com/photo-1536935338788-846bb9981813?w=400&h=300&fit=crop' },
                    { id:204, name:'مشروب خاص 4', desc:'مشروب دافئ للشتاء', price:55, oldPrice:0, emoji:'🥃', img:'https://images.unsplash.com/photo-1569529465841-dfecdab7503b?w=400&h=300&fit=crop' },
                ],
            };
        }

        function loadData() {
            const s = localStorage.getItem('MF_DATA_V4');
            if (s) { try { return JSON.parse(s); } catch(e) {} }
            return getDefaultData();
        }
        function saveData() { localStorage.setItem('MF_DATA_V4', JSON.stringify(cafeData)); }

        let cafeData = loadData();
        let cart = JSON.parse(localStorage.getItem('MF_CART_V4') || '[]');
        let selectedPayment = 'cash';
        let isAdminLoggedIn = localStorage.getItem('MF_ADMIN_V4') === 'true';
        let currentUser = JSON.parse(localStorage.getItem('MF_USER_V4') || 'null');

        // ==================== جسيمات ====================
        const pc = document.getElementById('particlesCanvas');
        const pctx = pc.getContext('2d');
        pc.width = window.innerWidth;
        pc.height = window.innerHeight;
        const particles = [];
        class Particle {
            constructor() { this.reset();
                this.y = Math.random() * pc.height; }
            reset() { this.x = Math.random() * pc.width;
                this.y = -10;
                this.size = Math.random() * 3 + 1;
                this.sy = Math.random() * 1.5 + 0.3;
                this.sx = (Math.random() - 0.5) * 0.5;
                this.op = Math.random() * 0.6 + 0.2;
                this.c = ['#d4a853','#f0d78c','#b8922e'][Math.floor(Math.random()*3)]; }
            update() { this.y += this.sy;
                this.x += this.sx; if (this.y > pc.height + 10) this.reset(); }
            draw() { pctx.beginPath();
                pctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                pctx.fillStyle = this.c;
                pctx.globalAlpha = this.op;
                pctx.fill();
                pctx.globalAlpha = 1; }
        }
        for (let i = 0; i < 50; i++) particles.push(new Particle());
        function animParticles() { pctx.clearRect(0, 0, pc.width, pc.height);
            particles.forEach(p => { p.update();
                p.draw(); });
            requestAnimationFrame(animParticles); }
        animParticles();
        window.addEventListener('resize', () => { pc.width = window.innerWidth;
            pc.height = window.innerHeight; });

        // ==================== توست ====================
        function toast(msg, err = false) {
            const c = document.getElementById('toastContainer');
            const t = document.createElement('div');
            t.className = 'toast';
            t.style.borderColor = err ? 'var(--red)' : 'var(--gold)';
            t.textContent = msg;
            c.appendChild(t);
            setTimeout(() => t.remove(), 3000);
        }

        // ==================== عرض المنتجات ====================
        function cardHTML(p) {
            const ci = cart.find(i => i.id === p.id);
            const qty = ci ? ci.quantity : 0;
            const disc = p.oldPrice > 0 && p.oldPrice > p.price;
            const pct = disc ? Math.round((1 - p.price / p.oldPrice) * 100) : 0;
            const img = p.img ? `<img src="${p.img}" alt="${p.name}" loading="lazy" onerror="this.style.display='none';this.parentElement.querySelector('.fb').style.display='flex';">` : '';
            return `
            <div class="product-card" style="position:relative;">
              ${disc?`<div class="badge">🔥 -${pct}%</div>`:''}
              <div class="img-wrap">
                ${img}
                <div class="img-fallback fb" style="${p.img?'display:none;':''}">${p.emoji||'🍽️'}</div>
              </div>
              <div class="info-wrap">
                <h3>${p.emoji||''} ${p.name}</h3>
                <p class="desc">${p.desc}</p>
                <div class="price-row">
                  <div>
                    ${disc?`<span class="old-price">${p.oldPrice} ج.م</span>`:''}
                    <span class="current-price">${p.price} ج.م</span>
                  </div>
                  ${qty>0?`
                    <div class="qty-row">
                      <button class="qty-btn" onclick="chgQty(${p.id},'${p.name.replace(/'/g,"\\'")}',${p.price},-1,event)">➖</button>
                      <span class="qty-val">${qty}</span>
                      <button class="qty-btn" onclick="chgQty(${p.id},'${p.name.replace(/'/g,"\\'")}',${p.price},1,event)">➕</button>
                    </div>
                  `:`<button class="add-btn" onclick="chgQty(${p.id},'${p.name.replace(/'/g,"\\'")}',${p.price},1,event)">🛒 أضف</button>`}
                </div>
              </div>
            </div>`;
        }

        function renderAll() {
            document.getElementById('drinksGrid').innerHTML = cafeData.drinks.map(cardHTML).join('');
            document.getElementById('foodGrid').innerHTML = cafeData.food.map(cardHTML).join('');
            document.getElementById('drinks2Grid').innerHTML = cafeData.drinks2.map(cardHTML).join('');
            updateBadge();
            updateAdminStats();
            document.getElementById('s1').textContent = cafeData.drinks.length;
            document.getElementById('s2').textContent = cafeData.food.length;
            document.getElementById('s3').textContent = cafeData.drinks2.length;
        }

        function chgQty(id, name, price, delta, e) {
            if (e) e.stopPropagation();
            const ex = cart.find(i => i.id === id);
            if (ex) { ex.quantity += delta; if (ex.quantity <= 0) cart = cart.filter(i => i.id !== id); } else if (delta > 0) { cart.push({ id, name, price, quantity: delta }); }
            saveCart();
            renderAll();
            if (delta > 0) toast(`✅ تمت إضافة "${name}"`);
        }

        // ==================== السلة ====================
        function saveCart() { localStorage.setItem('MF_CART_V4', JSON.stringify(cart));
            updateBadge(); }

        function updateBadge() {
            const cnt = cart.reduce((s, i) => s + i.quantity, 0);
            const b = document.getElementById('cartBadge');
            const f = document.getElementById('floatCart');
            b.textContent = cnt;
            b.style.display = cnt > 0 ? 'flex' : 'none';
            if (cnt > 0) f.classList.add('show');
            else f.classList.remove('show');
        }

        function openCart() { document.getElementById('cartModal').classList.add('active');
            renderCart(); }

        function closeCart() { document.getElementById('cartModal').classList.remove('active'); }

        function renderCart() {
            const c = document.getElementById('cartItems');
            const t = document.getElementById('cartTotal');
            if (cart.length === 0) {
                c.innerHTML = '<div style="text-align:center;padding:40px;color:#555;"><div style="font-size:4em;">🛒</div><p>السلة فارغة</p></div>';
                t.textContent = 'الإجمالي: 0 ج.م';
                return;
            }
            let total = 0;
            c.innerHTML = cart.map(i => { const it = i.price * i.quantity;
                total += it; return `
              <div class="cart-item">
                <div class="cart-item-info"><span class="cart-item-name">${i.name} ×${i.quantity}</span><br><span class="cart-item-price">${it} ج.م</span></div>
                <button class="cart-remove" onclick="removeCart(${i.id})">🗑️</button>
              </div>`; }).join('');
            t.textContent = `الإجمالي: ${total} ج.م`;
        }

        function removeCart(id) { cart = cart.filter(i => i.id !== id);
            saveCart();
            renderAll();
            renderCart(); }

        function selectPay(m, el) { selectedPayment = m;
            document.querySelectorAll('#payOpts .pay-opt').forEach(o => o.classList.remove('selected'));
            el.classList.add('selected'); }

        function checkout() {
            if (cart.length === 0) { toast('⚠️ السلة فارغة!', true); return; }
            const total = cart.reduce((s, i) => s + (i.price * i.quantity), 0);
            const pn = { cash: 'نقداً عند الاستلام', vodafone: 'فودافون كاش' };
            const sum = cart.map(i => `• ${i.name} ×${i.quantity} = ${i.price*i.quantity} ج.م`).join('\n');
            const msg = `🛒 *طلب جديد - كافيه مصطفى*\n━━━━━━━━━━\n${sum}\n━━━━━━━━━━\n💰 *الإجمالي:* ${total} ج.م\n💳 *الدفع:* ${pn[selectedPayment]}\n📞 *${PHONE}*\n━━━━━━━━━━\n🙏 شكراً! ☕`;
            const url = `https://wa.me/${WA_NUMBER}?text=${encodeURIComponent(msg)}`;
            toast('🎉 جاري إرسال الطلب للواتساب...');
            cart = [];
            saveCart();
            renderAll();
            closeCart();
            setTimeout(() => window.open(url, '_blank'), 700);
        }

        function openWa() { window.open(`https://wa.me/${WA_NUMBER}?text=مرحباً كافيه مصطفى`, '_blank'); }

        // ==================== المصادقة ====================
        function toggleAuth() { document.getElementById('authOverlay').classList.toggle('active'); }

        function closeAuth() { document.getElementById('authOverlay').classList.remove('active'); }

        function switchTab(t) {
            document.querySelectorAll('.auth-tab').forEach(x => x.classList.remove('active'));
            if (t === 'login') {
                document.querySelector('.auth-tab:nth-child(1)').classList.add('active');
                document.getElementById('loginForm').style.display = 'block';
                document.getElementById('registerForm').style.display = 'none';
            } else {
                document.querySelector('.auth-tab:nth-child(2)').classList.add('active');
                document.getElementById('loginForm').style.display = 'none';
                document.getElementById('registerForm').style.display = 'block';
            }
            document.getElementById('loginErr').style.display = 'none';
            document.getElementById('regErr').style.display = 'none';
            document.getElementById('regOk').style.display = 'none';
        }

        function doLogin() {
            const u = document.getElementById('loginUser').value.trim();
            const p = document.getElementById('loginPass').value.trim();
            const err = document.getElementById('loginErr');
            if (!u || !p) { err.textContent = '⚠️ املأ جميع الحقول';
                err.style.display = 'block'; return; }
            const users = JSON.parse(localStorage.getItem('MF_USERS_V4') || '[]');
            const user = users.find(x => x.username.toLowerCase() === u.toLowerCase() && x.password === p);
            if (user) {
                currentUser = user;
                localStorage.setItem('MF_USER_V4', JSON.stringify(user));
                // التحقق من الأدمن
                if (user.isAdmin) { isAdminLoggedIn = true;
                    localStorage.setItem('MF_ADMIN_V4', 'true');
                    updateAdminUI(); }
                closeAuth();
                updateUserBtn();
                toast(`✅ مرحباً ${user.username}!`);
                if (user.isAdmin) { document.getElementById('adminPanel').classList.add('active');
                    renderAdminList();
                    document.getElementById('adminPanel').scrollIntoView({ behavior: 'smooth' }); }
            } else { err.textContent = '❌ بيانات غير صحيحة';
                err.style.display = 'block'; }
        }

        function doRegister() {
            const u = document.getElementById('regUser').value.trim();
            const e = document.getElementById('regEmail').value.trim();
            const p = document.getElementById('regPass').value.trim();
            const p2 = document.getElementById('regPass2').value.trim();
            const err = document.getElementById('regErr');
            const ok = document.getElementById('regOk');
            err.style.display = 'none';
            ok.style.display = 'none';
            if (!u || !e || !p || !p2) { err.textContent = '⚠️ املأ جميع الحقول';
                err.style.display = 'block'; return; }
            if (p !== p2) { err.textContent = '❌ كلمتا المرور غير متطابقتين';
                err.style.display = 'block'; return; }
         
