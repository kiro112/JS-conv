# Best Practices

## Folder Structure
    
    Per component structure

    ```
    .
    └── app.js
    └── config
        └── config.js (base-config)
        └── env
            └── local
                └── database.js
            └── development
                └── database.js
            └── production
                └── database.js // values should be retrieve from background env and not defined
            └── test
                └── database.js
        └── routes.js
    └── components
        └── user
            └── index.js // will export user related route
            └── user-ctrl.js
            └── user-model.js // all queries used in user will be put here
            └── user.test.js
        └── etc
            └── index.js
            └── etc-ctrl.js
            └── etc-model.js
            └── etc.test.js
    └── models (db-connection)
        └── index.js // will export connection only
        └── sequelize
            └── index.js
            └── user.js
            └── etc.js
        └── mongo.js
    └── templates // templates for mailer, etc..
    └── logs
    └── lib // middlewares and lib's
    └── helpers // helper functions
    ```