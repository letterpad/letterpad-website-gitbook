# Typescript

To access data from a Graphql API, there are various clients available than can simplify the process. We are going to keep it simple and use the default `fetch` API.

You can have all the queries typed by configuring [codegen](https://www.graphql-code-generator.com/docs/getting-started/index). Lets see how to configure this.

Install these modules.

```bash
# as dependencies
yarn add typescript graphql graphql-tag

# as dev-dependencies
yarn add @graphql-codegen/cli \
         @graphql-codegen/typescript \
         @graphql-codegen/typescript-operations \
         @types/graphql -D
```

Create a file `codegen.yml` in your root directory and add the below lines

```yaml
schema: https://letterpad.app/admin/api/graphql
documents:
  - ./**/*.tsx
generates:
  lib/graphql.ts:
    plugins:
      - typescript
      - typescript-operations
    config:
      exportFragmentSpreadSubTypes: true

```

Lets understand whats going on here.

`schema` - Link to graphql schema

`documents` - Path of your queries

`generates` - It is going to generate the types in `lib/graphql.ts` file.

`plugins` - The plugins it will use to create the types.

`exportFragmentSpreadSubTypes` - If set to true, it will export the sub-types created in order to make it easier to access fields declared under fragment spread.

Refer to this [documentation](https://www.graphql-code-generator.com/docs/plugins/typescript-operations) for more details.

### Generate Types

Enter a new script in `package.json` to execute the  codegen.

{% code title="package.json" %}
```yaml
scripts: {
   ...
   "generate": "graphql-codegen",
   ...
}
```
{% endcode %}

Executing `yarn generate` wont generate any types yet because we have not written any query.

So lets write a query in `index.ts` which is again in the root folder.

```typescript
import gql from "graphql-tag";

const pageQuery = gql`
  query PageQuery($slug: String) {
    post(filters: { slug: $slug }) {
      ... on Post {
        id
        title
      }
      ... on PostError {
        message
      }
      __typename
    }
  }
`;
```

Graphql Codegen is going to read all files having a query or mutation and will generate types for it. So execute the below command.

```text
yarn generate
```

You should see a new file - `lib/graphql.ts` which got generated and has all the necessary types.

{% hint style="info" %}
Since the name of query is `PageQuery` the respose type corresponding to this would be `PageQueryQuery`.
{% endhint %}

Now lets try to send an API request to get the data.

```typescript
import { print } from "graphql";
import fetch from "node-fetch";
import { PageQueryQuery } from "../lib/graphql";

fetch("https://letterpad.app/admin/api/graphql", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    Authorization: "Bearer YOUR-CLIENT-ID",
  },
  body: JSON.stringify({
    query: print(postQuery),
    variables: { slug: "walk-around-music" },
  }),
})
  .then(res => res.json())
  .then(({ data }: { data: PageQueryQuery }) => {
    if (data.post.__typename === "Post") {
      console.log(data.post.title);
    }
  })
```

