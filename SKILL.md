---
name: 'create-next-boilerplate'
description: 'Creates a custom nextjs boilerplate project.'
metadata:
    author: 'inthahouse'
    version: '0.0.1'
    created: '2026-08-11'
---

# Custom Nextjs Boilerplate project

## Overview

This will install the necessary packages to boot a nextjs project.

## Prequisites Checklist

- [ ] Nodejs 24.19 or higher installed
- [ ] npm 11.17 or higher installed
- [ ] Ensure installation is done at the root level of the directory

## Step-by-Step Guide

### Step 1: Create package.json file

```bash
npm init -y
```
This command will create a `package.json` file and fill it with the following initial structure

```json
{
  "name": "<name of the project as is>",
  "version": "0.0.1",
  "private": true,
  "author": {
    "name": "inthahouse"
  },
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start"
  },
  "type": "module"
}

```

### Step 2: initialize git repository

```bash
git init
```

### Step 3: create .gitignore and apply config

```bash
touch .gitignore
```
and add the following in the .gitignore file
```
# See https://help.github.com/articles/ignoring-files/ for more about ignoring files.

# dependencies
/node_modules
/.pnp
.pnp.*
.yarn/*
!.yarn/patches
!.yarn/plugins
!.yarn/releases
!.yarn/versions

# testing
/coverage

# next.js
/.next/
/out/

# production
/build

# misc
.DS_Store
*.pem

# debug
npm-debug.log*
yarn-debug.log*
yarn-error.log*
.pnpm-debug.log*

# env files (can opt-in for committing if needed)
.env*

# vercel
.vercel

# typescript
*.tsbuildinfo
next-env.d.ts
```

### Step 4: install dependencies

```bash
npm i next@latest react@latest react-dom@latest
```

### Step 5: install dev dependencies

```bash
npm i -D @types/{node,react,react-dom} typescript@latest tailwindcss@latest babel-plugin-react-compiler@latest @tailwindcss/postcss
```

### Step 6: Create the next config file and apply config

```bash
touch next.config.ts
```

then apply the following config

```typescript
import type { NextConfig } from "next"

const nextConfig: NextConfig = {
  reactCompiler: true,
}

export default nextConfig
```

### Step 7: Create next-env.d.ts and apply following code

```bash
touch next-env.d.ts
```

then apply the following in the newly created file.

```typescript
/// <reference types="next" />
/// <reference types="next/image-types/global" />
import "./.next/dev/types/routes.d.ts";
import "./.next/dev/types/root-params.d.ts";

// NOTE: This file should not be edited
// see https://nextjs.org/docs/app/api-reference/config/typescript for more information.

```

### Step 8: initialize tsconfig.json

```bash
tsc --init
```

Modify `tsconfig.json` with the following config.

```json
{
  "compilerOptions": {
    "target": "esnext",
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true,
    "skipLibCheck": true,
    "strict": true,
    "noEmit": true,
    "esModuleInterop": true,
    "module": "esnext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "react-jsx",
    "incremental": true,
    "plugins": [
      {
        "name": "next"
      }
    ],
    "paths": {
      "@/*": ["./*"]
    },

    "types": ["node"],
    "sourceMap": true,
    "declaration": true,
    "declarationMap": true,
    "noUncheckedIndexedAccess": true,
    "exactOptionalPropertyTypes": true,
    "verbatimModuleSyntax": true,
    "noUncheckedSideEffectImports": true,
    "moduleDetection": "force",
  },
  "include": [
    "next-env.d.ts",
    ".next/types/**/*.ts",
    ".next/dev/types/**/*.ts",
    "**/*.mts",
    "**/*.ts",
    "**/*.tsx"
  ],
  "exclude": [
    "node_modules"
  ]
}

```

### Step 9: Create postcss config and apply config

```bash
touch postcss.config.mjs
```

Add the following code in the newly created config file.
```js
const config = {
  plugins: {
    "@tailwindcss/postcss": {},
  },
}

export default config
```

### Step 10: Create readme file

```bash
touch README.md
```

### Step 11: Create app directory with page, layout, and styles files.

```bash
mkdir app
touch app/globals.css app/layout.tsx page.tsx
```

### Step 12: Populate globals.css

Add the following styles in `globals.css`

```css
@import "tailwindcss";

:root {
  --background: #ffffff;
  --foreground: #171717;
}

@theme inline {
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  --font-sans: var(--font-geist-sans);
  --font-mono: var(--font-geist-mono);
}

@media (prefers-color-scheme: dark) {
  :root {
    --background: #0a0a0a;
    --foreground: #ededed;
  }
}

body {
  background: var(--background);
  color: var(--foreground);
}

```

### Step 13: Populate layout.tsx

Add the following code in `app/layout.tsx`

```tsx
import type { Metadata } from "next"
import { Geist, Geist_Mono } from "next/font/google"
import "./globals.css"

const geistSans = Geist({
  variable: "--font-geist-sans",
  subsets: ["latin"],
})

const geistMono = Geist_Mono({
  variable: "--font-geist-mono",
  subsets: ["latin"],
})

export const metadata: Metadata = {
  title: "Create Next App",
  description: "Generated by create next app",
}

export default function RootLayout({ children }: LayoutProps<"/">) {
  return (
    <html
      lang="en"
      className={`${geistSans.variable} ${geistMono.variable} h-full antialiased`}
    >
      <body className="min-h-full flex flex-col">{children}</body>
    </html>
  )
}
```

### Step 14: Populate `app/page.tsx`

Add the following code in `app/page.tsx`

```tsx
export default function Home() {
  return (
    <div className="">
      <header>
        <h1>Boilerplate is up</h1>
      </header>
      <main className="">
        <h2>body here</h2>
      </main>
    </div>
  )
}
```
