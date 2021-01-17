## Urent Graphql server

Written in JS/Node.js.

To develop, first install the
latest node.js
yarn or npm (a package manager).
For the production server, you'll then need to install `pm2` (process manager)

```
# install pm2 (may need sudo)
# not needed for local development
# or the CI server
npm install --global pm2
```

Then, make a file named `.env` with the following keys.

```
ACCESS_TOKEN_SECRET=accessTokenSecret
REFRESH_TOKEN_SECRET=refreshTokenSecret
MAIL_HOST="smtp.googlemail.com"
MAIL_USER="test@gmail.com"
MAIL_PASSWORD="test123"
MONGODB_URL='mongodb://localhost:27017/test'
```

## Development

```
#install packages
`yarn` or `npm i`

#start server
yarn dev or npm run dev
```

## Production

Use **staging** branch for production

```
git checkout staging
#install packages
`yarn` or `npm i`

# build server
yarn build or npm run build

# start server
yarn prod or npm run prod
```

To test GraphQL query in your local environment,
Open a browser and connect to GraphQL Playground

> http://localhost:4000/graphql

### Test Query

```gql
query {
  me {
    id
    phone
    nickname
  }
}
```
