Phalcon Rest JWT
=================

First of all i wanna give credits to CMOORE, Jeteokefe and Redound for their outstanding Phalcon Rest API Frameworks, i have learned a lot from your work, i took some of your code integrated them to create my own version of PhalconRest Micro Framework with JWT and ACL.


This project uses Phalcon Micro Framework for REST API with JWT and ACL
---------------------------------------------------

The purpose of this project is to have a base Phalcon REST API framework with JWT and ACL applied. And also to apply some practices done by Cmoore, Jeteokefe and Redound. 

This project idea is a collection of different approaches from the most popular phalcon rest api frameworks created, together with some of my ideas which i thought of enhancements.

Things that i have done: I added an easy to setup routes for each collections separated in each file, a JWT authentication event, and an ACL records checking event for each user, response and request envelopes (request class is from redound). You may find some of the codes familiar, i have added comments to credit the code owner and also to identify which are my creations.

Because phalconphp is all about speed and usability, using kcachegrind and xdebug to check when having a huge large route collection, still works fine but as suggestion in the phalcon documentation use cache. ( Caching of routes is next release.)

Why do this?
http://www.thebuzzmedia.com/designing-a-secure-rest-api-without-oauth-authentication/

Requirements
---------
-PHP 5.4 above until 7
-Phalconphp 2 until 3
-PDO-MySQL

Configuration (Database, URL's, Redis and Others)
--------------
Open  `/app/config/` and and create your own config.<your-desired-name>.php setup your database connection credentials and other configuration credentials

Change the env ```env => 'dev'``` to prod when your on the production server.

```php

```


Setup and Installation
--------------

If you are in Linux or Mac run the setup.sh by passing your config name in used in the <your-desired-name>

Example:

```bash
bash setup.sh ef
```

You can setup it manually:

1. by copying your configuration in dist/config into the app/config
2. change the value of the APP_ENV in the public/index.php to youre-desired-name in your config filename
3. create a cache folder in app because it is being ignored by .gitignore

Database Migration
-------------

When you want to migrate database only use the following command:

```bash 
bash migratesql.sh <host> <username> <password> <type> <databasename>
```

Routes
-------------
Routes are stored in `app/routes/nameRoute.php` as an object. A route has a method (GET, POST, DELETE, PUT, MAP(post or get)).

Conventions:

1. All lower case
2. ACL should depend on the roles on the database, You can have multiple ACL for routes
3. After adding your own route go to app/library/app/bootstrap/CollectionBootstrap.php and add your route. 
4. 

```php
namespace App\Routes;
use PhalconRestJWT\App\Resources;

class ExampleRoute extends Resources {
    public function initialize()
    {
        $this
            ->handler('App\Controllers\ExampleController')
            ->lazy(true)
            ->collections([
                "/testpost" => [
                    'post',
                    'newnewsample',
                    false,
                    's1',
                ],
                "/testget/{id}" => [
                    'get',
                    'testAction',
                    false,
                    's2'
                ],
                "/authtest" => [
                    'post',
                    'testAuth',
                    false,
                    's3'
                ],
                "/ping" => [
                    'map',
                    'pingAction',
                    true,
                    ['s4', 's2']
                ]
            ]);
    }
}
```

Note: For Routes with Paramters, make sure the action you map to has the proper parameters set (in order to read paramters correctly). 
http://docs.phalconphp.com/en/latest/reference/micro.html#defining-routes

Client Requirements
-------------
PHP 5.3+

Required PHP Modules
- Curl (http://php.net/curl)

To check for that module
```bash
$ php -m | grep -i "curl"
curl
```

Server Test
-------------


Next Release
-------------

- fixing ACL
- applying multiple assignment to a single route