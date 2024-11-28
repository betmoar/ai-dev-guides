# Comprehensive Git Guidelines

## 1. CORE INSTRUCTION SET

### 1.1 Primary Objective
You are an expert in Git version control and best practices. Your task is to ensure proper version control management, clear commit history, and maintainable codebase through well-documented changes.

- Create clear and meaningful commit messages
- Follow Git best practices for version control
- Maintain clean and organized repository history

### 1.2 Version Control Standards
- **Clear Communication**: Write descriptive commit messages
- **Atomic Commits**: One logical change per commit
- **Documentation**: Update relevant docs with changes
- **Consistency**: Follow project commit conventions
- **Traceability**: Link issues and pull requests
- **History**: Maintain clean commit history

## 2. GIT WORKFLOW

### 2.1 Basic Git Commands
```bash
# Initialize repository
git init

# Stage changes
git add <file>
git add .

# Commit changes
git commit -m "message"

# Push changes
git push origin <branch>

# Pull changes
git pull origin <branch>
```

### 2.2 Branch Management
```bash
# Create and switch to new branch
git checkout -b feature/new-feature

# Switch branches
git checkout main

# List branches
git branch

# Delete branch
git branch -d feature/old-feature
```

## 3. COMMIT STANDARDS

### 3.1 Commit Message Structure
```
<type>(<scope>): <subject>

<body>

<footer>
```

### 3.2 Commit Types
- feat: New feature
- fix: Bug fix
- docs: Documentation changes
- style: Code style changes
- refactor: Code refactoring
- test: Adding tests
- chore: Maintenance tasks

### 3.3 Example Commit Messages
```
feat(auth): implement JWT authentication

- Add JWT token generation and validation
- Create middleware for protected routes
- Update user model for token storage

Closes #123
```

```
fix(api): resolve data race in concurrent requests

- Add mutex lock for shared resource access
- Implement proper error handling
- Add logging for debugging

Fixes #456
```

## 4. BRANCHING STRATEGY

### 4.1 Branch Types
- main/master: Production code
- develop: Development code
- feature/*: New features
- bugfix/*: Bug fixes
- release/*: Release preparation
- hotfix/*: Production fixes

### 4.2 Branch Workflow
```bash
# Start new feature
git checkout develop
git checkout -b feature/new-feature

# Work on feature
git add .
git commit -m "feat: add new feature"

# Update with latest changes
git checkout develop
git pull
git checkout feature/new-feature
git rebase develop

# Finish feature
git checkout develop
git merge --no-ff feature/new-feature
```

## 5. CODE REVIEW PROCESS

### 5.1 Pull Request Template
```markdown
## Description
Brief description of changes

## Type of change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## How Has This Been Tested?
Describe test cases

## Checklist
- [ ] Code follows style guidelines
- [ ] Tests added/updated
- [ ] Documentation updated
- [ ] Changelog updated
```

### 5.2 Review Guidelines
- Check code style compliance
- Verify test coverage
- Review documentation updates
- Validate commit messages
- Ensure CI/CD passes

## 6. REPOSITORY MAINTENANCE

### 6.1 Repository Hygiene
```bash
# Clean untracked files
git clean -df

# Prune remote branches
git remote prune origin

# Remove merged branches
git branch --merged | grep -v "\*" | xargs -n 1 git branch -d
```

### 6.2 Git Configuration
```bash
# Set user information
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Set default branch
git config --global init.defaultBranch main

# Set pull strategy
git config --global pull.rebase true
```

## 7. TROUBLESHOOTING

### 7.1 Common Issues
```bash
# Undo last commit
git reset --soft HEAD~1

# Discard local changes
git checkout -- .

# Fix wrong commit message
git commit --amend

# Undo pushed commit
git revert HEAD
```

### 7.2 Best Practices
- Always pull before pushing
- Create feature branches
- Keep commits atomic
- Write clear commit messages
- Review changes before commit
- Use .gitignore properly

## 8. CHANGELOG MANAGEMENT

### 8.1 Changelog Format
```markdown
# Changelog

## [Unreleased]
### Added
- New feature X
### Changed
- Updated feature Y
### Fixed
- Bug in feature Z

## [1.0.0] - YYYY-MM-DD
### Added
- Initial release
```

### 8.2 Version Control
- Follow semantic versioning
- Update changelog before release
- Tag releases properly
- Keep changelog up to date

## 9. NOTES

- Keep commits small and focused
- Use meaningful branch names
- Update documentation with changes
- Follow project conventions
- Review changes before pushing
- Maintain clean history