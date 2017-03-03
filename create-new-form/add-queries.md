# Add queries

**Note: **

* learn more about queries in GraphQL: [http://graphql.org/learn/queries/](http://graphql.org/learn/queries/)
* learn more about Relay specification of GraphQL queries: 
  [https://facebook.github.io/relay/docs/graphql-relay-specification.html\#content](https://facebook.github.io/relay/docs/graphql-relay-specification.html#content)

In order to get data from the database, we need to describe GraphQL queries.  The queries are used in the pages, and they are placed in the `/beAdmin/src/query` folder.   
**Note: ** Name file of the query by the name of entity that you want to get. If the name of the file is composite, you should use `_` as a divider. And the name should be in lower case.

In our example we need two queries.

1.**Currency \(currency.js file\)** is the collection of currencies to display in select field of the form. If you will choose one of the values, the corresponding entity will be related with Ach through a mutation.

The code of this query describes the fields of _Currency_ entity. It will be used in the page with `import currency from '../query/currency'` and then `currency.view()`. It is also used in all queries that have a currency field.

```javascript
import Relay from 'react-relay';

export default {
  view: ()=> Relay.QL`
    fragment on Currency {
      value
      key
      symbol
      id
    }`,
}
```

2.**Ach \(**_**ach.js**_**\)** is the main entity for our form.

```javascript
import Relay from 'react-relay';

import country from './country.js';
import currency from './currency.js';

import UpdateAchMutation from '../mutation/updateAch';
import CreateAchMutation from '../mutation/createAch';

import AddAchToCurrencyMutation from '../mutation/addAchToCurrency';


export default {
  create: ()=> Relay.QL `
    fragment on Ach {
      id
      status
      currency {
        ${currency.view()}
      }
      ${UpdateAchMutation.getFragment('ach')}
      ${CreateAchMutation.getFragment('ach')}
    }`,
  edit: ()=> Relay.QL `
    fragment on Ach {
      id
      status
      currency {
        ${currency.view()}
      }
      ${UpdateAchMutation.getFragment('ach')}
      ${AddAchToCurrencyMutation.getFragment('ach')}
    }
    `,
  view: () => Relay.QL `
    fragment on Ach {
      id
      status
      currency {
        ${currency.view()}
      }
      ${UpdateAchMutation.getFragment('ach')}
      ${AddAchToCurrencyMutation.getFragment('ach')}
    }
  `,
  grid:() => Relay.QL`
    fragment on Ach {
      id
      status
      currency {
        ${currency.view()}
      }
    }
  `,
}
```

It has this sections:

* **import** contains Relay, queries for the child entities and mutations. The declaration of mutations requires an update of data in places where these fragments are used.

**Note: ** learn more about mutations from [the 'Describe mutations' section](/create-new-form/describe-mutations.md) of this documentation.

* **export** contains named fragments for the description of entity's fields. The query can used in different places of the system and different parts of the entity may be needed. Therefore, there are several named fragments in the query file. For example, the `Create` fragment is used in CreateAch form and so on. 



