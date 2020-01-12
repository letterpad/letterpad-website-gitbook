# Layout

The Layout container is the first component in the theme which is run. A layout may look something like this.

{% code title="Layout" %}
```text
        ------------------------------------------------------
        |                      Header                        |
        ------------------------------------------------------
        |                                                    |
        |                                                    |
        |                    <Content/>                      |
        |                                                    |
        |   (Home, Posts, SinglePost, SinglePage, Search)    |
        |                                                    |
        |                                                    |
        ------------------------------------------------------
        |                      Footer                        |
        ------------------------------------------------------
```
{% endcode %}

Notice the component `<Content/>`. This is a special prop that the Layout container receives to render the appropriate content. This content can be a collection of posts, a single post or a single page. The above layout can be translated to React in the below way. 

```jsx
import React from "react";
import { ILayoutProps } from "../types";

const Layout: React.FC<ILayoutProps> = ({Content, ...rest}) => {
    return (
        <Container>
            <Header/>
            <Content {...rest}/> 
            <Footer/>
        </Container>
    );
}
```

Below are the props that are received by the Layout container and is typed as **`ILayoutProps`**.

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Name</b>
      </th>
      <th style="text-align:left"><b>Type</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>router</b>
      </td>
      <td style="text-align:left">RouteComponentProps&lt;T&gt;</td>
      <td style="text-align:left">{match, history, location,...}</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>settings</b>
      </td>
      <td style="text-align:left">TypeSettings</td>
      <td style="text-align:left">admin dashboard <a href="../../resources/queries.md#query_settings">configured settings</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>themeSettings</b>
      </td>
      <td style="text-align:left">ThemeSettings[]</td>
      <td style="text-align:left">custom theme settings through settings.json</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>contentType</b>
      </td>
      <td style="text-align:left">
        <p>EnumContentType</p>
        <p></p>
      </td>
      <td style="text-align:left"><code>Home</code> component will need this to render the appropriate component
        like <code>SinglePage</code> or <code>Posts</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>initialProps</b>
      </td>
      <td style="text-align:left">{[ComponentName: string]: any }</td>
      <td style="text-align:left">props needed by the component before rendering. <a href="../../resources/server-side-rendering.md">Read more</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>client</b>
      </td>
      <td style="text-align:left">ApolloClient</td>
      <td style="text-align:left">Instance of apollo client.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Content</b>
      </td>
      <td style="text-align:left">IThemeContainer</td>
      <td style="text-align:left">One of the containers to be rendered. <code>Posts, SinglePage, SinglePost, Home, SearchWrapper, NotFound</code> 
      </td>
    </tr>
  </tbody>
</table>The prop **Content** is basically one of the containers \(Posts, SinglePage, SinglePost, Home, SearchWrapper, NotFound\). You do not have to decide under what condition which component should be rendered. We have already made that decision and have passed you the relevant component with the name `Content`.  

The prop **settings** will have the below data:

```javascript
{
  site_title: {
    id: 1,
    option: "site_title",
    value: "Letterpad1",
    __typename: "Setting",
  },
  site_tagline: {
    id: 2,
    option: "site_tagline",
    value: "Compose a story",
    __typename: "Setting",
  },
  site_email: {
    id: 3,
    option: "site_email",
    value: "admin@letterpad.app",
    __typename: "Setting",
  },
  site_url: {
    id: 4,
    option: "site_url",
    value: "https://letterpad.app/demo",
    __typename: "Setting",
  },
  site_footer: {
    id: 5,
    option: "site_footer",
    value: "",
    __typename: "Setting",
  },
  site_description: {
    id: 6,
    option: "site_description",
    value: "",
    __typename: "Setting",
  },
  social_twitter: {
    id: 7,
    option: "social_twitter",
    value: "https://twitter.com",
    __typename: "Setting",
  },
  social_facebook: {
    id: 8,
    option: "social_facebook",
    value: "https://facebook.com",
    __typename: "Setting",
  },
  social_instagram: {
    id: 9,
    option: "social_instagram",
    value: "https://instagram.com",
    __typename: "Setting",
  },
  social_github: {
    id: 10,
    option: "social_github",
    value: "https://www.github.com",
    __typename: "Setting",
  },
  text_notfound: {
    id: 11,
    option: "text_notfound",
    value: "Sorry, we went deep inside, but found nothing",
    __typename: "Setting",
  },
  text_posts_empty: {
    id: 12,
    option: "text_posts_empty",
    value: "Sorry, we couldn't find any posts",
    __typename: "Setting",
  },
  displayAuthorInfo: {
    id: 13,
    option: "displayAuthorInfo",
    value: "1",
    __typename: "Setting",
  },
  site_logo: {
    id: 14,
    option: "site_logo",
    value: "/uploads/logo.png",
    __typename: "Setting",
  },
  menu: {
    id: 15,
    option: "menu",
    value:
      '[{"id":3,"title":"Abstract","type":"category","disabled":true,"slug":"abstract"},{"id":2,"title":"Nature","type":"category","disabled":true,"slug":"nature"},{"id":111,"title":"Not Found","slug":"404","type":"page","disabled":true},{"id":18,"title":"hello","slug":"bh","type":"page","disabled":true},{"id":26,"title":"About me12","slug":"about-me","type":"page","disabled":true}]',
    __typename: "Setting",
  },
  css: {
    id: 16,
    option: "css",
    value: "",
    __typename: "Setting",
  },
  google_analytics: {
    id: 17,
    option: "google_analytics",
    value: "UA-120251616-1",
    __typename: "Setting",
  },
  locale: {
    id: 18,
    option: "locale",
    value: '{"en":true,"fr":false,"pl":false}',
    __typename: "Setting",
  },
  theme: {
    id: 19,
    option: "theme",
    value: "hugo",
    __typename: "Setting",
  },
  disqus_id: {
    id: 20,
    option: "disqus_id",
    value: "letterpad",
    __typename: "Setting",
  },
  banner: {
    id: 21,
    option: "banner",
    value: "/uploads/banner.jpg",
    __typename: "Setting",
  },
}
```

This is how the `Layout` may look like. You can set it up with header, footer or whatever design you want to have.

{% code title="containers/Layout.tsx" %}
```javascript
import React, { Component } from "react";
import { ILayoutProps } from "../types";

class Layout extends Component<ILayoutProps> {
  render() {
    // `Content` is special prop received only in Layout
    const { Content, ...props } = this.props;
    
    return (
      <div>
        <nav className="navbar navbar-default">
          <ul>
            <li>Home</li>
            <li>About</li>
          </ul>
        </nav>
        <main>
          <Content {...props} />;
        </main>
      </div>
    );
  }
}

export default Layout;
```
{% endcode %}

