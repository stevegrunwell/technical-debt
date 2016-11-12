```php
/**
 * Convert a string to all caps and append an exclamation mark.
 *
 * @param string $string The string to yell from the rooftops.
 * @return string The string, but louder.
 */
function rage($string) {
	$letters = str_split($string);
	$letters = array_map('strtoupper', $letters);

	return implode('', $letters) . '!!!';
}
```

Note:

Looking at our function again, that looks like it'll work, but we also have this weird str_split() thing going on; whoever wrote this seemed to think it made sense to convert the string to an array before we process it, then re-combine it using implode().
