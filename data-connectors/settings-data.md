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
site_title site_taglinesite_emailsite_urlsite_footersite_descriptionpost_displaylayout_displaysocial_twittersocial_facebooksocial_instagramsocial_githubtext_notfoundtext_posts_emptysidebar_latest_post_countsidebar_aboutmenucsslocalethemebannerdisplayAuthorInfodisqus_id

site_logogoogle_analyticseditor
```

