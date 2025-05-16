
# E-commerce Platform Prototype

# --- Product Classes ---
class Product:
    def __init__(self, product_id, name, price):
        self.product_id = product_id
        self.name = name
        self.price = price

    def __str__(self):
        return f"{self.name} (${self.price})"


class Electronics(Product):
    """ Electronics product that extends the Product class """
    def __init__(self, product_id, name, price, warranty):
        super().__init__(product_id, name, price)
        self.warranty = warranty


class Clothing(Product):
    """ Clothing product that extends the Product class """
    def __init__(self, product_id, name, price, size, color):
        super().__init__(product_id, name, price)
        self.size = size
        self.color = color


class Grocery(Product):
    """ Grocery product that extends the Product class """
    def __init__(self, product_id, name, price, expiry_date):
        super().__init__(product_id, name, price)
        self.expiry_date = expiry_date


# --- User Classes ---
class User:
    def __init__(self, user_id, name):
        self.user_id = user_id
        self.name = name


class Customer(User):
    """ Customer user that can add products to their shopping cart """
    def __init__(self, user_id, name, email):
        super().__init__(user_id, name)
        self.email = email
        self.cart = []

    def add_to_cart(self, product):
        self.cart.append(product)


class Admin(User):
    """ Admin user with special permissions """
    def __init__(self, user_id, name, admin_level):
        super().__init__(user_id, name)
        self.admin_level = admin_level


# --- Order Class ---
class Order:
    def __init__(self, order_id, customer, products):
        self.order_id = order_id
        self.customer = customer
        self.products = products

    def calculate_total(self):
        subtotal = sum(map(lambda p: p.price, self.products))
        tax = subtotal * 0.08
        shipping = 10 if subtotal < 100 else 0
        return subtotal + tax + shipping


# --- Lambdas for filtering and sorting ---
# Filter example: Electronics products only
filter_electronics = lambda products: list(filter(lambda p: isinstance(p, Electronics), products))

# Lambda to sort products by price
sort_by_price = lambda products: sorted(products, key=lambda p: p.price)

# --- Example Usage ---
products = [
    Electronics(1, 'Laptop', 1200, '2 Years'),
    Clothing(2, 'T-Shirt', 20, 'M', 'Red'),
    Grocery(3, 'Apple', 1, '2025-05-20'),
    Electronics(4, 'Phone', 800, '1 Year')
]

# Filtering Electronics
print("Filtered Electronics:")
print(filter_electronics(products))

# Sorting by Price
print("\nSorted by Price:")
print(sort_by_price(products))

