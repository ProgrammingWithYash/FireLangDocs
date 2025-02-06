# 🔥 Fire Template Language Documentation

## 📚 Table of Contents
1. [Basic Syntax](#-basic-syntax)
2. [Variables](#-variables)
3. [Control Structures](#-control-structures)
4. [Comments](#-comments)
5. [Schema Variables](#-schema-variables)
6. [System API Reference](#-system-api-reference)
7. [Special Variables](#-special-variables)
8. [String Concatenation](#-string-concatenation)
9. [Best Practices](#-best-practices)
10. [Error Handling](#-error-handling)

## 🎯 Basic Syntax

Fire template code is written between `{{` and `}}` delimiters. Multiple statements can be separated using semicolons within these delimiters.

```fire
{{ statement1; statement2; statement3 }}
```

To output values, use the `output` keyword or its shorthand `=`:

```fire
{{ output $variable }}
{{ = $variable }}  // Shorthand syntax
```

## 🔄 Variables

Variables can be declared and modified in two ways:

1. Using explicit keywords:
```fire
{{ declare $myVariable = "value" }}
{{ modify $myVariable = "new value" }}
```

2. Using direct assignment (automatic declaration/modification):
```fire
{{ $myVariable = "value" }}
```

## 🔀 Control Structures

### Foreach Loops
```fire
{{ with each $array as $item at $index }}
    // Loop body
{{ endwith }}
```

### If Statements
If statements support optional else blocks:
```fire
{{ if $condition }}
    // If body code
{{ else }}  // Optional else block
    // Else body code
{{ endif }}
```

### While Loops
```fire
{{ while $condition }}
    // While body code
{{ endwhile }}
```

## 💭 Comments
Comments in Fire are written with a hyphen after the opening delimiter:

```fire
{{- This is a comment }}
{{- 
    Multi-line
    comments 
    are supported
}}
```

## 🎨 Schema Variables

Schema items are accessed using the `&` prefix. These are configured through the GUI system and can be used directly in your templates:

```fire
{{ output &schema_item_id }}
```

## 🌟 Special Variables

Special variables are predefined and can be used directly in your templates without the `{{` and `}}` delimiters:

- `$_SECTION` or `$_section`: References current section's class (`.theme-section-X`)
- `$_S_CLASS` or `$_s_class`: References current section's class name (`theme-section-X`)
- `$_FORM[name]`: Generates form submission URL
- `$_REDIRECTFORM[name]`: Generates form submission URL with redirect

For example:
```fire
/* Trying to add some css that would only apply to buttons inside this section */
<style>
    $_section button {
        background-color: #000;
        color: #fff;
    }
</style>

```

## 🚀 System API Reference

### Actions API
- `system.actions.kill($msg)` → void
  - Returns: Terminates execution with optional message

### Advanced API
- `system.advanced.address_display($address, $should_style)` → string
  - Returns: Formatted address display
- `system.advanced.unique_id($prefix, $more_entropy)` → string
  - Returns: Unique identifier
- `system.advanced.parse_link($link)` → array
  - Returns: Parsed link data [type, data]
- `system.advanced.get_link($link)` → string
  - Returns: Processed URL for product/collection links

### Array API
- `system.array.join($arr, $delim)` → string
  - Returns: Array joined with delimiter
- `system.array.check($arr)` → boolean
  - Returns: Whether input is array
- `system.array.has($arr, $val)` → boolean
  - Returns: Whether array contains value
- `system.array.has_key($arr, $key)` → boolean
  - Returns: Whether array has key
- `system.array.find($arr, $val)` → mixed
  - Returns: Key of first matching value
- `system.array.find_all($arr, $val)` → array
  - Returns: All keys matching value
- `system.array.min($arr)` → mixed
  - Returns: Minimum value
- `system.array.max($arr)` → mixed
  - Returns: Maximum value
- `system.array.sort($arr)` → array
  - Returns: Sorted array
- `system.array.length($arr)` → integer
  - Returns: Array length
- `system.array.stringify($arr)` → string
  - Returns: JSON string of array
- `system.array.remove_key($arr, $key)` → array
  - Returns: Array with key removed
- `system.array.remove_index($arr, $index)` → array
  - Returns: Array with index removed

### Colors API
- `system.colors.get($id)` → array
  - Returns: Color details by ID

### Date API
- `system.date.now()` → string
  - Returns: Current datetime
- `system.date.today()` → string
  - Returns: Current date
- `system.date.format($date, $format)` → string
  - Returns: Formatted date string

### Math API
- `system.math.floor($num)` → integer
  - Returns: Floor value
- `system.math.ceil($num)` → integer
  - Returns: Ceiling value
- `system.math.round($num)` → integer
  - Returns: Rounded value
- `system.math.abs($num)` → integer
  - Returns: Absolute value
- `system.math.pow($base, $exp)` → integer
  - Returns: Power calculation
- `system.math.sqrt($num)` → float
  - Returns: Square root
- `system.math.log($num)` → float
  - Returns: Natural logarithm
- `system.math.number_format($num)` → string
  - Returns: Formatted number with commas

### Menu API
- `system.menu.get_main_menu()` → array
  - Returns: Main menu structure
- `system.menu.get_menu($menu_id)` → array
  - Returns: Menu structure by ID
- `system.menu.get_item_content($item)` → array
  - Returns: Processed menu item content

### Multi Product API
- `system.multi_product.get_products($get)` → array
  - Returns: Filtered products based on criteria
- `system.multi_product.get_constant_filters($prods)` → array
  - Returns: Available filters for products
- `system.multi_product.get_custom_filters($prods)` → array
  - Returns: Custom filters for products
- `system.multi_product.get_filter_names($fstring, $get)` → array
  - Returns: Human-readable filter names

### Orders API
- `system.orders.get_coupons($cart)` → array
  - Returns: Available coupons for cart

### Requests API
- `system.requests.get($key)` → mixed
  - Returns: GET parameter value
- `system.requests.post($key)` → mixed
  - Returns: POST parameter value
- `system.requests.is_set($type, $param)` → boolean
  - Returns: Whether parameter exists
- `system.requests.current()` → string
  - Returns: Current URL
- `system.requests.encode($str)` → string
  - Returns: URL encoded string
- `system.requests.decode($str)` → string
  - Returns: URL decoded string
- `system.requests.redirect($url)` → void
  - Returns: Redirects to URL
- `system.requests.reload()` → void
  - Returns: Reloads current page
- `system.requests.remove_params($url, $params)` → string
  - Returns: URL with parameters removed
- `system.requests.url_without_params()` → string
  - Returns: Current URL without parameters

### Site Settings API
- `system.site_settings.get($key)` → string
  - Returns: Site setting value

### User API
- `system.user.logged_in()` → boolean
  - Returns: Whether user is logged in
- `system.user.id()` → integer
  - Returns: Current user ID
- `system.user.info()` → array
  - Returns: Current user details
- `system.user.logout()` → void
  - Returns: Logs out current user

### Cart API
- `system.cart.get_cart()` → array
  - Returns: Current user's cart with product and variant details
- `system.cart.get_cart_static()` → array
  - Returns: Raw cart data from database
- `system.cart.get_cart_total_price($coupon, $cart)` → float
  - Returns: Total cart price with optional coupon
- `system.cart.get_cart_total_discount($coupon, $cart)` → float
  - Returns: Total discount amount
- `system.cart.apply_coupon($coupon)` → float
  - Returns: Discount amount for the coupon

### Collection API
- `system.collection.get_collections()` → array
  - Returns: Array of all collection IDs
- `system.collection.get_collection($id)` → array
  - Returns: Collection details including name, image, handle, and products
- `system.collection.get_collection_products($id)` → array
  - Returns: Array of products in the collection

### Cookie API
- `system.cookie.set($key, $value, $time)` → void
  - Returns: Sets cookie with specified expiry time
- `system.cookie.get($key)` → string
  - Returns: Cookie value
- `system.cookie.exists($key)` → boolean
  - Returns: Whether cookie exists
- `system.cookie.remove($key)` → void
  - Returns: Removes cookie
- `system.cookie.destroy()` → void
  - Returns: Removes all cookies

### Posts API
- `system.posts.get_posts()` → array
  - Returns: All blog posts
- `system.posts.get_post($id)` → array
  - Returns: Single post details
- `system.posts.get_post_by_type($type)` → array
  - Returns: Posts of specific type
- `system.posts.get_post_meta($id)` → array
  - Returns: Post meta information
- `system.posts.get_blog_posts_by_category($category)` → array
  - Returns: Posts in specified category

### Product API
- `system.product.get_products()` → array
  - Returns: Array of all product IDs
- `system.product.get_product($id)` → array
  - Returns: Product details including name, description, images, variants, and slug
- `system.product.get_metafields($id)` → array
  - Returns: Array of product metafields with field names and values
- `system.product.get_meta_content_blocks($id)` → array
  - Returns: Array of content block metafields
- `system.product.similar($id)` → array
  - Returns: Array of similar product IDs
- `system.product.get_prod_variants($id)` → array
  - Returns: Array of product variant details
- `system.product.get_prod_from_variant($v_id)` → array
  - Returns: Parent product details for a variant
- `system.product.get_metafield($metafields, $slug)` → array
  - Returns: Specific metafield value by slug

### Session API
- `system.session.set($key, $value)` → void
  - Returns: Sets session variable
- `system.session.get($key)` → mixed
  - Returns: Session variable value
- `system.session.exists($key)` → boolean
  - Returns: Whether session variable exists
- `system.session.remove($key)` → void
  - Returns: Removes session variable
- `system.session.destroy()` → void
  - Returns: Destroys entire session

### String API
- `system.string.split($str, $delim)` → array
  - Returns: Array of strings split by delimiter
- `system.string.split_no_empty($str, $delim)` → array
  - Returns: Array of non-empty strings split by delimiter
- `system.string.trim($str)` → string
  - Returns: String with whitespace removed from both ends
- `system.string.concat($str1, $str2)` → string
  - Returns: Concatenated string
- `system.string.parse($str)` → mixed
  - Returns: Parsed JSON string as PHP value
- `system.string.to_int($str)` → integer
  - Returns: String converted to integer

## 🔗 String Concatenation

String concatenation is performed using the period (.) operator:

```fire
{{ $fullName = $firstName . " " . $lastName }}
```

## 💡 Best Practices

1. 🎯 Always initialize variables before use
2. 📝 Use meaningful variable names
3. 🧩 Keep template sections modular
4. 🔍 Validate data before output
5. 📊 Use appropriate API calls for data operations
6. 🎨 Follow consistent indentation
7. 💭 Use comments to explain complex logic
8. 🔍 Check return types of API calls
9. ⚡ Use shorthand output when appropriate
10. 🎯 Keep control structures clean and well-indented

## ⚠️ Error Handling

The template system displays errors in this format:
```
<b>ERROR: </b>Description of the error
```

Common errors include:
- ❌ Undeclared variables
- ❌ Invalid schema items
- ❌ Syntax errors
- ❌ Invalid API calls 
