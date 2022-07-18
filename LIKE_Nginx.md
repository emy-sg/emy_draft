After the small intro that I give in the Readme.txt

Let's dive in:
We are asked to build a webserv like nginx, with some specification:

The first thing we gonna do is install nginx in our machine and start testing, but what are we gonna test exactly ??
==> Well it simply mean go to the config file of nginx and create new server blocks or locations blocks and start testing.

	-----------------------------------
1- Config file like nginx:
I really strugle with this part, cuz I didn't know what directives should I support.

``` C++
http {

	// Create a new server
	server {
		// the directives 

		listen 80;	// host:port	
		server_name example.com;	//string

		root	/home/emy/emyDrafts_webserv;	// path to the root

		allowed_method GET DELETE POST;	// method allowed request
		error_pages 404 /my_404_error_pages.html; // I used the absolute path 
		client_max_body_size 1000;	// used in the upload

		// Create a location
		location /path {
			root /home/emy/emyDrafts_webserv/file.html;
			
			allowed_method GET;

			error_pages 404 /my_location_errors;

			client_max_body_size 10; 

			redirection 305 /path;
			cgi_php /path;
			upload /path_to_upload;
		}
	}


}
```
