# Overview

Welcome to Letterpad's theme development guide!

Letterpad themes are intended to be very simple to build and maintain. You should have some knowledge on React to build a theme.

Letterpad takes care of the dependencies of your theme, manages the build and takes care of server side rendering. A theme is always server sided rendered to take care of SEO.

All themes are contained inside the folder `src/client/themes`. To start building your first theme, create a folder inside themes directory. You can name this folder whatever you want. For this example, lets call it `mytheme`.

A theme is responsible to fetch the appropriate data from the graphql API and render it with a relevant design. These are essential files of a theme.

```text
- mytheme
    - public
    - app.tsx
    - config.json
    - tsconfig.json
    - package.json
    - settings.json [optional]
```

The file **`config.json`** should contain the metadata of the theme. This is used in displaying the theme in the admin dashboard.

{% code title="config.json" %}
```javascript
{      
  "name": "Theme Name",
  "description": "A lightweight theme for writing stories.",    
  "author": "Foo Bar",    
  "thumbnail": "/images/thumbnail.png" // keep this in public folder
}

tsconfig.json
```
{% endcode %}

`tsconfig.json` file is used to build your theme. You can the default settings.

{% code title="tsconfig.json" %}
```javascript
{
  "include": ["*"],
  "compilerOptions": {
    "module": "commonjs",
    "target": "es2015",
    "outDir": "../../../../dist",
    "jsx": "react",
    "allowJs": true,
    "skipLibCheck": true,
    "moduleResolution": "Node",
    "esModuleInterop": true
  },
  "exclude": ["node_modules"]
}

```
{% endcode %}

`app.tsx` is the root file of any theme. It exports some components with defined names that Letterpad uses to map to each route.

{% code title="app.tsx" %}
```javascript
export default {
  Layout,
  Home,
  Page,
  Posts,
  Post,
  NotFound,
};
```
{% endcode %}

When a route is matched, the relevant component is picked up. It is then passed to the `Layout` container as a prop with some other additional props. We will learn more about the props in the [next page.](components/)

{% hint style="info" %}
There is no significant difference between a **page** and a **post** except that page cannot have taxonomies like tags and categories. The difference is mostly on how we use them. For eg. When you are reading a blog post, you might give a suggestion below the post about the next and previous post. But it is unlikely that you will mention that in Page.
{% endhint %}

### External Libraries

You can import third party libraries in your theme. So your theme can have a `package.json` fille containing all the dependencies. Letterpad will internally install them by using `yarn install`.

### Loading the right theme

When a request comes in, the server decides which theme to use based on environment variable or the theme set through admin dashboard. If none of theme are found, then the default theme `hugo` is used.

