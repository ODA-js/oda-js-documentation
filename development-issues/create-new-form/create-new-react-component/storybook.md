# React Storybook

**Note:** learn more about Storybook and how to use it: https://getstorybook.io/docs/react-storybook/basics/quick-start-guide

React Storybook is a UI development environment for your React components. With it, you can visualize different states of your UI components and develop them interactively.

The command to run Storybook: 
`npm run storybook`

The configuration of React Storybook for the admin forms is placed in the `beAdmin/.storybook/config.js` file. If you want to view the component in Storybook, describe it in `beAdmin/components/stories` folder. 

This is the file of the description of the BonusMatcher form in Storybook: 

```javascript
import React from 'react';
import { storiesOf } from '@kadira/storybook';
import BonusMatcherEdit from '../bonus_matcher_edit';
import Layout from './layout/admin.jsx';


storiesOf('Bonus Matcher Edit', module)
  .add('Bonus Matcher Edit', () => {
    const data = {
      "goal": {
        "bonusGoal": "$100,000.00",
        "matchAmount":"$50,000.00",
        "sentFrom":""
      },
      "matchers": [
        {
          "status": "Pending",
          "firstName": "Matcher 1",
          "lastName": "",
          "email": "",
          "amountRequested":"",
          "number": "1",
          "type": "individual"
        }, {
          "status": "Pending",
          "firstName": "Matcher 2",
          "lastName": "",
          "email": "",
          "amountRequested":"",
          "number": "2",
          "type": "group"
        }, {
          "status": "Pending",
          "firstName": "Matcher 3",
          "lastName": "",
          "email": "",
          "amountRequested":"",
          "number": "3",
          "type": ""
        }
      ]
    };
    const ctx = {
      actions: {
        onChange: name => e  => {e.preventDefault();},
        onResetModal: () => {},
        onSubmitModal: () => {},
        onSubmit: () => {}
      },
      locale: 'en',
    };
    return (
      <Layout>
        <div className="form-wrapper">
          <BonusMatcherEdit
            data={data}
            actions={ctx.actions}
            locale={ctx.locale}
          />
        </div>
      </Layout>
    );
  });
```

It contains:
* import of form component;
* the required data for the form (it included a locale and actions);
* the component with a wrapper and with the required props.