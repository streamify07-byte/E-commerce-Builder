# MegaMart - E-Commerce Marketplace

## Overview
A complete e-commerce marketplace platform similar to Daraz.pk, where users can create stores to sell products, customers can browse and purchase items, and the platform owner has full administrative control.

## Architecture
- **Frontend**: React + Vite + TailwindCSS + Shadcn UI components
- **Backend**: Express.js with TypeScript
- **Database**: PostgreSQL with Drizzle ORM
- **Auth**: Replit Auth (OpenID Connect)

## Key Features
- Landing page for logged-out users
- Home page with featured products, categories, and product listings
- Product detail pages with add-to-cart functionality
- Shopping cart with quantity management
- Checkout with cash on delivery
- Order tracking with expandable order items (shows products inside each order)
- **Seller marketplace**: Users can create stores, manage products, and view orders for their products
- **Admin panel**: Role-based admin with full control over products, orders, categories, and stores
- Category-based browsing and search
- Public store pages (browse individual store inventories)
- Dark/light theme toggle
- Request validation using Zod schemas

## Authorization Model
- **Users**: isAdmin field on user table for admin role
- **Sellers**: Store ownership checked on seller product CRUD routes
- **Admin**: isAdmin middleware protects all /api/admin/* routes
- **Become Admin**: /api/admin/make-me-admin endpoint for first user setup

## Project Structure
- `client/src/pages/` - All page components (landing, home, product-detail, cart, checkout, orders, search, category, admin, my-store, store)
- `client/src/components/` - Shared components (navbar, footer, product-card, theme-provider)
- `server/routes.ts` - All API endpoints with auth/admin middleware
- `server/storage.ts` - Database CRUD operations (IStorage interface)
- `server/seed.ts` - Seed data for initial products and categories
- `server/db.ts` - Database connection
- `shared/schema.ts` - Drizzle schema definitions (categories, stores, products, cart, orders)
- `shared/models/auth.ts` - Auth-related schemas (users with isAdmin, sessions)

## API Routes
- `GET /api/categories` - List all categories
- `GET /api/products` - List active products
- `GET /api/products/featured` - Featured products
- `GET /api/products/slug/:slug` - Product by slug
- `GET /api/products/category/:slug` - Products by category
- `GET /api/products/search/:query` - Search products
- `GET /api/stores` - List active stores (public)
- `GET /api/my-store` - Get current user's stores (auth required)
- `POST /api/stores` - Create a store (auth required)
- `GET /api/stores/:slug` - Store details
- `GET /api/stores/:storeId/products` - Store products
- `POST/PATCH/DELETE /api/seller/products` - Seller product management (ownership validated)
- `GET /api/seller/orders` - Orders containing seller's products
- `GET/POST/PATCH/DELETE /api/cart` - Cart operations (auth required)
- `GET/POST /api/orders` - Order operations (auth required)
- `GET /api/orders/:id/items` - Order items with product details
- `GET/POST/PATCH/DELETE /api/admin/products` - Admin product management (admin only)
- `GET/PATCH /api/admin/orders` - Admin order management (admin only)
- `POST/PATCH/DELETE /api/admin/categories` - Admin category management (admin only)
- `GET/PATCH /api/admin/stores` - Admin store management with activate/deactivate (admin only)
- `POST /api/admin/make-me-admin` - Become admin (auth required)
- `GET /api/admin/check` - Check admin status (auth required)

## Database Tables
- users (with isAdmin), sessions (auth)
- stores (name, slug, description, ownerId, logo, active)
- categories, products (with optional storeId), cart_items, orders, order_items

## Recent Changes (Feb 20, 2026)
- Added order items display in orders page (expandable to show products in each order)
- Added admin category management (add, edit, delete categories)
- Added admin store management (view all stores, activate/deactivate)
- Added seller orders view (tab in my-store to see orders containing their products)
- Added public store page (/store/:slug) to browse individual store inventories
- Fixed footer "Sell on MegaMart" link to point to /my-store
- Generated placeholder image for products without images
