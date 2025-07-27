<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Sale4u - Cash on Delivery Order</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      margin: 0;
    }

    .form-container {
      background-color: #fff;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
      width: 100%;
      max-width: 500px;
      box-sizing: border-box;
    }

    h2 {
      color: #2c3e50;
      text-align: center;
      margin-bottom: 10px;
    }

    .info-line {
      text-align: center;
      font-size: 15px;
      color: #27ae60;
      margin-bottom: 5px;
    }

    .info-line.replace {
      color: #e67e22;
      margin-bottom: 20px;
    }

    p {
      text-align: center;
      color: #666;
      margin-bottom: 20px;
    }

    .form-group {
      margin-bottom: 18px;
    }

    label {
      display: block;
      margin-bottom: 6px;
      color: #333;
      font-weight: bold;
    }

    input[type="text"],
    textarea {
      width: 100%;
      padding: 12px;
      border: 1px solid #ccc;
      border-radius: 6px;
      font-size: 16px;
      box-sizing: border-box;
    }

    textarea {
      resize: vertical;
      min-height: 80px;
    }

    .whatsapp-button {
      display: block;
      width: 100%;
      padding: 14px;
      background-color: #25D366;
      color: #fff;
      text-align: center;
      text-decoration: none;
      border-radius: 8px;
      font-size: 18px;
      font-weight: bold;
      margin-top: 25px;
      transition: background-color 0.3s ease;
    }

    .whatsapp-button:hover {
      background-color: #1DA851;
    }

    .note {
      font-size: 14px;
      color: #777;
      text-align: center;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <div class="form-container">
    <h2>Sale4u - Cash on Delivery</h2>
    <div class="info-line">✅ Delivery in 3 to 4 Days</div>
    <div class="info-line replace">🔄 5-Day Replacement Guarantee</div>

    <p>Fill in your details to place an order. We offer <strong>Cash on Delivery</strong> only.</p>

    <form id="orderForm">
      <div class="form-group">
        <label for="fullName">Full Name:</label>
        <input type="text" id="fullName" name="fullName" required />
      </div>

      <div class="form-group">
        <label for="address">Delivery Address:</label>
        <textarea id="address" name="address" required></textarea>
      </div>

      <div class="form-group">
        <label for="mobileNumber">Mobile Number:</label>
        <input type="text" id="mobileNumber" name="mobileNumber" pattern="[0-9]{10}" title="Please enter a 10-digit mobile number" required />
      </div>

      <a href="#" id="whatsappLink" class="whatsapp-button">Send Order on WhatsApp</a>
    </form>

    <p class="note">Your order will be sent to us via WhatsApp. Please make sure all details are correct before sending.</p>
  </div>

  <script>
    document.getElementById('whatsappLink').addEventListener('click', function (event) {
      event.preventDefault();

      const name = document.getElementById('fullName').value.trim();
      const address = document.getElementById('address').value.trim();
      const mobile = document.getElementById('mobileNumber').value.trim();

      if (!name || !address || !mobile) {
        alert("Please fill in all the fields before submitting.");
        return;
      }

      const message = `📦 *New COD Order from Sale4u*\n\n👤 Name: ${name}\n🏠 Address: ${address}\n📱 Mobile: ${mobile}\n\nI would like to place a *Cash on Delivery* order.`;

      const whatsappNumber = "919667302392";
      const whatsappURL = `https://wa.me/${whatsappNumber}?text=${encodeURIComponent(message)}`;

      window.open(whatsappURL, "_blank");
    });
  </script>
</body>
</html>
