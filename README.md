# Kailashsagar Enterprise

> B2B Digital Product Catalogue & Enquiry/RFQ Platform

Kailashsagar Enterprise is a business-focused digital catalogue platform designed to help hotels, restaurants, caterers, canteens, institutions, distributors, retailers, and other business buyers discover products and submit product requirements directly to the business.

The platform is **not an e-commerce store**. It does not provide public product pricing, checkout, online payment, or conventional order processing in the current version.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Core Objective](#core-objective)
- [Key Features](#key-features)
- [Application Flow](#application-flow)
- [Technology Stack](#technology-stack)
- [Architecture](#architecture)
- [Project Structure](#project-structure)
- [User Types](#user-types)
- [Public Website](#public-website)
- [Admin Panel](#admin-panel)
- [Firebase Architecture](#firebase-architecture)
- [Data Flow](#data-flow)
- [Security](#security)
- [SEO & Analytics](#seo--analytics)
- [Environment Variables](#environment-variables)
- [Local Development](#local-development)
- [Firebase Setup](#firebase-setup)
- [Git & GitHub Workflow](#git--github-workflow)
- [Deployment](#deployment)
- [Development Rules](#development-rules)
- [AI Development Workflow](#ai-development-workflow)
- [Testing Checklist](#testing-checklist)
- [Production Checklist](#production-checklist)
- [Scope Boundaries](#scope-boundaries)
- [Documentation](#documentation)
- [Project Status](#project-status)

---

# Project Overview

**Project Name:** Kailashsagar Enterprise

**Domain:**

`https://kailashsagarenterprise.in`

**Project Type:**

B2B Digital Product Catalogue + Enquiry/RFQ Platform

The website provides a structured digital catalogue where business buyers can:

1. Discover products
2. Browse categories
3. Search and filter products
4. View detailed product information
5. Select variants
6. Specify quantities
7. Add multiple products to an enquiry
8. Submit business/contact information
9. Send their requirement to Kailashsagar Enterprise
10. Contact the business through supported communication channels

The business can then manage the catalogue and incoming enquiries through an authenticated admin panel.

---

# Core Objective

The primary objective is to create a professional B2B digital presence that makes product discovery and business enquiries simple.

The primary user journey is:

```text
Discover
   ↓
Browse Catalogue
   ↓
View Product
   ↓
Select Variant
   ↓
Specify Quantity
   ↓
Add to Enquiry
   ↓
Review Enquiry
   ↓
Enter Business Details
   ↓
Submit Enquiry
   ↓
Business Follow-up

The system is intentionally designed around enquiries rather than purchases.

Key Features
Public Features
Responsive homepage
Business introduction
Product category navigation
Featured products
Product catalogue
Product search
Product filtering
Category pages
Product detail pages
Multiple product images
Product specifications
Product variants
MOQ information
Availability information
Add to enquiry
Multi-product enquiry list
Quantity selection
Business enquiry form
Customer/business information collection
Enquiry review
Enquiry confirmation
WhatsApp contact
Phone contact
Email contact
Business/contact information
Google Maps/location information
Responsive mobile-first interface
Admin Features

The admin panel provides day-to-day catalogue and enquiry management.

Product Management
Create products
Edit products
Publish products
Archive products
Manage product categories
Manage product images
Manage product variants
Manage specifications
Manage availability
Manage MOQ
Mark products as featured
Product Visibility

Products use controlled visibility states:

Draft
Published
Archived

Only appropriate published products should be visible to public users.

Enquiry Management

Admins can:

View incoming enquiries
View customer details
View business details
View requested products
View variants
View quantities
View enquiry date/time
Update enquiry status
Add internal notes
Contact the customer
Enquiry Status
New
Contacted
Quotation Sent
Converted
Closed
Application Flow
Public Flow
                         HOME
                          │
            ┌─────────────┼─────────────┐
            ▼             ▼             ▼
        CATALOGUE      CONTACT       ABOUT
            │
       ┌────┴─────┐
       ▼          ▼
    SEARCH      CATEGORY
       │          │
       └────┬─────┘
            ▼
         PRODUCT
            │
            ▼
     SELECT VARIANT
            │
            ▼
       SET QUANTITY
            │
            ▼
     ADD TO ENQUIRY
            │
            ▼
      ENQUIRY LIST
            │
            ▼
     BUSINESS DETAILS
            │
            ▼
          REVIEW
            │
            ▼
      SUBMIT ENQUIRY
            │
            ▼
         SUCCESS
            │
       ┌────┴─────┐
       ▼          ▼
   WHATSAPP   CATALOGUE
Admin Flow
ADMIN LOGIN
     │
     ▼
FIREBASE AUTH
     │
     ▼
AUTHORIZATION
     │
     ▼
DASHBOARD
     │
 ┌───┼───────────────┐
 ▼   ▼               ▼
PRODUCTS         CATEGORIES      ENQUIRIES
 │                  │               │
 ▼                  ▼               ▼
CREATE/EDIT      CREATE/EDIT    ENQUIRY DETAIL
 │                                  │
 ▼                                  ▼
PUBLISH/ARCHIVE                STATUS / NOTES
Technology Stack

The project follows a Firebase-centric architecture.

Frontend
Technology	Purpose
Next.js	Frontend framework
React	UI library
TypeScript	Application language
Tailwind CSS	Styling
Next.js App Router	Application routing
Firebase Web SDK	Firebase integration
Backend / Cloud
Technology	Purpose
Firebase Authentication	Admin authentication
Cloud Firestore	Application database
Firebase Cloud Storage	Product/category image storage
Firebase Security Rules	Database and storage authorization
Firebase CLI	Firebase project management/deployment

Cloud Functions are not required by default and should only be introduced when a confirmed server-side requirement exists.

Hosting & Infrastructure
Service	Purpose
Vercel	Next.js frontend hosting
Firebase	Database, authentication and storage
Cloudflare	DNS
GitHub	Source code and version control
Google Stitch	UI/UX generation and design exploration
Development Tools
Tool	Purpose
Antigravity	Primary IDE
Gemini Pro	AI coding agent
ChatGPT	Architecture, planning, analysis, debugging and development discussion
Firebase CLI	Firebase development/deployment
Git	Version control
GitHub	Remote repository
Architecture

The application follows a frontend + Firebase architecture.

                         USER
                           │
                           ▼
                    NEXT.JS APPLICATION
                           │
             ┌─────────────┼─────────────┐
             │             │             │
             ▼             ▼             ▼
        Firestore      Firebase       Storage
                       Auth
             │
             ▼
       Security Rules
Why Firebase Is Used

The current project does not require a traditional custom backend server for its core V1 functionality.

Firebase provides the required backend infrastructure:

Firebase Authentication
        +
Cloud Firestore
        +
Cloud Storage
        +
Security Rules

This reduces unnecessary backend infrastructure while keeping the architecture scalable enough for the current catalogue and enquiry requirements.

A separate Express/NestJS/etc. backend should not be introduced unless a future requirement genuinely requires server-side infrastructure that Firebase cannot appropriately handle.

Project Structure

The project follows a feature-oriented Next.js structure.

kailashsagar-enterprise/
│
├── app/
│   ├── home/
│   ├── catalogue/
│   ├── category/
│   │   └── [slug]/
│   ├── product/
│   │   └── [slug]/
│   ├── enquiry/
│   ├── contact/
│   ├── admin/
│   │   ├── login/
│   │   ├── products/
│   │   ├── categories/
│   │   ├── enquiries/
│   │   └── settings/
│   │
│   ├── layout.tsx
│   ├── page.tsx
│   ├── loading.tsx
│   ├── error.tsx
│   ├── not-found.tsx
│   ├── sitemap.ts
│   └── robots.ts
│
├── components/
│   ├── ui/
│   ├── layout/
│   ├── catalogue/
│   ├── product/
│   ├── enquiry/
│   └── admin/
│
├── features/
│   ├── catalogue/
│   ├── products/
│   ├── categories/
│   ├── enquiries/
│   └── admin/
│
├── lib/
│   ├── firebase/
│   ├── analytics/
│   ├── seo/
│   ├── utils/
│   └── constants/
│
├── hooks/
├── types/
├── schemas/
├── config/
├── public/
│
├── functions/
│   └── # Optional; only when required
│
├── scripts/
├── tests/
│
├── firebase.json
├── firestore.rules
├── firestore.indexes.json
├── storage.rules
│
├── .env.example
├── .env.local
├── .gitignore
├── AGENTS.md
│
├── next.config.ts
├── tsconfig.json
├── postcss.config.mjs
├── package.json
└── README.md
User Types
Public Visitor

Authentication is not required.

Public users can:

Browse
Search
Filter
View Products
Select Variants
Add to Enquiry
Submit Enquiry
Contact Business
Admin

Authentication is required.

Admins can:

Manage Products
Manage Categories
Manage Images
Manage Variants
Manage Catalogue Visibility
View Enquiries
Update Enquiry Status
Add Internal Notes
Manage Site Information

Authentication and authorization are separate concepts.

Authentication
"What account is this?"

Authorization
"Is this account allowed to administer the system?"
Public Website
Homepage

The homepage introduces the business and provides direct routes into the catalogue and enquiry system.

Primary sections:

Hero
Product categories
Featured products
Why Kailashsagar Enterprise
Industries served
How it works
Business/trust information
Final enquiry CTA

Primary actions:

Browse Catalogue
Send Enquiry
Catalogue

The catalogue is the primary product discovery interface.

Users can:

Search
Filter
Browse categories
Open product details
Add products to an enquiry

The catalogue does not display public pricing.

Category Pages

Category pages display:

Category information
Category image where available
Products belonging to that category
Relevant filtering/search functionality

Example URL:

/category/[slug]
Product Pages

Product pages display:

Product name
Product code
Product images
Description
Specifications
Variants
MOQ
Availability
Quantity
Add to Enquiry
Contact actions
Related products

Example URL:

/product/[slug]
Enquiry System

The enquiry system is not a shopping cart.

Use:

Enquiry
Enquiry List
Add to Enquiry
Submit Enquiry

Do not use:

Cart
Checkout
Buy Now
Purchase
Payment
Enquiry Lifecycle
Visitor
   ↓
Select Products
   ↓
Select Variants
   ↓
Set Quantities
   ↓
Enter Requirements
   ↓
Enter Business Details
   ↓
Review
   ↓
Submit
   ↓
New
   ↓
Contacted
   ↓
Quotation Sent
   ↓
Converted
   ↓
Closed

Not every enquiry is required to pass through every state.

Enquiry Data Principle

Adding a product to an enquiry does not immediately create an official Firestore enquiry.

The process is:

Product Selection
       ↓
Client-side Enquiry State
       ↓
Business Details
       ↓
Review
       ↓
Validation
       ↓
Firestore Enquiry

This keeps temporary visitor activity separate from actual business enquiries.

Product Snapshot Principle

At final enquiry submission, relevant product information should be snapshotted into the enquiry.

Example:

productId
productName
productCode
variantId
variantName
variantOptions
quantity

This preserves the product context of the enquiry even if the catalogue changes later.

Admin Panel

The admin panel is a private operational interface.

Admin Routes
/admin
/admin/login

/admin/products
/admin/products/new
/admin/products/[id]

/admin/categories

/admin/enquiries
/admin/enquiries/[id]

/admin/settings
Admin Dashboard

The dashboard provides an overview of:

Total products
Published products
Draft products
New enquiries
Recent enquiries
Quick actions

The dashboard should focus on useful operational information rather than unnecessary analytics.

Product Management

Admins can:

Create
Read
Update
Publish
Archive

products.

Product information may include:

Name
Code
Category
Description
Specifications
Images
Variants
MOQ
Availability
Featured Status
SEO Information
Product Visibility
Draft

Internal preparation state.

Published

Visible to public users.

Archived

Removed from normal public catalogue visibility while retaining the record.

Category Management

Admins can manage:

Category name
Slug
Description
Image
Sort order
Active/inactive state
SEO information
Enquiry Management

Admins can view:

Enquiry number
Customer name
Company/business name
Phone
WhatsApp
Email
City
Business type
Requested products
Variants
Quantities
Date/time
Customer message
Status
Internal notes
Firebase Architecture
Firebase Services

The project uses:

Firebase Authentication
Cloud Firestore
Firebase Cloud Storage
Firebase Security Rules
Firebase CLI
Authentication

Firebase Authentication is used for admin authentication.

Public catalogue browsing does not require authentication.

The application must not implement a custom password system unless a future requirement explicitly requires one.

Firestore

Firestore stores application data such as:

Products
Categories
Enquiries
Admin-related data
Site configuration

The exact collection/document structure is defined in the Backend Schema document.

The README is not the authoritative database schema.

Storage

Firebase Cloud Storage is used for catalogue media such as:

Product Images
Category Images

Product images should not unnecessarily be committed into the Git repository.

Security Rules

Security is enforced using:

Firestore Security Rules
+
Storage Security Rules
+
Firebase Authentication
+
Application Validation

The frontend is not considered a trusted security boundary.

Public Data Access

Public users should only be able to access intended public catalogue information.

Conceptually:

Published Products → Public Read
Draft Products     → Admin Only
Archived Products  → Admin / controlled access
Enquiries          → Admin Only
Internal Notes     → Admin Only
Enquiry Security

Public users may create an enquiry, but must not be able to read arbitrary existing enquiries.

Public users must not be able to:

Read all enquiries
Modify existing enquiries
Delete existing enquiries
Read internal notes
Modify products
Modify categories
Access admin configuration
Admin Security

Admin access requires:

Firebase Authentication
        +
Admin Authorization
        +
Firestore/Storage Security Rules

Hiding an admin page in the frontend is not sufficient security.

Input Validation

All user-controlled input must be treated as untrusted.

Validate:

Name
Company
Phone
Email
City
Business type
Message
Product ID
Variant ID
Quantity
Search input
URL parameters
Variant Validation

Before creating an enquiry:

Selected Product
       ↓
Validate Product
       ↓
Validate Variant
       ↓
Verify Variant belongs to Product
       ↓
Verify availability where applicable
Quantity Validation

Quantity must:

Be numeric
Be greater than zero
Remain within the application's defined reasonable maximum
Image Upload Security

Admin uploads must validate:

File type
File size
Storage path
User authorization
Appropriate image handling

Public users must not be able to upload arbitrary files.

Secrets

Never commit:

.env.local
Firebase service-account credentials
Private keys
Passwords
Private API tokens
Production secrets

to GitHub.

SEO & Analytics
Search Engines

The project will be configured for:

Google Search Console
Microsoft/Bing Webmaster ecosystem

Public catalogue pages should use SEO-friendly URLs and metadata.

SEO

The application should support:

Metadata
Page titles
Meta descriptions
Canonical URLs where appropriate
Sitemap
Robots configuration
Breadcrumbs
Semantic headings
Product/category SEO content
Structured data where appropriate

Public product and category pages should be indexable when they are intended to be publicly discoverable.

Analytics

The project will use:

Google Analytics

Analytics should help understand:

Catalogue visits
Product views
Search activity where implemented
Enquiry initiation
Enquiry submission
Contact interactions
General website engagement

Do not collect unnecessary personal information through analytics.

Environment Variables

Use environment variables for environment-specific configuration.

Example:

NEXT_PUBLIC_FIREBASE_API_KEY=
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=
NEXT_PUBLIC_FIREBASE_PROJECT_ID=
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=
NEXT_PUBLIC_FIREBASE_APP_ID=

NEXT_PUBLIC_SITE_URL=

NEXT_PUBLIC_GA_ID=

The exact variables are determined by the actual implementation.

Important Environment Rule

.env.local must never be committed.

.env.example may be committed with placeholder values.

Example:

.env.local       → PRIVATE / LOCAL
.env.example     → SAFE TEMPLATE
Local Development
Prerequisites

Install:

Node.js
npm
Git
Firebase CLI

Then clone the repository.

git clone <repository-url>
cd kailashsagar-enterprise

Install dependencies:

npm install

Create local environment configuration:

cp .env.example .env.local

Fill in the required Firebase configuration.

Start development:

npm run dev

The local application should normally be available at:

http://localhost:3000
Firebase Setup

The project currently requires a Firebase project before Firebase integration can be completed.

Required Firebase services:

Authentication
Firestore
Storage

The Firebase project should be created specifically for Kailashsagar Enterprise.

Firebase CLI

Authenticate:

firebase login

Check the current Firebase project:

firebase use

Initialize Firebase configuration if required:

firebase init

Deploy Firestore rules:

firebase deploy --only firestore:rules

Deploy Firestore indexes:

firebase deploy --only firestore:indexes

Deploy Storage rules:

firebase deploy --only storage

Do not deploy blindly to production.

Always verify the selected Firebase project first.

Git & GitHub Workflow

The GitHub repository is the source-control authority for application code and configuration.

Recommended workflow:

Feature / Change
      ↓
Local Development
      ↓
Test
      ↓
Git Diff Review
      ↓
Commit
      ↓
Push
      ↓
Vercel Preview
      ↓
Review
      ↓
Production
Commit Guidelines

Use meaningful commit messages.

Examples:

feat: add catalogue search
feat: add enquiry submission flow
feat: add admin product management

fix: resolve product image loading
fix: correct enquiry validation

security: tighten firestore enquiry rules

refactor: simplify product card component

docs: update firebase setup

Avoid:

update
changes
final
final2
new
test
Development Rules
Rule 1 — Follow the Documentation

The following documents form the project specification:

PRD
 ↓
TRD
 ↓
Backend Schema
 ↓
Folder Structure & Security
 ↓
UI/UX Brief
 ↓
App Flow

Code must follow these documents.

Rule 2 — Do Not Invent Features

Do not add:

Checkout
Payment
Public pricing
Customer accounts
Order tracking
Wishlist
Loyalty system
Unrequested ERP integrations
Unrequested APIs

unless the project scope is officially changed.

Rule 3 — Do Not Change the Architecture Casually

The project uses:

Next.js
React
TypeScript
Firebase
Vercel
Cloudflare

Do not introduce another backend framework or database simply to solve a small implementation problem.

Rule 4 — Do Not Bypass Security

Never solve:

PERMISSION_DENIED

by changing rules to:

allow read, write: if true;

Security rules must be fixed according to the intended authorization model.

Rule 5 — Do Not Trust Client Input

Validate user-controlled data before writing important data to Firebase.

Rule 6 — Do Not Duplicate Firebase Initialization

Firebase initialization should remain centralized inside:

lib/firebase/
Rule 7 — Reuse Components

Use shared components rather than creating multiple slightly different versions of:

Button
Input
Card
ProductCard
Modal
Table
Badge
AI Development Workflow

This project uses AI-assisted development.

Tools
Google Stitch
      ↓
UI/UX generation

ChatGPT
      ↓
Planning / Architecture / Analysis / Debugging

Gemini Pro
      ↓
Coding Agent

Antigravity
      ↓
IDE / Development Environment

Firebase CLI
      ↓
Firebase Management

GitHub
      ↓
Version Control

Vercel
      ↓
Frontend Deployment
AI Coding Rules

AI agents must follow the existing project documentation.

Before implementing a new feature, the agent should determine:

1. Is the feature in the PRD?
2. Is it supported by the TRD?
3. Does it match the Backend Schema?
4. Does it match the App Flow?
5. Does it match the UI/UX specification?
6. Does it respect the security model?

If the answer is no, the agent must not silently invent an alternative architecture.

AI Agent Must Never

AI agents must never:

Expose secrets
Commit .env.local
Commit service-account credentials
Disable authentication to fix an issue
Make Firestore completely public
Remove validation
Bypass authorization
Modify database schema without documentation
Introduce a second backend unnecessarily
Replace Firebase with another database without approval
Change framework versions without checking compatibility
Add unnecessary dependencies
Delete security rules to make deployment succeed
Version Compatibility Rule

The repository's dependency files are the final authority for installed package versions.

Before changing dependencies:

Check package.json
        ↓
Check lockfile
        ↓
Check existing implementation
        ↓
Check compatibility
        ↓
Install/update
        ↓
Run build
        ↓
Run tests

Do not blindly upgrade:

Next.js
React
TypeScript
Firebase SDK
Tailwind
Node.js

during feature development.

Dependency upgrades should be treated as deliberate changes.

Google Stitch Workflow

Google Stitch is used for UI/UX exploration and generation.

The UI should follow the UI/UX Brief.

Design generation order:

Design System
      ↓
Header / Footer
      ↓
Homepage
      ↓
Catalogue
      ↓
Category
      ↓
Product
      ↓
Enquiry
      ↓
Business Details
      ↓
Success
      ↓
Contact
      ↓
Admin Login
      ↓
Admin Dashboard
      ↓
Admin CRUD

Stitch must not invent business claims, products, prices, certifications, testimonials, or other factual information.

Testing Checklist
Public Website
 Homepage loads
 Catalogue loads
 Category pages work
 Product pages work
 Search works
 Filters work
 Product variants work
 Quantity selection works
 Add to Enquiry works
 Multiple products can be added
 Enquiry quantities can be changed
 Products can be removed
 Empty enquiry state works
 Business form validation works
 Enquiry submission works
 Duplicate submission is prevented
 Success page works
 WhatsApp links work
 Phone links work
 Email links work
 404 page works
Admin Testing
 Admin login works
 Invalid login is handled
 Unauthorized users cannot access admin
 Dashboard loads
 Product creation works
 Product editing works
 Product publishing works
 Product archiving works
 Category management works
 Image upload works
 Variant management works
 Enquiry list works
 Enquiry details work
 Status updates work
 Internal notes work
 Admin logout works
Security Testing
Public User
Can read published products       YES
Can read draft products           NO
Can modify products               NO
Can create products               NO
Can read enquiries                NO
Can create enquiry                YES
Can modify existing enquiry       NO
Can read admin data               NO
Authorized Admin
Can manage products               YES
Can manage categories             YES
Can upload catalogue images       YES
Can read enquiries                YES
Can update enquiry status         YES
Can add internal notes            YES
Unauthorized User
Can access admin data             NO
Can modify catalogue              NO
Can read enquiries                NO
Responsive Testing

The website must be tested on:

Mobile
Tablet
Desktop
Large Desktop

Important flows must work with touch interaction on mobile.

Priority mobile flows:

Search
Catalogue
Product Detail
Add to Enquiry
Enquiry Review
Business Form
Submission
Accessibility Testing

Check:

 Semantic HTML
 Correct heading hierarchy
 Keyboard navigation
 Visible focus states
 Form labels
 Accessible error messages
 Image alt text
 Sufficient contrast
 Touch-friendly controls
 Buttons have meaningful labels
 No functionality depends only on color
Production Checklist
Firebase
 Correct production Firebase project selected
 Authentication configured
 Firestore configured
 Storage configured
 Firestore rules deployed
 Storage rules deployed
 Required indexes deployed
 Admin authorization verified
 Security tests completed
Vercel
 Production project configured
 Correct GitHub repository connected
 Environment variables configured
 Production build succeeds
 Preview deployment tested
 Production domain configured
Cloudflare
 Domain configured
 DNS records verified
 HTTPS enabled
 Production routing verified
 No unintended development endpoint exposed
SEO
 Sitemap generated
 Robots configuration verified
 Metadata configured
 Canonical URLs checked
 Google Search Console configured
 Microsoft/Bing webmaster configuration completed
 Important public pages crawlable
Analytics
 Google Analytics configured
 Important events tested
 No unnecessary personal information collected
 Production measurement verified
Scope Boundaries

The current V1 application intentionally does not implement:

Customer Accounts
Customer Login
Shopping Cart
Checkout
Online Payments
Order Processing
Order Tracking
Public Product Pricing
Wishlist
Loyalty Program
Customer Dashboard

The core system remains:

Catalogue
   ↓
Product
   ↓
Enquiry
   ↓
Business Details
   ↓
Submission
   ↓
Business Follow-up
Future Expansion

Future versions may introduce additional functionality if required.

Possible future modules:

Customer Accounts
Formal Quotation System
Order Management
Online Payments
Customer Dashboard
Order Tracking
ERP Integration
CRM Integration
Advanced Analytics
Automated Notifications

These should be introduced as separate scope changes rather than silently added to V1.

Documentation

The project documentation is organized as follows:

01 — PRD
     Defines WHAT the product should do.

02 — TRD
     Defines HOW the product is technically built.

03 — Backend Schema
     Defines the Firebase/Firestore data structure.

04 — Folder Structure & Security
     Defines WHERE code lives and HOW the application is protected.

05 — UI/UX Brief
     Defines HOW the application looks and behaves.

06 — App Flow
     Defines HOW users and system states move through the application.

07 — README
     Provides the GitHub project overview and development reference.
Source of Truth

When implementing the project, use the following priority:

Business Requirement
        ↓
PRD
        ↓
TRD
        ↓
Backend Schema
        ↓
Security Specification
        ↓
UI/UX Specification
        ↓
App Flow
        ↓
Code

If code conflicts with the documented architecture, the code should be corrected rather than silently changing the specification.

If two documents conflict, stop and resolve the conflict before implementing the affected functionality.

Project Status

Current planning/design stage:

[✓] Requirements Document
[✓] Technical Requirements Document
[✓] Backend Schema
[✓] Folder Structure & Security Specification
[✓] UI/UX Brief
[✓] App Flow
[✓] GitHub README
[ ] Firebase Project Creation
[ ] Firebase Configuration
[ ] GitHub Repository Initialization
[ ] Next.js Project Initialization
[ ] Design System Implementation
[ ] Google Stitch UI Generation
[ ] Public Website Development
[ ] Firebase Integration
[ ] Admin Panel Development
[ ] Security Rules Testing
[ ] Full QA
[ ] Production Deployment
[ ] Domain Configuration
[ ] Search Console Setup
[ ] Analytics Verification
Deployment Architecture

The intended production architecture is:

                     kailashsagarenterprise.in
                              │
                              ▼
                         Cloudflare
                         DNS Layer
                              │
                              ▼
                            Vercel
                         Next.js App
                              │
             ┌────────────────┼────────────────┐
             │                │                │
             ▼                ▼                ▼
       Firebase Auth     Firestore          Storage
             │                │                │
             └────────────────┼────────────────┘
                              ▼
                       Firebase Rules
Development Principle

The project should remain:

Simple
Maintainable
Secure
Fast
Scalable enough for the current requirement

Avoid unnecessary infrastructure.

The guiding principle is:

Build only what the business requirement needs, but build the required parts correctly.

License

This project is proprietary software for Kailashsagar Enterprise.

Unauthorized copying, redistribution, modification, or commercial reuse is not permitted without appropriate authorization from the project owner.

Maintainers

Project: Kailashsagar Enterprise

Domain:
kailashsagarenterprise.in

Repository:
Kailashsagar Enterprise GitHub Repository

Development Environment:
Antigravity

AI Coding Agent:
Gemini Pro

Architecture & Technical Discussion:
ChatGPT

UI/UX Generation:
Google Stitch

Frontend Hosting:
Vercel

Backend / Database / Storage:
Firebase

DNS:
Cloudflare


### One important correction to how I'd use this

Don't treat the README as the **technical source of truth**. It should be the **entry point** to the repository. The detailed documents remain authoritative for their respective areas:

```text
README
  │
  ├── Project overview
  ├── Setup
  ├── Development rules
  └── Links/references
        │
        ├── PRD       → Product requirements
        ├── TRD       → Technical architecture
        ├── Schema    → Firebase data model
        ├── Security  → Security rules
        ├── UI/UX     → Design specification
        └── App Flow  → User/system flows
