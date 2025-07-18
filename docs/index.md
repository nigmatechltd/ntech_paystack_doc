# Ntech Paystack Integration for ERPNext

## Introduction

Ntech Paystack is a robust payment integration module that seamlessly connects Paystack's payment gateway with your ERPNext system. This module enables businesses to accept secure online payments through Paystack while maintaining full integration with ERPNext's financial workflows.

## Key Features

- **Secure Payment Processing**: Fully integrated Paystack payment gateway
- **Real-time Webhooks**: Automatic payment status updates via secure webhooks
- **Role-based Access Control**: Admin and Payments User roles with appropriate permissions
- **Payment Request Management**: Generate and track payment requests
- **Automatic Payment Entry Creation**: Automatic creation of Payment Entries upon successful payments
- **Signature Verification**: Secure HMAC SHA512 signature verification for webhook requests
- **IP Whitelisting**: Optional IP restriction for webhook requests

## Technical Overview

Ntech Paystack consists of several key components:

1. **Paystack Settings**: Configuration for Paystack API keys and settings
2. **Webhook Handler**: Secure processing of Paystack webhook notifications
3. **Payment Request Flow**: Integration with ERPNext's payment request system
4. **Payment Entry Integration**: Automatic creation of payment entries
5. **Security Features**: Signature verification and IP whitelisting

## Getting Started

To get started with Ntech Paystack:

1. Install the module using Bench
2. Configure Paystack settings
3. Set up user roles and permissions
4. Generate your first payment request

## Documentation Structure

This documentation is organized into several sections:

- **Installation & Setup**: How to install and configure the module
- **User Roles & Permissions**: Understanding and managing user access
- **Paystack Settings**: Configuring payment gateway settings
- **Payment Request Flow**: Understanding the payment process
- **API Reference**: Technical documentation for developers
- **Developer Guide**: Implementation details and customization options
- **Troubleshooting**: Common issues and solutions
- **Changelog**: Version history and updates

## Support

For support and questions, please contact:
- Email: info@nigmatech.net
- GitHub: https://github.com/nigmatechltd

---

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.
