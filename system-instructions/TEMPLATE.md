# Comprehensive Development Stack Guidelines

## 1. PROJECT INITIALIZATION AND SETUP

### 1.1 Project Creation
```bash
# Template for project initialization command
# Replace with stack-specific command
<package_manager> create <project_name> --template <stack_template>

# Move into project directory
cd <project_name>

# Install dependencies
<package_manager> install
```

### 1.2 Recommended Project Structure
```
<project_name>/
│
├── src/                 # Source code directory
│   ├── components/      # Reusable UI/logic components
│   ├── utils/           # Utility functions
│   ├── hooks/           # Custom hooks/functions
│   ├── types/           # Type definitions
│   ├── assets/          # Static assets
│   └── main.<extension> # Entry point
│
├── tests/               # Test files
├── docs/                # Documentation
├── config/              # Configuration files
├── scripts/             # Utility scripts
│
├── package.json         # Dependency management
├── <config_file>        # Language/framework specific config
└── README.md            # Project documentation
```

## 2. LANGUAGE/TYPE SYSTEM CONFIGURATION

### 2.1 Type System Guidelines
- Mandatory type annotations
- Use strong typing
- Leverage type inference
- Create comprehensive type definitions
- Avoid `any` type

#### Type Definition Example
```<language>
// Generic type definition template
interface EntityBase<T> {
  id: string
  createdAt: Date
  updatedAt: Date
  data: T
}

// Example type constraint
type Nullable<T> = T | null | undefined

// Utility type for strict type checking
type StrictOmit<T, K extends keyof T> = Pick<T, Exclude<keyof T, K>>
```

## 3. CORE DEVELOPMENT PRINCIPLES

### 3.1 Universal Coding Standards
- Write clean, readable code
- Follow SOLID principles
- Implement single responsibility principle
- Minimize complexity
- Write self-documenting code
- Favor composition over inheritance
- Implement robust error handling

### 3.2 Code Quality Checklist
- [ ] Type safety ensured
- [ ] Comprehensive documentation
- [ ] Error handling implemented
- [ ] Performance considered
- [ ] Follows language best practices
- [ ] Passes all automated checks

## 4. DEPENDENCY MANAGEMENT

### 4.1 Package Management
```bash
# Install dependencies
<package_manager> install

# Add a new package
<package_manager> add <package_name>

# Add development dependency
<package_manager> add -D <dev_package_name>

# Remove a package
<package_manager> remove <package_name>
```

### 4.2 Dependency Guidelines
- Pin exact versions
- Regularly update dependencies
- Use lockfiles
- Audit security vulnerabilities
- Minimize external dependencies

## 5. CONFIGURATION MANAGEMENT

### 5.1 Environment Configuration
```<language>
// Example environment configuration
interface EnvironmentConfig {
  environment: 'development' | 'staging' | 'production'
  apiBaseUrl: string
  debugMode: boolean
  features: {
    [key: string]: boolean
  }
}

// Configuration loader
function loadConfig(env: string): EnvironmentConfig {
  // Implementation for loading config based on environment
}
```

## 6. ERROR HANDLING AND LOGGING

### 6.1 Error Handling Principles
- Create custom error classes
- Provide context-rich error messages
- Implement global error handlers
- Log errors with sufficient detail
- Handle both expected and unexpected errors

#### Error Handling Template
```<language>
// Base custom error class
class BaseApplicationError extends Error {
  constructor(
    public message: string, 
    public code: string, 
    public metadata?: Record<string, unknown>
  ) {
    super(message)
    this.name = this.constructor.name
  }
}

// Specific error types
class ValidationError extends BaseApplicationError {
  constructor(message: string, validationDetails?: unknown) {
    super(message, 'VALIDATION_ERROR', { details: validationDetails })
  }
}
```

## 7. LOGGING STRATEGY

### 7.1 Logging Configuration
```<language>
// Logging interface
interface Logger {
  info(message: string, context?: Record<string, unknown>): void
  warn(message: string, context?: Record<string, unknown>): void
  error(message: string, error?: Error, context?: Record<string, unknown>): void
  debug(message: string, context?: Record<string, unknown>): void
}

// Example implementation
class ConsoleLogger implements Logger {
  // Logging methods implementation
}
```

## 8. PERFORMANCE OPTIMIZATION

### 8.1 Performance Considerations
- Implement memoization
- Use lazy loading
- Minimize unnecessary computations
- Profile and optimize critical paths
- Implement caching strategies

#### Performance Optimization Template
```<language>
// Memoization utility
function memoize<T extends (...args: any[]) => any>(fn: T): T {
  const cache = new Map()
  return ((...args: Parameters<T>): ReturnType<T> => {
    const key = JSON.stringify(args)
    if (cache.has(key)) {
      return cache.get(key)
    }
    const result = fn(...args)
    cache.set(key, result)
    return result
  }) as T
}
```

## 9. TESTING STRATEGY

### 9.1 Testing Principles
- Aim for high test coverage
- Write tests before implementation (TDD)
- Test both happy and edge cases
- Use property-based testing
- Mock external dependencies
- Implement integration and unit tests

#### Testing Template
```<language>
// Generic test structure
describe('<ComponentOrModule>', () => {
  beforeEach(() => {
    // Setup before each test
  })

  afterEach(() => {
    // Cleanup after each test
  })

  it('should handle primary scenario', () => {
    // Test implementation
  })

  it('should handle edge cases', () => {
    // Edge case testing
  })
})
```

## 10. DEVELOPMENT WORKFLOW

### 10.1 Recommended Scripts
```json
{
  "scripts": {
    "dev": "development server command",
    "build": "build command",
    "test": "test command",
    "lint": "linting command",
    "format": "formatting command",
    "prepare": "pre-commit or setup script"
  }
}
```

## 11. SECURITY CONSIDERATIONS

### 11.1 Security Principles
- Validate and sanitize all inputs
- Use parameterized queries
- Implement proper authentication
- Never hardcode secrets
- Use environment variables
- Regular security audits

## 12. CONTINUOUS IMPROVEMENT

### 12.1 Ongoing Development Guidelines
- Regular code reviews
- Continuous learning
- Stay updated with language/ecosystem changes
- Refactor regularly
- Document architectural decisions

## 13. PHILOSOPHICAL APPROACH

"Code is communication. Write for humans first, machines second. 
Strive for clarity, elegance, and simplicity in every line."

## 14. ADAPTATION GUIDELINES

### 14.1 How to Use This Template
1. Replace `<language>` with actual language syntax
2. Modify examples to fit specific stack
3. Add stack-specific configurations
4. Remove or expand sections as needed
5. Customize to project requirements

## 15. TEMPLATE VERSIONING

### 15.1 Version Control
- Keep this template in version control
- Update regularly based on team experiences
- Share and collaborate on improvements
- Treat this as a living document
```

## APPENDIX: TEMPLATE CUSTOMIZATION CHECKLIST

### Customization Steps
- [ ] Replace placeholder commands
- [ ] Add stack-specific configurations
- [ ] Adjust type system section
- [ ] Customize error handling
- [ ] Update performance optimization techniques
- [ ] Modify testing approach
- [ ] Add specific security considerations

**Template Version**: 1.0.0
**Last Updated**: Current Date