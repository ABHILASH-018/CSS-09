# CSS-9: Thala 7 Footwear Co. E-Commerce Website

This is a multi-page e-commerce website interface designed for a CSS layout assignment. It features modern typography, a fixed header navigation, responsive Flexbox-based grids/rows, and simple, hand-crafted JavaScript interactivity suitable for a beginner.

---

## 📂 Project Structure

This project consists of the following files:

- **`index.html`**: The home page of the website. Includes a hero section with a call-to-action (CTA) button, a service stats banner, and footer copyright information.
- **`product.html`**: The product details page. Showcases the "Thala Impulse 7" footwear with a description, color/size selection, quantity selector, and a thumbnail gallery image-switcher.
- **`cart.html`**: The shopping cart page. Lists items, calculates subtotal/taxes/totals, enables quantity increment/decrement, support for promo codes (`THALA7`), and item removal.
- **`payment.html`**: The checkout page. Allows simulating a purchase with options for Credit Card or Cash on Delivery, including fields validation and final redirection.
- **`styles.css`**: The central stylesheet containing all colors, Flexbox layout declarations, container definitions, and visual formatting rules.
- **Image Assets (`*.png`)**: Product and showcase graphics (`hero-shoe.png`, `shoe-1.png`, etc.).
- **`README.md`**: Project setup instructions and step-by-step code explanation document (this file).

---

## 🚀 How to Run and Setup

1. **Locate Folder**: Locate the folder containing this project (e.g., `CSS-9`).
2. **Open HTML File**: Double-click the `index.html` file (or right-click and choose **Open With...** -> select Google Chrome, Microsoft Edge, Mozilla Firefox, or Safari).
3. **Navigate pages**: Click the links in the header navigation (Home, Product Details, Shopping Cart, Checkout) to navigate between the pages.
4. **Open Developer Console**: To verify the interactive functions, press **F12** on your keyboard (or right-click anywhere on the page, select **Inspect**, and click the **Console** tab).

---

## 💡 JavaScript Function Explanations

Each interactive feature was rewritten using basic DOM methods (`document.getElementById`, `document.getElementsByClassName`), standard `for` loops, and standard `var` assignments. Below are explanations of each function so you can explain your code line-by-line.

### 1. Product Details Page (`product.html`)

#### `changeImage(imagePath, clickedThumbnail)`
This function is triggered when a user clicks on any gallery thumbnail image.
- **How it works:**
  - `document.getElementById('main-product-image').src = imagePath;` — Changes the `src` attribute of the main product image to show the clicked image.
  - `var thumbnails = document.getElementsByClassName('gallery-thumbnail');` — Grabs all thumbnail elements on the page as an array-like list.
  - `for (var i = 0; i < thumbnails.length; i++) { thumbnails[i].classList.remove('active'); }` — Loops through every single thumbnail and removes the class name `active` so they no longer have the active border style.
  - `clickedThumbnail.classList.add('active');` — Adds the `active` class to the thumbnail that the user clicked to highlight it.

#### `updateQty(amount)`
This function runs when a user clicks the plus (`+`) or minus (`-`) quantity buttons on the product page.
- **How it works:**
  - `var qtyInput = document.getElementById('qty-value');` — Grabs the number input field.
  - `var currentVal = parseInt(qtyInput.value);` — Converts the input value string to an integer.
  - `if (isNaN(currentVal)) { currentVal = 1; }` — If the input value is empty or not a valid number, sets the value to `1`.
  - `currentVal = currentVal + amount;` — Adds or subtracts the quantity amount (e.g., `+1` or `-1`).
  - `if (currentVal < 1) { currentVal = 1; }` — Safeguards the quantity so it cannot drop below `1`.
  - `qtyInput.value = currentVal;` — Updates the text field with the new quantity.

---

### 2. Shopping Cart Page (`cart.html`)

#### `changeQtyRow(button, amount)`
Adjusts the quantity of a specific item in the cart table.
- **How it works:**
  - `var parentDiv = button.parentNode;` — Gets the button's parent element (the container wrapping the input and spinner buttons).
  - `var inputField = parentDiv.getElementsByClassName('row-qty')[0];` — Finds the input field with class name `row-qty` inside that parent container.
  - `var currentVal = parseInt(inputField.value);` — Parses the value as an integer.
  - `if (isNaN(currentVal)) { currentVal = 1; }` — Falls back to `1` if invalid.
  - `currentVal = currentVal + amount;` — Modifies the quantity value.
  - `if (currentVal < 1) { currentVal = 1; }` — Keeps the quantity at least `1`.
  - `inputField.value = currentVal;` — Writes the new quantity value back to the input.
  - `recalcCart();` — Recalculates the subtotal, taxes, discount, and grand total prices.

#### `removeCartRow(button)`
Deletes a row from the cart table.
- **How it works:**
  - `var row = button.parentNode.parentNode;` — Walks up the DOM. The button's parent is the `<td>` tag, and the `<td>`'s parent is the `<tr>` (table row) tag.
  - `if (row) { row.parentNode.removeChild(row); recalcCart(); }` — If the row is found, uses the table body (`row.parentNode`) to remove that row (`removeChild(row)`) and triggers a recalculation of the totals.

#### `recalcCart()`
Calculates the shopping cart prices and updates the order summary.
- **How it works:**
  - `var itemRows = document.getElementsByClassName('cart-item-row');` — Grabs all row elements in the cart table.
  - It uses a standard `for` loop `for (var i = 0; i < itemRows.length; i++)` to loop through every row:
    - `var priceText = row.getElementsByClassName('unit-price')[0].innerText;` — Gets the price text (e.g. `"$149.00"`).
    - `var priceVal = parseFloat(priceText.slice(1));` — Slices off the first character (the `$`) and converts the remaining text to a decimal number.
    - `var qtyInput = row.getElementsByClassName('row-qty')[0];` and `var qtyVal = parseInt(qtyInput.value);` — Gets the current quantity.
    - `var rowTotal = priceVal * qtyVal;` — Calculates total price for this row.
    - `row.getElementsByClassName('row-total')[0].innerText = '$' + rowTotal.toFixed(2);` — Updates the total price column text formatted to 2 decimal places.
    - `totalSubtotal = totalSubtotal + rowTotal;` and `totalItemsCount = totalItemsCount + qtyVal;` — Accumulates running totals.
  - `var salesTax = totalSubtotal * 0.10;` — Calculates 10% sales tax.
  - Checks if `isPromoApplied` is `true`. If so, calculates a 10% coupon discount (`(totalSubtotal + salesTax) * 0.10`), displays the discount row, and sets its text. Otherwise, hides the discount row.
  - `var grandTotal = totalSubtotal + salesTax - discountVal;` — Computes the grand total.
  - Updates the subtotal, tax, and grand total text displays in the Order Summary card.
  - `document.getElementById('cart-badge').innerText = totalItemsCount;` — Updates the notification badge count in the navigation bar.

#### `applyPromoCode()`
Validates code entry in the coupon field.
- **How it works:**
  - `var codeVal = promoInput.value.trim().toUpperCase();` — Grabs user entry, trims white space, and converts it to upper-case.
  - If code is `'THALA7'`, sets `isPromoApplied = true` and updates status message text in green. Otherwise, sets `isPromoApplied = false` and shows error text in red.
  - Calls `recalcCart()` to re-apply calculation based on the coupon state.

---

### 3. Checkout Page (`payment.html`)

#### `toggleCardForm(showCardForm)`
Toggles sections when selecting Credit Card vs alternative methods.
- **How it works:**
  - Sets the `display` style of `credit-card-section` to `'block'` and `alt-redirect-section` to `'none'` if `showCardForm` is true.
  - Otherwise, swaps them so Credit Card inputs are hidden and the external redirect container is shown.

#### `processPayment(event)`
Simulates checkout form completion.
- **How it works:**
  - `event.preventDefault();` — Stop form from reloading the page automatically.
  - `var lastFourDigits = cardNum.substring(cardNum.length - 4);` — Extracts the final 4 digits of the card number for secure receipt simulation.
  - `alert(...);` — Triggers browser alert indicating confirmation.
  - `window.location.href = 'index.html';` — Redirects browser to the home page.

#### `processAltRedirect()`
- Shows a simple notification alert and redirects to the home page.
