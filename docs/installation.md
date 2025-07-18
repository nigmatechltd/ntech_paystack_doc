# Installation & Setup

## Prerequisites

Before installing Ntech Paystack, ensure you have:

1. A running ERPNext instance
2. Access to the Bench command-line tool
3. A Paystack account with API credentials
4. Python 3.8 or higher
5. Required dependencies installed:
   ```bash
   pip install requests
   pip install frappe
   ```

## Installation Steps

1. Add the Ntech Paystack repository to your Bench:
   ```bash
   bench get-app https://github.com/nigmatechltd/ntech_paystack
   ```

2. Install the app:
   ```bash
   bench --site [your-site-name] install-app ntech_paystack
   ```

3. Update your site:
   ```bash
   bench --site [your-site-name] migrate
   ```

## Configuration

### Paystack Settings

1. Go to: **Settings > Paystack Settings**
2. Configure the following fields:
   - **Payment Gateway Title**: Display name for the payment gateway
   - **API Key**: Your Paystack API key
   - **Secret Key**: Your Paystack secret key
   - **Mode**: Choose between Test and Live mode
   - **Enabled**: Enable/disable the payment gateway

### User Roles

1. Create two user roles:
   - **Admin User**: Full access to configure Paystack settings
   - **Payments User**: Limited access to generate payments only

2. Assign these roles via Role Permission Manager:
   - Go to: **Settings > Role Permission Manager**
   - Select the appropriate role
   - Assign the necessary permissions

## Post-Installation Steps

1. Verify installation:
   ```bash
   bench --site [your-site-name] list-apps
   ```

2. Check webhook endpoints:
   ```bash
   bench --site [your-site-name] get-webhook-endpoints
   ```

3. Test the integration:
   - Create a test payment request
   - Verify webhook notifications
   - Check payment entry creation

## Troubleshooting Installation

### Common Issues

1. **Missing Dependencies**
   - Solution: Install missing packages using pip

2. **Permission Errors**
   - Solution: Check file permissions and ownership

3. **Configuration Errors**
   - Solution: Verify Paystack API credentials

### Verification Steps

1. Check logs:
   ```bash
   bench --site [your-site-name] logs
   ```

2. Verify database migrations:
   ```bash
   bench --site [your-site-name] migrate-status
   ```

## Best Practices

1. Always test in sandbox mode first
2. Keep API keys secure
3. Regularly backup your database
4. Monitor webhook logs
5. Test payment flows thoroughly

## Security Recommendations

1. Use HTTPS for all payment-related endpoints
2. Keep API keys in environment variables
3. Regularly rotate API keys
4. Monitor failed payment attempts
5. Implement rate limiting for webhooks
