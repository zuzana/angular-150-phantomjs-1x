# angular150-phantomjs1x

## Why

This project is to demonstrate problem with Phantomjs and Angular 1.5

This project is generated with yo angular generator version 0.15.1. I only changed package.json to demonstrate the problem with PhantomJs 1.x.

## Step by Step

1. Prepare project

        git clone https://github.com/zuzana/angular-150-phantomjs-1x.git
        cd angular-150-phantomjs-1x
        npm install
        bower install

1. Run project, it is working well.

        grunt serve

1. Run tests - there is only one in `test\spec\controllers\main.js`.

        grunt test

    Tests are failing.

1. **First possible solution:** Update phantomjs from 1.x to 2.x (npm package changed name to phantomjs-prebuilt) and update karma-phantomjs-launcher from 0.2.3 to 1.0.0

        npm uninstall phantomjs --save-dev
        npm install phantomjs-prebuilt --save-dev
        npm install karma-phantomjs-launcher@1.0.0

1. Run tests again - now all is well.

        grunt test

1. Second possible solution: Keep PhantomJS 1.x and karma-phantomjs-launcher 0.2.3 and add [phantomjs-polyfill](https://github.com/tom-james-watson/phantomjs-polyfill).
    Btw. I tried [mozilla polyfill](https://github.com/kdimatteo/bind-polyfill), but that was not working as well.

        npm uninstall phantomjs-prebuilt --save-dev
        npm install phantomjs@1.9.19
        npm install karma-phantomjs-launcher@0.2.3

        npm install phantomjs-polyfill --save-dev

1. Now uncomment line 24 in `test/karma.conf.js` (`// PHANTOMJS POLYFILL`)

1. Run tests again - now all is well.

        grunt test

Angular commit that most likely caused this issue is following: https://github.com/angular/angular.js/commit/1c6edd416b4baad0c8b01148f429eb78e0ad7eaa

I personally prefer moving to PhantomJS 2.
