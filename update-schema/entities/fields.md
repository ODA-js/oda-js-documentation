# Field

Field have next atributes:

* **name** - string, **required** atribute. Not contain spaces or other special characters and start with a lowercase letter.
* **description** - string, any text;
* **type** - string, by default value _string_. Types supported by project:

1) string;
2) boolean;
3) number;
* **required** - boolean, by default value _false_;
* **indexed** - boolean, by default value _false_;
* **identity** - boolean, by default value _false_;
* **relation** - object. Atribute which describes relation by object with another object of data model. (See [Relation](./relation.md))





