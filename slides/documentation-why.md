```php
/**
 * Get me some coffee.
 */
public function getCoffee(): Coffee
{
	$pot = $this->getCoffeePot();

	if (! $pot->hasCoffee()) {
		$pot->makeCoffee();
	}

	return $pot->getCup();
}
```

Note:

Consider this getCoffee() function which, from the documentation, we know gets us some coffee.

Unfortunately, that's literally all the docs tell us; why do we have this conditional around $pot->hasCoffee()?
