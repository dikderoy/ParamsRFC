Concepts:
=========

1. describe a process needed to prepare value from context
2. describe a process needed to validate provided value
3. describe expected type
4. describe behavior if value not provided
5. all in one simple definition of a parameter no longer than one line
6. reference described pameter or type within the document containing definition or reference to one
7. present processes and definitions as functional sequences and / or call chains

Usage concepts:
===============

type as reference to context
----------------------------

simple textual reference to contextual entity within document
e.g. "city" - is an entity with known attributes on which described interface operates on
it is contextualy described

type as function call
---------------------

cast abstract textual definition of entity to contextualy defined type
e.g. in document we contextualy define a type "city" as entity, having id, name and location(lat,lng) attributes

    city(MSK)

abstract definition "MSK", which references Moscow, Russia - is casted to known contextual entity "city"
so output value of this sentence is object of type "city", representing a city of Moscow
with some integer id, name equal to "Moscow" and location(lat,lng) subentity

attribute or field as function call
-----------------------------------

pick an attribute from object of type by calling attribute name from typeReference
e.g.

    id(city)

meas what you need to supply attribute "id" of type "city"

chains of transformation
------------------------

transformer element allows you to describe sequences of transformations applyed to type or value
under definition of transformation you can understood:

- picking attribute from typeReference
- applying self-describable function to typeReference
- calling contextualy known method of type

e.g.

    city.location.latitude - is chain to peek a nested attribute from typeReference
    enum([city].name) - extract and enumerate name from all cities

chains of transformation with dependencies
------------------------------------------

used to describe changeable value treating dependent on other parameter or abstract condition

    <address(&channelType)=email/phone:string|null>

treating of this parameter's value is dependent on others parameter value (<channelType>) and could be resolved as email or phone

simple types
------------

one may specify expected simple type as parameter value, transformation result, default value or full definition of parameter
e.g.

    <int> - expecting some integer value
    <str(100)> - expecting string no longer than 100 chars
    <enum([city].id):int> - expecting enumerated city id as int

collections
-----------

one may specify parameter expected to be a collection of type
e.g.

    <[int]> - expecting array of int
    <list([city].location)=[location]> - expecting collection of locations extracted from city collection