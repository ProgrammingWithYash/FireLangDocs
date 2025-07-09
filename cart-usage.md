# The Ultimate Guide to FlickSell's Template Cart

Welcome, developer! This guide is your one-stop resource for mastering the `<flicksell-template-cart>`. This powerful component is the recommended way to build a product purchasing interface in any FlickSell theme. It's designed to be incredibly flexible and easy to use—you simply provide a product ID, and it handles all the complex data fetching and state management for you.

---

## 🚀 Chapter 1: Your First Product Page

Let's dive right in and build a functional product UI in minutes.

### 1.1: The Basic Structure

The core idea is simple: you create HTML templates for how you want things to look, and FlickSell populates them with live data.

Here is the essential structure. Copy and paste this into your product page.

```html
<!-- The main wrapper for a single product's cart interface -->
<flicksell-template-cart product-id="123">

    <!-- Part 1: Skeleton Loader (Optional, but recommended) -->
    <!-- This is shown automatically while product data is loading. -->
    <flicksell-skeleton>
        <div style="height: 40px; background: #eee; border-radius: 8px; margin-bottom: 1rem;"></div>
        <div style="height: 20px; width: 50%; background: #eee; border-radius: 8px;"></div>
    </flicksell-skeleton>

    <!-- Part 2: Variant Selection Template -->
    <!-- This section defines how variant groups (like "Color", "Size") are rendered. -->
    <flicksell-variant-groups>
        <!-- This is a template for a SINGLE variant group. It will be duplicated for each group found. -->
        <flicksell-variant-group>
            <flicksell-variant-group-label>
                <!-- The group name (e.g., "Color") will be inserted here automatically. -->
            </flicksell-variant-group-label>
            
            <flicksell-variant-pills>
                <!-- This is a template for a SINGLE variant option. It will be duplicated for each option in the group. -->
                <flicksell-template-variant-pill class="my-custom-pill-style">
                    <!-- The option name (e.g., "Red", "Large") will be inserted here. -->
                </flicksell-template-variant-pill>
            </flicksell-variant-pills>
        </flicksell-variant-group>
    </flicksell-variant-groups>

    <!-- Part 3: Pricing Display -->
    <div class="price-container" style="margin-top: 1rem;">
        <flicksell-template-product-price class="current-price"></flicksell-template-product-price>
        <flicksell-template-product-mrp class="original-price"></flicksell-template-product-mrp>
    </div>

    <!-- Part 4: Action Buttons -->
    <!-- "Add to Cart" button - automatically shown/hidden -->
    <flicksell-template-add-to-cart>
        <button class="btn-add-to-cart">
            <flicksell-template-add-to-cart-normal-content>Add to Cart</flicksell-template-add-to-cart-normal-content>
            <flicksell-template-add-to-cart-loading-content>Adding...</flicksell-template-add-to-cart-loading-content>
        </button>
    </flicksell-template-add-to-cart>

    <!-- "Update Cart" controls - automatically shown/hidden -->
    <flicksell-template-update-cart>
        <div class="quantity-selector">
            <flicksell-template-quantity-decrement><button>-</button></flicksell-template-quantity-decrement>
            <flicksell-template-quantity-input><input type="number" min="0" value="1"></flicksell-template-quantity-input>
            <flicksell-template-quantity-increment><button>+</button></flicksell-template-quantity-increment>
        </div>
        <flicksell-template-update-cart-loading-content>Updating quantity...</flicksell-template-update-cart-loading-content>
    </flicksell-template-update-cart>

</flicksell-template-cart>
```

**How It Works:**

1.  `<flicksell-template-cart>` fetches all data for product `123`.
2.  While loading, it displays whatever is inside `<flicksell-skeleton>`.
3.  Once loaded, it hides the skeleton and builds the UI using your templates.
4.  It intelligently shows either the "Add to Cart" or the "Update Cart" controls based on whether the selected variant is already in the user's cart. This logic works for both guest and logged-in users.

### 1.2: Styling Your Cart

You have 100% control over the appearance using CSS. The system adds helpful attributes to the generated elements for easy styling.

#### Key CSS Selectors:

| Selector                                      | Description                                                                                                   |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `flicksell-template-variant-pill`             | Styles all variant pills.                                                                                     |
| `flicksell-template-variant-pill[selected]`   | Styles the pill the user has currently selected.                                                              |
| `flicksell-template-variant-pill[disabled]`   | Styles pills for unavailable variant combinations.                                                            |
| `[dynamic-source-color-pill]`                 | Specifically targets pills generated from a Color Dynamic Source, allowing for unique styling (e.g., no text).  |
| `flicksell-template-add-to-cart[hidden]`      | These elements get a `hidden` attribute when not active. Use this selector to hide them.                        |
| `flicksell-template-update-cart[hidden]`      | A reliable way to hide them is `[hidden] { display: none !important; }`.                                      |

#### Example CSS:

```css
/* A modern, clean style for the variant pills */
flicksell-template-variant-pill {
    display: inline-block;
    padding: 10px 18px;
    margin: 4px;
    border: 1px solid #d1d5db;
    border-radius: 8px;
    background-color: #ffffff;
    cursor: pointer;
    font-weight: 500;
    transition: all 0.2s ease-in-out;
}

flicksell-template-variant-pill:hover {
    border-color: #6366f1;
    color: #6366f1;
}

/* Style for the currently selected pill */
flicksell-template-variant-pill[selected] {
    background-color: #6366f1;
    border-color: #6366f1;
    color: #ffffff;
    box-shadow: 0 4px 14px 0 rgba(99, 102, 241, 0.3);
}

/* Style for pills that are part of an invalid/unavailable combination */
flicksell-template-variant-pill[disabled] {
    opacity: 0.4;
    cursor: not-allowed;
    background-color: #f3f4f6;
}
```

---

## ⚙️ Chapter 2: Advanced Features

Take your product page to the next level with these powerful features.

### 2.1: Real-time Updates with Polling

Keep stock status and pricing perfectly in sync by adding the `poll` attribute. The value is in seconds. Use this judiciously, as it can increase server load.

```html
<!-- Poll for updates every 10 seconds -->
<flicksell-template-cart product-id="123" poll="10">
    ...
</flicksell-template-cart>
```

### 2.2: Callbacks for Variant Changes

Execute custom JavaScript whenever the user selects a different combination of variants. This is essential for updating things *outside* the cart component, like the main product image gallery.

-   `on-variant-change`: A global JavaScript function to call when the selected variant changes.
-   `combination-image-callback`: A more specific callback just for updating an image based on the `img` property of the selected variant.

```html
<img id="main-product-image" src="/path/to/default.jpg" alt="Product Image">

<flicksell-template-cart 
    product-id="123"
    on-variant-change="myGlobalVariantUpdater"
    combination-image-callback="updateMainImage">
</flicksell-template-cart>

<script>
// The most specific callback runs first.
// Use this for the most common use case: updating an image.
function updateMainImage(imagePath) {
    if (imagePath) {
        document.getElementById('main-product-image').src = '/path/to/images/' + imagePath;
    }
}

// A more general callback for handling any other logic.
function myGlobalVariantUpdater(combinationString, variantData) {
    console.log('User selected:', combinationString);
    // e.g., "Size:Medium/Color:Red"

    console.log('Variant details:', variantData);
    // e.g., { price: "999", mrp: "1299", stock: 50, sku: "MY-SKU", img: "path/to/image.jpg" }

    // Your custom logic here, like updating a shipping time estimate
    const shippingElement = document.getElementById('shipping-estimate');
    if (variantData.stock > 0) {
        shippingElement.textContent = 'Ships in 1-2 days.';
    } else {
        shippingElement.textContent = 'Currently out of stock.';
    }
}
</script>
```

### 2.3: Wishlists & "Move to Cart" Mode

The cart component can be adapted for other use cases, like adding an item from a wishlist to the main cart. The `mode="move-to-cart"` attribute changes the component's behavior slightly: after a successful "add to cart" action, it will fire a callback function.

```html
<!-- Inside your wishlist page template -->
<flicksell-template-cart 
    product-id="123" 
    mode="move-to-cart"
    on-cart-action="handleItemMovedFromWishlist">
    
    <!-- You might only have an "Add to Cart" button here -->
    <flicksell-template-add-to-cart>
        <button>Move to Cart</button>
    </flicksell-template-add-to-cart>

</flicksell-template-cart>

<script>
// This function will be called AFTER the item has been successfully added to the cart.
function handleItemMovedFromWishlist(action, productId, combination, quantity) {
    console.log(`Action '${action}' completed for product ${productId}`);
    
    // Now you can safely remove the item from the wishlist UI
    const wishlistItemElement = document.getElementById(`wishlist-item-${productId}`);
    if (wishlistItemElement) {
        wishlistItemElement.remove();
    }

    // And maybe show a confirmation toast
    showToast('Item moved to your cart!');
}
</script>
```

### 2.4: Manual Quantity Updates

By default, changing the quantity in the `<flicksell-template-update-cart>` block will automatically fire a debounced update request. If you want the user to explicitly click an "Update" button, simply add a `<flicksell-template-update-button>` element. Its presence will disable the automatic updates.

```html
<flicksell-template-update-cart>
    <flicksell-template-quantity-input>
        <input type="number" min="0" value="1">
    </flicksell-template-quantity-input>
    
    <!-- The existence of this button disables auto-updates. -->
    <flicksell-template-update-button>
        <button>Update</button>
    </flicksell-template-update-button>
</flicksell-template-update-cart>
```

---

## 🎨 Chapter 3: Mastering Dynamic Sources (Colors)

For variants based on "Dynamic Sources" like colors, you can create a much richer and more visual selection experience.

### 3.1: Rich Color Templates

Provide a special template inside `<flicksell-dynamic-source-templates>` to override the default pill structure for color options.

```html
<flicksell-template-cart product-id="456">
    <flicksell-variant-groups>
        <!-- This is a fallback template for non-dynamic variants (e.g., Size) -->
        <flicksell-variant-group>
            <flicksell-variant-pills>
                <flicksell-template-variant-pill class="pill-size"></flicksell-template-variant-pill>
            </flicksell-variant-pills>
        </flicksell-variant-group>
    </flicksell-variant-groups>

    <!-- Define a special, rich template JUST for dynamic sources -->
    <flicksell-dynamic-source-templates>
        <flicksell-dynamic-source-template source="color">
            <!-- 
              This HTML will be used for any pill generated from a "Color" source.
              The system will automatically populate the inner elements.
            -->
            <div class="color-pill-wrapper" title="The color name will be here">
                <!-- Populated with color swatch/image -->
                <span dynamic-source-color-images></span> 
                <!-- Populated with color name -->
                <span dynamic-source-color-text></span>
            </div>
        </flicksell-dynamic-source-template>
    </flicksell-dynamic-source-templates>
    
    <!-- ... pricing and action buttons ... -->
</flicksell-template-cart>
```

### 3.2: Styling Hooks for Dynamic Pills

When using dynamic source templating, the system adds special attributes to help you write highly specific CSS.

-   `[dynamic-source-color-pill]`: Added to the root `<flicksell-template-variant-pill>` if it's a color.
-   `[dynamic-source-color-images]`: The `<span>` containing the visual color swatch/image.
-   `[dynamic-source-color-text]`: The `<span>` containing the color name.

**Example:** Create a swatch-only pill by hiding the text.

```css
flicksell-template-variant-pill[dynamic-source-color-pill] {
    /* Reset padding for a square look */
    padding: 2px;
    width: 40px;
    height: 40px;
    border-radius: 50%; /* Make it a circle */
}

/* Hide the color name text */
[dynamic-source-color-text] {
    display: none;
}

/* Make the image container fill the pill */
[dynamic-source-color-images] {
    display: block;
    width: 100%;
    height: 100%;
}
```

---

## 📚 Appendix: API & Events

### Required Server Endpoints

For the template cart to function, your server must expose these endpoints:

1.  **`/flicksell-template-cart-data?product_id={id}`**: (GET) Returns a JSON object with all product and variant data.
2.  **`/flicksell-product-cart-status?product_id={id}`**: (GET) Returns a JSON object indicating which variants of this product are in the current user's cart and their quantities.
3.  **`/flicksell-add-to-cart`**: (POST) Adds an item to the cart. Expects `product_id`, `combination`, and `quantity`.
4.  **`/flicksell-update-cart`**: (POST) Updates an item's quantity in the cart. Expects `product_id`, `combination`, and `quantity`.

### Global Cart Event

Listen for the `flicksell:cartUpdated` event on the `document` to know when any cart action (add, update, remove) has successfully completed anywhere on the page. This is perfect for updating a mini-cart icon in your site header.

```javascript
document.addEventListener('flicksell:cartUpdated', function(event) {
    console.log('The cart has changed!');
    
    // Example: Update a cart counter in the header
    const cartCounter = document.getElementById('header-cart-count');
    if (cartCounter) {
        // You would typically fetch the new count from your server here
        updateCartCount(); 
    }
});
```
