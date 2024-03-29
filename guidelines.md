Guidelines & Examples
=====================

TypeReference
-------------

defines type reference for described interface "real types" (the ones interface operates on)
i.e. there is some interface which operates certain "real" type e.g. - cities

cities is a complex type, consisting of id, name and another complex type - coordinates,
which in turn consists of latitude and longtitude
if we want to say what, in some place, as a parameter, we want a city id we can do it like what:

simple notation:

    city_id
    cityId

process notation (forces checking of city_id existence)

    enum(city_id)

transform notation: pick a city , get its id

    id(city)
    city.id()

process notation - ensure existense of passed value within typed collection of city ids

    enum([city_id])

process-transform notation understood as: ensure existence of value in set,
defined by extraction id from all cities (from typed collection of cities):

    enum(id([city]))
    city.id().enum()

ComplexTypeDefinition
---------------------

simple value type expected:

    <int>

simple value type with limited length expected

    <string(160)>

type reference with expected value type

    <cityId:int>

type reference with expected value type limited to specified lenght

    <cityName:string(160)>

type reference with expected value type and actual default value

    <quantity:int|1>

type reference transformed by typeDefinitionFunctor, expected value type, actual default value

    <enum(cities):int|1>

type reference, expected value described as functor, actual default value

    <typeName:enum(1,2,3)|1>

transformed notation (forces checking of city_id existence), ensure it represented as INT, if not supplied 1 must be used as value

    <enum(city_id):int|1>

transform notation: pick a city , get its id, represent as int , if not provided assume 1 as value

    <id(city):int|1>

strong notation understood as:
    ensure existence of value in set defined by extraction id from all cities,
    ensure it is represented as int,
    defaulted to id of city known as MSK

    <enum(id([city])):int|id(city(MSK))>

full notation

    <city.enum().id():int(4)|city(MSK).id()=1>
    <id(enum([city])):int(4)|id(city(MSK))=1>
    <enum(city.id()):trim()=string(160)|city(MSK).name()=Moscow>