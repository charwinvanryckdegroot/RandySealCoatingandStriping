# Universal Production-Safe Debugging Rule

## CRITICAL PRODUCTION DIRECTIVE
You are debugging in a PRODUCTION or PRODUCTION-LIKE environment across ANY platform (iOS/Android/Web/Backend). Every change must be:
- **MINIMAL**: Fix only what's broken, nothing more
- **SAFE**: No breaking changes to existing functionality
- **REVERSIBLE**: Easy to rollback if needed
- **TESTED**: Verify the fix doesn't break anything else

## PLATFORM-AGNOSTIC DEBUGGING PROTOCOL

### 1. IMMEDIATE ASSESSMENT
**STOP and assess before any changes:**
- **Severity Level**: 
  - 🔴 CRITICAL: App/System down, data loss risk, security breach
  - 🟡 HIGH: Major feature broken, significant UX impact
  - 🟢 MEDIUM: Minor feature issue, workaround available
  - ⚪ LOW: Cosmetic, edge case, minimal impact
- **Platform Affected**: iOS / Android / Web / Backend / Multiple
- **Blast Radius**: How many users/features are affected?
- **Workaround Available**: Can users complete their task another way?
- **Data Integrity Risk**: Could this cause data corruption/loss?

### 2. ERROR ANALYSIS
**Gather ALL information before touching code:**
```markdown
Error Classification:
- [ ] Compilation/Build Error
- [ ] Runtime Exception/Crash
- [ ] Logic Error (wrong output)
- [ ] Performance Issue
- [ ] Network/API Error
- [ ] Database/Data Error
- [ ] UI/UX Broken
- [ ] Security Vulnerability
- [ ] Platform-Specific Issue

Error Details:
- Exact Error Message: [Copy full error]
- Stack Trace/Crash Log: [Full trace]
- When Started: [Timestamp]
- Frequency: [Always/Sometimes/Rare]
- User Actions That Trigger: [Steps]
- Platform Details:
  - iOS: [Version, Device, Xcode version]
  - Android: [API Level, Device, Studio version]
  - Web: [Browser, Version, OS]
  - Backend: [Runtime, Version, Environment]
```

### 3. ROOT CAUSE INVESTIGATION
**Before fixing, understand WHY it's broken:**

#### A. Platform-Specific Investigation

**iOS (Xcode)**:
```markdown
- [ ] Check crash logs in Organizer
- [ ] Review memory graph for leaks
- [ ] Inspect view hierarchy debugger
- [ ] Check Instruments for performance
- [ ] Review TestFlight crash reports
- [ ] Verify provisioning/certificates
```

**Android (Android Studio)**:
```markdown
- [ ] Check Logcat for exceptions
- [ ] Review Android Profiler
- [ ] Inspect Layout Inspector
- [ ] Check Play Console crash reports
- [ ] Review ANR reports
- [ ] Verify ProGuard/R8 rules
```

**Web**:
```markdown
- [ ] Check browser console errors
- [ ] Review Network tab for failed requests
- [ ] Inspect browser compatibility
- [ ] Check performance metrics
- [ ] Review error tracking service
- [ ] Verify build/bundle issues
```

#### B. Universal Root Causes to Check
- **Memory Issues**: Leaks, retain cycles, excessive usage
- **Threading**: Race conditions, deadlocks, main thread blocking
- **Null/Nil/Undefined**: Missing checks, optional handling
- **Type Mismatches**: Casting errors, type safety violations
- **API Changes**: Contract violations, version mismatches
- **State Management**: Inconsistent state, stale data
- **Permissions**: Missing permissions, security policies
- **Resource Loading**: Missing assets, failed network requests
- **Configuration**: Environment variables, build settings

### 4. SOLUTION PLANNING
**Plan the MINIMAL fix needed:**

#### A. Fix Options Analysis
```markdown
Option 1: [Description]
- Risk Level: LOW/MEDIUM/HIGH
- Files/Components Affected: [List]
- Platform Impact: [iOS/Android/Web/All]
- Side Effects: [Any possible impacts]
- Rollback Strategy: [Platform-specific rollback]

Selected Option: [Number] because [Reasoning]
```

#### B. Platform-Specific Change Scope
- [ ] iOS: No changes to app architecture or Core Data schema
- [ ] Android: No changes to database schema or manifest permissions (unless required)
- [ ] Web: No changes to API contracts or database migrations
- [ ] All: Maintains backward compatibility
- [ ] All: No dependency updates unless required for fix

### 5. IMPLEMENTATION SAFEGUARDS

#### A. Pre-Implementation Backup

**iOS/macOS**:
```bash
# Create git checkpoint
git checkout -b hotfix/issue-description-$(date +%Y%m%d)
# Archive current build
xcodebuild archive -scheme YourScheme
```

**Android**:
```bash
# Create git checkpoint
git checkout -b hotfix/issue-description-$(date +%Y%m%d)
# Backup current APK/AAB
cp app/build/outputs/apk/release/app-release.apk ../backups/
```

**Web**:
```bash
# Create git checkpoint
git checkout -b hotfix/issue-description-$(date +%Y%m%d)
# Backup current build
cp -r dist/ ../backups/dist-$(date +%Y%m%d)/
```

#### B. Defensive Implementation Patterns

**iOS (Swift)**:
```swift
// Safe unwrapping
guard let data = optionalData else {
    print("Warning: data is nil")
    return defaultValue
}

// Defensive error handling
do {
    try riskyOperation()
} catch {
    print("Error in operation: \(error)")
    // Fallback behavior
}

// Thread safety
DispatchQueue.main.async { [weak self] in
    self?.updateUI()
}
```

**Android (Kotlin)**:
```kotlin
// Null safety
data?.let { safeData ->
    // Process data
} ?: run {
    Log.w(TAG, "Data is null")
    // Fallback behavior
}

// Exception handling
try {
    riskyOperation()
} catch (e: Exception) {
    Log.e(TAG, "Operation failed", e)
    // Fallback behavior
}

// Lifecycle awareness
lifecycleScope.launchWhenStarted {
    // Safe coroutine operations
}
```

**Web (JavaScript/TypeScript)**:
```javascript
// Defensive checks
if (data && typeof data === 'object') {
    // Process data
} else {
    console.warn('Invalid data structure');
    return fallbackValue;
}

// Error boundaries (React)
try {
    // Risky operation
} catch (error) {
    console.error('Operation failed:', error);
    // Report to error tracking
    // Return fallback UI/behavior
}

// Safe async operations
async function safeOperation() {
    try {
        const result = await riskyAsyncCall();
        return result;
    } catch (error) {
        console.error('Async operation failed:', error);
        return defaultValue;
    }
}
```

### 6. VALIDATION PROTOCOL

#### A. Platform-Specific Testing

**iOS Testing**:
```markdown
- [ ] Run unit tests: cmd+U in Xcode
- [ ] Run UI tests on multiple devices
- [ ] Test on minimum supported iOS version
- [ ] Memory leak detection with Instruments
- [ ] Test with network link conditioner
- [ ] Verify on actual devices, not just simulator
```

**Android Testing**:
```markdown
- [ ] Run unit tests: ./gradlew test
- [ ] Run instrumented tests on multiple API levels
- [ ] Test on minimum supported SDK version
- [ ] Memory profiling with Android Studio
- [ ] Test with network throttling
- [ ] Verify on actual devices, not just emulator
```

**Web Testing**:
```markdown
- [ ] Run test suite: npm test / yarn test
- [ ] Cross-browser testing (Chrome, Firefox, Safari, Edge)
- [ ] Mobile responsive testing
- [ ] Performance profiling (Lighthouse)
- [ ] Network throttling tests
- [ ] Test with real user conditions
```

#### B. Universal Testing Checklist
- [ ] Original bug no longer reproduces
- [ ] All existing features still work
- [ ] No performance degradation
- [ ] No new warnings/errors in logs
- [ ] Edge cases handled
- [ ] Error states handled gracefully
- [ ] Offline/poor connectivity handled

### 7. DEPLOYMENT SAFETY

#### A. Platform-Specific Deployment

**iOS Deployment**:
```markdown
1. TestFlight Beta:
   - Deploy to internal testers first
   - Monitor crash reports for 24h
   - Deploy to external beta testers
   - Gather feedback for 48h
2. Phased Release:
   - 1% of users for 24h
   - 10% of users for 48h
   - 50% of users for 48h
   - 100% if metrics are stable
```

**Android Deployment**:
```markdown
1. Internal Testing Track:
   - Deploy to internal testers
   - Monitor crash reports for 24h
2. Staged Rollout:
   - 5% of users for 24h
   - 20% of users for 48h
   - 50% of users for 48h
   - 100% if metrics are stable
```

**Web Deployment**:
```markdown
1. Staging Environment:
   - Deploy and verify fix
   - Run smoke tests
2. Production Deployment:
   - Blue-green deployment if available
   - Feature flag for gradual rollout
   - Monitor error rates
   - Keep previous version ready
```

### 8. POST-FIX MONITORING

#### A. Platform-Specific Monitoring

**iOS**:
- [ ] App Store Connect: Check crash rates
- [ ] Analytics: Monitor user engagement
- [ ] Performance: Check app launch time
- [ ] Reviews: Monitor for new issues

**Android**:
- [ ] Play Console: Check crash rates, ANRs
- [ ] Analytics: Monitor user metrics
- [ ] Performance: Check app startup time
- [ ] Reviews: Monitor for complaints

**Web**:
- [ ] Error tracking: Monitor error rates
- [ ] Analytics: Check bounce rates
- [ ] Performance: Monitor Core Web Vitals
- [ ] User feedback: Check support tickets

### 9. DOCUMENTATION

#### A. Universal Fix Documentation
```markdown
## Issue: [Brief Description]
**Date**: [YYYY-MM-DD]
**Platforms Affected**: iOS / Android / Web / Backend
**Severity**: CRITICAL/HIGH/MEDIUM/LOW

### Root Cause
[Platform-agnostic explanation]
[Platform-specific details if relevant]

### Fix Applied
**Common Fix**: [What was changed across platforms]
**iOS Specific**: [If applicable]
**Android Specific**: [If applicable]
**Web Specific**: [If applicable]

### Files Modified
- iOS: `path/to/File.swift`
- Android: `path/to/File.kt`
- Web: `path/to/file.js`
- Shared: `path/to/shared/file`

### Rollback Instructions
[Platform-specific rollback steps]

### Prevention Measures
[How to prevent this across all platforms]
```

## PLATFORM-SPECIFIC COMMANDS

### iOS/macOS Debug Commands
```bash
# Xcode command line
xcrun simctl list              # List simulators
xcrun simctl openurl booted    # Test deep links
instruments -s devices         # List connected devices

# Crash logs
find ~/Library/Logs/DiagnosticReports -name "*.crash" -mtime -1
```

### Android Debug Commands
```bash
# ADB commands
adb logcat -c                  # Clear logs
adb logcat *:E                 # Show only errors
adb shell dumpsys activity     # Activity state

# Gradle commands
./gradlew clean build          # Clean rebuild
./gradlew dependencies         # Check dependencies
```

### Web Debug Commands
```bash
# NPM/Yarn
npm list                       # Check dependencies
npm audit                      # Security check
npm run build -- --source-map  # Debug build

# Browser debugging
console.trace()               # Stack trace
performance.mark()            # Performance tracking
```

## GOLDEN RULES FOR ALL PLATFORMS

1. **Test on real devices/browsers** - Simulators lie
2. **Check the basics first** - Often it's simple
3. **One change at a time** - Easier to track impact
4. **Document platform differences** - Each has quirks
5. **Monitor after deployment** - Issues can be delayed
6. **Keep fixes minimal** - Stability over elegance

Remember: In production, **WORKING > PERFECT** across all platforms.