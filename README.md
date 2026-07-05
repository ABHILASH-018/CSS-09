# CSS-9: Thala 7 Footwear - E-Commerce Website

This is my CSS layout assignment where I built a multi-page shoe store website. I used Flexbox and Grid for the layouts, CSS variables for the colour scheme, and kept everything in one shared stylesheet. No JavaScript was used — it's all HTML and CSS.

## Pages

- **index.html** — Home page with a hero banner, stats bar, and product cards
- **product.html** — Shows one product in detail with thumbnail images, size buttons, and a quantity picker
- **cart.html** — Shopping cart with a table of items, a coupon box, and an order summary panel
- **payment.html** — Checkout page with payment method options, a card form, and order overview
- **styles.css** — Single CSS file shared across all pages

## How to open

1. Open the `CSS-9` folder
2. Double-click `index.html` (opens in your default browser)
3. Use the nav links at the top to move between pages

## CSS concepts I used

- **CSS Variables** — defined colours and font in `:root` so they're easy to change everywhere
- **Flexbox** — used for the header nav, hero section, cart layout, payment layout, stats bar
- **CSS Grid** — the product cards on the home page use `grid-template-columns: repeat(auto-fit, minmax(280px, 1fr))` to wrap into rows automatically
- **Fixed header** — `position: fixed` keeps the nav bar at the top when scrolling
- **Hover effects** — product cards lift up on hover, buttons change colour, nav links get an underline
- **Media query** — one `@media (max-width: 768px)` block stacks everything vertically on small screens
- **Google Fonts** — imported Inter font for clean typography
- **Font Awesome** — used icon classes for cart, star, trash, and payment icons

## Promo code

On the cart page there's a coupon input field. The code `THALA7` is shown as a placeholder hint. (The apply logic was removed since this is a CSS-only submission.)

## Notes

- All images are `.png` files in the same folder
- The site is static — no backend, no database
- Tested on Chrome and Edge
