# What are macros in Laravel
Laravel allows us to create macros, it's like creating custom static methods for the classes. In this file you'll find lot of **cool** 😎 macros made by the community.

- [Estimated reading minutes](#estimated-reading-minutes)

## Estimated reading minutes
[Shared by LaraShout](https://twitter.com/LaraShout/status/1612101861892390912)  
If you're writing blogs it's always **cool** 😎 to have an estimation for the reading duration. With this macro you can do it easily!  

```php
// Register the macro inside of any provider's boot method
class AppServiceProvider extends ServiceProvider
{
  public function boot()
  {
    Str::macro('readingMinutes', funciton ($subject, $wordsPerMinute = 200) {
      return intval(ceil(Str::wordCount(strip_tags($subject)) / $wordsPerMinute))
    });
  }
}

// And use it anywhere!
Str::readingMinutes('Estimate this text!');
// And of course you can set a custom value for wordsPerMinute
Str::readingMinutes('Some text here...', 100);
```

