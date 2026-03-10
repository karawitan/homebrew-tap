# Contributing to Homebrew Tap

## 🌳 **Git Workflow**

### **Branch Strategy**
- `main` - Stable, production-ready formulas only
- `develop` - Integration branch for features
- `feature/*` - New features or experiments
- `bugfix/*` - Bug fixes and improvements
- `release/*` - Release preparation

### **Never Work Directly on `main`**
```bash
# ❌ WRONG - Never do this
git checkout main
# ... make changes ...

# ✅ CORRECT - Always use branches
git checkout -b feature/new-feature
# ... make changes ...
git checkout main
git merge feature/new-feature
```

## 🚀 **Feature Development**

### **1. Create Feature Branch**
```bash
git checkout develop
git pull origin develop
git checkout -b feature/your-feature-name
```

### **2. Make Changes**
- Edit formulas
- Test locally with `brew install ./Formula/your-formula.rb`
- Update documentation
- Add tests if needed

### **3. Test Thoroughly**
```bash
# Test formula syntax
brew audit Formula/your-formula.rb

# Test installation
brew install ./Formula/your-formula.rb --build-from-source

# Test functionality
# ... run your formula's tests ...
```

### **4. Commit Changes**
```bash
git add .
git commit -m "feat: add your feature description

- What changed
- Why it changed
- How to test
- Any breaking changes"
```

### **5. Merge to Develop**
```bash
git checkout develop
git merge feature/your-feature-name
git push origin develop
```

### **6. Release to Main**
```bash
# When ready for production
git checkout main
git pull origin main
git merge develop
git push origin main
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
```

## 🐛 **Bug Fix Process**

### **1. Create Bugfix Branch**
```bash
git checkout develop
git checkout -b bugfix/fix-issue-description
```

### **2. Fix and Test**
```bash
# Make the fix
# Test thoroughly
brew audit Formula/affected-formula.rb
brew install ./Formula/affected-formula.rb --build-from-source
```

### **3. Merge and Release**
```bash
git checkout develop
git merge bugfix/fix-issue-description
git checkout main
git merge develop  # If critical, merge directly to main
```

## 📋 **Branch Naming Convention**

- `feature/ceph-version-update` - New Ceph version support
- `feature/macos-compatibility` - macOS compatibility fixes
- `bugfix/boost-dependency` - Fix dependency issues
- `release/v18.2.7` - Release preparation
- `hotfix/critical-security` - Critical security fixes

## 🧪 **Testing Requirements**

### **Before Any Merge:**
```bash
# 1. Formula syntax check
brew audit Formula/ceph-client.rb

# 2. Installation test
brew install ./Formula/ceph-client.rb --build-from-source

# 3. Functionality test
brew info karawitan/tap/ceph-client

# 4. Clean up test
brew uninstall ceph-client
```

### **For Ceph Client Specifically:**
```bash
# Test dependencies are available
brew install boost@1.85
brew install python@3.11
brew install gperftools

# Test build (may fail due to known issues, but dependencies should work)
cmake -DWITH_CEPHFS=ON -DOPENSSL_ROOT_DIR=$(brew --prefix openssl)
```

## 🔄 **Merge Guidelines**

### **When to Merge to `main`:**
- ✅ All tests pass
- ✅ Documentation updated
- ✅ Breaking changes documented
- ✅ Dependencies verified
- ✅ Experimental status clearly marked

### **When to Use Hotfix Branch:**
- 🚨 Critical security issues
- 🚨 Broken installation
- 🚨 Major dependency conflicts

```bash
git checkout main
git checkout -b hotfix/critical-fix
# ... fix quickly ...
git checkout main
git merge hotfix/critical-fix
git push origin main
```

## 📝 **Commit Message Format**

```
type(scope): description

[optional body]

[optional footer]
```

### **Types:**
- `feat` - New feature
- `fix` - Bug fix
- `docs` - Documentation
- `style` - Formatting
- `refactor` - Code refactoring
- `test` - Testing
- `chore` - Maintenance

### **Examples:**
```
feat(ceph): add support for Reef 18.2.7

- Update URL to latest Ceph release
- Add boost@1.85 dependency
- Mark as experimental for macOS/Tahoe

Closes #1
```

```
fix(deps): resolve boost@1.76 availability issue

- Change to boost@1.85 (available in Homebrew)
- Update dependency checks
- Test installation flow

Fixes #2
```

## 🚨 **Current Status**

### **Main Branch:**
- ✅ Stable experimental formula
- ✅ All dependencies resolved
- ✅ Ready for user installation

### **Known Issues (Track in Issues):**
- StdFilesystem library issue (5% remaining)
- Native build not 100% complete
- Working alternatives available

### **Development Workflow:**
1. **Features** → `feature/*` → `develop` → `main`
2. **Bugfixes** → `bugfix/*` → `develop` → `main`
3. **Hotfixes** → `hotfix/*` → `main` (critical only)

## 🎯 **Best Practices**

1. **Never commit to main directly**
2. **Always test before merging**
3. **Use descriptive commit messages**
4. **Update documentation with changes**
5. **Mark experimental status clearly**
6. **Track issues in GitHub Issues**
7. **Use semantic versioning for releases**

## 📞 **Getting Help**

- **Issues:** https://github.com/karawitan/homebrew-tap/issues
- **Discussions:** https://github.com/karawitan/homebrew-tap/discussions
- **Wiki:** https://github.com/karawitan/homebrew-tap/wiki

---

**Remember:** `main` is for users. `develop` is for integration. `feature/*` is for work!
