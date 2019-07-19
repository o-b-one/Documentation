---
description: Use building configuration from configuration files
---

# Get build configuration

## Overview

As mentioned on the [configuration under cli](configurations.md#configuration-files), we can define configuration which will be injected during build time\(only when building using Sugoi/cli\).

## Resolving configuration

All of the passed configuration is stored under the configuration container of @sugoi/core in a map where the key is the name of the file \(without suffix\) and the value is the object the file contained.

For resolving the configuration both @sugoi/core and @sugoi/server expose the `getConfiguration(configurationKey?: string)`method, when no argument pass the entire configuration map will return.

### Example:

#### Using core

```typescript
import { getConfiguration } from '@sugoi/core';

const deploymentVars = getConfiguration('deployment_variables');
Logger.setDebugLevel(deploymentVars.debugLevel);
```

#### Using server

```typescript
import { getConfiguration } from '@sugoi/server';

const deploymentVars = getConfiguration('deployment_variables');
Logger.setDebugLevel(deploymentVars.debugLevel);
```

