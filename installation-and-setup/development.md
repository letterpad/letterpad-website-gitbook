# Development

This installs a site that will run in development mode using sqlite3. You should use this installation for testing letterpad and for developing themes.

### Install from github

```bash
git clone https://github.com/letterpad/letterpad.git 
cd letterpad
```

### Create Environment

You will find a file `.env.development.local` in the root. This file has some configurations which you don't necessarily have to change for the development environment unless you want to play around.

### Install dependencies & run

```text
yarn install 
yarn dev
```

### Run

Now visit [http://localhost:3000/admin/login](http://localhost:3000/admin/login) and checkout your installation

#### Admin Dashboard

The initial credentials of admin are:

* Email: **demo@demo.com**
* Password: **demo**

