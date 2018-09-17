```php
/**
 * Get me some coffee.
 *
 * Before getting a cup, this method will first check to see if
 * more coffee needs to be brewed, which helps us avoid throwing
 * NoCoffee exceptions.
 *
 * @return Coffee Some fresh, hot coffee.
 */
public function getCoffee(): Coffee
{
	// ...
}
```

Note:

Consider the same function, but see how we've improved the documentation. Now, we can tell not only what the function does, but why (so we don't get the dreaded NoCoffee exception).
