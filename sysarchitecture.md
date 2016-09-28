# System Architecture

in this section we will see what is the architecture of the system we provide to Charidy.




### Data layer



Data layer is build using GraphQL. We use Facebook Relay framework as transportlayer for GraphQL.



As far as React is a UI-framework to build single page appilcation, it isrenders server data on the client, but we can also can use server side renderingengine for every client page and this feature can be configured differentlyfor any route in the system. This techinque is called server-side render \(SSR\).SSR is very usefull for SEO optimization.



### UI



We've used beAdmin theme for bootstrap and building reusable component forthe appliation to provide true React UIX. We use `react-bootstrap` library.Every form reuse existing component-base to make the UI feel consistent withthe selected theme.



#### Storybook



We use storybook for designing the forms of an appilcation to make thedevelopment prosess as far as possible independent one aspect of developmentfrom another. Storybook provide us with ability to build and test formsconsistency with out connecting it to real data.



#### Editnig the data



We've build a common way to edit get and save data from api. It can use anystructured data source that can provide specified JSON format, so the forms canuse different data sources only by switching the data-provider.



#### Translation\/Localization



The forms we build is localizable by its nature. Every form or its small partscontain translation for every UI-field and parts. Translation is the serviceof the appilcation.



#### Translating Dictionary values



We've findout that there is two kinds of dictionary: localizable andnot localizable. so currentlty we didn't provide a way to translate it,but we have the solution using current localization service.



### Project folder structured



