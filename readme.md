# ETL FW

## Overview
ETL FW describes considerations, and maybe a loose framework, for implementing data ETLs / pipelines. As every environment is different, this document is not prescriptive nor does it cover every possible condition, constraint, or available option.

For clarification, the abbreviation "ETL" is interpreted as:

a. Extract (E) - Extract (export, download, qurey) data from a source repository, or storage.

b. Transform (T) - Transform (change, manipulate, modify) some or all of data extracted from the source repository, before loading (next) into the destination repository. Transformation is optional.

c. Load (L) - Load (import, upload, insert) the data extracted, and possibly transformed, into a designated desitination repository.
## Aspects
There are several aspects which must be considered, such as:

- Execution Runtime
  - Monolithic program
  - Modular, with some glue
  - Execution host(s)
- Configuration
- Respositories
  - Types
  - Source
  - Destination
- Extract
  - source repository
  - Schedule
  - Failures
  - Duration
  - Threadedness
- Transform
  - Source format
  - Output format
  - Attribute (column) level changes
  - Moment of transform
    - During query (coded into query language)
    - Server side (query-driven trigger, stored procedure)
    - In extract code (client side)
  - Failures
- Load
  - destination repository
  - Schedule
  - Failures
  - Duration
  - Threadedness
- 