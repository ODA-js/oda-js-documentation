# Mutations for Entity

For each entity in schema are created next mutations:

* **create** + Name of entity in singular;
* **update** + Name of entity in singular;
* **delete** + Name of entity in singular.

Take entity `City`, in schema will be create mutation with name:
`createCity`
`updateCity`
`deleteCity`

For each mutations are created - input type and payload type:
- **Input**

`name of mutation + Name of entity in singular + Input`
For example: `createCityInput`.
- **Payload**

`name of mutation + Name of entity in singular + Payload`
For example: `createCityPayload`


