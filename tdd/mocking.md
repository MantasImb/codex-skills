# When to Mock

Mock at **system boundaries** only:

- External APIs (payment, email, etc.)
- Databases (sometimes - prefer test DB)
- Time/randomness
- File system (sometimes)

Don't mock:

- Your own classes/modules
- Internal collaborators
- Anything you control

Rust additions:

- Prefer a fake implementation of a trait or port over a behavior-heavy mock when the boundary is under your control
- Keep traits small so test doubles stay simple
- Do not introduce a trait only for testing if no real boundary exists

## Designing for Mockability

At system boundaries, design interfaces that are easy to mock:

**1. Use dependency injection**

Pass external dependencies in rather than creating them internally:

```typescript
// Easy to mock
function processPayment(order, paymentClient) {
  return paymentClient.charge(order.total);
}

// Hard to mock
function processPayment(order) {
  const client = new StripeClient(process.env.STRIPE_KEY);
  return client.charge(order.total);
}
```

```rust
// Easy to substitute in tests
async fn process_payment(
    order: &Order,
    payment_client: &dyn PaymentClient,
) -> Result<ChargeId, PaymentError> {
    payment_client.charge(order.total()).await
}

// Hard to substitute in tests
async fn process_payment(order: &Order) -> Result<ChargeId, PaymentError> {
    let client = StripeClient::new(std::env::var("STRIPE_KEY")?);
    client.charge(order.total()).await
}
```

**2. Prefer SDK-style interfaces over generic fetchers**

Create specific functions for each external operation instead of one generic function with conditional logic:

```typescript
// GOOD: Each function is independently mockable
const api = {
  getUser: (id) => fetch(`/users/${id}`),
  getOrders: (userId) => fetch(`/users/${userId}/orders`),
  createOrder: (data) => fetch("/orders", { method: "POST", body: data }),
};

// BAD: Mocking requires conditional logic inside the mock
const api = {
  fetch: (endpoint, options) => fetch(endpoint, options),
};
```

The SDK approach means:

- Each mock returns one specific shape
- No conditional logic in test setup
- Easier to see which endpoints a test exercises
- Type safety per endpoint

Rust equivalent:

- Prefer a trait with explicit methods such as `get_user`, `get_orders`, and `create_order`
- Avoid one generic `request` method that pushes branching and protocol details into every test double
