# Layouts

Layouts are usually high order components or functions and this is the same in Letterpad. It will receive the arguments `Element` and `props`. The Element is the Component that needs to be rendered. It can be Home, Posts, SinglePage, SinglePost, SearchWrapper, 404.

```text
export default function Layout(Element, props) {
       class Child extends Component {
            // this.props will have addition information
            render() {
               const _props = { ...this.props, ...props };
                  // [..navigation]
                  // [...sidebar]
                  return <Element {..._props} />
            }
       } 
       return Child;
}
```

### Data

The props will contain the below information.

```text
{
    settings: {...},
    slug: "hello-world",
    type: "page" // page/post/posts/tag/category
}
```

> The Child component can access the history, location and match object through `this.props`

You may combine the props recieved as argument and the internal props of the Child component and pass it as new props to the Element.

