# Features

This page describes all the features of the Letterpad API. While building a client, you can select the ones that you think is necessary.



#### Branding

Most of the branding data can be found in the settings query.

```graphql
query settings{
  settings{
    ...on Setting{
      site_title # String! =>  Title of the site
      site_tagline # String! => A caption of the site
      site_footer # String! => Can contain html
      site_description # String! => About the site
      social_twitter # String! => Twitter profile
      social_facebook # String! => Facebook profile
      social_instagram # String! => Instagram profile
      social_github # String! => Github profile
      displayAuthorInfo # Boolean! => Author info after post 
      menu # [Navigation!]! => Contains navigation items
      css # String! => css string to append
      google_analytics # String! 
      banner # Image! => contains {src, width, height}
      site_logo # Image! => contains {src, width, height}
      site_favicon # Image! => contains {src, width, height}
    }
  }
}    
```

| Fields | Type | Description |
| :--- | :--- | :--- |
| **site\_title** | `string(100)` | Title of the site. limit - 100 chars. |
| **site\_tagline** | `string(160)` | A tagline of the site. limit - 200 chars |
| **site\_description** | `string(500)` | Description of the site. limit - 500 chars |
| **social\_twitter** | `string` | Url of twitter profile |
| **social\_facebook** | `string` | Url of facebook profile |
| **social\_github** | `string` | Url of github profile |
| **social\_instagram** | `string` | Url of instagram profile |
| **displayAuthorInfo** | `boolean` | To show author info after post |
| **menu** | `[NavigationItem]` | Contains data about site navigation |
| **css** | `string` | Custom css  |
| **banner** | `Image` | Banner of the site |
| **site\_logo** | `Image` | Logo of the site |
| **site\_favicon** | `Image` | Favicon of the site |

### 

### Navigation Menu

The type of Navigation is shown below.

```graphql
type Navigation {
  type: NavigationType!
  slug: String!
  original_name: String!
  label: String!
}
```

**The first item will be considered as home.**

{% hint style="info" %}
Home can be a single page or a collection of posts\(denoted by tag\). 

If the first item has type as **page**, then its corresponding slug will contain the path to that page.

And if the first item has type as **tag**, then its corresponding slug will contain the path to that tag.
{% endhint %}

Depending on the type, you can fetch posts in the below way.

```graphql
# by tag
query Posts {
   posts(filters: { tagSlug: "home" }) { # or "/tag/home"
       ...on PostsNode {
           rows{
            title
           	publishedAt
            featured
            reading_time
            author{
                name
                avatar
            }
          }
       }
    }
}

# by page
query Post{
  post(filters:{slug:"a-page"}){
    ...on Post{
        title
      	excerpt
        reading_time
        author{
            name
            avatar
            bio
        }
    }
  }
}
```

### 

### Featured Posts

If the home page is a collection of posts, you might want to make it unique. Posts can be featured if they are selected from the admin dashboard. Its upto you how you want to create the UI for that.

### 

### Display Author Info

If  display author info is checked you should display the info of the author, `name`, `avatar` and `bio`.

### 

### Reading Time

Every post has a `reading_time`. You can display it say, near the title.

### 

### Gallery

The `html` string is the content of a post or a page in html. If a gallery is present, its markup would be as below.

```markup
<div class="gallery">
    <figure>
      <img>
    </figure>
    
    <figure>
      <img />
    </figure>
    
    <figure>
      <img />
    </figure>
</div>
```

You can use only css to build a grid or something similar and also add fullscreen option using javascript. Letterpad only provides the markup. 



### Footer

Footer is a html string. Make sure to render is as html and not as a string.



#### Lazy loading Images

We take care of the images and add all the necessary attributes to lazy load them. Although lazy loading is supported by most modern browsers, we use [lazysizes](https://github.com/aFarkas/lazysizes) library to make it more performant. Simply add this script in the head of your document and its done.

```markup
<script
   src="https://cdnjs.cloudflare.com/ajax/libs/lazysizes/5.3.2/lazysizes.min.js"
   async
/>
```



