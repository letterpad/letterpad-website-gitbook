# Search Engine Optimization



Letterpad uses **react-helmet** to take care of search engine optimization, SEO. You can read more about the library [over here](https://github.com/nfl/react-helmet) . Letterpad provides is a helper component called `SEO.js` which has some boilerplate to take care of default data. To add SEO, lets say in your SinglePage.js, simply make the component render along with the below tag and it will automatically set up the appropriate meta tags in the head of your document. It does the same while rendering on the server.

```jsx
<SEO
  schema="BlogPosting"
  title={post.title}
  description={post.excerpt}
  path={"/post/" + this.props.match.params.slug}
  contentType="article"
  category={categories.join(",")}
  tags={tags}
  image={post.cover_image}
  settings={this.props.settings || {}}
 />
```

