# Components

A container is a React Component exported from a `tsx` file. Containers are associated with a component in the route. Thats why the below containers are essential to take care of rendering a theme.

| Component | Purpose |
| :--- | :--- |
| Home | To render the home page. The home page can be a list of posts or a single page. It receives a prop called **contentType** to determine which component should be rendered, `Posts` or `SinglePage` |
| Posts | Renders a list of posts. |
| Page | Renders a single page. |
| Post | Renders a single post. |
| NotFound | Rendered when no routes are matched. |
| **Layout** | The first component which is run and is responsible to render all the above  components. |



