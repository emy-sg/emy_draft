After the small intro that I give in the Readme.md

How Ngnix works ??</br>

To discover this and more, u have to install Nginx in ur machine OR a VM. </br>
And VOILA, let's dive in ... </br>

First of all, u have to look to the default config file of nginx. </br>
The config file of nginx is pretty complicated there is a lot of blocks that we don't have to simulate in our webserv, we gonna focus only on the HTTP block, to build our HTTP webserver.</br>

The path of the file that we gonna use in our testing is: </br>
		"/etc/nginx/sites-available/default" </br>

Example: 

``` C++
server {
	listen 80;
	server_name localhost;

	location / {
		root /var/www/nginx-default;
		index index.html index.htm;
	}
}
```

Description:

==> In the example above, we have only ONE server, that listen on port 80 in the interface (localhost: 127.0.0.1),</br>
so we have to create a socket and bind it to port 80 and 127.0.0.1 (networking part).</br>

==> Second thing to discuss is the "location block", so what is the location block is used for?</br>
In your server you can have multiple blocks of locations</br>
Each location have some directives, when and how to serve the client the ressources.</br>

- To serve a client a ressource you have to choose from which location, if none location exist, you must have the root directive within your server.</br>
- Location syntax:</br>
``` C++
	location /PATH {
		directive_one;
		directive_two;
		....
	}
```

==> The location block can have root directive in "absolute path", and the "indexes" files, for example.

- You compare the URL received in the request send by the client, with the locations Path to choose the right location.
How to choose the right location ??

The URL is also absolute path, so:
	URL is /.../.../.../ and Path of location is /.../.../...

first of all we compare the all URL string with the location path,
if u find one of the locations(in case multiple location) much the URL string,
==> so we find the right location.
But if we didn't, we truncat the last slash from the URL and research if there is any of the truncate URL much one of the locations.
And ainsi de suite, til '/' in case we coudn't find any location that much,
In this case, if you have the location '/', we can use this location as default location, if we can't find the default location make sure you have the root directive within your server to use it.

ps: It's just a simple example to have an idea about the config file.
you can make your own configfile, but it must have the elements in the subject.
using nginx as reference helps alot in testing, and understanding of the subject.

==> From here we can imagine how important to parse our config file to have an idea how much servers we have, and how much locations in each server, before launching our server sockets to listenning mode, to new connections from any clients.

PS:

I know it's alot of infos here, but to have more structered infos about the HTTP server, this book helped me alot:
 Click GET to download the book:
	 http://library.lol/main/739DBA0D69B8A300D3F30D4EB7A1C182


