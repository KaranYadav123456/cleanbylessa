# Clean by Lesa LLC

Website with customer accounts, one booking/quote page, a private admin panel, local SQLite storage, required space photos, and Zelle-only payment requests. It does not use Supabase or an external payment processor.

## Start on Windows

1. Install Node.js 22 or newer from [nodejs.org](https://nodejs.org) if it is not installed.
2. Double-click **Start Website.bat**.
3. Use the address `http://localhost:3101` that opens. Keep the **Clean by Lesa Server** window open. Do not use a `C:\...` file path for account sign-in or bookings.
4. Open `http://localhost:3101/admin.html`. On the first run, the server window prints the admin email and temporary password. Save those and change the password in the admin panel.

Customer accounts, bookings, and uploaded images are saved under `data/` on this computer. There are no npm packages to install, database accounts to link, or card-payment keys to enter.

## Prepare a deployment bundle

Run `npm run build` from the project folder. This creates `dist/` with the site pages, assets, `server.js`, and `package.json`. It does not copy the local database, session key, or customer uploads. Deploy the contents of `dist/` to a Node.js host and use `npm start` as its start command. Read `dist/README.md` for the required Node version and persistent storage settings.

## Customer quote and payment steps

1. The customer creates an account at `http://localhost:3101/signup.html` or signs in at `http://localhost:3101/login.html`.
2. On `account.html`, they select their service, enter the address and preferred schedule, and upload at least one photo of the space. Their request appears in the admin panel as **new / quote pending**.
3. Lesa reviews the photos, enters the price and her Zelle-enrolled email or US phone in the admin panel, then saves the request as **quote ready / payment requested**.
4. The customer sees the amount and Zelle recipient in their account, pays from their bank app, and uploads a screenshot of the Zelle confirmation.
5. Lesa checks the payment in her bank and marks it **confirmed**. Only then does the customer see that payment is confirmed and that Lesa will contact them to arrange the cleaning.

Space photos and payment screenshots must be JPG, PNG, WebP, or GIF, up to 5 MB each. Booking requests allow up to five photos and 15 MB total. Uploaded files are stored privately; customers can view their own files and the admin can view all of them.

Zelle does not automatically notify this website when money arrives, so Lesa must verify each transfer in her bank before marking it confirmed. Confirm the business recipient in your bank before entering it. Zelle is the only payment option on the site.

## Admin panel

Go directly to `http://localhost:3101/admin.html` and sign in with the admin credentials printed the first time the server starts. This is a separate login; no customer login is needed first. The panel shows each account booking, required space photos, any payment screenshot, and controls for the price, Zelle recipient, status, and payment confirmation.

## Internet hosting

`Start Website.bat` runs the app on this computer. To accept customer bookings over the internet, the Node app must be hosted online with HTTPS and persistent disk storage. Keep the `data/` folder on persistent storage so accounts, booking details, and uploaded images survive restarts.

## Pages

- `index.html` — Home
- `residential.html` — Residential packages and add-ons
- `commercial.html` — Commercial services
- `how-it-works.html` — New-client information
- `about.html` — Brand story
- `gallery.html` — Gallery
- `faq.html` — Frequently asked questions
- `login.html` — Customer sign in
- `signup.html` — Customer account creation
- `auth.html` — Compatibility redirect to sign in
- `account.html` — The single customer booking, photo upload, quote, and Zelle status page
- `admin.html` — Admin login, booking dashboard, and password change

## Customize

- Edit palette and typography in `css/style.css`.
- Update page content and photos in the HTML files.
- SQLite tables and private uploads are created automatically inside `data/`.
- `ADMIN_EMAIL` and `ADMIN_PASSWORD` can be set before the first run. Keep admin credentials private.
