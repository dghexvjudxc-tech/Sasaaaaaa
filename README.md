<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>كافيه مصطفى - الطلب أونلاين</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #1a1a1a;
            color: #f0e6d2;
        }

        /* الهيدر */
        .header {
            background: linear-gradient(135deg, #2c1810 0%, #4a2c17 50%, #2c1810 100%);
            padding: 20px;
            text-align: center;
            border-bottom: 3px solid #c8a45c;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 4px 15px rgba(0,0,0,0.5);
        }

        .header h1 {
            font-size: 2.5em;
            color: #c8a45c;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            letter-spacing: 3px;
        }

        .header .subtitle {
            color: #d4b87a;
            font-size: 1.1em;
            margin-top: 5px;
        }

        .cart-icon {
            position: fixed;
            top: 25px;
            left: 30px;
            background: #c8a45c;
            color: #2c1810;
            padding: 12px 20px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            z-index: 101;
            font-size: 1.1em;
            box-shadow: 0 4px 15px rgba(200,164,92,0.4);
            transition: all 0.3s;
        }

        .cart-icon:hover {
            background: #d4b87a;
            transform: scale(1.05);
        }

        .cart-count {
            background: #e74c3c;
            color: white;
            border-radius: 50%;
            padding: 2px 8px;
            font-size: 0.8em;
            margin-right: 5px;
        }

        /* المحتوى الرئيسي */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .section-title {
            text-align: center;
            color: #c8a45c;
            font-size: 2em;
            margin: 40px 0 30px;
            border-bottom: 2px solid #4a2c17;
            padding-bottom: 15px;
        }

        /* قائمة المنتجات */
        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 25px;
        }

        .product-card {
            background: linear-gradient(145deg, #2c2420, #1f1a16);
            border-radius: 20px;
            overflow: hidden;
            border: 1px solid #3a2f25;
            transition: all 0.3s;
            box-shadow: 0 8px 25px rgba(0,0,0,0.3);
        }

        .product-card:hover {
            transform: translateY(-8px);
            border-color: #c8a45c;
            box-shadow: 0 15px 40px rgba(200,164,92,0.2);
        }

        .product-image {
            width: 100%;
            height: 220px;
            object-fit: cover;
            border-bottom: 2px solid #4a2c17;
            /* صورة افتراضية ملونة إذا لم تتحمل الصورة */
            background: linear-gradient(135deg, #3d2b1f, #5a3d2b);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 4em;
        }

        .product-info {
            padding: 20px;
        }

        .product-name {
            font-size: 1.3em;
            color: #f0e6d2;
            margin-bottom: 8px;
        }

        .product-desc {
            color: #a89070;
            font-size: 0.9em;
            margin-bottom: 15px;
            min-height: 45px;
        }

        .product-price {
            font-size: 1.4em;
            color: #c8a45c;
            font-weight: bold;
            margin-bottom: 15px;
        }

        .add-to-cart {
            width: 100%;
            padding: 12px;
            background: #c8a45c;
            color: #2c1810;
            border: none;
            border-radius: 12px;
            font-size: 1.1em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
        }

        .add-to-cart:hover {
            background: #d4b87a;
            box-shadow: 0 5px 20px rgba(200,164,92,0.4);
        }

        /* نافذة عربة التسوق */
        .cart-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            z-index: 200;
            justify-content: center;
            align-items: center;
        }

        .cart-content {
            background: #2c2420;
            border: 2px solid #c8a45c;
            border-radius: 20px;
            padding: 30px;
            width: 90%;
            max-width: 600px;
            max-height: 80vh;
            overflow-y: auto;
            position: relative;
        }

        .close-cart {
            position: absolute;
            top: 15px;
            left: 20px;
            background: none;
            border: none;
            color: #c8a45c;
            font-size: 2em;
            cursor: pointer;
        }

        .cart-title {
            color: #c8a45c;
            font-size: 1.8em;
            margin-bottom: 25px;
            text-align: center;
        }

        .cart-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            border-bottom: 1px solid #3a2f25;
        }

        .cart-item-name {
            color: #f0e6d2;
            font-size: 1.1em;
        }

        .cart-item-price {
            color: #c8a45c;
            font-weight: bold;
        }

        .remove-item {
            background: #e74c3c;
            color: white;
            border: none;
            padding: 5px 10px;
            border-radius: 5px;
            cursor: pointer;
        }

        .cart-total {
            font-size: 1.5em;
            color: #c8a45c;
            text-align: center;
            margin: 20px 0;
            font-weight: bold;
        }

        /* طرق الدفع */
        .payment-section {
            margin: 20px 0;
        }

        .payment-methods {
            display: flex;
            justify-content: space-around;
            flex-wrap: wrap;
            gap: 15px;
            margin: 20px 0;
        }

        .payment-method {
            background: #1f1a16;
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            cursor: pointer;
            border: 2px solid transparent;
            transition: all 0.3s;
            flex: 1;
            min-width: 120px;
            font-size: 2.5em;
        }

        .payment-method:hover, .payment-method.selected {
            border-color: #c8a45c;
            background: #2c1810;
        }

        .payment-method span {
            display: block;
            font-size: 0.4em;
            margin-top: 8px;
            color: #f0e6d2;
        }

        .checkout-btn {
            width: 100%;
            padding: 15px;
            background: linear-gradient(135deg, #27ae60, #2ecc71);
            color: white;
            border: none;
            border-radius: 12px;
            font-size: 1.3em;
            font-weight: bold;
            cursor: pointer;
            margin-top: 20px;
            transition: all 0.3s;
        }

        .checkout-btn:hover {
            box-shadow: 0 5px 25px rgba(46,204,113,0.4);
            transform: scale(1.02);
        }

        .empty-cart {
            text-align: center;
            color: #a89070;
            font-size: 1.2em;
            padding: 40px;
        }

        /* إشعار */
        .notification {
            position: fixed;
            bottom: 30px;
            right: 30px;
            background: #27ae60;
            color: white;
            padding: 15px 25px;
            border-radius: 50px;
            z-index: 300;
            display: none;
            font-weight: bold;
            box-shadow: 0 5px 20px rgba(0,0,0,0.5);
        }

        /* Footer */
        .footer {
            text-align: center;
            padding: 30px;
            background: #2c1810;
            color: #a89070;
            margin-top: 40px;
            border-top: 2px solid #4a2c17;
        }

        .footer a {
            color: #c8a45c;
            text-decoration: none;
        }

        /* زر واتساب */
        .whatsapp-float {
            position: fixed;
            bottom: 30px;
            left: 30px;
            background: #25D366;
            color: white;
            width: 60px;
            height: 60px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2em;
            z-index: 99;
            box-shadow: 0 5px 20px rgba(37,211,102,0.4);
            cursor: pointer;
            text-decoration: none;
            transition: all 0.3s;
        }

        .whatsapp-float:hover {
            transform: scale(1.1);
        }

        @media (max-width: 768px) {
            .header h1 { font-size: 1.8em; }
            .cart-icon { top: 15px; left: 15px; padding: 8px 15px; font-size: 0.9em; }
            .products-grid { grid-template-columns: 1fr 1fr; gap: 15px; }
            .product-image { height: 150px; font-size: 3em; }
        }
    </style>
</head>
<body>

    <!-- الهيدر -->
    <div class="header">
        <h1>☕ كافيه مصطفى</h1>
        <p class="subtitle">أجود أنواع القهوة والمأكولات - الطلب أونلاين</p>
    </div>

    <!-- أيقونة السلة -->
    <div class="cart-icon" onclick="openCart()">
        🛒 <span class="cart-count" id="cartCount">0</span> السلة
    </div>

    <!-- المحتوى الرئيسي -->
    <div class="container">

        <!-- قسم المشروبات -->
        <h2 class="section-title">🥤 المشروبات الساخنة والباردة</h2>
        <div class="products-grid" id="drinksGrid"></div>

        <!-- قسم المأكولات -->
        <h2 class="section-title">🍽️ المأكولات والحلويات</h2>
        <div class="products-grid" id="foodGrid"></div>

        <!-- قسم طرق الدفع -->
        <h2 class="section-title">💳 طرق الدفع المتاحة</h2>
        <div class="payment-methods" style="background: #1f1a16; padding: 30px; border-radius: 20px; margin-bottom: 40px;">
            <div class="payment-method">
                💵<span>نقداً عند الاستلام</span>
            </div>
            <div class="payment-method">
                📱<span>فودافون كاش</span>
            </div>
            <div class="payment-method">
                🏦<span>تحويل بنكي</span>
            </div>
            <div class="payment-method">
                💳<span>بطاقة ائتمان</span>
            </div>
            <div class="payment-method">
                📲<span>محفظة إلكترونية</span>
            </div>
        </div>
    </div>

    <!-- نافذة السلة -->
    <div class="cart-modal" id="cartModal">
        <div class="cart-content">
            <button class="close-cart" onclick="closeCart()">✕</button>
            <h2 class="cart-title">🛒 سلة المشتريات</h2>
            <div id="cartItems"></div>
            <div class="cart-total" id="cartTotal">الإجمالي: 0 ج.م</div>

            <div class="payment-section">
                <h4 style="color: #c8a45c; margin-bottom: 15px;">اختر طريقة الدفع:</h4>
                <div class="payment-methods" id="paymentMethods">
                    <div class="payment-method" onclick="selectPayment('cash')" data-method="cash">
                        💵<span>نقداً</span>
                    </div>
                    <div class="payment-method" onclick="selectPayment('vodafone')" data-method="vodafone">
                        📱<span>فودافون كاش</span>
                    </div>
                    <div class="payment-method" onclick="selectPayment('bank')" data-method="bank">
                        🏦<span>تحويل بنكي</span>
                    </div>
                </div>
            </div>

            <button class="checkout-btn" onclick="checkout()">✅ تأكيد الطلب</button>
        </div>
    </div>

    <!-- إشعار -->
    <div class="notification" id="notification"></div>

    <!-- زر واتساب -->
    <a href="https://wa.me/201000000000?text=مرحباً كافيه مصطفى، أريد الاستفسار عن طلب" target="_blank" class="whatsapp-float" title="تواصل معنا واتساب">
        💬
    </a>

    <!-- Footer -->
    <div class="footer">
        <p>© 2026 <strong>كافيه مصطفى</strong> - جميع الحقوق محفوظة</p>
        <p>📍 شارع القهوة، مدينة النكهات | 📞 01000000000</p>
        <p>تابعنا على: 
            <a href="#">فيسبوك</a> | 
            <a href="#">إنستجرام</a> | 
            <a href="#">تويتر</a>
        </p>
    </div>

    <script>
        // بيانات المنتجات (صور من unsplash مع معلمات للتحميل السريع)
        const products = {
            drinks: [
                { id: 1, name: "قهوة تركية", desc: "قهوة تركية أصلية على الرمل", price: 25, emoji: "☕", img: "https://images.unsplash.com/photo-1572442388796-11668a67e53d?w=400&h=300&fit=crop" },
                { id: 2, name: "لاتيه", desc: "لاتيه كريمي بحليب طازج", price: 35, emoji: "🥛", img: "https://images.unsplash.com/photo-1570968915860-54d5c301fa9f?w=400&h=300&fit=crop" },
                { id: 3, name: "كابتشينو", desc: "كابتشينو إيطالي برغوة كثيفة", price: 30, emoji: "☕", img: "https://images.unsplash.com/photo-1534778101976-62847782c213?w=400&h=300&fit=crop" },
                { id: 4, name: "شاي كرك", desc: "شاي كرك هندي أصلي", price: 20, emoji: "🍵", img: "https://images.unsplash.com/photo-1564890369478-c89ca6d9cde9?w=400&h=300&fit=crop" },
                { id: 5, name: "موكا مثلجة", desc: "موكا باردة بصوص الشوكولاتة", price: 40, emoji: "🧊", img: "https://images.unsplash.com/photo-1461023058943-07fcbe16d735?w=400&h=300&fit=crop" },
                { id: 6, name: "عصير مانجو", desc: "عصير مانجو طبيعي 100%", price: 30, emoji: "🥭", img: "https://images.unsplash.com/photo-1546173159-315724a31696?w=400&h=300&fit=crop" },
                { id: 7, name: "ليمون بالنعناع", desc: "عصير ليمون طازج بالنعناع", price: 22, emoji: "🍋", img: "https://images.unsplash.com/photo-1621263764928-df1444c5e859?w=400&h=300&fit=crop" },
                { id: 8, name: "سحلب", desc: "سحلب ساخن بالمكسرات والقرفة", price: 28, emoji: "🥜", img: "https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=400&h=300&fit=crop" }
            ],
            food: [
                { id: 101, name: "كرواسون زبدة", desc: "كرواسون فرنسي طازج", price: 30, emoji: "🥐", img: "https://images.unsplash.com/photo-1555507036-ab1f4038024a?w=400&h=300&fit=crop" },
                { id: 102, name: "تشيز كيك", desc: "تشيز كيك بالتوت الطازج", price: 45, emoji: "🍰", img: "https://images.unsplash.com/photo-1533134242443-d4fd215305ad?w=400&h=300&fit=crop" },
                { id: 103, name: "وافل شوكولاتة", desc: "وافل بلجيكي بصوص الشوكولاتة", price: 40, emoji: "🧇", img: "https://images.unsplash.com/photo-1558584724-0e4d32ca55a6?w=400&h=300&fit=crop" },
                { id: 104, name: "بان كيك", desc: "بان كيك أمريكي بالعسل", price: 35, emoji: "🥞", img: "https://images.unsplash.com/photo-1567620905732-2d1ec7ab7445?w=400&h=300&fit=crop" },
                { id: 105, name: "ساندوتش دجاج", desc: "ساندوتش دجاج مشوي طازج", price: 50, emoji: "🥪", img: "https://images.unsplash.com/photo-1528735602780-2552fd46c7af?w=400&h=300&fit=crop" },
                { id: 106, name: "بيتزا صغيرة", desc: "بيتزا مارجريتا إيطالية", price: 45, emoji: "🍕", img: "https://images.unsplash.com/photo-1574071318508-1cdbab80d002?w=400&h=300&fit=crop" },
                { id: 107, name: "بقلاوة", desc: "بقلاوة تركية بالفستق", price: 35, emoji: "🍯", img: "https://images.unsplash.com/photo-1519676640347-7c69e22b734b?w=400&h=300&fit=crop" },
                { id: 108, name: "مكرونة بشاميل", desc: "مكرونة بشاميل بالفرن", price: 55, emoji: "🍝", img: "https://images.unsplash.com/photo-1621996346565-e3dbc646d9a9?w=400&h=300&fit=crop" }
            ]
        };

        let cart = [];
        let selectedPayment = 'cash';

        // تحميل السلة من localStorage
        if (localStorage.getItem('mustafaCafeCart')) {
            cart = JSON.parse(localStorage.getItem('mustafaCafeCart'));
            updateCartCount();
        }

        // عرض المنتجات
        function renderProducts() {
            const drinksGrid = document.getElementById('drinksGrid');
            const foodGrid = document.getElementById('foodGrid');

            drinksGrid.innerHTML = products.drinks.map(p => `
                <div class="product-card">
                    <img class="product-image" src="${p.img}" alt="${p.name}" 
                         onerror="this.style.display='none'; this.nextElementSibling.style.display='flex';" 
                         loading="lazy">
                    <div class="product-image" style="display:none;">${p.emoji}</div>
                    <div class="product-info">
                        <h3 class="product-name">${p.name}</h3>
                        <p class="product-desc">${p.desc}</p>
                        <p class="product-price">${p.price} ج.م</p>
                        <button class="add-to-cart" onclick="addToCart(${p.id}, '${p.name}', ${p.price})">🛒 أضف للسلة</button>
                    </div>
                </div>
            `).join('');

            foodGrid.innerHTML = products.food.map(p => `
                <div class="product-card">
                    <img class="product-image" src="${p.img}" alt="${p.name}" 
                         onerror="this.style.display='none'; this.nextElementSibling.style.display='flex';" 
                         loading="lazy">
                    <div class="product-image" style="display:none;">${p.emoji}</div>
                    <div class="product-info">
                        <h3 class="product-name">${p.name}</h3>
                        <p class="product-desc">${p.desc}</p>
                        <p class="product-price">${p.price} ج.م</p>
                        <button class="add-to-cart" onclick="addToCart(${p.id}, '${p.name}', ${p.price})">🛒 أضف للسلة</button>
                    </div>
                </div>
            `).join('');
        }

        function addToCart(id, name, price) {
            const existing = cart.find(item => item.id === id);
            if (existing) {
                existing.quantity++;
            } else {
                cart.push({ id, name, price, quantity: 1 });
            }
            updateCartCount();
            saveCart();
            showNotification(`✅ تم إضافة "${name}" إلى السلة`);
        }

        function removeFromCart(id) {
            cart = cart.filter(item => item.id !== id);
            updateCartCount();
            saveCart();
            renderCart();
        }

        function updateCartCount() {
            const count = cart.reduce((sum, item) => sum + item.quantity, 0);
            document.getElementById('cartCount').textContent = count;
        }

        function saveCart() {
            localStorage.setItem('mustafaCafeCart', JSON.stringify(cart));
        }

        function openCart() {
            document.getElementById('cartModal').style.display = 'flex';
            renderCart();
        }

        function closeCart() {
            document.getElementById('cartModal').style.display = 'none';
        }

        function renderCart() {
            const cartItems = document.getElementById('cartItems');
            const cartTotal = document.getElementById('cartTotal');

            if (cart.length === 0) {
                cartItems.innerHTML = '<div class="empty-cart">🛒 السلة فارغة - أضف منتجاتك المفضلة</div>';
                cartTotal.textContent = 'الإجمالي: 0 ج.م';
                return;
            }

            let total = 0;
            cartItems.innerHTML = cart.map(item => {
                const itemTotal = item.price * item.quantity;
                total += itemTotal;
                return `
                    <div class="cart-item">
                        <span class="cart-item-name">${item.name} ×${item.quantity}</span>
                        <span class="cart-item-price">${itemTotal} ج.م</span>
                        <button class="remove-item" onclick="removeFromCart(${item.id})">🗑️</button>
                    </div>
                `;
            }).join('');

            cartTotal.textContent = `الإجمالي: ${total} ج.م`;
        }

        function selectPayment(method) {
            selectedPayment = method;
            document.querySelectorAll('#paymentMethods .payment-method').forEach(el => {
                el.classList.remove('selected');
                if (el.dataset.method === method) el.classList.add('selected');
            });
        }

        function checkout() {
            if (cart.length === 0) {
                showNotification('⚠️ السلة فارغة! أضف منتجات أولاً');
                return;
            }

            let total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            const paymentNames = { cash: 'نقداً عند الاستلام', vodafone: 'فودافون كاش', bank: 'تحويل بنكي' };
            const paymentName = paymentNames[selectedPayment] || 'نقداً';

            const orderSummary = cart.map(item => `• ${item.name} ×${item.quantity} = ${item.price * item.quantity} ج.م`).join('\n');
            const message = `🛒 *طلب جديد من كافيه مصطفى*\n\n${orderSummary}\n\n💰 *الإجمالي:* ${total} ج.م\n💳 *الدفع:* ${paymentName}\n\nشكراً لثقتكم! 🙏`;

            // محاولة فتح واتساب
            const phone = '201000000000'; // ضع رقم الواتساب الحقيقي هنا
            const whatsappUrl = `https://wa.me/${phone}?text=${encodeURIComponent(message)}`;
            
            showNotification('🎉 تم إرسال طلبك! جاري تحويلك للواتساب...');
            cart = [];
            updateCartCount();
            saveCart();
            closeCart();
            
            setTimeout(() => {
                window.open(whatsappUrl, '_blank');
            }, 1500);
        }

        function showNotification(msg) {
            const notif = document.getElementById('notification');
            notif.textContent = msg;
            notif.style.display = 'block';
            setTimeout(() => { notif.style.display = 'none'; }, 2500);
        }

        // إغلاق السلة عند النقر خارجها
        document.getElementById('cartModal').addEventListener('click', function(e) {
            if (e.target === this) closeCart();
        });

        // بدء التشغيل
        renderProducts();
        updateCartCount();
    </script>
</body>
</html>
