# Single Page

A page very much behaves like a post. The differences are mostly in capabilities. A page can never be a collection. You cannot assign taxonomies like categories or tags to a page. A page is considered to be completely independent. 

You should use the **`GET_SINGLE_POST`** query to fetch data for a particular slug. See below.

```jsx
const result = useQuery<PostQuery, PostQueryVariables>(
    QUERY_POST,
    {
      variables: {
        filters: {
          slug: router.match.params.slug,
        },
      },
    },
);
```

The result of the above query will like below.

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
        slug: "post-6",
        type: "post",
        author: {
            fname: "John1",
            lname: "Dave",
            avatar: "/admin/images/avatar.png",
            bio: "Provident quis sed perferendis sed.",
            __typename: "Author"
        },
        taxonomies: [
            {id: 1, name: "Abstract", type: "post_category", slug: "abstract", __typename: "Taxonomy"},
            {id: 2, name: "sports", type: "post_tag", slug: "sports", __typename: "Taxonomy"}
        ]
        __typename: "Post"
    }   
}
```

This is an example component of how your **SinglePost** code may look like.

```javascript
const SinglePost: IThemeContainer = ({ router, settings }) => {
  const { loading, data } = useQuery<PostQuery, PostQueryVariables>(
    QUERY_POST,
    {
      variables: {
        filters: {
          slug: router.match.params.slug,
        },
      },
    },
  );
  if (loading) return <Loader />;
  if (!data || data.post === null) {
    return (
      <OhSnap message="Sorry, this post does not exist or might be restricted." />
    );
  }
  const { post } = data;
  const { tags, categories } = utils.getTagsAndCategories(post.taxonomies);

  return (
    <div>
      <SEO
        schema="BlogPosting"
        title={post.title}
        description={post.excerpt}
        path={router.location.pathname}
        contentType="article"
        category={categories.join(",")}
        tags={tags}
        image={post.cover_image}
        settings={settings || {}}
      />
      <Article
        post={post}
        settings={settings}
        adjacentPosts={<AdjacentPosts slug={post.slug} />}
      />
    </div>
  );
};
```

