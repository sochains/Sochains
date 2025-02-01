<!DOCTYPE html>
<html lang="en" data-theme="light">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nexus - Modern E-Commerce Template</title>
    <link href="https://cdn.jsdelivr.net/npm/@splidejs/splide@4.1.4/dist/css/splide.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #2563eb;
            --secondary: #1e40af;
            --dark: #1e293b;
            --light: #f8fafc;
            --success: #22c55e;
            --shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }

        body {
            background: var(--light);
            color: var(--dark);
            transition: all 0.3s ease;
        }

        .dark body {
            background: var(--dark);
            color: var(--light);
        }

        .header {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            box-shadow: var(--shadow);
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
        }

        .dark .header {
            background: rgba(30, 41, 59, 0.95);
        }

        .hero {
            height: 80vh;
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            clip-path: ellipse(100% 60% at 50% 40%);
        }

        .product-card {
            background: white;
            border-radius: 16px;
            padding: 1.5rem;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }

        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
        }

        .product-image {
            height: 300px;
            object-fit: cover;
            border-radius: 8px;
            transition: transform 0.3s ease;
        }

        .product-card:hover .product-image {
            transform: scale(1.05);
        }

        .badge {
            position: absolute;
            top: 1rem;
            right: 1rem;
            background: var(--success);
            color: white;
            padding: 0.25rem 0.75rem;
            border-radius: 999px;
            font-size: 0.875rem;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            padding: 2rem;
            max-width: 1440px;
            margin: 0 auto;
        }

        .theme-toggle {
            position: fixed;
            bottom: 2rem;
            right: 2rem;
            background: var(--primary);
            color: white;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            box-shadow: var(--shadow);
        }

        @media (max-width: 768px) {
            .menu {
                display: none;
            }
            
            .mobile-menu {
                display: block;
            }
        }
    </style>
</head>
<body>
    <header class="header">
        <nav class="container flex justify-between items-center py-4">
            <div class="text-2xl font-bold">Nexus</div>
            <div class="flex gap-8 menu">
                <a href="#" class="hover:text-primary">Shop</a>
                <a href="#" class="hover:text-primary">Categories</a>
                <a href="#" class="hover:text-primary">Cart <span class="cart-count">0</span></a>
            </div>
            <button class="mobile-menu hidden">
                <i class="fas fa-bars text-xl"></i>
            </button>
        </nav>
    </header>

    <section class="hero">
        <div class="text-center">
            <h1 class="text-5xl font-bold mb-4">Next-Gen Shopping Experience</h1>
            <p class="text-xl mb-8">Discover premium products curated for you</p>
            <button class="bg-white text-primary px-8 py-3 rounded-full font-bold hover:bg-opacity-90">
                Explore Collection
            </button>
        </div>
    </section>

    <main class="py-20 mt-20">
        <div class="grid">
            <!-- Product Cards -->
            <div class="product-card">
                <div class="badge">New</div>
                <img src="product1.jpg" alt="Product" class="product-image">
                <h3 class="text-xl font-bold mt-4">Premium Smart Watch</h3>
                <p class="text-gray-500 mt-2">Advanced health monitoring</p>
                <div class="flex justify-between items-center mt-4">
                    <span class="text-2xl font-bold">$299</span>
                    <button class="add-to-cart bg-primary text-white px-4 py-2 rounded-lg hover:bg-secondary">
                        <i class="fas fa-cart-plus"></i> Add to Cart
                    </button>
                </div>
            </div>

            <!-- More product cards... -->
        </div>
    </main>

    <div class="theme-toggle">
        <i class="fas fa-moon"></i>
    </div>

    <script>
        // Dark Mode Toggle
        const themeToggle = document.querySelector('.theme-toggle');
        themeToggle.addEventListener('click', () => {
            document.documentElement.classList.toggle('dark');
            themeToggle.querySelector('i').classList.toggle('fa-moon');
            themeToggle.querySelector('i').classList.toggle('fa-sun');
        });

        // Cart Functionality
        class Cart {
            constructor() {
                this.items = JSON.parse(localStorage.getItem('cart')) || [];
                this.updateCartCount();
            }

            addItem(product) {
                this.items.push(product);
                this.saveCart();
                this.updateCartCount();
            }

            saveCart() {
                localStorage.setItem('cart', JSON.stringify(this.items));
            }

            updateCartCount() {
                document.querySelectorAll('.cart-count').forEach(el => {
                    el.textContent = this.items.length;
                });
            }
        }

        const cart = new Cart();

        // Add to Cart Buttons
        document.querySelectorAll('.add-to-cart').forEach(button => {
            button.addEventListener('click', () => {
                const product = {
                    name: button.closest('.product-card').querySelector('h3').textContent,
                    price: button.closest('.product-card').querySelector('span').textContent,
                    image: button.closest('.product-card').querySelector('img').src
                };
                cart.addItem(product);
                showToast('Item added to cart!');
            });
        });

        // Toast Notification
        function showToast(message) {
            const toast = document.createElement('div');
            toast.className = 'fixed bottom-4 left-4 bg-green-500 text-white px-4 py-2 rounded-lg';
            toast.textContent = message;
            document.body.appendChild(toast);
            
            setTimeout(() => {
                toast.remove();
            }, 3000);
        }
    </script>
</body>
</html>
