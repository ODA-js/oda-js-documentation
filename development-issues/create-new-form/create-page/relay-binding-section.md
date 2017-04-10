## 'Relay Binding' section

**Note: **

* Learn more about Recompose and it's functions mentioned below: [https://github.com/acdlite/recompose/blob/master/docs/API.md\#toc](https://github.com/acdlite/recompose/blob/master/docs/API.md#toc)
* Learn more about Relay queries, fragments and mutations: [https://facebook.github.io/relay/docs/api-reference-relay-ql.html](https://facebook.github.io/relay/docs/api-reference-relay-ql.html) 
* Learn more about Relay Container: [https://facebook.github.io/relay/docs/api-reference-relay-container.html](https://facebook.github.io/relay/docs/api-reference-relay-container.html)

**'Relay binding' section** is contained in the "RelayBinding" constant. It is the function _compose\(\)_ from Recompose.

It consists of six parts:

**1. createContainer** contains the queries for getting data.  
`Viewer` describes a query for getting the main \(parent\) entity for view on the form. You also may need additional entities like a collection of values for a dropdown list or an other entity. In this example `Currencies` fragment is a collection of currencies to select and relate it with _Ach_ entity.

```javascript
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
  })
```

**Note:** If the component is opened in the modal window from some parent form, you must add a fragment for the component's data to _CreateContainer_ of the **parent** page, too.

**2.  editForm** contains the set of the procedures to edit form fields, get and reset changes. Besides we describe the next functions:

```javascript
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
  })
```

_GetData_ eliminates unnecessary nesting \(like `edge{node {...}}`\) and forms the data for sending to the component.  
_filterQuery_ describes fields that you want to check on changes. The fields corresponds to the fragments from _CreateContainer\(\)_.

**3. withHandlers** contains `onSubmit` and `onReset` actions.

* **onSubmit** parses the changing data of the form and sends it to the server through _Update_ \(or _AddTo_, if you need to relate the entities\) mutation.

* **onReset** discards the changes and returns the user to the previous page.

```javascript
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
  })
```

**4. withProps** connects the definition of above-mentioned handlers to an existing actions as a prop:

```javascript
withProps((props)=>({
    actions:Object.assign({},
      props.actions,
      {
        onSubmit: props.onSubmit,
        onReset: props.onReset,
      }
    )
  }))
```

Then handlers will become available as _{actions.handlerName}_ in the React component.

**5. bindLocale** provides the localization of your component. It connects to the state of an application, gets the locale value and sends it to the component.

**6. bindCityOrgId **provides initial rerendering form by using city select box\(actual with saving city & country\). 

**7. bindCountryFilter **provides filtering city by country. 

**8. bindLiveOrgId **provides initial load organization by selecting id. 

**9. renderChildren** provides the hierarchical rendering of the child components.

