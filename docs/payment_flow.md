# Payment Request Flow

## Overview

The payment request flow in Ntech Paystack integrates seamlessly with ERPNext's payment system, allowing users to generate and process payments through Paystack. This section details the complete payment request lifecycle.

## Payment Request Creation

### Step 1: Generate Payment Request

1. **Payment Request DocType**
   - Create new Payment Request
   - Select payment type (Advance, Against Sales Order, etc.)
   - Enter payment amount
   - Select currency
   - Add reference document

2. **Required Fields**
   - **Payment Type**: Required
   - **Party Type**: Required
   - **Party**: Required
   - **Amount**: Required
   - **Currency**: Required
   - **Reference Document**: Required

### Step 2: Payment Generation

1. **Payment URL Generation**
   ```python
   # Example payment URL generation
   payment_url = frappe.get_doc({
       "doctype": "Payment Request",
       "payment_type": "Advance",
       "party_type": "Customer",
       "party": "CUST-001",
       "amount": 1000,
       "currency": "NGN",
       "reference_doctype": "Sales Invoice",
       "reference_name": "SI-001"
   }).generate_payment_url()
   ```

2. **Payment Link**
   - Format: `https://your-site.com/api/method/ntech_paystack.webhook.handle_webhook_response`
   - Includes payment reference
   - Secure HTTPS connection

### Step 3: Payment Processing

1. **Payment Flow**
   - User clicks payment link
   - Redirected to Paystack payment page
   - Payment processed through Paystack
   - Webhook notification sent

2. **Payment Status Updates**
   - **Pending**: Payment initiated
   - **Processing**: Payment in progress
   - **Completed**: Payment successful
   - **Failed**: Payment failed

### Step 4: Payment Completion

1. **Webhook Processing**
   ```python
   # Webhook handler
   def handle_webhook_response():
       # Verify signature
       # Process payment
       # Update Payment Log
       # Create Payment Entry
   ```

2. **Payment Entry Creation**
   - Automatic creation on success
   - Links to reference document
   - Updates payment status
   - Creates payment entry

## Error Handling

### Common Errors

1. **Payment Failures**
   - Solution: Check payment status
   - Check: Payment logs
   - Solution: Retry payment

2. **Webhook Failures**
   - Solution: Verify webhook URL
   - Check: Network connectivity
   - Solution: Enable debug mode

### Error Recovery

1. **Failed Payments**
   - Retry payment
   - Check logs
   - Contact support

2. **Webhook Failures**
   - Manual reconciliation
   - Check logs
   - Verify settings

## Best Practices

1. **Payment Generation**
   - Verify amounts
   - Check currency
   - Validate references
   - Use secure links

2. **Payment Processing**
   - Monitor status
   - Check logs
   - Verify webhooks
   - Test thoroughly

3. **Payment Completion**
   - Verify entries
   - Check reconciliation
   - Monitor failures
   - Regular audits

## Security Considerations

1. **Payment Links**
   - Use HTTPS
   - Secure references
   - Time-limited links
   - Monitor usage

2. **Webhook Security**
   - Verify signatures
   - Check IP addresses
   - Monitor attempts
   - Set up alerts

3. **Payment Data**
   - Encrypt sensitive data
   - Regular audits
   - Monitor access
   - Secure backups

## Troubleshooting

### Common Issues

1. **Payment Failures**
   - Solution: Verify payment details
   - Check: Payment logs
   - Solution: Retry payment

2. **Webhook Failures**
   - Solution: Verify webhook URL
   - Check: Network connectivity
   - Solution: Enable debug mode

### Verification Steps

1. Check payment status:
   ```python
   frappe.get_doc("Payment Request", "PR-001").status
   ```

2. Verify webhook logs:
   ```python
   frappe.get_all("Webhook Log", filters={"status": "Failed"})
   ```

3. Check payment entries:
   ```python
   frappe.get_all("Payment Entry", filters={"reference_no": "PR-001"})
   ```
