# Best Practices

## Folder Structure
    
    Per component structure


    ```
    .
    └── app.js
    └── bin
        └── www
    └── config
    └── config
        └── config.js (base-config)
        └── env
            └── local
                └── database.js
            └── development
                └── database.js
            └── production
                └── database.js
            └── test
                └── database.js
        └── routes.js
    └── components
        └── user
            └── index.js
            └── user-ctrl.js
            └── user-model.js
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
       └── util.js
       └── util.test.js 
    ```

    **app.js** - API declaration
    **www*** - networking concerns
    **config > env > production** - values should be retrieve from env variables
    **models > index.js** will export the database connection that will be used
    **components > component > index** - will export routes connected to controller
    **components > component > model** - all queries of user controller
    **components > component > test** - components test 
    **templates** - template's that will be used for API
    **helpers** - helper functions
    **lib** - middleware's etc