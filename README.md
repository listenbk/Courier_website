# Courier_website
Admin_login and User form

A PHP courier-services website with a pickup form and MySQL-backed admin dashboard.
A responsive PHP website for a courier business. Visitors can browse courier services and submit a pickup request; administrators can sign in to review requests and create additional admin accounts.

## Features

- Responsive public pages for the company, its services, and contact details
- Pickup-request form with server-side validation
- Automatically generated booking reference numbers
- MySQL database storage for bookings and administrator accounts
- Password-hashed administrator login with session protection
- Admin dashboard for reviewing submitted pickup requests
- Admin-account management and a disabled-by-default recovery tool

## Technology

- PHP 8+
- MySQL / MariaDB
- PDO MySQL extension
- HTML, CSS, and vanilla JavaScript

## Run locally

1. Import `sql_code.sql` in phpMyAdmin.
2. Set your MySQL credentials in `includes/config.php`.
3. From this folder, run `php -S localhost:8000`, then open `http://localhost:8000`.
1. Install PHP 8+ and MySQL or MariaDB. XAMPP, WAMP, or Laragon are suitable local environments.
2. Create the database and tables by importing [`sql_code.sql`](msql_code.sql) in phpMyAdmin or from the MySQL command line.
3. Update the database settings in [`includes/config.php`](includes/config.php):

## Admin credentials
   ```php
   const DB_HOST = 'localhost';
   const DB_NAME = 'Add_your_db_name';
   const DB_USER = 'root';
   const DB_PASSWORD = '';
   ```

## Administrator access

After signing in, open `admin/manage-admins.php` to create a new, strong administrator account. Test it, then remove the default `admin` account in phpMyAdmin. The PHP installation must have the PDO MySQL extension enabled.
The SQL setup creates an initial administrator account:

If the default login was imported incorrectly, import `reset_default_admin.sql` in phpMyAdmin. It resets only the `admin` account back to `admin` / `password`.
| Field | Initial value |
| --- | --- |
| Username | `admin` |
| Password | `password` |
| Admin login | `/admin/login.php` |

## Booking flow

1. A visitor completes the form on `booking.php`.
2. `submit-booking.php` validates required fields and the email address.
3. The application generates a reference such as `MMC-260721-A1B2C3`.
4. The request is saved to the `bookings` table with a default **Pending** status.
5. An authenticated administrator views the request from `admin/dashboard.php`.

## Before deploying

- Use a strong, non-default MySQL password and never commit production credentials.
- Create a new administrator and remove the included `admin` account.
- Keep `ADMIN_RECOVERY_ENABLED` set to `false`.
- Serve the site over HTTPS.
- Restrict database access to the application server.
