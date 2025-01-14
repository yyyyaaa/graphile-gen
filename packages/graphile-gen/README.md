# graphile-gen

Generate the GraphQL mutations/queries for your PostGraphile projects

* assumes using simple inflection

```sh
npm install graphile-gen
```

## introspecting via GraphQL

```js
import {
  generate
} from 'graphile-gen';
import { print } from 'graphql/language';

const gen = generate(resultOfIntrospectionQuery);
const output = Object.keys(gen).reduce((m, key) => {
  m[key] = print(gen[key].ast);
  return m;
}, {});

console.log(output);
```

# output

which will output the entire API as an object with the mutations and queries as values

```json
{
  "createApiTokenMutation": "mutation createApiTokenMutation($id: UUID, $userId: UUID!, $accessToken: String, $accessTokenExpiresAt: Datetime) {
  createApiToken(input: {apiToken: {id: $id, userId: $userId, accessToken: $accessToken, accessTokenExpiresAt: $accessTokenExpiresAt}}) {
    apiToken {
      id
      userId
      accessToken
      accessTokenExpiresAt
    }
  }
}
```
