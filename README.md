<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Your Market - Sale4u</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    /* Custom styles for a touch of elegance */
    .product-card {
      transition: transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out;
    }
    .product-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 10px 15px rgba(0, 0, 0, 0.1);
    }
    .btn-primary {
      transition: background-color 0.2s ease-in-out, transform 0.1s ease-in-out;
    }
    .btn-primary:hover {
      transform: translateY(-1px);
    }
  </style>
</head>
<body class="bg-gradient-to-br from-gray-100 to-blue-50 text-gray-800 font-sans antialiased">

  <header class="bg-blue-700 text-white p-4 shadow-lg">
    <div class="container mx-auto flex flex-col md:flex-row justify-between items-center">
      <div class="text-center md:text-left">
        <h1 class="text-4xl font-extrabold tracking-tight">Your Market <span class="text-blue-200 text-2xl font-semibold">(Sale4u)</span></h1>
        <p class="text-sm md:text-base opacity-90 mt-1">Discover the Best Deals on Trendy Clothes and Stylish Shoes</p>
      </div>
      <a href="#order" class="mt-4 md:mt-0 bg-white text-blue-700 px-6 py-2 rounded-full font-semibold shadow-md hover:bg-blue-100 hover:scale-105 btn-primary">Shop Now!</a>
    </div>
  </header>

  <section class="p-6 text-center bg-white shadow-md mb-8">
    <div class="container mx-auto">
      <h2 class="text-3xl font-bold text-blue-800 mb-3 animate-pulse">Welcome to Your Market!</h2>
      <p class="mb-5 text-lg text-gray-700 leading-relaxed">Your one-stop destination for quality clothes and shoes, delivered right to your doorstep. Explore our collection and elevate your style!</p>
      <a href="#order" class="bg-blue-600 text-white px-8 py-3 rounded-lg text-lg font-semibold hover:bg-blue-700 focus:outline-none focus:ring-4 focus:ring-blue-300 transition duration-300 btn-primary">Order Your Favorites Today!</a>
    </div>
  </section>

  <section class="p-6 container mx-auto">
    <h3 class="text-3xl font-bold mb-8 text-center text-blue-800">Our Handpicked Products</h3>
    <div id="product-list" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8"></div>
  </section>

  <section id="order" class="bg-blue-100 p-8 rounded-lg shadow-inner my-8">
    <div class="container mx-auto">
      <h3 class="text-3xl font-bold mb-6 text-center text-blue-800">Place Your Order Here!</h3>
      <form id="orderForm" class="max-w-xl mx-auto bg-white p-6 rounded-xl shadow-lg space-y-5" onsubmit="submitOrder(event)">
        <input type="text" id="orderName" placeholder="Your Full Name" class="w-full border border-gray-300 p-3 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
        <input type="tel" id="orderMobile" placeholder="Mobile Number (e.g., 9876543210)" class="w-full border border-gray-300 p-3 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
        <input type="text" id="orderProduct" placeholder="Product Name (e.g., Stylish T-Shirt, Running Shoes)" class="w-full border border-gray-300 p-3 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
        <textarea id="orderAddress" placeholder="Full Delivery Address (Street, City, Pincode)" rows="4" class="w-full border border-gray-300 p-3 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required></textarea>
        <p class="text-md text-gray-700 flex items-center">
          <span class="mr-2 text-xl">💰</span> Payment Method: <strong class="ml-2 text-blue-700">Cash on Delivery (COD)</strong>
        </p>
        <button type="submit" class="w-full bg-blue-600 text-white px-6 py-3 rounded-lg font-semibold text-lg hover:bg-blue-700 focus:outline-none focus:ring-4 focus:ring-blue-300 transition duration-300 btn-primary">
          Send My Order
        </button>
      </form>
    </div>
  </section>

  <footer class="bg-gray-900 text-white text-center p-6 mt-10 shadow-inner">
    <div class="container mx-auto">
      <p class="text-lg">&copy; 2025 Your Market (Sale4u). All rights reserved.</p>
      <button onclick="document.getElementById('loginBox').classList.remove('hidden')" class="text-sm underline mt-3 opacity-80 hover:opacity-100 transition duration-200">Seller/Admin Login</button>
    </div>
  </footer>

  <section id="loginBox" class="p-6 bg-white mt-8 shadow-lg rounded-lg hidden container mx-auto max-w-md">
    <h3 class="text-2xl font-bold mb-5 text-center text-gray-800">🛍️ Seller/Admin Access</h3>
    <input type="password" id="adminPassword" placeholder="Enter Admin Password" class="w-full border border-gray-300 p-3 rounded-lg mb-4 focus:outline-none focus:ring-2 focus:ring-blue-500">
    <button onclick="checkAdminPassword()" class="w-full bg-blue-600 text-white p-3 rounded-lg font-semibold hover:bg-blue-700 focus:outline-none focus:ring-4 focus:ring-blue-300 transition duration-300 btn-primary">Login Securely</button>
    <p id="adminError" class="text-red-600 text-sm mt-3 text-center hidden">Oops! Incorrect password. Please try again.</p>
  </section>

  <section id="adminPanel" class="hidden mt-8 container mx-auto max-w-md bg-white p-6 rounded-lg shadow-lg">
    <h3 class="text-2xl font-bold mb-5 text-center text-gray-800">✨ Add New Product</h3>
    <form id="addProductForm" class="space-y-4">
      <input type="text" id="newName" placeholder="Product Name (e.g., Denim Jacket)" class="w-full border border-gray-300 p-3 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
      <input type="text" id="newPrice" placeholder="Price (e.g., ₹999, ₹1200)" class="w-full border border-gray-300 p-3 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
      <input type="url" id="newImage" placeholder="Image URL (e.g., https://example.com/image.jpg)" class="w-full border border-gray-300 p-3 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
      <textarea id="newDesc" placeholder="Brief Description (e.g., Classic fit, all-season wear)" rows="3" class="w-full border border-gray-300 p-3 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required></textarea>
      <button type="submit" class="w-full bg-blue-600 text-white p-3 rounded-lg font-semibold hover:bg-blue-700 focus:outline-none focus:ring-4 focus:ring-blue-300 transition duration-300 btn-primary">
        Add Product to Store
      </button>
    </form>
  </section>

  <script>
    const productList = document.getElementById("product-list");
    // Load products from localStorage or use defaults
    let products = JSON.parse(localStorage.getItem("products")) || [
      {
        name: "Stylish Casual T-Shirt",
        price: "₹499",
        image: "https://images.unsplash.com/photo-1576566588028-cdfd787ec7bf?q=80&w=1974&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
        desc: "Premium cotton comfort, available in various sizes and colors. Perfect for everyday wear."
      },
      {
        name: "Modern Running Shoes",
        price: "₹1199",
        image: "https://images.unsplash.com/photo-1542291026-79eddc872736?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
        desc: "Lightweight and durable design, providing excellent support and cushioning for your runs."
      },
      {
        name: "Elegant Summer Dress",
        price: "₹899",
        image: "https://images.unsplash.com/photo-1581044777550-4cfa68786538?q=80&w=1972&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
        desc: "Flowy and breathable fabric, perfect for sunny days and special occasions. Available in multiple patterns."
      },
      {
        name: "Classic Leather Wallet",
        price: "₹650",
        image: "https://images.unsplash.com/photo-1621609764095-fd93f6659617?q=80&w=1964&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
        desc: "Handcrafted from genuine leather, with multiple compartments for cards and cash. Timeless design."
      }
    ];

    // Saves products to localStorage
    function saveProducts() {
      localStorage.setItem("products", JSON.stringify(products));
    }

    // Renders products on the page
    function renderProducts() {
      productList.innerHTML = "";
      products.forEach((p, index) => {
        productList.innerHTML += `
          <div class="bg-white p-5 rounded-xl shadow-lg relative product-card">
            <button onclick="deleteProduct(${index})" class="absolute top-3 right-3 bg-red-500 text-white px-3 py-1 text-xs rounded-full hover:bg-red-600 transition duration-200 hidden admin-btn">Delete</button>
            <img src="${p.image}" alt="${p.name}" class="w-full h-52 object-cover rounded-lg mb-4 shadow-sm">
            <h4 class="font-bold text-xl text-blue-800 mb-2">${p.name}</h4>
            <p class="text-lg font-semibold text-green-600 mb-2">Price: ${p.price}</p>
            <p class="text-sm text-gray-600 leading-relaxed">${p.desc}</p>
          </div>
        `;
      });
    }

    // Deletes a product
    function deleteProduct(index) {
      if (confirm("Are you sure you want to delete this product? This action cannot be undone.")) {
        products.splice(index, 1);
        saveProducts();
        renderProducts();
        showDeleteButtons(); // Re-show delete buttons if admin is still logged in
      }
    }

    // Initial render of products when the page loads
    renderProducts();

    // Handles adding a new product from the admin panel
    document.getElementById("addProductForm").addEventListener("submit", function (e) {
      e.preventDefault();
      const name = document.getElementById("newName").value;
      const price = document.getElementById("newPrice").value;
      const image = document.getElementById("newImage").value;
      const desc = document.getElementById("newDesc").value;
      products.push({ name, price, image, desc });
      saveProducts();
      renderProducts();
      showDeleteButtons(); // Ensure delete buttons appear for new products
      this.reset(); // Clear the form
    });

    // Checks admin password for login
    function checkAdminPassword() {
      const correctPassword = "yourmarket123"; // Sensitive: In a real app, this would be handled server-side
      const input = document.getElementById("adminPassword").value;
      const error = document.getElementById("adminError");
      const panel = document.getElementById("adminPanel");
      if (input === correctPassword) {
        panel.classList.remove("hidden");
        error.classList.add("hidden");
        document.getElementById("loginBox").classList.add("hidden");
        showDeleteButtons(); // Show delete buttons upon successful login
      } else {
        error.classList.remove("hidden");
      }
    }

    // Shows delete buttons for admin
    function showDeleteButtons() {
      document.querySelectorAll(".admin-btn").forEach(btn => btn.classList.remove("hidden"));
    }

    // Handles order submission and opens WhatsApp
    function submitOrder(e) {
      e.preventDefault();
      const name = document.getElementById("orderName").value;
      const mobile = document.getElementById("orderMobile").value;
      const product = document.getElementById("orderProduct").value;
      const address = document.getElementById("orderAddress").value;

      // WhatsApp message format
      const message = `🛒 *New Order from Your Market*%0A%0A👤 *Customer Name:* ${name}%0A📞 *Mobile Number:* ${mobile}%0A📦 *Product Ordered:* ${product}%0A🏠 *Delivery Address:* ${address}%0A%0A💰 *Payment Method:* Cash on Delivery`;

      // Replace 919667302392 with the actual WhatsApp number
      const whatsappURL = `https://wa.me/919667302392?text=${message}`;
      window.open(whatsappURL, '_blank'); // Open in a new tab

      alert("Your order has been sent! We will contact you shortly.");
      document.getElementById("orderForm").reset(); // Clear the form after submission
    }
  </script>

</body>
</html>
