# System Architecture

In this section we will describe main principales of the system architecture.





#### Editnig the data



We've build a common way to edit get and save data from api. It can use anystructured data source that can provide specified JSON format, so the forms canuse different data sources only by switching the data-provider.



#### Translation\/Localization



The forms we build is localizable by its nature. Every form or its small partscontain translation for every UI-field and parts. Translation is the serviceof the appilcation.



#### Translating Dictionary values



We've findout that there is two kinds of dictionary: localizable andnot localizable. so currentlty we didn't provide a way to translate it,but we have the solution using current localization service.



### Project folder structured



