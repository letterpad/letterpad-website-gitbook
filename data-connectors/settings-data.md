# Settings Data



This connector can be used to fetch the settings of your site. This is already available as props in your theme's root component `Layout.js`.

**input props:**

none

**output props:**

```text
{
   "settings":{         
      "loading":true | false,      
      "data":{}
   }
}
```

`data` will be on object containing the below keys. You can get the value of any key using

```text
settings.data[key].value
```

All these values are configuration from the Admin Dashboard.

```text
site_title 
site_tagline
site_email
site_url
site_footer
site_description
post_display
layout_display
social_twitter
social_facebook
social_instagram
social_github
text_not
foundtext_posts_empty
sidebar_latest_post_count
sidebar_about
menu
css
locale
theme
banner
displayAuthorInfo
disqus_id
site_logo
google_analytics
editor
```

