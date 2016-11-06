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

Consider this rage() function – we give it a string, and it's going to make it all caps and append some exclamation marks.
