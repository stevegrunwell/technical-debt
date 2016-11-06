#### Branching for special cases

```php
if ('http://example.com' === $_SERVER['HTTP_HOST']) {
	// Do something different.

} else {
	// Default behavior.
}
```

Note:

One of the easiest ways for your application to get out of control is by writing conditionals that branch the logic based on special cases.

How will you test that? Will you remember to test that branch of logic?

In these cases, it's best to take a step back and see if there are cleaner ways to apply this custom logic; does your application support any sort of hook system where you can adjust the logic in a particular environment? Can you create something like a child theme or a plugin that makes that functionality change more explicit?
