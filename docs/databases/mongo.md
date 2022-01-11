# Upsert example

```javascript
{
    "_id": 1,
    "sensor": 5,
    "date": Date("2020-10-10"),
    "valcount": 2,
    "total": 80,
    "readings": [
        {"v": 50, "t": 23},
        {"v": 30, "t": 24}
    ]
}
```

```javascript
db.iot.updateOne(
	{
        "sensor": 5,
        "date": var.date,
        "valcount": { $lt : 48 }
    },
    {
    	"$push": { "readings": {"v": var.v, "t", var.t}},
    	"$inc": {"valcount": 1, "total": var.v}
    },
    { upsert: true}
)
```

# Workload description

- Query (Anomalies in inventory)
- Quantification (X/day Y/sec)
- Qualification (<1s, slate data is fine, critical write)

Details of critical operations

- Description
- Type (R/W)
- Frequency
- Size
- Consistency
- Latency
- Durability
- Life/Duration
- Security

# Schema design patterns

## Computed pattern

Sum all views of all screenings of movie into movie document

## Bucket pattern

Used in IoT

One document per device per day/week

## Extended reference

Copy required fields from one element to the other (example shipping address)

# Change streams

# Indexes

Order fields by equally, sort, range

## Patterns

### Attribute pattern / Polymorphic pattern

Move all diferent attributes but similar and want to search on multiple to a spec array of key-value objects, then create a index on that key-value pair

### Extended reference pattern

Copy required fields from one element to the other (example shipping address)

### Subset pattern

Move some fields or part of that fields (list, keep top x) to other documents

### Computed pattern

Sum all views of all screenings of movie into movie document

### Bucket pattern

One document per device per day/hour with all readings (upser use case)

### Schema version pattern

Add version to documents and modify application with multiple handlers while migrations run in batch on background task

### Tree pattern

- Parent references
  - Ancestors of X is COMPLEX
  - Reports to Y is SIMPLE
  - All nodes under Z is COMPLEX
  - Change all under N to under P is SIMPLE
- Child references
  - Ancestors of X is COMPLEX
  - Reports to Y is COMPLEX
  - All nodes under Z is SIMPLE
  - Change all under N to under P is COMPLEX
- Array of ancestors
  - Ancestors of X is SIMPLE
  - Reports to Y is SIMPLE
  - All nodes under Z is COMPLEX
  - Change all under N to under P is COMPLEX

- Materialized paths
  - Ancestors of X is SIMPLE
  - Reports to Y is COMPLEX
  - All nodes under Z is COMPLEX
  - Change all under N to under P is COMPLEX



Recomended: Array of ancestors + Parent

### Polymorphic pattern

Used in single view cases (join data from different sources). Has a type field.

### Approximation pattern

Does not matter if data is not precise. (page counter, counters with tolerance to imprecisions)

### Outlier pattern

Handle documents in different maner if they are outliers

![https://university-courses.s3.amazonaws.com/M320/patterns-use-cases.png](D:\workspace\notes\patterns-use-cases.png)

## Investigate

https://www.youtube.com/watch?v=bxw1AkH2aM4