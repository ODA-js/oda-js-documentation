# Create customer mutation

1.Go to folder `api4/src/schema/mutations`

2.Create a new file with description of the mutation. 

**Note:** File must be named by next rules:  
`mutation (create/update/delete) + name entity + action (relation with other entity and etc).ts`  
For example: you need to add new image to Campaign. Name of mutation will be next:  
`createMediumAddCampaign.ts`

3.in file `index.ts` define new Mutation:

```javascript
import createMediumAddCampaign from './createMediumAddCampaign';

export default [
  createMediumAddCampaign,
];
```

4.In terminal go to root folder of your project and generate schema of project:

```
cd path to your project/api4
npm run compile
```

5.Go to folder `api4/src/graphql-gen/default/mutation`  
Find folder with name of your customer mutation \(`createMediumAddCampaign`\). Open file `resolver.ts` it is template for your customer mutation. **Copy code from this file**.

6.Go to folder `api4/src/model/common/mutations`

7.Create new file with name:  
`name your customer mutation + .resolver.ts (for example, createMediumAddCampaign.resolver.ts)`  
and past copied code. In this file you can also add description of behavior your customer mutation.

For example, here's customer mutation which create new image for Campaign. For this mutation, we need to create new image and then create relation between new image and Campaign.

```javascript
import { mutateAndGetPayload, idToCursor } from '@charidy/graphql-backend-common';
import { fromGlobalId } from 'graphql-relay';
import Connectors from '../../packages/default/connectors';

export const resolver = {
  createMediumAddCampaign: mutateAndGetPayload(
    async (
      args: {
        campaign?: string,
        type?: string,
        url?: string,
      },
      context: { connectors: Connectors },
      info
    ) => {
      let result: {
        mediumEdge?: any; // Return Medium of Campaign,
        campaign?: any; // Return Medium of Campaign,
      };

      let campaignId = fromGlobalId(args.campaign).id;

      let campaignObj = await context.connectors.Campaign.findOneById(campaignId);


      let medium = await context.connectors.Medium.create({
        type: args.type,
        url: args.url,
      });

      await context.connectors.Campaign.addToMedia({
        campaign: campaignId,
        medium: medium.id,
      });

      result = {
        campaign: campaignObj,
        mediumEdge: {
          cursor: idToCursor(medium._id),
          node: medium,
        },
      };

      return result;
    },
  ),
};
```

8.Go to folder `api4/src/model/packages/default`.

9.In file `index.ts` define new customer mutation

```javascript
import { common } from '@charidy/graphql-backend-gen';

const { types: commonTypes } = common;
const {deepMerge} = common.lib;

import * as graphql from './../../../graphql-gen/default/entity';
import * as mutations from './../../../graphql-gen/default/mutation';

//customer mutation
import * as createMediumAddCampaign from '../../common/mutations/createMediumAddCampaign.resolver';
//customer mutation

import passwordHook from '../../common/api-hooks/fixupPassword';

export const hooks: { [key: string]: any }[] = [
  ...passwordHook,
  ...commonTypes.hooks,
  ...graphql.hooks,
];

export const resolver: { [key: string]: any } = deepMerge(
  commonTypes.resolver,
  graphql.resolver,
);

export const query: { [key: string]: any } = deepMerge(
  commonTypes.query,
  graphql.query,
);

export const typeDef: () => string[] = () => {
  return [
    ...commonTypes.typeDef(),
    ...graphql.typeDef(),
    ...mutations.typeDef(),
  ];
};

export const mutationEntry: () => string[] = () => {
  return [
    ...commonTypes.mutationEntry(),
    ...graphql.mutationEntry(),
    ...mutations.mutationEntry(),
  ];
};

export const queryEntry: () => string[] = () => {
  return [
    ...commonTypes.queryEntry(),
    ...graphql.queryEntry(),
  ];
};

export const viewerEntry: () => string[] = () => {
  return [
    ...commonTypes.viewerEntry(),
    ...graphql.viewerEntry(),
  ];
};

export const mutation: () => { [key: string]: any } = () => {
  return deepMerge(
    commonTypes.mutation(),
    graphql.mutation(),
    mutations.mutation(),
    createMediumAddCampaign.resolver, //customer mutation

  );
};
```



