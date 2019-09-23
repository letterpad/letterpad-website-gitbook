# Development



This installs a site that will run in development mode using sqlite3. You should use this installation for testing letterpad and for developing themes.

#### 

### Install from github

```text
git clone https://github.com/letterpad/letterpad.git cd letterpad
```

### Create Environment

Make a copy of `.env.sample` and name it `.env`. This files has some configurations which you don't necessarily have to change for the development environment unless you want to play around.

### Install dependencies & run

```text
yarn install 
yarn seed
yarn dev
```

### Run

Now visit [http://localhost:4040](http://localhost:4040/) and checkout your installation

To visit the admin dashboard, visit [http://localhost:4040/admin](http://localhost:4040/admin). The initial credentials of admin are:

* Email: [admin@letterpad.com](mailto:admin@letterpad.com)
* Password: password

