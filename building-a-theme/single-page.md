# Single Page

This component will be called to render a page. The page will most probably be an item in the navigation menu. For this we will use the data connector `SinglePageData.js` to wrap this component.

Below are the props that will be passed to the `SingplePage` component.

```text
{
    "match": {
      "path": "/page/:slug",
      "url": "/page/home-component",
      "isExact": true,
      "params": {
        "slug": "home-component"
      }
    },
    "location": {...},
    "history": {...},
    "settings": {...},
    "page": {
      "ok": true,
      "post": {...},
      "errors": [],
    },
    "loading": false #true/false
  }
```

With the help of the above data, you can write your own component that will be rendered. Below is an example.

> Rembere to pass this data to the [SEO component](../others/seo.md) and include it while developing this.

```javascript
import React, { Component } from "react";
import PropTypes from "prop-types";
import Article from "../components/Post/Article";
import Loader from "../components/Loader";
import OhSnap from "client/helpers/OhSnap";
import SinglePageData from "shared/data-connectors/SinglePageData";

class SinglePage extends Component {
    render() {
        if (this.props.loading) {
            return <Loader />;
        }
        if (this.props.page === null) {
            return (
                <OhSnap message="Sorry, this page does not exist or might be restricted." />
            );
        }
        return (
            <Article post={ this.props.page} />
        );
    }
}

SinglePage.propTypes = {
    page: PropTypes.object,
    loading: PropTypes.bool
};

export default SinglePageData(SinglePage);
```

