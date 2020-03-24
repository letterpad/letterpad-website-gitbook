---
description: The core responsibility of this component to display a blog post
---

# Post

The single post container is responsible to display a single blog post. You will recieve the data inside props and you can access the below result using `props.data`.

```javascript
{
    loading: true,
    post: {
        id: 1,
        title: "Another day on the terrace",
        body: "It was January ...",
        status: "publish",
        createdAt: "2019-11-22T13:24:00.166Z",
        publishedAt: "2019-11-22T13:24:00.166Z",
        updatedAt: "2019-11-24T01:27:44.828Z",
        excerpt: "Beatae alias ullam. Commodi modi et voluptatem quam. Nostrum occaecati ut id rem omnis soluta. Distinctio facere quia laudantium quia numquam vero iste.",
        cover_image: "/uploads/6.jpg",
        cover_image_width: 1100,
        cover_image_height: 600,
        slug: "post/post-6",
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
        ],
        __typename: "Post"
    }   
}
```

This is an example component of how your code may look like.

```javascript
const SinglePost: IThemeContainer['Post'] = ({ router, settings, data }) => {
  
  if (loading) return <Loader />;
  
  if (!data || data.post === null) {
    return (
      <div>"Sorry, this post does not exist or might be restricted."<div/>
    );
  }
  const { post } = data;
  
  return (
    <div>
      <Article
        post={post}
        settings={settings}
      />
    </div>
  );
};
```

