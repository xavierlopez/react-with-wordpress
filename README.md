# React with WordPress



:fire: Example of react application with WordPress REST API

******* PLEASE STAR MY REPO TO SUPPORT MY WORK 🙏 ******

Please follow me 🙏 on [twitter](https://twitter.com/imranhsayed)

## Dashboard Demo

![](demo-dashboard.gif)

## Pagination :video_camera:
![](pagination.gif)

## Post Listings Demo :video_camera:

![](render-posts.gif)

## [Live Demo](https://react-with-wordpress.netlify.com/)

## Features

1. CRUD operation with WordPress REST API
2. Authentication with JWT ( Login Logout )
3. Accessing public and private routes 
4. Handing WordPress REST API custom end points.
5. Creating Dashboard with React for CRUD operation.
6. Pagination

## Installation

1. Clone this repo in `git clone https://github.com/imranhsayed/react-with-wordpress`

2. `git checkout branchname`

3. Run `npm install`

## Add [REST API ENDPOINTS WordPress Plugin](https://github.com/imranhsayed/rest-api-endpoints)

* Clone the [REST API ENDPOINTS](https://github.com/imranhsayed/rest-api-endpoints) plugin in your WordPress plugin directory.

`git clone git@github.com:imranhsayed/rest-api-endpoints.git`

## Configure

Add your wordPress siteUrl in `src/client-config.js`

```ruby
const clientConfig = {
	siteUrl: 'http://localhost:8888/wordpress'
};

export default clientConfig;
``` 

## Branches

### 1. [login-with-jwt-wordpress-plugin](https://github.com/imranhsayed/react-with-wordpress/tree/login-with-jwt-wordpress-plugin)

> A React App where you can login using the endpoint provided by `JWT Authentication for WP-API` WordPress Plugin.
So you need to have this plugin installed on WordPress. The plugin's endpoint returns the user object and a jwt-token on success,
which we can then store in localstorage and login the user on front React Application

### Steps
* You need to install and activate [JWT Authentication for WP REST API](https://wordpress.org/plugins/jwt-authentication-for-wp-rest-api/) plugin on you WordPress site
* Then you need to configure it by adding these:

i. Add the last three lines in your WordPress `.htaccess` file as shown:
```ruby
# BEGIN WordPress
   <IfModule mod_rewrite.c>
   RewriteEngine On
   RewriteBase /wordpress/
   RewriteRule ^index\.php$ - [L]
   RewriteCond %{REQUEST_FILENAME} !-f
   RewriteCond %{REQUEST_FILENAME} !-d
   RewriteRule . /wordpress/index.php [L]
   
   
   RewriteCond %{HTTP:Authorization} ^(.*)
   RewriteRule ^(.*) - [E=HTTP_AUTHORIZATION:%1]
   SetEnvIf Authorization "(.*)" HTTP_AUTHORIZATION=$1
   
   </IfModule>
```
ii. Add the following in your `wp-config.php` Wordpress file. You can choose your own secret key.

```ruby
define('JWT_AUTH_SECRET_KEY', '&BZd]N-ghz|hbH`=%~a5z(`mR=n%7#8-Iz@KoqtDhQ6(8h$og%-IbI#>N*T`s9Dg');
define('JWT_AUTH_CORS_ENABLE', true);
```

iii. Now you can make a request to `/wp-json/jwt-auth/v1/token` REST API provided by the plugin. You need to pass 
username and password and it returns a user object and token . You can save the token in localstorage and send it in the headers
of your protected route requests ( e.g. [Create Post](https://developer.wordpress.org/rest-api/reference/posts/#create-a-post) `/wp-json/wp/v2/posts` ) 

iiv. So whenever you send a request to WordPress REST API for your protected routes, you send the token received in the headers of
your request
```
{
	'Accept': 'application/json',
	'Content-Type': 'application/json',
	'Authorization': `Bearer putTokenReceivedHere`
}

```

This repo also demonstrates how to create posts in React Application by sending request to protected endpoints ( passing the token in the header )

### 2. [jwt-verify-with-node](https://github.com/imranhsayed/react-with-wordpress/tree/jwt-verify-with-node)  

> A React(front end) + Node(back end) application. It uses `jwt.sign()` ( from `jwtwebtoken` npm package ) to generate a token using the username and password
sent from front end( React ) and returns it as a response, which we then store in localstorage to login the user.
This token received by frond end, will be sent with all further request for protected routes, which will then be verified in node route
using `jwt.verify()`
Besides generating the token, the end point in node also accesses the WordPress rest api to confirm the credentials and returns the user object
or errors if any.

> It also has functionality to create post where we make a request from front end along with token( React ) to a node end point.
The node endpoint verifies the token and then makes a request to WordPress REST API endpoint to create the post and then returns the
new post id, or error if any.  

## Commands

1. Branch [master](https://github.com/imranhsayed/react-with-wordpress) and [build-app-for-heroku](https://github.com/imranhsayed/react-with-wordpress/tree/build-app-for-heroku)
- `start` Runs node server for development ( in watch mode ). The server.js sends all front end route request to index.html and then all front end route requests is handled by reach router

2. Branch [jwt-verify-with-node](https://github.com/imranhsayed/react-with-wordpress/tree/jwt-verify-with-node) and
[login-with-jwt-wordpress-plugin](https://github.com/imranhsayed/react-with-wordpress/tree/login-with-jwt-wordpress-plugin)

- `dev` Runs webpack dev server for development ( in watch mode )

Common
- `prod` Runs webpack in production mode

## Free Courses

[Codeytek](https://codeytek.com/)

