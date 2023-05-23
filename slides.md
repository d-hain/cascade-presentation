# User
Docker container:
```shell
php bin/console make:Entity
```
Name: User
| Property | Type   | Length | nullable |
| -------- | ------ | ------ | -------- |
| email    | String | 255    | no       |
| name     | String | 255    | no       |
| password | String | 255    | no       |

---

# Cascade?

## Persist

If an entity is persisted (added/updated) then all its children will also be persisted.

## Remove

If one entity gets deleted then all its children also get deleted.

---

## Cascade for the Cart
`Cart.php`
```php
#[ORM\OneToMany(
    mappedBy: "cart", 
    targetEntity: CartProduct::class, 
    cascade: ["persist", "remove"], 
    orphanRemoval: true
)]
private Collection $cartProducts;
```

--

`CartProduct.php`
```php
#[ORM\ManyToOne(
    inversedBy: "cartProducts"
)] 
#[ORM\JoinColumn(
    nullable: false, 
    onDelete: "cascade"
)] 
private ?Product $product = null; 

#[ORM\ManyToOne(
    inversedBy: "cartProducts"
)] 
#[ORM\JoinColumn(
    nullable: false, 
    onDelete: "cascade"
)] 
private ?Cart $cart = null;
```

---

# User Controller
Docker container:
```shell
php bin/console make:Controller
```
Name: User
