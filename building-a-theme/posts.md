# Posts



The Post component is responsible to display a list of posts along with pagination. You can use the default helper components to take care of pagination or you can create your own pagination component. For this we will use the data connector `PostsData.js` to wrap this component.

> You do not have to keep an internal state for posts and append pagination data into it. The new posts coming from pagination will be available inside the props _posts_.

```javascript
import React, { Component } from "react";
import PropTypes from "prop-types";
// A component to display post
import ArticleListItem from "../components/Post/ArticleListItem";
// You can access the config object with the alias "config"
import config from "config";
// Using default helper components. You can use the alias "client" to point to client directory.
import Paginate from "client/helpers/Paginate";
import OhSnap from "client/helpers/OhSnap";
// Data source. You can use the alias "shared" to point to shared directory.
import PostsData from "shared/data-connectors/PostsData";

class Posts extends Component {
    page = 1;

    async loadMore = (num) => {
        let result = await this.props.fetchMore({
            type: "post_category",
            slug: this.props.slug || this.props.match.params.slug,
            postType: "post",
            limit: config.itemsPerPage,
            offset: (num - 1) * config.itemsPerPage
        });
        this.page = num;
    }

    render() {
        if (this.props.loading) {
            return <span>Loading...</span>;
        }
        if (!this.props.posts) {
            return (
                <OhSnap message={this.props.settings.search_notFound.value} />
            );
        }
        if (this.props.posts.length === 0) {
            return (
                <OhSnap message={this.props.settings.text_posts_empty.value} />
            );
        }
        const posts = (
            <div className="post-row">
                {this.props.posts.map((post, i) => {
                    return <ArticleListItem idx={i} key={i} post={post} />;
                })}
            </div>
        );
        return (
            <Paginate
                data={posts}
                count={this.props.total}
                page={this.page}
                loadMore={this.loadMore}
            />
        );
    }
}

Posts.propTypes = {
    posts: PropTypes.array,
    total: PropTypes.number,
    loading: PropTypes.bool,
    fetchMore: PropTypes.func
};
export default PostsData(Posts);
```

