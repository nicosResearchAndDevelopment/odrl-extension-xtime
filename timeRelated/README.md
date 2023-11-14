# xtime, time related Data Types, Properties and Operands

## Data Types

| Scope     | Data Type      | Comment        | Example                                         |
|-----------|----------------|----------------|-------------------------------------------------|
| **xsd**   | dateTime       | instant        |                                                 |
|           | dateTimestamp  | instant        |                                                 |
| **xtime** | temporalEntity | instant/period | "2023:10:12T12:00:00Z;P0Y;2023:10:12T12:00:00Z" |

*Time related Data Types*.

---

## Properties

| Scope     | Property                                                                                 | Comment                                                                                                                                                     | Example      |
|-----------|------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| **prov**  |                                                                                          |                                                                                                                                                             |              |
|           | [generatedAtTime ](https://www.w3.org/TR/2013/REC-prov-o-20130430/#generatedAtTime)      | instant                                                                                                                                                     |              |
|           | [startedAtTime](https://www.w3.org/TR/2013/REC-prov-o-20130430/#startedAtTime)           | instant                                                                                                                                                     |              |
|           | [endedAtTime](https://www.w3.org/TR/2013/REC-prov-o-20130430/#endedAtTime)               | instant                                                                                                                                                     |              |
|           | [atTime](https://www.w3.org/TR/2013/REC-prov-o-20130430/#endedAtTime)                    | instant                                                                                                                                                     |              |
|           | [invalidatedAtTime ](https://www.w3.org/TR/2013/REC-prov-o-20130430/#invalidatedAtTime)  | instant                                                                                                                                                     |              |
| **eIDAS** | dateOfBirth                                                                              | period; [Verifiable ID - natural Person](https://ec.europa.eu/digital-building-blocks/wikis/display/EBSIDOC/Verifiable+ID+-+Natural+Person), dataType::date | "2023:10:12" |

*Time related Properties*.

---

## Operands

| Scope | Operand  | Comment      | Example  |
|-------|----------|--------------|----------|
| **odrl**  | dateTime | Left Operand |          |

*Time related Operands*.

---

## Operators

| Scope      | Operator | Comment | Example |
|------------|----------|---------|---------|
| **odrl**   | eq       |         |         |

*Time related Operators*.

---