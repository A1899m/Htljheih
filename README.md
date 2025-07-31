<!DOCTYPE html>
<html lang="fa">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Armin Shop</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #fff;
            color: #333;
        }
        header {
            background-color: #ff4500;
            color: #fff;
            padding: 10px;
            text-align: center;
        }
        nav {
            background-color: #ff6347;
            padding: 10px;
            text-align: center;
        }
        nav a {
            color: #fff;
            margin: 0 10px;
            text-decoration: none;
        }
        .search-bar {
            margin: 20px;
            text-align: center;
        }
        .products {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
        }
        .product {
            border: 1px solid #ccc;
            margin: 10px;
            padding: 10px;
            width: 200px;
            text-align: center;
        }
        .product img {
            width: 100%;
            height: auto;
        }
        .cart {
            position: fixed;
            bottom: 10px;
            right: 10px;
            background-color: #ff4500;
            color: #fff;
            padding: 10px;
            border-radius: 5px;
        }
        .cart-content {
            display: none;
            position: fixed;
            bottom: 50px;
            right: 10px;
            background-color: #fff;
            color: #333;
            border: 1px solid #ccc;
            padding: 10px;
            border-radius: 5px;
        }
        .cart-content ul {
            list-style-type: none;
            padding: 0;
        }
        .cart-content ul li {
            margin: 5px 0;
        }
    </style>
</head>
<body onload="showWelcomePage()">
    <header>
        <h1>Armin Shop</h1>
        <p>پشتیبانی: 09376304272</p>
    </header>
    <nav>
        <a href="#" onclick="showHomePage()">صفحه اصلی</a>
        <a href="#">محصولات</a>
        <a href="#" onclick="showContact()">تماس با ما</a>
    </nav>
    <div class="search-bar">
        <input type="text" id="searchInput" placeholder="جستجوی محصولات...">
        <button onclick="searchProduct()">جستجو="products" id="productList">
        <!-- محصولات -->
        <!-- اضافه کردن سایر محصولات به همین روش -->
        <!-- افزودن شلوارها -->
        <div class="product" data-name="شلوار اسکینی" data-price="150000" data-type="اسکینی" data-material="نخی" data-color="آبی" data-brand="Levis">
            <img src="IMAGE_URL" alt="شلوار اسکینی">
            <h2>شلوار اسکینی</h2>
            <p>قیمت: 150,000 تومان</p>
            <button onclick="addToCart(this)">افزودن به سبد خرید</button>
        </div>
        <!-- افزودن سایر محصولات به همین روش -->
    </div>
    <div class="cart" onclick="toggleCartContent()">
        <p>سبد خرید</p>
        <p>تعداد: <span id="cartCount">0</span></p>
    </div>
    <div class="cart-content" id="cartContent">
        <ul id="cartItems">
            <!-- آیتم‌های سبد خرید -->
        </ul>
        <button onclick="clearCart()">پاک کردن سبد خرید</button>
    </div>

    <script>
        let cart = [];

        function showProductDetails(name, price, type, brand) {
            alert('نام: ' + name + '\\nقیمت: ' + price + '\\nنوع: ' + type + '\\nبرند: ' + brand);
        }

        function showContact() {
            alert('تماس با ما\\nنام: آرمین فلاح\\nشماره: 09376304272');
        }

        function searchProduct() {
            const input = document.getElementById('searchInput').value.toLowerCase();
            const products = document.querySelectorAll('.product');
            products.forEach(product => {
                const name = product.getAttribute('data-name').toLowerCase();
                if (name.includes(input)) {
                    product.style.display = 'block';
                } else {
                    product.style.display = 'none';
                }
            });
        }

        function addToCart(button) {
            const product = button.closest('.product');
            const name = product.getAttribute('data-name');
            const price = product.getAttribute('data-price');
            cart.push({ name, price });
            updateCartCount();
            updateCartContent();
        }

        function updateCartCount() {
            document.getElementById('cartCount').innerText = cart.length;
        }

        function updateCartContent() {
            const cartItems = document.getElementById('cartItems');
            cartItems.innerHTML = '';
            cart.forEach(item => {
                const li = document.createElement('li');
                li.innerText = item.name + ' - ' + item.price + ' تومان';
                cartItems.appendChild(li);
            });
        }

        function clearCart() {
            cart = [];
            updateCartCount();
            updateCartContent();
        }

        function toggleCartContent() {
            const cartContent = document.getElementById('cartContent');
            if (cartContent.style.display === 'none' || cartContent.style.display === '') {
                cartContent.style.display = 'block';
            } else {
                cartContent.style.display = 'none';
            }
        }

        function showHomePage() {
            window.location
