# Node REM

NodeJS Rest Express MongoDB (REM) - a production-ready lightweight backend setup.

[![Build Status](https://travis-ci.org/ngduc/node-rem.svg?branch=master)](https://travis-ci.org/ngduc/node-rem) [![Maintainability](https://api.codeclimate.com/v1/badges/11155b15b675ef311f72/maintainability)](https://codeclimate.com/github/ngduc/node-rem/maintainability)

🌟 It rains ~~cats and dogs~~ features:

```
  Typescript      Express 4.15       CORS     Helmet    DotEnv   joi (validation)   forever
  Mongoose 4.9    Passport  JWT      Await
  Tslint          Apidoc    Docker   Husky    Morgan    Travis   Unix/Mac/Win (Powershell)
  Tests
            Mocha  Chai     Sinon    istanbul
  MORE:
            HTTPS           HTTP2 (spdy)      Socketio 2.1       Init DB Data
            Slack message   Nodemailer        Mailgun            Email Templates    Forgot Password
            VSCode Debug    Dependabot        Codacy             File upload (multer)
      API
            API response    (data, meta: limit, offset, sort)    Transform res
            apiJson         Pagination query
            Regex query     Whitelist fields in response         Populate deep fields
            mstime          API response time     Stack trace in Response
```
  - More details in [Documentation / Features](src_docs/features.md)
  - [Live Demo](https://node-rem-demo.now.sh/) (login & inspect API calls to learn more)

### 📦 Installation

Require: `MongoDB` and `NodeJS v8.12.0 +`

Clone this project:
```
git clone https://github.com/ngduc/node-rem.git your-app
cd your-app
rm -rf .git
yarn
```
- Update `package.json` and `.env` file with your information.
- Run `yarn dev`, it will create a new Mongo DB "node-rem"
- Verify `yarn test` can run all unit tests.
- Verify: use Postman to POST https://localhost:3009/v1/auth/register to create a new user. (set payload to have email, password)
```
curl -k -d '{"email": "example1@email.com", "password": "testpsw"}' -H "Content-Type: application/json" -X POST https://localhost:3009/v1/auth/register
```

### 🔧 Commands

```
yarn dev      launch DEV mode
yarn start    launch PROD mode
yarn stop

yarn test     Run tests   (requires MongoDB)
```

### 📖 Features

Your simple `API Route Handler` will have a nice syntax like this: (packed with ~~vitamins~~ cool stuffs)
```js
exports.list = async (req: Request, res: Response, next: NextFunction) => {
  try {
    const data = (await User.list(req)).transform(req); // query & run userSchema.transform() for response
    apiJson({ req, res, data, model: User }); // return standard API Response
  } catch (e) {
    next(e);
  }
};
```

API Response is similar to [JSON API](http://jsonapi.org/examples/#pagination) standard:

```js
GET https://localhost:3009/v1/users?fields=id,name&name=*john* (get id & name only in response)
GET https://localhost:3009/v1/users?role=user&page=1&perPage=20 (query & pagination)
GET https://localhost:3009/v1/users?role=user&limit=5&offset=0&sort=email:desc,createdAt
{
    "meta": {
        "limit": 5,
        "offset": 0,
        "sort": {
            "email": -1,
            "createdAt": 1
        },
        "totalCount": 4,
        "timer": 3.85,
        "timerAvg": 5.62
    },
    "data": [
        {
            "id": "5bad07cdc099dfbe49ef69d7",
            "name": "John Doe",
            "email": "john.doe@gmail.com",
            "role": "user",
            "createdAt": "2018-09-27T16:39:41.498Z"
        },
        // more items...
    ]
}
```
Example of generated API Docs (using `apidoc`) - https://node-rem.netlify.com

### 📖 Documentation

- [Documentation / Features](src_docs/features.md)
- [Build System](src_docs/build.md)
- [Dependencies Notes](src_docs/dependencies.md)
- [Change Log](CHANGELOG.md)

### 🙌 Thanks

All contributions are welcome!