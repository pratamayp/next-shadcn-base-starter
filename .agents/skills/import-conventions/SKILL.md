---
name: import-conventions
description: 'Enforce strict import sorting, grouping, and barrel export conventions for Next.js, React, and shadcn/ui projects. Use this when generating new components, refactoring code, or cleaning up files to maintain a conflict-free and readable codebase.'
license: MIT
---

# Next.js & React Import Conventions

## Overview

Maintain clean, readable, and highly organized imports in Next.js (App Router) projects. Strict adherence to these rules minimizes merge conflicts, optimizes bundler performance, and ensures a uniform codebase.

## Strict Sorting & Grouping

Always sort and group imports logically with exactly ONE blank line between groups. The order must strictly follow this hierarchy:

1. **Core & Framework**: `react`, `next`, and their direct sub-modules.
2. **Third-party Packages**: Libraries from `node_modules` (e.g., `zod`, `lucide-react`, `framer-motion`).
3. **Absolute Aliases**: Project-internal imports using the `@/` alias (e.g., `@/components`, `@/lib`, `@/hooks`).
4. **Relative Imports**: Local directory imports (`../`, `./`). _Keep these to an absolute minimum._
5. **Styles & Assets**: `.css` files, fonts, or image assets.

## Import Best Practices

### 1. Prefer Absolute Aliases

Always use absolute paths with the `@/` alias for importing files outside the current component's directory.
**NEVER** use deep relative navigation (e.g., `../../../lib/utils`). Relative imports are only permitted for files residing in the exact same feature folder.

### 2. Enforce Barrel Exports

Always prioritize importing from barrel files (`index.ts`) when available.

- **DO**: `import { Button, Input } from '@/components/ui'`
- **DO NOT**: `import { Button } from '@/components/ui/button'` (Unless explicitly required to avoid circular dependencies).

### 3. Type-Only Imports

When importing TypeScript types or interfaces, you **must** use the `type` modifier. This ensures the Next.js bundler (Turbopack/Webpack) properly strips them out during the build process.

- **DO**: `import type { UserProps } from '@/types'`

### 4. Zero Unused Imports

Never leave unused or dead imports in a file. Always clean up leftover import declarations after refactoring or deleting component usage.

### 5. Server/Client Segregation

Respect Next.js App Router boundaries. Never import server-only utilities (like database connections or files marked with `server-only`) into client components (files containing the `"use client"` directive).

### 6. The `cn()` Utility

For shadcn/ui and Tailwind styling, always import the `cn` utility cleanly when dynamic class manipulation is required.

- **DO**: `import { cn } from '@/lib/utils'`

## Code Examples

### ❌ Incorrect (Messy & Unstructured)

```tsx
import { Button } from '@/componpx -y skills add https://smithery.ai/skills/MadAppGang/tanstack-query --agent gemini-clinents/ui/button';
import React, { useState } from 'react';
import { cn } from '../../../lib/utils';
import { z } from 'zod';
import { Input } from '@/components/ui/input';
import type { FormProps } from '../types';
import Image from 'next/image';
```
