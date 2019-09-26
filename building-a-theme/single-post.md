# Single Post

A post cannot be linked with the navigation menu. For that we use page. So this component will always reply on the slug to render a post. For this we will use the data connector `SinglePostData.js` to wrap this component.

Below are the props that will be passed on to this component.

```text
{

    "match": {
      "path": "/post/:slug",
      "url": "/post/hello-world",
      "isExact": true,
      "params": {
        "slug": "hello-world
      }
    },
    "location": {...},
    "history": {...},
    "settings": {...},
    "post": {... },
    "loading": false #true/false
  }
```

You can handle an invalid slug by checking if `post` is `null`.

> To show adjacent posts, you can wrap this component with _AdjacentPostsData.js_ to get additional props `adjacentPosts` and `adjPostsLoading`.  
> The data in adjacentPosts will have previous and next.

```text
adjacentPosts = {previous: {}, next:{}} ;
```

This is an example component of how your code may look like.

```javascript
import React, { Component } from "react";
import PropTypes from "prop-types";
import Article from "../components/Post/Article";
import Loader from "../components/Loader";
import OhSnap from "client/helpers/OhSnap";
import SinglePostData from "shared/data-connectors/SinglePostData";

class SinglePost extends Component {
    render() {
        if (this.props.loading) {
            return <Loader />;
        }
        if (this.props.post === null) {
            return (
                <OhSnap message="Sorry, this page does not exist or might be restricted." />
            );
        }
        return (
            <Article post={ this.props.post} />
        );
    }
}

SinglePost.propTypes = {
    page: PropTypes.object,
    loading: PropTypes.bool
};

export default SinglePostData(SinglePost);
```

