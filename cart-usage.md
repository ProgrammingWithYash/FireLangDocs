# FlickSell Cart System Documentation

## Overview

FlickSell provides two comprehensive cart systems:

1. **Classic Cart System** (`<flicksell-cart>`) - Requires server-side variant data preparation
2. **Template Cart System** (`<flicksell-template-cart>`) - Auto-fetches data with just a product ID

Both systems support guest carts, real-time updates, polling, and complete customization.

---

## Template Cart System (Recommended)

### Basic Usage

```html
<flicksell-template-cart product-id="123">
    <!-- Skeleton loader -->
    <flicksell-skeleton>
        <div class="skeleton-box" style="height: 200px; border-radius: 8px;"></div>
    </flicksell-skeleton>

    <!-- Variant selection -->
    <flicksell-variant-groups>
        <flicksell-variant-group>
            <flicksell-variant-group-label></flicksell-variant-group-label>
            <flicksell-variant-pills>
                <flicksell-template-variant-pill class="variant-pill"></flicksell-template-variant-pill>
            </flicksell-variant-pills>
        </flicksell-variant-group>
    </flicksell-variant-groups>

    <!-- Pricing -->
    <div class="price-section">
        <flicksell-template-product-price class="current-price"></flicksell-template-product-price>
        <flicksell-template-product-mrp class="original-price"></flicksell-template-product-mrp>
    </div>

    <!-- Cart actions -->
    <flicksell-template-add-to-cart>
        <button class="btn btn-primary">
            <flicksell-template-add-to-cart-normal-content>Add to Cart</flicksell-template-add-to-cart-normal-content>
            <flicksell-template-add-to-cart-loading-content>Adding...</flicksell-template-add-to-cart-loading-content>
        </button>
    </flicksell-template-add-to-cart>

    <flicksell-template-update-cart>
        <div class="quantity-controls">
            <flicksell-template-quantity-decrement>
                <button>-</button>
            </flicksell-template-quantity-decrement>
            <flicksell-template-quantity-input>
                <input type="number" min="0" value="1">
            </flicksell-template-quantity-input>
            <flicksell-template-quantity-increment>
                <button>+</button>
            </flicksell-template-quantity-increment>
        </div>
        <flicksell-template-update-cart-loading-content>Updating...</flicksell-template-update-cart-loading-content>
    </flicksell-template-update-cart>
</flicksell-template-cart>
```

### Advanced Features

#### 1. Real-time Polling
```html
<flicksell-template-cart product-id="123" poll="5">
    <!-- Updates every 5 seconds -->
</flicksell-template-cart>
```

#### 2. Move-to-Cart Mode (for Wishlists)
```html
<flicksell-template-cart 
    product-id="123" 
    mode="move-to-cart"
    on-cart-action="handleWishlistAction">
    <!-- Cart actions will call handleWishlistAction after completion -->
</flicksell-template-cart>

<script>
function handleWishlistAction(action, productId, combination, quantity) {
    console.log('Cart action:', action, productId, combination, quantity);
    // Remove from wishlist, show notification, etc.
}
</script>
```

#### 3. Variant Change Callbacks
```html
<flicksell-template-cart 
    product-id="123"
    on-variant-change="handleVariantChange">
</flicksell-template-cart>

<script>
function handleVariantChange(combination, variantData) {
    console.log('Variant changed:', combination, variantData);
    // Update product images, descriptions, etc.
}
</script>
```

#### 4. Dynamic Color Templates
```html
<flicksell-template-cart product-id="123">
    <!-- Dynamic source templates for rich color display -->
    <flicksell-dynamic-source-templates>
        <flicksell-dynamic-source-template source="color">
            <div class="color-option">
                <div class="color-swatch" style="background-color: var(--color-hex);"></div>
                <span class="variant-name"></span>
            </div>
        </flicksell-dynamic-source-template>
        
        <flicksell-dynamic-source-template source="default">
            <span class="variant-name"></span>
        </flicksell-dynamic-source-template>
    </flicksell-dynamic-source-templates>
    
    <!-- Rest of template... -->
</flicksell-template-cart>
```

#### 5. Manual Update Mode
```html
<flicksell-template-cart product-id="123">
    <flicksell-template-update-cart>
        <flicksell-template-quantity-input>
            <input type="number" min="0" value="1">
        </flicksell-template-quantity-input>
        <!-- When this button exists, quantity changes won't auto-update -->
        <flicksell-template-update-button>
            <button>Update Cart</button>
        </flicksell-template-update-button>
    </flicksell-template-update-cart>
</flicksell-template-cart>
```

### CSS Styling

```css
/* Variant pills */
flicksell-template-variant-pill {
    padding: 8px 16px;
    border: 2px solid #ddd;
    border-radius: 6px;
    margin: 4px;
    transition: all 0.2s;
}

flicksell-template-variant-pill[selected] {
    border-color: #007bff;
    background-color: #007bff;
    color: white;
}

flicksell-template-variant-pill[disabled] {
    opacity: 0.5;
    cursor: not-allowed;
}

/* Hide elements with hidden attribute */
flicksell-template-add-to-cart[hidden],
flicksell-template-update-cart[hidden] {
    display: none !important;
}

/* Pricing */
.current-price {
    font-size: 1.5rem;
    font-weight: 600;
    color: #28a745;
}

.original-price {
    text-decoration: line-through;
    color: #6c757d;
    margin-left: 0.5rem;
}
```

---

## Classic Cart System

### Basic Usage

```html
<flicksell-cart 
    product-id="123"
    variants-data='<?= json_encode($product_variants) ?>'
    currency-symbol="₹">
    
    <!-- Variant pills -->
    <flicksell-variant-pill variant="Size:Small" data-variant-group="Size">Small</flicksell-variant-pill>
    <flicksell-variant-pill variant="Size:Medium" data-variant-group="Size">Medium</flicksell-variant-pill>
    <flicksell-variant-pill variant="Color:Red" data-variant-group="Color">Red</flicksell-variant-pill>
    <flicksell-variant-pill variant="Color:Blue" data-variant-group="Color">Blue</flicksell-variant-pill>

    <!-- Pricing -->
    <flicksell-product-variant-price></flicksell-product-variant-price>
    <flicksell-product-variant-mrp></flicksell-product-variant-mrp>

    <!-- Cart actions -->
    <flicksell-add-to-cart>
        <button>
            <flicksell-add-to-cart-normal-content>Add to Cart</flicksell-add-to-cart-normal-content>
            <flicksell-add-to-cart-loading-content>Adding...</flicksell-add-to-cart-loading-content>
        </button>
    </flicksell-add-to-cart>

    <flicksell-update-cart>
        <flicksell-quantity-decrement><button>-</button></flicksell-quantity-decrement>
        <flicksell-quantity-input><input type="number" min="0" value="1"></flicksell-quantity-input>
        <flicksell-quantity-increment><button>+</button></flicksell-quantity-increment>
        <flicksell-update-cart-loading-content>Updating...</flicksell-update-cart-loading-content>
    </flicksell-update-cart>
</flicksell-cart>
```

---

## Cart View System

### Basic Cart Display

```html
<flicksell-cart-view poll="10">
    <!-- Skeleton loader -->
    <flicksell-skeleton>
        <div class="skeleton-box" style="height: 300px;"></div>
    </flicksell-skeleton>

    <!-- Cart item template -->
    <flicksell-cart-card class="cart-item">
        <flicksell-cart-card-image class="item-image"></flicksell-cart-card-image>
        
        <div class="item-details">
            <flicksell-cart-card-title class="item-title"></flicksell-cart-card-title>
            <flicksell-cart-card-variant class="item-variant"></flicksell-cart-card-variant>
            <flicksell-cart-card-price class="item-price"></flicksell-cart-card-price>
        </div>

        <div class="item-controls">
            <flicksell-cart-card-controls>
                <flicksell-cart-card-quantity-decrement><button>-</button></flicksell-cart-card-quantity-decrement>
                <flicksell-cart-card-quantity-input><input type="number" min="0"></flicksell-cart-card-quantity-input>
                <flicksell-cart-card-quantity-increment><button>+</button></flicksell-cart-card-quantity-increment>
            </flicksell-cart-card-controls>
            
            <flicksell-cart-card-remove><button>Remove</button></flicksell-cart-card-remove>
            <flicksell-cart-card-loading-content>Loading...</flicksell-cart-card-loading-content>
        </div>

        <flicksell-cart-card-total class="item-total"></flicksell-cart-card-total>
    </flicksell-cart-card>

    <!-- Empty state -->
    <flicksell-cart-empty>
        <div class="empty-cart">
            <h3>Your cart is empty</h3>
            <p>Add some products to get started!</p>
        </div>
    </flicksell-cart-empty>

    <!-- Cart summary -->
    <flicksell-cart-summary class="cart-summary">
        <div class="summary-row">
            <span>Items (<flicksell-cart-summary-item-count></flicksell-cart-summary-item-count>):</span>
            <span><flicksell-cart-summary-subtotal></flicksell-cart-summary-subtotal></span>
        </div>
        <div class="summary-row">
            <span>Total:</span>
            <span><flicksell-cart-summary-total></flicksell-cart-summary-total></span>
        </div>
    </flicksell-cart-summary>
</flicksell-cart-view>
```

---

## Authentication System

### User State Management

```html
<flicksell-auth poll="30">
    <!-- Loading state -->
    <flicksell-skeleton>
        <div class="skeleton-box" style="height: 40px; width: 120px;"></div>
    </flicksell-skeleton>

    <!-- Logged in state -->
    <flicksell-signed-in>
        <div class="user-menu">
            <span>Welcome back!</span>
            <a href="/account">My Account</a>
            <a href="/logout">Logout</a>
        </div>
    </flicksell-signed-in>

    <!-- Logged out state -->
    <flicksell-signed-out>
        <div class="auth-buttons">
            <a href="/login" class="btn btn-outline">Login</a>
            <a href="/register" class="btn btn-primary">Sign Up</a>
        </div>
    </flicksell-signed-out>
</flicksell-auth>
```

---

## Checkout Modal

### Floating Checkout

```html
<!-- Trigger button -->
<button onclick="document.querySelector('flicksell-checkout').setAttribute('open', 'true')">
    Checkout
</button>

<!-- Modal (can be placed anywhere) -->
<flicksell-checkout>
    <!-- Modal opens automatically when open="true" -->
</flicksell-checkout>

<!-- Or use JavaScript -->
<script>
// Show checkout
flicksellShowFloatingCheckout();

// Hide checkout  
flicksellHideFloatingCheckout();
</script>
```

---

## Complete Example: Product Page

```html
<!DOCTYPE html>
<html>
<head>
    <title>Product Page</title>
    <style>
        .product-container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
        }
        
        .variant-section {
            margin: 20px 0;
        }
        
        .variant-group {
            margin-bottom: 15px;
        }
        
        .variant-group label {
            display: block;
            font-weight: 600;
            margin-bottom: 8px;
        }
        
        .variant-pills {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
        }
        
        .variant-pill {
            padding: 8px 16px;
            border: 2px solid #ddd;
            border-radius: 6px;
            background: white;
            cursor: pointer;
            transition: all 0.2s;
        }
        
        .variant-pill[selected] {
            border-color: #007bff;
            background-color: #007bff;
            color: white;
        }
        
        .price-section {
            margin: 20px 0;
            font-size: 1.2rem;
        }
        
        .current-price {
            font-size: 1.5rem;
            font-weight: 600;
            color: #28a745;
        }
        
        .original-price {
            text-decoration: line-through;
            color: #6c757d;
            margin-left: 0.5rem;
        }
        
        .cart-section {
            margin: 20px 0;
        }
        
        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 1rem;
            transition: all 0.2s;
        }
        
        .btn-primary {
            background-color: #007bff;
            color: white;
        }
        
        .btn-primary:hover {
            background-color: #0056b3;
        }
        
        .quantity-controls {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-top: 10px;
        }
        
        .quantity-controls button {
            width: 40px;
            height: 40px;
            border: 1px solid #ddd;
            background: white;
            cursor: pointer;
        }
        
        .quantity-controls input {
            width: 60px;
            height: 40px;
            text-align: center;
            border: 1px solid #ddd;
        }
    </style>
</head>
<body>
    <div class="product-container">
        <h1>Premium T-Shirt</h1>
        
        <!-- Template Cart with all features -->
        <flicksell-template-cart 
            product-id="123" 
            poll="10"
            on-variant-change="handleVariantChange">
            
            <!-- Loading skeleton -->
            <flicksell-skeleton>
                <div class="skeleton-box" style="height: 200px; border-radius: 8px;"></div>
            </flicksell-skeleton>

            <!-- Variant selection -->
            <div class="variant-section">
                <flicksell-variant-groups>
                    <flicksell-variant-group class="variant-group">
                        <flicksell-variant-group-label></flicksell-variant-group-label>
                        <flicksell-variant-pills class="variant-pills">
                            <flicksell-template-variant-pill class="variant-pill"></flicksell-template-variant-pill>
                        </flicksell-variant-pills>
                    </flicksell-variant-group>
                </flicksell-variant-groups>
            </div>

            <!-- Dynamic color templates -->
            <flicksell-dynamic-source-templates>
                <flicksell-dynamic-source-template source="color">
                    <div style="display: flex; align-items: center; gap: 8px;">
                        <div style="width: 20px; height: 20px; border-radius: 50%; background-color: var(--color-hex); border: 1px solid #ddd;"></div>
                        <span class="variant-name"></span>
                    </div>
                </flicksell-dynamic-source-template>
            </flicksell-dynamic-source-templates>

            <!-- Pricing -->
            <div class="price-section">
                <flicksell-template-product-price class="current-price"></flicksell-template-product-price>
                <flicksell-template-product-mrp class="original-price"></flicksell-template-product-mrp>
            </div>

            <!-- Cart actions -->
            <div class="cart-section">
                <flicksell-template-add-to-cart>
                    <button class="btn btn-primary">
                        <flicksell-template-add-to-cart-normal-content>Add to Cart</flicksell-template-add-to-cart-normal-content>
                        <flicksell-template-add-to-cart-loading-content>Adding...</flicksell-template-add-to-cart-loading-content>
                    </button>
                </flicksell-template-add-to-cart>

                <flicksell-template-update-cart>
                    <div class="quantity-controls">
                        <flicksell-template-quantity-decrement>
                            <button>-</button>
                        </flicksell-template-quantity-decrement>
                        <flicksell-template-quantity-input>
                            <input type="number" min="0" value="1">
                        </flicksell-template-quantity-input>
                        <flicksell-template-quantity-increment>
                            <button>+</button>
                        </flicksell-template-quantity-increment>
                    </div>
                    <flicksell-template-update-cart-loading-content>
                        <div style="margin-top: 10px;">Updating cart...</div>
                    </flicksell-template-update-cart-loading-content>
                </flicksell-template-update-cart>
            </div>
        </flicksell-template-cart>
    </div>

    <script>
        function handleVariantChange(combination, variantData) {
            console.log('Variant changed:', combination, variantData);
            
            // Update product images based on variant
            if (variantData && variantData.images) {
                // Update main product image
                updateProductImages(variantData.images);
            }
        }
        
        function updateProductImages(images) {
            // Your image update logic here
            console.log('Updating images:', images);
        }
    </script>
</body>
</html>
```

---

## API Endpoints

### Required Server Endpoints

1. **`/flicksell-template-cart-data`** - Product data for template cart
2. **`/flicksell-product-cart-status`** - Cart status for product
3. **`/flicksell-add-to-cart`** - Add item to cart
4. **`/flicksell-update-cart`** - Update cart quantity
5. **`/flicksell-signed-in`** - Check authentication status
6. **`/flicksell_get_cart.php`** - Get full cart data
7. **`/flicksell_sync_guest_cart.php`** - Sync guest cart after login

### Guest Cart Support

Both systems automatically handle guest carts using localStorage. When users log in, carts are automatically synced.

---

## Events

### Cart Events
- `flicksell:cartUpdated` - Fired when cart changes
- Custom variant change callbacks
- Custom cart action callbacks

### Usage
```javascript
document.addEventListener('flicksell:cartUpdated', function(event) {
    console.log('Cart was updated!');
    // Update cart counters, refresh displays, etc.
});
```

---

## Best Practices

1. **Use Template Cart** for new implementations - it's more flexible
2. **Always include skeleton loaders** for better UX
3. **Style with CSS attributes** (`[selected]`, `[disabled]`, `[hidden]`)
4. **Use polling sparingly** - only when real-time updates are critical
5. **Test guest cart functionality** thoroughly
6. **Implement proper error handling** in callbacks
7. **Use semantic HTML** inside FlickSell elements

---

## Browser Support

- Modern browsers with Web Components support
- IE11+ with polyfills
- Mobile browsers (iOS Safari, Chrome Mobile)

---

## Migration Guide

### From Classic to Template Cart

```html
<!-- Old Classic Cart -->
<flicksell-cart product-id="123" variants-data='<?= json_encode($data) ?>'>
    <flicksell-variant-pill variant="Size:Small">Small</flicksell-variant-pill>
</flicksell-cart>

<!-- New Template Cart -->
<flicksell-template-cart product-id="123">
    <flicksell-variant-groups>
        <flicksell-variant-group>
            <flicksell-variant-pills>
                <flicksell-template-variant-pill></flicksell-template-variant-pill>
            </flicksell-variant-pills>
        </flicksell-variant-group>
    </flicksell-variant-groups>
</flicksell-template-cart>
```

The template cart automatically generates variant pills from server data, eliminating the need for manual PHP data preparation.
