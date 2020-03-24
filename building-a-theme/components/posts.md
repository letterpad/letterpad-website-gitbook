---
description: The core responsibility of this component is to render a collection of posts.
---

# Posts

The Posts component is responsible to display a collection of posts. This collection is made possible due to the taxonomies, `tags` and `categories`. The posts that you want to display as a collection should have a common category. Posts component will render if the url matches one the below ones.

```text
/posts/:category
/category/:category
/tag/:tag
```

{% hint style="info" %}
The navigation menu can contain a **category**, or a **page**. The category **will always** be a collection of posts.
{% endhint %}

## Data

Since we are using typescript, you will have the advantage to know what data `props.data` will have.

```javascript
{
    loading: true,
    rows: {
        count: 4,
        rows:[
            {
                id: 1,
                title: "Another day on the terrace",
                body: "...[truncated]",
                status: "publish",
                createdAt: "March 1, 2020",
                publishedAt: "March 1, 2020",
                updatedAt: "March 1, 2020",
                excerpt: "Beatae alias ullam. Commodi modi et voluptatem quam. Nostrum occaecati ut id rem omnis soluta. Distinctio facere quia laudantium quia numquam vero iste.",
                cover_image: "/uploads/6.jpg",
                cover_image_width: 1100,
                cover_image_height: 600,
                slug: "post-6",
                featured: true,
                type: "post",
                reading_time: '3 min read',
                author: {
                    fname: "John1",
                    lname: "Dave",
                    avatar: "/admin/images/avatar.png",
                    bio: "Provident quis sed perferendis sed.",
                    __typename: "Author"
                },
                tags: [
                    {id: 2, name: "sports", type: "post_tag", slug: "sports", __typename: "Taxonomy"}
                ],
                categories: [
                    {id: 1, name: "Abstract", type: "post_category", slug: "abstract", __typename: "Taxonomy"}
                ]
                __typename: "Post"
            }
        ]
    }
}
```

Check this complete example of the Posts container.

{% code title="Posts.tsx" %}
```javascript
// - src/client/types.ts
import { IThemeContainer } from "../../../types"
import React from "react";

const Posts: IThemeContainer["Posts"] = ({  
  router,
  settings,
  initialProps,
  loading,
  data,
  helpers
  ...rest 
}) => {
  
  const posts = data;
  
  if (loading) return <Loader />;
  
  if (!posts) {
    return null;
  }

  if (posts.rows.length === 0) {
    return null;
  }
  return (
    <div>
      <button onClick={() => loadMore(2)}>Load more</button>
      {(result as Post[]).map(post => (
        <li key={post.id}>{post.title}</li>
      ))}
    </div>
  );
};
```
{% endcode %}

