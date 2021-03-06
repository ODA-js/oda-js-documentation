# Create custom mutation

1.Go to folder `src/schema/mutations`

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

3.In file `src/schema/mutations/index.ts` define new Mutation:

```javascript
import createMediumAddCampaign from './createMediumAddCampaign';

export default [
  createMediumAddCampaign,
];
```

4.Run for generate mutation:

```
npm run compile
```

5.Go to folder `src/graphql-gen/system/mutation`  
Find folder with name of your custom mutation \(`createMediumAddCampaign`\). Open file `resolver.ts` it is template for your custom mutation. **Copy code from this file**.

6.Go to folder `src/model/common/mutations`

7.Create new file with name:  
`name your custom mutation + .resolver.ts (for example, createMediumAddCampaign.resolver.ts)`  
and past copied code. In this file you describes of behavior your custom mutation.

For example, here's custom mutation which create new image for Campaign. For this mutation, we need to create new image and then create relation between new image and Campaign.

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
          campaign?: any; // Return Campaign,
        };

        let campaignId = fromGlobalId(args.campaign).id;

        // Find Campaign
        let campaignObj = await context.connectors.Campaign.findOneById(campaignId);

        // Create Image
        let medium = await context.connectors.Medium.create({
          type: args.type,
          url: args.url,
        });
        
        // Create relation between found Campaign and new Image
        await context.connectors.Campaign.addToMedia({
          campaign: campaignId,
          medium: medium.id,
        });
        
        // Result which return to client
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

8.Go to folder `src/model/common`.

9.In file `index.ts` define new custom mutation

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
In mutation use `connectors` which take from `context`. More info here: [Connectors and models](https://github.com/apollographql/graphql-tools/blob/master/designs/connectors.md).
Example connector:
```javascript
  public async findOneById(id?: string) {
    logger.trace(`findOneById with ${id} `);
    let result = await this.loaders.byId.load(id);
    return this.ensureId(result ? result.toJSON() : result);
  }
```





