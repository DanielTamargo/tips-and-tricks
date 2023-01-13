# Route tips
Some useful tips for using routes in Laravel.

### Multiple ways to redirect users
```php
// 1- Redirecting to a raw URL
return redirect('/home');

// 2- Redirecting to a named route
return redirect()->route('home');

// 3- Redirecting to a controller's action
return redirect()->action([DashboardController::class, 'index']);

// 4- Since Laravel 9, redirecting to a named route with to_route helper
return to_route('home');
```

Options 2 and 4 do exactly the same, **`to_route`** helper was added in Laravel 9.