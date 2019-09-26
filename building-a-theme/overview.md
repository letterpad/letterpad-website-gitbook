# Overview

Welcome to Letterpad's theme development guide!

Letterpad themes are intended to be very simple to build and maintain. You should have some knowledge on React to build a theme.

Letterpad takes care of the dependencies of your theme, manages the build and takes care of server side rendering. You can consider a theme like a standalone application. Letterpad provides a set of HOC's \(High Order Components\) which are data-connectors. You can use them as a wrapper for your components to get data. You can also create your own data-extracting HOC's and use them in your components.

### Behind the scenes

In the development mode, the themes are bundled on the fly whereas in production mode, the themes are pre-bundled to be used directly. The router is responsible to take the request and call the appropriate component. Below are the list of components that should exist for each theme.

* Layout \(hoc\)
* Home
* Posts
* SinglePage
* SinglePost
* SearchWrapper
* 404

These components already exist outside the themes directory as the default components. When you implement these components inside your theme, letterpad detects them and uses them instead of the default ones.

The most **important** component is the `Layout` component. This is the component which will be called everytime a request comes in. The layout component will recieve two arguments:

* Element - Component to be rendered
* props - additional data like settings, slug, router, etc.

You dont have to worry about what `Element` is this, it can be Home, Posts, SingplePage etc. You just have to make sure that the Layout component is creating the layout for your theme and the Element is being called with the required props.

### Loading the right theme

When a request comes in, the server decides which theme to use based on _environment variable_ or the theme _set through admin dashboard_. If none of theme are found, then the default theme `hugo` is used.

