# Generation of UML diagrams

The structure of the system database can be described by a UML diagram. You can generate UML diagrams for all system or any part of it. 
Diagrams is based on the data schema (see [Working with schema](/update-schema.md) section).

For example, you want to see the relations of the _Campaign_ entity with an _InviteMatcher_ and it's own _InvitedMatchers_.
Generate a UML diagram for 3 entities by the next steps:

1. Open `api4/src/schema/packages` folder. Create packages for the entities:
  + **Campaign.ts**
  ``` javascript
  export default {
      name: 'Campaign',
      title: 'Campaign',
      description: 'Campaign',
      abstract: true,
      entities: [
        'Campaign',
        'InviteMatcher',
        'InvitedMatcher'
      ],
      mutations: [
      ],
    };
  ```
  **Note: ** _entities_ section contains the entities what you want to see on the final diagram of _Campaign_. 
  + **InviteMatcher.ts**
  ```javascript
  export default {
      name: 'InviteMatcher',
      title: 'InviteMatcher',
      description: 'InviteMatcher',
      abstract: true,
      entities: [
        'Campaign',
        'InviteMatcher',
        'InvitedMatcher'
      ],
      mutations: [
      ],
  };
```
  + **InvitedMatcher.ts**  
  ```javascript
  export default {
      name: 'InvitedMatcher',
      title: 'InvitedMatcher',
      description: 'InvitedMatcher',
      abstract: true,
      entities: [
        'Campaign',
        'InviteMatcher',
        'InvitedMatcher'
      ],
      mutations: [
      ],
    };
  ```
* Add to **index.ts** the definitions ot these packages:

  ```javascript
  import Campaign from './Campaign';
  import InviteMatcher from './InviteMatcher';
  import InvitedMatcher from './InvitedMatcher';
  
  export default [
    Campaign,
    InviteMatcher,
    InvitedMatcher,
  ];
  ```
* Add to **api4/src/genUml.ts** the names of packages what you want to see on the diagram:
```javascript
    packages: [
      'Campaign',
      'InviteMatcher',
      'InvitedMatcher',
    ]
```
* Run `npm run compile` command from api4
* Run `npm run gemUml` command from api4

Generated UML diagrams is placed in files:
* `api4/src/graphql-gen/Campaign/schema/schema.puml`
* `api4/src/graphql-gen/InviteMatcher/schema/schema.puml`
* `api4/src/graphql-gen/InvitedMatcher/schema/schema.puml` 

You can look any of them, because their packages are equal (and generated diagrams are equal accordingly).

The generated file looks like this: 
```javascript
@startuml
  Campaign --> "* inviteMatcher" InviteMatcher
  InviteMatcher --> "* invitedMatcher" InvitedMatcher

  class Campaign {
    name: String
    startDate: String
    endDate: String
    description: String
    howItWork: String
    organizationInfo: String
    amountGoal: number
    matchAmount: number
    id: ID
    createdAt: Date
    updatedAt: Date
    removed: boolean
    owner: String
  }
  
  class InviteMatcher {
    type: String
    displayName: String
    campaign: String
    id: ID
    createdAt: Date
    updatedAt: Date
    removed: boolean
    owner: String
  }
  
  class InvitedMatcher {
    amount: number
    email: String
    firstName: String
    lastName: String
    fullName: String
    inviteMatcher: String
    id: ID
    createdAt: Date
    updatedAt: Date
    removed: boolean
    owner: String
  }
  
@enduml
```

Generation of the image is carried out with VisualCode + additions:
* **PlantUML** with dependencies (java, graphwiz)
* **Yog PlantUML Highlight**
 
Open the generated file and click the content by the right mouse button.

You can see the _Preview of the current diagram_ in the right part of window or _export current diagram_ in one of the available formats. 

![](/assets/Снимок экрана от 2017-03-13 11-35-01.png)

We recommend to use svg format. 
If you open VScode from the root directory of the project, output images will be created in `/out/api4/src/graphql-gen/Entity/schema/schema/` folder. 