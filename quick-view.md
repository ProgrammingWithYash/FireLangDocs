# The Ultimate Guide to FlickSell's Product Quick View

Welcome, developer! This guide is your complete resource for mastering the `<flicksell-product-quick-view>` component. This powerful element allows you to create dynamic product displays that can instantly switch between different products without page reloads. It's perfect for product galleries, quick view modals, related products, and any scenario where you need to show product information dynamically.

---

## 🚀 Chapter 1: Your First Quick View

Let's start by building a functional product quick view in minutes.

### 1.1: The Basic Structure

The core concept is simple: you provide a product ID, and the component fetches and displays all the product information using your HTML templates.

Here's the essential structure. Copy and paste this to get started:

```html
<!-- The main wrapper for a single product's quick view -->
<flicksell-product-quick-view product-id="123">

    <!-- Part 1: Skeleton Loader (Optional, but recommended) -->
    <!-- This is shown automatically while product data is loading -->
    <flicksell-skeleton>
        <div style="height: 200px; background: #eee; border-radius: 8px; margin-bottom: 1rem;"></div>
        <div style="height: 24px; background: #eee; border-radius: 4px; margin-bottom: 0.5rem;"></div>
        <div style="height: 16px; width: 70%; background: #eee; border-radius: 4px;"></div>
    </flicksell-skeleton>

    <!-- Part 2: Product Images -->
    <!-- Container for all product images -->
    <flicksell-product-quick-view-images>
        <!-- Template for a single image - this will be duplicated for each product image -->
        <flicksell-product-quick-view-image class="product-image">
            <!-- The actual <img> tag will be auto-generated and inserted here -->
        </flicksell-product-quick-view-image>
    </flicksell-product-quick-view-images>

    <!-- Part 3: Product Information -->
    <div class="product-info">
        <!-- Product title - automatically populated -->
        <flicksell-product-quick-view-title class="product-title">
            <!-- Product name will be inserted here -->
        </flicksell-product-quick-view-title>

        <!-- Product description - automatically populated -->
        <flicksell-product-quick-view-description class="product-description">
            <!-- Product description HTML will be inserted here -->
        </flicksell-product-quick-view-description>
    </div>

    <!-- Part 4: Integrated Cart (Optional) -->
    <!-- You can embed a template cart that automatically inherits the product ID -->
    <flicksell-template-cart>
        <flicksell-variant-groups>
            <flicksell-variant-group>
                <flicksell-variant-group-label></flicksell-variant-group-label>
                <flicksell-variant-pills>
                    <flicksell-template-variant-pill class="variant-pill"></flicksell-template-variant-pill>
                </flicksell-variant-pills>
            </flicksell-variant-group>
        </flicksell-variant-groups>

        <flicksell-template-add-to-cart>
            <button class="btn-add-to-cart">Add to Cart</button>
        </flicksell-template-add-to-cart>

        <flicksell-template-update-cart>
            <div class="quantity-controls">
                <flicksell-template-quantity-decrement><button>-</button></flicksell-template-quantity-decrement>
                <flicksell-template-quantity-input><input type="number" min="0" value="1"></flicksell-template-quantity-input>
                <flicksell-template-quantity-increment><button>+</button></flicksell-template-quantity-increment>
            </div>
        </flicksell-template-update-cart>
    </flicksell-template-cart>

</flicksell-product-quick-view>
```

**How It Works:**

1. `<flicksell-product-quick-view>` fetches all data for product `123`
2. While loading, it displays the skeleton content
3. Once loaded, it populates your templates with real product data
4. Any nested `<flicksell-template-cart>` automatically inherits the product ID
5. When the product ID changes, everything updates dynamically

### 1.2: Styling Your Quick View

You have complete control over the appearance using CSS. Here are the key selectors:

#### Key CSS Selectors:

| Selector                                    | Description                                                           |
| ------------------------------------------- | --------------------------------------------------------------------- |
| `flicksell-product-quick-view`              | The main container                                                    |
| `flicksell-product-quick-view-images`       | Container for all product images                                      |
| `flicksell-product-quick-view-image`        | Individual image containers                                           |
| `flicksell-product-quick-view-image img`    | The actual image elements (auto-generated)                           |
| `flicksell-product-quick-view-title`        | Product title container                                               |
| `flicksell-product-quick-view-description`  | Product description container                                         |
| `flicksell-skeleton[hidden]`                | Hidden skeleton (use `[hidden] { display: none !important; }`)       |

#### Example CSS:

```css
/* Modern product quick view layout */
flicksell-product-quick-view {
    display: block;
    max-width: 800px;
    margin: 0 auto;
    padding: 2rem;
    background: #ffffff;
    border-radius: 12px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
}

/* Image gallery grid */
flicksell-product-quick-view-images {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 1rem;
    margin-bottom: 2rem;
}

flicksell-product-quick-view-image {
    aspect-ratio: 1;
    overflow: hidden;
    border-radius: 8px;
    background: #f8f9fa;
}

flicksell-product-quick-view-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.3s ease;
}

flicksell-product-quick-view-image:hover img {
    transform: scale(1.05);
}

/* Product information */
flicksell-product-quick-view-title {
    display: block;
    font-size: 1.5rem;
    font-weight: 600;
    color: #1f2937;
    margin-bottom: 1rem;
}

flicksell-product-quick-view-description {
    display: block;
    color: #6b7280;
    line-height: 1.6;
    margin-bottom: 2rem;
}

/* Skeleton loading state */
flicksell-skeleton {
    animate: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}

@keyframes pulse {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.5; }
}

/* Hide elements when not needed */
[hidden] {
    display: none !important;
}
```

---

## ⚙️ Chapter 2: Advanced Features

### 2.1: Dynamic Product Switching

The real power of the quick view comes from its ability to dynamically switch between products. Simply change the `product-id` attribute and everything updates automatically.

```html
<flicksell-product-quick-view id="main-quick-view" product-id="123">
    <!-- Your template content -->
</flicksell-product-quick-view>

<!-- Product switcher buttons -->
<div class="product-switcher">
    <button onclick="switchProduct('123')">Product 1</button>
    <button onclick="switchProduct('456')">Product 2</button>
    <button onclick="switchProduct('789')">Product 3</button>
</div>

<script>
function switchProduct(productId) {
    const quickView = document.getElementById('main-quick-view');
    quickView.setAttribute('product-id', productId);
    // Everything updates automatically!
}
</script>
```

### 2.2: Callbacks for Product Changes

Execute custom JavaScript when products change using callback functions:

```html
<flicksell-product-quick-view 
    product-id="123"
    on-id-change="handleProductChange"
    on-loaded="handleProductLoaded">
    
    <!-- Your template content -->
</flicksell-product-quick-view>

<script>
// Called BEFORE the product changes - must return true to proceed
function handleProductChange(oldProductId, newProductId) {
    console.log(`Switching from product ${oldProductId} to ${newProductId}`);
    
    // You can prevent the change by returning false
    if (newProductId === '999') {
        alert('This product is not available');
        return false; // Prevents the change
    }
    
    // Show loading state
    showLoadingIndicator();
    
    return true; // Allow the change
}

// Called AFTER the product has loaded successfully
function handleProductLoaded(productId, productData) {
    console.log(`Product ${productId} loaded:`, productData);
    
    // Hide loading state
    hideLoadingIndicator();
    
    // Update page title
    document.title = productData.name + ' - My Store';
    
    // Update URL without page reload
    history.pushState({}, '', `/product/${productId}`);
    
    // Track analytics
    gtag('event', 'product_view', {
        product_id: productId,
        product_name: productData.name
    });
}
</script>
```

### 2.3: Creating a Product Gallery with Quick View

Perfect for category pages or product listings:

```html
<div class="product-gallery">
    <!-- Product thumbnails -->
    <div class="product-thumbnails">
        <div class="thumbnail" onclick="showProduct('123')">
            <img src="/thumbs/product-123.jpg" alt="Product 1">
            <h3>Product 1</h3>
        </div>
        <div class="thumbnail" onclick="showProduct('456')">
            <img src="/thumbs/product-456.jpg" alt="Product 2">
            <h3>Product 2</h3>
        </div>
        <div class="thumbnail" onclick="showProduct('789')">
            <img src="/thumbs/product-789.jpg" alt="Product 3">
            <h3>Product 3</h3>
        </div>
    </div>

    <!-- Quick view modal -->
    <div id="quick-view-modal" class="modal" style="display: none;">
        <div class="modal-content">
            <span class="close" onclick="closeQuickView()">&times;</span>
            
            <flicksell-product-quick-view 
                id="gallery-quick-view"
                on-loaded="handleQuickViewLoaded">
                
                <!-- Two-column layout -->
                <div class="quick-view-layout">
                    <div class="images-column">
                        <flicksell-product-quick-view-images>
                            <flicksell-product-quick-view-image>
                                <!-- Images auto-generated -->
                            </flicksell-product-quick-view-image>
                        </flicksell-product-quick-view-images>
                    </div>
                    
                    <div class="info-column">
                        <flicksell-product-quick-view-title></flicksell-product-quick-view-title>
                        <flicksell-product-quick-view-description></flicksell-product-quick-view-description>
                        
                        <!-- Integrated cart -->
                        <flicksell-template-cart>
                            <flicksell-variant-groups>
                                <flicksell-variant-group>
                                    <flicksell-variant-group-label></flicksell-variant-group-label>
                                    <flicksell-variant-pills>
                                        <flicksell-template-variant-pill></flicksell-template-variant-pill>
                                    </flicksell-variant-pills>
                                </flicksell-variant-group>
                            </flicksell-variant-groups>
                            
                            <flicksell-template-product-price></flicksell-template-product-price>
                            <flicksell-template-product-mrp></flicksell-template-product-mrp>
                            
                            <flicksell-template-add-to-cart>
                                <button class="btn-primary">Add to Cart</button>
                            </flicksell-template-add-to-cart>
                        </flicksell-template-cart>
                    </div>
                </div>
                
            </flicksell-product-quick-view>
        </div>
    </div>
</div>

<script>
function showProduct(productId) {
    const quickView = document.getElementById('gallery-quick-view');
    const modal = document.getElementById('quick-view-modal');
    
    // Set product ID and show modal
    quickView.setAttribute('product-id', productId);
    modal.style.display = 'block';
}

function closeQuickView() {
    document.getElementById('quick-view-modal').style.display = 'none';
}

function handleQuickViewLoaded(productId, productData) {
    // Optional: Update modal title
    document.querySelector('.modal-content h2').textContent = productData.name;
}

// Close modal when clicking outside
window.onclick = function(event) {
    const modal = document.getElementById('quick-view-modal');
    if (event.target === modal) {
        closeQuickView();
    }
}
</script>

<style>
.product-gallery {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem;
}

.product-thumbnails {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 1.5rem;
    margin-bottom: 2rem;
}

.thumbnail {
    cursor: pointer;
    border: 1px solid #e5e7eb;
    border-radius: 8px;
    padding: 1rem;
    transition: all 0.3s ease;
}

.thumbnail:hover {
    border-color: #6366f1;
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.thumbnail img {
    width: 100%;
    height: 150px;
    object-fit: cover;
    border-radius: 4px;
    margin-bottom: 0.5rem;
}

.modal {
    position: fixed;
    z-index: 1000;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    backdrop-filter: blur(5px);
}

.modal-content {
    background-color: #fefefe;
    margin: 2% auto;
    padding: 0;
    border-radius: 12px;
    width: 90%;
    max-width: 900px;
    max-height: 90vh;
    overflow-y: auto;
    position: relative;
}

.close {
    position: absolute;
    top: 1rem;
    right: 1.5rem;
    color: #aaa;
    font-size: 28px;
    font-weight: bold;
    cursor: pointer;
    z-index: 1001;
}

.close:hover {
    color: #000;
}

.quick-view-layout {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
    padding: 2rem;
}

.images-column flicksell-product-quick-view-images {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
    gap: 0.5rem;
}

.info-column {
    display: flex;
    flex-direction: column;
    gap: 1rem;
}

@media (max-width: 768px) {
    .quick-view-layout {
        grid-template-columns: 1fr;
    }
    
    .modal-content {
        width: 95%;
        margin: 5% auto;
    }
}
</style>
```

### 2.4: Related Products Carousel

Create a dynamic related products section:

```html
<div class="related-products">
    <h2>Related Products</h2>
    
    <!-- Product navigation -->
    <div class="product-nav">
        <button onclick="previousProduct()" id="prev-btn">← Previous</button>
        <span id="product-counter">1 of 5</span>
        <button onclick="nextProduct()" id="next-btn">Next →</button>
    </div>
    
    <!-- Main product display -->
    <flicksell-product-quick-view 
        id="related-product-view"
        product-id="123"
        on-loaded="updateProductCounter">
        
        <div class="related-product-card">
            <flicksell-product-quick-view-images>
                <flicksell-product-quick-view-image class="main-image">
                    <!-- Single main image -->
                </flicksell-product-quick-view-image>
            </flicksell-product-quick-view-images>
            
            <div class="product-details">
                <flicksell-product-quick-view-title></flicksell-product-quick-view-title>
                <flicksell-product-quick-view-description></flicksell-product-quick-view-description>
                
                <!-- Compact cart -->
                <flicksell-template-cart>
                    <flicksell-template-product-price class="price"></flicksell-template-product-price>
                    <flicksell-template-add-to-cart>
                        <button class="btn-sm">Quick Add</button>
                    </flicksell-template-add-to-cart>
                </flicksell-template-cart>
            </div>
        </div>
        
    </flicksell-product-quick-view>
</div>

<script>
const relatedProducts = ['123', '456', '789', '101', '202'];
let currentIndex = 0;

function previousProduct() {
    if (currentIndex > 0) {
        currentIndex--;
        showRelatedProduct();
    }
}

function nextProduct() {
    if (currentIndex < relatedProducts.length - 1) {
        currentIndex++;
        showRelatedProduct();
    }
}

function showRelatedProduct() {
    const quickView = document.getElementById('related-product-view');
    quickView.setAttribute('product-id', relatedProducts[currentIndex]);
    
    // Update button states
    document.getElementById('prev-btn').disabled = currentIndex === 0;
    document.getElementById('next-btn').disabled = currentIndex === relatedProducts.length - 1;
}

function updateProductCounter() {
    document.getElementById('product-counter').textContent = 
        `${currentIndex + 1} of ${relatedProducts.length}`;
}

// Initialize
showRelatedProduct();
</script>
```

### 2.5: Programmatic Control

You can also control the quick view programmatically:

```html
<flicksell-product-quick-view id="my-quick-view" product-id="123">
    <!-- Your template -->
</flicksell-product-quick-view>

<script>
// Get the quick view element
const quickView = document.getElementById('my-quick-view');

// Change product programmatically
quickView.setAttribute('product-id', '456');

// Or use the refresh method to reload current product
quickView.refresh();

// Get current product data
const productData = quickView.getProductData();
console.log('Current product:', productData);

// Listen for product changes
quickView.addEventListener('productLoaded', function(event) {
    console.log('Product loaded:', event.detail);
});
</script>
```

---

## 📚 Chapter 3: Integration with Template Cart

### 3.1: Automatic Cart Integration

When you nest a `<flicksell-template-cart>` inside a `<flicksell-product-quick-view>`, the cart automatically inherits the product ID:

```html
<flicksell-product-quick-view product-id="123">
    
    <flicksell-product-quick-view-title></flicksell-product-quick-view-title>
    
    <!-- This cart automatically gets product-id="123" -->
    <!-- When quick view changes to product 456, cart updates too -->
    <flicksell-template-cart>
        <flicksell-variant-groups>
            <flicksell-variant-group>
                <flicksell-variant-group-label></flicksell-variant-group-label>
                <flicksell-variant-pills>
                    <flicksell-template-variant-pill></flicksell-template-variant-pill>
                </flicksell-variant-pills>
            </flicksell-variant-group>
        </flicksell-variant-groups>
        
        <flicksell-template-add-to-cart>
            <button>Add to Cart</button>
        </flicksell-template-add-to-cart>
    </flicksell-template-cart>
    
</flicksell-product-quick-view>
```

### 3.2: Multiple Cart Configurations

You can have different cart configurations for different scenarios:

```html
<flicksell-product-quick-view product-id="123">
    
    <!-- Product info -->
    <flicksell-product-quick-view-title></flicksell-product-quick-view-title>
    <flicksell-product-quick-view-description></flicksell-product-quick-view-description>
    
    <!-- Full cart with all features -->
    <flicksell-template-cart>
        <flicksell-variant-groups>
            <flicksell-variant-group>
                <flicksell-variant-group-label></flicksell-variant-group-label>
                <flicksell-variant-pills>
                    <flicksell-template-variant-pill></flicksell-template-variant-pill>
                </flicksell-variant-pills>
            </flicksell-variant-group>
        </flicksell-variant-groups>
        
        <div class="pricing">
            <flicksell-template-product-price></flicksell-template-product-price>
            <flicksell-template-product-mrp></flicksell-template-product-mrp>
        </div>
        
        <flicksell-template-add-to-cart>
            <button class="btn-primary">Add to Cart</button>
        </flicksell-template-add-to-cart>
        
        <flicksell-template-update-cart>
            <div class="quantity-controls">
                <flicksell-template-quantity-decrement><button>-</button></flicksell-template-quantity-decrement>
                <flicksell-template-quantity-input><input type="number" min="0"></flicksell-template-quantity-input>
                <flicksell-template-quantity-increment><button>+</button></flicksell-template-quantity-increment>
            </div>
        </flicksell-template-update-cart>
    </flicksell-template-cart>
    
    <!-- Minimal cart for quick actions -->
    <flicksell-template-cart class="quick-cart">
        <flicksell-template-add-to-cart>
            <button class="btn-sm">Quick Buy</button>
        </flicksell-template-add-to-cart>
    </flicksell-template-cart>
    
</flicksell-product-quick-view>
```

### 3.3: Cart Callbacks in Quick View Context

Combine quick view and cart callbacks for powerful interactions:

```html
<flicksell-product-quick-view 
    product-id="123"
    on-loaded="handleProductLoaded">
    
    <flicksell-product-quick-view-title></flicksell-product-quick-view-title>
    
    <flicksell-template-cart 
        on-variant-change="handleVariantChange"
        combination-image-callback="updateQuickViewImage">
        
        <flicksell-variant-groups>
            <flicksell-variant-group>
                <flicksell-variant-group-label></flicksell-variant-group-label>
                <flicksell-variant-pills>
                    <flicksell-template-variant-pill></flicksell-template-variant-pill>
                </flicksell-variant-pills>
            </flicksell-variant-group>
        </flicksell-variant-groups>
        
        <flicksell-template-add-to-cart>
            <button>Add to Cart</button>
        </flicksell-template-add-to-cart>
    </flicksell-template-cart>
    
</flicksell-product-quick-view>

<script>
function handleProductLoaded(productId, productData) {
    console.log('Product loaded in quick view:', productData.name);
    
    // Update page analytics
    trackProductView(productId, productData.name);
}

function handleVariantChange(combination, variantData) {
    console.log('Variant changed:', combination);
    
    // Update quick view specific elements
    updateStockStatus(variantData.stock);
    updateShippingInfo(variantData);
}

function updateQuickViewImage(imagePath) {
    // Update the main product image in quick view
    const mainImage = document.querySelector('.main-product-image');
    if (mainImage && imagePath) {
        mainImage.src = '/assets/images/uploaded/' + imagePath;
    }
}
</script>
```

---

## 🎨 Chapter 4: Advanced Styling & Layouts

### 4.1: Responsive Grid Layout

Create a responsive product display:

```html
<flicksell-product-quick-view product-id="123" class="responsive-quick-view">
    
    <div class="product-grid">
        <!-- Images column -->
        <div class="images-section">
            <flicksell-product-quick-view-images class="image-gallery">
                <flicksell-product-quick-view-image class="gallery-image">
                    <!-- Auto-generated images -->
                </flicksell-product-quick-view-image>
            </flicksell-product-quick-view-images>
        </div>
        
        <!-- Info column -->
        <div class="info-section">
            <flicksell-product-quick-view-title class="product-title"></flicksell-product-quick-view-title>
            <flicksell-product-quick-view-description class="product-description"></flicksell-product-quick-view-description>
            
            <!-- Cart section -->
            <div class="cart-section">
                <flicksell-template-cart>
                    <flicksell-variant-groups class="variant-selection">
                        <flicksell-variant-group class="variant-group">
                            <flicksell-variant-group-label class="variant-label"></flicksell-variant-group-label>
                            <flicksell-variant-pills class="variant-options">
                                <flicksell-template-variant-pill class="variant-pill"></flicksell-template-variant-pill>
                            </flicksell-variant-pills>
                        </flicksell-variant-group>
                    </flicksell-variant-groups>
                    
                    <div class="price-section">
                        <flicksell-template-product-price class="current-price"></flicksell-template-product-price>
                        <flicksell-template-product-mrp class="original-price"></flicksell-template-product-mrp>
                    </div>
                    
                    <flicksell-template-add-to-cart class="add-to-cart">
                        <button class="btn-primary">Add to Cart</button>
                    </flicksell-template-add-to-cart>
                </flicksell-template-cart>
            </div>
        </div>
    </div>
    
</flicksell-product-quick-view>

<style>
.responsive-quick-view {
    max-width: 1000px;
    margin: 0 auto;
    padding: 2rem;
}

.product-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 3rem;
    align-items: start;
}

.images-section {
    position: sticky;
    top: 2rem;
}

.image-gallery {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 1rem;
}

.gallery-image {
    aspect-ratio: 1;
    overflow: hidden;
    border-radius: 8px;
    background: #f8f9fa;
}

.gallery-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.3s ease;
}

.gallery-image:hover img {
    transform: scale(1.05);
}

.info-section {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
}

.product-title {
    font-size: 1.875rem;
    font-weight: 700;
    color: #1f2937;
    line-height: 1.2;
}

.product-description {
    color: #6b7280;
    line-height: 1.6;
}

.cart-section {
    background: #f9fafb;
    padding: 1.5rem;
    border-radius: 12px;
    border: 1px solid #e5e7eb;
}

.variant-selection {
    margin-bottom: 1.5rem;
}

.variant-group {
    margin-bottom: 1rem;
}

.variant-label {
    font-weight: 600;
    color: #374151;
    margin-bottom: 0.5rem;
    display: block;
}

.variant-options {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
}

.variant-pill {
    padding: 0.5rem 1rem;
    border: 1px solid #d1d5db;
    border-radius: 6px;
    background: white;
    cursor: pointer;
    transition: all 0.2s ease;
}

.variant-pill:hover {
    border-color: #6366f1;
}

.variant-pill[selected] {
    background: #6366f1;
    border-color: #6366f1;
    color: white;
}

.price-section {
    display: flex;
    align-items: center;
    gap: 1rem;
    margin-bottom: 1.5rem;
}

.current-price {
    font-size: 1.5rem;
    font-weight: 700;
    color: #059669;
}

.original-price {
    font-size: 1.125rem;
    color: #9ca3af;
    text-decoration: line-through;
}

.add-to-cart .btn-primary {
    width: 100%;
    padding: 0.75rem 1.5rem;
    background: #6366f1;
    color: white;
    border: none;
    border-radius: 8px;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.2s ease;
}

.add-to-cart .btn-primary:hover {
    background: #5856eb;
}

/* Responsive design */
@media (max-width: 768px) {
    .product-grid {
        grid-template-columns: 1fr;
        gap: 2rem;
    }
    
    .images-section {
        position: static;
    }
    
    .image-gallery {
        grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
    }
    
    .product-title {
        font-size: 1.5rem;
    }
    
    .responsive-quick-view {
        padding: 1rem;
    }
}
</style>
```

### 4.2: Card-Based Layout

Create a compact card layout for product grids:

```html
<div class="product-cards-container">
    <flicksell-product-quick-view product-id="123" class="product-card">
        <div class="card-image">
            <flicksell-product-quick-view-images>
                <flicksell-product-quick-view-image class="main-image">
                    <!-- First image only -->
                </flicksell-product-quick-view-image>
            </flicksell-product-quick-view-images>
        </div>
        
        <div class="card-content">
            <flicksell-product-quick-view-title class="card-title"></flicksell-product-quick-view-title>
            
            <flicksell-template-cart>
                <flicksell-template-product-price class="card-price"></flicksell-template-product-price>
                <flicksell-template-add-to-cart class="card-action">
                    <button class="btn-card">Add to Cart</button>
                </flicksell-template-add-to-cart>
            </flicksell-template-cart>
        </div>
    </flicksell-product-quick-view>
</div>

<style>
.product-cards-container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 1.5rem;
    padding: 2rem;
}

.product-card {
    background: white;
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.product-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

.card-image {
    position: relative;
    aspect-ratio: 1;
    overflow: hidden;
}

.main-image {
    width: 100%;
    height: 100%;
}

.main-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.card-content {
    padding: 1.5rem;
}

.card-title {
    font-size: 1.125rem;
    font-weight: 600;
    color: #1f2937;
    margin-bottom: 0.5rem;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
}

.card-price {
    font-size: 1.25rem;
    font-weight: 700;
    color: #059669;
    margin-bottom: 1rem;
}

.card-action .btn-card {
    width: 100%;
    padding: 0.75rem;
    background: #6366f1;
    color: white;
    border: none;
    border-radius: 8px;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.2s ease;
}

.card-action .btn-card:hover {
    background: #5856eb;
}
</style>
```

---

## 🔧 Chapter 5: API & Technical Details

### 5.1: Required Server Endpoints

The product quick view requires this server endpoint:

**`/flicksell-product-quick-view-data?product_id={id}`** (GET)

Returns a JSON object with product information:

```json
{
    "success": true,
    "product": {
        "id": 123,
        "name": "Amazing Product",
        "description": "<p>Full HTML description</p>",
        "short_description": "Brief description",
        "main_img": "main-image.jpg",
        "images": [
            "image1.jpg",
            "image2.jpg",
            "image3.jpg"
        ]
    }
}
```

### 5.2: JavaScript API

#### Methods:

| Method                    | Description                                           |
| ------------------------- | ----------------------------------------------------- |
| `refresh()`               | Manually refresh the current product data            |
| `getProductData()`        | Get the current product data object                  |

#### Events:

| Event           | Description                                           |
| --------------- | ----------------------------------------------------- |
| `productLoaded` | Fired when product data is successfully loaded       |
| `productError`  | Fired when product data fails to load                |

#### Example Usage:

```javascript
const quickView = document.getElementById('my-quick-view');

// Refresh current product
quickView.refresh();

// Get current data
const productData = quickView.getProductData();

// Listen for events
quickView.addEventListener('productLoaded', function(event) {
    console.log('Product loaded:', event.detail);
});

quickView.addEventListener('productError', function(event) {
    console.error('Product failed to load:', event.detail);
});
```

### 5.3: Performance Considerations

#### Image Loading Optimization:

```html
<flicksell-product-quick-view product-id="123">
    <flicksell-product-quick-view-images>
        <flicksell-product-quick-view-image class="lazy-image">
            <!-- Images are loaded dynamically -->
        </flicksell-product-quick-view-image>
    </flicksell-product-quick-view-images>
</flicksell-product-quick-view>

<style>
.lazy-image img {
    loading: lazy; /* Browser-native lazy loading */
    transition: opacity 0.3s ease;
}

.lazy-image img:not([src]) {
    opacity: 0;
}

.lazy-image img[src] {
    opacity: 1;
}
</style>
```

#### Caching Strategy:

The quick view automatically caches product data to avoid redundant requests when switching between the same products.

---

## 📋 Chapter 6: Complete Attribute Reference

### Main Element Attributes

| Attribute      | Type     | Description                                                                      |
| -------------- | -------- | -------------------------------------------------------------------------------- |
| `product-id`   | String   | **Required.** The ID of the product to display                                  |
| `on-id-change` | String   | Global function name called before product ID changes (must return true to proceed) |
| `on-loaded`    | String   | Global function name called after product data loads successfully               |

### Child Elements

| Element                                      | Purpose                                                    |
| -------------------------------------------- | ---------------------------------------------------------- |
| `<flicksell-skeleton>`                       | Loading state content                                      |
| `<flicksell-product-quick-view-images>`      | Container for all product images                           |
| `<flicksell-product-quick-view-image>`       | Template for individual product images                     |
| `<flicksell-product-quick-view-title>`       | Product title display                                      |
| `<flicksell-product-quick-view-description>` | Product description display                                |
| `<flicksell-template-cart>`                  | Nested cart (automatically inherits product ID)           |

### Callback Function Signatures

#### `on-id-change` Callback:
```javascript
function myIdChangeCallback(oldProductId, newProductId) {
    // Return true to allow the change, false to prevent it
    return true;
}
```

#### `on-loaded` Callback:
```javascript
function myLoadedCallback(productId, productData) {
    // Handle successful product load
    console.log('Loaded product:', productData);
}
```

---

## 🎯 Chapter 7: Best Practices & Tips

### 7.1: Performance Best Practices

1. **Use Skeleton Loading**: Always provide skeleton content for better UX
2. **Optimize Images**: Use appropriate image sizes and formats
3. **Minimize DOM Changes**: Let the component handle DOM updates
4. **Cache Callbacks**: Store callback functions to avoid recreation

### 7.2: Accessibility Guidelines

```html
<flicksell-product-quick-view product-id="123" role="main" aria-label="Product details">
    
    <flicksell-product-quick-view-images role="img" aria-label="Product images">
        <flicksell-product-quick-view-image>
            <!-- Images get proper alt attributes automatically -->
        </flicksell-product-quick-view-image>
    </flicksell-product-quick-view-images>
    
    <flicksell-product-quick-view-title role="heading" aria-level="1">
        <!-- Product title -->
    </flicksell-product-quick-view-title>
    
    <flicksell-product-quick-view-description role="article">
        <!-- Product description -->
    </flicksell-product-quick-view-description>
    
</flicksell-product-quick-view>
```

### 7.3: Error Handling

```javascript
// Robust error handling
function handleProductChange(oldId, newId) {
    try {
        // Validate product ID
        if (!newId || newId.trim() === '') {
            console.error('Invalid product ID');
            return false;
        }
        
        // Check if product exists (optional)
        if (!isValidProductId(newId)) {
            showErrorMessage('Product not found');
            return false;
        }
        
        return true;
    } catch (error) {
        console.error('Error in product change:', error);
        return false;
    }
}

function handleProductLoaded(productId, productData) {
    try {
        // Validate product data
        if (!productData || !productData.name) {
            console.error('Invalid product data received');
            return;
        }
        
        // Update UI safely
        updateProductMetadata(productData);
        
    } catch (error) {
        console.error('Error handling product load:', error);
    }
}
```

### 7.4: SEO Considerations

```html
<!-- Update page metadata when product changes -->
<script>
function handleProductLoaded(productId, productData) {
    // Update page title
    document.title = `${productData.name} - My Store`;
    
    // Update meta description
    const metaDesc = document.querySelector('meta[name="description"]');
    if (metaDesc) {
        metaDesc.setAttribute('content', productData.short_description);
    }
    
    // Update Open Graph tags
    const ogTitle = document.querySelector('meta[property="og:title"]');
    if (ogTitle) {
        ogTitle.setAttribute('content', productData.name);
    }
    
    const ogImage = document.querySelector('meta[property="og:image"]');
    if (ogImage && productData.main_img) {
        ogImage.setAttribute('content', `/assets/images/uploaded/${productData.main_img}`);
    }
    
    // Update structured data
    updateProductStructuredData(productData);
}
</script>
```

This comprehensive guide covers all aspects of the FlickSell Product Quick View system. The component provides a powerful foundation for creating dynamic, interactive product displays that enhance the user experience while maintaining clean, maintainable code. 
