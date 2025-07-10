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
                    <!-- Note: For "Color" variants, this pill is automatically populated with rich swatch/image content. -->
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

You have 100% control over the appearance using CSS. The system adds helpful attributes and elements to the generated pills for easy styling.

#### Key CSS Selectors:

| Selector                                      | Description                                                                                                   |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `flicksell-template-variant-pill`             | Styles all variant pills.                                                                                     |
| `flicksell-template-variant-pill[selected]`   | Styles the pill the user has currently selected.                                                              |
| `flicksell-template-variant-pill[disabled]`   | Styles pills for unavailable variant combinations.                                                            |
| `flicksell-template-add-to-cart[hidden]`      | These elements get a `hidden` attribute when not active. Use this selector to hide them.                        |
| `flicksell-template-update-cart[hidden]`      | A reliable way to hide them is `[hidden] { display: none !important; }`.                                      |
| `[dynamic-source-color-pill]`                 | Targets pills generated from a Color source for special styling.                                              |
| `[dynamic-source-color-images]`               | The inner `<span>` that the system injects to hold the color swatch or image.                                 |
| `[dynamic-source-color-text]`                 | The inner `<span>` that the system injects to hold the color name.                                            |


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

/* Example: Create swatch-only pills for colors by targeting the auto-injected elements */
flicksell-template-variant-pill[dynamic-source-color-pill] {
    /* Reset padding for a square look */
    padding: 2px;
    width: 40px;
    height: 40px;
    border-radius: 50%; /* Make it a circle */
}

/* Hide the color name text inside the pill */
[dynamic-source-color-text] {
    display: none;
}

/* Make the auto-injected image container fill the pill */
[dynamic-source-color-images] {
    display: block;
    width: 100%;
    height: 100%;
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
-   `combination-not-selected-callback`: Called when user tries to add to cart without selecting a valid combination.

```html
<img id="main-product-image" src="/path/to/default.jpg" alt="Product Image">

<flicksell-template-cart 
    product-id="123"
    on-variant-change="myGlobalVariantUpdater"
    combination-image-callback="updateMainImage"
    combination-not-selected-callback="handleNoSelection">
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

// Called when user tries to add to cart without selecting a combination
function handleNoSelection() {
    alert('Please select all product options before adding to cart.');
    // Or show a more elegant notification
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

### 2.5: Linking Multiple Cart Elements

You can link multiple `<flicksell-template-cart>` elements together so they work as a single unit. This is perfect for complex product pages where you want to show variant selections in different locations (e.g., color picker in the gallery, size selector in the product details).

```html
<!-- Main cart element with cart functionality -->
<flicksell-template-cart 
    product-id="123" 
    id="main-cart"
    linked-with="color-selector,size-selector">
    
    <!-- This element handles the cart actions -->
    <flicksell-template-add-to-cart>
        <button>Add to Cart</button>
    </flicksell-template-add-to-cart>
    
    <!-- Show all variant groups here -->
    <flicksell-variant-groups>
        <flicksell-variant-group>
            <flicksell-variant-group-label></flicksell-variant-group-label>
            <flicksell-variant-pills>
                <flicksell-template-variant-pill></flicksell-template-variant-pill>
            </flicksell-variant-pills>
        </flicksell-variant-group>
    </flicksell-variant-groups>
</flicksell-template-cart>

<!-- Color selector in the image gallery area -->
<flicksell-template-cart 
    product-id="123" 
    id="color-selector"
    fetch-only="Color">
    
    <!-- Only show Color variants here -->
    <flicksell-variant-groups>
        <flicksell-variant-group>
            <flicksell-variant-pills>
                <flicksell-template-variant-pill class="color-swatch"></flicksell-template-variant-pill>
            </flicksell-variant-pills>
        </flicksell-variant-group>
    </flicksell-variant-groups>
</flicksell-template-cart>

<!-- Size selector in the product details -->
<flicksell-template-cart 
    product-id="123" 
    id="size-selector"
    fetch-only="Size">
    
    <!-- Only show Size variants here -->
    <flicksell-variant-groups>
        <flicksell-variant-group>
            <flicksell-variant-group-label></flicksell-variant-group-label>
            <flicksell-variant-pills>
                <flicksell-template-variant-pill class="size-pill"></flicksell-template-variant-pill>
            </flicksell-variant-pills>
        </flicksell-variant-group>
    </flicksell-variant-groups>
</flicksell-template-cart>
```

**How Linking Works:**

1. The main element (with `linked-with` attribute) coordinates all linked elements
2. When a user selects a variant in any linked element, all elements update together
3. Only the main element shows cart controls and handles cart actions
4. All elements share the same product data and selection state

### 2.6: Filtering Variant Groups with fetch-only

Use the `fetch-only` attribute to show only specific variant groups. This is perfect for creating specialized variant selectors or when you want to split variant selection across different UI sections.

```html
<!-- Show only Color and Material variants -->
<flicksell-template-cart 
    product-id="123" 
    fetch-only="Color,Material">
    
    <flicksell-variant-groups>
        <flicksell-variant-group>
            <flicksell-variant-group-label></flicksell-variant-group-label>
            <flicksell-variant-pills>
                <flicksell-template-variant-pill></flicksell-template-variant-pill>
            </flicksell-variant-pills>
        </flicksell-variant-group>
    </flicksell-variant-groups>
</flicksell-template-cart>
```

**Note:** When using `fetch-only`, the system automatically selects the first option from hidden variant groups to ensure a valid combination is always available.

### 2.7: Disabling Auto-Selection

By default, the system automatically selects the first available option from each variant group. Use `no-auto-select` to disable this behavior if you want users to explicitly choose all options.

```html
<!-- User must select all options manually -->
<flicksell-template-cart 
    product-id="123" 
    no-auto-select>
    
    <flicksell-variant-groups>
        <flicksell-variant-group>
            <flicksell-variant-group-label></flicksell-variant-group-label>
            <flicksell-variant-pills>
                <flicksell-template-variant-pill></flicksell-template-variant-pill>
            </flicksell-variant-pills>
        </flicksell-variant-group>
    </flicksell-variant-groups>
</flicksell-template-cart>
```

### 2.8: Customizing Dynamic Source Display (e.g., Colors)

When you have variants that use a dynamic data source, like "Color", the system automatically renders rich content like color swatches or images inside the variant pills. You can control how this content is displayed using the `color-source-style` attribute.

```html
<!-- Control how color swatches are rendered -->
<flicksell-template-cart 
    product-id="123" 
    color-source-style="compact">
    ...
</flicksell-template-cart>
```

#### Available Display Modes:

| Mode             | Description                                                                                             |
| ---------------- | ------------------------------------------------------------------------------------------------------- |
| `full` (default) | Shows the visual swatch/image alongside the full color name (e.g., "Midnight Blue").                     |
| `compact`        | Shows the visual swatch and a summarized name (e.g., "Midnight Blue +2 more").                           |
| `text-only`      | Shows only the color names, without the visual swatch.                                                  |
| `text-compact`   | A more condensed text-only version, which might show a count (e.g., "3 colors").                        |
| `visual-only`    | Renders only the visual swatch, with no text. This is great for creating clean, circular color pickers. |

#### Override Dynamic Source Settings

You can override specific visual settings for dynamic sources using override attributes:

```html
<!-- Override color display settings -->
<flicksell-template-cart 
    product-id="123" 
    color-source-style="visual-only"
    override-color-source-radius="20"
    override-color-source-shadow="strong"
    override-color-source-border_style="dark"
    override-color-source-rotation="45">
    ...
</flicksell-template-cart>
```

#### Available Override Settings:

| Attribute                                    | Description                                                    | Values                                    |
| -------------------------------------------- | -------------------------------------------------------------- | ----------------------------------------- |
| `override-color-source-radius`               | Border radius for color boxes                                 | Number (pixels)                          |
| `override-color-source-shadow`               | Shadow intensity                                               | `none`, `light`, `medium`, `strong`       |
| `override-color-source-border_style`         | Border style                                                   | `none`, `light`, `medium`, `dark`         |
| `override-color-source-rotation`             | Rotation angle for multi-color stripes                        | Number (degrees)                          |
| `override-color-source-use_grid_layout`      | Use grid layout for 4 colors                                  | `true`, `false`                           |
| `override-color-source-rotation_2_colors`    | Specific rotation for 2-color combinations                     | Number (degrees)                          |
| `override-color-source-rotation_3_colors`    | Specific rotation for 3-color combinations                     | Number (degrees)                          |
| `override-color-source-rotation_4_colors`    | Specific rotation for 4-color combinations                     | Number (degrees)                          |
| `override-color-source-rotation_5_colors`    | Specific rotation for 5+ color combinations                    | Number (degrees)                          |

---

## 📚 Chapter 3: API & Events

### Required Server Endpoints

For the template cart to function, your server must expose these endpoints:

1.  **`/flicksell-template-cart-data?product_id={id}`**: (GET) Returns a JSON object with all product and variant data.
2.  **`/flicksell-template-cart-data`**: (POST) Batch endpoint for multiple products. Expects `{ product_ids: [...] }` in request body.
3.  **`/flicksell-product-cart-status?product_id={id}`**: (GET) Returns a JSON object indicating which variants of this product are in the current user's cart and their quantities.
4.  **`/flicksell-add-to-cart`**: (POST) Adds an item to the cart. Expects `product_id`, `combination`, and `quantity`.
5.  **`/flicksell-update-cart`**: (POST) Updates an item's quantity in the cart. Expects `product_id`, `combination`, and `quantity`.

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

### Performance Optimizations

The template cart system includes several performance optimizations:

#### Batch Data Fetching

When multiple template cart elements are present on the same page, the system automatically batches their data requests to reduce server load:

```html
<!-- These will be fetched in a single batch request -->
<flicksell-template-cart product-id="123"></flicksell-template-cart>
<flicksell-template-cart product-id="456"></flicksell-template-cart>
<flicksell-template-cart product-id="789"></flicksell-template-cart>
```

#### Intelligent Polling

When multiple elements use polling, the system coordinates their updates to minimize server requests:

```html
<!-- These will poll together, not separately -->
<flicksell-template-cart product-id="123" poll="10"></flicksell-template-cart>
<flicksell-template-cart product-id="456" poll="10"></flicksell-template-cart>
```

#### Change Detection

The system only re-renders when data actually changes, preventing unnecessary DOM updates during polling.

---

## 🎨 Chapter 4: Dynamic Source Templates

For advanced customization of dynamic source content (like colors), you can provide custom templates:

```html
<flicksell-template-cart product-id="123">
    
    <!-- Your variant groups as usual -->
    <flicksell-variant-groups>
        <flicksell-variant-group>
            <flicksell-variant-pills>
                <flicksell-template-variant-pill></flicksell-template-variant-pill>
            </flicksell-variant-pills>
        </flicksell-variant-group>
    </flicksell-variant-groups>
    
    <!-- Custom templates for dynamic sources -->
    <flicksell-dynamic-source-templates>
        <!-- Template for color variants -->
        <flicksell-dynamic-source-template source="color">
            <div class="custom-color-pill">
                <flicksell-variant-color-box class="color-swatch"></flicksell-variant-color-box>
                <flicksell-variant-name class="color-name"></flicksell-variant-name>
            </div>
        </flicksell-dynamic-source-template>
        
        <!-- Default template for other dynamic sources -->
        <flicksell-dynamic-source-template source="default">
            <span class="variant-name"></span>
        </flicksell-dynamic-source-template>
    </flicksell-dynamic-source-templates>
    
</flicksell-template-cart>
```

This allows you to create completely custom layouts for how dynamic source content is displayed within variant pills.

---

## 🔧 Chapter 5: Complete Attribute Reference

### Main Element Attributes

| Attribute                          | Type     | Description                                                                                          |
| ---------------------------------- | -------- | ---------------------------------------------------------------------------------------------------- |
| `product-id`                       | String   | **Required.** The ID of the product to load                                                         |
| `poll`                             | Number   | Polling interval in seconds (minimum 2)                                                             |
| `mode`                             | String   | `normal` (default) or `move-to-cart` for specialized behavior                                        |
| `linked-with`                      | String   | Comma-separated list of element IDs to link with this cart                                          |
| `fetch-only`                       | String   | Comma-separated list of variant group names to display                                              |
| `no-auto-select`                   | Boolean  | Disable automatic selection of first options                                                        |
| `color-source-style`               | String   | Display style for color variants: `full`, `compact`, `text-only`, `text-compact`, `visual-only`    |
| `on-variant-change`                | String   | Global function name to call when variant selection changes                                         |
| `on-cart-action`                   | String   | Global function name to call after cart actions (for move-to-cart mode)                            |
| `combination-image-callback`       | String   | Global function name to call when combination image should update                                   |
| `combination-not-selected-callback`| String   | Global function name to call when user tries to add to cart without valid selection                |
| `override-color-source-*`          | Various  | Override specific visual settings for color display (see section 2.8)                             |

### Child Elements

| Element                                        | Purpose                                                                                      |
| ---------------------------------------------- | -------------------------------------------------------------------------------------------- |
| `<flicksell-skeleton>`                         | Loading state content                                                                        |
| `<flicksell-variant-groups>`                   | Container for all variant groups                                                             |
| `<flicksell-variant-group>`                    | Template for a single variant group                                                          |
| `<flicksell-variant-group-label>`              | Label for the variant group (auto-populated)                                                |
| `<flicksell-variant-pills>`                    | Container for variant options                                                                |
| `<flicksell-template-variant-pill>`            | Template for a single variant option                                                         |
| `<flicksell-template-add-to-cart>`             | Add to cart button container                                                                 |
| `<flicksell-template-update-cart>`             | Update cart controls container                                                               |
| `<flicksell-template-quantity-input>`          | Quantity input field                                                                         |
| `<flicksell-template-quantity-increment>`      | Increase quantity button                                                                     |
| `<flicksell-template-quantity-decrement>`      | Decrease quantity button                                                                     |
| `<flicksell-template-update-button>`           | Manual update button (disables auto-update)                                                 |
| `<flicksell-template-product-price>`           | Current price display                                                                        |
| `<flicksell-template-product-mrp>`             | Original price display                                                                       |
| `<flicksell-dynamic-source-templates>`         | Container for custom dynamic source templates                                                |
| `<flicksell-dynamic-source-template>`          | Custom template for dynamic source content                                                   |

This comprehensive guide should help you leverage all the powerful features of the FlickSell Template Cart system!
