---
description: >-
  The core responsibility of the Home is either to display a collection of posts
  or a single page.
---

# Home

Home is the first item in the navigation menu. If the first item is a category, then it will display a collection of posts from the `Posts` component matching that category. And if the first item is a page, then it will display the page with the `Page` component. 

{% hint style="info" %}
In the admin dashboard,  move the approtiate navigation menu item which you want to render as the homepage to the top.
{% endhint %}

{% code title="containers/Home.tsx" %}
```javascript
import React from "react";
import Posts from "./Posts";
import Page from "./Page";
import { IThemeContainer, EnumContentType } from "../../../types";

const Home: IThemeContainer = props => {
  if (props.contentType === EnumContentType.posts) {
    return <Posts {...props} />;
  }
  return <Page {...props} />;
};
```
{% endcode %}

Since Home can display a collection of posts or a single page, it is a good approach to split them here. 

