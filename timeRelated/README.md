# xtime, time related Data Types, Properties and Operands

## Data Types

| Scope     | Data Type         | Comment                    | Example                                                                                                                                                                                                                            |
|-----------|-------------------|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **xsd**   |                   |                            |                                                                                                                                                                                                                                    |
|           | date              | period                     | `"2020-12-20"^^xsd:date`                                                                                                                                                                                                           |
|           | time              |                            |                                                                                                                                                                                                                                    |
|           | dateTime          | instant                    |                                                                                                                                                                                                                                    |
|           | dateTimestamp     | instant; explicit Timezone |                                                                                                                                                                                                                                    |
|           | gDay              |                            | `"---3"^^xsd:gDate`                                                                                                                                                                                                                |
|           | gMonth            |                            | `"--2"^^xsd:gMonth`                                                                                                                                                                                                                |
|           | ...               |                            |                                                                                                                                                                                                                                    |
|           | duration          | not recommended            | `"P0Y"^^xsd:duration`                                                                                                                                                                                                              |
|           | dayTimeDuration   | no year or month portion   | `"P1DT3H2M1S"^^xsd:dayTimeDuration`                                                                                                                                                                                                |
|           | yearMonthDuration |                            | `"P2M"^^xsd:yearMonthDuration; "P1Y2M"^^xsd:yearMonthDuration`                                                                                                                                                                     |
| **xtime** |                   |                            |                                                                                                                                                                                                                                    |
|           | temporalEntity    | instant/period             | instant :: `"2023:10:12T12:00:00Z;P0Y;2023:10:12T12:00:00Z"^^xtime:temporalEntity`, period :: `"2023:10:12T12:00:00Z;P1D;"^^xtime:temporalEntity`, same as :: `"2023:10:12T12:00:00Z;;2023:10:13T12:00:00Z"^^xtime:temporalEntity` |

*Time related Data Types*.

---

## Properties, Data Type

| Scope              | Property                                                                               | Comment                                                                                                                                                     | Example                   |
|--------------------|----------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------|
| **foaf**           |                                                                                        |                                                                                                                                                             |                           |
|                    | birthday                                                                               | ??? :: period, based on now                                                                                                                                 | `"10-12"^^ xsd:gMonthDay` |
| **cred (vp/vc)**   |                                                                                        | Verifiable Presentation and Credential                                                                                                                      |                           |
|                    | issuanceDate                                                                           | instant; `xsd:dateTime`                                                                                                                                     |                           |
|                    | validFrom                                                                              | instant; `xsd:dateTime`                                                                                                                                     |                           |
|                    | validUntil                                                                             | instant; `xsd:dateTime`                                                                                                                                     |                           |
| **dcat**           |                                                                                        |                                                                                                                                                             |                           |
|                    | endDate                                                                                | instant; `rdfs:Literal / xsd:dateTime / xsd:date / xsd gYear`                                                                                               |                           |
|                    | startDate                                                                              | instant; `rdfs:Literal / xsd:dateTime / xsd:date / xsd gYear`                                                                                               |                           |
|                    | temporalResolution                                                                     | duration; `xsd:duration`                                                                                                                                    |                           |
| **prov**           |                                                                                        |                                                                                                                                                             |                           |
|                    | [generatedAtTime](https://www.w3.org/TR/2013/REC-prov-o-20130430/#generatedAtTime)     | instant                                                                                                                                                     |                           |
|                    | [startedAtTime](https://www.w3.org/TR/2013/REC-prov-o-20130430/#startedAtTime)         | instant                                                                                                                                                     |                           |
|                    | [endedAtTime](https://www.w3.org/TR/2013/REC-prov-o-20130430/#endedAtTime)             | instant                                                                                                                                                     |                           |
|                    | [atTime](https://www.w3.org/TR/2013/REC-prov-o-20130430/#endedAtTime)                  | instant                                                                                                                                                     |                           |
|                    | [invalidatedAtTime](https://www.w3.org/TR/2013/REC-prov-o-20130430/#invalidatedAtTime) | instant                                                                                                                                                     |                           |
| **< < Higher > >** |                                                                                        |                                                                                                                                                             |                           |
| **eIDAS**          |                                                                                        |                                                                                                                                                             |                           |
|                    | dateOfBirth                                                                            | period; [Verifiable ID - natural Person](https://ec.europa.eu/digital-building-blocks/wikis/display/EBSIDOC/Verifiable+ID+-+Natural+Person), dataType::date | `"2023:10:12"^^xsd:date`  |

*Time related Properties (Data Type)*.

---

## Properties, Object Type

| Scope              | Property     | Comment                                                                                                                           | Example                  |
|--------------------|--------------|-----------------------------------------------------------------------------------------------------------------------------------|--------------------------|
| **org**            |              | Organization Ontology                                                                                                             |                          |
|                    | memberDuring | period; `owlTime:Interval`; from source: "This now an informative, not a normative, range constraint", `rdfs:range  owlTime:Interval` |                          |

*Time related Properties (Object Type)*.

---

## Left Operands

| Scope     | Operand     | Comment                                      | Example |
|-----------|-------------|----------------------------------------------|---------|
| **odrl**  |             |                                              |         |
|           | dateTime    |                                              |         |
| **xtime** |             |                                              |         |
|           | now         | instant; set at runtime once!                |         |
|           | hour        | period (from now)                            |         |
|           | minute      | period (from now)                            |         |
|           | second      | period (from now)                            |         |
|           | day         | period (from now)                            |         |
|           | week        | period (from now)                            |         |
|           | month       | period (from now)                            |         |
|           | year        | period (from now)                            |         |
|           | dayOfWeek   | {time:Monday .. time:Sunday}, (from now)     |         |
|           | dayOfYear   | {xsd:NonNegativeInteger}, (from now)         |         |
|           | weekOfYear  | {xsd:NonNegativeInteger}, (from now)         |         |
|           | monthOfYear | {greg:January .. greg:December}, (from now)  |         |

*Time related Left Operands*.

---

## Operators

| Scope     | Operator                  | Comment | Example |
|-----------|---------------------------|---------|---------|
| **odrl**  | eq                        |         |         |
| **xtime** | *alpha sorted*            |         |         |
|           | after                     |         |         |
|           | before                    |         |         |
|           | contains                  |         |         |
|           | disjoint                  |         |         |
|           | durationEquals            |         |         |
|           | durationLargerThan        |         |         |
|           | durationLargerThanEquals  |         |         |
|           | durationShorterThan       |         |         |
|           | durationShorterThanEquals |         |         |
|           | during                    |         |         |
|           | equals                    |         |         |
|           | finishedBy                |         |         |
|           | finishes                  |         |         |
|           | in                        |         |         |
|           | meets                     |         |         |
|           | metBy                     |         |         |
|           | overlappedBy              |         |         |
|           | overlaps                  |         |         |
|           | startedBy                 |         |         |
|           | starts                    |         |         |

*Time related Operators*.

---

## Ontology

### prov

## Higher

### eIDAS

---