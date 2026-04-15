# Afmilk data model

## Overview
This section describes the model for the Afimilk data collected by NU Farms. It is in two sections. Firstly, the generalised schema defining the model are presented in a tabular format that will be more readable to researchers and data processors. Then, links to appropriate schema definition structures (e.g. JSON) that can be used in programmatic validation of data are given.

## Data model
This data model uses the [CSVW](https://csvw.org/) standard. All keywords (e.g. data types, URLs etc) are in accordance with this standard; which also adheres to the JSON schema keywords standard.

### Notes
- Dates and times generally do not comform to ISO8601 format and require a custom datatype to interpret the field

### Collar Hourly Data <a name="collar-hourly-data"></a>
Sheet name: "Collar hourly data"

| Name | Type | Units |
| --- | --- | --- |
| AnimalId | integer | n/a |
| Date | custom datatype | n/a |
| Hour | integer | h |
| RuminationTimeInSeconds | integer | s |
| EatingTimeInSeconds | integer | s |
| PantingTimeInSeconds | integer | s |

### Daily Data Milk Weight Collar <a name="daily-data-milk-weight-collar"></a>
Sheet name: "Daily data_milk weight collar"

| Name | Type | Units |
| --- | --- | --- |
| Animal_Id | integer | n/a |
| Group_Id | integer | n/a |
| Date | custom datatype | n/a |
| Days_in_Milk | integer | d |
| Age_Days | integer | d |
| Lactation_Num | integer | |
| Yield(gr) | integer | g |
| Conductivity | number | [??] |
| Weight(gr) | integer | g |
| HeatIndicator | integer | [??]
| RuminationTime(seconds) | integer | s |
| EatingTime(seconds) | integer | s |
| Panting(seconds) | integer | s |

### Milk By Session <a name="milk-by-session"></a>
Sheet name: "Milk by session"

| Name | Type | Units |
| --- | --- | --- |
| AnimalId | integer | n/a |
| Date | custom datatype | n/a |
| Session | integer | n/a |
| LatestIdentificationTime | custom datatype | n/a |
| HerdManagerMilkingGroup | integer | n/a |
| Yield(gr) | integer | g |
| Conductivity | number | [??] |
| AMT(seconds) | integer | s |
| ProductionRate(gr/hour) | integer | g/h |

#### Categorical Data

| Category | Value | Description |
| --- | --- | --- |
| Session | 0 | Morning milking |
| Session | 1 | Noon milking |
| Session | 2 | Evening milking |

### Body Weight By Session <a name="body-weight-by-session"></a>
Sheet name: "Body weight by session"

| Name | Type | Units |
| --- | --- | --- |
| AnimalId | integer | n/a |
| Date | custom datatype | n/a |
| Session | integer | n/a |
| Weight(gr) | integer | g |

#### Categorical Data

| Category | Value | Description |
| --- | --- | --- |
| Session | 0 | Morning milking |
| Session | 1 | Noon milking |
| Session | 2 | Evening milking |

### Leg Tag Hourly Activity & Steps <a name="leg-tag-hourly-activity-and-steps"></a>

Sheet name: "LegTag hourly activity & steps"
| Name | Type | Units |
| --- | --- | --- |
| Time | custom datatype | n/a |
| Date | custom datatype | n/a |
| AnimalId | integer | n/a |
| Tag | integer | n/a |
| Step(#) | integer | n/a |
| Activity(steps/hour) | integer | h^(-1) |

### Leg Tag Hourly Rest Data <a name="leg-tag-hourly-rest-data"></a>

Sheet name: "Leg tag hourly rest data"
| Name | Type | Units |
| --- | --- | --- |
| AnimalId | integer | n/a |
| Hour | integer | h |
| Date | custom datatype | n/a |
| RestTime(minutes) | integer | m |
| RestBout(#) | integer | n/a |

### Leg Tag Daily Data <a name="leg-tag-daily-data"></a>

Sheet name: "Leg tag daily data"
| Name | Type | Units |
| --- | --- | --- |
| Animal_Id | integer | n/a |
| Group_Id | integer | n/a |
| Date | custom datatype | n/a |
| Days_in_Milk | integer | d |
| Age_Days | integer | d |
| Lactation_Num | integer | |
| Activity(steps/hour) | integer | h^(-1)
| RestTime(minutes) | integer | m |
| RestBout(#) | integer | n/a |

### Collar 90 Seconds Data 1 Week <a name="collar-90-seconds-data-1-week"></a>

Sheet name: "Collar 90 seconds data 1 week"
| Name | Type | Units |
| --- | --- | --- |
| AnimalId | integer | n/a |
| datetime | custom datatype | n/a |
| Ingestion | integer | n/a |

#### Categorical Data

| Category | Value | Description |
| --- | --- | --- |
| Ingestion | 0 | Other |
| Ingestion | 1 | Rumination |
| Ingestion | 2 | Eating |
| Ingestion | 3 | Panting |
