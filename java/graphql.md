---
topic: GraphQL-java
---

# GraphQL-java

## Problem

A client-server protocol to retrieve complex JSON data from a server using a query language. 

## Examples

* Access an address book on a server
* Access an abstract syntax tree

## Description

[GraphQL][2] is a query language and runtime for APIs developed by Facebook. It allows clients to request only the data they need, enabling more efficient data retrieval compared to REST APIs. GraphQL provides a strongly-typed schema, introspection capabilities, and allows for real-time updates through subscriptions. It supports queries, mutations for data modification, and aggregating data from multiple sources.


## Structure of GraphQL

```alloy
module GraphQL


abstract sig Type {
	name : String
}
abstract sig ScalarType extends Type {}

sig ListType extends Type {
	component : Type
}

one sig IntType , FloatType, StringType, BooleanType, IDType extends ScalarType {}

abstract sig StructuredType  extends Type {
  fields: set Field,
  directives: set Directive,
}

sig InterfaceType extends StructuredType {}

sig ObjectType extends StructuredType {
  implements: set InterfaceType
}

sig EnumType  extends Type {
	values : set String
} 

abstract sig NamedType {
	name		: String,
	type		: Type
}

sig ArgumentType extends NamedType {
}

sig Field extends NamedType {
    arguments: set ArgumentType,
}



abstract sig Directive {}
sig Include, Skip, Deprecated extends Directive {
  args: set Field
}


one sig QueryType extends ObjectType {}
lone sig MutatonType extends QueryType {}


one sig Schema {
  types: set Type,
}

sig Value {
	type	: Type
}

one sig QueryDoc {
	selections 	: set Selection,
    fragments 	: set Fragment
}

sig Fragment {
  id : String,
  on: StructuredType,
  fields: set FieldQuery
}

sig Selection {
	field 			: FieldQuery,
	fragment	 	: set Fragment
}

sig FieldQuery {
    alias			: lone String,
	field 			: Field,
	arguments 		: ArgumentType lone -> Value,
    directives 		: set Directive,
	selections	 	: set Selection
}	

```

## Review GraphQL 




## Issues

> Must have a GrapQL scheme contain a Query type?

Yes, in a GraphQL schema, a Query type is generally required as it serves as the entry point for data retrieval operations. According to the official GraphQL specification, if a schema provides no Query type, it is considered incomplete and should not be used for executing queries. The Query type is essential for clients to know what queries they can perform against the API.

> What is the priority of fields and methods in beans?

Methods than fields. Fields & methods can be private


[1]: https://www.graphql-java.com
[2]: https://graphql.org/
