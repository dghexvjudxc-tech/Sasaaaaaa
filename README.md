<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>☕ كافيه مصطفى - النظام المتكامل</title>
    <style>
        :root {
            --gold: #d4a853;
            --gold-light: #f0d78c;
            --gold-dark: #b8922e;
            --bg-primary: #0a0a0a;
            --bg-secondary: #141414;
            --bg-card: #1a1a1a;
            --bg-input: #1e1e1e;
            --text-primary: #f5e6d0;
            --text-secondary: #a89070;
            --border: #2a2a2a;
            --border-gold: rgba(212, 168, 83, 0.3);
            --red: #ff4757;
            --green: #2ed573;
            --blue: #5352ed;
            --purple: #a55eea;
            --orange: #ffa502;
            --pink: #ff6b81;
            --teal: #1dd1a1;
            --shadow: 0 10px 40px rgba(0, 0, 0, 0.5);
            --shadow-gold: 0 10px 40px rgba(212, 168, 83, 0.2);
            --radius: 20px;
            --radius-sm: 12px;
            --transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Cairo', 'Segoe UI', Tahoma, sans-serif;
            background: var(--bg-primary);
            color: var(--text-primary);
            min-height: 100vh;
            overflow-x: hidden;
            scroll-behavior: smooth;
            -webkit-tap-highlight-color: transparent;
        }

        /* ============ مؤشر مخصص ============ */
        .cursor-glow {
            width: 30px;
            height: 30px;
            border: 2px solid var(--gold);
            border-radius: 50%;
            position: fixed;
            pointer-events: none;
            z-index: 99999;
            transition: all 0.15s;
            mix-blend-mode: difference;
        }
        .cursor-dot-inner {
            width: 8px;
            height: 8px;
            background: var(--gold-light);
            border-radius: 50%;
            position: fixed;
            pointer-events: none;
            z-index: 99999;
            transition: all 0.05s;
        }

        /* ============ جسيمات ============ */
        #particleCanvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        /* ============ شاشة التحميل ============ */
        .splash-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--bg-primary);
            z-index: 99999;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            transition: all 1s cubic-bezier(0.77, 0, 0.175, 1);
        }
        .splash-screen.hidden {
            opacity: 0;
            pointer-events: none;
            transform: scale(1.5);
        }
        .splash-logo {
            font-size: 6em;
            animation: splashBounce 1.5s infinite;
        }
        @keyframes splashBounce {
            0%,
            100% {
                transform: translateY(0) rotate(0);
            }
            25% {
                transform: translateY(-20px) rotate(-5deg);
            }
            50% {
                transform: translateY(0) rotate(0);
            }
            75% {
                transform: translateY(-10px) rotate(5deg);
            }
        }
        .splash-title {
            font-size: 2.5em;
            font-weight: 900;
            background: linear-gradient(135deg, var(--gold), var(--gold-light), var(--gold));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-top: 20px;
            letter-spacing: 5px;
        }
        .splash-progress {
            width: 300px;
            height: 5px;
            background: #222;
            border-radius: 10px;
            margin-top: 40px;
            overflow: hidden;
        }
        .splash-progress-bar {
            height: 100%;
            background: linear-gradient(90deg, var(--gold-dark), var(--gold), var(--gold-light));
            border-radius: 10px;
            animation: splashLoad 2s ease-in-out;
        }
        @keyframes splashLoad {
            0% {
                width: 0;
            }
            100% {
                width: 100%;
            }
        }

        /* ============ النافبار ============ */
        .navbar {
            background: rgba(10, 10, 10, 0.85);
            backdrop-filter: blur(40px) saturate(180%);
            -webkit-backdrop-filter: blur(40px) saturate(180%);
            border-bottom: 1px solid var(--border-gold);
            padding: 12px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 1000;
            animation: navbarIn 0.8s ease-out;
            box-shadow: 0 5px 30px rgba(0, 0, 0, 0.6);
        }
        @keyframes navbarIn {
            from {
                transform: translateY(-120%);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }
        .logo-wrap {
            display: flex;
            align-items: center;
            gap: 12px;
            cursor: pointer;
            transition: var(--transition);
        }
        .logo-wrap:hover {
            transform: scale(1.05);
        }
        .logo-ico {
            font-size: 2.5em;
            animation: logoFloat 3s ease-in-out infinite;
            filter: drop-shadow(0 0 20px rgba(212, 168, 83, 0.7));
        }
        @keyframes logoFloat {
            0%,
            100% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-12px);
            }
        }
        .logo-txt {
            font-size: 1.8em;
            font-weight: 900;
            background: linear-gradient(135deg, var(--gold), var(--gold-light), var(--gold));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            letter-spacing: 3px;
        }
        .nav-actions {
            display: flex;
            gap: 12px;
            align-items: center;
            flex-wrap: wrap;
        }
        .nav-btn {
            background: transparent;
            border: 1px solid rgba(212, 168, 83, 0.35);
            color: var(--gold);
            padding: 10px 20px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            font-size: 0.9em;
            transition: var(--transition);
            position: relative;
            overflow: hidden;
            white-space: nowrap;
        }
        .nav-btn::after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            background: rgba(212, 168, 83, 0.2);
            border-radius: 50%;
            transform: translate(-50%, -50%);
            transition: all 0.5s;
        }
        .nav-btn:hover::after {
            width: 400px;
            height: 400px;
        }
        .nav-btn:hover {
            border-color: var(--gold);
            color: #fff;
            transform: translateY(-3px);
            box-shadow: var(--shadow-gold);
        }
        .nav-cart-btn {
            background: linear-gradient(135deg, var(--gold-dark), var(--gold));
            color: #1a1a1a;
            border: none;
            padding: 12px 28px;
            border-radius: 50px;
            font-weight: 900;
            cursor: pointer;
            position: relative;
            transition: var(--transition);
            font-size: 1em;
            box-shadow: 0 5px 25px rgba(212, 168, 83, 0.35);
        }
        .nav-cart-btn:hover {
            transform: translateY(-4px);
            box-shadow: 0 10px 40px rgba(212, 168, 83, 0.55);
        }
        .cart-badge {
            position: absolute;
            top: -10px;
            right: -10px;
            background: var(--red);
            color: #fff;
            border-radius: 50%;
            width: 28px;
            height: 28px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.8em;
            font-weight: 900;
            animation: badgePop 0.5s ease-out;
            display: none;
        }
        @keyframes badgePop {
            0% {
                transform: scale(0);
            }
            60% {
                transform: scale(1.4);
            }
            100% {
                transform: scale(1);
            }
        }
        .nav-user-btn {
            background: transparent;
            border: 1px solid var(--purple);
            color: var(--purple);
            padding: 10px 20px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            font-size: 0.9em;
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .nav-user-btn:hover {
            background: rgba(165, 94, 234, 0.15);
            transform: translateY(-3px);
        }
        .nav-user-btn.logged-in {
            background: var(--purple);
            color: #fff;
        }

        /* ============ المحتوى الرئيسي ============ */
        .main-wrap {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 1;
        }

        /* ============ الهيرو ============ */
        .hero-section {
            text-align: center;
            padding: 60px 20px 40px;
            position: relative;
        }
        .hero-title {
            font-size: clamp(2.5em, 6vw, 4.5em);
            font-weight: 900;
            background: linear-gradient(135deg, var(--gold), var(--gold-light), #fff, var(--gold));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: heroGlow 2.5s ease-in-out infinite;
            margin-bottom: 15px;
            line-height: 1.2;
        }
        @keyframes heroGlow {
            0%,
            100% {
                filter: brightness(1) drop-shadow(0 0 10px rgba(212, 168, 83, 0.3));
            }
            50% {
                filter: brightness(1.4) drop-shadow(0 0 30px rgba(212, 168, 83, 0.7));
            }
        }
        .hero-desc {
            font-size: 1.2em;
            color: var(--text-secondary);
            max-width: 700px;
            margin: 0 auto 30px;
            line-height: 1.7;
        }
        .hero-search {
            display: flex;
            max-width: 500px;
            margin: 0 auto 30px;
            gap: 10px;
        }
        .hero-search input {
            flex: 1;
            padding: 15px 25px;
            background: var(--bg-input);
            border: 2px solid var(--border);
            border-radius: 50px;
            color: var(--text-primary);
            font-size: 1em;
            transition: var(--transition);
            font-family: inherit;
        }
        .hero-search input:focus {
            outline: none;
            border-color: var(--gold);
            box-shadow: 0 0 25px rgba(212, 168, 83, 0.2);
        }
        .hero-search button {
            padding: 15px 25px;
            background: var(--gold);
            color: #1a1a1a;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            font-weight: 900;
            font-size: 1.2em;
            transition: var(--transition);
        }
        .hero-search button:hover {
            background: var(--gold-light);
            transform: scale(1.05);
        }
        .stats-row {
            display: flex;
            justify-content: center;
            gap: 25px;
            flex-wrap: wrap;
        }
        .stat-item {
            background: rgba(20, 20, 20, 0.8);
            border: 1px solid var(--border-gold);
            border-radius: var(--radius);
            padding: 25px 35px;
            text-align: center;
            backdrop-filter: blur(20px);
            transition: var(--transition);
            cursor: default;
        }
        .stat-item:hover {
            transform: translateY(-10px);
            border-color: var(--gold);
            box-shadow: var(--shadow-gold);
        }
        .stat-num {
            font-size: 2.8em;
            font-weight: 900;
            color: var(--gold);
            display: block;
        }
        .stat-label {
            color: var(--text-secondary);
            font-size: 0.95em;
            margin-top: 5px;
        }

        /* ============ عناوين الأقسام ============ */
        .section-head {
            text-align: center;
            font-size: 2.2em;
            font-weight: 900;
            color: var(--gold);
            margin: 50px 0 20px;
            position: relative;
        }
        .section-head::after {
            content: '';
            display: block;
            width: 70px;
            height: 3px;
            background: linear-gradient(90deg, transparent, var(--gold), var(--gold-light), var(--gold), transparent);
            margin: 12px auto;
            border-radius: 10px;
        }
        .section-sub {
            text-align: center;
            color: var(--text-secondary);
            margin-bottom: 30px;
            font-size: 1em;
        }

        /* ============ الفلاتر ============ */
        .filter-bar {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            justify-content: center;
            margin-bottom: 25px;
        }
        .filter-chip {
            padding: 10px 22px;
            border-radius: 50px;
            border: 1px solid var(--border);
            background: transparent;
            color: var(--text-secondary);
            cursor: pointer;
            font-weight: bold;
            transition: var(--transition);
            font-size: 0.9em;
        }
        .filter-chip.active {
            background: var(--gold);
            color: #1a1a1a;
            border-color: var(--gold);
            box-shadow: 0 5px 20px rgba(212, 168, 83, 0.3);
        }
        .filter-chip:hover {
            border-color: var(--gold);
            color: var(--gold);
        }
        .filter-chip.active:hover {
            color: #1a1a1a;
        }

        /* ============ شبكة المنتجات ============ */
        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(310px, 1fr));
            gap: 25px;
            padding: 10px;
        }
        .product-card {
            background: linear-gradient(160deg, #1a1a1a, #111);
            border-radius: var(--radius);
            overflow: hidden;
            border: 1px solid var(--border);
            transition: var(--transition);
            position: relative;
            cursor: pointer;
            box-shadow: 0 8px 30px rgba(0, 0, 0, 0.4);
        }
        .product-card:hover {
            transform: translateY(-14px);
            border-color: var(--gold);
            box-shadow: 0 25px 60px rgba(212, 168, 83, 0.25), 0 0 50px rgba(212, 168, 83, 0.08);
        }
        .product-card .discount-badge {
            position: absolute;
            top: 15px;
            left: 15px;
            background: var(--red);
            color: #fff;
            padding: 7px 16px;
            border-radius: 20px;
            font-size: 0.8em;
            font-weight: 900;
            z-index: 2;
            animation: badgeGlow 1.5s infinite;
        }
        @keyframes badgeGlow {
            0%,
            100% {
                box-shadow: 0 0 0 0 rgba(255, 71, 87, 0.5);
            }
            50% {
                box-shadow: 0 0 0 18px rgba(255, 71, 87, 0);
            }
        }
        .product-card .wishlist-btn {
            position: absolute;
            top: 15px;
            right: 15px;
            background: rgba(0, 0, 0, 0.7);
            border: none;
            color: #fff;
            width: 42px;
            height: 42px;
            border-radius: 50%;
            cursor: pointer;
            z-index: 2;
            font-size: 1.3em;
            transition: var(--transition);
            display: flex;
            align-items: center;
            justify-content: center;
            backdrop-filter: blur(10px);
        }
        .product-card .wishlist-btn.liked {
            background: var(--pink);
            animation: heartBeat 0.6s;
        }
        @keyframes heartBeat {
            0%,
            100% {
                transform: scale(1);
            }
            30% {
                transform: scale(1.35);
            }
            60% {
                transform: scale(0.9);
            }
        }
        .product-img-wrap {
            width: 100%;
            height: 260px;
            position: relative;
            overflow: hidden;
        }
        .product-img-wrap img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: all 0.7s;
        }
        .product-card:hover .product-img-wrap img {
            transform: scale(1.15) rotate(3deg);
        }
        .product-img-fallback {
            width: 100%;
            height: 260px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 7em;
            background: linear-gradient(135deg, #1a1008, #2a1a10, #0d0502);
        }
        .product-details {
            padding: 20px;
        }
        .product-name {
            font-size: 1.2em;
            font-weight: 900;
            color: var(--text-primary);
            margin-bottom: 6px;
        }
        .product-desc {
            color: #7a6a55;
            font-size: 0.85em;
            margin-bottom: 14px;
            line-height: 1.4;
        }
        .product-bottom {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .product-price-wrap .old-price {
            font-size: 0.8em;
            color: #555;
            text-decoration: line-through;
            margin-left: 6px;
        }
        .product-price-wrap .current-price {
            font-size: 1.5em;
            font-weight: 900;
            color: var(--gold);
        }
        .add-btn {
            background: linear-gradient(135deg, var(--gold-dark), var(--gold));
            color: #1a1a1a;
            border: none;
            padding: 11px 22px;
            border-radius: var(--radius-sm);
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
            font-size: 0.9em;
        }
        .add-btn:hover {
            transform: scale(1.08);
            box-shadow: 0 8px 25px rgba(212, 168, 83, 0.45);
        }
        .add-btn:active {
            transform: scale(0.93);
        }
        .qty-control {
            display: flex;
            align-items: center;
            gap: 12px;
        }
        .qty-btn {
            background: var(--bg-input);
            border: 2px solid var(--gold);
            color: var(--gold);
            width: 36px;
            height: 36px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 1.2em;
            transition: var(--transition);
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .qty-btn:hover {
            background: var(--gold);
            color: #1a1a1a;
            transform: scale(1.15);
        }
        .qty-val {
            font-size: 1.2em;
            font-weight: 900;
            min-width: 30px;
            text-align: center;
        }

        /* ============ مودال السلة ============ */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.92);
            backdrop-filter: blur(15px);
            z-index: 5000;
            display: none;
            justify-content: center;
            align-items: center;
        }
        .modal-overlay.active {
            display: flex;
            animation: fadeIn 0.3s;
        }
        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }
        .modal-dialog {
            background: linear-gradient(160deg, #1a1a1a, #0d0d0d);
            border: 2px solid rgba(212, 168, 83, 0.5);
            border-radius: 28px;
            padding: 35px;
            width: 92%;
            max-width: 700px;
            max-height: 88vh;
            overflow-y: auto;
            position: relative;
            animation: modalPop 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            box-shadow: 0 0 100px rgba(212, 168, 83, 0.2);
        }
        @keyframes modalPop {
            from {
                transform: scale(0.4) translateY(60px);
                opacity: 0;
            }
            to {
                transform: scale(1) translateY(0);
                opacity: 1;
            }
        }
        .modal-close-btn {
            position: absolute;
            top: 18px;
            left: 22px;
            background: none;
            border: none;
            color: var(--gold);
            font-size: 2em;
            cursor: pointer;
            transition: var(--transition);
        }
        .modal-close-btn:hover {
            color: var(--red);
            transform: rotate(90deg) scale(1.3);
        }
        .cart-heading {
            text-align: center;
            color: var(--gold);
            font-size: 2em;
            margin-bottom: 25px;
        }
        .cart-list-item {
            display: flex;
            align-items: center;
            gap: 15px;
            padding: 15px;
            border-bottom: 1px solid #222;
            animation: fadeInUp 0.4s;
        }
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        .cart-item-info {
            flex: 1;
        }
        .cart-item-title {
            font-weight: 900;
            color: var(--text-primary);
        }
        .cart-item-sub {
            color: var(--gold);
            font-size: 0.85em;
        }
        .cart-remove-btn {
            background: var(--red);
            color: #fff;
            border: none;
            padding: 8px 16px;
            border-radius: 10px;
            cursor: pointer;
            transition: var(--transition);
        }
        .cart-remove-btn:hover {
            background: #d63031;
            transform: scale(1.1);
        }
        .cart-summary {
            text-align: center;
            font-size: 1.8em;
            font-weight: 900;
            color: var(--gold);
            margin: 20px 0;
            text-shadow: 0 0 35px rgba(212, 168, 83, 0.5);
        }
        .payment-methods {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            justify-content: center;
            margin: 20px 0;
        }
        .payment-option {
            background: var(--bg-input);
            border: 2px solid transparent;
            padding: 15px 18px;
            border-radius: var(--radius-sm);
            cursor: pointer;
            text-align: center;
            font-size: 2em;
            transition: var(--transition);
            flex: 1;
            min-width: 100px;
        }
        .payment-option.selected {
            border-color: var(--gold);
            background: #1a1008;
            box-shadow: 0 0 30px rgba(212, 168, 83, 0.3);
        }
        .payment-option span {
            display: block;
            font-size: 0.3em;
            margin-top: 5px;
            color: var(--text-primary);
        }
        .btn-checkout {
            width: 100%;
            padding: 18px;
            background: linear-gradient(135deg, #2ed573, #1dd1a1);
            color: #000;
            border: none;
            border-radius: var(--radius-sm);
            font-size: 1.3em;
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
            letter-spacing: 2px;
        }
        .btn-checkout:hover {
            transform: translateY(-4px);
            box-shadow: 0 15px 45px rgba(46, 213, 115, 0.4);
        }

        /* ============ مودال المصادقة ============ */
        .auth-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.95);
            backdrop-filter: blur(20px);
            z-index: 6000;
            display: none;
            justify-content: center;
            align-items: center;
        }
        .auth-overlay.active {
            display: flex;
        }
        .auth-dialog {
            background: linear-gradient(160deg, #1a1a1a, #0d0d0d);
            border: 2px solid rgba(212, 168, 83, 0.5);
            border-radius: 28px;
            padding: 40px;
            width: 92%;
            max-width: 500px;
            animation: modalPop 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            box-shadow: 0 0 100px rgba(212, 168, 83, 0.2);
        }
        .auth-dialog h2 {
            text-align: center;
            color: var(--gold);
            font-size: 2em;
            margin-bottom: 25px;
        }
        .auth-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
        }
        .auth-tab {
            flex: 1;
            padding: 12px;
            background: transparent;
            border: 2px solid rgba(212, 168, 83, 0.35);
            color: var(--gold);
            border-radius: var(--radius-sm);
            cursor: pointer;
            font-weight: 900;
            transition: var(--transition);
        }
        .auth-tab.active {
            background: var(--gold);
            color: #1a1a1a;
            border-color: var(--gold);
        }
        .form-group {
            margin-bottom: 16px;
        }
        .form-group label {
            display: block;
            color: var(--gold);
            margin-bottom: 6px;
            font-weight: bold;
        }
        .form-group input {
            width: 100%;
            padding: 14px 18px;
            background: var(--bg-input);
            border: 2px solid #2a2a2a;
            border-radius: var(--radius-sm);
            color: var(--text-primary);
            font-size: 1em;
            transition: var(--transition);
            font-family: inherit;
        }
        .form-group input:focus {
            outline: none;
            border-color: var(--gold);
            box-shadow: 0 0 20px rgba(212, 168, 83, 0.2);
        }
        .btn-auth {
            width: 100%;
            padding: 16px;
            background: linear-gradient(135deg, var(--gold-dark), var(--gold));
            color: #1a1a1a;
            border: none;
            border-radius: var(--radius-sm);
            font-size: 1.2em;
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
        }
        .btn-auth:hover {
            transform: translateY(-3px);
            box-shadow: var(--shadow-gold);
        }
        .error-msg {
            color: var(--red);
            text-align: center;
            margin-top: 10px;
            display: none;
            font-weight: bold;
        }
        .success-msg {
            color: var(--green);
            text-align: center;
            margin-top: 10px;
            display: none;
            font-weight: bold;
        }

        /* ============ لوحة تحكم المطور ============ */
        .dev-dashboard {
            display: none;
            background: linear-gradient(160deg, #0d0d0d, #1a1a1a);
            border: 2px solid var(--purple);
            border-radius: 25px;
            padding: 30px;
            margin: 30px 0;
            animation: fadeInUp 0.6s;
        }
        .dev-dashboard.active {
            display: block;
        }
        .dev-dashboard h2 {
            color: var(--purple);
            text-align: center;
            font-size: 1.8em;
            margin-bottom: 25px;
        }
        .dev-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(340px, 1fr));
            gap: 20px;
        }
        .dev-card {
            background: #141414;
            border: 1px solid #2a2a2a;
            border-radius: 18px;
            padding: 22px;
        }
        .dev-card h3 {
            color: var(--gold);
            text-align: center;
            margin-bottom: 15px;
        }
        .dev-card input,
        .dev-card select,
        .dev-card textarea {
            width: 100%;
            padding: 11px;
            margin-bottom: 10px;
            background: #0d0d0d;
            border: 1px solid #2a2a2a;
            border-radius: 8px;
            color: var(--text-primary);
            font-family: inherit;
            font-size: 0.9em;
            transition: var(--transition);
        }
        .dev-card input:focus,
        .dev-card select:focus {
            outline: none;
            border-color: var(--purple);
        }
        .dev-card button {
            width: 100%;
            padding: 12px;
            border: none;
            border-radius: 10px;
            font-weight: 900;
            cursor: pointer;
            transition: var(--transition);
            margin-top: 5px;
        }
        .btn-add-prod {
            background: var(--green);
            color: #000;
        }
        .btn-del-prod {
            background: var(--red);
            color: #fff;
            width: auto;
            padding: 7px 14px;
            font-size: 0.8em;
        }
        .btn-reset-data {
            background: var(--orange);
            color: #000;
        }
        .btn-export-data {
            background: var(--purple);
            color: #fff;
        }
        .btn-import-data {
            background: var(--blue);
            color: #fff;
        }
        .dev-prod-list {
            max-height: 380px;
            overflow-y: auto;
        }
        .dev-prod-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            border-bottom: 1px solid #1a1a1a;
            font-size: 0.88em;
        }
        .dev-prod-item button {
            width: auto;
            padding: 6px 12px;
            font-size: 0.8em;
        }
        #importFileInput {
            display: none;
        }

        /* ============ الإشعارات ============ */
        .toast-container {
            position: fixed;
            top: 100px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 9999;
            display: flex;
            flex-direction: column;
            gap: 10px;
            align-items: center;
            pointer-events: none;
        }
        .toast {
            background: #1a1a1a;
            border: 1px solid var(--gold);
            color: var(--text-primary);
            padding: 15px 35px;
            border-radius: 50px;
            font-weight: 900;
            animation: toastSlideIn 0.5s, toastSlideOut 0.5s 2.8s forwards;
            white-space: nowrap;
            box-shadow: var(--shadow);
            pointer-events: auto;
        }
        @keyframes toastSlideIn {
            from {
                transform: translateY(-60px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }
        @keyframes toastSlideOut {
            from {
                opacity: 1;
            }
            to {
                opacity: 0;
                transform: translateY(-40px);
            }
        }

        /* ============ أزرار عائمة ============ */
        .float-actions {
            position: fixed;
            bottom: 30px;
            left: 30px;
            display: flex;
            flex-direction: column;
            gap: 12px;
            z-index: 100;
        }
        .float-btn {
            width: 55px;
            height: 55px;
            border-radius: 50%;
            border: none;
            cursor: pointer;
            font-size: 1.5em;
            transition: var(--transition);
            box-shadow: var(--shadow);
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .float-btn:hover {
            transform: scale(1.18);
        }
        .float-whatsapp {
            background: #25D366;
            color: #fff;
            animation: floatGlow 2s infinite;
        }
        @keyframes floatGlow {
            0%,
            100% {
                box-shadow: 0 0 0 0 rgba(37, 211, 102, 0.5);
            }
            50% {
                box-shadow: 0 0 0 22px rgba(37, 211, 102, 0);
            }
        }
        .float-dev {
            background: linear-gradient(135deg, #6c5ce7, #a55eea);
            color: #fff;
            font-size: 1.2em;
            font-weight: 900;
        }
        .float-cart {
            background: var(--gold);
            color: #1a1a1a;
            display: none;
        }
        .float-cart.visible {
            display: flex;
            animation: bounceIn 0.5s;
        }
        @keyframes bounceIn {
            0% {
                transform: scale(0);
            }
            60% {
                transform: scale(1.25);
            }
            100% {
                transform: scale(1);
            }
        }
        .float-theme {
            background: #333;
            color: #fff;
            font-size: 1.2em;
        }

        /* ============ الفوتر ============ */
        .site-footer {
            text-align: center;
            padding: 50px 20px;
            background: #050505;
            border-top: 1px solid rgba(212, 168, 83, 0.15);
            margin-top: 70px;
            position: relative;
            z-index: 1;
        }
        .site-footer h3 {
            color: var(--gold);
            font-size: 2em;
            margin-bottom: 10px;
        }
        .site-footer .phone-display {
            color: var(--gold);
            font-size: 1.4em;
            margin: 10px 0;
            direction: ltr;
            display: inline-block;
            font-weight: 900;
        }
        .social-links {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin: 25px 0;
        }
        .social-icon {
            width: 48px;
            height: 48px;
            border-radius: 50%;
            background: #1a1a1a;
            border: 1px solid #2a2a2a;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.3em;
            cursor: pointer;
            transition: var(--transition);
        }
        .social-icon:hover {
            border-color: var(--gold);
            background: var(--gold);
            color: #1a1a1a;
            transform: translateY(-8px);
            box-shadow: var(--shadow-gold);
        }

        /* ============ الوضع الفاتح ============ */
        body.light-mode {
            --bg-primary: #fafafa;
            --bg-secondary: #f0f0f0;
            --bg-card: #fff;
            --bg-input: #f5f5f5;
            --text-primary: #1a1a1a;
            --text-secondary: #666;
            --border: #e0e0e0;
            --border-gold: rgba(180, 140, 50, 0.3);
        }
        body.light-mode .navbar {
            background: rgba(255, 255, 255, 0.9);
        }
        body.light-mode .product-card {
            background: #fff;
            border-color: #e0e0e0;
        }
        body.light-mode .modal-dialog,
        body.light-mode .auth-dialog {
            background: #fff;
        }
        body.light-mode .toast {
            background: #fff;
            color: #1a1a1a;
        }

        /* ============ Responsive ============ */
        @media (max-width: 768px) {
            .navbar {
                flex-wrap: wrap;
                gap: 8px;
                justify-content: center;
                padding: 10px;
            }
            .nav-btn {
                padding: 8px 14px;
                font-size: 0.78em;
            }
            .hero-title {
                font-size: 2em;
            }
            .products-grid {
                grid-template-columns: 1fr 1fr;
                gap: 14px;
            }
            .product-img-wrap,
            .product-img-fallback {
                height: 170px;
            }
            .product-img-fallback {
                font-size: 4em;
            }
            .section-head {
                font-size: 1.5em;
            }
            .stats-row {
                gap: 12px;
            }
            .stat-item {
                padding: 15px 20px;
            }
            .stat-num {
                font-size: 2em;
            }
            .modal-dialog {
                padding: 20px;
            }
            .dev-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700;900&display=swap" rel="stylesheet">
</head>
<body>

    <!-- مؤشر مخصص -->
    <div class="cursor-glow" id="cursorGlow"></div>
    <div class="cursor-dot-inner" id="cursorDot"></div>

    <!-- شاشة التحميل -->
    <div class="splash-screen" id="splashScreen">
        <div class="splash-logo">☕</div>
        <div class="splash-title">كافيه مصطفى</div>
        <div class="splash-progress"><div class="splash-progress-bar"></div></div>
    </div>

    <!-- جسيمات -->
    <canvas id="particleCanvas"></canvas>

    <!-- النافبار -->
    <nav class="navbar" id="navbar">
        <div class="logo-wrap" onclick="scrollToTop()">
            <span class="logo-ico">☕</span>
            <span class="logo-txt">كافيه مصطفى</span>
        </div>
        <div class="nav-actions">
            <button class="nav-btn" onclick="scrollToSection('drinksSection')">🥤 مشروبات</button>
            <button class="nav-btn" onclick="scrollToSection('foodSection')">🍽️ مأكولات</button>
            <button class="nav-btn" onclick="scrollToSection('offersSection')">🎁 عروض</button>
            <button class="nav-btn" onclick="scrollToSection('paymentSection')">💳 دفع</button>
            <button class="nav-user-btn" id="navUserBtn" onclick="toggleAuth()">👤 دخول</button>
            <button class="nav-cart-btn" onclick="openCart()">
                🛒 السلة <span class="cart-badge" id="cartBadge">0</span>
            </button>
        </div>
    </nav>

    <!-- المحتوى -->
    <div class="main-wrap">

        <!-- الهيرو -->
        <div class="hero-section">
            <h1 class="hero-title">☕ كافيه مصطفى</h1>
            <p class="hero-desc">أجود أنواع القهوة والمأكولات الطازجة يومياً - اطلب أونلاين واستمتع بأفضل تجربة مع خدمة توصيل سريعة</p>
            <div class="hero-search">
                <input type="text" id="searchInput" placeholder="🔍 ابحث عن منتج...">
                <button onclick="searchProducts()">بحث</button>
            </div>
            <div class="stats-row">
                <div class="stat-item"><span class="stat-num" id="statTotal">0</span><span class="stat-label">منتج</span></div>
                <div class="stat-item"><span class="stat-num">5</span><span class="stat-label">طرق دفع</span></div>
                <div class="stat-item"><span class="stat-num">24/7</span><span class="stat-label">خدمة</span></div>
                <div class="stat-item"><span class="stat-num">⭐4.9</span><span class="stat-label">تقييم</span></div>
            </div>
        </div>

        <!-- المشروبات -->
        <div id="drinksSection">
            <h2 class="section-head">🥤 المشروبات</h2>
            <p class="section-sub">مشروبات ساخنة وباردة بأيدي أمهر الباريستا</p>
            <div class="filter-bar" id="drinksFilter"></div>
            <div class="products-grid" id="drinksGrid"></div>
        </div>

        <!-- المأكولات -->
        <div id="foodSection">
            <h2 class="section-head">🍽️ المأكولات والحلويات</h2>
            <p class="section-sub">مأكولات طازجة يومياً بأفضل المكونات</p>
            <div class="filter-bar" id="foodFilter"></div>
            <div class="products-grid" id="foodGrid"></div>
        </div>

        <!-- العروض -->
        <div id="offersSection">
            <h2 class="section-head">🎁 العروض والخصومات</h2>
            <p class="section-sub">عروض حصرية لمدة محدودة - لا تفوتها!</p>
            <div class="products-grid" id="offersGrid"></div>
        </div>

        <!-- طرق الدفع -->
        <div id="paymentSection">
            <h2 class="section-head">💳 طرق الدفع الآمنة</h2>
            <div style="display:flex;flex-wrap:wrap;gap:15px;justify-content:center;padding:20px;">
                <div class="payment-option" style="font-size:2.5em;padding:25px;flex:1;min-width:120px;">💵<span>نقداً</span></div>
                <div class="payment-option" style="font-size:2.5em;padding:25px;flex:1;min-width:120px;">📱<span>فودافون كاش</span></div>
                <div class="payment-option" style="font-size:2.5em;padding:25px;flex:1;min-width:120px;">🏦<span>تحويل بنكي</span></div>
                <div class="payment-option" style="font-size:2.5em;padding:25px;flex:1;min-width:120px;">💳<span>بطاقة ائتمان</span></div>
                <div class="payment-option" style="font-size:2.5em;padding:25px;flex:1;min-width:120px;">📲<span>محفظة رقمية</span></div>
            </div>
        </div>

        <!-- لوحة المطور -->
        <div class="dev-dashboard" id="devDashboard">
            <h2>👑 لوحة تحكم المطور - Mustafa</h2>
            <div class="dev-grid">
                <div class="dev-card">
                    <h3>➕ إضافة منتج جديد</h3>
                    <select id="devCategory">
                        <option value="drinks">🥤 مشروبات</option>
                        <option value="food">🍽️ مأكولات</option>
                        <option value="offers">🎁 عروض</option>
                    </select>
                    <input type="text" id="devName" placeholder="اسم المنتج">
                    <input type="text" id="devDesc" placeholder="وصف المنتج">
                    <input type="number" id="devPrice" placeholder="السعر (ج.م)">
                    <input type="number" id="devOldPrice" placeholder="السعر قبل الخصم (اختياري)">
                    <input type="text" id="devEmoji" placeholder="إيموجي (☕ 🍰)">
                    <input type="text" id="devImage" placeholder="رابط الصورة">
                    <button class="btn-add-prod" onclick="devAddProduct()">✅ إضافة المنتج</button>
                </div>
                <div class="dev-card">
                    <h3>📋 إدارة المنتجات</h3>
                    <div class="dev-prod-list" id="devProductList"></div>
                </div>
                <div class="dev-card">
                    <h3>⚙️ أدوات متقدمة</h3>
                    <p style="color:var(--gold);">🥤 مشروبات: <b id="devStatDrinks">0</b></p>
                    <p style="color:var(--gold);">🍽️ مأكولات: <b id="devStatFood">0</b></p>
                    <p style="color:var(--gold);">🎁 عروض: <b id="devStatOffers">0</b></p>
                    <hr style="border-color:#222;margin:12px 0;">
                    <button class="btn-reset-data" onclick="devResetAll()">🔄 إعادة ضبط البيانات</button>
                    <button class="btn-export-data" onclick="devExportJSON()">📤 تصدير البيانات</button>
                    <button class="btn-import-data" onclick="document.getElementById('importFileInput').click()">📥 استيراد البيانات</button>
                    <input type="file" id="importFileInput" accept=".json" onchange="devImportJSON(event)">
                </div>
            </div>
        </div>
    </div>

    <!-- مودال السلة -->
    <div class="modal-overlay" id="cartModal">
        <div class="modal-dialog">
            <button class="modal-close-btn" onclick="closeCart()">✕</button>
            <h2 class="cart-heading">🛒 سلة المشتريات</h2>
            <div id="cartItemsContainer"></div>
            <div class="cart-summary" id="cartTotal">الإجمالي: 0 ج.م</div>
            <p style="text-align:center;color:var(--gold);">اختر طريقة الدفع:</p>
            <div class="payment-methods" id="paymentMethodsContainer">
                <div class="payment-option selected" onclick="selectPayment('cash', this)">💵<span>نقداً</span></div>
                <div class="payment-option" onclick="selectPayment('vodafone', this)">📱<span>فودافون كاش</span></div>
                <div class="payment-option" onclick="selectPayment('bank', this)">🏦<span>تحويل بنكي</span></div>
            </div>
            <button class="btn-checkout" onclick="checkoutOrder()">✅ تأكيد الطلب وإرسال واتساب</button>
        </div>
    </div>

    <!-- مودال المصادقة -->
    <div class="auth-overlay" id="authOverlay">
        <div class="auth-dialog">
            <h2>🔐 حساب المستخدم</h2>
            <div class="auth-tabs">
                <button class="auth-tab active" onclick="switchAuthTab('login')">تسجيل الدخول</button>
                <button class="auth-tab" onclick="switchAuthTab('register')">إنشاء حساب</button>
            </div>
            <div id="loginFormBlock">
                <div class="form-group"><label>👤 اسم المستخدم</label><input type="text" id="loginUsername" placeholder="اسم المستخدم"></div>
                <div class="form-group"><label>🔒 كلمة المرور</label><input type="password" id="loginPassword" placeholder="كلمة المرور"></div>
                <div class="error-msg" id="loginError"></div>
                <button class="btn-auth" onclick="handleLogin()">🚪 دخول</button>
            </div>
            <div id="registerFormBlock" style="display:none;">
                <div class="form-group"><label>👤 اسم المستخدم</label><input type="text" id="regUsername" placeholder="اختر اسم مستخدم"></div>
                <div class="form-group"><label>📧 البريد الإلكتروني</label><input type="email" id="regEmail" placeholder="بريدك الإلكتروني"></div>
                <div class="form-group"><label>🔒 كلمة المرور</label><input type="password" id="regPassword" placeholder="كلمة مرور قوية (6+ أحرف)"></div>
                <div class="form-group"><label>🔒 تأكيد كلمة المرور</label><input type="password" id="regPasswordConfirm" placeholder="أعد كتابة كلمة المرور"></div>
                <div class="error-msg" id="regError"></div>
                <div class="success-msg" id="regSuccess"></div>
                <button class="btn-auth" onclick="handleRegister()">📝 إنشاء حساب</button>
            </div>
            <button style="width:100%;margin-top:15px;padding:12px;background:transparent;border:1px solid #333;color:#888;border-radius:10px;cursor:pointer;" onclick="closeAuth()">✕ إغلاق</button>
        </div>
    </div>

    <!-- أزرار عائمة -->
    <div class="float-actions">
        <button class="float-btn float-whatsapp" onclick="openWhatsApp()" title="واتساب">💬</button>
        <button class="float-btn float-dev" id="floatDevBtn" onclick="toggleDevDashboard()" title="لوحة المطور">👑</button>
        <button class="float-btn float-cart" id="floatCartBtn" onclick="openCart()" title="السلة">🛒</button>
        <button class="float-btn float-theme" id="floatThemeBtn" onclick="toggleTheme()" title="تغيير الوضع">🌓</button>
    </div>

    <!-- توست -->
    <div class="toast-container" id="toastContainer"></div>

    <!-- فوتر -->
    <div class="site-footer">
        <h3>☕ كافيه مصطفى</h3>
        <p style="color:var(--text-secondary);">📍 شارع النخيل، مدينة القهوة</p>
        <p class="phone-display">📞 01026966717</p>
        <div class="social-links">
            <div class="social-icon">📘</div>
            <div class="social-icon">📷</div>
            <div class="social-icon">🐦</div>
            <div class="social-icon">📱</div>
        </div>
        <p style="color:#555;margin-top:20px;">© 2026 كافيه مصطفى - جميع الحقوق محفوظة</p>
        <p style="color:#444;font-size:0.8em;">Developed with ❤️ by Mustafa 👑</p>
    </div>

    <script>
        // ==================== الإعدادات والثوابت ====================
        const WHATSAPP_NUMBER = '201026966717';
        const PHONE_DISPLAY = '01026966717';
        const DEV_USERNAMES = ['mustafa', 'مصطفى', 'mostafa', 'MUSTAFA'];

        // ==================== حالة التطبيق ====================
        let cafeData = loadCafeData();
        let cart = JSON.parse(localStorage.getItem('MF_CART') || '[]');
        let wishlist = JSON.parse(localStorage.getItem('MF_WISHLIST') || '[]');
        let selectedPayment = 'cash';
        let isDevLoggedIn = localStorage.getItem('MF_DEV_LOGGEDIN') === 'true';
        let currentUser = JSON.parse(localStorage.getItem('MF_CURRENT_USER') || 'null');
        let activeFilters = { drinks: 'all', food: 'all' };

        // ==================== تحميل وحفظ البيانات ====================
        function loadCafeData() {
            const saved = localStorage.getItem('MF_CAFE_D
