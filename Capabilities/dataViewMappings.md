#dataViewMappings

A DataViewMapping describes how the data roles relate to each other and allows you to specify conditional requirements for the them.

Each valid mapping will produce a DataView, but currently we only support performing one query per visual so in most situations you will only get one DataView. However, you can provide multiple data mappings with different conditions which allow

```json
[
    {
        "conditions": [ ... ],
        "requiredProperties": [ ... ],
        "single": { ... },
        "categorical": { ... },
        "table": { ... },
        "matrix": { ... }
    }
]
```

###Conditions

Describes conditions for a particular data mapping. You can provide multiple sets of conditions and if the data matches one of the described sets of conditions the visual will accept the data as valid.

Currently, for each field you can specify a min and max value. This represents the number of fields that can be bound to that data role. Note: if a data role is ommitted in the condition it can have any number of fields.

**Example 1**

By default, you can drag multiple fields into each data role. In this example we limited category to 1 and y to 2.

```json
[
    { "category": { "max": 1 }, "y": { "max": 2 } },
]
```

**Example 2**

In this example, there can be at most 2 y values, but not until there is at least 1 category assigned (min: 1).

```json
[
    { "category": { "min": 1, "max": 1 }, "y": { "max": 2 } },
]
```

###Required Properties

```typescript
//todo
```

###Single Data Mapping

Single data mapping is the simplest form of data mapping. It accepts a single measure field and gives you the total. If the field is numeric it will give you the sum. Otherwise it will give you a count of unique values.

To use single data mapping you simply define the name of the data role you want to map. This will only work with a single measure field. If a second field is assigned no data view will be generated so it is also good practice to include a condition that limits the data to a single field.

Note: This data mapping cannot be used in conjunction with any other data mapping. It is meant to reduce data into a single numeric value.

**Example**

```json
{
    "conditions": [
        { "Y": { "max": 1 } }
    ],
    "single": {
        "role": "Y"
    }
}  
```

The resulting data view will still contain the other types (table, categorical, etc), but each mapping will only contain the single value. Best practice is to just access the value inside of single.

![](../images/DataViewMappingResultSingle.png)

###Categorical Data Mapping

Categorical is the most commonly used data mapping.

```json
{
    "categorical": {
        "categories": {
            "for": {
                "in": "category"
            }
        },
        "values": {
            "select": [
                {
                    "bind": {
                        "to": "measure"
                    }
                }
            ]
        }
    }
}

```

###Table Data Mapping

```typescript
//TODO
```

###Matrix Data Mapping

```typescript
//TODO
```
