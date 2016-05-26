Cache Buster for Angular JS $http and $resource.
Especially useful with Internet Explorer (IE8, IE9)

This repository is forked from 

# install

Add this to your bower.json file.

    {
      "dependencies": {
        "angular-cache-buster": "https://github.com/j-combee/angular-cache-buster.git#0.5.2"
      }
    }


In your app module definition, add `ngCacheBuster` as a dependency

    angular.module('myApp', ['ngCacheBuster']);

# configure

AngularCacheBuster adds a cache buster to any $http requests (and hence to $resource requests).
Since you probably want to maintain browser caching for your views, partials or other routes, you can supply a list of regexes that will be matched against all URL's. By default the supplied matchlist is a whitelist (i.e. busting everything not matching an entry in the list) but you can also set it to be a blacklist, (i.e. busting everything except the matching entries)

For instance, if you want to bust everything except views in a 'partials' folder and images in a 'images' folder , you can configure AngularCacheBuster this way:

    angular.module('yourApp', ['ngCacheBuster'])
      .config(['httpRequestInterceptorCacheBusterProvider', function(httpRequestInterceptorCacheBusterProvider){
        httpRequestInterceptorCacheBusterProvider.setMatchlist([/.*partials.*/,/.*images.*/]);
      }]);

If instead you want to allow everything to be cached, except your "/api/users" and "api/orders" (assuming they are the only things that change frequently), you can supply a matchlist as before, but pass in a second boolean argument "blacklist" set to true as well:


    angular.module('yourApp', ['ngCacheBuster'])
      .config(['httpRequestInterceptorCacheBusterProvider', function(httpRequestInterceptorCacheBusterProvider){
        httpRequestInterceptorCacheBusterProvider.setMatchlist([/.*orders.*/,/.*users.*/],true);
      }]);

If you have a personal key that you want to append on the url you can set that key like this.


    angular.module('yourApp', ['ngCacheBuster'])
      .config(['httpRequestInterceptorCacheBusterProvider', function(httpRequestInterceptorCacheBusterProvider){
        httpRequestInterceptorCacheBusterProvider.setMatchlist([/.*orders.*/,/.*users.*/],true).setCustomKey('YourOwnKey');
      }]);

This is used for versioning.


# use

That's it! All your resource calls will have a cache buster added for anything not in the whitelist, or if you specified "blacklist", for everything matching the blacklist,

# test
`karma start` to launch the tests
