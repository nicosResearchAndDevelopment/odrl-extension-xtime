# xtime, ODRL extension for OWL Time Ontology, Version 1

Suggested prefix for the 'Time Extension' prefix:

`xtime`

(`time` is reserved for [OWL Time Ontology](https://www.w3.org/TR/owl-time/).)

URI: <https://github.com/nicosResearchAndDevelopment/odrl-extension-xtime/tree/main/v1/>

`xtime`, e**x**tending [OWL Time Ontology](https://www.w3.org/TR/owl-time/).

## Table of Content

- [Prologue](#prologue)
- [Introduction](#introduction)
- [Left Operand](#left-operand)
- [Operator](#operator)
- [Right Operand](#right-operand)
- [TODO](./TODO.md)

*Table of Content "xtime, ODRL extension for OWL Time Ontology"*.

## Prologue

Some initial thoughts about time [here](./prologue.md). 

## Introduction

The **ODRL Profile Context 'xtime, ODRL extension for OWL Time Ontology'** aims to answer most questions related to
time-problems.
Given [OWL Time Ontology](https://www.w3.org/TR/owl-time/) does not know operators, as used in ODRL constraints:
[time:before](https://www.w3.org/TR/owl-time/#time:before) is a property glued to
a [time:TemporalEntity](https://www.w3.org/TR/owl-time/#time:TemporalEntity) and states that given subject is before
another temporal entity.

So `xtime` aims to solve this problem, introducing those thirteen operators, aligned to those [*thirteen elementary
possible relations between time periods*](https://www.w3.org/TR/owl-time/#topology), well-defined by OWL Time Ontology.

```text
                      |     i     |        j
  Before(i, j)        |<.........>|   <--------->    After(j, i)
   Meets(i, j)        |           |<------------>    MetBy(j, i)
Overlaps(i, j)        |       <---|------------->    OverlappedBy(j, i)
  Starts(i, j)        |<----------|------------->    StartedBy(j, i)
  During(i, j)    <---|-----------|------------->    Contains(j, i)
Finishes(i, j)    <---|---------->|                  FinishedBy(j, i)
  Equals(i, j)        |<--------->|                  Equals(j, i)
```

*Thirteen elementary possible relations between time periods*.

Two additional relations, `In` and `Disjoint`, expressed as pseudocode:

```text
      In(i, j) === (Starts(i, j) || During(i, j) || Finishes(i, j))
Disjoint(i, j) === (Before(i, j) || After(i, j))
```

`xtime`also introduces some operators to equip constraints handling duration-related problems,
like `xtime:durationLargerThan`

*Example. Two years are longer than one year leads to 'true'*:

(turtle)

```turtle

@prefix odrl:              <http://www.w3.org/ns/odrl/2/> .
@prefix xsd:               <http://www.w3.org/2001/XMLSchema#> .
@prefix xtime:             <https://github.com/nicosResearchAndDevelopment/odrl-extension-xtime/v1/> .

[
    a odrl:Constraint ;
    odrl:leftOperand  "P2Y"^^xsd:duration ;
    odrl:operator     xtime:durationLargerThan ;
    odrl:rightOperand "P1Y"^^xsd:duration ;
] .
```

(json)

```json
{
  "@type": "odrl:Constraint",
  "odrl:leftOperand": {
    "@type": "xsd:duration",
    "@value": "P2Y"
  },
  "odrl:operator": "xtime:durationLargerThan",
  "odrl:rightOperand": {
    "@type": "xsd:duration",
    "@value": "P1Y"
  }
}
```

Using the namespace (prefix) `xtime` and **NOT** `time` has one important reason: editors of **xtime**
do not want to collide with *suggested prefix for the OWL-Time namespace* **time**!

> TODO: Time as a stand alone ODRL Profile

> At a first glance time seem to be simple to understand, but - it isn't.

---

## Left Operand

All `xtime` Left Operands:

> [dayOfWeek](#dayofweek), [dayOfYear](#dayofyear), [monthOfYear](#monthofyear), [now](#now),


### dayOfWeek

Day of week from current time (now). See [Time Ontology, "Day of week"](https://www.w3.org/TR/owl-time/#time:DayOfWeek).

Data type: `xsd:anyURI`.
Possible results

```
time:Monday
time:Tuesday
time:Wednesday
time:Thursday
time:Friday
time:Saturday
time:Sunday
```

```turtle

@prefix rdf:        <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs:       <http://www.w3.org/2000/01/rdf-schema#> .
@prefix time:       <https://www.w3.org/TR/owl-time/> .
@prefix odrl:       <http://www.w3.org/ns/odrl/2/> .
@prefix xsd:        <http://www.w3.org/2001/XMLSchema#> .
@prefix xtime:      <https://github.com/nicosResearchAndDevelopment/odrl-extension-xtime/v1/> .

<https://www.example.com/constraint/42-42-42-42-42>
    a                 odrl:Constraint ;
    odrl:leftOperand  xtime:dayOfWeek ;
    odrl:operator     odrl:isPartOf ;
    odrl:rightOperand [ rdf:type  xsd:anyURI ;
                        rdf:value "https://www.w3.org/TR/owl-time/Monday", "https://www.w3.org/TR/owl-time/Friday" ; ] ;
    odrl:dataType     xsd:anyURI ;
    rdfs:isDefinedBy  <https://www.example.com/> .
```

### dayOfYear

Day of year from current time (now).

Data type: `xsd:nonNegativeInteger`.

```turtle

@prefix rdf:        <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs:       <http://www.w3.org/2000/01/rdf-schema#> .
@prefix time:       <https://www.w3.org/TR/owl-time/> .
@prefix odrl:       <http://www.w3.org/ns/odrl/2/> .
@prefix xsd:        <http://www.w3.org/2001/XMLSchema#> .
@prefix xtime:      <https://github.com/nicosResearchAndDevelopment/odrl-extension-xtime/v1/> .

<https://www.example.com/constraint/42-42-42-42-44>
    a                 odrl:Constraint ;
    odrl:leftOperand  xtime:dayOfYear ;
    odrl:operator     odrl:gt ;
    odrl:rightOperand "42"^^xsd:nonNegativeInteger ;
    odrl:dataType     xsd:nonNegativeInteger ;
    rdfs:isDefinedBy  <https://www.example.com/> .
```

### monthOfYear

Month of year from current time (now).
See [Time Ontology, "Month of year"](https://www.w3.org/TR/owl-time/#time:MonthOfYear).

See Gregorian-[turtle](https://raw.githubusercontent.com/w3c/sdw/gh-pages/time/rdf/time-gregorian.ttl).

Data type: `xsd:anyURI`.

Possible results

```
greg:January
greg:February
greg:March
greg:April
greg:May
greg:June
greg:July
greg:August
greg:September
greg:October
greg:November
greg:December
```

```turtle

@prefix greg:       <http://www.w3.org/ns/time/gregorian/> .
@prefix rdf:        <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs:       <http://www.w3.org/2000/01/rdf-schema#> .
@prefix time:       <https://www.w3.org/TR/owl-time/> .
@prefix odrl:       <http://www.w3.org/ns/odrl/2/> .
@prefix xsd:        <http://www.w3.org/2001/XMLSchema#> .
@prefix xtime:      <https://github.com/nicosResearchAndDevelopment/odrl-extension-xtime/v1/> .

<https://www.example.com/constraint/42-42-42-42-43>
    a                 odrl:Constraint ;
    odrl:leftOperand  xtime:monthOfYear ;
    odrl:operator     odrl:isPartOf ;
    odrl:rightOperand [ rdf:type  xsd:anyURI ;
                        rdf:value "http://www.w3.org/ns/time/gregorian/April",
                                  "http://www.w3.org/ns/time/gregorian/May" ; ] ;
    odrl:dataType     xsd:anyURI ;
    rdfs:isDefinedBy  <https://www.example.com/> .
```

### now

Current time (now).

Data type: `xtime:temporalEntity`.

```turtle

@prefix rdf:        <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs:       <http://www.w3.org/2000/01/rdf-schema#> .
@prefix time:       <https://www.w3.org/TR/owl-time/> .
@prefix odrl:       <http://www.w3.org/ns/odrl/2/> .
@prefix xsd:        <http://www.w3.org/2001/XMLSchema#> .
@prefix xtime:      <https://github.com/nicosResearchAndDevelopment/odrl-extension-xtime/v1/> .

<https://www.example.com/constraint/42-42-42-42-42>
    a                 odrl:Constraint ;
    odrl:leftOperand  xtime:now ;       ## "2023-06-01T12:00:00Z;P0Y;2024-06-01T12:00:00Z"^^xtime:temporalEntity
    odrl:operator     xtime:before ;
    odrl:rightOperand xtime:tomorrow ;  ## "2023-06-02T00:00:00Z;P1D;2024-06-03T00:00:00Z"^^xtime:temporalEntity
    odrl:dataType     xtime:temporalEntity ;
    rdfs:isDefinedBy  <https://www.example.com/> .
```

---

## Operator

All `xtime` Operators:

> [after](#after), [before](#before), [contains](#contains), [disjoint](#disjoint), [during](#during), [equals](#equals)
> , [finishedBy](#finishedby), [finishes](#finishes), [in](#in), [meets](#meets), [metBy](#metby)
> , [overlappedBy](#overlappedby), [overlaps](#overlaps), [startedBy](#startedby)
> , [starts](#starts)<br>duration<br>[durationEquals](#durationequals), [durationLargerThan](#durationlargerthan)
> , [durationLargerThanEquals](#durationlargerthanequals), [durationShorterThan](#durationshorterthan)
> , [durationShorterThanEquals](#durationshorterthanequals)

### after

### before

### contains

### disjoint

### during

### equals

### finishedBy

### finishes

### in

### meets

### metBy

### overlappedBy

### overlaps

### startedBy

### starts

### durationEquals

### durationLargerThan

### durationLargerThanEquals

### durationShorterThan

### durationShorterThanEquals

## Right Operand

All `xtime` Right Operands:

> [day](#day), [month](#month), [now](#now), [quarterOfYearFirst](#quarterOfYearFirst), [quarterOfYearSecond](#quarterOfYearSecond)
> , [quarterOfYearThird](#quarterOfYearThird), [quarterOfYearFourth](#quarterOfYearFourth), [tomorrow](#tomorrow), [year](#year)

### Day

Current day (from now) as an Interval.

Data type `xtime:temporalEntity`


### Month

Current month (from now) as an Interval.

Data type `xtime:temporalEntity`

```turtle

@prefix rdf:        <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs:       <http://www.w3.org/2000/01/rdf-schema#> .
@prefix time:       <https://www.w3.org/TR/owl-time/> .
@prefix odrl:       <http://www.w3.org/ns/odrl/2/> .
@prefix xsd:        <http://www.w3.org/2001/XMLSchema#> .
@prefix xtime:      <https://github.com/nicosResearchAndDevelopment/odrl-extension-xtime/v1/> .

<https://www.example.com/constraint/43-42-42-42-42>
    a                 odrl:Constraint ;
    odrl:leftOperand  "2049-06-01T12:00:00.42Z;P0Y;2049-06-01T12:00:00.42Z"^^xtime:temporalEntity ;
    ## same as
    odrl:leftOperand  "2049-06-01T12:00:00.42Z;P0Y;"^^xtime:temporalEntity ;
    ## same as
    odrl:leftOperand  "2049-06-01T12:00:00.42Z;;2049-06-01T12:00:00.42Z"^^xtime:temporalEntity ;
    ## same as
    odrl:leftOperand  "2049-06-01T12:00:00.42Z;;"^^xtime:temporalEntity ;
    ## same as
    odrl:leftOperand  "2049-06-01T12:00:00.42Z"^^xtime:temporalEntity ;
    ## same as
    odrl:leftOperand  "2049-06-01T12:00:00.42Z"^^xsd:dateTimeStamp ;
    ## will be also "true"^^xsd:boolean
    odrl:leftOperand  "2049-06-01"^^xsd:date ; ## "2049-06-01T00:00:00Z;P1D;2049-06-02T00:00:00Z"^^xtime:temporalEntity
    odrl:operator     xtime:after ;
    odrl:rightOperand xtime:month ; ## "2023-01-01T00:00:00Z;P1M;2024-02-01T00:00:00Z"^^xtime:temporalEntity
    odrl:dataType     xtime:temporalEntity ;
    rdfs:isDefinedBy  <https://www.example.com/> .
```

### Now

Current time as an Instance.

Data type `xtime:temporalEntity`

### QuarterOfYearFirst

First quarter of year (from now) as an Interval.

Data type `xtime:temporalEntity`

### QuarterOfYearSecond

Second quarter of year (from now) as an Interval.

Data type `xtime:temporalEntity`

### QuarterOfYearThird

Third quarter of year (from now) as an Interval.

Data type `xtime:temporalEntity`

### QuarterOfYearFourth

Forth quarter of year (from now) as an Interval.

Data type `xtime:temporalEntity`

### Tomorrow

Tomorrow, the following day (from now) as an Interval.

Data type `xtime:temporalEntity`

### Year

Current year (from now) as an Interval.

Data type `xtime:temporalEntity`

```turtle

@prefix rdf:        <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs:       <http://www.w3.org/2000/01/rdf-schema#> .
@prefix time:       <https://www.w3.org/TR/owl-time/> .
@prefix odrl:       <http://www.w3.org/ns/odrl/2/> .
@prefix xsd:        <http://www.w3.org/2001/XMLSchema#> .
@prefix xtime:      <https://github.com/nicosResearchAndDevelopment/odrl-extension-xtime/v1/> .

<https://www.example.com/constraint/43-42-42-42-42>
    a                 odrl:Constraint ;
    odrl:leftOperand  "2049-06-01T12:00:00.42Z;P0Y;2049-06-01T12:00:00.42Z"^^xtime:temporalEntity ;
    ## same as
    odrl:leftOperand  "2049-06v01T12:00:00.42Z;P0Y;"^^xtime:temporalEntity ;
    ## same as
    odrl:leftOperand  "2049-06-01T12:00:00.42Z;;2049-06-01T12:00:00.42Z"^^xtime:temporalEntity ;
    ## same as
    odrl:leftOperand  "2049-06-01T12:00:00.42Z;;"^^xtime:temporalEntity ;
    ## same as
    odrl:leftOperand  "2049-06-01T12:00:00.42Z"^^xtime:temporalEntity ;
    ## same as
    odrl:leftOperand  "2049-06-01T12:00:00.42Z"^^xsd:dateTimeStamp ;
    ## will be also "true"^^xsd:boolean
    odrl:leftOperand  "2049-06-01"^^xsd:date ; ## "2049-06-01T00:00:00Z;P1D;2049-06-02T00:00:00Z"^^xtime:temporalEntity
    odrl:operator     xtime:after ;
    odrl:rightOperand xtime:year ; ## "2023-01-01T00:00:00Z;P1Y;2024-01-01T00:00:00Z"^^xtime:temporalEntity
    odrl:dataType     xtime:temporalEntity ;
    rdfs:isDefinedBy  <https://www.example.com/> .
```

---