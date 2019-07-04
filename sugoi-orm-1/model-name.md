# Model name

By default the model name is the name of the class \(case sensitive\).

For changing the model name use:

1. Class static method `setModelName(name:string)`:

   ```typescript
    Post.setModelName("posts");
   ```

2.  `@ModelName(name:string)` decorator:

   ```typescript
    @ModelName("posts")
    export class Post extends ModelAbstract{
    }
   ```

