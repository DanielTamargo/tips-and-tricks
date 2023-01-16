# Test tips? Test tips!
Test is that **cool** 😎 thing that most of the developers avoid or ignore, but did you know that testing your code will not only help you with code integrity but also with developing better code skills? If you test your own code you'll learn about your mistakes, for example, if your code doesn't follow good practices, testing that code will be a nightmare and you'll learn how to set your code structure much better, trust me!  

- [Custom validation rule](#test-a-custom-validation-rule)


### Custom validation rule
You can pass the rule as param and use the method **`toPassWith`** and check if the value passed correctly! **Cool**, right? 😎
```php
it('will only pass uppercased strings', function() {
  $rule = new UppercaseRule();

  expect($rule)->toPassWith('HELLO');
  expect($rule)->not()->toPassWith('hello');
});
```