

## 1. Resource Controllers

## Creating a resource controller
- php artisan make:controller Product -r

## Creating a Model
- php artisan make:model Product -m

## Migrate fresh table
- php artisan migrate

## for an existing table if you edit
- php artisan migrate:refresh 

## Dependency Injection

## Create service


- mkdir app/Services
- touch app/Services/PostService.php
- Register post service in AppServiceProvider
- Inject the post service into the controller

## Create API 
- Run the command php artisan install:api
- Add post resource url to api route in the file routes/api.php 
- Test with Thunder Client

* All Posts :     (GET) http://internship:8000/api/posts
* Single Post :   (GET)  http://internship:8000/api/posts/1
* Update Post  :  (PUT)  http://internship:8000/api/posts/1
* Delete Post :   (DELETE)  http://internship:8000/api/posts/1
* Add Post :      (POST)  http://internship:8000/api/posts



## 2.  Laravel Events
# Observers 
- Observers in Laravel allow you to listen to events that occur on models. Events that can  occur, such as creating, updating, deleting
- Create an observer : php artisan make:observer PostObserver --model=Post
- In the PostObserver class, define the methods for the events you want to handle
- Register the Observer in app\Providers\AppServiceProvider


## Localization
Localization in Laravel allows you to manage and display your application in different languages. You create language files the languages and use them to display content based on the user's language preference.

- create a file in : resources/lang/en/messages.php
- You can set the default locale in the config/app.php file by modifying the locale option: ie to en or es, or change in .env
- reference it in your views

## 3. ELOQUENT RELATIONSHIPS 


Eloquent is the Object-Relational Mapper (ORM) included with Laravel. It provides a simple and intuitive Active Record implementation for working with your database. Each database table has a corresponding "Model" that is used to interact with that table. Eloquent models allow you to query for data in your tables, as well as insert new records into the table.

In Laravel, a relationship is a way to define the connection between two database tables. Laravel provides a powerful and expressive ORM (Object-Relational Mapping) called Eloquent, which makes it easy to interact with the database and define relationships. Eloquent relationships allow you to query related data and work with your database using an object-oriented approach.

# One to One relationships & One To Many
- php artisan make:model Product -m
- php artisan make:model Category -m
- php artisan make:controller ProductController --resource
- php artisan make:controller CategoryController --resource
- create the views for the products crud
- create the views for the categories crud


## key Points
- One-to-One: One record in the first table is related to one and only one record in the second table.
- One-to-Many: One record in the first table is related to multiple records in the second table
- One-to-One: Used when there is a strict one-to-one correspondence between records
- One-to-Many: Used when one record in the first table can have multiple associated records in the second table.

## Many To Many Relationships
- Article Table: php artisan make:model Article -m
- Tage Table : php artisan make:model Tag -m
- Pivot Table ; php artisan make:migration create_article_tag_table --create=article_tag
- php artisan make:controller ArticleController --resource
- create the views for the articles crud

## Add data to your database for testing, Add Tags to tags table
- capture name ( add 4 tags)
- Test the many to many relationships


# 4. CSRF protection
- Cross-Site Request Forgery (CSRF) protection is a security measure to prevent unauthorized commands from being transmitted from a user that the web application trusts. Laravel provides built-in CSRF protection to guard against these types of attacks.

## How it works
- Laravel automatically generates a CSRF token for each active user session managed by the application.
- This token is stored in the session and can be accessed using the csrf_token() helper function.
- When creating forms in Laravel, you can include the CSRF token as a hidden input field. This can be done using the @csrf Blade directive.
- The @csrf directive will generate a hidden input field with the CSRF token value.
- When a form is submitted, Laravel automatically verifies that the request includes a valid CSRF token.
- This verification is done by checking the token submitted with the form against the token stored in the session.
- If the tokens do not match, the request is rejected with a 419 HTTP status code, indicating that the CSRF token verification failed.
- By using Laravel's built-in CSRF protection, you can help secure your application against CSRF attacks if tokens done match, the request is rejected.

## Test the csrf token
- Go to your form and insert the @csrf 
- Go to controller and die dump the request on store method dd($request->all());
- Inspect the browser code , with Dev Tools , and View page source :: check if token exists
- check if token in dd is same as token when you view page source
- check sample file in csrf_attacks/csrf_attacks.blade.php


## Form input validation
- php artisan make:request StoreProductRequest
- Add custom rules and messages
- Import the use App\Http\Requests\StoreProductRequest in your Product Controller
- Pick the validations from the Products/Create and test


## ERROR HANDLING
- Using validations , test in ProductController@store
- Exeption using Try Catch : Test in PostController@show, delete
- Using Logs ( check : PostObserver.php and test logging)
- Error Custom Views/Pages


## Custom error pages
. create an error file in : resources/views/errors
. create 404.blade.php
. create 500.blade.php

## Testing Error pages
- put a wrong page route to test 404
- rename .env to .env2 to create a server error 500
