# 🔥 Fire Template Language Documentation

## 📚 Table of Contents
1. [Basic Syntax](#basic-syntax)
2. [Variables](#variables)
3. [Control Structures](#control-structures)
4. [Schema Variables](#schema-variables)
5. [System API Reference](#system-api-reference)
6. [Special Variables](#special-variables)
7. [Best Practices](#best-practices)

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
```fire
{{ if $condition }}
    // If body code
{{ endif }}
```

### While Loops
```fire
{{ while $condition }}
    // While body code
{{ endwhile }}
```

## 🎨 Schema Variables

Schema items are accessed using the `&` prefix. These are configured through the GUI system and can be used directly in your templates:

```fire
{{ output &schema_item_id }}
```

## 🌟 Special Variables

- `$_SECTION` or `$_section`: References current section's class (`.theme-section-X`)
- `$_S_CLASS` or `$_s_class`: References current section's class name (`theme-section-X`)
- `$_FORM[name]`: Generates form submission URL
- `$_REDIRECTFORM[name]`: Generates form submission URL with redirect

## 🚀 System API Reference

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

### Array API
- `system.array.merge($arr1, $arr2)` → array
  - Returns: Merged array
- `system.array.filter($arr, $condition)` → array
  - Returns: Filtered array based on condition
- `system.array.map($arr, $callback)` → array
  - Returns: Array with callback applied to each element

### Session API
- `system.session.get($key)` → mixed
  - Returns: Session value for key
- `system.session.set($key, $value)` → boolean
  - Returns: Success status
- `system.session.remove($key)` → boolean
  - Returns: Success status

### Cookie API
- `system.cookie.get($name)` → string
  - Returns: Cookie value
- `system.cookie.set($name, $value, $expiry)` → boolean
  - Returns: Success status
- `system.cookie.delete($name)` → boolean
  - Returns: Success status

### Database API
- `system.db.query($sql, $params)` → array
  - Returns: Query results
- `system.db.insert($table, $data)` → integer
  - Returns: Inserted ID
- `system.db.update($table, $data, $where)` → boolean
  - Returns: Success status

### Posts API
- `system.posts.get_posts()` → array
  - Returns: All blog posts
- `system.posts.get_post($id)` → array
  - Returns: Single post details
- `system.posts.get_post_by_type($type)` → array
  - Returns: Posts of specific type
- `system.posts.get_post_meta($id)` → array
  - Returns: Post meta information

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
7. 💭 Comment complex logic

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
