# Generate Queries

The generated queries includes: 

* Query to get the single entity by unique fields (id, key, ...)
    **singular name of the entity** (id, key)
    _For example: user (id: !ID)_

* Query to get list of entities with parameters.
    **plural name of the entity**( [_params_] )
    _For example: users (first: 10, last: 15)_

_params_ includes: 

1.**Variables of the pagination**
    - before
    - after
    - first
    - last
    - limit 
    - skip
    - offset  
                
2.**filter** returns the entities where one or more fields contains the values from the filter.

3.**orderBy** sort results by the specified **indexed field**.

4.**System parameters** like _owner_ and others.