Implement feature flags to enable safe deployment of new features, A/B testing, and gradual rollouts while maintaining code stability and allowing instant rollback capabilities.

## When to Use

- Rolling out a new feature gradually to a subset of users before full deployment
- Implementing A/B tests to compare different feature implementations
- Deploying code to production while keeping features disabled until ready
- Providing organization-level or user-level feature access control
- Testing features in production with internal users before public release

## Context Validation Checkpoints

* [ ] What is the scope of the feature flag (global, organization-level, or user-level)?
* [ ] What is the default state of the feature flag (enabled or disabled)?
* [ ] Where will the feature flag configuration be stored (database, config file, or external service)?
* [ ] Are there any dependencies between this feature and other feature flags?
* [ ] What is the rollout strategy (percentage-based, whitelist, or all-at-once)?

## Recipe Steps

### Step 1: Define Feature Flag Schema

Create a feature flag configuration schema with a unique key, description, default value, and scope (global/org/user level)

```typescript
interface FeatureFlag {
  key: string;
  description: string;
  enabled: boolean;
  scope: 'global' | 'organization' | 'user';
  rolloutPercentage?: number;
}
```

### Step 2: Create Feature Flag Service

Implement a service that checks feature flag status based on context (user, organization) and returns whether the feature is enabled

```typescript
class FeatureFlagService {
  async isEnabled(flagKey: string, context: { userId?: string; orgId?: string }): Promise<boolean> {
    const flag = await this.repository.findByKey(flagKey);
    if (!flag) return false;
    
    if (flag.scope === 'global') return flag.enabled;
    if (flag.scope === 'organization' && context.orgId) {
      return await this.isEnabledForOrg(flagKey, context.orgId);
    }
    // Additional scope checks...
    return flag.enabled;
  }
}
```

### Step 3: Add Feature Flag Guards

Wrap feature-specific code with feature flag checks to conditionally execute logic based on flag status

```typescript
if (await featureFlagService.isEnabled('new-analytics', { orgId })) {
  return await newAnalyticsEngine.process(data);
} else {
  return await legacyAnalyticsEngine.process(data);
}
```

### Step 4: Create Admin Interface

Build an admin UI or API endpoints to toggle feature flags without code deployment, allowing quick rollback if needed

### Step 5: Implement Frontend Feature Toggle

Create a React hook or context provider to check feature flags on the frontend and conditionally render components

```typescript
const { isEnabled } = useFeatureFlag('new-dashboard');

return (
  <>
    {isEnabled ? <NewDashboard /> : <LegacyDashboard />}
  </>
);
```

### Step 6: Add Monitoring and Analytics

Track feature flag usage and impact with analytics events to measure adoption and performance differences

### Step 7: Clean Up After Full Rollout

Once a feature is fully rolled out and stable, remove the feature flag code to reduce technical debt and simplify the codebase
