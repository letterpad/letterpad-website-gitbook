# Queries

In the [previous page](querying-graphql-api.md), we read about how to query the graphql API. Here we will go though a list of queries.

### **QUERY\_POSTS**

This query is used to fetch a collection of posts with various filtering options.

**Using Apollo**

```javascript
import { QUERY_POSTS } from "...Queries";
import {
  Post,
  PostsQuery,
  PostsQueryVariables,
} from "...gqlTypes";

const { loading, data } = useQuery<PostsQuery, PostsQueryVariables>(
    QUERY_POSTS,
    {
      variables: {
        filters,
      },
    },
  );
  
```

**Filtering** options in the above query**:** \(filters\)

```graphql
{
    /* name of a tag */
    tag: String
    
    /* name of a category */    
    category: String
    
    /* path of a category */
    categorySlug: String
    
    /* path of a category */
    tagSlug: String
    
    /* asc/desc */
    sortBy: PostSortBy
    
    /* publish | draft| trash */
    status: PostStatusOptions
    
    /* name of author */
    author: String
    
    /* search the title of the post */
    query: String
    
    /* page | post */
    type: PostTypes
    
    /* id after which posts will be selected */
    cursor: Int
    
    /* total number of posts to be fetched */
    limit: Int
    
    /* page no */
    page: Int
}
```

**Output:**

{% code title="data.posts" %}
```graphql
posts {
    count
    rows {
      id 
      title 
      body 
      status 
      createdAt 
      publishedAt 
      updatedAt 
      excerpt 
      cover_image 
      slug  
      type 
      author { 
        fname 
        lname 
        avatar 
        bio 
      } 
      taxonomies { 
        id 
        name 
        type 
        slug 
      }
    }
}
```
{% endcode %}





### **QUERY\_POST**

This query is used to fetch a collection of posts with various filtering options.

**Using Apollo**

```javascript
import { QUERY_POST } from "...Queries";
import {
  Post,
  PostsQuery,
  PostsQueryVariables,
} from "...gqlTypes";

const { loading, data } = useQuery<PostsQuery, PostsQueryVariables>(
    QUERY_POSTS,
    {
      variables: {
        filters,
      },
    },
  );
  
```

**Filtering** options in the above query**:** \(filters\)

```graphql
{
    /* name of a tag */
    tag: String
    
    /* name of a category */    
    category: String
    
    /* path of a category */
    categorySlug: String
    
    /* path of a category */
    tagSlug: String
    
    /* asc/desc */
    sortBy: PostSortBy
    
    /* publish | draft| trash */
    status: PostStatusOptions
    
    /* name of author */
    author: String
    
    /* search the title of the post */
    query: String
    
    /* page | post */
    type: PostTypes
    
    /* id after which posts will be selected */
    cursor: Int
    
    /* total number of posts to be fetched */
    limit: Int
    
    /* page no */
    page: Int
}
```

**Output:**

{% code title="QUERY\_POSTS" %}
```graphql
posts {
    count
    rows {
      id 
      title 
      body 
      status 
      createdAt 
      publishedAt 
      updatedAt 
      excerpt 
      cover_image 
      slug  
      type 
      author { 
        fname 
        lname 
        avatar 
        bio 
      } 
      taxonomies { 
        id 
        name 
        type 
        slug 
      }
    }
}
```
{% endcode %}



### **QUERY\_TAXONOMY**

This query is used to fetch a collection of taxonomies. 

**Using Apollo**

```javascript
import { QUERY_TAXONOMY } from "...Queries";
import {
  TaxonomiesQuery,
  TaxonomiesQueryVariables,
} from "...gqlTypes";

const { loading, data } = useQuery<TaxonomiesQuery, TaxonomiesQueryVariables>(
    QUERY_TAXONOMIES,
    {
      variables: {
        filters: {type: 'post_category'},
      },
    },
);
  
```

**Filtering** options in the above query**:** \(filters\)

```javascript
{
    // type of taxonomy post_tag | post_category
    type: String
    
    // fetch active taxonomies which are linked with published posts
    active: Boolean #(default: true)
}
```

**Output:**

{% code title="data.taxonomies" %}
```graphql
 [
    {
      name: "Abstract",
      type: "post_category",
      desc: null,
      slug: "abstract",
      id: 3,
    },
    {
      name: "Books",
      type: "post_category",
      desc: null,
      slug: "books",
      id: 10,
    },
    {
      name: "Nature",
      type: "post_category",
      desc: null,
      slug: "nature",
      id: 2,
    },
}
```
{% endcode %}

\*\*\*\*

\*\*\*\*

### **QUERY\_SETTINGS**

This query is used to fetch blog settings. This data is already made available to `Layout.tsx`, so you will mostly not need this query to run. [Read th](../building-a-theme/containers/layouts.md)[is block](../building-a-theme/containers/layouts.md) for more information. And you will receive a better formatted data like this:

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

**Using Apollo**

```javascript
import { QUERY_SETTINGS } from "...Queries";
import { SettingsQuery } from "...gqlTypes";

const { loading, data } = useQuery<SettingsQuery>(QUERY_SETTINGS);
  
```

**Output from query:**

{% code title="data.taxonomies" %}
```graphql
 {
  "data": {
    "settings": [
      {
        "id": 1,
        "option": "site_title",
        "value": "Letterpad1"
      },
      {
        "id": 2,
        "option": "site_tagline",
        "value": "Compose a story"
      },
      {
        "id": 3,
        "option": "site_email",
        "value": "admin@letterpad.app"
      },
      {
        "id": 4,
        "option": "site_url",
        "value": "https://letterpad.app/demo"
      },
      {
        "id": 5,
        "option": "site_footer",
        "value": ""
      },
      {
        "id": 6,
        "option": "site_description",
        "value": ""
      },
      {
        "id": 7,
        "option": "social_twitter",
        "value": "https://twitter.com"
      },
      {
        "id": 8,
        "option": "social_facebook",
        "value": "https://facebook.com"
      },
      {
        "id": 9,
        "option": "social_instagram",
        "value": "https://instagram.com"
      },
      {
        "id": 10,
        "option": "social_github",
        "value": "https://www.github.com"
      },
      {
        "id": 11,
        "option": "text_notfound",
        "value": "Sorry, we went deep inside, but found nothing"
      },
      {
        "id": 12,
        "option": "text_posts_empty",
        "value": "Sorry, we couldn't find any posts"
      },
      {
        "id": 13,
        "option": "displayAuthorInfo",
        "value": "1"
      },
      {
        "id": 14,
        "option": "site_logo",
        "value": "/uploads/logo.png"
      },
      {
        "id": 15,
        "option": "menu",
        "value": "[{\"id\":3,\"title\":\"Abstract\",\"type\":\"category\",\"disabled\":true,\"slug\":\"abstract\"},{\"id\":2,\"title\":\"Nature\",\"type\":\"category\",\"disabled\":true,\"slug\":\"nature\"},{\"id\":111,\"title\":\"Not Found\",\"slug\":\"404\",\"type\":\"page\",\"disabled\":true},{\"id\":18,\"title\":\"hello\",\"slug\":\"bh\",\"type\":\"page\",\"disabled\":true},{\"id\":26,\"title\":\"About me12\",\"slug\":\"about-me\",\"type\":\"page\",\"disabled\":true}]"
      },
      {
        "id": 16,
        "option": "css",
        "value": ""
      },
      {
        "id": 17,
        "option": "google_analytics",
        "value": "UA-120251616-1"
      },
      {
        "id": 18,
        "option": "locale",
        "value": "{\"en\":true,\"fr\":false,\"pl\":false}"
      },
      {
        "id": 19,
        "option": "theme",
        "value": "hugo"
      },
      {
        "id": 20,
        "option": "disqus_id",
        "value": "letterpad"
      },
      {
        "id": 21,
        "option": "banner",
        "value": "/uploads/banner.jpg"
      }
    ]
  }
}
```
{% endcode %}



### **QUERY\_THEMES**

This query is used to fetch the custom ui configuration of  themes. This query wont be required when you are developing a theme. This is already passed down to you in the `Layout` component as a prop, **themeSettings.** [Read more](../building-a-theme/containers/layouts.md) about this in the Layout section.

**Using Apollo**

```javascript
import { QUERY_THEMES } from "...Queries";
import {
  ThemesQuery,
  ThemesQueryVariables,
} from "...gqlTypes";

const { loading, data } = useQuery<ThemesQuery, ThemesQueryVariables>(
    QUERY_THEMES,
    {
      variables: {
        name: 'hugo'
      },
    },
);
  
```

**Filtering** options in the above query**:** \(filters\)

```javascript
{
    // `short_name` of the theme theme - config.json
    // this is optional. so the result will always be an array.
    name: String
}
```

**Output:**

{% code title="data.themes" %}
```graphql
[
  {
    name: "hugo",
    settings: [
      {
        name: "theme-color",
        type: "radio",
        tag: "input",
        options: ["Light", "Dark"],
        placeholder: null,
        defaultValue: "Dark111",
        changedValue: "Dark111",
        selectedValue: null,
        label: "Change theme color",
        helpText: "..",
      },
    ],
  },
  {...}
]

```
{% endcode %}



