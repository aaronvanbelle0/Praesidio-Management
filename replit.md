# Praesidio Management Group - Luxury Home Concierge Platform

## Overview

Praesidio Management Group is a luxury property management platform designed to connect high-end homeowners with vetted professionals for comprehensive estate care. The application features a marketing-focused landing page with service tier presentation, inquiry intake forms, a comprehensive About page, and a sophisticated design system inspired by luxury hospitality brands like Airbnb Luxe and Stripe.

**Core Purpose**: Provide a trusted, convenient platform for luxury homeowners to access premium home management services through a tiered subscription model (Executive Management, Estate Concierge).

**Trust & Convenience Features**:
- 24/7 Response Time Money-Back Guarantee prominently displayed
- Service coverage from King County to Whatcom County in Pacific Northwest
- Security & Privacy statement with bank-level encryption and background checks
- Comprehensive About page showcasing company mission, values, and service philosophy

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework Stack**:
- **React 18** with TypeScript for type-safe component development
- **Vite** as the build tool and development server
- **Wouter** for lightweight client-side routing
- **TanStack Query (React Query)** for server state management and API calls

**UI Component System**:
- **Shadcn UI** component library with Radix UI primitives for accessible, headless components
- **Tailwind CSS** for utility-first styling with custom design tokens
- **Custom CSS variables** for theming (light/dark mode support)
- **Typography**: Playfair Display (serif) for headings, Inter (sans-serif) for body text

**Design System**:
- Reference-based luxury aesthetic (documented in `design_guidelines.md`)
- Color palette centered on deep charcoal, refined slate blue, and generous whitespace
- Consistent spacing system using Tailwind units (4, 6, 8, 12, 16, 20, 24)
- Responsive breakpoints with mobile-first approach

**State Management**:
- React Query for async data fetching and caching
- React hooks for local component state
- Form state managed via React Hook Form with Zod validation

### Backend Architecture

**Server Framework**:
- **Express.js** running on Node.js with ESM modules
- **TypeScript** for type safety across the stack
- RESTful API design pattern

**API Endpoints**:
- `POST /api/inquiries` - Create new service inquiry (automatically sends email notification)
- `GET /api/inquiries` - Retrieve all inquiries

**Email Notifications**:
- **Service**: Zoho Mail SMTP (smtp.zoho.com:587)
- **Email address**: aaron@praesidiomanagement.com
- **Implementation**: server/email.ts using nodemailer
- **Trigger**: Automatically sent after each inquiry form submission
- **Credentials**: Stored in environment variables (ZOHO_EMAIL, ZOHO_PASSWORD)
- **Email content**: HTML and plain text with all inquiry details
- **Error handling**: Asynchronous delivery with fallback logging

**Request/Response Flow**:
- JSON request bodies with validation via Zod schemas
- Inquiry saved to database
- Email notification sent asynchronously (non-blocking)
- Standardized error handling middleware
- Response logging for API routes (truncated to 80 characters)

**Build Configuration**:
- Separate client (Vite) and server (esbuild) build processes
- Production server runs compiled ESM bundle from `dist/`
- Development mode uses Vite middleware for HMR

### Data Layer

**Database**:
- **PostgreSQL** via Neon serverless platform
- **Drizzle ORM** for type-safe database operations
- WebSocket connection pooling for serverless environments

**Schema Design** (`shared/schema.ts`):
- `inquiries` table stores customer intake forms
  - UUID primary keys (auto-generated)
  - Contact information (firstName, lastName, email, phone)
  - Property details (propertyAddress, propertyType)
  - Service preferences (serviceInterest, additionalDetails)
  - Timestamp tracking (createdAt)

**Data Access Pattern**:
- Repository pattern via `DbStorage` class in `server/storage.ts`
- Interface-based abstraction (`IStorage`) for potential future storage implementations
- Zod schemas for runtime validation matching database schema

**Database Configuration**:
- Connection string via `DATABASE_URL` environment variable
- Drizzle Kit for schema migrations (output to `./migrations`)
- Schema push capability for development (`npm run db:push`)

### Application Pages

**Homepage** (`/`):
- Hero section with 24/7 money-back guarantee messaging
- Service tier comparison (Executive Management $8k/year, Estate Concierge $35k/year)
- Service Guarantees section (24/7 response, quality workmanship, damage protection)
- Contractor Vetting Process section (background checks, licensing, performance reviews)
- Service Area coverage display (King to Whatcom County)
- How It Works process flow
- FAQ accordion
- Inquiry intake form

**About Page** (`/about`):
- Company mission and founding story
- Core values section (Trust & Integrity, White-Glove Service, 24/7 Availability, Excellence Standards)
- Why Choose Praesidio differentiators (6 key advantages)
- Service philosophy (Prevention Over Reaction, Relationships Built on Trust, Clear Communication)
- Pacific Northwest service area details
- Call-to-action section linking back to service tiers and contact form

**Plan Details Pages** (`/plans/:tier`):
- Executive Management (`/plans/executive`, also supports `/plans/premium` for backward compatibility)
  - $8,000/year
  - Full maintenance coordination, vendor management, routine inspections
  - Quarterly complimentary services (deep cleaning, window washing, landscape refresh, etc.)
  - Ideal for primary/secondary homeowners seeking year-round oversight
- Estate Concierge (`/plans/estate`)
  - $35,000/year
  - All Executive Management services plus 24/7 priority response
  - Dedicated client manager for personalized oversight
  - Six annual complimentary premium services
  - Multi-residence coordination and comprehensive estate management

### Project Structure

```
├── client/               # Frontend application
│   ├── src/
│   │   ├── components/  # React components (UI library & custom)
│   │   ├── pages/       # Route components (Home, About, PlanDetails)
│   │   ├── hooks/       # Custom React hooks
│   │   ├── lib/         # Utilities (query client, helpers)
│   │   └── index.css    # Global styles & CSS variables
│   └── index.html       # HTML entry point
├── server/              # Backend application
│   ├── index.ts         # Express server setup
│   ├── routes.ts        # API route definitions
│   ├── storage.ts       # Data access layer
│   └── vite.ts          # Vite dev server integration
├── shared/              # Shared types & schemas
│   └── schema.ts        # Database & validation schemas
├── db/                  # Database configuration
│   └── index.ts         # Drizzle client setup
└── migrations/          # Database migrations
```

### Form Handling

**Intake Form Architecture**:
- React Hook Form for form state management
- Zod resolver for schema validation
- TanStack Query mutation for async submission
- Toast notifications for user feedback
- Form reset on successful submission

**Validation Schema**:
- Shared between client and server via `@shared/schema`
- Runtime type checking with Zod
- Database schema derived from Drizzle ORM types

## External Dependencies

### Third-Party Services

**Database Hosting**:
- **Neon** - Serverless PostgreSQL platform
- WebSocket-based connection for serverless compatibility
- Requires `DATABASE_URL` environment variable

**Development Tools**:
- **Replit** specific plugins:
  - Runtime error modal overlay
  - Cartographer for code navigation
  - Development banner

### Key NPM Packages

**UI & Styling**:
- `@radix-ui/*` - Accessible component primitives (accordion, dialog, dropdown, etc.)
- `tailwindcss` - Utility-first CSS framework
- `class-variance-authority` - Component variant management
- `lucide-react` - Icon library

**Data & Forms**:
- `@tanstack/react-query` - Async state management
- `react-hook-form` - Form state management
- `zod` - Schema validation
- `@hookform/resolvers` - Form validation integration

**Database**:
- `drizzle-orm` - TypeScript ORM
- `drizzle-zod` - Zod schema generation
- `@neondatabase/serverless` - Neon database driver
- `ws` - WebSocket client for database connections

**Router & Navigation**:
- `wouter` - Lightweight routing library
- `react-router` is NOT used

**Server**:
- `express` - Web framework
- `connect-pg-simple` - PostgreSQL session store (installed but not actively used)

### Asset Management

**Static Assets**:
- Logo and property images stored in `attached_assets/`
- Vite alias `@assets` for asset imports
- Images optimized for web delivery

**Font Loading**:
- Google Fonts (Playfair Display, Inter)
- Preconnect hints for performance
- Additional fonts loaded but may not be actively used (DM Sans, Fira Code, Geist Mono, Architects Daughter)