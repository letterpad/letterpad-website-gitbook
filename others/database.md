# Database

The `api` folder has well defined schemas in the `schema` folder and its resolvers in the `resolvers` folder. If you wish to make any change in the database, then you should create a migration file. To create a migration file, enter this command:

```bash
yarn sequelize migration:generate --name specify-a-name-for-this-migration

#eg.
yarn sequelize migration:generate --name addGoogleAnalyticsField
```

The above migration will be created in \`api/housekeeper/migrations/xxxxxxxx-addGoogleAnalyticsField.js

In order to run the migrations, enter the below command.

```text
yarn sequelize db:migrate
```

You can play around with the Graphql API locally on [http://localhost:3030/graphql](http://localhost:3030/graphql)



### Seeding

If you want to seed the database with sample data, run the below command:

```bash
# you should have babel-cli installed. Its good to have this package installed globally.
yarn seed
```

