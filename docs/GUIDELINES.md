# Development Guidelines

Development standards and best practices for the Nercana Angular project.

## General AI Rules
- If port 4200 is already in use, do not start the development server again. Just use the existing one.
- If you have to chain commands on the command line, use `;` instead of `&&`, because we use PowerShell.
- If running Jest tests, run all Jest tests at once rather than individual test files. 
- If you are unsure about an approach or need clarification, ask for help. It's better to ask than to guess.

## AI Agent Workflow

Follow this systematic approach for any code changes (and follow the general AI rules above):

1. **Research**: Read GUIDELINES.md, SETTING.md, and related files to understand context and requirements
2. **Analyze**: Examine existing code, tests, and dependencies affected by the change
3. **Plan**: Design solution following project architecture and identify all impacted files
4. **Implement**: Make focused, consistent changes following the guidelines below
    - Do not care about legacy compatibility; focus on clean, modern code
5. **Test**: Add/update tests for new functionality, ensure comprehensive coverage
    - Use the deterministic TestRandomProvider for predictable test data
6. **Prune**: Remove unused code, imports, legacy functions and dependencies
7. **Validate**: Run all tests (Jest + Playwright) and iterate until passing

## Core Standards

- **Architecture**: Models in `/models/`, business logic in `/services/`, UI in `/components/`
- **State**: Use NgRx Signal Store exclusively, keep state immutable
- **TypeScript**: Explicit types everywhere, avoid `any`, use interfaces for contracts
- **Testing**: Jest for units, Playwright for e2e, aim for 80%+ coverage on critical features
- **Styling**: SCSS only (no inline styles), use BEM naming, component-scoped styles

## Angular Specifics

### State Management

- NgRx Signal Store for all state
- Never modify state directly, use store methods
- Access state only through stores, not duplicate service properties

### Components

- Small, focused components with single responsibilities
- Container/presentational pattern for complex views
- Use `OnPush` change detection when appropriate

### Performance

- Prefer Angular bindings over DOM manipulation
- Unsubscribe observables to prevent memory leaks
- Use `trackBy` with `*ngFor` for better rendering

### Testing

- Mock dependencies with Jest
- Test edge cases and error scenarios
- Use Angular TestBed sparingly, only for integration tests
- Maintain clean test setup/teardown
- **Performance**: Run all Jest tests at once rather than individual test files - Jest context setup is expensive and running the full suite is more efficient than multiple partial runs

## Development Lifecycle

### Pre-Production Guidelines

- **No Legacy Compatibility Required**: Since the application is not yet in production, prioritize clean, simplified data structures over backward compatibility
- **Breaking Changes Allowed**: Feel free to make breaking changes to improve architecture and code quality
- **Data Structure Evolution**: Update models and interfaces freely to reflect the best design for current requirements
- **Migration Strategy**: Focus on forward-looking design rather than maintaining deprecated patterns

Following these guidelines ensures consistent, maintainable code that integrates well with the existing codebase.
