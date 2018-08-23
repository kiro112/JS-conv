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


**app.js** - API declaration <br>
**www*** - networking concerns <br>
**config > env > production** - values should be retrieve from env variables <br>
**models > index.js** will export the database connection that will be used <br>
**components > component > index** - will export routes connected to controller <br>
**components > component > model** - all queries of user controller <br>
**components > component > test** - components test  <br>
**templates** - template's that will be used for API <br>
**helpers** - helper functions <br>
**lib** - middleware's etc

-----
## Wrap common utilities as npm packages

In a large app that constitutes a large code base, cross-cutting-concern utilities like logger, encryption and alike, should be wrapped by your own code and exposed as private npm packages. This allows sharing them among multiple code bases and projects

-----
## Use environment aware, secure and hierarchical config

A perfect and flawless configuration setup should ensure (a) keys can be read from file AND from environment variable (b) secrets are kept outside committed code (c) config is hierarchical for easier findability.

-----
## Error Handling Practices

### Use Async-Await or promises for async error handling

Handling async errors in callback style is probably the fastest way to hell (a.k.a the pyramid of doom).

### Document API errors using Swagger

Let your API callers know which errors might come in return so they can handle these thoughtfully without crashing.

### Shut the process gracefully when a stranger comes to town

When an unknown error occurs (a developer error, see best practice number #3)- there is uncertainty about the application healthiness. A common practice suggests restarting the process carefully using a ‘restarter’ tool like Forever and PM2

### Use a mature logger to increase errors visibility

it will speed-up error discovery and understanding. So forget about console.log.

### Test error flows using your favorite test framework

Ensure that your code not only satisfies positive scenario but also handle and return the right errors. Testing framework like Mocha & Chai can handle this easily

### Fail fast, validate arguments

Assert API input to avoid nasty bugs that are much harder to track later. Validation code is usually tedious



## Testing And Overall Quality Practices

### At the very least, write API (component) testing

Most projects just don't have any automated testing due to short timetables or often the 'testing project' run out of control and being abandoned. For that reason, prioritize and start with API testing which is the easiest to write and provide more coverage than unit testing (you may even craft API tests without code using tools like Postman. Afterward, should you have more resources and time, continue with advanced test types like unit testing, DB testing, performance testing, etc


### Carefully choose your CI platform (Jenkins vs CircleCI vs Travis vs Rest of the world)

Your continuous integration platform (CICD) will host all the quality tools (e.g test, lint) so it should come with a vibrant ecosystem of plugins. Jenkins used to be the default for many projects as it has the biggest community along with a very powerful platform at the price of complex setup that demands a steep learning curve. Nowadays, it became much easier to set up a CI solution using SaaS tools like CircleCI and others. These tools allow crafting a flexible CI pipeline without the burden of managing the whole infrastructure. Eventually, it's a trade-off between robustness and speed - choose your side carefully


### Constantly inspect for vulnerable dependencies

most reputable dependencies such as Express have known vulnerabilities. This can get easily tamed using community and commercial tools such as link nsp that can be invoked from your CI on every build

use nsp: https://github.com/nodesecurity/nsp
and snyk: https://snyk.io/

### Use docker-compose for e2e testing

End to end (e2e) testing which includes live data used to be the weakest link of the CI process as it depends on multiple heavy services like DB. Docker-compose turns this problem into a breeze by crafting production-like environment using a simple text file and easy commands. It allows crafting all the dependent services, DB and isolated network for e2e testing. Last but not least, it can keep a stateless environment that is invoked before each test suite and dies right after


## Production

### Monitoring!

At the very basic level, monitoring means you can easily identify when bad things happen at production.

### Lock dependencies

Your code must be identical across all environments, but amazingly npm lets dependencies drift across environments by default – when you install packages at various environments it tries to fetch packages’ latest patch version. Overcome this by using npm config files, .npmrc, that tell each environment to save the exact (not the latest) version of each package. Alternatively, for finer grain control use npm” shrinkwrap”. *Update: as of NPM5, dependencies are locked by default. The new package manager in town, Yarn, also got us covered by default

### Get your frontend assets out of Node

Serve frontend content using dedicated middleware (nginx, S3, CDN) because Node performance really gets hurt when dealing with many static files due to its single threaded model


### Set NODE_ENV=production

Set the environment variable NODE_ENV to ‘production’ or ‘development’ to flag whether production optimizations should get activated

### Use an LTS release of Node.js

Ensure you are using an LTS version of Node.js to receive critical bug fixes, security updates and performance improvements


## Security Best Practices

### Limit concurrent requests using a middleware

DOS attacks are very popular and relatively easy to conduct. Implement rate limiting using an external service such as cloud load balancers, cloud firewalls, nginx, or (for smaller and less critical apps) a rate limiting middleware (e.g. express-rate-limit)

### Extract secrets from config files or use packages to encrypt them

Never store plain-text secrets in configuration files or source code. Instead, make use of secret-management systems like Vault products, Kubernetes/Docker Secrets, or using environment variables


### Prevent query injection vulnerabilities with ORM/ODM libraries

To prevent SQL/NoSQL injection and other malicious attacks, always make use of an ORM/ODM or a database library that escapes data or supports named or indexed parameterized queries, and takes care of validating user input for expected types.


### Adjust the HTTP response headers for enhanced security

Your application should be using secure headers to prevent attackers from using common attacks like cross-site scripting (XSS), clickjacking and other malicious attacks. These can be configured easily using modules like helmet.


### Avoid using the Node.js crypto library for handling passwords, use Bcrypt

Passwords or secrets (API keys) should be stored using a secure hash + salt function like bcrypt, that should be a preferred choice over its JavaScript implementation due to performance and security reasons.

### Validate incoming JSON schemas

Validate the incoming requests' body payload and ensure it qualifies the expectations, fail fast if it doesn't.


### Support blacklisting JWTs

When using JSON Web Tokens (for example, with Passport.js), by default there's no mechanism to revoke access from issued tokens. Once you discover some malicious user activity, there's no way to stop them from accessing the system as long as they hold a valid token. Mitigate this by implementing a blacklist of untrusted tokens that are validated on each request.

### Limit the allowed login requests of each user

A brute force protection middleware such as express-brute should be used inside an express application to prevent brute force/dictionary attacks on sensitive routes such as /admin or /login based on request properties such as the user name, or other identifiers such as body parameters


### Hide error details from clients

An integrated express error handler hides the error details by default. However, great are the chances that you implement your own error handling logic with custom Error objects (considered by many as a best practice). If you do so, ensure not to return the entire Error object to the client, which might contain some sensitive application details

### Don’t use deprecated or vulnerable versions of Express

Express 2.x and 3.x are no longer maintained. Security and performance issues in these versions won’t be fixed.

### Use TLS

use Transport Layer Security (TLS) to secure the connection and the data.





<!-- 

    Source:
        https://github.com/i0natan/nodebestpractices
        https://www.joyent.com/node-js/production/design

 -->