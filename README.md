# Smart-save
Coupons for consumers 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>SmartSave Pay – Save with Coupons</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0; padding: 0;
      background-color: #f3f3f3;
      color: #333;
      text-align: center;
    }
    header {
      background-color: #0070f3;
      color: #fff;
      padding: 2rem 1rem;
    }
    .container {
      max-width: 600px;
      margin: 2rem auto;
      background: #fff;
      padding: 1.5rem;
      border-radius: 8px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    }
    h1 { margin-bottom: 1rem; }
    input[type="text"] {
      width: 80%;
      padding: 0.8rem;
      font-size: 1rem;
      margin-bottom: 1rem;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    button {
      padding: 0.8rem 1.5rem;
      font-size: 1rem;
      color: #fff;
      background-color: #0070f3;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
    button:hover {
      background-color: #005bb5;
    }
    .result {
      margin-top: 1.5rem;
      font-size: 1.1rem;
      color: #0070f3;
    }
    footer {
      margin-top: 2rem;
      font-size: 0.9rem;
      color: #777;
    }
  </style>
</head>
<body>
  <header>
    <h1>SmartSave Pay</h1>
    <p>Get the free app that automatically finds coupons at checkout!</p>
  </header>

  <div class="container">
    <h2>Test Our Coupon Finder</h2>
    <p>Enter your store name to see the best coupon we can apply:</p>
    <input type="text" id="storeInput" placeholder="e.g., Amazon">
    <br>
    <button id="findCouponBtn">Find Coupon</button>
    <div class="result" id="resultArea"></div>
  </div>

  <footer>
    &copy; 2025 SmartSave Inc.
  </footer>

  <script>
    // Our coupon database (could be later replaced by an API)
    const coupons = [
      { store: "Target", code: "SAVE10", discount: 10 },
      { store: "Amazon", code: "SPRING20", discount: 20 },
      { store: "Walmart", code: "FREESHIP", discount: 0 }
    ];

    // Function to match the best coupon for a given store name.
    const findBestCoupon = (store) => {
      // Filter coupons for the given store (case-insensitive)
      const filtered = coupons.filter(c => c.store.toLowerCase() === store.trim().toLowerCase());
      if (filtered.length === 0) return null;
      // From the matches, choose the one with the highest discount value
      return filtered.reduce((a, b) => a.discount > b.discount ? a : b);
    };

    // Event listener for the Find Coupon button
    document.getElementById("findCouponBtn").addEventListener("click", () => {
      const store = document.getElementById("storeInput").value;
      const resultArea = document.getElementById("resultArea");

      // Clear previous result
      resultArea.textContent = "";

      if (!store) {
        resultArea.textContent = "Please enter a store name.";
        return;
      }

      const bestCoupon = findBestCoupon(store);
      if (bestCoupon) {
        resultArea.textContent = `Best coupon for ${store}: ${bestCoupon.code} (${bestCoupon.discount}% off)`;
      } else {
        resultArea.textContent = `Sorry, no coupons available for "${store}".`;
      }
    });
  </script>
</body>
</html>