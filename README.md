# LUXE. - Headless E-Commerce Platform

LUXE. is a modern, high-performance headless e-commerce application designed for luxury fashion brands. It utilizes a decoupled architecture where React handles the frontend experience, WordPress (WooCommerce) manages the product inventory, and Firebase handles user authentication and customer data.

# Architecture Overview     

This project follows a Headless Commerce architecture:

-   Frontend (The Head): Built with React (Vite) and Tailwind CSS. It communicates with the backend via APIs.
-   Product Backend (The Body): WordPress + WooCommerce running on a local or cloud server (PHP/MySQL). It provides product data via the REST API.
-   User Backend (The Identity): Firebase Authentication & Firestore. It manages user logins, profiles, and order history records.

##   Features

-   Customer Features
    -   Modern SPA Interface: Fast, app-like browsing experience without page reloads.
    -   User Accounts: Registration and login via Firebase Auth.
    -   My Account Dashboard: Manage profile details, saved addresses, and view order history.
    -   Shopping Cart: Persistent cart state using LocalStorage.
    -   Checkout: Integrated order placement system that syncs with WooCommerce.
-   Admin Features
    -   CMS Dashboard: Manage site content (Hero banners, text, contact info) directly from the admin panel.
    -   Product Management: Add, edit, and delete products via the WordPress backend.
    -   Store Settings: Configure payment gateways, currency, and social media links.
    -   Security: Role-based access control (RBAC) ensuring only admins can access sensitive settings.

#   Tech Stack
-   Frontend: React.js, Vite, Tailwind CSS, Lucide React (Icons), React Router DOM, Axios.
-   Backend (CMS): WordPress, WooCommerce.
-   Backend (Auth/DB): Google Firebase (Auth, Firestore).
-   Local Server Environment: XAMPP (Apache/MySQL).

#   Prerequisites

Before you begin, ensure you have the following installed:

-   Node.js (v16 or higher) & npm.
-   XAMPP (or MAMP/WAMP) for running WordPress locally.
-   Git.
-   A Firebase Account (Free tier is sufficient).

#   Installation Guide

## Phase 1: Backend Setup (WordPress)

-   Install WordPress:
    -   Download WordPress and extract it to your XAMPP htdocs folder (e.g., C:\xampp\htdocs\luxe-backend).
    -   Create a database named luxe_db via phpMyAdmin.
    -   Run the WordPress installation wizard in your browser.

## Configure WooCommerce:
-   Install and activate the WooCommerce plugin.
-   Go to WooCommerce > Settings > Advanced > REST API.
-   Click Add Key.
-   Set Permissions to Read/Write.
-   Copy the Consumer Key and Consumer Secret. You will need these later.
-   Enable CORS (Critical):
    -   Open wp-config.php in your WordPress root folder.
    -   Add the following lines at the top to allow your React app to fetch data:
        header("Access-Control-Allow-Origin: *");
        header("Access-Control-Allow-Methods: GET, POST, OPTIONS, PUT, DELETE");
        header("Access-Control-Allow-Headers: Origin, X-Requested-With, Content-Type, Accept, Authorization");


## Permalinks:
-   Go to Settings > Permalinks in WordPress Admin.
    -   Select Post name. Click Save Changes.

## Phase 2: Frontend Setup (React)
-   Clone the Repository:
    -   git clone [https://github.com/your-username/luxe-fashion.git](https://github.com/your-username/luxe-fashion.git)
    -   cd luxe-fashion

-   Install Dependencies:
    -   npm install

-   Environment Variables:
    -   Create a file named .env in the root directory.
    -   Add your API keys as shown below:

# --- WORDPRESS CONFIG ---

# The URL to your local or live WordPress site

VITE_WORDPRESS_URL=http://localhost:8080/luxe-backend

# Keys generated in WooCommerce Settings

VITE_WC_CONSUMER_KEY=ck_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
VITE_WC_CONSUMER_SECRET=cs_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

# --- FIREBASE CONFIG ---

# Keys from Firebase Project Settings

VITE_API_KEY=AIzaSy...
VITE_AUTH_DOMAIN=luxe-fashion.firebaseapp.com
VITE_PROJECT_ID=luxe-fashion
VITE_STORAGE_BUCKET=luxe-fashion.appspot.com
VITE_MESSAGING_SENDER_ID=123456789
VITE_APP_ID=1:123456789:web:abcdef


## Run the App:
-   npm run dev

The app should now be running at http://localhost:5173.

## 🔐 Admin Access & Security

How to become an Admin:
-   Sign up as a normal user on the /login page.
-   Go to your Firebase Console > Firestore Database > users collection.
-   Find your user document.
-   Change the role field from "customer" to "admin".
-   Refresh the site. You can now access /admin.

## Security Note:
-   The .env file containing your secret keys is ignored by Git (.gitignore) to prevent leaking credentials. Never commit this file.

## 📂 Project Structure

src/
├── api/              # API connectors (WooCommerce bridge)
├── assets/           # Static images and fonts
├── components/       # Reusable UI components (Navbar, Footer, ProductCard)
├── context/          # Global State (ShopContext)
├── layouts/          # Page layouts (AdminLayout)
├── pages/            # Main views
│   ├── admin/        # Admin Dashboard pages (Settings, Analytics, etc.)
│   └── ...           # Public pages (Home, Shop, Account)
├── firebase.js       # Firebase initialization
├── App.jsx           # Main Router configuration
└── main.jsx          # Entry point

## 🤝 Contribution

-   Fork the repository.
-   Create a feature branch (git checkout -b feature/AmazingFeature).
-   Commit your changes (git commit -m 'Add some AmazingFeature').
-   Push to the branch (git push origin feature/AmazingFeature).
-   Open a Pull Request.

## 📄 License

Distributed under the MIT License. See LICENSE for more information.
