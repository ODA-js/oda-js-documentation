# Create a new route

If component with databinding is ready, we can set up the path to display it.

The routes of an app are configured by React-Router and placed in the file `/beAdmin/src/routes.js`.

**Note**: learn more about React router: [https://github.com/ReactTraining/react-router](https://github.com/ReactTraining/react-router).



For adding the new route for the component:

1. Import the created page.  
   `import AchEdit, { AchEditModal } from './pages/ach_edit'`

2. Configure Relay Viewer to send the page.

   ```javascript
   const editViewAch = {
   viewer: () => Relay.QL`query { viewer }`,
   currencies: () => Relay.QL`query { currencies }`,
   }; 
   ```

3. Finally, add the route:

   ```javascript
   <Route
    path="ach/edit/:id"
    components={{ modal: AchEditModal }}
    queries={{ modal: editViewAch }}
   />
   ```

**Note:** If you want to use modal window, you must specify it in the route. Else replace _**modal**_ on _**main**_.

React-router supports hierarchical paths. Learn an existing structure of app's routes. Make sure that you place the route's config in the right section before you add route.

So, full export section for the AchEdit form in the modal window looks like this:

```javascript
export default (
  <Route
    browserHistory={browserHistory}
    path="/admin"
    component={Admin}
    queries={viewer}
  >
    <IndexRedirect to="/admin/organization/profile" />
    <Route path="organization">
      <Route
        path="banking"
        components={ { main: Banking } }
        queries={ { main: viewer } }
        prepareParams={prepareWidgetListParams}
      >
        <Route
          path="ach/edit/:id"
          components={ { modal: AchEditModal } }
          queries={ { modal: editViewAch } }
        /> 
      </Route>
    </Route>
  </Route>
)
```

Note that **the main route \('/'\)** has only **one layout component**; the parent route for the modal **\('/banking'\)** has the **main** component 'Banking'; and **the modal route \('/banking/ach/edit/:id'\)** has the **modal** component 'AchEditModal' \(_remember: it is the AchEdit component wrapped by the ModalZone_\)\).

