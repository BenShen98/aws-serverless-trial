# Let's play
1. go to https://benshen98.github.io/aws-serverless-trial/
2. Click login and use 
   * Username: hello@world
   * Password: 123456

Yes, I know I had chosen  the most unbreakable password in the world!

# Intention

This project is built in order for me to get familiar with the cloud and serverless, as I had no previous experience relate to it. 

If you are also like me, want to get into serverless, but don't know where to start. I find these step might be helpful and could save you some valuable time
1. watch [aws essential from udemy](https://www.udemy.com/aws-essentials/), especially IAM, VPC and Lambda
2. install [serverless](https://serverless.com/) and follow the [quickstart guide](https://serverless.com/framework/docs/providers/aws/guide/quick-start/).\
Note that you **don't need to give serverless full admin right**, only the rights listed [here](https://gist.github.com/ServerlessBot/7618156b8671840a539f405dea2704c8) is enough.
3. Follow the guide by andreivmaksimov, both [part1](https://hands-on.cloud/serverless-framework-building-web-app-using-aws-lambda-amazon-api-gateway-s-3-dynamo-db-and-cognito-part-1/) and [part2](https://hands-on.cloud/serverless-framework-building-web-app-using-aws-lambda-amazon-api-gateway-s-3-dynamo-db-and-cognito-part-2).
4. Just play around with the config  files and js, for example,
   * I used github page instead of AWS S3, since it will always be free and available 

# Notes about js
#### `||` and `&&` in js can return non-bool value [ref](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_Operators)
   ``` js
   var WildRydes = window.WildRydes || {};
   ```
#### global variable use `var`, scope use `let`
  var `foo` can be called use `window.foo` as `window` is the root scope
  ``` js
  var WildRydes = window.WildRydes || {};
  ```
#### promises, resolve and reject [ref](https://scotch.io/tutorials/javascript-promises-for-dummies)
  `then` for `resolve`, `catch` for `reject`
   ``` js
   // cognito-auth.js
       WildRydes.authToken = new Promise(function fetchCurrentAuthToken(resolve, reject) {
        var cognitoUser = userPool.getCurrentUser();

        if (cognitoUser) {
            cognitoUser.getSession(function sessionCallback(err, session) {
                if (err) {
                    reject(err);
                } else if (!session.isValid()) {
                    resolve(null);
                } else {
                    resolve(session.getIdToken().getJwtToken());
                }
            });
        } else {
            resolve(null);
        }
    });
    
    //ride.js
    var authToken;
    WildRydes.authToken.then(function setAuthToken(token) {
        if (token) {
            authToken = token;
        } else {
            window.location.href = 'signin.html';
        }
    }).catch(function handleTokenError(error) {
        alert(error);
        window.location.href = 'signin.html';
    });
   ```
