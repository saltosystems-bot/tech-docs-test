---
title: "Mermaid example"
---

In general terms, CDC-based data integration consists of the following steps:

1. Capture changed data.
2. Transform changed data into a format your destination supports.
3. Upload the data to the destination target.

```mermaid
graph TB
  subgraph Destination
    MQ[Messaging Queue]
    FTI[Full text index]
    AE[Analytics engine]
    ...
  end

  subgraph Source
    subgraph Watched Rows
      Table1
      Table2 
      TableN
    end
    CD[Captured Data]
    Table1 --> CD
    Table2 --> CD
    TableN --> CD
    CD -- Subscriber 1 --> MQ
    CD -- Subscriber 2 --> FTI
    CD -- Subscriber 3 --> AE
    CD -- Subscriber N --> ...
  end
```
> Figure 1: We are watching for changes on N tables. 
> Those table changes are being captured and then sent to multiple destination targets.
