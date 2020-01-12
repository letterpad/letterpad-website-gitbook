# Querying Graphql API

Letterpad uses graphql and this helps in understanding the data quite easily. The best way to explore the graphql API is by exploring the [Graphql playground](https://letterpad.app/demo/graphql). This will help you understand the schema and also kind of data that you can fetch.

All kind of data can be accessed from a single endpoint which is `/graphql`.

Letterpad uses React Apollo to fetch data. These queries are fully typed, and Generics can be used to type both incoming operation variables and GraphQL result data. 

{% hint style="info" %}
All generics are kept in [/src/\_\_generated\_\_/gqlTypes.tsx](https://github.com/letterpad/letterpad/blob/master/src/server.js) and all queries are kept in [/src/shared/queries/Queries.ts](https://github.com/letterpad/letterpad/blob/master/src/shared/queries/Queries.js)
{% endhint %}

You can fetch the API data in different ways. Below are few examples.

#### Functional Component: Using Apollo useQuery hook:

In the below example, **`PostQuery`** is the data type we are asking for and **`PostQueryVariables`** are the variable types used in the query.

```jsx
import {
  PostQuery, 
  PostQueryVariables
} from "src/__generated__/gqlTypes.tsx";

const SinglePost: IThemeContainer = ({router, client}) => {
   
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
  if (!data || !data.post) {
    return <div>Something wrong happened</div>
  }
  
  return <...>
})
```

#### Component Class: Using Apollo Query Tag:

```jsx
class SinglePost extends React.Component<IThemeComponentProps, {}> {
  
  render() {
    const { router } = this.props;
    return (
      <Query<PostQuery, PostQueryVariables>
        query={QUERY_POST}
        variables={{
          filters: {
            slug: router.match.params.slug,
          },
        }}
      >
        {({ data, loading }) => {
          if (loading) return <div>loading...</div>;
          if (!data) return <div>something wrong happened</div>;
          return <div>Title: {data.post.title}</div>;
        }}
      </Query>
    );
  }
}
```

#### Using ApolloClient \(Functional / Component Class\)

Letterpad also exposes the ApolloClient for querying. Using the apollo client forces us to use an internal state. This can be useful in displaying infinite scrolling posts. Below is an example.

{% code title="Posts.tsx" %}
```jsx

const Posts: IThemeContainer = ({ router, client }) => {
  
  // Initialize en empty state
  const [posts, setPosts] = useState<Post[] | []>([]);
  
  // This will be run on server and client
  const { loading, data } = useQuery<
    PostsQuery,
    PostsQueryVariables
  >(POSTS_FROM_CATEGORY_SLUG, {
    variables: {
      filters: {
        slug: router.match.params.slug || "/",
        type: MenuTypes.Category,
        limit: 4,
        page: 0,
      },
    },
  });

  // save the above result in state
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

  // on load more, fetch append data to the state
  const loadMore = async page => {
    // fetch new data
    const { loading, data } = await client.query<
      PostsQuery,
      PostsQueryVariables
    >({
      query: GET_POSTS,
      variables: {
        filters: {
          slug: router.match.params.slug || "/",
          type: MenuTypes.Category,
          limit: 4,
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

