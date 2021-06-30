# Production

This guide is intended for self hosters, looking for a step-by-step guide to getting Letterpad installed, setup and configured on their own servers

If you're looking to install Letterpad on your local machine, perhaps just to test it out or to develop a theme, please follow the [local install guide instead](https://letterpad.app/page/installation-dev). 

### Create A Non-root User

We will create a new user, letterpad, with sudo access as its not advised to do everything as the root user:

```text
adduser letterpad
```

Follow the prompts to set the new user’s name and password. You can leave all the other fields blank by hitting _Enter_.

Now let’s add the new user to two groups:

```text
gpasswd -a letterpad sudo
gpasswd -a letterpad www-data
```

This gives the `letterpad` user administrative access and adds it to the same group as Nginx, which we'll get to later.

### Configure Environment

First, let’s run system updates:

```text
sudo apt-get update && sudo apt-get upgrade -y
```

Now let’s install git, nodejs and nginx server:

Letterpad requires min Node v8.10.0+, but we will install the latest one directly from the NodeSource repo:

```text
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Install yarn. We will use yarn instead of npm to manage dependencies.

```text
sudo curl -o- -L https://yarnpkg.com/install.sh | bash
```

### Install Letterpad

Since we’re installing with the beta version of Letterpad, we need to build it from the source. Let’s start by cloning the repo from GitHub:

```text
cd /var/www
sudo git clone https://github.com/letterpad/letterpad.git
sudo chown -R $USER:www-data /var/www/letterpad
cd letterpad
```

This will create `/var/www/letterpad` and copy the source from GitHub.

Next we need to copy `.env.development.local` to `.env.production.local`file. Setup your production configurations in this file. 

```text
cp .env.development.local .env.production.local
nano .env
```

Next, change `SECRET_KEY` to a random string. Just make sure it's reasonably long and random.

Lastly, update the SMTP section. This section is important, otherwise you won’t be able to create users, reset passwords, etc. If you don’t already have a transactional email service, you may use your gmail credentials to configure this.

Now save the file by pressing `ctrl + x, y, enter`.

### Configure Nginx

Now we need to configure Nginx to act as a reverse proxy for Letterpad. All the traffic will first hit this nginx server and then nginx server will route this to your nodejs server where letterpad is running.

Let’s replace the default nginx config with a custom one:

```text
sudo nano /etc/nginx/sites-available/default
```

Delete everything and paste the following:

```bash
server {
  listen 80;
  server_name example.com;

  # Max upload size for proxy
  client_max_body_size 100m;

  location / {
    proxy_pass http://localhost:3030/;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
  }
}
```

Make sure to change `yourdomain.com` to the same domain or IP address you used in the `.env` file.

Save and exit by pressing `ctrl + x, y, enter`.

Now test the config and restart Nginx:

```text
sudo nginx -t
sudo systemctl restart nginx
```

### Install Dependencies

We will use — production=false as an argument to install the devDependencies as well for building optimised letterpad assets.

```text
yarn install --production=false
```

### Build Letterpad

Before starting letterpad, we have to create the optimized bundles. We can do so by entering the below command in your terminal.

```text
yarn build
```

This will build the letterpad admin dashboard.

### Run Letterpad

Once that is done, we will run the below command to turn on letterpad. Remember to have the environment variable `NODE_ENV` to `production` 

```text
yarn start
```

If everything is setup properly, you’ll be able to access Letterpad from the URL or IP address you entered in the last step.

### Run continiously

To run any nodeJS application continiously, we will need a task runner like pm2 to launch and monitor the app. If Letterpad crashes, pm2 will restart it. If your droplet gets restarted, pm2 will make sure Letterpad relaunches on startup.

```text
yarn global add pm2
pm2 start yarn --name "letterpad" --interpreter bash -- start
sudo pm2 startup systemd
```

If you encounter any issues with the above article, drop a comment and we will try to fix it together.

