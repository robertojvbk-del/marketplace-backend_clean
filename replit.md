# Marketplace Analytics Dashboard

## Overview

A comprehensive marketplace analytics platform that consolidates data from multiple e-commerce integrations (Bling, Shopee, Mercado Livre, and Loja Integrada) into a unified dashboard. The application provides real-time insights into orders, products, customers, and sales analytics across all connected marketplaces.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework**: React with TypeScript using Vite as the build tool

**UI Component Library**: Radix UI primitives with shadcn/ui component system styled using Tailwind CSS. The design follows Material Design principles adapted for data-heavy dashboards, emphasizing efficiency and information density.

**State Management**: TanStack Query (React Query) for server state management with optimistic updates and automatic cache invalidation. No global client state management library is used - component state and React Query suffice for this application's needs.

**Routing**: Wouter for lightweight client-side routing

**Type Safety**: Full TypeScript implementation with shared types between frontend and backend via the `@shared` module

**Design System**: 
- Uses the "new-york" shadcn/ui style variant
- Tailwind spacing units (2, 4, 6, 8) for consistent rhythm
- Inter or Roboto font family for clean data presentation
- Responsive grid patterns (2-column mobile, 4-column desktop for metrics)

### Backend Architecture

**Runtime**: Node.js with Express.js REST API

**API Pattern**: RESTful endpoints organized by resource (orders, products, customers, analytics)

**Data Access**: Repository pattern via `storage.ts` interface, abstracting database operations

**Services Layer**: Individual service modules for each marketplace integration (Bling, Shopee, Mercado Livre, Loja Integrada) that handle external API communication and data normalization

**Data Normalization**: 
- SKU normalization utility removes special characters and standardizes format across marketplaces
- Status normalization maps different marketplace status values to standard states (pending, processing, shipped, delivered, cancelled)

**Development vs Production**: Separate entry points (`index-dev.ts` with Vite dev server, `index-prod.ts` serving static files)

### Data Storage

**Database**: PostgreSQL via Neon serverless driver with WebSocket support

**ORM**: Drizzle ORM for type-safe database queries and schema management

**Schema Design**:
- `customers` - Centralized customer records with optional state/region
- `products` - Products with marketplace-specific IDs, normalized SKUs, and stock tracking
- `orders` - Orders with marketplace origin, customer reference, and status tracking
- `order_items` - Line items linking orders to products with quantities and pricing

**Schema Validation**: Drizzle-Zod for runtime validation of insert/update operations

### External Dependencies

**Marketplace APIs** (Mock implementations present, ready for real API integration):
- **Bling** - ERP/marketplace integration platform
- **Shopee** - E-commerce marketplace
- **Mercado Livre** - Latin American marketplace
- **Loja Integrada** - Brazilian e-commerce platform

**Database**: 
- Neon PostgreSQL (serverless)
- Connection pooling via `@neondatabase/serverless`

**Build Tools**:
- Vite for frontend bundling
- esbuild for backend production builds
- TypeScript compiler for type checking

**Development Tools** (Replit-specific):
- `@replit/vite-plugin-runtime-error-modal` - Development error overlay
- `@replit/vite-plugin-cartographer` - Development mapping
- `@replit/vite-plugin-dev-banner` - Development banner

**Session Management**: `connect-pg-simple` for PostgreSQL-backed sessions (infrastructure present but not fully implemented)

**Utilities**:
- `date-fns` for date manipulation
- `zod` for validation schemas
- `nanoid` for unique ID generation

### Key Architectural Decisions

**Monorepo Structure**: Client, server, and shared code in a single repository with path aliases (`@/`, `@shared/`, `@assets/`) for clean imports

**Type Sharing**: Database schema types are generated once in `shared/schema.ts` and consumed by both frontend and backend, ensuring type safety across the stack

**Mock Data Strategy**: Each marketplace service contains mock data arrays, allowing development and testing without live API credentials. Production implementation would replace these with actual API calls.

**Analytics Endpoints**: Dedicated analytics routes provide pre-aggregated data for dashboard metrics, revenue analysis, top/low-performing products, and geographic sales distribution

**Sync Architecture**: Mutation-based sync system that invalidates all related queries after data refresh, ensuring UI consistency. The sync endpoint is designed to pull data from all marketplace APIs in a single operation.

**Error Handling**: Centralized logging utility with structured log entries including timestamps, levels, and optional data payloads

**Validation Strategy**: Monetary values use Zod coercion with non-negative number validation to prevent invalid data persistence