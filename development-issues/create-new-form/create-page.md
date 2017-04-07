# Create page

1. Go to `/beAdmin/src/pages` folder 
2. Create a new file and name it by the name of the component.

   **Note:** You may need to create several files for different functions. Add the function as postfix to the name of your page \(e.g., `user_new` for the creating of a new user, `user_edit` for the editing of an existing user, etc\).
3. This is the page of your component. It provides the databinding of your component and the main actions with the form.

Let's look at the example of typical structure of the edit page.

**Note: ** Learn more about _RelayContainer_: https://facebook.github.io/relay/docs/api-reference-relay-container.html

```javascript
import React from 'react';
import Relay from 'react-relay';
import gql   from 'graphql-tag';

import { compose, withProps, withHandlers } from 'recompose';
import { createContainer } from 'recompose-relay';

import bindLocale from '../lib/compose/locale';
import editForm   from '../lib/compose/editForm';
import getPath    from '../lib/getPreviousPath';
import { renderChildren } from '../lib/compose/renderChildren';

import ModalZone  from '../controls/modal_zone'
import AchEdit from '../components/banking/edit_ach_form';

import ach from '../query/ach';
import currency    from '../query/currency';

import UpdateAchMutation from '../mutation/updateAch';
import AddAchToCurrencyMutation from '../mutation/addAchToCurrency';

const RelayBinding = compose(
  createContainer({
    initialVariables: {
      pageSize: 15,
      id:'unknown',
    },
    fragments: {
      viewer: () => Relay.QL `
        fragment on Viewer {
          id
          ach(id: $id) {
            ${ach.view()}
          }
        }
      `,
      currencies: () => Relay.QL `
        fragment on CurrenciesConnection {
          edges {
            node {
              ${currency.view()}
            }
          }
        }
      `,
    },
  }),
  editForm({
    isLoaded: (curr, next) => true,
    getData: (props) => {
      let result = Object.assign({},
        props.viewer.ach,
        {
          currencies: props.currencies.edges.map(e => e.node),
        }
      );
      return result;
    },
    getId: data => data.id,
    filterQuery: {
      ach: gql`{
        id
      }`,
      currency: gql`{
        currency
      }`,
    },
  }),
  withHandlers({
    onSubmit: props => event => {
      event.preventDefault();

      let ach = props.actions.getChanges('ach', 'ach');
      if (Object.keys(ach.changes).length > 1) {
        props.relay.commitUpdate(new UpdateAchMutation({
          viewer: props.viewer,
          ...ach,
        }));
      }

      let currency = props.actions.getChanges('ach', 'currency');
      if (currency.changes.currency) {
        props.relay.commitUpdate(new AddAchToCurrencyMutation({
          viewer: props.viewer,
          ...currency,
        }));
      }

      props.actions.resetChanges();
      let path = getPath(props.router.routes);
      props.router.push(path);
    },
    onReset:props => event => {
      event.preventDefault();
      props.actions.resetChanges();
      let path = getPath(props.router.routes);
      props.router.push(path);
    },
  }),
  withProps((props)=>({
    actions:Object.assign({},
      props.actions,
      {
        onSubmit: props.onSubmit,
        onReset: props.onReset,
      }
    )
  })),
  bindLocale,
  renderChildren,
)

const AchEditPage = RelayBinding(AchEdit);

export const AchEditModal = RelayBinding((props) => {
  let { locale } = props;
  return (
    <ModalZone locale={ locale }>
      <AchEdit {...props }/>
    </ModalZone>
  )
})

export default AchEditPage;
```



