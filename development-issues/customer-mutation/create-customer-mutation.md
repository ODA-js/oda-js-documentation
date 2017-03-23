# Create customer mutation

1.Go to folder `api4/src/schema/mutations`

2.Create a new file with description of the mutation.

**Note:** File must be named by next rules:  
`mutation (create/update/delete) + name entity + action (relation with other entity and etc).ts`  
For example: you need to add new image to Campaign. Name of mutation will be next:  
`createMediumAddCampaign.ts`

File _createMediumAddCampaign.ts_:

```javascript
export default {
  'name': 'createMediumAddCampaign',
  'desciption': 'Campaign - page Campaign Visual Editor - add new image for Campaign',
  'args': [
    {
      'name': 'campaign',
    },
    {
      'name': 'type',
    },
    {
      'name': 'url',
    },
  ],
  'payload': [
    {
      'name': 'campaign',
      'type': 'Campaign',
    },
    {
      'name': 'mediumEdge',
      'type': 'MediaEdge',
    },
  ],
};
```

3.In file `index.ts` define new Mutation:

```javascript
import createMediumAddCampaign from './createMediumAddCampaign';

export default [
  createMediumAddCampaign,
];
```

4.In terminal go to folder **api4** of your project and generate schema of project:

```
cd path_to_your_project/api4
npm run compile
```

5.Go to folder `api4/src/graphql-gen/system/mutation`  
Find folder with name of your customer mutation \(`createMediumAddCampaign`\). Open file `resolver.ts` it is template for your customer mutation. **Copy code from this file**.

6.Go to folder `api4/src/model/common/mutations`

7.Create new file with name:  
`name your customer mutation + .resolver.ts (for example, createMediumAddCampaign.resolver.ts)`  
and past copied code. In this file you can also add description of behavior your customer mutation.

For example, here's customer mutation which create new image for Campaign. For this mutation, we need to create new image and then create relation between new image and Campaign.

```javascript
import { mutateAndGetPayload, idToCursor } from '@charidy/graphql-backend-common';
import { fromGlobalId } from 'graphql-relay';
import Connectors from '../../connectors';

import { common } from '@charidy/graphql-backend-gen';

export class CreateMediumAddCampaignMutation extends common.types.GQLModule {
  protected _mutation = {
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
}
```

8.Go to folder `api4/src/model/common`.

9.In file `index.ts` define new customer mutation

```javascript
import { common } from '@charidy/graphql-backend-gen';
import { FixupPasswordHook } from './api-hooks/fixupPassword';
import { CreateMediumAddCampaignMutation } from './mutations/createMediumAddCampaign.resolver'; // your customer mutation

export class CommonExtends extends common.types.GQLModule {
  protected _extend = [
    new FixupPasswordHook({}),
    new CreateMediumAddCampaignMutation({}),
  ];
}
```
In mutation use `connectors` which take from `context`. More info here: https://github.com/apollographql/graphql-tools/blob/master/designs/connectors.md.
Example connector:
```javascript
  public async findOneById(id?: string) {
    logger.trace(`findOneById with ${id} `);
    let result = await this.loaders.byId.load(id);
    return this.ensureId(result ? result.toJSON() : result);
  }
```





