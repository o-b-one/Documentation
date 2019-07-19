# sugoi.json

## Overview

The sugoi.json file is defining the structure of the project and provide information for the building process.  
Using the sugoi.json file we are possible to define multiple micro-services under the same workspace \(root directory\)

### Structure

```javascript
{
  "version": "4.0.0",
  "workspace": "Your Project workspace",
  "projects":{ 
  // your projects which you can select in building process using --project=name flag
    "main": { 
      "entry": "src/app/server.ts", // entry point of the project
      "dist": "dist/main",// where to export the file
      "configurationDir": "configuration", // Where to resolve the configuration from
      "excludes": [], // path to exclude from building
      "includes": [] // path to include in building
    },
    "auth": {
      "entry": "src/app/auth.ts",
      "dist": "dist/auth",
      "configurationDir": "configuration",
      "excludes": [],
      "includes": []
    }
  }
}
```

