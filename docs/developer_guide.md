# Developer Guide

## Key Components

### Webhook Handler

```python
# webhook.py

def handle_webhook_response():
    """Handle incoming Paystack webhook requests."""
    # Get raw payload
    raw_data = get_raw_payload(frappe.request.data)
    
    # Verify signature
    if not verify_signature(raw_data):
        return frappe.throw("Invalid signature")
        
    # Process payment
    process_payment(raw_data)
    
    return {"status": "success"}
```

### Payment Request

```python
# payment_request.py

def generate_payment_url(self):
    """Generate payment URL for Paystack."""
    return f"https://paystack.com/pay/{self.reference}"
    
    def process_payment(self, data):
        """Process payment response."""
        if data["status"] == "success":
            self.create_payment_entry()
        else:
            self.log_payment_failure()
```

## Core Classes

### PaymentProcessor

```python
class PaymentProcessor:
    """Handles payment processing logic."""
    
    def __init__(self, reference):
        self.reference = reference
        
    def process_payment(self, data):
        """Process payment response."""
        if data["status"] == "success":
            self.create_payment_entry()
        else:
            self.log_payment_failure()
            
    def create_payment_entry(self):
        """Create Payment Entry."""
        pe = frappe.new_doc("Payment Entry")
        pe.reference_no = self.reference
        pe.paid_amount = data["amount"]
        pe.insert()
        pe.submit()
```

### WebhookManager

```python
class WebhookManager:
    """Manages webhook processing."""
    
    def __init__(self, signature, data):
        self.signature = signature
        self.data = data
        
    def verify_signature(self):
        """Verify webhook signature."""
        computed_signature = hmac.new(
            key=get_secret_key().encode('utf-8'),
            msg=self.data,
            digestmod=hashlib.sha512
        ).hexdigest()
        return hmac.compare_digest(computed_signature, self.signature)
        
    def process_webhook(self):
        """Process webhook data."""
        if self.verify_signature():
            process_payment(self.data)
        else:
            frappe.throw("Invalid signature")
```

## Extension Points

1. **Custom Payment Processors**
   - Override payment processing logic
   - Add custom validation
   - Modify payment flow

2. **Webhook Handlers**
   - Add custom webhook processing
   - Extend error handling
   - Add custom logging

3. **Payment Entry Hooks**
   - Modify payment entry creation
   - Add custom validations
   - Extend payment processing

## Best Practices

1. **Code Organization**
   - Keep logic modular
   - Use clear naming
   - Document all functions
   - Follow Frappe conventions

2. **Error Handling**
   - Handle all exceptions
   - Log errors properly
   - Provide clear messages
   - Implement retries

3. **Security**
   - Verify signatures
   - Check IPs
   - Sanitize inputs
   - Use HTTPS

## Common Customizations

### Custom Payment Validation

```python
def validate_payment(data):
    """Custom payment validation."""
    if not validate_amount(data["amount"]):
        frappe.throw("Invalid amount")
        
    if not validate_currency(data["currency"]):
        frappe.throw("Invalid currency")
```

### Custom Webhook Processing

```python
def custom_webhook_processor(data):
    """Custom webhook processing."""
    if data["event"] == "custom.event":
        process_custom_event(data)
```

## Debugging Tools

### Logging

```python
def log_payment(data):
    """Log payment details."""
    frappe.log_error(
        title="Payment Log",
        message=f"Payment Data: {json.dumps(data, indent=4)}"
    )
```

### Testing

```python
def test_webhook():
    """Test webhook processing."""
    test_data = {
        "event": "charge.success",
        "data": {
            "amount": 100000,
            "currency": "NGN",
            "reference": "test_123"
        }
    }
    handle_webhook_response(test_data)
```

## Performance Considerations

1. **Webhook Processing**
   - Use async processing
   - Implement retries
   - Add timeout handling
   - Monitor performance

2. **Payment Processing**
   - Batch operations
   - Use transactions
   - Add caching
   - Monitor load

## Security Best Practices

1. **API Keys**
   - Store in environment variables
   - Rotate regularly
   - Use different keys for environments
   - Never expose in code

2. **Webhooks**
   - Verify signatures
   - Check IPs
   - Limit retry attempts
   - Monitor failures

3. **Payment Data**
   - Encrypt sensitive data
   - Use HTTPS
   - Implement rate limiting
   - Monitor access

## Troubleshooting Guide

### Common Issues

1. **Payment Failures**
   - Solution: Check payment status
   - Check: Payment logs
   - Solution: Retry payment

2. **Webhook Failures**
   - Solution: Verify signature
   - Check: Network connectivity
   - Solution: Enable debug mode

### Verification Steps

1. Check webhook logs:
   ```python
   frappe.get_all("Webhook Log", filters={"status": "Failed"})
   ```

2. Verify payment status:
   ```python
   frappe.get_doc("Payment Request", "PR-001").status
   ```

3. Check payment entries:
   ```python
   frappe.get_all("Payment Entry", filters={"reference_no": "PR-001"})
   ```
