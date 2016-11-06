#### Recipe Custom Post Type

* <!-- .element: class="fragment" -->`register_my_custom_post_type()`
* <!-- .element: class="fragment" -->`register_custom_metabox()`
* <!-- .element: class="fragment" -->`metabox_callback()`
* <!-- .element: class="fragment" -->`stuff_to_do_on_post_save()`
* <!-- .element: class="fragment" -->`custom_front_end_template_tags()`

Note:

Let's take a look at a WordPress example: let's imagine we're registering a custom post type for recipes.

We'll definitely have our function that registers the post type, but we'll probably need a custom meta box too, so let's register that.

Of course, if we register a custom meta box, we need the callback to print the content. Then we need to save that custom meta.

Oh, and maybe we need some custom template tags to display it on the front-end...wow, we haven't done much but that's a lot of stuff going into functions.php.