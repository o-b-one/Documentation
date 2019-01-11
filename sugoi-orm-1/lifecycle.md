---
description: SugoiJS supply predefined ORM lifecycle
---

# Lifecycle

### Save & Update

SugoiJS ORM uses predefined lifecycle hooks that can be implemented by interfaces:

1. IBeforeValidate
2. IValidate
3. IBeforeSave / IBeforeUpdate
4. IAfterSave / IAfterUpdate

![SugoiJS save and update lifecycle hooks](../.gitbook/assets/lifecycle.png)

### Find & Remove

1. IBeforeFind/IBeforeRemove
2. IAfterFind/IAfterRemove

![SugoiJS find and remove lifecycle hooks](../.gitbook/assets/image.png)

