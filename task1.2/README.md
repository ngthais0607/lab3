#  Lab 04 – Task 1.2: Dynamic Shopping Cart

##  1. Objective
- To create a **dynamic shopping cart** that allows adding, removing, and updating product quantities using JavaScript.
- To apply DOM manipulation and event-driven programming concepts.
- To reinforce understanding of **arrays**, **object manipulation**, and **real-time UI updates** in JavaScript.

## ⚙️ 2. Tools & Environment
| Component | Description |
|------------|-------------|
| Languages | HTML, CSS, JavaScript |
| Browser | Google Chrome / Microsoft Edge |
| IDE | Visual Studio Code |
| Execution | Open the `.html` file directly in any browser |

##  3. Implementation Details

###  Product Data
```js
const products = [
  { id: 1, name: 'Laptop', price: 999.99, image: '💻' },
  { id: 2, name: 'Smartphone', price: 699.99, image: '📱' },
  { id: 3, name: 'Headphones', price: 199.99, image: '🎧' },
  { id: 4, name: 'Smartwatch', price: 299.99, image: '⌚' }
];
```
Each product contains an **id**, **name**, **price**, and **emoji image**.

###  Cart Structure
```js
let cart = [];
```
The `cart` array stores items currently added by the user. Each item has: `{ id, name, price, qty }`.

### ⚙️ Core Functions and Explanations

#### 1. addToCart(productId)
```js
function addToCart(productId) {
  const product = products.find(p => p.id === productId);
  const existing = cart.find(item => item.id === productId);
  if (existing) existing.qty += 1;
  else cart.push({ ...product, qty: 1 });
  renderCart();
}
```
Adds a new product or increases quantity if it already exists.

#### 2. removeFromCart(itemId)
```js
function removeFromCart(itemId) {
  cart = cart.filter(item => item.id !== itemId);
  renderCart();
}
```
Removes an item entirely from the cart based on its ID.

#### 3. updateQuantity(productId, change)
```js
function updateQuantity(productId, change) {
  const item = cart.find(x => x.id === productId);
  if (!item) return;
  item.qty += change;
  if (item.qty <= 0) removeFromCart(productId);
  else renderCart();
}
```
Adjusts quantity by +1 or −1 and removes item if quantity <= 0.

#### 4. calculateTotal()
```js
function calculateTotal() {
  return cart.reduce((sum, item) => sum + item.price * item.qty, 0);
}
```
Sums the total cost of all items in the cart.

#### 5. renderProducts()
```js
function renderProducts() {
  const grid = document.getElementById('productsGrid');
  grid.innerHTML = products.map(p => `
    <div class="product-card">
      <div class="product-image">${p.image}</div>
      <div class="product-name">${p.name}</div>
      <div class="product-price">$${p.price.toFixed(2)}</div>
      <button class="add-to-cart-btn" onclick="addToCart(${p.id})">Add to Cart</button>
    </div>
  `).join('');
}
```
Generates the product grid dynamically and attaches "Add to Cart" actions.

#### 6. renderCart()
```js
function renderCart() {
  const cartItems = document.getElementById('cartItems');
  const cartTotal = document.getElementById('cartTotal');
  const cartCount = document.getElementById('cartCount');

  const totalCount = cart.reduce((sum, item) => sum + item.qty, 0);
  cartCount.textContent = totalCount;

  if (cart.length === 0) {
    cartItems.innerHTML = '<p>Your cart is empty.</p>';
    cartTotal.textContent = '0.00';
    return;
  }

  cartItems.innerHTML = cart.map(item => `
    <div class="cart-item">
      <div><strong>${item.name}</strong> - $${item.price.toFixed(2)}</div>
      <div class="quantity-controls">
        <button onclick="updateQuantity(${item.id}, -1)">−</button>
        <span>${item.qty}</span>
        <button onclick="updateQuantity(${item.id}, 1)">+</button>
        <button onclick="removeFromCart(${item.id})">Remove</button>
      </div>
    </div>
  `).join('');

  cartTotal.textContent = calculateTotal().toFixed(2);
}
```
Updates product list, total amount, and cart count badge in real time.

#### 7. toggleCart()
```js
function toggleCart() {
  const cartSection = document.getElementById('cartSection');
  cartSection.style.display = cartSection.style.display === 'none' ? 'block' : 'none';
}
```
Toggles the cart visibility when clicking the 🛒 icon.

#### Initialization
```js
renderProducts();
```
Displays the product grid on page load.

##  4. Results
| Action | Behavior |
|--------|-----------|
| Add a product | Product added; cart count increases |
| Click “+” or “−” | Updates quantity instantly |
| Remove item | Deletes item from the cart |
| Toggle 🛒 icon | Shows or hides cart |
| Empty cart | Displays “Your cart is empty” |

All updates occur dynamically without reloading the page.

##  5. Program Flow
1. Page loads → `renderProducts()` creates product list.
2. Clicking "Add to Cart" runs `addToCart()`.
3. The cart updates with `renderCart()`.
4. Quantity buttons trigger `updateQuantity()`.
5. `calculateTotal()` updates the total cost.
6. 🛒 icon toggles cart visibility.

##  6. Conclusion
- Implemented a fully interactive and dynamic shopping cart.
- Practiced DOM manipulation, array methods, and event listeners.
- Enhanced interactivity with real-time updates and calculations.


