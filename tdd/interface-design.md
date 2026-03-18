# Interface Design for Testability

Good interfaces make testing natural:

1. **Accept dependencies, don't create them**

   ```typescript
   // Testable
   function processOrder(order, paymentGateway) {}

   // Hard to test
   function processOrder(order) {
     const gateway = new StripeGateway();
   }
   ```

   ```rust
   // Testable
   async fn process_order(
       order: &Order,
       gateway: &dyn PaymentGateway,
   ) -> Result<Receipt, Error> {}

   // Hard to test
   async fn process_order(order: &Order) -> Result<Receipt, Error> {
       let gateway = StripeGateway::new();
       gateway.charge(order.total()).await
   }
   ```

2. **Return results, don't produce side effects**

   ```typescript
   // Testable
   function calculateDiscount(cart): Discount {}

   // Hard to test
   function applyDiscount(cart): void {
     cart.total -= discount;
   }
   ```

   ```rust
   // Testable
   fn calculate_discount(cart: &Cart) -> Discount {}

   // Harder to reason about and verify
   fn apply_discount(cart: &mut Cart) {
       cart.total -= discount_for(cart);
   }
   ```

3. **Small surface area**
   - Fewer methods = fewer tests needed
   - Fewer params = simpler test setup

4. **Separate orchestration from side-effecting adapters**
   - Keep domain decisions in functions or services that can run with simple inputs
   - Push HTTP, database, queue, and SDK details behind thin adapters
