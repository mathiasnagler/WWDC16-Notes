# 242 - What's New in Core Data

## Query Generation

- Problem: Handling deletions
    - `managedObjectContext.shouldDeleteInaccessibleFaults` (usually what you want)
    - Prefetch everything
    - Write lots of code
- Provide UI with stable data
- All reads from a context see single generation of data
- Deleted objects remain still visible in specific context
- On save merge policy is applied and a new generation is generated
- Generations happen transactionality at context level
- Isolation of work in peer contexts
- Minimize prefetching
- Context chooses behaviour: unpinned (default), pin when data first loaded, pin to specific generation
- Manual refreshing objects on generation updates: `moc.fetch()`, `moc.refreshAllObjects()`
- Works only with SQL store
- `NSQueryGenerationToken`

## Concurrency

- No more PSC locking with multiple contexts (mutliple reader, one writer)
- Locking moved down to SQLite level
- Eleminates setup with 2 PSCs
- Better performance: Shared Row-Cache

## Setting up Core Data

- `NSPersistentStoreDescription`: Encapsulates everything to describe a store (type, url, configuration, options)
- Option for adding stores asynchronosly (useful for migrations)
- `NSPersistentContainer`: Encapsulates `NSObjectModel`, `NSPersistentStoreCoordinator`, `NSManagedObjectContext`
- Lot of boilerplate for stack setup eliminated
- Store locations and naming handled by `NSPersistentContainer`
- Other container features:
    - UI MOC property
    - Method for enqueuing background work `performBackgroundTask`
- MOC `automaticiallyMergeChangesFromParent`: Works for child contexts and toplevel contexts

## Generics

- New protocol `NSFetchRequestResult`
- Properly typed results

## Common Operations

- Entity description is now a class method on the subclass: `Subclass.entity()`
- Factory method for fully typed fetch requests: `Subclass.fetchRequest()`
- Object creation: `Subclass(context: moc)`
- Execute fetch request: `try fetchRequest.execute()` (inside `performBlock()`)

## Code Generation

- Automatic subclass generation
- Configered per entity
- Automatic regeneration
- Options: None, Class or Extension

## SQLite

- Multithreading Assertions: `SQLITE_ENABLE_THREAD_ASSERTIONS=1`
- `SQLITE_ENABLE_LOGGING=1`
- File operation are now safer: Prevents Corrupt Data  (`SQLITE_ENABLE_FILE_ASSERTIONS=1`)
- PSC operations are safe:
    - `replacePersistentStore()`
    - `destroyPersistentStore()`
