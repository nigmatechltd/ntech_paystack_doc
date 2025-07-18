# API Reference

## Webhook Endpoints

### Payment Webhook

**Endpoint**: `POST /api/method/ntech_paystack.webhook.handle_webhook_response`

**Headers**:
- `x-paystack-signature`: HMAC SHA512 signature
- `Content-Type`: `application/json`

**Request Body**:
```json
{
    "event": "charge.success",
    "data": {
        "id": "flw_REF_123456",
        "amount": 100000,
        "currency": "NGN",
        "reference": "PR-001",
        "status": "success",
        "customer": {
            "email": "customer@example.com",
            "name": "John Doe"
        }
    }
}
```

**Response**:
```json
{
    "status": "success",
    "message": "Webhook processed successfully"
}
```

### Payment URL Generation

**Endpoint**: `GET /api/method/ntech_paystack.api.get_payment_url`

**Parameters**:
- `payment_request`: Payment Request ID
- `amount`: Payment amount
- `currency`: Currency code
- `reference`: Reference document

**Response**:
```json
{
    "payment_url": "https://your-site.com/api/method/ntech_paystack.webhook.handle_webhook_response?reference=PR-001"
}
```

## Client-Side API

### Payment Request Generation

```javascript
// Generate payment request
function generatePaymentRequest(data) {
    return frappe.call({
        method: "ntech_paystack.api.generate_payment_request",
        args: {
            payment_type: data.type,
            party_type: data.party_type,
            party: data.party,
            amount: data.amount,
            currency: data.currency,
            reference_doctype: data.reference_doctype,
            reference_name: data.reference_name
        }
    });
}
```

### Payment Status Check

```javascript
// Check payment status
function checkPaymentStatus(reference) {
    return frappe.call({
        method: "ntech_paystack.api.get_payment_status",
        args: {
            reference: reference
        }
    });
}
```

## Error Handling

### Webhook Errors

```json
{
    "status": "error",
    "message": "Invalid signature",
    "code": 403
}
```

### Payment Errors

```json
{
    "status": "error",
    "message": "Payment failed",
    "code": 400,
    "data": {
        "error": "Insufficient funds"
    }
}
```

## Security Considerations

1. **Signature Verification**
   ```python
   # Example signature verification
   def verify_signature(payload, signature):
       secret_key = get_secret_key()
       computed_signature = hmac.new(
           key=secret_key.encode('utf-8'),
           msg=payload,
           digestmod=hashlib.sha512
       ).hexdigest()
       return hmac.compare_digest(computed_signature, signature)
   ```

2. **IP Whitelisting**
   ```python
   # Example IP verification
   def verify_ip(ip_address):
       whitelisted_ips = get_whitelisted_ips()
       return ip_address in whitelisted_ips
   ```

## Best Practices

1. **Webhook Processing**
   - Always verify signatures
   - Check IP addresses
   - Handle errors gracefully
   - Log all requests

2. **Payment Processing**
   - Validate all inputs
   - Check payment status
   - Handle failures
   - Monitor logs

3. **Security**
   - Use HTTPS
   - Verify signatures
   - Check IPs
   - Monitor logs

## Troubleshooting

### Common Issues

1. **Webhook Failures**
   - Solution: Verify signature
   - Check: Network connectivity
   - Solution: Enable debug mode

2. **Payment Failures**
   - Solution: Check payment status
   - Check: Payment logs
   - Solution: Retry payment

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
