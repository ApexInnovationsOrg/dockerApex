#DOCKER CHEATSHEET by John #
For more detailed information, look at the README inside the phpdocker folder

After docker is started up, you can access your site by going to the following URL: local.apexinnovations.com

# -d means detach, allows you to run a command and have that command run in the background so you can do more things in your powershell #

# Build your docker environment based on yml file #
docker-compose up --build -d

# If your environment is already built, you can turn it on with just #
docker-compose up -d

# To bring the env down for say...a reset #
docker-compose down

# You need to see if errors are being thrown? This will follow the error log. Great to have this running in its own powershell #
docker-compose logs -f

# New updates to docker file and want to clean out old containers? hit Y when its done saying stuff #
docker system prune

# Want to see what stuff is running? #
docker-compose ps

# Want to look at a different folder other than the website? Making your own site? #
Inside the docker-composer.yml, you will see three sections with "Volumes". In that section, there is a volume that looks like such:
	- ../website:/application/
Change 'website' to be the folder you want to run as your main site.
Then rebuild your docker environment.