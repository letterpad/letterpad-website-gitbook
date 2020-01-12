# Containers

A container is a React Component exported from a `tsx` file. Containers are associated with a component in the route. Thats why the below containers are essential to take care of rendering a theme.

| Component | Purpose |
| :--- | :--- |
| Home | To render the home page. The home page can be a list of posts or a single page. It receives a prop called **contentType** to determine which component should be rendered, `Posts` or `SinglePage` |
| Posts | Renders a list of posts. |
| SinglePage | Renders a single page. |
| SinglePost | Renders a single post. |
| Search | Renders search results. You may also use this to display posts for a particulat tag or category. |
| NotFound | Rendered when no routes are matched. |
| **Layout** | The first component which is run and is responsible to render all the above  components. |



