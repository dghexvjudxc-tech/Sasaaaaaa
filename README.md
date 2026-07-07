<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>☕ كافيه Evil Bar  - أونلاين</title>
    <style>
        :root {
            --gold: #d4a853;
            --gold2: #f0d78c;
            --gold3: #b8922e;
            --dark: #0a0a0a;
            --dark2: #1a1a1a;
            --dark3: #252525;
            --brown: #1e0f0a;
            --brown2: #2c1810;
            --brown3: #3d2519;
            --cream: #f5e6d0;
            --red: #ff4444;
            --green: #00e676;
            --blue: #448aff;
            --purple: #b388ff;
            --pink: #ff80ab;
            --orange: #ff9100;
            --teal: #1de9b6;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Cairo', 'Segoe UI', Tahoma, sans-serif;
            background: var(--dark);
            color: var(--cream);
            min-height: 100vh;
            overflow-x: hidden;
            cursor: default;
            scroll-behavior: smooth;
        }

        /* مؤشر مخصص */
        .custom-cursor {
            width: 20px;
            height: 20px;
            border: 2px solid var(--gold);
            border-radius: 50%;
            position: fixed;
            pointer-events: none;
            z-index: 99999;
            transition: all 0.1s;
            mix-blend-mode: difference;
        }
        .cursor-dot {
            width: 6px;
            height: 6px;
            background: var(--gold);
            border-radius: 50%;
            position: fixed;
            pointer-events: none;
            z-index: 99999;
            transition: all 0.05s;
        }

        /* جسيمات */
        #particlesCanvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        /* شريط تحميل */
        .loader {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--dark);
            z-index: 99999;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            transition: all 0.8s cubic-bezier(0.77, 0, 0.175, 1);
        }
        .loader.hidden {
            opacity: 0;
            pointer-events: none;
            transform: scale(1.2);
        }
        .loader .coffee-cup {
            font-size: 5em;
            animation: brewCoffee 1.5s infinite;
        }
        @keyframes brewCoffee {
            0%,
            100% {
                transform: rotate(0) scale(1);
            }
            25% {
                transform: rotate(-10deg) scale(1.1);
            }
            50% {
                transform: rotate(0) scale(0.95);
            }
            75% {
                transform: rotate(10deg) scale(1.1);
            }
        }
        .loader .loading-bar {
            width: 250px;
            height: 6px;
            background: #333;
            border-radius: 10px;
            margin-top: 30px;
            overflow: hidden;
        }
        .loader .loading-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--gold3), var(--gold), var(--gold2));
            border-radius: 10px;
            animation: fillBar 1.8s ease-in-out infinite;
        }
        @keyframes fillBar {
            0% {
                width: 0%;
            }
            50% {
                width: 100%;
            }
            100% {
                width: 0%;
            }
        }

        /* نافبار */
        .navbar {
            background: rgba(10, 10, 10, 0.9);
            backdrop-filter: blur(30px);
            -webkit-backdrop-filter: blur(30px);
            border-bottom: 1px solid rgba(212, 168, 83, 0.3);
            padding: 15px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 1000;
            animation: slideDown 0.8s ease-out;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.5);
        }
        @keyframes slideDown {
            from {
                transform: translateY(-100%);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }
        .logo-container {
            display: flex;
            align-items: center;
            gap: 12px;
            cursor: pointer;
            transition: all 0.3s;
        }
        .logo-container:hover {
            transform: scale(1.05);
        }
        .logo-icon {
            font-size: 2.8em;
            animation: logoFloat 3s infinite;
            filter: drop-shadow(0 0 15px rgba(212, 168, 83, 0.6));
        }
        @keyframes logoFloat {
            0%,
            100% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-10px);
            }
        }
        .logo-text {
            font-size: 1.8em;
            font-weight: 900;
            background: linear-gradient(135deg, var(--gold), var(--gold2), var(--gold));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            letter-spacing: 3px;
        }
        .nav-links {
            display: flex;
            gap: 15px;
            align-items: center;
            flex-wrap: wrap;
        }
        .nav-link {
            background: transparent;
            border: 1px solid rgba(212, 168, 83, 0.4);
            color: var(--gold);
            padding: 10px 20px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.4s;
            position: relative;
            overflow: hidden;
            font-size: 0.95em;
        }
        .nav-link::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            background: var(--gold);
            border-radius: 50%;
            transform: translate(-50%, -50%);
            transition: all 0.5s;
            z-index: -1;
        }
        .nav-link:hover::before {
            width: 400px;
            height: 400px;
        }
        .nav-link:hover {
            color: var(--dark);
            border-color: var(--gold);
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(212, 168, 83, 0.3);
        }
        .cart-nav-btn {
            background: linear-gradient(135deg, var(--gold3), var(--gold));
            color: var(--dark);
            border: none;
            padding: 12px 25px;
            border-radius: 50px;
            font-weight: bold;
            cursor: pointer;
            position: relative;
            transition: all 0.3s;
            font-size: 1em;
            box-shadow: 0 5px 20px rgba(212, 168, 83, 0.3);
        }
        .cart-nav-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 35px rgba(212, 168, 83, 0.5);
        }
        .cart-count-badge {
            position: absolute;
            top: -10px;
            right: -10px;
            background: var(--red);
            color: white;
            border-radius: 50%;
            width: 26px;
            height: 26px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.8em;
            font-weight: bold;
            animation: badgePop 0.5s ease-out;
        }
        @keyframes badgePop {
            0% {
                transform: scale(0);
            }
            60% {
                transform: scale(1.3);
            }
            100% {
                transform: scale(1);
            }
        }

        /* هيرو سكشن */
        .hero {
            text-align: center;
            padding: 80px 20px 60px;
            position: relative;
            z-index: 1;
        }
        .hero h1 {
            font-size: 4em;
            font-weight: 900;
            background: linear-gradient(135deg, var(--gold), var(--gold2), var(--cream), var(--gold));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: titleGlow 2s ease-in-out infinite;
            margin-bottom: 20px;
        }
        @keyframes titleGlow {
            0%,
            100% {
                filter: brightness(1);
            }
            50% {
                filter: brightness(1.5);
            }
        }
        .hero p {
            font-size: 1.3em;
            color: #a89070;
            max-width: 700px;
            margin: 0 auto;
            animation: fadeInUp 1s;
        }
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        .hero-stats {
            display: flex;
            justify-content: center;
            gap: 40px;
            margin-top: 40px;
            flex-wrap: wrap;
        }
        .stat-card {
            background: rgba(30, 15, 10, 0.8);
            border: 1px solid rgba(212, 168, 83, 0.3);
            border-radius: 20px;
            padding: 25px 35px;
            text-align: center;
            backdrop-filter: blur(20px);
            transition: all 0.3s;
            cursor: default;
        }
        .stat-card:hover {
            transform: translateY(-10px);
            border-color: var(--gold);
            box-shadow: 0 15px 40px rgba(212, 168, 83, 0.2);
        }
        .stat-number {
            font-size: 3em;
            font-weight: 900;
            color: var(--gold);
        }
        .stat-label {
            color: #a89070;
            margin-top: 5px;
        }

        /* سكشن العناوين */
        .section-container {
            max-width: 1300px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 1;
        }
        .section-title {
            text-align: center;
            font-size: 2.5em;
            font-weight: 900;
            color: var(--gold);
            margin: 50px 0 30px;
            position: relative;
        }
        .section-title::after {
            content: '';
            display: block;
            width: 80px;
            height: 4px;
            background: linear-gradient(90deg, transparent, var(--gold), var(--gold2), var(--gold),
                    transparent);
            margin: 15px auto;
            border-radius: 10px;
        }
        .section-subtitle {
            text-align: center;
            color: #a89070;
            margin-bottom: 30px;
            font-size: 1.1em;
        }

        /* شبكة المنتجات */
        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 25px;
            padding: 10px;
        }
        .product-card {
            background: linear-gradient(145deg, #1a1512, #0d0a08);
            border-radius: 25px;
            overflow: hidden;
            border: 1px solid #2a2018;
            transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            position: relative;
            cursor: pointer;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4);
        }
        .product-card:hover {
            transform: translateY(-15px);
            border-color: var(--gold);
            box-shadow: 0 25px 60px rgba(212, 168, 83, 0.3), 0 0 50px rgba(212, 168, 83, 0.1);
        }
        .product-card .card-badge {
            position: absolute;
            top: 15px;
            left: 15px;
            background: var(--red);
            color: white;
            padding: 6px 18px;
            border-radius: 20px;
            font-size: 0.8em;
            font-weight: bold;
            z-index: 2;
            animation: badgePulse 1.5s infinite;
        }
        @keyframes badgePulse {
            0%,
            100% {
                box-shadow: 0 0 0 0 rgba(255, 68, 68, 0.5);
            }
            50% {
                box-shadow: 0 0 0 15px rgba(255, 68, 68, 0);
            }
        }
        .product-card .wishlist-btn {
            position: absolute;
            top: 15px;
            right: 15px;
            background: rgba(0, 0, 0, 0.6);
            border: none;
            color: white;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            cursor: pointer;
            z-index: 2;
            font-size: 1.3em;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .product-card .wishlist-btn:hover {
            background: var(--pink);
            transform: scale(1.2);
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
                transform: scale(1.3);
            }
            60% {
                transform: scale(0.9);
            }
        }
        .product-image-container {
            width: 100%;
            height: 250px;
            position: relative;
            overflow: hidden;
        }
        .product-image-container img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: all 0.6s;
        }
        .product-card:hover .product-image-container img {
            transform: scale(1.15) rotate(2deg);
        }
        .product-image-placeholder {
            width: 100%;
            height: 250px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 6em;
            background: linear-gradient(135deg, #2a1508, #3d2519, #1a0a02);
        }
        .product-info {
            padding: 20px;
            position: relative;
        }
        .product-name {
            font-size: 1.3em;
            font-weight: bold;
            color: var(--cream);
            margin-bottom: 8px;
        }
        .product-desc {
            color: #8a7560;
            font-size: 0.9em;
            margin-bottom: 15px;
            line-height: 1.5;
        }
        .product-price-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .product-price {
            font-size: 1.6em;
            font-weight: 900;
            color: var(--gold);
        }
        .product-old-price {
            font-size: 0.8em;
            color: #666;
            text-decoration: line-through;
            margin-right: 8px;
        }
        .add-btn {
            background: linear-gradient(135deg, var(--gold3), var(--gold));
            color: var(--dark);
            border: none;
            padding: 12px 25px;
            border-radius: 15px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 1em;
        }
        .add-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 8px 25px rgba(212, 168, 83, 0.4);
        }
        .add-btn:active {
            transform: scale(0.95);
        }
        .quantity-row {
            display: flex;
            align-items: center;
            gap: 12px;
            justify-content: center;
            margin-top: 10px;
        }
        .qty-btn {
            background: var(--dark3);
            border: 2px solid var(--gold);
            color: var(--gold);
            width: 38px;
            height: 38px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 1.3em;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .qty-btn:hover {
            background: var(--gold);
            color: var(--dark);
            transform: scale(1.1);
        }
        .qty-value {
            font-size: 1.3em;
            font-weight: bold;
            min-width: 30px;
            text-align: center;
        }

        /* مودال السلة */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            backdrop-filter: blur(10px);
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
        .modal-box {
            background: linear-gradient(160deg, #1a1512, #0d0a08);
            border: 2px solid rgba(212, 168, 83, 0.5);
            border-radius: 30px;
            padding: 35px;
            width: 90%;
            max-width: 650px;
            max-height: 85vh;
            overflow-y: auto;
            position: relative;
            animation: modalIn 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            box-shadow: 0 0 80px rgba(212, 168, 83, 0.25);
        }
        @keyframes modalIn {
            from {
                transform: scale(0.5) translateY(50px);
                opacity: 0;
            }
            to {
                transform: scale(1) translateY(0);
                opacity: 1;
            }
        }
        .modal-close {
            position: absolute;
            top: 15px;
            left: 20px;
            background: none;
            border: none;
            color: var(--gold);
            font-size: 2em;
            cursor: pointer;
            transition: all 0.4s;
        }
        .modal-close:hover {
            color: var(--red);
            transform: rotate(90deg) scale(1.3);
        }
        .cart-title {
            text-align: center;
            color: var(--gold);
            font-size: 2em;
            margin-bottom: 25px;
        }
        .cart-item {
            display: flex;
            align-items: center;
            gap: 15px;
            padding: 15px;
            border-bottom: 1px solid #2a2018;
            animation: fadeInUp 0.4s;
        }
        .cart-item-info {
            flex: 1;
        }
        .cart-item-name {
            font-weight: bold;
            color: var(--cream);
        }
        .cart-item-price {
            color: var(--gold);
            font-size: 0.9em;
        }
        .cart-item-remove {
            background: var(--red);
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s;
        }
        .cart-item-remove:hover {
            background: #d32f2f;
            transform: scale(1.1);
        }
        .cart-total {
            text-align: center;
            font-size: 1.7em;
            font-weight: 900;
            color: var(--gold);
            margin: 20px 0;
            text-shadow: 0 0 30px rgba(212, 168, 83, 0.5);
        }
        .payment-options {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            justify-content: center;
            margin: 20px 0;
        }
        .payment-opt {
            background: #1a1512;
            border: 2px solid transparent;
            padding: 15px 20px;
            border-radius: 15px;
            cursor: pointer;
            text-align: center;
            font-size: 2em;
            transition: all 0.3s;
            flex: 1;
            min-width: 100px;
        }
        .payment-opt.selected {
            border-color: var(--gold);
            background: #2a1508;
            box-shadow: 0 0 25px rgba(212, 168, 83, 0.3);
        }
        .payment-opt span {
            display: block;
            font-size: 0.3em;
            margin-top: 5px;
        }
        .btn-checkout {
            width: 100%;
            padding: 18px;
            background: linear-gradient(135deg, var(--green), #00c853);
            color: #000;
            border: none;
            border-radius: 15px;
            font-size: 1.3em;
            font-weight: 900;
            cursor: pointer;
            transition: all 0.3s;
            letter-spacing: 1px;
        }
        .btn-checkout:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 40px rgba(0, 230, 118, 0.4);
        }

        /* مودال المصادقة */
        .auth-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.95);
            backdrop-filter: blur(15px);
            z-index: 6000;
            display: none;
            justify-content: center;
            align-items: center;
        }
        .auth-overlay.active {
            display: flex;
        }
        .auth-box {
            background: linear-gradient(160deg, #1a1512, #0d0a08);
            border: 2px solid rgba(212, 168, 83, 0.6);
            border-radius: 30px;
            padding: 40px;
            width: 90%;
            max-width: 500px;
            animation: modalIn 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            box-shadow: 0 0 100px rgba(212, 168, 83, 0.3);
        }
        .auth-box h2 {
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
            border: 2px solid rgba(212, 168, 83, 0.4);
            color: var(--gold);
            border-radius: 12px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
        }
        .auth-tab.active {
            background: var(--gold);
            color: var(--dark);
            border-color: var(--gold);
        }
        .form-group {
            margin-bottom: 18px;
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
            background: #1a1512;
            border: 2px solid #2a2018;
            border-radius: 12px;
            color: var(--cream);
            font-size: 1em;
            transition: all 0.3s;
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
            background: linear-gradient(135deg, var(--gold3), var(--gold));
            color: var(--dark);
            border: none;
            border-radius: 12px;
            font-size: 1.2em;
            font-weight: 900;
            cursor: pointer;
            transition: all 0.3s;
        }
        .btn-auth:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 30px rgba(212, 168, 83, 0.4);
        }
        .msg-error {
            color: var(--red);
            text-align: center;
            margin-top: 10px;
            display: none;
        }
        .msg-success {
            color: var(--green);
            text-align: center;
            margin-top: 10px;
            display: none;
        }

        /* لوحة تحكم المطور */
        .dev-panel {
            display: none;
            background: linear-gradient(160deg, #0d0a08, #1a1512);
            border: 2px solid var(--purple);
            border-radius: 25px;
            padding: 30px;
            margin: 30px 0;
            animation: fadeInUp 0.6s;
        }
        .dev-panel.active {
            display: block;
        }
        .dev-panel h2 {
            color: var(--purple);
            text-align: center;
            font-size: 1.8em;
            margin-bottom: 20px;
        }
        .dev-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 20px;
        }
        .dev-card {
            background: #1a1512;
            border: 1px solid #2a2018;
            border-radius: 18px;
            padding: 20px;
        }
        .dev-card h3 {
            color: var(--gold);
            margin-bottom: 15px;
            text-align: center;
        }
        .dev-card input,
        .dev-card select,
        .dev-card textarea {
            width: 100%;
            padding: 10px;
            margin-bottom: 10px;
            background: #0d0a08;
            border: 1px solid #2a2018;
            border-radius: 8px;
            color: var(--cream);
            font-family: inherit;
            font-size: 0.9em;
        }
        .dev-card button {
            width: 100%;
            padding: 12px;
            border: none;
            border-radius: 10px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            margin-top: 5px;
        }
        .btn-add-product {
            background: var(--green);
            color: #000;
        }
        .btn-delete {
            background: var(--red);
            color: white;
        }
        .btn-reset {
            background: var(--orange);
            color: #000;
        }
        .btn-dev {
            background: var(--purple);
            color: white;
        }
        .dev-product-list {
            max-height: 350px;
            overflow-y: auto;
        }
        .dev-product-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            border-bottom: 1px solid #1a1512;
            font-size: 0.9em;
        }
        .dev-product-item button {
            width: auto;
            padding: 6px 12px;
            font-size: 0.8em;
        }

        /* أزرار عائمة */
        .float-btns {
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
            transition: all 0.3s;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.4);
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .float-btn:hover {
            transform: scale(1.15);
        }
        .float-btn.whatsapp {
            background: #25D366;
            color: white;
            animation: floatPulse 2s infinite;
        }
        @keyframes floatPulse {
            0%,
            100% {
                box-shadow: 0 0 0 0 rgba(37, 211, 102, 0.5);
            }
            50% {
                box-shadow: 0 0 0 20px rgba(37, 211, 102, 0);
            }
        }
        .float-btn.dev-btn {
            background: linear-gradient(135deg, #6a1b9a, #9c27b0);
            color: white;
            font-size: 1.2em;
            font-weight: bold;
        }
        .float-btn.cart-float {
            background: var(--gold);
            color: var(--dark);
            display: none;
        }
        .float-btn.cart-float.show {
            display: flex;
            animation: bounceIn 0.5s;
        }
        @keyframes bounceIn {
            0% {
                transform: scale(0);
            }
            60% {
                transform: scale(1.2);
            }
            100% {
                transform: scale(1);
            }
        }

        /* توست */
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
        }
        .toast {
            background: #1a1512;
            border: 1px solid var(--gold);
            color: var(--cream);
            padding: 15px 30px;
            border-radius: 50px;
            font-weight: bold;
            animation: toastIn 0.5s, toastOut 0.5s 2.5s forwards;
            white-space: nowrap;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
        }
        @keyframes toastIn {
            from {
                transform: translateY(-50px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }
        @keyframes toastOut {
            from {
                opacity: 1;
            }
            to {
                opacity: 0;
                transform: translateY(-30px);
            }
        }

        /* فوتر */
        .footer {
            text-align: center;
            padding: 50px 20px;
            background: #0a0502;
            border-top: 1px solid rgba(212, 168, 83, 0.2);
            margin-top: 60px;
            position: relative;
            z-index: 1;
        }
        .footer h3 {
            color: var(--gold);
            font-size: 2em;
            margin-bottom: 15px;
        }
        .footer .social-icons {
            display: flex;
            justify-content: center;
            gap: 18px;
            margin: 25px 0;
        }
        .footer .social-icon {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: #1a1512;
            border: 1px solid #2a2018;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.4em;
            cursor: pointer;
            transition: all 0.3s;
        }
        .footer .social-icon:hover {
            border-color: var(--gold);
            background: var(--gold);
            color: var(--dark);
            transform: translateY(-8px);
            box-shadow: 0 10px 30px rgba(212, 168, 83, 0.3);
        }
        .footer .phone-number {
            color: var(--gold);
            font-size: 1.3em;
            margin: 10px 0;
            direction: ltr;
            display: inline-block;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .hero h1 {
                font-size: 2.2em;
            }
            .products-grid {
                grid-template-columns: 1fr 1fr;
                gap: 12px;
            }
            .product-image-container,
            .product-image-placeholder {
                height: 160px;
            }
            .navbar {
                flex-wrap: wrap;
                gap: 10px;
                justify-content: center;
                padding: 10px;
            }
            .nav-links {
                gap: 8px;
            }
            .nav-link {
                padding: 8px 14px;
                font-size: 0.8em;
            }
            .section-title {
                font-size: 1.6em;
            }
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700;900&display=swap" rel="stylesheet">
</head>
<body>

    <!-- مؤشر مخصص -->
    <div class="custom-cursor" id="customCursor"></div>
    <div class="cursor-dot" id="cursorDot"></div>

    <!-- شريط التحميل -->
    <div class="loader" id="loader">
        <div class="coffee-cup">☕</div>
        <p style="color:var(--gold);margin-top:15px;font-weight:bold;">كافيه مصطفى</p>
        <div class="loading-bar"><div class="loading-fill"></div></div>
    </div>

    <!-- جسيمات كانفاس -->
    <canvas id="particlesCanvas"></canvas>

    <!-- نافبار -->
    <nav class="navbar">
        <div class="logo-container" onclick="scrollToTop()">
            <span class="logo-icon">☕</span>
            <span class="logo-text">كافيه مصطفى</span>
        </div>
        <div class="nav-links">
            <button class="nav-link" onclick="scrollToSection('drinks')">🥤 المشروبات</button>
            <button class="nav-link" onclick="scrollToSection('food')">🍽️ المأكولات</button>
            <button class="nav-link" onclick="scrollToSection('payment')">💳 الدفع</button>
            <button class="nav-link" onclick="scrollToSection('offers')">🎁 العروض</button>
            <button class="cart-nav-btn" onclick="openCart()">
                🛒 السلة <span class="cart-count-badge" id="cartBadge" style="display:none;">0</span>
            </button>
        </div>
    </nav>

    <!-- هيرو -->
    <div class="hero">
        <h1>☕ كافيه مصطفى</h1>
        <p>أجود أنواع القهوة والمأكولات الطازجة - اطلب أونلاين واستمتع بأفضل تجربة</p>
        <div class="hero-stats">
            <div class="stat-card"><div class="stat-number" id="totalProductsStat">0</div><div class="stat-label">منتج</div></div>
            <div class="stat-card"><div class="stat-number">5</div><div class="stat-label">طرق دفع</div></div>
            <div class="stat-card"><div class="stat-number">24/7</div><div class="stat-label">خدمة</div></div>
            <div class="stat-card"><div class="stat-number">⭐4.9</div><div class="stat-label">تقييم</div></div>
        </div>
    </div>

    <!-- المحتوى -->
    <div class="section-container">
        <!-- المشروبات -->
        <div id="drinks">
            <h2 class="section-title">🥤 المشروبات الساخنة والباردة</h2>
            <p class="section-subtitle">أفضل المشروبات المحضرة بأيدي أمهر الباريستا</p>
            <div class="products-grid" id="drinksGrid"></div>
        </div>

        <!-- المأكولات -->
        <div id="food">
            <h2 class="section-title">🍽️ المأكولات والحلويات</h2>
            <p class="section-subtitle">مأكولات طازجة يومياً بأفضل المكونات</p>
            <div class="products-grid" id="foodGrid"></div>
        </div>

        <!-- العروض -->
        <div id="offers">
            <h2 class="section-title">🎁 العروض الخاصة</h2>
            <p class="section-subtitle">عروض حصرية لمدة محدودة</p>
            <div class="products-grid" id="offersGrid"></div>
        </div>

        <!-- طرق الدفع -->
        <div id="payment">
            <h2 class="section-title">💳 طرق الدفع</h2>
            <div style="display:flex;flex-wrap:wrap;gap:15px;justify-content:center;padding:20px;">
                <div class="payment-opt" style="font-size:3em;padding:30px;flex:1;min-width:130px;">💵<span>نقداً</span></div>
                <div class="payment-opt" style="font-size:3em;padding:30px;flex:1;min-width:130px;">📱<span>فودافون كاش</span></div>
                <div class="payment-opt" style="font-size:3em;padding:30px;flex:1;min-width:130px;">🏦<span>تحويل بنكي</span></div>
                <div class="payment-opt" style="font-size:3em;padding:30px;flex:1;min-width:130px;">💳<span>بطاقة ائتمان</span></div>
                <div class="payment-opt" style="font-size:3em;padding:30px;flex:1;min-width:130px;">📲<span>محفظة</span></div>
            </div>
        </div>

        <!-- لوحة تحكم المطور -->
        <div class="dev-panel" id="devPanel">
            <h2>👑 لوحة تحكم المطور - مصطفى فقط</h2>
            <div class="dev-grid">
                <div class="dev-card">
                    <h3>➕ إضافة منتج</h3>
                    <select id="devCat">
                        <option value="drinks">مشروبات</option>
                        <option value="food">مأكولات</option>
                        <option value="offers">عروض</option>
                    </select>
                    <input type="text" id="devName" placeholder="اسم المنتج">
                    <input type="text" id="devDesc" placeholder="الوصف">
                    <input type="number" id="devPrice" placeholder="السعر">
                    <input type="number" id="devOldPrice" placeholder="السعر قبل الخصم (اختياري)">
                    <input type="text" id="devEmoji" placeholder="إيموجي">
                    <input type="text" id="devImg" placeholder="رابط الصورة">
                    <button class="btn-add-product" onclick="devAddProduct()">✅ إضافة</button>
                </div>
                <div class="dev-card">
                    <h3>📋 المنتجات الحالية</h3>
                    <div class="dev-product-list" id="devProductList"></div>
                </div>
                <div class="dev-card">
                    <h3>⚙️ إعدادات</h3>
                    <p style="color:var(--gold);">🥤 مشروبات: <span id="devStatDrinks">0</span></p>
                    <p style="color:var(--gold);">🍽️ مأكولات: <span id="devStatFood">0</span></p>
                    <p style="color:var(--gold);">🎁 عروض: <span id="devStatOffers">0</span></p>
                    <button class="btn-reset" onclick="devResetData()" style="margin-top:15px;">🔄 إعادة ضبط</button>
                    <button class="btn-dev" onclick="devExportData()" style="margin-top:8px;">📤 تصدير البيانات</button>
                </div>
            </div>
        </div>
    </div>

    <!-- مودال السلة -->
    <div class="modal-overlay" id="cartModal">
        <div class="modal-box">
            <button class="modal-close" onclick="closeCart()">✕</button>
            <h2 class="cart-title">🛒 سلة المشتريات</h2>
            <div id="cartItems"></div>
            <div class="cart-total" id="cartTotal">الإجمالي: 0 ج.م</div>
            <p style="text-align:center;color:var(--gold);margin:10px 0;">اختر طريقة الدفع:</p>
            <div class="payment-options" id="paymentOptions">
                <div class="payment-opt selected" onclick="selectPayment('cash',this)">💵<span>نقداً</span></div>
                <div class="payment-opt" onclick="selectPayment('vodafone',this)">📱<span>فودافون كاش</span></div>
                <div class="payment-opt" onclick="selectPayment('bank',this)">🏦<span>تحويل</span></div>
            </div>
            <button class="btn-checkout" onclick="checkout()">✅ تأكيد الطلب واتساب</button>
        </div>
    </div>

    <!-- مودال تسجيل الدخول -->
    <div class="auth-overlay" id="authOverlay">
        <div class="auth-box">
            <h2>🔐 دخول / إنشاء حساب</h2>
            <div class="auth-tabs">
                <button class="auth-tab active" onclick="switchAuth('login')">تسجيل الدخول</button>
                <button class="auth-tab" onclick="switchAuth('register')">إنشاء حساب</button>
            </div>
            <div id="loginForm">
                <div class="form-group"><label>👤 اسم المستخدم</label><input type="text" id="loginUser" placeholder="أدخل اسم المستخدم"></div>
                <div class="form-group"><label>🔒 كلمة المرور</label><input type="password" id="loginPass" placeholder="كلمة المرور"></div>
                <div class="msg-error" id="loginError"></div>
                <button class="btn-auth" onclick="doLogin()">🚪 دخول</button>
            </div>
            <div id="registerForm" style="display:none;">
                <div class="form-group"><label>👤 اسم المستخدم</label><input type="text" id="regUser" placeholder="اختر اسم مستخدم"></div>
                <div class="form-group"><label>📧 البريد الإلكتروني</label><input type="email" id="regEmail" placeholder="بريدك الإلكتروني"></div>
                <div class="form-group"><label>🔒 كلمة المرور</label><input type="password" id="regPass" placeholder="كلمة مرور قوية"></div>
                <div class="form-group"><label>🔒 تأكيد كلمة المرور</label><input type="password" id="regPassConfirm" placeholder="أعد كتابة كلمة المرور"></div>
                <div class="msg-error" id="regError"></div>
                <div class="msg-success" id="regSuccess"></div>
                <button class="btn-auth" onclick="doRegister()">📝 إنشاء حساب</button>
            </div>
            <button style="width:100%;margin-top:15px;padding:12px;background:transparent;border:1px solid #333;color:#888;border-radius:10px;cursor:pointer;" onclick="closeAuth()">✕ إغلاق</button>
        </div>
    </div>

    <!-- أزرار عائمة -->
    <div class="float-btns">
        <button class="float-btn whatsapp" onclick="openWhatsApp()" title="واتساب">💬</button>
        <button class="float-btn dev-btn" id="devFloatBtn" onclick="toggleDevPanel()" title="لوحة المطور">👑</button>
        <button class="float-btn cart-float" id="cartFloatBtn" onclick="openCart()" title="السلة">🛒</button>
    </div>

    <!-- توست -->
    <div class="toast-container" id="toastContainer"></div>

    <!-- فوتر -->
    <div class="footer">
        <h3>☕ كافيه مصطفى</h3>
        <p>📍 شارع النخيل، مدينة القهوة</p>
        <p class="phone-number">📞 01026966717</p>
        <div class="social-icons">
            <div class="social-icon">📘</div>
            <div class="social-icon">📷</div>
            <div class="social-icon">🐦</div>
            <div class="social-icon">📱</div>
        </div>
        <p style="color:#666;margin-top:20px;">© 2026 كافيه مصطفى - جميع الحقوق محفوظة</p>
        <p style="color:#444;font-size:0.8em;">Developed by Mustafa 👑</p>
    </div>

    <script>
        // ==================== الثوابت ====================
        const DEV_CODE = "MOSTAFA2026"; // كود المطور
        const WHATSAPP_NUMBER = "201026966717"; // رقم الواتساب
        const PHONE_DISPLAY = "01026966717";

        // ==================== البيانات ====================
        function loadData() {
            const saved = localStorage.getItem('MUSTAFA_CAFE_DATA_V2');
            if (saved) return JSON.parse(saved);
            return {
                drinks: [
                    { id: 1, name: "قهوة تركية", desc: "قهوة تركية أصلية على الرمل", price: 25, oldPrice: 0, emoji: "☕",
                        img: "https://images.unsplash.com/photo-1572442388796-11668a67e53d?w=500&h=350&fit=crop" },
                    { id: 2, name: "لاتيه كريمي", desc: "لاتيه بحليب طازج وفن اللاتيه", price: 35, oldPrice: 40, emoji: "🥛",
                        img: "https://images.unsplash.com/photo-1570968915860-54d5c301fa9f?w=500&h=350&fit=crop" },
                    { id: 3, name: "كابتشينو إيطالي", desc: "كابتشينو برغوة كثيفة", price: 30, oldPrice: 0, emoji: "☕",
                        img: "https://images.unsplash.com/photo-1534778101976-62847782c213?w=500&h=350&fit=crop" },
                    { id: 4, name: "شاي كرك", desc: "شاي كرك هندي أصلي", price: 20, oldPrice: 25, emoji: "🍵",
                        img: "https://images.unsplash.com/photo-1564890369478-c89ca6d9cde9?w=500&h=350&fit=crop" },
                    { id: 5, name: "موكا مثلجة", desc: "موكا باردة بصوص الشوكولاتة", price: 40, oldPrice: 0, emoji: "🧊",
                        img: "https://images.unsplash.com/photo-1461023058943-07fcbe16d735?w=500&h=350&fit=crop" },
                    { id: 6, name: "عصير مانجو", desc: "مانجو طبيعي 100%", price: 30, oldPrice: 0, emoji: "🥭",
                        img: "https://images.unsplash.com/photo-1546173159-315724a31696?w=500&h=350&fit=crop" },
                    { id: 7, name: "ليمون بالنعناع", desc: "عصير ليمون طازج", price: 22, oldPrice: 0, emoji: "🍋",
                        img: "https://images.unsplash.com/photo-1621263764928-df1444c5e859?w=500&h=350&fit=crop" },
                    { id: 8, name: "سحلب ساخن", desc: "سحلب بالمكسرات والقرفة", price: 28, oldPrice: 32, emoji: "🥜",
                        img: "https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=500&h=350&fit=crop" },
                ],
                food: [
                    { id: 101, name: "كرواسون زبدة", desc: "كرواسون فرنسي طازج", price: 30, oldPrice: 0, emoji: "🥐",
                        img: "https://images.unsplash.com/photo-1555507036-ab1f4038024a?w=500&h=350&fit=crop" },
                    { id: 102, name: "تشيز كيك توت", desc: "تشيز كيك بالتوت الطازج", price: 45, oldPrice: 55, emoji: "🍰",
                        img: "https://images.unsplash.com/photo-1533134242443-d4fd215305ad?w=500&h=350&fit=crop" },
                    { id: 103, name: "وافل شوكولاتة", desc: "وافل بلجيكي بصوص الشوكولاتة", price: 40, oldPrice: 0, emoji: "🧇",
                        img: "https://images.unsplash.com/photo-1558584724-0e4d32ca55a6?w=500&h=350&fit=crop" },
                    { id: 104, name: "بان كيك بالعسل", desc: "بان كيك أمريكي بالعسل", price: 35, oldPrice: 0, emoji: "🥞",
                        img: "https://images.unsplash.com/photo-1567620905732-2d1ec7ab7445?w=500&h=350&fit=crop" },
                    { id: 105, name: "ساندوتش دجاج", desc: "دجاج مشوي طازج", price: 50, oldPrice: 60, emoji: "🥪",
                        img: "https://images.unsplash.com/photo-1528735602780-2552fd46c7af?w=500&h=350&fit=crop" },
                    { id: 106, name: "بيتزا مارجريتا", desc: "بيتزا إيطالية أصلية", price: 45, oldPrice: 0, emoji: "🍕",
                        img: "https://images.unsplash.com/photo-1574071318508-1cdbab80d002?w=500&h=350&fit=crop" },
                ],
                offers: [
                    { id: 201, name: "عرض الفطور", desc: "قهوة + كرواسون بسعر مميز", price: 40, oldPrice: 55, emoji: "🌅",
                        img: "https://images.unsplash.com/photo-1495474472287-4d71bcdd2085?w=500&h=350&fit=crop" },
                    { id: 202, name: "عرض المساء", desc: "مشروبين بسعر واحد", price: 45, oldPrice: 60, emoji: "🌙",
                        img: "https://images.unsplash.com/photo-1514432324607-a09d9b4aefda?w=500&h=350&fit=crop" },
                ],
            };
        }

        function saveData(data) { localStorage.setItem('MUSTAFA_CAFE_DATA_V2', JSON.stringify(data)); }

        let cafeData = loadData();
        let cart = JSON.parse(localStorage.getItem('MUSTAFA_CART_V2') || '[]');
        let selectedPayment = 'cash';
        let isDevLoggedIn = localStorage.getItem('MUSTAFA_DEV_LOGGEDIN') === 'true';
        let currentUser = JSON.parse(localStorage.getItem('MUSTAFA_CURRENT_USER') || 'null');
        let wishlist = JSON.parse(localStorage.getItem('MUSTAFA_WISHLIST') || '[]');

        // ==================== المؤشر المخصص ====================
        const cursor = document.getElementById('customCursor');
        const cursorDot = document.getElementById('cursorDot');
        document.addEventListener('mousemove', (e) => {
            cursor.style.left = e.clientX - 10 + 'px';
            cursor.style.top = e.clientY - 10 + 'px';
            cursorDot.style.left = e.clientX - 3 + 'px';
            cursorDot.style.top = e.clientY - 3 + 'px';
        });

        // ==================== جسيمات كانفاس ====================
        const canvas = document.getElementById('particlesCanvas');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        const particles = [];
        class Particle {
            constructor() { this.reset();
                this.y = Math.random() * canvas.height; }
            reset() { this.x = Math.random() * canvas.width;
                this.y = -10;
                this.size = Math.random() * 3 + 1;
                this.speedY = Math.random() * 1.5 + 0.5;
                this.speedX = (Math.random() - 0.5) * 0.5;
                this.opacity = Math.random() * 0.6 + 0.2;
                this.color = ['#d4a853', '#f0d78c', '#b8922e', '#c8a45c'][Math.floor(Math.random() * 4)]; }
            update() { this.y += this.speedY;
                this.x += this.speedX; if (this.y > canvas.height + 10) this.reset(); }
            draw() { ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fillStyle = this.color.replace(')', `,${this.opacity})`).replace('rgb',
                'rgba'); if (this.color.startsWith('#')) { ctx.fillStyle = this.color;
                    ctx.globalAlpha = this.opacity; } ctx.fill();
                ctx.globalAlpha = 1; }
        }
        for (let i = 0; i < 50; i++) particles.push(new Particle());

        function animateParticles() { ctx.clearRect(0, 0, canvas.width, canvas.height);
            particles.forEach(p => { p.update();
                p.draw(); });
            requestAnimationFrame(animateParticles); }
        animateParticles();
        window.addEventListener('resize', () => { canvas.width = window.innerWidth;
            canvas.height = window.innerHeight; });

        // ==================== لودر ====================
        window.addEventListener('load', () => { setTimeout(() => { document.getElementById('loader').classList.add(
                'hidden'); }, 1800); });

        // ==================== توست ====================
        function showToast(msg, isError = false) {
            const container = document.getElementById('toastContainer');
            const toast = document.createElement('div');
            toast.className = 'toast';
            toast.style.borderColor = isError ? 'var(--red)' : 'var(--gold)';
            toast.textContent = msg;
            container.appendChild(toast);
            setTimeout(() => toast.remove(), 3000);
        }

        // ==================== عرض المنتجات ====================
        function createProductCard(p, category) {
            const cartItem = cart.find(i => i.id === p.id);
            const qty = cartItem ? cartItem.quantity : 0;
