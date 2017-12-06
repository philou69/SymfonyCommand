Welcome
This tutorial is made for helping you to use the new Symfony 4.

Summary:
* [Starting project](#starting-project)
* [Developpement's Web Server](#developement-s-web-server)
* [Checking the environment](#checking-the-environment)
* [Securing the dependencies](#securing-the-dependencies)
* [Using annotation's route](#using-annotation-s-route)
* [Web Debugging](#web-debugging)
* [Rendering a Template ](#renderind-a-template)
* [Using the Session](#using-the-session)
* [Using Asset Package](#using-asset-package)
* [Using Database and Doctrine](#using-database-and-doctrine)
* [Using the Form component](#using-the-form-component)
* [Manange the security](#manage-the-security)
* [Sending email](#sending-email)

# Starting a project
For starting a new project we have to using composer and execute the following command :
 
```composer create-project myNewProjet ["3.*.*"]```

The part in [] is optionnal, that allow you to choose a specific version.

# Developpement's Web Server
For developing your application, you have several choices. 

* Using the PHP's server with the command ```php -S localhost:8000```
* Using a personal web server like WAMP, XAMP or even LEMP
* Or you can use the Symfony's web server. For this, you have to adding the server bundle with ```composer require server```

The word server is an alias for 'symfony/web-server-bundle'. Symfony has adding the Flex component who allow you to using alias like server, mailler, ...
Flex, also, hepling us about configuration and for removing a bundle. See more [here](https://symfony.com/doc/current/setup/flex.html)

The Symfony's server is pretty simple to use it like usual. 
You can launch it with :
```php bin/console server:run```
If you want to let it run :
```php bin/console server:star```

You can go to localhost:8000 to see the Symfony's homepage.
For more about Symfony's server, go [link](https://symfony.com/doc/current/setup/built_in_web_server.html)

# Checking the environment

If you want to be sure that your server support Symfony, you can use the requirements checker.
Firstable, on your project directory, install the requirement checker :
```composer require req-checker```

This command create 2 files. The first file is vendor/bin/requirements-checker. It check if your CLI environement is good, so launch it like this :
```php vendor/bin/requirements-checker```
The second is public/check.php. It tells you if your web server environment is ok. 
Launch that file on your browser. 
After fixed any issues, remove the component
```composer remove req-checker```

# Securing the dependencies
Symfony provide you a security checker how tell you all security vulnerabilty know about your project's dependencies.
Like ussually, for using it lunch the composer command :
```composer require sec-checker```
This utility is run automaticly when you install or update dependencies which meen that you see a clear message warning you about vulnerability

# Using annotation's route
With Symfony, you can use annotation for routes
```
	<?php 
	
	use Symfony\Component\Routing\Annotation\Route;
	
	 class DefaultController 
	 {

		/**
		 * @Route("path/we/want")
		 */
		public function home 
		{
			// code who return a Response
		}
	 }
```

In that case, you have to use the annotation bundle

```composer require annotation```

# Web Debugging

Symfony provide us a huge tool for debugging web application on browser, it's the Web Debug Toolbar(WDT)
```composer require --dev profiler```
Ẁe adding --dev flag because the WDT display a lot of information and  for security that does'nt be use on the prod server
You can find more about the profiler [here](https://symfony.com/doc/3.3/reference/configuration/web_profiler.html)

# Rendering a Template 

For your views, you can using php like you doing before, or you can using twig, the powerfull templating language of Symfony.
Using the traditional command :
```composer require twig```

Than you have two things to do.
First extends all your controllers to the basic controller for using the render function.
```
use Symfony\Bundle\FrameworkBundle\Controller\Controller;

class MyController extends Controller
{
	public function home()
	{
		return $this-render("home.html.twig");
	}
}
```

The second is to call all your view's file with the .twig extension.

For more about twig go [here](https://symfony.com/doc/3.3/reference/configuration/web_profiler.html) or [here](https://twig.symfony.com/)

# Using the Session
For using the session service, you have to activate him.
```
#config/packages/framework.yaml
framework:
	# ...
	
	#Uncomment this following lines:
	session:
		# The native PHP session handler will be used
		handler_id: ~

	#...
```

Now you can use it with the SessionInterface
```
use Symfony\Component\HttpFoundation\Session\SessionInterface;
public function index(SessionInterface $session)
{
	// Storing an attribute
	$session->set('foo', 'bar');

	// Get an attribut 
	$foobar = $session->get('foobar');
}
```

You can see more [here](https://symfony.com/doc/current/session.html)

# Using Asset Package

When many web sites using assets like css or js file or images, you can use the Asset package who allow you to calling dynamically path.
For using it, you have to install it 
```composer require asset```

Then you can use the asset() Twig function on your template file
```
#template/base.html.twig
<img src="{{ asset('images/logo.png) }}" alt='my logo' />

<link href="{{ asset('css/main.css" rel="stylesheet" />
```

You have to storage all of your assert on the public file.

For see more, you can go [here](https://symfony.com/doc/current/best_practices/web-assets.html)

# Using Database and Doctrine
Unsrtaed hardocing data on view, you storage them in a SQL database and display them dynamically. For helping you, Symfony integrate the third-party Doctrine ORM. 
You install her with composer
```composer require doctrine maker```
maker is for the MakerBundle, you can read [more](https://symfony.com/doc/current/bundles/SymfonyMakerBundle/index.html)

Now, you have installing the Doctrine ORM, you have to configure the connection to the database. So edit the .env like this 
```
# .env

# customize this line!
DATABASE_URL="mysql://db_user:db_password@127.0.0.1:3306/db_name"

# to use sqlite:
# DATABASE_URL="sqlite:///%kernel.project_dir%/var/app.db"
```
Ìf you does'nt all ready create the db_name, Doctrine can do that for you 
```php bin/console doctrine:database:create```
You can find more [here](https://symfony.com/doc/current/doctrine.html)


# Using the Form component
You want to use form in your web app for many things like store data in database, let user contact you ...
You can install the Form package 
```composer require form```

You can see more [here](https://symfony.com/doc/current/forms.html)

# Manange the security
For manage the security of your web app, you can use the Security Package
```composer require security```
Then you can create a firewal, a user's connetion, banishing IP....
You can see more [here](https://symfony.com/doc/current/security.html)

# Sending email
You may want to send emails for reset password or activate profil or anything else.
For helping you, Symfony provide you the SwiftMailerBundle
```composer require mailer```
You can see more [heere](https://symfony.com/doc/current/email.html)