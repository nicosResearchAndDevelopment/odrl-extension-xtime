# xtime, ODRL extension for OWL Time Ontology, Version 1

Suggested prefix for the 'Time Extension* namespace: `xtime`. (`time` is reserved for [OWL Time Ontology](https://www.w3.org/TR/owl-time/).)

`xtime`, e**x**tending [OWL Time Ontology](https://www.w3.org/TR/owl-time/).

## Table of Content

- [Introduction](#introduction)
- [Left Operand](#left-operand)
- [Operator](#operator)
- [Right Operand](#right-operand)
- [TODO](./TODO.md)

*Table of Content "xtime, ODRL extension for OWL Time Ontology"*.

## Introduction

The **ODRL Profile Context 'xtime, ODRL extension for OWL Time Ontology'** aims to answer most questions related to time-problems.
Given **OWL Time Ontology** does not know operators, as used in ODRL constraints:
[time:before](https://www.w3.org/TR/owl-time/#time:before) is a property glued to a [time:TemporalEntity](https://www.w3.org/TR/owl-time/#time:TemporalEntity) and states that given subject is before another temporal entity.

So `xtime` aims to solve this problem, introducing those thirteen operators, aligned to those [*thirteen elementary
possible relations between time periods*](https://www.w3.org/TR/owl-time/#topology), well-defined by OWL Time Ontology.

`xtime`also introduces some operators to equip constraints handling duration-related problems, like `xtime:durationLargerThan`

*Example: two years are longer than one year leads to 'true'*.

turtle:

```turtle
[
    a odrl:Constraint ;
    odrl:leftOperand  "P2Y"^^xsd:duration ;
    odrl:operator     xtime:durationLargerThan ;
    odrl:rightOperand "P1Y"^^xsd:duration ;
]
```

json:

```json
{
    @type: "odrl:Constraint",
    "odrl:leftOperand":  { @type: "xsd:duration", @value: "P2Y" },
    "odrl:operator":     "xtime:durationLargerThan",
    "odrl:rightOperand": { @type: "xsd:duration", @value: "P1Y" } ;
}
```

Using the namespace (prefix) `xtime` and **NOT** `time` has one important reason: editors of **xtime**
do not want to collide with *suggested prefix for the OWL-Time namespace* **time**!

> TODO: Time as a stand alone ODRL Profile

> At a first glance time seem to be simple to understand, but - it isn't.

---

## Left Operand

[Here](./leftOperand/README.md).

---

## Operator

[Here](./operator/README.md).

---

## Right Operand

[Here](./rightOperand/README.md).

---