# Mutations for Relation

The entities can be related by the different types of relations. Every relation generates two mutations:

* **addTo** + Name of the parent entity in singular + Name of relation + Name of child entity/entities
    
    adds to the parent entity a relation with the child entity. 
* **removeFrom** + Name of the parent entity in singular + Name of relation + Name of child entity/entities
    
    remove from the parent entity a relation with the child entity. 

For example, **Banking** entity relates with **CreditGuard** entity by **hasOne** relation. Then, the names of generated mutations will be:

- addToBankingHasOneCreditGuard
- removeFromBankingHasOneCreditGuard

Every mutation has input type and payload type named by the next rules:

- **Input**
    `name of mutation + Input`
    
    For example: `addToBankingHasOneCreditGuardInput`
- **Payload**
    `name of mutation + Payload`

    For example: `addToBankingHasOneCreditGuardPayload`