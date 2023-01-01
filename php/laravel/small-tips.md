# Small tips
Here you'll find small and concise but powerful tips. Feel free to explore them!  

- [Default password requirements](#default-password-requirements)

## Default password requirements
> **Tags**: security, password, validation rule  
> **Version**: Laravel v8.39 or superior

```php
// Add the configuration in a service provider
// File: app/Providers/AppServiceProvider.php
use Illuminate\Validation\Rules\Password;

class AppServiceProvider
{
    public function boot(): void
    {
        // Configure default requirements for password
        Password::defaults(function () {
            return Password::min(8) // at least 8 characters
                ->letters() // at least one letter
                ->numbers() // at least one number
                ->symbols() // at least one symbol
                ->mixedCase() // at least one uppercase and one lowercase letter
                ->uncompromised(); // has not been compromised in data leaks
        });
    }
}


// Then when you need it in the controller or the form request add the rule
$request->validate([
  ['password' => ['required', Password::defaults()]],
]);
```
**Note:** the `uncompromised()` method checks the password against a verification API to see if the password appears in data leaks. It uses the [NotPwnedVerifier](https://github.com/laravel/framework/blob/9.x/src/Illuminate/Validation/NotPwnedVerifier.php) implementation which checks password leaks using [Have I Been Pwned API](https://haveibeenpwned.com/API/v3). It was implemented in Laravel v8.39.