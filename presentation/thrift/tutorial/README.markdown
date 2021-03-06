## Apache Thrift Tutorial

This is a tutorial to guide through the basics of getting setup using the apache thrift project.


## Prerequisites
- Install Thrift
- Install PHP

### 101
Inside the 101 folder you'll find the examples from the Apache Thrift Website. If you enter this folder and run the following commands:
thrift -r --gen php tutorial.thift
thrift -r --gen java tutorial.thift

Two folders are created, gen-php and gen-java. If you examine these files you'll see the classes that have been generated from the .thrift files.

#### Basic User Model:
Create a thrift model based on the following object:
userId - 32 Bit Int
firstName - String
lastName - String

### Laravel API
Inside the lavel folder you'll find the base of a Laravel project that currently returns to the endpoint /user/{name}
with an XML represenation of a user class with the same structure - but written in a more traditional PHP Format.

composer install
php artisan migrate
php artisan serve

Add to app/Http/routes.php
```
Route::get('/user/{name}', function ($name) {
    $user = \App\User::all()->where('name', $name);
    $xmlSerialize = new \PhpParser\Serializer\XML();
    return $xmlSerialize->serialize($user->toArray());
});
```

TODO: Turn this into a migration
insert into users (name, email, password, created_at, updated_at) VALUES('testuser', 'testuser@paulsinternet.com', 'test', NOW(), NOW());

Visit: http://localhost:8000/user/testuser
(Chrome: inspect the DOM, you'll see it's XML returned)

##### Challenge 1:
Return an object that represents this same data, but in using the thrift models and returned as binary.

##### Challenge 2:
Based on the header, return the object in the original XML format.


