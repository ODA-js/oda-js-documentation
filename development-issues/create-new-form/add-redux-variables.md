# Add global variables

If "global" variables need to add, we can set up it in redux.

**Note**: learn more about Redux: [http://redux.js.org/docs/introduction/](http://redux.js.org/docs/introduction/).

Compose file put to:  `/lib/compose/example.js`.

It may contain:

```js
import { connect } from 'react-redux'

export default connect(
  (state)=>({locale: state.locale}),
);
```

Reducer file put to: `/lib/compose/example.js`

It contain:

```js
export const LOCALE_CHANGE = "locale.change";

export const action = (locale) => ({
  type: LOCALE_CHANGE,
  locale,
});

export const reducer = (state = {}, action)=>{
  switch (action.type) {
    case '@@INIT':
    case '@@redux/INIT':
      return 'en';
    case LOCALE_CHANGE:
      let locale = action.locale;
      return locale;
    default:
      return state;
  }
}
```

It bind to store. File: `/beAdmin/src/store.js`

```js
import createSaturnStore from '~/common/client/redux/store';
import ReduxThunk from 'redux-thunk'
import {reducer as locale} from '~/lib/reducers/localization';
import {reducer as notification} from '~/lib/reducers/notification';
import {reducer as selectorId} from '~/lib/reducers/selectId';
import {reducer as busyIndicator} from '~/lib/reducers/busyIndicator';

const createStore = ()=>
  createSaturnStore({
    reducers: {locale, notification, selectorId, busyIndicator},
    middleware:[ReduxThunk/*.withExtraArgument(client)*/]
  });

export default createStore;
```

For using on page need bind with relay-page for example **bindLocale** or **bindLiveOrgId **functions on Relay Binding section.

