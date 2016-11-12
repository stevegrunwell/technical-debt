#### Receipe Custom Post Type

```
# functions.php

// Load the Receipes functionality.
require_once __DIR__ . '/includes/recipe-cpt.php';
```
<!-- .element: class="fragment" -->

Note:

What if instead, we put all of the recipe-related functionality into a new file, recipe-cpt.php? We're using WordPress actions and filters to tie into the whole process anyway, and this lets us know that all the recipe-related stuff is happening in one place.

Now, we're able to just include the file from our functions.php file. Wow, that's a lot cleaner!

Down the road, if we decide we don't need the recipe functionality any more, we can just remove that `require_once` statement and recipe-cpt.php. Even if we just want to temporarily disable it, we can comment out the require_once line and it'll be as if that functionality never existed.
