<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="styles.css">
    <title>Shopping Cart</title>
</head>
<body>
    <div id="cart">
        <div class="cart-item" data-price="20">
            <h2>Item 1</h2>
            <button class="decrease">-</button>
            <span class="quantity">1</span>
            <button class="increase">+</button>
            <button class="like">❤️</button>
            <button class="remove">Remove</button>
            <span class="price">$20</span>
        </div>
        <div class="cart-item" data-price="15">
            <h2>Item 2</h2>
            <button class="decrease">-</button>
            <span class="quantity">1</span>
            <button class="increase">+</button>
            <button class="like">❤️</button>
            <button class="remove">Remove</button>
            <span class="price">$15</span>
        </div>
        <div id="total">Total: $35</div>
    </div>
    <script src="script.js"></script>
</body>
</html>

document.addEventListener('DOMContentLoaded', () => {
    const cartItems = document.querySelectorAll('.cart-item');

    cartItems.forEach(item => {
        const priceElement = item.querySelector('.price');
        const quantityElement = item.querySelector('.quantity');
        const increaseButton = item.querySelector('.increase');
        const decreaseButton = item.querySelector('.decrease');
        const removeButton = item.querySelector('.remove');
        const likeButton = item.querySelector('.like');

        increaseButton.addEventListener('click', () => {
            let quantity = parseInt(quantityElement.textContent);
            quantity++;
            quantityElement.textContent = quantity;
            updateTotal();
        });

        decreaseButton.addEventListener('click', () => {
            let quantity = parseInt(quantityElement.textContent);
            if (quantity > 1) {
                quantity--;
                quantityElement.textContent = quantity;
                updateTotal();
            }
        });

        removeButton.addEventListener('click', () => {
            item.remove();
            updateTotal();
        });

        likeButton.addEventListener('click', () => {
            likeButton.classList.toggle('liked');
            likeButton.textContent = likeButton.classList.contains('liked') ? '❤️' : '🤍';
        });
    });

    function updateTotal() {
        let total = 0;
        cartItems.forEach(item => {
            const price = parseFloat(item.dataset.price);
            const quantity = parseInt(item.querySelector('.quantity').textContent);
            total += price * quantity;
        });
        document.getElementById('total').textContent = `Total: $${total}`;
    }
});

body {
    font-family: Arial, sans-serif;
}

#cart {
    width: 300px;
    margin: auto;
}

.cart-item {
    border: 1px solid #ccc;
    padding: 10px;
    margin-bottom: 10px;
}

button {
    margin: 0 5px;
}

.liked {
    color: red;
}
