# Performance tips
It is always **cool** 😎 to improve the performance of your applications, right?  

Here you'll find out some Laravel tips that will increase the performance of your applications.  

- [Replace "Chunk and then foreach" with simply "each"](#replace-the-usage-of-chunk-and-then-foreach-with-the-method-each)
- [Avoid lazy loading when you'll need the data](#avoid-lazy-loading-when-youll-need-the-data)

## Replace the usage of Chunk and then foreach with the method each
> **Tags**: eloquent, performance, readability

If you have a lot of data to process instead of retrieving all the data you can do it with chunks and then running through results with a foreach, but you can simplify it with the each method!
```php
// If you have many users registered, retrieving all of them will impact your application so much
// ❌ Bad performance!
User::all(); // <- be careful!
foreach ($users as $user) {
    Mail::to($user)->send(new PaymentNotification());
}

// So if you already know there are a lot of data, you can go through them in chunks!
// ✅ Good performance!
$chunk_size = 100;
User::query()
    ->where('payment_status', 'success')
    ->chunk($chunk_size, function ($users) {
        foreach ($users as $user) {
             Mail::to($user)->send(new PaymentNotification());
        }
    });

// But maybe the readability of the previous code is not that good... so here's another way!
// ✅ Good performance AND better readability ✅
User::query()
    ->where('payment_status', 'success')
    ->each(function ($user) {
        Mail::to($user)->send(new PaymentNotification());
    }, $chunk_size); // 👈 Default chunk size is 1000
```


## Avoid lazy loading when you'll need the data
> **Tags**: eloquent, performance  

When you need to load any models relationship you have two different approach, lazy load and eager load. 
In only a few words, it's called **lazy loading** when you load the data the moment you try to access it, and **eager loading** when you pre-load the data because you know that you'll have to access to that data.  

Replacing lazy loading with eager loading will resolve the N+1 query problem.  
Let's compare both approachs.

### Lazy loading example
```php
// Imagine you have 20 users registered
// ❌ Lazy Loading
$users = User::all(); // Executes 1 query: select * from users
foreach ($users as $user) {
  $userPosts = $user->posts; // Executes 1 query everytime: select * from posts where user_id = ?
}
// Total queries: 21 (1 to retrieve all users, 1 to retrieve each user's posts)
```

### Eager loading example
```php
// Imagine you have 20 users registered
// ✅ Eager Loading
$usersWithPosts = User::with('posts')->get(); // This executes 2 queries
// 1- select * from users
// 2- select * from posts where user_id IN (1, 2, 3, 4, ..., 20)

foreach ($users as $user) {
  $userPosts = $user->posts; // no query executed
}
// Total queries: 2 (1 to retrieve all users, 1 to retrieve all users' posts)
```

**IMPORTANT**: only use eager loading **when you will need the data**, otherway you'll be loading unnecesary data ending up with losing performance and that's **not cool**.  

By the way! this was a basic example, if you want to learn more about lazy and eager loading, feel free to explore these links!  
- [Laravel official docs: Eager Loading](https://laravel.com/docs/9.x/eloquent-relationships#eager-loading)
- [Laravel official docs: Preventing unnecesary lazy loading](https://laravel.com/docs/9.x/eloquent-relationships#preventing-lazy-loading)
- [Laravel Daily: Avoid N+1 queries](https://www.youtube.com/watch?v=bLWYbyKcfYI&ab_channel=LaravelDaily)
