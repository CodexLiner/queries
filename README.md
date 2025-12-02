

# GraphQL Queries Documentation

This document provides well-structured references for two commonly used GraphQL queries:

- `GetProducts` — retrieves product details, variants, pricing, category information, and related metadata.
- `GetCategoriesWithProducts` — retrieves categories and the products belonging to each category.

Use these queries as part of integrations where product and category information is required, such as storefronts, admin tools, or external service integrations.

---

## 1. GetProducts Query

### **Purpose**
Fetches products for a specific sales channel, including detailed product metadata such as variants, pricing, media, attributes, and inventory availability.

### **Variables**
| Name | Type | Description |
|------|------|-------------|
| `channel` | `String!` | Sales channel slug from which to fetch product data. |
| `first` | `Int!` | Number of products to return. |

### **Query**
<details>
  <summary><strong>Show / Hide Query</strong></summary>

```graphql
query GetProducts($channel: String!, $first: Int!) {
    products(first: $first, channel: $channel) {
        edges {
            node {
                id
                name
                slug

                thumbnail {
                    url
                }

                category {
                    id
                    name
                }

                productType {
                    id
                    name
                    hasVariants
                }

                variants {
                    id
                    name
                    sku

                    media {
                        url
                    }

                    pricing {
                        price {
                            gross {
                                amount
                                currency
                            }
                        }
                    }

                    attributes {
                        attribute {
                            name
                            slug
                        }
                        values {
                            name
                            slug
                        }
                    }

                    quantityAvailable
                }
            }
        }
    }
}
````

</details>

---

## 2. GetCategoriesWithProducts Query

### **Purpose**

Retrieves a list of categories along with a paginated list of products in each category. Useful for building category-based navigation or filtering structures.

### **Variables**

| Name      | Type      | Description                                                      |
| --------- | --------- | ---------------------------------------------------------------- |
| `first`   | `Int!`    | Number of categories to fetch.                                   |
| `channel` | `String!` | Sales channel slug used to filter products within each category. |

### **Query**

<details>
  <summary><strong>Show / Hide Query</strong></summary>

```graphql
query GetCategoriesWithProducts($first: Int!, $channel: String!) {
  categories(first: $first) {
    edges {
      node {
        id
        name
        slug

        products(first: 20, channel: $channel) {
          totalCount
          edges {
            node {
              id
              name
              slug
              thumbnail {
                url
              }
            }
          }
        }
      }
    }
  }
}
```

</details>

---
