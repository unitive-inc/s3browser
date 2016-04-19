Amazon S3 Directory Browser
===========================

Please report any issues [here on GitHub](https://github.com/powdahound/s3browser/issues).

Installation on Heroku (preferred)
----------------------------------

1. Check out the latest release from GitHub:

        git clone git@github.com:powdahound/s3browser.git

2. Assuming you already have the heroku toolkit set up, create an app:

        heroku apps:create my-file-browser

3. Set the necessary config values:

        heroku config:set BUCKET_NAME=my-bucket
        heroku config:set S3_ACCESS_KEY=xxx  # a key with access to perform a bucket object listing
        heroku config:set S3_SECRET_KEY=xxx
        heroku config:set PAGE_HEADER=X's Files

        heroku config:set AUTH0_DOMAIN=mydomain.auth0.com
        heroku config:set AUTH0_CLIENT_ID=xxx # Your client application id from Auth0
        heroku config:set AUTH0_CLIENT_SECRET=xxx # Your client application secret from Auth0
        heroku config:set AUTH0_CALLBACK_URL=https://app.mydomain.com # The configured callback URL from Auth0        

4. Deploy to Heroku and load the site

        git push heroku master
        heroku open

Configure Auth0
---------------

1. Create an application in Auth0. The application will provide all of the configuration values needed for authentication.

2. Options configurations:

  a. Only allow Google logins. 

        Applications->(application)->Connections 
        only enable google-auth2

  b. Restrict the domains of user email addresses.
      
        Rules->Create Rule->Email domain whitelist
        Change the whitelist to your domains.

Installation on Apache
----------------------

1. Check out the latest release from GitHub:

        cd /srv/www
        git clone git@github.com:powdahound/s3browser.git

2. Add an Apache VirtualHost for your new subdomain. e.g.:

        <VirtualHost *:80>
          ServerName s3browser.example.com
          DocumentRoot /srv/www/s3browser/www

          <Directory />
            AllowOverride all
            Order allow, deny
            Allow from all
          </Directory>
        </VirtualHost>

3. Tweak config to your liking. Each option is documented in the config.php file. Since it defaults to loading the values from environment variables, using [SetEnv](http://httpd.apache.org/docs/2.2/mod/mod_env.html) is probably best. You could also edit config.php to your liking.

4. Reload your Apache config:

        sudo /etc/init.d/apache2 reload
