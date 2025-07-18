# User Roles & Permissions

## Overview

Ntech Paystack implements a role-based access control system with two primary user types:

1. **Admin User**
   - Full access to configure Paystack settings
   - Can generate all types of payment flows
   - Access to webhook management
   - View all payment requests

2. **Payments User**
   - Limited access to generate payments only
   - Can view their own payment requests
   - No access to settings or configuration

## Role Configuration

### Admin User Role

Permissions:
- **Paystack Settings**: Read, Write, Create, Delete
- **Payment Request**: Read, Write, Create
- **Payment Entry**: Read
- **Webhook Log**: Read
- **System Settings**: Read, Write

### Payments User Role

Permissions:
- **Payment Request**: Read, Write, Create (own records only)
- **Payment Entry**: Read (own records only)
- **Webhook Log**: Read (own records only)

## Role Assignment

1. Go to: **Settings > Role Permission Manager**
2. Create or edit roles:
   ```python
   # Example role creation
   frappe.get_doc({
       "doctype": "Role",
       "role_name": "Paystack Admin",
       "desk_access": 1
   }).insert()
   ```

3. Assign permissions:
   ```python
   # Example permission assignment
   frappe.get_doc({
       "doctype": "DocPerm",
       "role": "Paystack Admin",
       "parent": "Paystack Settings",
       "read": 1,
       "write": 1,
       "create": 1,
       "delete": 1
   }).insert()
   ```

## Role-Based Features

### Admin User Features

1. **Configuration Management**
   - Set up Paystack API keys
   - Configure webhook settings
   - Manage IP whitelisting
   - Set up payment gateway options

2. **System Monitoring**
   - View all payment requests
   - Monitor webhook logs
   - Track payment statuses
   - View payment history

3. **Security Management**
   - Configure IP restrictions
   - Set up signature verification
   - Manage user access levels
   - Monitor failed attempts

### Payments User Features

1. **Payment Generation**
   - Create payment requests
   - View own payment status
   - Generate payment links
   - Track own payment history

2. **Payment Management**
   - Cancel own payment requests
   - View payment details
   - Track payment status
   - Get payment receipts

## Best Practices

1. **Role Assignment**
   - Assign Admin role only to trusted users
   - Regularly review user permissions
   - Document access levels
   - Monitor user activity

2. **Security**
   - Never share API keys
   - Use strong passwords
   - Regularly audit permissions
   - Monitor failed login attempts

3. **Monitoring**
   - Track payment request patterns
   - Monitor webhook performance
   - Watch for unusual activity
   - Regularly review logs

## Troubleshooting

### Common Issues

1. **Access Denied**
   - Solution: Verify role permissions
   - Check: Role Permission Manager

2. **Missing Features**
   - Solution: Review role configuration
   - Check: User permissions

3. **Security Alerts**
   - Solution: Review access logs
   - Check: User activity history

### Verification Steps

1. Check user roles:
   ```python
   frappe.get_roles()
   ```

2. Verify permissions:
   ```python
   frappe.has_permission("doctype", "read")
   ```

3. Monitor activity:
   ```python
   frappe.get_all("Activity Log", filters={"user": "user@example.com"})
   ```
