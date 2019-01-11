# Model name

By default the model name is the name of the class \(case sensitive\).

For changing the model name use:

1. Class static method `setModelName(name:string)`:

   ```text
    Post.setModelName("posts");
   ```

2.  `@ModelName(name:string)` decorator:

   ```text
    @ModelName("posts")
    export class Post extends ModelAbstract{
    }
   ```

