# Theme Structure

All themes are contained inside the folder `client/themes`. To start building your first theme, create a folder inside themes directory. You can name this folder whatever you want. This folder should contain a `config.json` having the below structure.

```text
{      
  "name": "Theme Name",
  "short_name": "theme-name",   
  "description": "A lightweight theme for writing stories.",    
  "author": "Foo Bar",    
  "thumbnail": "/images/thumbnail.png"
}
```

This data will be read by letterpad to highlight your theme in the Themes section.

> The **`short_name`** is used to reference your theme. It should not contain spaces. You can think of this as a technical name of your theme.

A theme consists of a set of components which should reside inside the folder `containers`.

It should contain the below components.

* Layout
* Home
* Posts
* SinglePage
* SinglePost
* SearchWrapper

You might want to give some additional settings \(optional\) to the user to control the behaviour of your theme. In order to do that, you should create another file `settings.json` and keep it inside the root folder of your theme. In this file, you can create your UI elements as json object. We support:

* input box \(text\)
* radio
* checkbox
* select \(dropdown\)

You can read more about [these over here](https://letterpad.app/docs/page/theme-settings).

