# React-Inertia-Laravel-Test
Attempt to try react with laravel via inertia
## Guide:

### First create a laravel project
I used this method you can create on your own way 
```
composer global require laravel/installer
 
laravel new my-app
```
### Goto project directory by this command
```
cd my-app
```

### Install dependencies for inertia
```
composer require inertiajs/inertia-laravel
```

### Create a .blade.php file on "my-app\resources\views" and paste this code:
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
    @vite('resources/js/app.jsx')
    @inertiaHead
  </head>
  <body>
    @inertia
  </body>
</html>
```
I created app.blade.php file and pasted this code

### Install a middleware by this command
```
php artisan inertia:middleware
```

### Goto "my-app\app\Http\Kernel.php" and paste this code in $middlewareGroups array in web section
```php
    \App\Http\Middleware\HandleInertiaRequests::class,
```
This array might look like this:
```php
'web' => [
        \App\Http\Middleware\EncryptCookies::class,
        \Illuminate\Cookie\Middleware\AddQueuedCookiesToResponse::class,
        \Illuminate\Session\Middleware\StartSession::class,
        \Illuminate\View\Middleware\ShareErrorsFromSession::class,
        \App\Http\Middleware\VerifyCsrfToken::class,
        \Illuminate\Routing\Middleware\SubstituteBindings::class,
        \App\Http\Middleware\HandleInertiaRequests::class,
    ],
```

### Now, install some packages
```
npm install @inertiajs/react react-dom react @vitejs/plugin-react @inertiajs/inertia-react
```

### Create app.jsx file in "my-app\resources\js" and paste this code
You can delete app.js file present in the folder
```jsx
import { createInertiaApp } from "@inertiajs/react";
import { createRoot } from "react-dom/client";
import React from "react";

createInertiaApp({
    resolve: (name) => {
        const pages = import.meta.glob("./Pages/**/*.jsx", { eager: true });
        return pages[`./Pages/${name}.jsx`];
    },
    setup({ el, App, props }) {
        createRoot(el).render(<App {...props} />);
    },
});
```

### Create a folder named "Pages" in "my-app\resources\js" and create a file inside it named "Test.jsx"
Then write your own react code, for example
```jsx
import React from "react";

const Test = () => {
    return <div>Hi, this is a test page.</div>;
};

export default Test;
```

### Goto "my-app\routes\web.php" and call route like this
```php
Route::get('/', function () {
    // return view('welcome');
    return Inertia::render("Test");
});
```
Don't forget to import inertia
```php
use Inertia\Inertia;
```

### Run app
#### Open two terminal
In one run this command (make sure you are in my-app or in your laravel application folder)
```
npm run dev
```
In other one run this command
```
php artisan serve
```

Follow the link the php artisan created

### For more detailed guide follow this links
```
https://laravel.com/docs/10.x
https://inertiajs.com/
```

## Good luck 👋