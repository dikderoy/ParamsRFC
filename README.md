ParamsRFC
=========

*Reference for description of API parameters and their functional properties in Technical Documentation*

Main idea of this reference is to give you an instrument to describe various parameters in documents,
whatever you need it.

The description goes in context, and this allows description to be informative.

To give your developer a lead there to look for incoming data,
how to preprocess it and how to validate it, once it comes throught the interface

**see [concepts](/dikderoy/ParamsRFC/blob/master/concept.md) to fully understand the concepts of this reference**

Examples:
---------

Usualy, after you discussed your project with developers - you have something as Project Data Model,
which describes entities upon which project operates on.

It may be concrete declaration, class reference or abstract definition which only names and describes structures.

e.g. you abstractly described a structure of address

something like that:

Address is a complex type which has following parts(properties)

+ country
+ region
+ city
+ ward
+ street
+ house
+ flat
+ postalIndex

where Country, Region, City, Ward is also a complex type consisting of:

+ id
+ name
+ coordinates(lan,lat)
+ cross-references in structure (e.g. you can tell which wards city has)



so, having something like that, you can refer to it.

Let's say we need to describe just an REST-API URL to retrive a City with its info.
(assuming host part of API is off description)

here you go:

```
GET /api/city/<city.id:int>
```

Or we need to describe a parameter of a function:

```
<enum([country.id]):country.id=int|country(USA).id>
```

this line tells us following: here expected an id of country as integer value,
which must be in enumerated range (known to system) and if value is not provided,
interface must default it to id of USA country

and finally to describe full interface of Address in JSON based REST-API:

```
POST /api/address
{
	countryId: <enum([country.id]):country.id=int|country(USA).id>,
	regionId: <enum([country(&countryId).region.id]):region.id=int|required>,
	cityId: <enum([region(&regionId).city.id]):city.id=int|required>,
	wardId: <enum([city(&cityId).ward.id]):ward.id=int|required>,
	street: <string(300)|required(5)>,
	house: <int|required>,
	flat: <int|null>,
	postalIndex: <int|ward(&wardId).postalIndex>
}
```

**for more examples and full reference check [reference](/dikderoy/ParamsRFC/blob/master/reference.txt) and [guidelines](/dikderoy/ParamsRFC/blob/master/guidelines.md)**