# Home



Letterpad supports a list of posts or just a single page as the homepage. It will recieve a prop `type`, which can be either `category` or `page` .

If it is a category then it means, it can have multiple posts with that category assigned. So you should load a component which can handle multiple posts. This is where you load the `Posts` component.

For the other case, if the type is page then you load the `Page` component.

> You can import third party libraries if you want anywhere in your theme. Your theme can have a `package.json` file.

### Under the hood

When you are in the root url `http://localhost:4000`, the initial component will be determined from the menu's first child. If the first child is a folder, then its first child will be used. This child will contain the type and the slug and will be passed to the Home Component through Layout Component. Below is an example how your home component might look like.

```text
import React, { Component } from "react";
import PropTypes from "prop-types";
import Posts from "./Posts";
import SinglePage from "./SinglePage";

export default class Home extends Component {
    render() {
        if (this.props.type === "category") {
            return <Posts slug={this.props.slug} {...this.props} />;
        }
        return <SinglePage slug={this.props.slug} {...this.props} />;
    }}
```

