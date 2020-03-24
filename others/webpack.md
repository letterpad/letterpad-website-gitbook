# Webpack

The below commands will assist you in making a build of your Letterpad instance.

**Development**

```bash
# For running the theme set in the database
yarn dev 
# Forcing a custom theme to run in your development
yarn dev mytheme
# Forcing a build of a custom theme
yarn build mytheme
```

**Production**

```bash
yarn prod
# or
yarn start
```

In order to prevent switching themes from the admin panel without a restart, it is important to build the theme for the server to use. So each theme will have 2 compulsary bundles, one for the client and the other for the server.



