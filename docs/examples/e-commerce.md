---
title: E-Commerce Example
---

# E-Commerce Example

An online store with products, cart, and checkout.

## Features

- Product catalog with images
- Shopping cart (session-based)
- Checkout flow
- Order management

## Quick Start

```bash
tavp new my-store
cd my-store
tavp migrate
tavp serve
```

## Routes

```php
$router->get('/', [HomeController::class, 'index']);
$router->get('/products', [ProductController::class, 'index']);
$router->get('/products/{slug}', [ProductController::class, 'show']);
$router->post('/cart/add', [CartController::class, 'add']);
$router->get('/cart', [CartController::class, 'index']);
$router->post('/checkout', [CheckoutController::class, 'store']);
```

## Product Model

```php
class Product extends Model
{
    protected string $table = 'products';
    protected array $fillable = ['name', 'slug', 'description', 'price', 'image', 'stock'];
    protected array $casts = ['price' => 'float', 'stock' => 'integer'];
}
```

## Cart (Session-based)

```php
class CartController extends BaseController
{
    public function add(): Response
    {
        $productId = $this->request->input('product_id');
        $quantity = (int) $this->request->input('quantity', 1);

        $_SESSION['cart'][] = ['product_id' => $productId, 'quantity' => $quantity];

        return $this->redirect('/cart');
    }

    public function index(): string
    {
        $cart = $_SESSION['cart'] ?? [];
        return $this->view('cart/index', ['cart' => $cart]);
    }
}
```

## Learn More

- [ORM](/features/orm)
- [Storage](/features/storage)
