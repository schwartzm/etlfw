# ETL FW

## Overview
This document, ETL FW ("ETL Framework"), presents design considerations for ETL implementation. This can be used as a checklist, preliminary outline, or starting point for an ETL design. This design outline may present more than is necessary for a specific ETL implementation. Unused sections should be marked N/A, rather than be deleted.E, T, and L all execute in same local network.

## What This is Not
This document is not a prescription for creating an ETL, nor does it recommend any specific technology for ETL implementation.

## Terms
Terms, as used in this document, that might need some disambiguation or clarification.

**Extract (E in "ETL")** - Extract (i.e., export, download, query) data from a source repository (e.g., RDBMS), with the intent of loading the data into a destination repository.

**Transform (T in "ETL")** - Transform (i.e., change, manipulate, convert) all, or a subset, of the data extracted from the source repository, before loading data into the destination repository. Transformation may only be necessitated by business, analytics, or destination repository requirements.

**Load (L in "ETL")** - Load (i.e., import, upload, insert) the extracted, and possibly transformed, data into a desitination repository.

**Repository** - A medium that stores data to be extracted or loaded. Extract from a "source" repository. Load into a "destination" repository. E.g., relational database, document database, key-value database, flat file. A.k.a., "repo".

## Outline
Outline of aspects to be considered when designing an ETL.

- ETL Execution
  - E, T, and L Logic: Where is Each?
  - Monolithic Structure
    - E, T, & L in a Single Script or Binary
  - Component / Modular Structure
    - Extract Module
    - Transform Module
    - Load Module
    - Glue the E, T, & L together
    - Schedule each phase
  - Execution Platform
- Security
  - Repository access protocol and security
  - Repository authentication
  - Repository bind credentials storage
  - Network over which data is transferred
  - Cached Extracted Data (temporary, working storage)
    - Any of delete, shred, wipe, secure-delete, after run
  - Execution identity
  - ETL Program Files Ownership
- Source Repository
  - Type (e.g., RDBMS, Wide-Column NoSQL, CSV)
  - Access Protocol
  - ...
- Destination Repository
  - Type (e.g., RDBMS, Wide-Column NoSQL, CSV)
  - Access Protocol
  - ...
- Transfer From Source to Destination Repos
  - How the extracted data actually gets to the destination
  - Data traverses untrusted network (scp, sFTP, mTLS, key pairs, h/w encrypter)
  - Data remains in same local network, different hosts, all firewalled (scp, NFS)
  - Data all on same host until load (share common dir with strict ACLs)
- Configuration
  - Source Repo Connection Config
  - Destination Repo Connection Config
  - Source Repo Bind Credentials
  - Destination Repo Bind Credentials
  - Source Repo Query (Extract)
  - Destination Repo Query (Insert)
  - Extract data file naming (if files are in solution)
- Extract Phase
  - Source Repository
  - Schedule
  - Failure and Error Handling
  - Duration
    - Constant over time
    - Grow over time
  - Single or Multi-threaded
      - E.g., If extracting records from tables, each extract can run in parallel
  - Recall end of last ETL run; where to start next query (Sort of like Paging)
    - Store an extract record somewhere (e.g., last fetched primary key)
- Transform Phase
  - Transform Rules (what to transform, when, and how)
  - Source format
  - Output format
  - Attribute (column) level changes
  - Moment of transform
    - During query (coded into query language)
    - Server side (query-driven trigger, stored procedure)
    - In extract code (client side)
  - Failures
- Load Phase
  - Destination Repository
  - Schedule
  - Failure and Error Handling
  - Duration
    - Constant over time
    - Grow over time  
  - Single or Multi-threaded