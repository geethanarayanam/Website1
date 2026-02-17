<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vastramanjiri | Boutique</title>
    <style>
        :root { --maroon: #800000; --gold: #d4af37; }
        body { margin: 0; font-family: 'Arial', sans-serif; background: #fffaf0; }
        
        /* Header */
        header { background: var(--maroon); color: var(--gold); padding: 30px; text-align: center; position: sticky; top: 0; z-index: 1000; }
        
        /* Product Grid */
        .shop-container { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; padding: 20px; }
        
        .saree-card { background: white; border: 1px solid #eee; padding: 10px; border-radius: 10px; text-align: center; }
        .saree-card img { width: 100%; height: 250px; object-fit: cover; border-radius: 5px; }
        .saree-card h3 { font-size: 1.1rem; margin: 10px 0; color: #333; }
        .price { color: var(--maroon); font-weight: bold; font-size: 1.2rem; }
        
        .buy-btn { background: var(--maroon); color: white; border: none; width: 100%; padding: 10px; border-radius: 5px; cursor: pointer; margin-top: 10px; }

        /* Payment Modal */
        #checkout { display:none; position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.8); justify-content:center; align-items:center; z-index:2000; }
        .modal-box { background:white; padding: 25px; border-radius: 15px; width: 90%; max-width: 400px; }
        input { width: 100%; padding: 12px; margin: 8px 0; border: 1px solid #ddd; border-radius: 5px; box-sizing: border-box; }
        
        .pay-now { background: #27ae60; color: white; border: none; width: 100%; padding: 15px; font-size: 1.1rem; border-radius: 5px; cursor: pointer; }
    </style>
</head>
<body>

<header>
    <h1>VASTRAMANJIRI</h1>
    <p>Premium Saree Collection</p>
</header>

<div class="shop-container" id="product-grid">
    </div>

<div id="checkout">
    <div class="modal-box">
        <h2 style="color:var(--maroon)">Secure Checkout</h2>
        <input type="text" id="custName" placeholder="Your Full Name">
        <input type="text" id="cardNumber" placeholder="Card Number (16 digits)">
        <div style="display:flex; gap:10px;">
            <input type="text" id="expiry" placeholder="MM/YY">
            <input type="password" id="cvv" placeholder="CVV">
        </div>
        <button class="pay-now" onclick="completeOrder()">Pay & Notify Vastramanjiri</button>
        <button onclick="document.getElementById('checkout').style.display='none'" style="background:none; border:none; color:grey; margin-top:10px; cursor:pointer;">Cancel</button>
    </div>
</div>

<script>
    // DATA FOR 100 SAREES
    // To add more, simply add more items to this list [...]
    const sarees = [
        { id: 1, name: "Banarasi Silk", price: "4500", img: "https://via.placeholder.com/300x400?text=Saree+1" },
        { id: 2, name: "Kanchipuram Red", price: "5200", img: "https://via.placeholder.com/300x400?text=Saree+2" },
        { id: 3, name: "Chanderi Floral", price: "2800", img: "https://via.placeholder.com/300x400?text=Saree+3" },
        // ... You can add up to 100 here
    ];

    let selectedSaree = "";

    // Load Sarees into the page
    const grid = document.getElementById('product-grid');
    sarees.forEach(s => {
        grid.innerHTML += `
            <div class="saree-card">
                <img src="${s.img}" alt="${s.name}">
                <h3>${s.name}</h3>
                <p class="price">₹${s.price}</p>
                <button class="buy-btn" onclick="openCheckout('${s.name}', '${s.price}')">Add to Cart</button>
            </div>
        `;
    });

    function openCheckout(name, price) {
        selectedSaree = name + " (₹" + price + ")";
        document.getElementById('checkout').style.display = 'flex';
    }

    function completeOrder() {
        const name = document.getElementById('custName').value;
        if(!name) { alert("Please enter your name"); return; }

        // NOTIFICATION LOGIC: 
        // This will open WhatsApp with the order details to notify YOU!
        const myPhoneNumber = "91XXXXXXXXXX"; // <-- REPLACE WITH YOUR PHONE NUMBER
        const message = `New Order from Vastramanjiri Website!%0A%0AItem: ${selectedSaree}%0ACustomer: ${name}%0APayment: Card Details Provided.`;
        
        window.open(`https://wa.me/${myPhoneNumber}?text=${message}`, '_blank');
        
        alert("Payment Processed! You will be redirected to WhatsApp to confirm the order details with Vastramanjiri.");
        document.getElementById('checkout').style.display = 'none';
    }
</script>

</body>
</html>
