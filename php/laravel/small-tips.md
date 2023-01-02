# Small tips
Here you'll find small and concise but powerful tips. Feel free to explore them!  

- [Default password requirements](#default-password-requirements)
- [Loop variable in Blade](#loop-variable-in-blade)

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

## Loop variable in Blade
> **Tags**: blade, view, loop  

When you have a collection that you want to print into the view, you use the Blade's `foreach` directive.  
```php
@foreach ($posts as $post)
    <div class="post">
        <h2>{{ $post->title }}</h2>
        <p>{{ $post->description }}</p>
    <div>
@endforeach
```
What you might don't know is that **inside Blade's foreach directive, you can use the `$loop` variable**, which has some cool values
```php
$loop->index // Index of the current loop iteration (starts at 0)
$loop->remaining // The remaining iterations in the loop
$loop->first
$loop->last
$loop->even
$loop->odd

// And also, if you're nesting loops
$loop->parent // the parent's loop variable
// For example:
$loop->parent->first
```
And there are more! [You can check them in the documentation.](https://laravel.com/docs/9.x/blade#the-loop-variable).  

So now, for example you could add some styles using [Blade's conditional classes](https://laravel.com/docs/9.x/blade#conditional-classes) and even if you show a list of posts and its comments and only want to add custom styles for first post's comments, you could do it easily!  
```php
@foreach ($posts as $post)
    <div @class([
        'post', 
        'first-post' => $loop->first, 
        'even-post' => $loop->even
    ])>
        <h2>{{ $post->title }}</h2>
        <p>{{ $post->description }}</p>
        @foreach($posts->comments as $comment)
                <div @class([
                    'comment', 
                    'first-post-comments' => $loop->parent->first, 
                ])>
                    <h3>{{ $comment->author }}</h3>
                    <p>{{ $comment->message }}</p>
                </div>
        @endforeach
    </div>
@endforeach
```

