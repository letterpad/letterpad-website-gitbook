# Home

The home is the first item in the navigation menu. If the first item is a category, then it will display a list of posts matching that category. If the first item is a page, then we return the `SinglePage` container to render it. 

{% hint style="info" %}
In the admin dashboard,  move the approtiate navigation menu item which you want to render as the homepage to the top.
{% endhint %}

{% code title="containers/Home.tsx" %}
```javascript
import React from "react";
import Posts from "./Posts";
import SinglePage from "./SinglePage";
import { IThemeContainer, EnumContentType } from "../../../types";

const Home: IThemeContainer = props => {
  if (props.contentType === EnumContentType.posts) {
    // you may render a different component to render this.
    return <Posts {...props} />;
  }
  return <SinglePage {...props} />;
};
```
{% endcode %}

Here the Home container is either a list of posts or a single page. 

{% hint style="info" %}
The Home container never displays a single post. It will either display a collection of posts or single page. 
{% endhint %}

We will see how to fetch data using graphql in the later section.

