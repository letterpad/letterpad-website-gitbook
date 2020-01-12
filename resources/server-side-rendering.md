# Server side rendering

Letterpad can be run independently without a database as a static site. Since the static site is prebundled with data, you do not have to worry about server side rendering. However, if you would want to run it using sqlite, mysql or postgreSql you will have to pre-render the site on the server to support SEO. 

Every graphql query that is run inside a component returns a promise. When a particular route is matched, we execute all the queries of that route and wait for all the promises to resolve. After the promises are resolved, we collect all the data and then render the app on the server.

We use Apollo to fetch data from our graphql server. Apollo provides us with couple of ways to fetch data and thats what we are going to understand below.

Below is an example of fetching a post by url \(slug\) through apollo using the `useQuery` hook.

{% code title="SinglePost.tsx " %}
```jsx
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
    
  // render the post
  return (
    <...>
  )
}
```
{% endcode %}

## Special Data fetching method - \`getInitialProps\`

You might also want to fetch data from a third party source to build the ui and still support SSR. For those scenarios Letterpad offers a special static method, `getInitialProps`. You can do all the async work here and this will be executed on the server. The result will be available back to the component as a prop - `initialProps`. 

{% hint style="info" %}
For the initial page load, **`getInitialProps`** will execute on the server only. **`getInitialProps`** will only be executed on the client when navigating to a different route via the react-router-dom `<Link>`
{% endhint %}

For eg. if you would like to display the quote of the day in the homepage, you will have to fetch it first. You could do something like this. 

{% code title="Home.tsx" %}
```javascript
const Home: IThemeContainer = props => {
  // quotes are available here through props
  const [quote, setQuote] = useState(props.initialProps.Home.quote);
  
  return (
    <div>
      This is my home page. 
      This is the quote of the day.
      {props.initialProps.Home.quote}
    </div>
  )
};

// fetching quotes with the special static method
Home.getInitialProps = async ctx => {
  return {quote: await quoteOfTheDay()};
};

```
{% endcode %}

And because this is the `Home` component, quote will be available inside `initialProps.Home.quote`

