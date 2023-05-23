# User
Docker container:
```shell
php bin/console make:Entity
```
Name: User
<table>
    <tr>
        <td><strong>Property</strong></td>
        <td><strong>Type</strong></td>
        <td><strong>Length</strong></td>
        <td><strong>nullable</strong></td>
    </tr>
    <tr>
        <td>email</td>
        <td>String</td>
        <td>255</td>
        <td>no</td>
    </tr>
    <tr>
        <td>name</td>
        <td>String</td>
        <td>255</td>
        <td>no</td>
    </tr>
    <tr>
        <td>password</td>
        <td>String</td>
        <td>255</td>
        <td>no</td>
    </tr>
</table>

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
