# Queries and Mutations



Letterpad communicates with the backend through GraphQL. This is beneficial because its easy to visualize your data as a json objects and you have full control over what data to get, set and display. You can build entire publishing apps on top of it, and completely customise the reader experience.

All the available mutations and queries in the stored in the shared/queries directory. Below is an example of how a query to fetch a post might look like.

```text
export const GET_SINGLE_POST = gql`
    query getPost($id: Int!) {
        post(id: $id) {
            id
            title
            body
            ...
        }
    }
`;
```

Since the above query in reality will contain more output fields and since those output fields will be used in different queries, we make use of fragments to encapsulate some common fields. So the above query can be written as:

```text
import { PostFragment } from "./Fragments";

export const GET_SINGLE_POST = gql`
    query getPost($id: Int!) {
        post(id: $id) {
            ...postFields
        }
    }
    ${PostFragment}
`;
```

The folder `data-sources` contains components which uses this data and gives back a HOF which can be used to power up your components with data.

The above query can be used in any of the React component as below.

```text
import React, { Component } from "react";
import Article from "../components/Post/Article";
import Loader from "client/helpers/Loader";
import OhSnap from "client/helpers/OhSnap";
import SinglePageData from "shared/data-connectors/SinglePageData"; // <----- HOF

class SinglePage extends Component {
    render() {
        if (this.props.loading) {
            return <Loader />;
        }
        if (!this.props.page.ok) {
            return (
                <OhSnap message="Sorry, this page does not exist or might be restricted." />
            );
        }
        const post = this.props.page.post;
        return (
            <div>
                <Article post={post} />;
            </div>
        );
    }
}
export default SinglePageData(SinglePage);
```

