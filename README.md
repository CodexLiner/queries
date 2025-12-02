# GetProducts Query Documentation

This document contains the GraphQL query for fetching products along with variants, pricing, media, and attributes.

---

## Query

<details>
  <summary><strong>Show / Hide GraphQL Query</strong></summary>

```graphql
query GetProducts($channel: String!, $first: Int!) {
    products(first: $first, channel: $channel) {
        edges {
            node {
                id
                name
                slug
                # description

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
