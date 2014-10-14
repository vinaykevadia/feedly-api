**NOTICE** You can find the first edition of my code here [dev](https://github.com/stakisko/feedly-api/tree/legacy)


feedly-api
=========
PHP wrapper around [Feedly's REST API](http://developer.feedly.com/).

**Under Construction! Not every API's functionality implemented yet.**

[![Build Status](https://travis-ci.org/stakisko/feedly-api.svg?branch=dev)](https://travis-ci.org/stakisko/feedly-api)

Notes
-----
Check the [examples](https://github.com/stakisko/feedly-api/blob/master/example) before anything.

If you are working in Sandbox mode of Feedly's API you should know a couple of things.

* Your Client's ID, secret must taken from [here](https://groups.google.com/forum/#!topic/feedly-cloud/a_cGSAzv8bY), which is updated very often so be sure to check it once in while.
* While in Sandbox mode, only "http://localhost" is permited for callback url. So leave it as is and just replace it every time with your domain, if it's different. You can also add you own to permitted domains [here](https://groups.google.com/forum/#!topic/feedly-cloud/vSo0DuShvDg/discussion).
* Once you've done developing you can contact Feedly and ask them to put you on [production](http://developer.feedly.com/v3/sandbox/).


Instalation
-----------
Add this to your composer.json
```
"require": {
        "kbariotis/feedly-api": "dev-master"
    }
```

Or download the [ZIP](https://github.com/stakisko/feedly-api/archive/master.zip).

Documentation
-------------

**Constructor:**

```php
$sandbox=FALSE;
$storeAccessTokenToSession=TRUE;

$feedly = new Feedly($sandbox, $storeAccessTokenToSession);
```

Authentication:
--------------

Check the [example](https://github.com/stakisko/feedly-api/blob/master/example/authentication.php).

Note that not every Feedly actions need authentication. Passing a token is optional.

Endpoints
-------------

[**Profile:**](http://developers.feedly.com/v3/profile/)

```php

    $profile = $feedly->getEndpoint('Profile');

    var_dump($profile->fetch());

    $profile->setOptions(array(
        'email'=>'odysseus@ithaca.gr'
    ));

    $profile->persist();
```

[**Categories:**](http://developers.feedly.com/v3/categories/)

```php

    $categories = $feedly->getEndpoint('Categories');

    var_dump($categories->fetch());

    $categories->changeLabel($id, 'New Label');

    $categories->delete($id);
```

[**Entries:**](http://developers.feedly.com/v3/entries/)

```php

    $entries = $feedly->getEndpoint('Entries');

    var_dump($entries->get($id));

```

[**Markers:**](http://developers.feedly.com/v3/markers/)

```php

    $markers = $feedly->getEndpoint('Markers');

    var_dump($markers->get($id));

    var_dump($markers->getUnreadCount());

    $markers->markArticleAsRead(array(
        'TSxGHgRh4oAiHxRU9TgPrpYvYVBPjipkmUVSHGYCTY0=_14499073085:c034:d32dab1f',
        'TSxGHgRh4oAiHxRU9TgPrpYvYVBPjipkmUVSHGYCTY0=_1449255d60a:22c3491:9c6d71ab'
    ));

    $markers->markArticleAsUnread(array(
        'TSxGHgRh4oAiHxRU9TgPrpYvYVBPjipkmUVSHGYCTY0=_14499073085:c034:d32dab1f',
        'TSxGHgRh4oAiHxRU9TgPrpYvYVBPjipkmUVSHGYCTY0=_1449255d60a:22c3491:9c6d71ab'
    ));

    $markers->markFeedAsUnread(array(
        'feed/http://feeds.feedburner.com/design-milk'
    ));

    $markers->markFeedAsUnread(array(
        'user/c805fcbf-3acf-4302-a97e-d82f9d7c897f/category/design',
        'user/c805fcbf-3acf-4302-a97e-d82f9d7c897f/category/photography'
    ));

```

Licence
--------------------
```
The MIT License (MIT)

Copyright (c) 2014 Konstantinos Bariotis

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```
