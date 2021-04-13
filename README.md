# A simple MySQL playground with Docker-Compose

A simple setup to run a mysql server (_and maybe phpMyAdmin_) using docker-compose. This repo also provides a wrapper to simplify command line interaction with the mysql server.

## Getting started...
------------------
* Make sure you have [Docker](https://docs.docker.com/get-docker/) and [Docker-Compose](https://docs.docker.com/compose/install/) installed on your machine.
* Create a `.env` file. For that you can copy or just rename the provided `.env.sample` file.
* If you want to use the build in phpMyAdmin you have to uncomment the corresponding lines in `docker-compose.yaml`.
* Finally run `docker-compose up -d` to start the container[s]. You can check if they are runnig correctly by inspecting the logs using `docker-compose logs -f` (_`Ctrl+C` to exit_).
* If you enabled phpMyAdmin you can access it at [http://localhost:8080](http://localhost:8080/).
* Connect to the server at `localhost:3306` (_mysql default port_). If you installed `mysql` cli on your local machine you can connect using:
```
mysql -h localhost -u <username> -p<password>
```
#### Info
By default both the mysql server as well as phpMyAdmin will only listen on `localhost` (or `127.0.0.1`). To change that remove or replace `127.0.0.1` in the `ports` section inside the `docker-compose` file.

## Connect to mysql server using the included wapper
----------------------------
##### (currently only in bash)
### Passing down all arguments
The wrapper is a script located at `./mysql` that, if called with any arguments, will simply pass all arguments provided to the wrapper down to the mysql shell inside the container. You will need to authenticate with the mysql server manually.
\
A list with all possible arguments can be found [here](https://dev.mysql.com/doc/refman/5.7/en/mysql-command-options.html).

##### Usage Example:
```
./mysql -u <username> -p<password>
```


### Passing down all arguments
When called without any arguments the wrapper will try to read your credentials from the `.env` file and automatically drop you into an authenticated mysql shell inside the container.

##### Usage Example:
```
./mysql
```


### Make wrapper usage even easier!
You can also load a bash alias for the wrapper by sourcing the `alias` file using `source ./alias` or `. alias`. This will allow you the use the wrapper without the `./` at the beginnig.

##### Instead of typing `./mysql` you can now simply use:
```
mysql
```