# PHP-script-wrapper-for-reddit
A wrapper for reddit's API using the password grandtype

This wrapper utilizes reddit's "password" grand_type to allow people to make cron driven scripts/bots. If you are looking for a wrapper to allows users to login to your script I reccomend looking in [/u/jcleblanc's php wrapper](https://github.com/jcleblanc/reddit-php-sdk). 

# Usage 

Go to your reddit [app preferences](https://www.reddit.com/prefs/apps/) and create a new app of the script type. The redirect uri can be fictional as it will not be used. 

You can then simply use it as follows

```php
<?php
require('reddit.php');


$reddit = new Reddit("USER", "PASS", "CLIENT_ID", "CLIENT_SECRET"); 

$raw = $reddit->getRaw('r/history.json');

$reddit->submitComment('t3_IDGOESHERE', 'test');

?>
```

When succesfull the wrapper will return a object containing both a header and body property. The header contains the return headers from curl, which allow you to implement rate limiting in a way you see fit. The body contains the json as returned by reddit converted to an object. 

In case of a failure on authentication level the wrapper will die.

When the API returns errors it will throw an exception for those specific calls and return those instead of the object payload. 

# Api methods 

Very much a work in progress

## getRaw

Allows you to do a get request for any reddit url. Simply input the part after ```reddit.com/``` so for example for ```https://www.reddit.com/r/history.json``` you use ```r/history.json```

```php
$reddit->getRaw('r/history.json');
```

## getMe

```php
$reddit->getMe();
```

## getMeKarma

```php
$reddit->getMeKarma();
```

## getMePrefs

```php
$reddit->getMePrefs();
```

## getListing

Get a listing of a subreddit. Takes a subreddit (when not provided defaults to all) without /r/ and an array of GET parameters 

```php
$reddit->getListing('history', array("limit" => 1));
```

## submitComment

Submit a comment, takes a fullname and comment content as input. 

```php
$reddit->submitComment('t3_IDGOESHERE', 'test');
```



