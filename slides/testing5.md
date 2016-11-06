```php
/**
 * Convert a string to all caps and append an exclamation mark.
 *
 * @param string $string The string to yell from the rooftops.
 * @return string The string, but louder.
 */
function rage($string) {
	return strtoupper($string) . '!!!';
}
```

Note:

Fortunately for us, `strtoupper()` is designed to work on strings, so we can cut the array portion out entirely.
