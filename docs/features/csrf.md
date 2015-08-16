---
title: CSRF Protection
---

Slim 3 uses the optional standalone [slimphp/Slim-Csrf](https://github.com/slimphp/Slim-Csrf)
PHP component to protect your application from CSRF (cross-site request forgery).
This component generates a unique token per request that validates subsequent
POST requests from client-side HTML forms.

## Installation

Execute this bash command from your project's root directory:

{% highlight bash %}
composer require slim/csrf
{% endhighlight %}

## Usage

The `slimphp/Slim-Csrf` component contains an application middleware. Add it
to your application like this:

{% highlight php %}
// Add middleware to the application
$app = new \Slim\App;
$app->add(new \Slim\Csrf\Guard);

// Create your application routes...

// Run application
$app->run();
{% endhighlight %}

## Fetch the CSRF token name and value

The latest CSRF token's name and value are available as attributes on the
PSR7 request object. The CSRF token name and value are unique for each request.
You can fetch the current CSRF token name and value like this.

{% highlight php %}
$app->get('/foo', function ($req, $res, $args) {
    // Fetch CSRF token name and value
    $name = $req->getAttribute('csrf_name');
    $value = $req->getAttribute('csrf_value');

    // TODO: Render template with HTML form and CSRF token hidden field
});
{% endhighlight %}

You should pass the CSRF token name and value to the template so they
may be submitted with HTML form POST requests. They are often stored as a hidden
field with HTML forms.