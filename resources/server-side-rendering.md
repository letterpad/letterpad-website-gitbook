# Server side rendering

Letterpad can be run independently without a database as a static site. Since the static site is prebundled with data, you do not have to worry about server side rendering. However, if you would want to run it using sqlite, mysql or postgreSql you will have to pre-render the site on the server to support SEO. 

Every graphql query that is run inside a component returns a promise. When a particular route is matched, all the queries of that route is executed and returned as an array of promises. After all the promises are resolved, the data is used to render the app on the server.

We use Apollo to fetch data from our graphql server.

> You will mostly not need to know any of the data fetching technics as Letterpad provides the necessary data for all the routes. For advanced themes, you will need to know [how to fetch data using apollo](querying-graphql-api.md).

### Fetching external data with - getInitialProps

You might  want to fetch data from a third party source to build the UI and still support SSR. For those scenarios Letterpad offers a special static method, `getInitialProps`. You can do all the async work here and this will be executed on the server. The result will be available back to the component as a prop - `initialProps`. 

{% hint style="success" %}
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

