# Single Post Data



Used to fetch a single post. This connector will read the slug from the url and fetch the relevant data - `https://localhost:4040/post/:slug`

:slug - Post slug

**input props:**

```text
slug:    (default) props.match.params.slug   
```

**output props:**

```text
{    
    "loading": true | false,
    "post": {
        id
        title
        body
        status
        created_at
        excerpt
        cover_image
        slug
        type
        author {
            fname,
            lname,
            avatar,
            bio
        }
        taxonomies [
              {
                  id
                  name
                  type
                  slug
               },
               {...}
         ]
     }
 }
```

