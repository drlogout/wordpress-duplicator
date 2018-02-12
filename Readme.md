# wordpress-duplicator

This image sets up the environment to clone and run a wordpress archive created by the [Wordpress Duplicator Plugin](https://de.wordpress.org/plugins/duplicator).

## Setup

Download the template files, which contains a docker-compose file and the project structure.

```bash
$ curl -L https://github.com/drlogout/wordpress-duplicator/blob/v1.0.0/duplicator-template.tar.gz\?raw\=true | tar xz
```

Rename the folder.

```bash
$ mv duplicator-template wpclone
```

Copy your `*.archive.zip` file into `wpclone/wordpress`.

Create an external volume for mysql data.

```bash
docker volume create dbvolume
```

If you plan to run this in production set secure passwords in `wpclone/docker-compose.yml`!

Then start up the containers.

```bash
$ cd wpclone
$ docker-compose up
```

When the mysql container is started the first time it takes a while until the database is initialized.

Then navigate to [http://localhost:8080/installer.php](http://localhost:8080/installer.php)

Enter the database settings as shown in the image below:

![DB settings](https://github.com/drlogout/wordpress-duplicator/raw/master/images/installer-db-settings.png "DB settings")

### Opcache

For devlopment you may want to disable opcache. You can add the following line to the htaccess file in `wpclone/wordpress/.htaccess`:

`php_flag opcache.enable Off`
