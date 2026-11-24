# ABL Business Entity Architecture Pattern

Condensed from the ProjectGengar Step-16 architecture guide.

## Layers

1. UI windows present data and call business entity methods with datasets; the target architecture keeps database access out of UI code.
2. Business entities inherit from `OpenEdge.BusinessLogic.BusinessEntity` and encapsulate data access, validation, and business rules.
3. Database tables are attached to entities through data sources.

The Step-16 customer window demonstrates this separation. The original item window still accesses the database directly and remains a workshop refactoring exercise.

## Components

- [EntityFactory](../src/business/EntityFactory.cls) is a singleton with lazy creation of the customer entity. `ResetInstances()` deletes its cached entity and clears the reference.
- [CustomerDataset.i](../src/business/CustomerDataset.i) defines `ttCustomer` and `dsCustomer`. Its before-table supports change tracking, and its unique primary index uses `CustNum`.
- [CustomerEntity](../src/business/CustomerEntity.cls) passes the dataset handle to its superclass constructor, assigns data-source handles to `ProDataSource`, and provides a matching `SkipList` entry for each source.

## Data operations

- Reads build a filter, call the inherited `ReadData()`, check the resulting temp-table, and return a logical result plus an `OUTPUT DATASET`. In this pattern the output dataset is copied back to the caller; do not substitute `BY-REFERENCE` on output read calls.
- Creates, updates, and deletes use `INPUT-OUTPUT DATASET` parameters and pass datasets by reference to the inherited `CreateData()`, `UpdateData()`, and `DeleteData()` methods.
- To update: fetch the record, enable `TRACKING-CHANGES`, modify the temp-table, validate it, and call the entity update method.
- Customer validation rejects an empty customer name and returns an error message for the UI to display.

## Development guidance

Reuse dataset includes between callers and entities, keep business rules in entities, and use explicitly named buffers for database table access in new code. Preserve dataset parameter directions and change tracking when extending the examples. The copied Step-16 source is intentionally retained rather than retroactively refactored.

See the [README](../README.md) for database setup and the [schema summary](../dump/sports2000-schema.txt) for the included schema scope.
