# Marketplace Analytics Dashboard - Design Guidelines

## Design Approach

**Selected Framework:** Material Design (adapted for data-heavy dashboard)
**Rationale:** This is a utility-focused, information-dense application requiring clear data visualization, efficient workflows, and professional presentation of complex marketplace analytics. Material Design provides robust patterns for data tables, cards, and dashboard layouts while maintaining clarity at scale.

---

## Core Design Principles

1. **Data-First Hierarchy:** Analytics and metrics take visual priority
2. **Efficiency Over Aesthetics:** Fast scanning, clear CTAs, minimal decoration
3. **Density with Breathing Room:** Pack information efficiently without cluttering
4. **Consistent Patterns:** Reusable components across all views

---

## Layout System

**Spacing Units:** Tailwind units of **2, 4, 6, and 8** for consistent rhythm
- Micro spacing (cards, buttons): `p-2`, `gap-2`
- Standard spacing (sections, grids): `p-4`, `gap-4`, `mb-6`
- Macro spacing (page sections): `p-8`, `mb-8`

**Container Strategy:**
- Main content area: `max-w-7xl mx-auto px-4 md:px-6 lg:px-8`
- Dashboard cards: Full-width within container
- Data tables: Horizontal scroll on mobile, full-width on desktop

**Grid Patterns:**
- Metrics overview: 2 columns mobile, 4 columns desktop (`grid-cols-2 lg:grid-cols-4`)
- Analytics cards: 1 column mobile, 2 columns desktop (`grid-cols-1 lg:grid-cols-2`)
- Product/order lists: Single column with responsive tables

---

## Typography

**Font Family:** Inter or Roboto via Google Fonts
- Primary: Inter (clean, modern, excellent for data)
- Fallback: system-ui, sans-serif

**Type Scale:**
- Page Headers: `text-3xl font-bold` (h1)
- Section Headers: `text-xl font-semibold` (h2)
- Card Titles: `text-lg font-medium` (h3)
- Body Text: `text-base` (default)
- Table Headers: `text-sm font-medium uppercase tracking-wide`
- Metadata/Secondary: `text-sm`
- Captions: `text-xs`

**Line Heights:**
- Headers: `leading-tight`
- Body: `leading-normal`
- Dense data: `leading-snug`

---

## Component Library

### 1. Dashboard Layout
**Structure:**
- Fixed sidebar navigation (240px width on desktop, collapsible on mobile)
- Top bar with breadcrumbs, user menu, sync status indicator
- Main content area with page header + content grid
- Sidebar includes: Dashboard, Orders, Products, Customers, Analytics sections

### 2. Navigation Components
**Sidebar:**
- Grouped navigation items with icons (use Heroicons)
- Active state: subtle background treatment
- Item spacing: `py-2 px-4`
- Icon + text layout with `gap-2`

**Top Bar:**
- Height: `h-16`
- Includes: Breadcrumb trail, search (future), notification bell, sync status badge, user avatar dropdown
- Sticky positioning for persistent access

### 3. Metric Cards (Dashboard Overview)
**Card Structure:**
- Background surface with subtle border
- Padding: `p-6`
- Layout: Icon + Metric stack
- Components: Large number display, label, trend indicator (↑ 12% vs. last period)
- Border radius: `rounded-lg`

**Grid:** 4 key metrics in top row
- Total Revenue (Faturamento)
- Orders Today
- Active Products
- Total Customers

### 4. Data Tables
**Table Design:**
- Full-width responsive tables
- Header: `bg-surface` with `text-sm font-medium uppercase`
- Row padding: `py-4 px-6`
- Alternating row backgrounds for scannability
- Hover state for rows
- Action buttons on row hover (right-aligned)
- Pagination controls at bottom

**Table Patterns:**
- Orders Table: ID, Marketplace (badge), Customer, Date, Amount, Status (badge), Actions
- Products Table: SKU, Name, Marketplace, Price, Stock, Last Sync, Actions
- Customers Table: Name, Email, Orders Count, Total Spent, Last Order Date

### 5. Analytics Widgets
**Chart Cards:**
- Padding: `p-6`
- Header with title + time range selector
- Chart area with adequate height (300-400px)
- Legend below chart
- Use placeholder for chart libraries (Chart.js or Recharts)

**Widget Types:**
- Revenue Over Time (line chart)
- Sales by Marketplace (donut chart)
- Top 10 Products (horizontal bar chart)
- Sales by State (Brazil map or bar chart)

### 6. Forms & Inputs
**Input Fields:**
- Height: `h-10` or `h-12` for touch targets
- Padding: `px-4`
- Border radius: `rounded-md`
- Labels: `text-sm font-medium mb-2`
- Helper text: `text-xs mt-1`

**Buttons:**
- Primary: Solid with `px-6 py-2` or `px-8 py-3` for major actions
- Secondary: Outlined or ghost variant
- Icon buttons: `h-10 w-10` with centered icon
- Border radius: `rounded-md`

### 7. Status Badges
**Badge Patterns:**
- Marketplace badges: Bling, Shopee, Mercado Livre, Loja Integrada (use distinct subtle background per platform)
- Order status: Pending, Processing, Shipped, Delivered, Cancelled
- Sync status: Synced, Syncing, Error
- Sizing: `px-3 py-1 text-xs font-medium rounded-full`

### 8. Empty States
**Pattern:**
- Centered icon + message
- Illustration or icon (use Heroicons outline)
- Helpful text explaining why it's empty
- Primary action button to add/sync data

### 9. Loading States
**Patterns:**
- Skeleton loaders for tables and cards
- Spinner for sync operations
- Progress bar for batch operations (72h reprocessing)

---

## Page-Specific Layouts

### Dashboard Home
**Structure:**
1. Page header with "Dashboard" title + date range selector
2. 4-column metric cards (responsive to 2 cols, then 1 col)
3. 2-column grid:
   - Left: Revenue chart (full height)
   - Right: Top 5 products list + Marketplace distribution donut
4. Recent orders table (last 10 orders)

### Orders Page
**Structure:**
1. Page header with "Orders" + filters (marketplace, status, date range)
2. Summary metrics bar (Total Orders, Pending, Processing, Completed)
3. Full-width data table with pagination
4. Bulk action controls (sync, export)

### Products Page
**Structure:**
1. Page header with "Products" + search + filters
2. Product count metrics
3. Data table with product listings
4. SKU normalization status indicator column

### Analytics Pages
**Faturamento (Billing):**
- Large revenue number display
- Time period selector
- Revenue trend chart
- Breakdown by marketplace table

**Top Produtos:**
- Horizontal bar chart (top 10)
- Accompanying data table
- Metric: Units sold + revenue generated

**Menos Vendidos (Bottom 10):**
- Similar to Top Produtos but inverted focus
- Highlight products needing attention

**Vendas por Estado (Sales by State):**
- Brazil map visualization (or sortable table as fallback)
- State-by-state breakdown table
- Top 5 states summary cards

---

## Responsive Behavior

**Breakpoints:**
- Mobile: < 768px (single column, collapsible nav)
- Tablet: 768px - 1024px (2 columns where applicable)
- Desktop: > 1024px (full multi-column layouts, fixed sidebar)

**Mobile Adaptations:**
- Sidebar becomes bottom navigation or hamburger menu
- Tables scroll horizontally with sticky first column
- Metric cards stack to single column
- Charts maintain aspect ratio, reduce height

---

## Accessibility

- All interactive elements have `min-h-[44px]` touch targets
- Form inputs have visible labels (not just placeholders)
- Tables have proper `<thead>`, `<tbody>`, semantic markup
- Skip to content link for keyboard navigation
- ARIA labels for icon-only buttons
- Focus visible states on all interactive elements

---

## Images

**No hero images required** - This is a data-focused dashboard application. Images limited to:
- Empty state illustrations (simple icons or minimal graphics)
- Marketplace logos in badges/filters (small, icon-sized)
- User avatars (top bar, customer lists)
- Product thumbnails in tables (small, 40x40px or 48x48px)

---

## Technical Specifications

**Icons:** Heroicons (outline for navigation, solid for status indicators)
**Charts:** Use Chart.js or Recharts with placeholder `<div>` comments
**Fonts:** Google Fonts CDN (Inter)
**No animations** except subtle transitions on hover/focus states (100-200ms duration)