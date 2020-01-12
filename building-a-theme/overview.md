# Overview

Welcome to Letterpad's theme development guide!

Letterpad themes are intended to be very simple to build and maintain. You should have some knowledge on React to build a theme.

Letterpad takes care of the dependencies of your theme, manages the build and takes care of server side rendering. A theme is always server sided rendered to take care of SEO.

All themes are contained inside the folder `src/client/themes`. To start building your first theme, create a folder inside themes directory. You can name this folder whatever you want. For this example, lets call it `mytheme`.

A theme is responsible to fetch the appropriate data from the graphql API and render it with a relevant design. These are mandatory files of a theme.

```text
- mytheme
    - containers
        - Home.tsx
        - SinglePage.tsx
        - SinglePost.tsx
        - SearchWrapper.tsx
        - Posts.tsx
        - NotFound.tsx
        - Layout.tsx
    - config.json
```

All the files in the containers gets mapped with the routes. When a route is matched, the relevant container is picked up. It is then passed to the `Layout` container as a prop with some other additional props. We will learn more about containers in the [next page.](containers/)

{% hint style="info" %}
There is no significant difference between a **page** and a **post** except that page cannot have taxonomies like tags and categories. The difference is mostly on how we use them. For eg. When you are reading a blog post, you might give a suggestion below the post about the next and previous post. But it is unlikely that you will mention that in Page.
{% endhint %}

The file **`config.json`** should contains the metadata of the theme. This is used in displaying the theme in the admin dashboard.

{% code title="config.json" %}
```javascript
{      
  "name": "Theme Name",
  "short_name": "theme-name",   
  "description": "A lightweight theme for writing stories.",    
  "author": "Foo Bar",    
  "thumbnail": "/images/thumbnail.png"
}
```
{% endcode %}

{% hint style="info" %}
The **`short_name`** is used to reference your theme. It should not contain spaces. You can think of this as a technical name of your theme.
{% endhint %}

### External Libraries

You can import third party libraries in your theme. So your theme can have a `package.json` fille containing all the dependencies. Letterpad will internally install them by using `yarn install`.

### Loading the right theme

When a request comes in, the server decides which theme to use based on environment variable or the theme set through admin dashboard. If none of theme are found, then the default theme `hugo` is used.

