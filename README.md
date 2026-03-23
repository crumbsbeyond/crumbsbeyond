[index.html](https://github.com/user-attachments/files/26174688/index.html)
<!DOCTYPE html>
<html>
<head>
  <title>Crumbs & Beyond</title>

  <style>
    body {
      margin: 0;
      font-family: Arial;
      background: #f6f1ea;
      color: #222;
    }

    header {
      background: #111;
      color: #f6d365;
      text-align: center;
      padding: 20px;
    }

    h1 { margin: 0; }

    .layout {
      display: flex;
      flex-wrap: wrap;
    }

    .products {
      flex: 2;
      padding: 20px;
    }

    .cart {
      flex: 1;
      background: white;
      padding: 20px;
      border-left: 2px solid #ddd;
      min-width: 300px;
    }

    .card {
      background: white;
      padding: 15px;
      margin-bottom: 15px;
      border-radius: 10px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    }

    h3 { color: #c49b3b; margin: 0; }

    select, input, textarea {
      width: 100%;
      padding: 8px;
      margin-top: 6px;
      border: 1px solid #ddd;
      border-radius: 6px;
    }

    button {
      width: 100%;
      padding: 10px;
      background: #111;
      color: #f6d365;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      margin-top: 8px;
      font-weight: bold;
    }

    button:hover {
      background: #c49b3b;
      color: white;
    }

    .cart-item {
      font-size: 14px;
      margin-bottom: 6px;
      border-bottom: 1px solid #eee;
      padding-bottom: 5px;
    }

    .total {
      font-size: 20px;
      color: green;
      margin-top: 10px;
    }

    .price {
      font-size: 12px;
      color: #666;
      margin-top: 4px;
    }
  </style>
</head>

<body>

<header>
  <h1>Crumbs & Beyond</h1>
  <p>Fresh • Handmade • Made With Love</p>
</header>

<div class="layout">

  <!-- PRODUCTS -->
  <div class="products">

    <!-- COOKIES -->
    <div class="card">
      <h3>Cookies (5oz)</h3>
      <div class="price">
        Single $3.50 • 4 Pack $12 • Half Dozen $18 • Dozen $36
      </div>

      <select id="cookieFlavor">
        <option>Chocolate Chip</option>
        <option>Banana Pudding</option>
        <option>Strawberry</option>
        <option>Lemon</option>
        <option>Red Velvet</option>
        <option>Biscoff</option>
        <option>Strawberry Banana</option>
        <option>Sweet Potato Pie</option>
        <option>S’more</option>
        <option>Reese Peanut Butter</option>
      </select>

      <select id="cookiePack">
        <option value="3.5">Single</option>
        <option value="12">4 Pack</option>
        <option value="18">Half Dozen</option>
        <option value="36">Dozen</option>
      </select>

      <button onclick="add('Cookies','cookieFlavor','cookiePack')">Add to Cart</button>
    </div>

    <!-- BROWNIES -->
    <div class="card">
      <h3>Brownies</h3>
      <div class="price">
        Single $6 • 4 Pack $22 • Half Dozen $33 • Dozen $66
      </div>

      <select id="brownieFlavor">
        <option>Butter Pecan</option>
        <option>Oreo</option>
        <option>Red Velvet</option>
        <option>Blue Velvet</option>
        <option>Strawberry Crunch</option>
        <option>Frosted</option>
        <option>Snickerdoodle</option>
      </select>

      <select id="browniePack">
        <option value="6">Single</option>
        <option value="22">4 Pack</option>
        <option value="33">Half Dozen</option>
        <option value="66">Dozen</option>
      </select>

      <button onclick="add('Brownies','brownieFlavor','browniePack')">Add to Cart</button>
    </div>

    <!-- CAKE POPS -->
    <div class="card">
      <h3>Cake Pops</h3>
      <div class="price">
        Half Dozen $20 • Dozen $35
      </div>

      <select id="cakeFlavor">
        <option>Vanilla</option>
        <option>Chocolate</option>
        <option>Strawberry</option>
        <option>Oreo</option>
        <option>Snickerdoodle</option>
        <option>Pineapple</option>
        <option>Lemon</option>
      </select>

      <select id="cakePack">
        <option value="20">Half Dozen</option>
        <option value="35">Dozen</option>
      </select>

      <button onclick="add('Cake Pops','cakeFlavor','cakePack')">Add to Cart</button>
    </div>

    <!-- BROWNIE POPS -->
    <div class="card">
      <h3>Brownie Pops</h3>
      <div class="price">
        Half Dozen $25 • Dozen $45
      </div>

      <select id="bpopsFlavor">
        <option>Vanilla</option>
        <option>Chocolate</option>
        <option>Strawberry</option>
        <option>Oreo</option>
        <option>Snickerdoodle</option>
        <option>Pineapple</option>
        <option>Lemon</option>
      </select>

      <select id="bpopsPack">
        <option value="25">Half Dozen</option>
        <option value="45">Dozen</option>
      </select>

      <button onclick="add('Brownie Pops','bpopsFlavor','bpopsPack')">Add to Cart</button>
    </div>

  </div>

  <!-- CART -->
  <div class="cart">

    <h2>🛒 Cart</h2>
    <div id="cart"></div>

    <div class="total">
      Total: $<span id="total">0</span>
    </div>

    <hr>

    <form onsubmit="sendOrder(event)">

      <input type="text" placeholder="Name" required>
      <input type="email" placeholder="Email" required>

      <label>Pickup Date</label>
      <input type="date" required>

      <label>Pickup Time</label>
      <select required>
        <option>10:00 AM</option>
        <option>12:00 PM</option>
        <option>3:00 PM</option>
        <option>5:00 PM</option>
      </select>

      <textarea placeholder="Notes"></textarea>

      <button type="submit">Place Order</button>

    </form>

  </div>

</div>

<script>
let cart = [];

function add(item, flavorId, priceId) {
  let flavor = document.getElementById(flavorId).value;
  let price = parseFloat(document.getElementById(priceId).value);

  cart.push({item, flavor, price});
  render();
}

function render() {
  let html = "";
  let total = 0;

  cart.forEach(c => {
    html += `<div class="cart-item">${c.item} - ${c.flavor} - $${c.price}</div>`;
    total += c.price;
  });

  document.getElementById("cart").innerHTML = html;
  document.getElementById("total").innerText = total;
}

function sendOrder(e){
  e.preventDefault();
  alert("Order placed successfully! Cart total: $" + document.getElementById("total").innerText);
}
</script>

</body>
</html>
