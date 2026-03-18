# Good and Bad Tests

## Good Tests

**Integration-style**: Test through real interfaces, not mocks of internal parts.

```typescript
// GOOD: Tests observable behavior
test("user can checkout with valid cart", async () => {
  const cart = createCart();
  cart.add(product);
  const result = await checkout(cart, paymentMethod);
  expect(result.status).toBe("confirmed");
});
```

```rust
// GOOD: Tests observable behavior
#[tokio::test]
async fn checkout_confirms_a_valid_cart() {
    let cart = Cart::with_product(product());
    let result = checkout(&cart, &payment_gateway).await.unwrap();
    assert_eq!(result.status, CheckoutStatus::Confirmed);
}
```

Characteristics:

- Tests behavior users/callers care about
- Uses public API only
- Survives internal refactors
- Describes WHAT, not HOW
- One logical assertion per test

## Bad Tests

**Implementation-detail tests**: Coupled to internal structure.

```typescript
// BAD: Tests implementation details
test("checkout calls paymentService.process", async () => {
  const mockPayment = jest.mock(paymentService);
  await checkout(cart, payment);
  expect(mockPayment.process).toHaveBeenCalledWith(cart.total);
});
```

```rust
// BAD: Tests implementation details
#[tokio::test]
async fn checkout_calls_payment_gateway_once() {
    let gateway = SpyGateway::default();
    checkout(&cart(), &gateway).await.unwrap();
    assert_eq!(gateway.charge_call_count(), 1);
}
```

Red flags:

- Mocking internal collaborators
- Testing private methods
- Asserting on call counts/order
- Test breaks when refactoring without behavior change
- Test name describes HOW not WHAT
- Verifying through external means instead of interface

```typescript
// BAD: Bypasses interface to verify
test("createUser saves to database", async () => {
  await createUser({ name: "Alice" });
  const row = await db.query("SELECT * FROM users WHERE name = ?", ["Alice"]);
  expect(row).toBeDefined();
});

// GOOD: Verifies through interface
test("createUser makes user retrievable", async () => {
  const user = await createUser({ name: "Alice" });
  const retrieved = await getUser(user.id);
  expect(retrieved.name).toBe("Alice");
});
```

```rust
// BAD: Reaches past the public API to inspect storage directly
#[tokio::test]
async fn create_user_writes_a_row() {
    let user_id = create_user(&app, NewUser::named("Alice")).await.unwrap();
    let row = app.pool().fetch_user_row(user_id).await.unwrap();
    assert_eq!(row.name, "Alice");
}

// GOOD: Verifies through a public interface
#[tokio::test]
async fn create_user_makes_the_user_retrievable() {
    let user = create_user(&app, NewUser::named("Alice")).await.unwrap();
    let retrieved = get_user(&app, user.id).await.unwrap();
    assert_eq!(retrieved.name, "Alice");
}
```

Rust note:

- Prefer ordinary assertions on returned values, domain events, or HTTP responses.
- Use `tests/` integration tests when behavior spans multiple modules or adapters.
- Reach into database tables, queues, or internals only when that storage boundary is itself the public contract being tested.
