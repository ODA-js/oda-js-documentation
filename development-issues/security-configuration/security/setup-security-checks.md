# Setup security checks

The file `api4/src/model/hooks.ts` is responsible for security setup.

The model infrastructure has hooks-api to make generation-time modifications.

when we genearates the schema we use it like mentioned in `api4/src/generate.ts` and `api4/src/genUml.ts`.

the source of `generate.ts`-flie

```javascript
import * as  path from 'path';
import { generator } from '@charidy/graphql-backend-gen';
import schema from './schema';
import * as modelHooks from './model/hooks';

generator({
  // role: 'admin', // public, admin, system
  hooks: [
    // entities
    modelHooks.adapter,
    modelHooks.userCollectionName,
    // fields
    // fix default visibility
    modelHooks.accessFixEntities,

    modelHooks.defaultVisibility,
    modelHooks.dictionariesVisibility,

    // secure fields without default
    modelHooks.securityFields,
    modelHooks.ownerFields,
    // metadata
    modelHooks.securityAcl,
    modelHooks.ownerAcl,

    // mutations
    modelHooks.accessFixMutations,
    modelHooks.defaultMutationAccess,
    // id is visible by default to all
    modelHooks.defaultIdVisibility,
    // user
    modelHooks.userIsAdmin,
    modelHooks.userIsSystem,
  ] as any,
  pack: schema,
  rootDir: path.join(__dirname, '../src', 'graphql-gen'),
  config: {
    graphql: false,
    packages: true,
  },
});

```

### hooks

The hook tell the system wiich entities and how must be changed.

for example this hook updates all entities fields `createdBy`,`updateBy`,`createdAt`, `updatedAt` with metadata inoformation about acl, that is it only read for `admin`-user profile.


```javascript
export let securityAcl = {
  name: 'security',
  'entities.*.fields.[createdBy,updateBy,createdAt, updatedAt].metadata.acl.read': 'admin',
};
```

**selectors** 

`*` -  all listed subitems

`[...]` - only listed items

`^[...]` - all except listed items
 
**NOTE!!!**

hooks is just json files that can be packed in one line

for example this record `entities.User.fields.name.metatdata.acl.read:'owner'` will be transformed to 
```
{
  entities: {
    User:{
      fields:{
        name:{
          metadata:{
            acl:{
              read:'owner'
            }
          }
        }
      }
    }
  }
}
```

**Using this hooks developer can shape model to any structure of model he need.
**

