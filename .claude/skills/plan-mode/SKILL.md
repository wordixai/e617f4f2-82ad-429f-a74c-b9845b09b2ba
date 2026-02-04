---
name: plan
description: Currently in plan mode, plan mode uses this guidance - plan mode provides as much product output as possible, only provides technical solutions when asking about specific technology, technical solutions are decided during implementation. Only plan mode uses this skill
---

# Plan Mode - Intelligent Task Planning and Execution

## Overview

Plan Mode is a **product-output-oriented** intelligent task planning system that breaks down complex tasks into clear product feature steps.

**Core Principles:**
- 📦 **Product Output First**: Planning focuses on describing product features, user value, and business goals
- 🎯 **On-Demand Technical Solutions**: Only provide technical solution details when users explicitly ask about specific technical implementations
- 🔧 **Implementation Decides Solutions**: Technology selection and implementation solutions are decided during the actual execution phase based on project environment
- 📊 **Value-Visible Delivery**: Every step is oriented towards visible product feature output

**Working Method:**
- 🎯 **Intelligent Decomposition**: Break down product requirements into user-understandable functional modules
- 📋 **Product Planning**: Display product feature plan before execution (what to do, why, what's the value)
- 🚀 **Visible Progress**: Display real-time completion status of each feature
- 🔧 **Flexible Implementation**: Choose the best technical solution based on actual situation during implementation
- 📊 **Product Report**: Generate product delivery report after execution (not technical implementation report)

**Important Distinctions:**
- ✅ **Default Output**: Product feature descriptions ("Implement user login functionality", "Add product list display")
- ❌ **Avoid by Default**: Technical implementation details ("Use Supabase Auth", "Create ProductList component")
- ✅ **Special Cases**: Only explain technical solutions in detail when users explicitly ask "how to implement" or "what technology to use"
- ❌ **Avoid Output**: File structures and directory trees, unless user explicitly requests to view project structure

**Announce at Start:** "I will use Plan Mode to plan this task, focusing on product features and value delivery."

## Usage Conditions

**Trigger Condition: Only Use in Plan Mode**

```
✅ When running in Plan Mode
   → Must use this Skill as execution guidance

❌ Other cases
   → No need to use this Skill
```

## Project Initialization Structure Description

**Project is a standard React + Vite + TypeScript + shadcn/ui structure, components under components/ui do not need to be inspected, use directly.**

### Project Structure

```
app/
├── components.json          # shadcn/ui configuration ✨
├── eslint.config.js         # ESLint configuration
├── index.html               # HTML entry
├── package.json             # Dependency management
├── pnpm-lock.yaml           # pnpm lock file (use pnpm)
├── postcss.config.js        # PostCSS configuration
├── tailwind.config.ts       # Tailwind CSS configuration ✨
├── tsconfig.app.json        # TypeScript app configuration
├── tsconfig.json            # TypeScript base configuration
├── tsconfig.node.json       # TypeScript Node configuration
├── vite.config.ts           # Vite configuration
└── src/
    ├── App.css              # App styles
    ├── App.tsx              # Root component
    ├── index.css            # Global styles
    ├── main.tsx             # React entry
    ├── vite-env.d.ts        # Vite type definitions
    ├── components/
    │   └── ui/              # shadcn/ui component library ✨ (50+ components)
    │       ├── accordion.tsx
    │       ├── alert-dialog.tsx
    │       ├── alert.tsx
    │       ├── aspect-ratio.tsx
    │       ├── avatar.tsx
    │       ├── badge.tsx
    │       ├── breadcrumb.tsx
    │       ├── button.tsx
    │       ├── calendar.tsx
    │       ├── card.tsx
    │       ├── carousel.tsx
    │       ├── chart.tsx
    │       ├── checkbox.tsx
    │       ├── collapsible.tsx
    │       ├── command.tsx
    │       ├── context-menu.tsx
    │       ├── dialog.tsx
    │       ├── drawer.tsx
    │       ├── dropdown-menu.tsx
    │       ├── form.tsx
    │       ├── hover-card.tsx
    │       ├── input-otp.tsx
    │       ├── input.tsx
    │       ├── label.tsx
    │       ├── menubar.tsx
    │       ├── navigation-menu.tsx
    │       ├── pagination.tsx
    │       ├── popover.tsx
    │       ├── progress.tsx
    │       ├── radio-group.tsx
    │       ├── resizable.tsx
    │       ├── scroll-area.tsx
    │       ├── select.tsx
    │       ├── separator.tsx
    │       ├── sheet.tsx
    │       ├── sidebar.tsx
    │       ├── skeleton.tsx
    │       ├── slider.tsx
    │       ├── sonner.tsx          # Toast notifications
    │       ├── switch.tsx
    │       ├── table.tsx
    │       ├── tabs.tsx
    │       ├── textarea.tsx
    │       ├── toast.tsx
    │       ├── toaster.tsx
    │       ├── toggle-group.tsx
    │       ├── toggle.tsx
    │       ├── tooltip.tsx
    │       └── use-toast.ts
    ├── hooks/               # Custom Hooks
    │   ├── use-mobile.tsx
    │   └── use-toast.ts
    ├── lib/                 # Utility library
    │   └── utils.ts         # Utility functions (includes cn() function)
    └── pages/               # Pages directory
        ├── Index.tsx        # Home page
        └── NotFound.tsx     # 404 page
```

**Project Configuration Notes:**
- ✅ React 18 + TypeScript + Vite fully configured
- ✅ Tailwind CSS style framework ready to use
- ✅ shadcn/ui component library fully installed (50+ components)
- ✅ pnpm is the package manager (must use `pnpm add`)
- ✅ Basic page structure in `src/pages/` directory
- ⚠️ Backend services not integrated (if database, AI, or email features needed, use corresponding skills)

**⚠️ Important: shadcn/ui components under `components/ui/` do not need source code reading, import and use directly!**

```typescript
// Use directly, no need to read source code
import { Button } from '@/components/ui/button';
import { Card } from '@/components/ui/card';
import { Dialog } from '@/components/ui/dialog';
// ... Other 50+ components
```


### Backend Integration Check

#### Supabase Integration

**If Supabase integration is needed, use the `supabase-integration` skill:**

```
If the project needs database, authentication, or storage features:
1. Use supabase-integration skill for integration
2. Skill will automatically create necessary configurations and files
3. After integration completion, it will include:
   - src/lib/supabase.ts client configuration
   - .env environment variable configuration
   - supabase/ directory (migrations, functions)
```

#### AI Feature Integration

**If AI features are needed (image recognition, intelligent analysis, etc.), use the `ai-integration` skill:**

```
If the project needs AI capabilities:
1. Use ai-integration skill for integration
2. Skill will create AI service functions and frontend calling code
```

#### Email Sending Feature

**If email sending feature is needed, use the `resend-integration` skill:**

```
If the project needs to send emails (welcome emails, notification emails, etc.):
1. Use resend-integration skill for integration
2. Skill will create email sending Edge Function
3. Configure Resend API Key environment variable
```

### Package Manager

**Project uses pnpm:**
- ✅ Install dependencies: `pnpm add [package]`
- ✅ Install dev dependencies: `pnpm add -D [package]`
- ❌ Do not use npm or yarn

### Routing Solution

**If routing feature is needed, install React Router:**
```bash
pnpm add react-router-dom
```


**Important Reminders:**
⚠️ This project uses pnpm, all dependency installations must use `pnpm add`, do not use npm or yarn!
⚠️ No need to read source code of components under `components/ui/` directory, shadcn/ui components can be imported and used directly!
```

