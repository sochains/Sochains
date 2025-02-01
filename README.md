## Hi there 👋

<!--
**sochains/Sochains** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
ecommerce-template/
│
├── index.html            # Homepage
├── products.html         # Product listing page
├── product-detail.html   # Product detail page
├── cart.html             # Shopping cart page
├── checkout.html         # Checkout page
│
├── css/
│   └── style.css         # Main stylesheet
│
├── js/
│   └── script.js         # Main JavaScript file
│
├── assets/               # Image/icon assets
│   ├── images/
│   └── icons/
│
├── README.md             # Documentation
└── LICENSE               # License file
home page
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>E-Commerce Template</title>
    <link rel="stylesheet" href="css/style.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
</head>
<body>
    <!-- Header -->
    <header>
        <nav>
            <div class="logo">E-Shop</div>
            <ul class="nav-links">
                <li><a href="index.html">Home</a></li>
                <li><a href="products.html">Products</a></li>
                <li><a href="cart.html">Cart (<span id="cart-count">0</span>)</a></li>
            </ul>
        </nav>
    </header>

    <!-- Hero Section -->
    <section class="hero">
        <h1>Welcome to Our Store</h1>
        <p>Discover Amazing Products</p>
        <a href="products.html" class="cta-button">Shop Now</a>
    </section>

    <!-- Featured Products -->
    <section class="featured-products">
        <h2>Featured Products</h2>
        <div class="product-grid">
            <!-- Product cards will be dynamically loaded -->
        </div>
    </section>

    <script src="js/script.js"></script>
</body>
</html>
style.css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>E-Commerce Template</title>
    <link rel="stylesheet" href="css/style.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
</head>
<body>
    <!-- Header -->
    <header>
        <nav>
            <div class="logo">E-Shop</div>
            <ul class="nav-links">
                <li><a href="index.html">Home</a></li>
                <li><a href="products.html">Products</a></li>
                <li><a href="cart.html">Cart (<span id="cart-count">0</span>)</a></li>
            </ul>
        </nav>
    </header>

    <!-- Hero Section -->
    <section class="hero">
        <h1>Welcome to Our Store</h1>
        <p>Discover Amazing Products</p>
        <a href="products.html" class="cta-button">Shop Now</a>
    </section>

    <!-- Featured Products -->
    <section class="featured-products">
        <h2>Featured Products</h2>
        <div class="product-grid">
            <!-- Product cards will be dynamically loaded -->
        </div>
    </section>

    <script src="js/script.js"></script>
</body>
</html>
script.js
// Sample product data
const products = [
    {
        id: 1,
        name: "Product 1",
        price: 29.99,
        image: "assets/images/product1.jpg"
    },
    // Add more products...
];

// Cart functionality
let cart = JSON.parse(localStorage.getItem('cart')) || [];

function updateCartCount() {
    document.getElementById('cart-count').textContent = cart.length;
}

function addToCart(productId) {
    const product = products.find(p => p.id === productId);
    cart.push(product);
    localStorage.setItem('cart', JSON.stringify(cart));
    updateCartCount();
}

// Initialize homepage
document.addEventListener('DOMContentLoaded', () => {
    // Load featured products
    const productGrid = document.querySelector('.product-grid');
    products.forEach(product => {
        productGrid.innerHTML += `
            <div class="product-card">
                <img src="${product.image}" alt="${product.name}">
                <h3>${product.name}</h3>
                <p>$${product.price}</p>
                <button onclick="addToCart(${product.id})">Add to Cart</button>
            </div>
        `;
    });
    
    updateCartCount();
});
