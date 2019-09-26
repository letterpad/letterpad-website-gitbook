# Layouts

Layouts is a high order component. It will receive the arguments `Element` and `props`. The Element is the Component that needs to be rendered. It can be Home, Posts, SinglePage, SinglePost, SearchWrapper, 404.

`props` will have the below data

```javascript
{
  "settings": {
    "site_title": {
      "id": 1,
      "option": "site_title",
      "value": "Letterpad",
      "__typename": "Setting"
    },
    "site_tagline": {
      "id": 2,
      "option": "site_tagline",
      "value": "Compose a story",
      "__typename": "Setting"
    },
    "site_email": {
      "id": 3,
      "option": "site_email",
      "value": "admin@letterpad.app",
      "__typename": "Setting"
    },
    "site_url": {
      "id": 4,
      "option": "site_url",
      "value": "https://letterpad.app/demo",
      "__typename": "Setting"
    },
    "site_footer": {
      "id": 5,
      "option": "site_footer",
      "value": "",
      "__typename": "Setting"
    },
    "site_description": {
      "id": 6,
      "option": "site_description",
      "value": "",
      "__typename": "Setting"
    },
    "social_twitter": {
      "id": 7,
      "option": "social_twitter",
      "value": "https://twitter.com",
      "__typename": "Setting"
    },
    "social_facebook": {
      "id": 8,
      "option": "social_facebook",
      "value": "https://facebook.com",
      "__typename": "Setting"
    },
    "social_instagram": {
      "id": 9,
      "option": "social_instagram",
      "value": "https://instagram.com",
      "__typename": "Setting"
    },
    "social_github": {
      "id": 10,
      "option": "social_github",
      "value": "https://www.github.com",
      "__typename": "Setting"
    },
    "text_notfound": {
      "id": 11,
      "option": "text_notfound",
      "value": "Sorry, we went deep inside, but found nothing",
      "__typename": "Setting"
    },
    "text_posts_empty": {
      "id": 12,
      "option": "text_posts_empty",
      "value": "Sorry, we couldn't find any posts",
      "__typename": "Setting"
    },
    "displayAuthorInfo": {
      "id": 13,
      "option": "displayAuthorInfo",
      "value": "1",
      "__typename": "Setting"
    },
    "site_logo": {
      "id": 14,
      "option": "site_logo",
      "value": "/uploads/logo.png",
      "__typename": "Setting"
    },
    "menu": {
      "id": 15,
      "option": "menu",
      "value": "[{\"id\":3,\"title\":\"Abstract\",\"type\":\"category\",\"name\":\"Home\",\"disabled\":true,\"slug\":\"home\"},{\"id\":2,\"title\":\"Nature\",\"type\":\"category\",\"name\":\"Nature\",\"disabled\":true,\"slug\":\"nature\"},{\"id\":11,\"title\":\"Single Page\",\"slug\":\"about\",\"type\":\"page\",\"name\":\"About\",\"disabled\":true},{\"id\":111,\"title\":\"Not Found\",\"slug\":\"404\",\"type\":\"page\",\"name\":\"Not Found\",\"disabled\":true}]",
      "__typename": "Setting"
    },
    "css": {
      "id": 16,
      "option": "css",
      "value": "",
      "__typename": "Setting"
    },
    "google_analytics": {
      "id": 17,
      "option": "google_analytics",
      "value": "UA-120251616-1",
      "__typename": "Setting"
    },
    "locale": {
      "id": 18,
      "option": "locale",
      "value": "{\"en\":true,\"fr\":false,\"pl\":false}",
      "__typename": "Setting"
    },
    "theme": {
      "id": 19,
      "option": "theme",
      "value": "hugo",
      "__typename": "Setting"
    },
    "disqus_id": {
      "id": 20,
      "option": "disqus_id",
      "value": "letterpad",
      "__typename": "Setting"
    },
    "banner": {
      "id": 21,
      "option": "banner",
      "value": "/uploads/banner.jpg",
      "__typename": "Setting"
    },
    "themeConfig": {
      "theme-color": "Dark"
    }
  },
  "slug": "home",
  "type": "category"
}
```

```javascript
export default function Layout(Element, props) {
       class Child extends Component {
            // this.props will have addition information
            render() {
               const _props = { ...this.props, ...props };
                  // [..navigation]
                  // [...sidebar]
                  return <Element {..._props} />
            }
       } 
       return Child;
}
```

### Data

The props will contain the below information.

```text
{
    settings: {...},
    slug: "hello-world",
    type: "page" // page/post/posts/tag/category
}
```

> The Child component can access the history, location and match object through `this.props`

You may combine the props recieved as argument and the internal props of the Child component and pass it as new props to the Element.

