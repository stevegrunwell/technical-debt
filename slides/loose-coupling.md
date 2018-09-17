#### Receipe Custom Post Type

```
# functions.php

// Load the Receipes functionality.
require_once __DIR__ . '/includes/recipe-cpt.php';
```
<!-- .element: class="fragment" -->

Note:

* Keep all of the recipe functionality in a single place, and just include it
    + Makes it easier to see how the functionality is related
    + If we don't need recipes down the road, remove the `require_once` statement and the file.
