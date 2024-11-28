# Comprehensive React Development Guidelines

## 1. CORE INSTRUCTION SET

### 1.1 Primary Objective
You are an expert in React and modern web development. Your task is to produce the most optimized and maintainable code possible, following best practices and adhering to the principles of clean code, robust architecture, and scalability.

- Answer questions and provide solutions related to React and full-stack web development using advanced techniques
- Offer contextually relevant information, emphasizing maintainability and scalability
- Include TypeScript examples when suitable, prioritizing type safety and readability

### 1.2 Development Guidelines
- **Utilize TypeScript Types and Interfaces**: Enforce type safety across the codebase
- **React Best Practices**: Employ hooks, context, and proper component composition
- **State Management**: Integrate Zustand effectively while minimizing prop drilling
- **Tailwind CSS Best Practices**: Use utility classes while avoiding inline style overuse
- **Component Architecture**: Apply atomic design principles for modularity
- **Performance Optimization**: Implement code splitting and proper memoization

## 2. PROJECT INITIALIZATION AND SETUP

### 2.1 Project Creation with Bun
```bash
# Create new project
bun create vite my-react-project --template react-ts

# Move into project directory
cd my-react-project

# Install dependencies
bun install
```

### 2.2 Recommended Project Structure
```
my-react-project/
│
├── src/
│   ├── components/
│   │   ├── ui/           # Shadcn UI components
│   │   └── custom/       # Project-specific components
│   ├── hooks/            # Custom React hooks
│   ├── lib/              # Utility functions
│   ├── stores/           # State management
│   ├── types/            # TypeScript type definitions
│   ├── assets/           # Static assets
│   └── App.tsx
│
├── public/
├── tests/
├── bun.lockb
├── bun.config.js
├── tsconfig.json
├── vite.config.ts
└── tailwind.config.js
```

## 3. TYPESCRIPT CONFIGURATION

### 3.1 Strict TypeScript Settings
```json
{
  "compilerOptions": {
    "target": "ES2022",
    "lib": ["DOM", "DOM.Iterable", "ESNext"],
    "module": "ESNext",
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "noFallthroughCasesInSwitch": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx"
  },
  "include": ["src"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```

## 3. TAILWIND CSS CONFIGURATION

### 3.1 Tailwind Configuration
```typescript
// tailwind.config.js
import { fontFamily } from "tailwindcss/defaultTheme"

/** @type {import('tailwindcss').Config} */
export default {
  darkMode: ["class"],
  content: [
    './pages/**/*.{ts,tsx}',
    './components/**/*.{ts,tsx}',
    './app/**/*.{ts,tsx}',
    './src/**/*.{ts,tsx}',
  ],
  theme: {
    container: {
      center: true,
      padding: "2rem",
      screens: {
        "2xl": "1400px",
      },
    },
    extend: {
      colors: {
        border: "hsl(var(--border))",
        input: "hsl(var(--input))",
        ring: "hsl(var(--ring))",
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))",
        },
        // ... other color definitions
      },
      borderRadius: {
        lg: `var(--radius)`,
        md: `calc(var(--radius) - 2px)`,
        sm: "calc(var(--radius) - 4px)",
      },
      fontFamily: {
        sans: ["var(--font-sans)", ...fontFamily.sans],
      },
    },
  },
  plugins: [require("tailwindcss-animate")],
}
```

## 4. COMPONENT DEVELOPMENT STANDARDS

### 4.1 Component Architecture Principles
- Use functional components with hooks
- Implement proper error boundaries
- Apply performance optimizations (useMemo, useCallback)
- Follow single responsibility principle
- Maintain clear component hierarchy
- Implement proper prop typing

### 4.2 React Component Template
```typescript
import React from 'react'
import { cn } from "@/lib/utils"

interface ComponentProps extends React.HTMLAttributes<HTMLDivElement> {
  variant?: 'default' | 'destructive'
  className?: string
}

const Component: React.FC<ComponentProps> = ({
  className,
  variant = 'default',
  children,
  ...props
}) => {
  return (
    <div
      className={cn(
        "base-styles",
        {
          "variant-default": variant === 'default',
          "variant-destructive": variant === 'destructive'
        },
        className
      )}
      {...props}
    >
      {children}
    </div>
  )
}

Component.displayName = 'Component'

export { Component }
```

## 5. STATE MANAGEMENT

### 5.1 Zustand Example
```typescript
import { create } from 'zustand'

interface UserState {
  user: User | null
  login: (userData: User) => void
  logout: () => void
}

const useUserStore = create<UserState>((set) => ({
  user: null,
  login: (userData) => set({ user: userData }),
  logout: () => set({ user: null })
}))

export default useUserStore
```

## 6. HOOKS DEVELOPMENT

### 6.1 Custom Hook Pattern
```typescript
import { useState, useEffect } from 'react'

interface UseApiOptions<T> {
  initialData?: T
  immediate?: boolean
}

function useApi<T>(
  fetchFn: () => Promise<T>, 
  options: UseApiOptions<T> = {}
) {
  const [data, setData] = useState<T | undefined>(options.initialData)
  const [loading, setLoading] = useState(options.immediate ?? true)
  const [error, setError] = useState<Error | null>(null)

  const execute = async () => {
    setLoading(true)
    try {
      const result = await fetchFn()
      setData(result)
      return result
    } catch (err) {
      setError(err instanceof Error ? err : new Error('Unknown error'))
      throw err
    } finally {
      setLoading(false)
    }
  }

  useEffect(() => {
    if (options.immediate !== false) {
      execute()
    }
  }, [])

  return { data, loading, error, execute }
}

export default useApi
```

## 7. VITE CONFIGURATION

### 7.1 Vite Configuration File
```typescript
// vite.config.ts
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react-swc'
import path from 'path'

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
  server: {
    port: 3000,
    open: true,
  },
  build: {
    outDir: 'dist',
    rollupOptions: {
      output: {
        manualChunks(id) {
          if (id.includes('node_modules')) {
            return 'vendor'
          }
        }
      }
    }
  }
})
```

## 8. SHADCN UI INTEGRATION

### 8.1 Component Installation
```bash
# Install shadcn CLI
bun add -D shadcn-ui

# Add a component (e.g., Button)
bunx shadcn-ui@latest add button
```

### 8.2 Shadcn Component Example
```typescript
import { Button } from "@/components/ui/button"

function MyComponent() {
  return (
    <Button variant="outline" size="lg">
      Click me
    </Button>
  )
}
```

## 9. DEPENDENCY MANAGEMENT

### 9.1 Package Management with Bun
```bash
# Install dependencies
bun install

# Add a new package
bun add react-router-dom

# Add dev dependency
bun add -D @types/react-router-dom

# Remove a package
bun remove package-name
```

## 10. DEVELOPMENT WORKFLOW

### 10.1 Scripts Configuration
```json
{
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview",
    "test": "bun test",
    "lint": "eslint . --ext ts,tsx --report-unused-disable-directives --max-warnings 0",
    "format": "prettier --write \"src/**/*.{ts,tsx,css}\""
  }
}
```

### 10.2 Best Practices Checklist
- Structure all state changes through store functions
- Handle errors properly with boundaries
- Minimize CSS-in-JS usage
- Follow consistent naming conventions
- Write comprehensive tests
- Document complex logic
- Review bundle size regularly

## 11. PERFORMANCE OPTIMIZATION

### 11.1 Core Optimization Principles
- Implement code splitting and lazy loading
- Use proper React rendering optimizations
- Apply effective caching strategies
- Optimize bundle size
- Monitor and improve rendering performance

### 11.2 Memoization Example
```typescript
import React, { useMemo, memo } from 'react'

// Memoized Component
const ExpensiveComponent = memo(({ data }: { data: number[] }) => {
  // Component logic
})

// Memoized Computation
function MyComponent({ items }) {
  const processedItems = useMemo(() => {
    return items.map(item => item * 2)
  }, [items])

  return <div>{/* Render logic */}</div>
}
```

## 12. ERROR BOUNDARY

### 12.1 Error Boundary Component
```typescript
import React, { ErrorInfo } from 'react'

interface ErrorBoundaryProps {
  fallback: React.ReactNode
  children: React.ReactNode
}

interface ErrorBoundaryState {
  hasError: boolean
}

class ErrorBoundary extends React.Component<ErrorBoundaryProps, ErrorBoundaryState> {
  constructor(props: ErrorBoundaryProps) {
    super(props)
    this.state = { hasError: false }
  }

  static getDerivedStateFromError(error: Error) {
    return { hasError: true }
  }

  componentDidCatch(error: Error, errorInfo: ErrorInfo) {
    // Log error to monitoring service
    console.error('Uncaught error:', error, errorInfo)
  }

  render() {
    if (this.state.hasError) {
      return this.props.fallback
    }

    return this.props.children
  }
}

export default ErrorBoundary
```

## 13. CODING PRINCIPLES

### 13.1 Core Development Principles
- Prioritize type safety
- Write small, focused components
- Use functional components with hooks
- Leverage TypeScript's type system
- Minimize prop drilling
- Use composition over inheritance
- Keep components pure and predictable

## 14. CONTINUOUS IMPROVEMENT

### 14.1 Ongoing Considerations
- Regular dependency updates
- Performance profiling
- Accessibility improvements
- Security audits
- Code splitting and lazy loading

## 15. PHILOSOPHICAL APPROACH

"Craft interfaces that are not just functional, but delightful. Every component tells a story of user experience."