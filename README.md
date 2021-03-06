# WP Skateboard
A bare-bones starter WordPress environment using Docker and Composer. Right now, this just quickly sets up a functional local environment and does not include any starter theme. That's yet to come.

## How to Stand This Up
Make sure [Docker](https://www.docker.com/), [Docker Compose](https://docs.docker.com/compose/), and [Composer](https://getcomposer.org/) are installed on your machine. 

1. If it's not built already, build the `wp-skateboard` image with `make docker`. 
2. Run `make up` to turn on the Docker container. The `wp-content` directory is where you'll want to put the themes and plugins you're developing.
3. Run `make prep` to remove default plugins, themes, and database content.
4. Run `composer install` to install any dependencies you want.
5. When you're done, run `make down` to turn off the container.

There are some other commands in the `Makefile` too, so feel free to check those out or add your own.

## Want to Tinker w/ WordPress Core?
Out of the box, the WordPress core files will only exist inside the running container, with no _easy_ access to modify them if you want to play around or troubleshoot. To give yourself the core files with which to tinker, run the `make localize` command while your container is running to install the files locally, mount them to your container, and modify your WordPress configuration so the site uses these files instead of what's built by the image. 

After running this command, run `make down` to turn off your container, and uncomment the `- ./core:/var/www/html/core` line in the `docker-compose.yml` file to mount that directory to the container. Run `make up` to get it going again. Any changes you make to core files should appear in the browser. 

Now, to access this WP admin location, navigate to `localhost:8000/core/wp-admin`. 

## License
MIT © [Alex MacArthur](https://macarthur.me)