## Change Data Feed (CDF) with Lakebase Postgres

### Create the Lakebase table

Open your Lakebase SQL Editor and run:
```sql
CREATE TABLE customer_orders (
    order_id INTEGER NOT NULL,
    customer_name TEXT NOT NULL,
    product TEXT NOT NULL,
    amount BIGINT NOT NULL,
    status TEXT NOT NULL,
    PRIMARY KEY (order_id)
);
```

### Add some initial orders

```sql
INSERT INTO customer_orders
    (order_id, customer_name, product, amount, status)
VALUES
    (1001, 'Alice', 'Laptop', 1200, 'PLACED'),
    (1002, 'Bob', 'Headphones', 200, 'PLACED'),
    (1003, 'Charlie', 'Monitor', 450, 'PLACED');
```

### Enable full row information for changes

```sql
ALTER TABLE customer_orders
REPLICA IDENTITY FULL;
```

### Test INSERT

Now pretend a customer places a new order.

Run in Lakebase:

```sql
INSERT INTO customer_orders
    (order_id, customer_name, product, amount, status)
VALUES
    (1004, 'David', 'Keyboard', 100, 'PLACED');
```

### Test UPDATE

```sql
UPDATE customer_orders
SET status = 'SHIPPED'
WHERE order_id = 1004;
```