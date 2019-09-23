# Posts Data

Used to fetch multiple posts. Posts are grouped through category and so you should be fetching posts based on a category. This category item will be a part of the navigation menu.

You can set the slug of this category item from the Navigation item.

If you use the default Pagination helper, then on clicking each page item, the url will have the below format

`https://localhost:4040/:slug/page/:page_no`

:slug - Category slug

:page\_no - Page number

> This will not return pages

**input props:**

```text
slug:    (default) props.match.params.slug             
limit:   (default) config.itemsPerPage                
offset:  (default) offset || 0

// offset = props.match.params.page_no == 1 ? 0 : props.match.params.page_no;
```

**output props:**

```text
{    "fetchMore": function
    "loading": true | false,
    "total": 10,
    "posts": [
         {...},
         {...},
         {
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
     ]}
```

