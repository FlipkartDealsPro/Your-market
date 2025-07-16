<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Your Market - Sale4u</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 text-gray-800 font-sans">

  <!-- HEADER -->
  <header class="bg-blue-600 text-white p-4 text-center">
    <h1 class="text-3xl font-bold">Your Market (Sale4u)</h1>
    <p class="text-sm">Best Deals on Clothes and Shoes</p>
  </header>

  <!-- WELCOME -->
  <section class="p-6 text-center bg-white">
    <h2 class="text-2xl font-semibold mb-2">Welcome to Your Market</h2>
    <p class="mb-4 text-gray-600">Clothes and Shoes delivered to your door</p>
    <a href="#order" class="bg-blue-600 text-white px-6 py-2 rounded hover:bg-blue-700">Order Now</a>
  </section>

  <!-- PRODUCT LIST -->
  <section class="p-6">
    <h3 class="text-xl font-bold mb-4 text-center">Our Products</h3>
    <div id="product-list" class="grid grid-cols-1 md:grid-cols-2 gap-6"></div>
  </section>

  <!-- ORDER FORM -->
  <section id="order" class="bg-blue-50 p-6">
    <h3 class="text-xl font-bold mb-4 text-center">Order Now</h3>
    <form id="orderForm" class="max-w-md mx-auto bg-white p-4 rounded shadow space-y-4" onsubmit="submitOrder(event)">
      <input type="text" id="orderName" placeholder="Your Name" class="w-full border p-2 rounded" required>
      <input type="tel" id="orderMobile" placeholder="Mobile Number" class="w-full border p-2 rounded" required>
      <input type="text" id="orderProduct" placeholder="Product Name" class="w-full border p-2 rounded" required>
      <textarea id="orderAddress" placeholder="Delivery Address" class="w-full border p-2 rounded" required></textarea>
      <p class="text-sm text-gray-600">💰 Payment: <strong>Cash on Delivery</strong></p>
      <button type="submit" class="bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700">Send Order</button>
    </form>
  </section>

  <!-- FOOTER -->
  <footer class="bg-gray-800 text-white text-center p-4 mt-6">
    <p>&copy; 2025 Your Market (Sale4u)</p>
    <button onclick="document.getElementById('loginBox').classList.remove('hidden')" class="text-sm underline mt-2">Seller Login</button>
  </footer>

  <!-- SELLER LOGIN -->
  <section id="loginBox" class="p-6 bg-white mt-6 hidden">
    <div class="max-w-md mx-auto">
      <h3 class="text-xl font-bold mb-4 text-center">🛍️ Seller/Admin Login</h3>
      <input type="password" id="adminPassword" placeholder="Enter Admin Password" class="w-full border p-2 rounded mb-2">
      <button onclick="checkAdminPassword()" class="w-full bg-blue-600 text-white p-2 rounded hover:bg-blue-700">Login</button>
      <p id="adminError" class="text-red-500 text-sm mt-2 hidden">Incorrect password</p>
    </div>
  </section>

  <!-- ADMIN PANEL -->
  <section id="adminPanel" class="hidden mt-4 max-w-md mx-auto bg-white p-6 rounded shadow">
    <h3 class="text-xl font-bold mb-4 text-center">Add New Product</h3>
    <form id="addProductForm" class="space-y-3">
      <input type="text" id="newName" placeholder="Product Name" class="w-full border p-2 rounded" required>
      <input type="text" id="newPrice" placeholder="Price (₹)" class="w-full border p-2 rounded" required>
      <input type="url" id="newImage" placeholder="Image URL" class="w-full border p-2 rounded" required>
      <textarea id="newDesc" placeholder="Description" class="w-full border p-2 rounded" required></textarea>
      <button type="submit" class="w-full bg-blue-600 text-white p-2 rounded hover:bg-blue-700">Add Product</button>
    </form>
  </section>

  <!-- SCRIPT -->
  <script>
    const productList = document.getElementById("product-list");
    let products = JSON.parse(localStorage.getItem("products")) || [
      {
        name: "Stylish T-Shirt",
        price: "₹499",
        image: "https://via.placeholder.com/300x200?text=T-Shirt",
        desc: "Cotton comfort, various sizes"
      },
      {
        name: "Running Shoes",
        price: "₹1199",
        image: "https://via.placeholder.com/300x200?text=Shoes",
        desc: "Lightweight, durable"
      }
    ];

    function saveProducts() {
      localStorage.setItem("products", JSON.stringify(products));
    }

    function renderProducts() {
      productList.innerHTML = "";
      products.forEach((p, index) => {
        productList.innerHTML += `
          <div class="bg-white p-4 rounded shadow relative">
            <button onclick="deleteProduct(${index})" class="absolute top-2 right-2 bg-red-500 text-white px-2 py-1 text-xs rounded hover:bg-red-600 hidden admin-btn">Delete</button>
            <img src="${p.image}" alt="${p.name}" class="w-full h-48 object-cover rounded mb-3">
            <h4 class="font-bold">${p.name}</h4>
            <p>Price: ${p.price}</p>
            <p class="text-sm text-gray-600">${p.desc}</p>
          </div>
        `;
      });
    }

    function deleteProduct(index) {
      if (confirm("Delete this product?")) {
        products.splice(index, 1);
        saveProducts();
        renderProducts();
        showDeleteButtons();
      }
    }

    renderProducts();

    document.getElementById("addProductForm").addEventListener("submit", function (e) {
      e.preventDefault();
      const name = document.getElementById("newName").value;
      const price = document.getElementById("newPrice").value;
      const image = document.getElementById("newImage").value;
      const desc = document.getElementById("newDesc").value;
      products.push({ name, price, image, desc });
      saveProducts();
      renderProducts();
      showDeleteButtons();
      this.reset();
    });

    function checkAdminPassword() {
      const correctPassword = "yourmarket123";
      const input = document.getElementById("adminPassword").value;
      const error = document.getElementById("adminError");
      const panel = document.getElementById("adminPanel");
      if (input === correctPassword) {
        panel.classList.remove("hidden");
        error.classList.add("hidden");
        document.getElementById("loginBox").classList.add("hidden");
        showDeleteButtons();
      } else {
        error.classList.remove("hidden");
      }
    }

    function showDeleteButtons() {
      document.querySelectorAll(".admin-btn").forEach(btn => btn.classList.remove("hidden"));
    }

    function submitOrder(e) {
      e.preventDefault();
      const name = document.getElementById("orderName").value;
      const mobile = document.getElementById("orderMobile").value;
      const product = document.getElementById("orderProduct").value;
      const address = document.getElementById("orderAddress").value;

      const message = `🛒 *New Order*%0A%0A👤 Name: ${name}%0A📞 Mobile: ${mobile}%0A📦 Product: ${product}%0A🏠 Address: ${address}%0A💰 Payment: Cash on Delivery`;

      const whatsappURL = `https://wa.me/919667302392?text=${message}`;
      window.open(whatsappURL, '_blank');
      document.getElementById("orderForm").reset();
    }
  </script>

</body>
</html>
