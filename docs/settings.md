# Paystack Settings

## Overview

The Paystack Settings doctype allows administrators to configure and manage the Paystack payment gateway integration within ERPNext. This section provides detailed information about each configuration option.

## Configuration Fields

### Basic Settings

1. **Payment Gateway Title**
   - Display name for the payment gateway
   - Used in payment request forms
   - Default: "Paystack"

2. **Mode**
   - Test/Live mode toggle
   - Test mode: Uses sandbox API keys
   - Live mode: Uses production API keys

### API Configuration

1. **API Key**
   - Your Paystack API key
   - Required for payment processing
   - Keep secure and never expose

2. **Secret Key**
   - Your Paystack secret key
   - Used for webhook verification
   - Never expose in client-side code

3. **Webhook URL**
   - URL where Paystack sends notifications
   - Must be HTTPS
   - Format: `https://your-site.com/api/method/ntech_paystack.webhook.handle_webhook_response`

### Security Settings

1. **IP Whitelisting**
   - Restrict webhook access to specific IPs
   - Format: `192.168.1.1,192.168.1.2`
   - Leave blank to allow all IPs

2. **Signature Verification**
   - Enable/disable HMAC SHA512 verification
   - Default: Enabled
   - Recommended: Always enabled

### Payment Settings

1. **Currency**
   - Default currency for payments
   - Format: `NGN`
   - Can be overridden per payment request

2. **Minimum Amount**
   - Minimum allowed payment amount
   - Format: `100`
   - Leave blank for no minimum

3. **Maximum Amount**
   - Maximum allowed payment amount
   - Format: `1000000`
   - Leave blank for no maximum

### Advanced Settings

1. **Debug Mode**
   - Enable detailed logging
   - Default: Disabled
   - Use for troubleshooting

2. **Retry Count**
   - Number of webhook retries
   - Default: 3
   - Maximum: 10

3. **Retry Interval**
   - Time between retries (minutes)
   - Default: 5
   - Minimum: 1

## Best Practices

1. **Security**
   - Store API keys in environment variables
   - Rotate API keys regularly
   - Enable signature verification
   - Use HTTPS for all endpoints

2. **Configuration**
   - Test in sandbox mode first
   - Set appropriate limits
   - Monitor webhook logs
   - Regularly backup settings

3. **Monitoring**
   - Track failed payments
   - Monitor webhook performance
   - Watch for unusual patterns
   - Regularly review logs

## Troubleshooting

### Common Issues

1. **Webhook Failures**
   - Solution: Verify webhook URL
   - Check: Network connectivity
   - Solution: Enable debug mode

2. **Payment Failures**
   - Solution: Check API keys
   - Check: Payment limits
   - Solution: Verify currency

3. **Configuration Errors**
   - Solution: Review settings
   - Check: Field formats
   - Solution: Reset to defaults

### Verification Steps

1. Test webhook:
   ```python
   frappe.get_doc("Paystack Settings").test_webhook()
   ```

2. Check logs:
   ```python
   frappe.get_all("Webhook Log", filters={"status": "Failed"})
   ```

3. Verify settings:
   ```python
   frappe.get_doc("Paystack Settings").validate()
   ```

## Security Recommendations

1. **API Key Management**
   - Never expose API keys
   - Rotate keys regularly
   - Use different keys for test/live
   - Store in environment variables

2. **Webhook Security**
   - Enable IP whitelisting
   - Use signature verification
   - Monitor failed attempts
   - Set up alerts

3. **Payment Security**
   - Set appropriate limits
   - Monitor suspicious activity
   - Use HTTPS
   - Regularly audit payments
