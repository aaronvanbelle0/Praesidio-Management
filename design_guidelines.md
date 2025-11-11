# Luxury Home Concierge Design Guidelines

## Design Approach: Reference-Based (Luxury Service Platform)

**Primary Inspirations**: Airbnb Luxe (trust & elegance) + Stripe (clean sophistication) + luxury hospitality brands

**Core Principles**: 
- Timeless elegance over trendy aesthetics
- Trust through professional polish and restraint
- Clarity in service tier presentation
- Luxury through whitespace and typography

## Color Palette

**Light Mode:**
- Primary: 240 8% 15% (Deep charcoal - sophistication)
- Background: 0 0% 100% (Pure white)
- Accent: 215 25% 45% (Refined slate blue - trust)
- Success: 150 40% 45% (Muted emerald - premium)
- Borders: 240 5% 90% (Subtle gray)

**Dark Mode:**
- Primary: 0 0% 98% (Off-white text)
- Background: 240 8% 8% (Rich charcoal)
- Accent: 215 30% 60% (Lighter slate blue)
- Card backgrounds: 240 6% 12%

## Typography

**Fonts via Google Fonts:**
- Headings: 'Playfair Display' (serif - luxury, trust)
- Body: 'Inter' (sans-serif - clarity, modern)

**Scale:**
- Hero headline: text-5xl md:text-7xl, font-serif
- Section headings: text-3xl md:text-5xl, font-serif
- Tier titles: text-2xl md:text-3xl, font-serif
- Body: text-base md:text-lg
- Fine print: text-sm

## Layout System

**Spacing Primitives**: Tailwind units of 4, 6, 8, 12, 16, 20, 24 for consistent rhythm

**Container Strategy:**
- Hero: Full-width with max-w-7xl inner content
- Content sections: max-w-6xl mx-auto
- Pricing cards: max-w-5xl for focused comparison

**Section Padding**: py-16 md:py-24 for generous breathing room

## Component Library

### Hero Section
- Large, sophisticated property image (modern luxury home exterior/interior)
- Overlay with gradient (from black/60% to transparent)
- Centered headline + subheadline emphasizing trust/convenience
- Single primary CTA button (variant="default" with blurred background if over image)
- Trust indicators below: "24/7 Response • Vetted Professionals • [X] Homes Managed"

### Pricing Tiers Section
- Three-column grid on desktop (grid-cols-1 md:grid-cols-3)
- Premium tier: Elevated with border-accent, "Most Popular" badge
- Each card: Clean white background, subtle shadow, hover lift effect
- Card structure: Tier name (serif) → Price (large, bold) → Feature list (checkmarks) → CTA button
- 15-20px spacing between features for scanability

### Trust Indicators Section
- Two-column layout: Image left (tradesman at work, professional setting) + content right
- Key stats in grid (2x2): "500+ Vetted Professionals", "24/7 Availability", "98% Satisfaction", "50+ Properties"
- Large numbers (text-4xl) with descriptive labels

### How It Works / Process Section
- Three-step horizontal flow with connecting lines
- Icons from Heroicons (shield-check for vetting, clock for 24/7, wrench for service)
- Step numbers in accent color circles

### Footer
- Three-column layout: Brand + Quick Links + Contact
- Newsletter signup with inline form
- Trust badges: "Licensed & Insured", "Background Checked"
- Social proof: "Serving [City] since [Year]"

## Images

**Hero Image**: Wide-angle luxury home exterior at dusk/golden hour with warm lighting (sophisticated, aspirational)

**Trust Section Image**: Professional tradesman in branded uniform working on high-end property detail (builds credibility)

**Optional Background**: Subtle texture/pattern on pricing section background for depth (very subtle, 2-3% opacity)

## Key Interactions

- Pricing cards: Subtle scale on hover (scale-105)
- CTA buttons: Use default shadcn states (no custom hover needed)
- Smooth scroll to pricing section from hero CTA
- Tier comparison: Highlight matching features across tiers on hover

## Accessibility

- WCAG AAA contrast ratios (especially accent on dark backgrounds)
- Pricing information in semantic table structure
- Focus states: 2px accent color ring with offset
- Dark mode: Maintain all hierarchy and readability

## Layout Sections (In Order)

1. **Navigation**: Sticky header, logo left, links right, "Get Started" CTA
2. **Hero**: Full-viewport height with image, centered messaging
3. **Value Proposition**: Three-column benefits (Trust, Convenience, Quality)
4. **Pricing Tiers**: The three plans as provided
5. **How It Works**: 3-step process
6. **Trust/Social Proof**: Stats + tradesman image
7. **FAQ**: Accordion with 5-6 common questions
8. **Final CTA**: Simple centered "Schedule Consultation" with phone number
9. **Footer**: Comprehensive with newsletter

**Critical Design Notes:**
- Luxury = restraint and whitespace, not ornamentation
- Trust built through professional photography and precise typography
- All buttons on hero use blurred backgrounds (backdrop-blur-sm bg-white/10)
- Pricing is the centerpiece - make it impossible to miss