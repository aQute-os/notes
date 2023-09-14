---
---

# GraphQL 

```alloy
module GraphQLSchema

abstract sig Type {
  name: String
}

sig ObjectType extends Type {
  fields: set Field
}

abstract sig ScalarType extends Type {}
sig IntType, FloatType, StringType, BooleanType extends ScalarType {}

sig Field {
  name: String,
  type: Type
}

sig Query extends ObjectType {}

sig Schema {
  query: Query,
  types: set Type
} {
  query in types
  all t: ObjectType | all f: t.fields | f.type in types
}
```

## Issues

> Must have a GrapQL scheme contain a Query type?

Yes, in a GraphQL schema, a Query type is generally required as it serves as the entry point for data retrieval operations. According to the official GraphQL specification, if a schema provides no Query type, it is considered incomplete and should not be used for executing queries. The Query type is essential for clients to know what queries they can perform against the API.

> What is the priority of fields and methods?

Methods than fields. Fields & methods can be private


[1]: https://www.graphql-java.com
