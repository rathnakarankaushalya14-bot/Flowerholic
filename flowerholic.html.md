<!DOCTYPE html>  
<html lang="en">  
<head>  
<meta charset="UTF-8">  
<meta name="viewport" content="width=device-width, initial-scale=1.0">  
<title>FLOWERHOLIC</title>  
  
<style>  
body {  
    margin: 0;  
    font-family: 'Poppins', sans-serif;  
    background: linear-gradient(#ffeef3, #fff);  
    position: relative;  
}  
  
/* GLOW CURSOR */  
.cursor {  
    position: fixed;  
    width: 15px;  
    height: 15px;  
    background: #ff4f81;  
    border-radius: 50%;  
    pointer-events: none;  
    box-shadow: 0 0 15px #ff4f81, 0 0 30px #ff4f81;  
    transform: translate(-50%, -50%);  
}  
  
/* NAV */  
nav {  
    position: fixed;  
    width: 100%;  
    background: white;  
    display: flex;  
    justify-content: center;  
    gap: 15px;  
    padding: 10px;  
    z-index: 1000;  
}  
  
nav a {  
    text-decoration: none;  
    color: #ff4f81;  
    font-weight: bold;  
    position: relative; /* badge positioning */  
}  
  
/* CART BADGE */  
#cartBadge {  
    position: absolute;  
    top: -5px;  
    right: -10px;  
    background: #ff4f81;  
    color: white;  
    font-size: 12px;  
    width: 18px;  
    height: 18px;  
    border-radius: 50%;  
    display: flex;  
    align-items: center;  
    justify-content: center;  
}  
  
/* HEADER */  
header {  
    height: 100vh;  
    display: flex;  
    justify-content: center;  
    align-items: center;  
    flex-direction: column;  
}  
  
header h1 {  
    color: #ff4f81;  
    font-size: 3em;  
}  
  
.btn {  
    background: #ff4f81;  
    color: white;  
    padding: 10px 20px;  
    border-radius: 20px;  
    border: none;  
    cursor: pointer;  
    margin-top: 5px;  
    transition: all 0.3s ease;  
}  
  
/* GLOW EFFECT ON BUTTON HOVER */  
.btn:hover {  
    box-shadow: 0 0 15px #ff4f81, 0 0 30px #ff4f81;  
    transform: scale(1.05);  
}  
  
/* SECTION */  
section {  
    padding: 80px 20px;  
    max-width: 900px;  
    margin: auto;  
}  
  
.card {  
    background: white;  
    padding: 15px;  
    margin: 10px 0;  
    border-radius: 15px;  
    box-shadow: 0 5px 15px rgba(0,0,0,0.1);  
}  
</style>  
</head>  
  
<body>  
  
<div class="cursor" id="cursor"></div>  
  
<nav>  
<a href="#home">Home</a>  
<a href="#products">Products</a>  
<a href="#cart">Cart  
  <span id="cartBadge">0</span>  
</a>  
<a href="#contact">Contact</a>  
</nav>  
  
<header id="home">  
<h1>FLOWERHOLIC💐</h1>  
<p>Pure floral love</p>  
</header>  
  
<section id="products">  
<h2>Products</h2>  
  
<div class="card">  
<h3>DIY Tulip Kit 🌷</h3>  
<p>Rs.300</p>  
<button class="btn" onclick="addToCart('DIY Tulip Kit',300)">Add to Cart</button>  
</div>  
  
<div class="card">  
<h3>Custom Bouquet 💐</h3>  
<p>Rs.500</p>  
<button class="btn" onclick="addToCart('Custom Bouquet',500)">Add to Cart</button>  
</div>  
  
</section>  
  
<section id="cart">  
<h2>Your Cart 🛒</h2>  
<div class="card" id="cartItems">No items yet</div>  
<button class="btn" onclick="checkout()">Checkout via WhatsApp</button>  
</section>  
  
<section id="contact">  
<h2>Contact</h2>  
<div class="card">  
<p>📞 94762819290</p>  
<p>📱 @flowerholix</p>  
</div>  
</section>  
  
<script>  
let cart = JSON.parse(localStorage.getItem('cart')) || [];  
  
// Add item to cart  
function addToCart(name, price) {  
    cart.push({name, price});  
    localStorage.setItem('cart', JSON.stringify(cart));  
    displayCart();  
    updateBadge();  
    alert(`🌸 Added "${name}" to your cart!`);  
}  
  
// Display cart  
function displayCart() {  
    let cartDiv = document.getElementById("cartItems");  
    if (cart.length === 0) {  
        cartDiv.innerHTML = "No items yet";  
        return;  
    }  
  
    let html = "";  
    let total = 0;  
  
    cart.forEach(item => {  
        html += item.name + " - Rs." + item.price + "<br>";  
        total += item.price;  
    });  
  
    html += "<br><b>Total: Rs." + total + "</b>";  
    cartDiv.innerHTML = html;  
}  
  
// Update badge  
function updateBadge() {  
    document.getElementById("cartBadge").innerText = cart.length;  
}  
  
// Checkout  
function checkout() {  
    if (cart.length === 0) {  
        alert("Your cart is empty! 🌸");  
        return;  
    }  
  
    let message = "Hello! I want to order 💐%0A%0A";  
    cart.forEach(item => {  
        message += item.name + " - Rs." + item.price + "%0A";  
    });  
  
    var number = "94762819290"; // your number  
    window.location.href = "https://wa.me/" + number + "?text=" + message;  
  
    // Clear cart after checkout  
    cart = [];  
    localStorage.removeItem('cart');  
    displayCart();  
    updateBadge();  
}  
  
/* SMOOTH CURSOR EFFECT */  
let cursor = document.getElementById("cursor");  
let mouseX = 0, mouseY = 0;  
  
document.addEventListener("mousemove", e => {  
    mouseX = e.clientX;  
    mouseY = e.clientY;  
});  
  
function animateCursor() {  
    let cx = parseFloat(cursor.style.left || 0);  
    let cy = parseFloat(cursor.style.top || 0);  
    cursor.style.left = cx + (mouseX - cx) * 0.15 + "px";  
    cursor.style.top = cy + (mouseY - cy) * 0.15 + "px";  
    requestAnimationFrame(animateCursor);  
}  
animateCursor();  
  
// Initialize cart on load  
displayCart();  
updateBadge();  
</script>  
  
</body>  
</html>  
