# MereRouter

This is primarily for my own personal use. It works well for my projects where I have a PHP file for each page that needs to be included depending on the url. A htaccess rewrite rule must be defined for this to work.

Include in your project using Composer:

    "require": {        
        "fletcherjohns/mere-router": "v1.0.0"
    }

To register your endpoints, call static function `registerRoutes($routes)` passing an array in the following format.

    TestMereRouter::registerRoutes([

        'path-segment' => [

            MereRouter::GET => [
                MereRouter::PAGE => 'filename.php',
                MereRouter::METHOD => function() {
                    ...
                },
                MereRouter::PRIVILEGE => MEMBER,
                MereRouter::REDIRECT => 'home',
                MereRouter::ROUTES => [
                    ...
                ]
            ],

            MereRouter::POST => [
                ...
            ]
        ],

        'other-segment' => [
            ...
        ]
    ]);

Then at appropriate point in your code, call static function `processRequest()` which will select appropriate route, and depending on privilege level, run associated method and return page filename. If path segment is not found, or privilege not satisfied, a redirect will occur.

Only registered path segments and request methods will be processed, otherwise a redirect will occur.