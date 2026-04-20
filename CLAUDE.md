\# CLAUDE.md — StyleDesk.ai Landing Page



\## Project

Marketing landing page for StyleDesk.ai — AI receptionist for barbers and nail techs.



\## Stack

Static HTML + CSS + JS. No framework. Hosted on Vercel.



\## Live URL

styledesk-landing-wdky.vercel.app



\## Files

\- index.html — main landing page (all sections, styles, and scripts in one file)

\- privacy.html — privacy policy

\- terms.html — terms of service

\- styledesk-logo.png — crown logo (rounded square, 1427x1427)

\- images/basic-dashboard.png — Basic dashboard screenshot

\- images/pro-dashboard.png — Pro dashboard screenshot

\- images/premium-dashboard.png — Premium dashboard screenshot



\## Design

\- Background: linear-gradient(to bottom, #3a0018, #2a0012, #1a000b)

\- Font: Inter (300-900) + DM Mono

\- Floating particles on every section (15 per section)

\- Scroll reveal animations (.reveal class)

\- Phone mockup with animated SMS conversation in hero

\- Dashboard carousel with Basic/Pro/Premium screenshots



\## Landing Page Sections (in order)

1\. Nav — logo, How it Works, Features, Pricing, Book Demo

2\. Live counter banner — Supabase-powered call/text counts

3\. Hero — "Every Call. Every Text. Handled." + phone mockup

4\. Pain point — "Your phone is your biggest weakness..."

5\. How it Works — 3 steps

6\. Live demo — call/text (301) 888-7454

7\. Works With — Booksy, Square, Fresha, Vagaro

8\. Features — 8 features included in every plan

9\. Dashboard carousel — tier screenshots

10\. Pricing — $49/$179/$299 with Stripe checkout links

11\. Final CTA — "Ready to never miss a client again?"

12\. Footer — links, social, legal



\## Stripe Checkout Links

\- Basic: https://buy.stripe.com/eVqeVf6Vea0jgB3duPgEg04

\- Pro: https://buy.stripe.com/5kQ28t2EY3BV1G99ezgEg05

\- Premium: https://buy.stripe.com/14A14p7ZifkD70t4YjgEg06



\## Demo Link

Book Demo: https://meetings-na2.hubspot.com/tabish-akbar



\## Key Rules

\- Keep all CSS and JS inline in index.html (single file)

\- Maintain mobile responsiveness on all sections

\- Particles must span full viewport width (not constrained by max-width)

\- Phone mockup SMS conversation auto-types on load



\## Instagram / Social Post Design System

Locked visual system for Instagram, Reels covers, and other social content. Reference `instagram/01-may-launch-announcement.svg` as the canonical template.

\- Canvas: 1080×1350 (4:5 Instagram portrait)

\- Background: linear-gradient top→bottom `#3a0018 → #2a0012 → #1a000b` (same as site)

\- Ambient glow: radial gradient top-center, `#c9a064` at 0.18 opacity fading through `#7c1f36` to transparent

\- Palette: gold `#c9a064`, pink `#f0c6cf`, white `#ffffff`. Gold gradient fill `#f0c6cf → #c9a064 → #f0c6cf` (same gradient stops as site headlines)

\- Font stack: `'Helvetica Neue', 'Inter', -apple-system, 'SF Pro Display', sans-serif` — ultralight (200) for neutral copy, medium (500) for gold emphasis

\- Hero rhythm: eyebrow (small gold caps, letter-spacing ~4) → hero line (one row, weight+color contrast, ~105px) → two-line sub (light 28px + medium 30px) → ornamental divider (line · dot · line in gold) → url (tracked caps in gold, letter-spacing ~8)

\- No decorative particles on social posts unless explicitly requested — the ambient radial glow alone carries the mood

\- Use `<tspan>` on a single source line (no whitespace between) when mixing weights/colors on one hero line, otherwise SVG renderers may wrap it

