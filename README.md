# Groovy Gecko Developer role interview task

## PHP with FFMPEG

### Installation steps

We use Docker in our development environment and would expect you to use this too.

We have created a base project with the following Docker containers:

1. `PHP 7.4 FPM` with `FFMPEG 4.1.4` installed - to run `.php` scripts
2. `NGINX` - to serve PHP files

#### Docker

Install Docker https://docs.docker.com/get-docker/

note: If you are using Linux, you need to additionally install docker-compose as it is not included with the base installation.


Run the following in a command shell (make sure you have navigated to the project directory)

1. Run `docker-compose build` to create the docker images for NGINX and PHP (7.4 fpm)
2. Run `docker-compose up -d` to run docker in detached mode

Once this is complete, you will be able to open http://localhost:8081 in your browser and see the output of `./public/index.php`

note: If you are using port 8081 for another project, you can change this by editing line 12 `docker-compose.yml` and then executing `docker-compose up -d` to load the changes.

To stop the project, run `docker-compose down`

#### Composer

To install PHP dependencies using composer, you need to have `docker-compose up -d` running.

`composer` is executed inside the PHP docker container, so `composer` functions should be prefixed with `docker-compose exec phpfpm`.

`composer install` and can be executed with `docker-compose exec phpfpm composer install`.

`composer require` and be executed with `docker-compose exec phpfpm composer require`

### The task

1.       Build a page (/var/www/html/index.php) which loads all videos from  folder (/var/www/html/media/videos/) and displays them to the user in a list (use bootstrap for all styling) in the left hand column. It should just say the name of the file – no need for anything else.

2.       Generate a form which allows the user to choose any two of the video files in the list and concatenate (combine) them and put them in the middle form. The videos are all the same codec, so make sure you use savefromsamecodec in the options. Use the first example rather than the second on their page.

3.       Submit a name of the file and the two videos via ajax to another page which will use php-ffmpeg (Library already installed under /var/www/html/ffmpeg/) to combine the videos and then encode the files to two bandwidths. Once the videos have completed encoding the form returns and the download urls of the two encoded files are written on the page (in the right hand column) as urls for the user to download. You don’t need to worry about progress of the file transcode.  We’re a very patient user.

4.       Once finished commit your changes to a branch on the project ( you can make up the branch name) and then submit a pull request to merge with master.

Inside /public/videos/ there are a number of video assets.

### Encoding Specs:

Wrapper – mp4

Video Codec : H.264

Highest – 736kbps Video 64 kbps Audio 1024px X 576px

Middle – 384kbps Video 64 kbps Audio 640px X 360px

### Links

https://github.com/PHP-FFMpeg/PHP-FFMpeg - The github of php-ffmpeg

http://malsup.com/jquery/form/ - Jquery Ajax Form documentation.
 

Don’t worry too much about how it looks or input verification. You can use a form builder to create the form if you like. We’re testing to see whether you can handle using a documented library from github and that you are comfortable building pages and using jquery to submit forms.

### Hints:

First work on getting files to concatenate and producing a united file, then work on the encoding to the different bitrates.

Always use full file path for files.
