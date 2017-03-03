# Describe mutations

**Note**:

* Learn more about mutations in GraphQl: [http://graphql.org/learn/queries/\#mutations](http://graphql.org/learn/queries/#mutations)
* Learn more about mutations in Relay: 
  [http://blog.pathgather.com/blog/a-beginners-guide-to-relay-mutations](http://blog.pathgather.com/blog/a-beginners-guide-to-relay-mutations)

If you want to use one of the system mutations, you should describe them in the `/beAdmin/src/mutation` folder.

Create file of the mutation and name it with the name of the mutation what you want to describe. Make sure that required mutation is not already exist.

**Note**: check the list of available mutations in the Documentation Explorer of GraphiQL. \(See Graphiql section for more information\)

In our example we need two mutations:

* **UpdateAch** updates fields of an existed Ach entity. The 'updateAch.js' file has next code:

  ```javascript
  import Relay from 'react-relay';
  export default class UpdateAchMutation extends Relay.Mutation {

  getVariables() {
    return {
      id: this.props.ach.id,
      ...this.props.changes,
    }
  }

  getMutation() {
    return Relay.QL`mutation{updateAch}`;
  }

  static fragments = {
    ach: () => Relay.QL`
      fragment on Ach {
        id
      }
    `,
  }

  getFatQuery() {
    return Relay.QL`
      fragment on updateAchPayload {
        ach
      }
    `;
  }

  getConfigs() {
    return [{
      type: 'FIELDS_CHANGE',
      fieldIDs: {
        ach: this.props.ach.id,
      },
    }];
  }

  getOptimisticResponse() {
    return {
      ach:{
        ...this.props.changes
      }
    };
  }
  }
  ```

  _getVariables\(\)_ parses data from the page \(see ['Create page' section](/create-new-form/create-page.md\) of this documentation\).
  _getMutation\(\)_ gets the corresponding system mutation.
  _getFatQuery\(\)_ describes via _fragments_ what the data must change.
  _getConfigs\(\)_ defines the type of an operation and the required data to find the entity. In this example the operation is a field change and the required data is an id of  the entity.
  _getOptimisticResponse\()\) and returns the input of the mutation. It is a set of changing fields.

* **AddAchToCurrency** relates an existing Currency entity with an existing Ach entity and has the same code.



