# Webpack

The below commands will assist you in making a build of your Letterpad instance.

**Development**

```bash
# For running the theme set in the database
yarn dev 
# Forcing a custom theme to run in your development
theme=hugo yarn dev
# Forcing a build of a custom theme
theme=hugo yarn build
```

**Production**

```bash
yarn prod
# or
yarn start
```

In order to prevent switching themes from the admin panel without a restart, it is important to build the theme for the server to use. So each theme will have 2 compulsary bundles, one for the client and the other for the server.

How does it build ?

```text
theme=hugo yarn build
```

Here we are setting a temporary environment variable `theme`. Webackpack needs to do the below tasks to successfully build the theme.

It will create the below files.

```text
|-dist
|--|client
|  |  |---themes
|  |  |   |---[theme]    
            |---public
            |   |---dist
            |   |   |---client-bundle.min.js
            |   |   |---server.node.js
            |   |   |---client.min.css
```

  
`server.node.js` file is going to be executed in the server. So when a request comes in, the server contacts the backend to check the default theme and then uses the build `themes/theme-name/public/dist/server.node.js` to serve that.

During this build, the files in the `client/containers` directory will be replaced with the theme files residing in the `themes/[theme-name]/containers` folder.

