# Datalexicon sales model example

This example models a small sales domain: customers place sales orders, each
order contains product lines, and country codes identify customer and shipping
countries.

## Models

- `models/customer.yaml` — customer details and home country
- `models/country.yaml` — country code lookup
- `models/sales_order.yaml` — order header, customer, and shipping country
- `models/sales_order_line.yaml` — products, quantities, and prices captured on
  each order line
- `models/product.yaml` — product catalogue

Relationships are declared on both sides to make cardinality clear. Each sales
order line has its own identifier; `UnitPrice` records the price at the time of
the order, while the line total can be calculated from quantity and unit price.

## Project configuration

- `datalexicon.yml` selects the `models/` and `standards/` directories and the
  PostgreSQL dialect.
- `standards/naming.yml` defines physical naming and constraint conventions.
- `standards/abbreviations.yml` shows examples such as `Customer: CUST`,
  `Product: PROD`, `Quantity: QTY`, and `Date: DT` for generated names.
- `standards/glossary.yml` documents the business entities.

Validate the models and regenerate the PostgreSQL output after making changes:

```shell
datalexicon validate
datalexicon build
```

Generated SQL is written under `target/postgres/`.
