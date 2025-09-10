# app.garlip.com-releases
# Garlip Changelog

All notable changes to the Garlip application will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---
## [0.1.8] - 2025-08-13 - Various fixes

### Fixed
-   Microsoft SSO redirect loop on failure.
-   If copyright already exists, the modal messages are the same if either Register button is clicked.
-   Removed progress status after 3 seconds or if modal opens.
-   A number of instances where local time was being ingested instead of UTC at database level.

## [0.1.7] - 2025-07-24 - Various fixes

This release enhances the documentation and removes the crypto.js dependancy.

### Added
-   **Documentation:** Gitbook like documentation for FAQs and Token documentation.

### Fixed
-   PWA caching issues through manifest.json changes and tightening up the sw.js.
-   PWA CSS tweaks.

### Changed
-   Removed crypto.js for speed and dependancy removal.

## [0.1.6] - 2025-07-23 - Tokenization

This release adds the functionality to allocate and issue snard tokens to new and existing users.

### Added
-   **Tokens:** Tokens added to the account on subscription based on tranching.
  
## [0.1.5] - 2025-07-21 - Certificates & Proving

This release allows users to configure the certificates and reprove copyrights.

### Added
-   **Public Link:** Certificates can be viewed publically using a short url. Can be used in a QR code.
-   **Template:**
    -   Up to 10 Certificate templates can be configured and mapped against copyrights.
    -   5 custom labels and values e.g. address of lawyers
    -   square logo url link
    -   show and hide copyright information
-   **Proving:** Uploading a file will now confirm if it has been copyrighted previously and will link to a public certificate if available.
    
### Fixed
-   Enhanced security using key rotation.

## [0.1.4] - 2025-07-19 - API test area

This release allows developers to test the API for sending requests and the various responses communicated from the server.

### Added
-   **Swagger Like:** API test page. With API key can validate responses for single api calls.

## [0.1.3] - 2025-07-13 - Metered Payments and Accounting
### Added
-   **Checkout:** Stripe Integration for metered copyrighting with scaleable credit system and audit trail.
-   **Credit Gating:** API checks a user's balance and rejects requests if they have insufficient credits, providing the correct 402 Payment Required status.
-   **Statements:** Account & Billing Dashboard.
-   **Certificates:** Certificate for each copyright viewable and downloadable via print.
  
### Fixed
-   Resolved caching of dashboard after subscriptions paid.

## [0.1.2] - 2025-07-12 - Logging

### Added
-   **Centralised Logging:** Avoided use of Splunk and created own fully automated logging for faster resolution of bugs.

## [0.1.1] - 2025-07-11 - Google Drive & Blockchain Integration

This release adds the functionality to store creative content on the users own Google Drive folder.

### Added
-   **Menu Icons:** Created icon to view collateral stored on Google drive.
-   **Dashboard:** Copyrights stored on the Google drive have a clickable icon next to the datatable record.
-   **Google Sync:** Sync index in Google drive ensures app has the source of truth.
-   **Blockchain:**
    -   Bulk batch blockchain writes where it is a bit slow onchain.
    -   Blockchain proof json includes copyright meta and file type.

## [0.1.0] - 2025-07-10 - Initial Release

This is the initial beta release of the Garlip application, establishing the core infrastructure and features for copyright registration and web scraping.

### Added

-   **User Authentication:** Secure user sign-up and login using Google and Microsoft accounts.
-   **SSO Integration:** Single Sign-On flow established with session management and logging.
-   **Stripe Subscription Foundation:**
    -   Integrated Stripe library.
    -   Created database tables to store customer and subscription data.
    -   Implemented Stripe Checkout flow for new subscriptions.
    -   Added a Stripe Webhook endpoint to handle subscription status changes (`active`, `canceled`, etc.).
-   **Copyright Dashboard:**
    -   Main user interface for uploading files and registering copyrights.
    -   Features file hashing (SHA-256) on the client-side.
    -   Displays a paginated and searchable table of all registered copyrights.
-   **Dynamic Navigation Menu:**
    -   Centralized, server-driven menu system.
    -   Menu items are fetched from an API based on user role.
    -   Admins see additional links for management pages.
    -   Desktop view uses a clean, icon-based menu with tooltips.
    -   Mobile view uses a traditional responsive burger menu.
-   **Admin User Management:**
    -   Secure page for administrators to view all registered users.
    -   Admins can manually toggle a user's `isLive` (paid) status.
-   **Web Scraper Service:**
    -   A background worker that periodically checks for new content from registered sources.
    -   A robust process that fetches content, checks for changes via hashing, and stores new content as copyrights.
    -   Added table for managing URLs to be scraped.
-   **Admin Bot Management - robots.txt:**
    -   UI for viewing scrape collateral and managing scrape sources.
    -   Admins can add, update, and delete sources.
    -   Includes a "Force Run" button to manually trigger the scraping process for all active sources.
-   **Custom Error Pages:** Added user-friendly pages for 404 (Not Found), 403 (Forbidden), and 500 (Server Error).

### Changed

-   Refactored application startup to enforce clean, extensionless URLs (e.g., `/my-account` instead of `/my-account.html`).
-   Improved database connection management in background services using `IServiceScopeFactory` to prevent leaks and errors.

### Fixed

-   Resolved numerous bugs related to Dependency Injection, routing conflicts, and database constraint violations.
-   Corrected UI display issues where menu items were duplicated or had conflicting event listeners.
-   Hardened API endpoints against common errors (e.g., duplicate entries, null data).
