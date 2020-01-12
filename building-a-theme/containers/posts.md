# Posts

The Posts container is responsible to display a collection of posts. This collection is made possible due to the taxonomies, `tags` and `categories`. The posts that you want to display as a collection should have a common category. Posts container will render if the url matches one the below ones.

```text
/posts/:category
/category/:category
/tag/:tag
```

This category can be a one of the first menu item in the navigation menu. 

{% hint style="info" %}
The navigation menu can contain a **category**, or a **page** or a **folder** containing category or page. The category **will always** be a collection of posts.
{% endhint %}

You can use **`GET_POSTS`** query to fetch those posts. It access the below paramaters for filtering.

tag: String category: String categorySlug: String tagSlug: String authorName: String sortBy: PostSortBy status: PostStatusOptions author: String query: String type: PostTypes cursor: Int limit: Int page: Int

| Filtering Keys | Description |
| :--- | :--- |
| tag | name of a tag |
| tagSlug | slug of a tag |
| category | name of a category |
| categorySlug | slug of a category |
| query | search string to search posts |
| status | status of post. You can only query published posts from a theme. |
| sortBy |  |
| author | search posts by author |
| cursor | id of the post after which the next posts will be displayed. |
| limit | set the limit of posts per page |
| page | page to display |

You can request data from api using `useQuery` hook from Apollo. Check this example below.

```javascript
const result = useQuery<PostsQuery, PostsQueryVariables>(
    QUERY_POSTS,
    {
      variables: {
        filters: {
          categorySlug: router.params.category
        },
      },
    },
);
```

The result of the above request will look like below.

{% code title="result" %}
```javascript
{
    loading: true,
    rows: {
        count: 4,
        rows:[
            {
                id: 1,
                title: "Another day on the terrace",
                body: "<p>👋 Welcome, it's great to have you here.</p>",
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
        ]
    }
}
```
{% endcode %}

Check this complete example of the Posts container.

{% code title="Posts.tsx" %}
```javascript
const Posts: IThemeContainer = ({ router, client }) => {
  
  // Initialize en empty state
  const [posts, setPosts] = useState<Post[] | []>([]);
  
  const { params } = router.match;
  const slug = params.category || "/";
 
  // This will be run on server and client
  const { loading, data } = useQuery<PostsQuery, PostsQueryVariables>(
      POSTS_FROM_CATEGORY_SLUG, {
      variables: {
        filters: {
         categorySlug: slug
        }
      },
  });

  // save the above that in state
  useEffect(() => {
    if (
      data &&
      data.posts &&
      data.posts.rows &&
      data.posts.rows.length > 0
    ) {
      setPosts(data.posts.rows as Post[]);
    }
  }, [loading]);

  const loadMore = async page => {
    // fetch new data
    const { loading, data } = await client.query<PostsQuery, PostsQueryVariables>(
      {
        query: QUERY_POSTS,
        variables: {
          filters: {
            categorySlug: slug,
            page: parseInt(page),
          },
        },
    });
    
    // append the data in the state
    if (
      data &&
      data.posts &&
      data.posts.rows &&
      data.posts.rows.length > 0
    ) {
      setPosts([...posts, ...data.posts.rows] as Post[]);
    }
  };
  
  // During the first render, SSR will wait for the `useQuery` 
  // hook to resolve which will give us data to render on server.
  // When this runs in client, it will save the data 
  // in the internal state and use the state instead. 
  // This way when you want to load more, 
  // you append new data in the state.
  
  let result = (data && data.posts && data.posts.rows) || [];
  if (posts.length > 0) {
    result = posts;
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

