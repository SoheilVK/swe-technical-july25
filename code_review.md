# Code Review - Production Booking System

## Instructions

You are reviewing code for a ticket booking system that is currently running in production. This function handles purchasing tickets for events and processes real payments.

Please review the code below and identify any issues, concerns, or improvements you would recommend. Consider:

- Security vulnerabilities
- Potential bugs or edge cases
- Performance concerns
- Code quality and maintainability
- Production readiness

Feel free to think out loud and explain your reasoning as you review the code.

## Code to Review

```python
def purchase_tickets(event_id, user_id, quantity):
    # Check availability
    query = f"SELECT available_tickets FROM events WHERE id = {event_id}"
    result = db.execute(query)
    available = result[0]['available_tickets']
   
    if available >= quantity:
        # Calculate total price
        price_query = f"SELECT min_price FROM events WHERE id = {event_id}"
        price_result = db.execute(price_query)
        total_price = price_result[0]['min_price'] * quantity
       
        # Process payment
        payment_result = process_payment(user_id, total_price)
       
        if payment_result == "success":
            # Update inventory
            update_query = f"UPDATE events SET available_tickets = available_tickets - {quantity} WHERE id = {event_id}"
            db.execute(update_query)
           
            # Record purchase
            insert_query = f"INSERT INTO purchases (user_id, event_id, quantity, total_price) VALUES ({user_id}, {event_id}, {quantity}, {total_price})"
            db.execute(insert_query)
           
            return {"status": "success", "message": f"Purchased {quantity} tickets"}
        else:
            return {"status": "error", "message": "Payment failed"}
    else:
        return {"status": "error", "message": "Not enough tickets"}
```

## Context

- This is a high-traffic e-commerce system
- Multiple users may attempt to purchase tickets simultaneously
- The system processes real money transactions
- Event tickets can sell out quickly (think concert tickets)

---

*Take your time and walk through the code systematically. There's no rush.*