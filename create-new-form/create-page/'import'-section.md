## **'Import' section**

**'Import' section** defines external components and modules that we need for databind and display of our component.  
The databinding of the component is produced by Relay.

In this section you need:

1. **React** for working with React components.  
   `import React from 'react'`

2. **Relay** for databinding.  
   `import Relay from 'react-relay'`  
   **Note: **_learn more about Relay:_ [https://facebook.github.io/relay/](https://facebook.github.io/relay/)

3. **gql** for parsing graphQL query.  
   `import gql   from 'graphql-tag'`

4. **Recompose** and **Recompose-relay** to create a container with required actions and procedures for data processing.  
   `import { compose, withProps, withHandlers } from 'recompose'`  
   `import { createContainer } from 'recompose-relay'`

5. **bindLocale** for localization of your component.  
   `import bindLocale from '../lib/compose/locale'`

6. **editForm** \(or **createForm**\) with the procedures set of editing the form fields, getting and resetting changes.  
   `import editForm   from '../lib/compose/editForm'`

7. **getPath** for the calculation of the previous path when you close/submit the form.  
   `import getPath    from '../lib/getPreviousPath';`

8. **renderChildren** for the hierarchical rendering of the child components.  
   `import { renderChildren } from '../lib/compose/renderChildren'`

9. **Components and controls** what you need. It is AchEdit form and ModalZone window for form's placing in this example.  
   `import ModalZone  from '../controls/modal_zone'`  
   `import AchEdit from '../components/banking/edit_ach_form';`

10. **Queries** for getting data from the database.   
    `import ach from '../query/ach'`  
    `import currency    from '../query/currency'`  
    **Note**: Learn more about Queries in the ['Add queries' section](/create-new-form/add-queries.md) of this documentation.

11. **Mutations** for modification \(create, update, remove\) of data in the database.   
    `import UpdateAchMutation from '../mutation/updateAch'`  
    `import AddAchToCurrencyMutation from '../mutation/addAchToCurrency'`  
    **Note**: Learn more about Mutations in the ['Describe mutations' section](/create-new-form/describe-mutations.md) of this documentation.



