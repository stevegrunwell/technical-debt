```php
public function testRage()
{
	$this->assertEquals('HELLO!!!', rage('hello'));
}
```

Note:

Now, consider a very simple PHPUnit test for the function: we pass "hello" in all lowercase, and we expect to receive "HELLO!!!" in all caps with three exclamation marks.
