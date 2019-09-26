# Folder Aliases

To make it easy to access different files in different folders, there are few aliases that you can use to avoid confusion. These aliases are setup in the webpack config file.

When you are developing a theme, you will be inside the folder `./src/client/themes/theme-name/`. From within your components you can access the root folders like `client`, `shared`, `config` by using aliases.

```jsx
import config from "config";
import PostsData from "shared/data-connectors/PostsData";
import Loader from "client/helpers/Loader";
```

It is a good practice to use these aliases becuase if in future we restructure the folders then your theme will still work.

