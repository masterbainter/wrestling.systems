# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Wrestling.Systems is a static website for a wrestling training platform with Firebase authentication integration. The site serves as a landing page with early access signup, login functionality, and workout tracking features (WOD - Workout of the Day).

## Tech Stack

- **Frontend**: Pure HTML/CSS/JavaScript (no build system)
- **Styling**: Tailwind CSS (via CDN)
- **Authentication**: Firebase Auth with multiple providers (Google, Facebook, Microsoft)
- **Database**: Firebase Firestore
- **Hosting**: Firebase Hosting
- **Security**: Firebase App Check with reCAPTCHA v3

## Firebase Configuration

Firebase project: `wrestlingsystems`
- Auth domain: `auth.wrestling.systems`
- Project is configured in `.firebaserc`
- Hosting configuration in `firebase.json` (serves from `auth` directory)

## Key Commands

### Deploy to Firebase
```bash
firebase deploy
```

### Deploy hosting only
```bash
firebase deploy --only hosting
```

### Serve locally
```bash
firebase serve
```

## Architecture

### Directory Structure

- `index.html` - Main landing page with early access signup
- `login/` - User sign-in page
- `register/` - User registration page (likely mirrors main page functionality)
- `auth/` - Firebase hosting target directory (default Firebase welcome page)
- `2025/preseason/wod/` - Workout tracking interface
- `terms/` - Terms of Service pages (general, Google, Facebook variants)
- `privacypolicy/` - Privacy Policy pages (general, Google, Facebook variants)
- `free/workout/wod/` - Free workout features
- `repdown/` - Workout-related feature
- `what_is_wrestling-systems/` - Information page

### Authentication Flow

All authentication pages follow a common pattern:
1. Firebase SDK loaded via ESM imports from CDN
2. Firebase App Check initialized with reCAPTCHA v3
3. Email/password and social auth (Google, Facebook, Microsoft) options
4. User data stored in Firestore `users` collection with fields:
   - `firstName`, `lastName`, `email`, `createdAt`
   - `provider` (for social logins)

### Styling Conventions

- Black background with gold accents (#D4AF37 primary, #E6C75E secondary)
- Custom gold color classes: `.bg-gold-500`, `.hover:bg-gold-600`, `.text-gold-300`
- Gradient backgrounds: `from-black to-gray-900`
- Inter font family via Google Fonts

### Firebase Configuration Details

**API Key and Project Details** (index.html:155-163):
- These are public and meant to be in client code
- App Check and Firestore security rules provide actual security
- reCAPTCHA site key: `6Ler2pgrAAAAAAQwDvNoe4voerXxtlVTwvdi0sg2`

### Common Patterns

**Error Handling**:
- Friendly error messages for common auth errors
- Specific handling for: `email-already-in-use`, `weak-password`, `app-check`, `unauthorized-domain`, `permission-denied`, `account-exists-with-different-credential`

**Success States**:
- Forms hide and show success message with green checkmark
- Success message thanks user and promises email notification at launch

## Important Notes

- No build process - all files are static HTML with inline JavaScript
- All dependencies loaded via CDN (Tailwind, Firebase, Google Fonts)
- Assets hosted at `https://assets.wrestling.systems/`
- Multiple backup versions of index.html exist (`.bk20250807`, `.bkup202508020835pm`)
