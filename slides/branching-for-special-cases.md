#### Branching for special cases

```php
if ('http://example.com' === $_SERVER['HTTP_HOST']) {
	// Do something different.

} else {
	// Default behavior.
}
```

Note:

- Writing conditionals for special cases is a slippery slope
- Cyclomatic complexity
- Are there cleaner ways to apply this logic? Dependency injection?
- Should absolutely be tested
