# 242 - What's new in Core Data

## Query Generations

* Provide stable view of data to UI
* Handle changes deterministically
* Get rid of `CoreData could not fullfill a fault for ...` errors
* All reads from a context see a single generation of data
* Advance at predictable times
* Full Transactionality at context level
* Isolation of work in peer contexts
* Context chooses it's behavior
  * Unpinned (old behavior, default)
  * Pin when data is first loaded
  * Pin to specific generation
  * Nested contexts inherit data from parent
* Changing Generations
  * Explicit by setting generation token
  * On save
  * during `managedObjectContext.mergeChanges()`
  * As a result of `managedObjectContext.reset()`
  * Registered objects **are not** refreshed on generation update --> `managedObjectContext.refreshAllObjects()`
* Opaque token to track generation (`NSQueryGenerationToken.current()`)
* Generations will not include stores added after token creation
* Does not prevent from removing stores from coordinator

---
## Concurrency

* Use `perform()` and `performAndWait` as in older versions
* `-performBlockAndWait:` now has autorelease pool
* SQL store can now handle multiple concurrent requests
  * Multiple readers
  * Single writer
* More responsive UI
  * Fetch while background work is happening
* Simpler architecture
  * Less need for multiple stacks
  * fewer complicated handoffs
  * Shared row cache means lower memory footprint
* Enabled by default
* All stores must be SQL Stores
* `NSPersistentStoreConnectionPoolMaxSizeKey` to configure maximum pool size
* Should be transparent
* Should simplify code

---
## Stack Configuration

* `NSPersistensStoreDescription` encapsulates
  * `type`
  * `configuration`
  * `url`
  * `options`
  * and provides convenience methods
* `addPersistensStore` can be async (`shouldAddStoreAsynchronously`) and gets a completion handler
* `NSPersistentContainer` enpasulates
  * `NSManagedObjectModel`
  * `NSPersistentStoreCoordinator`
  * `NSManagedObjectContext`
* Reduced boilerplate code necessary

**Defaults when using NSPersistentContainer**
* Model looked up by container name
* Store filename determined by container name
* Store directory provided by the container class
* Main queue context property for UI
* Private queue context factory method
* Method for enqueuing background work (`performBackgroundTask`)


---
## New API

* `NSManagedObjectContext` now has `automaticallyMergesChangesFromParent` (merging parent changes to child)
  * Works great with Quey Generations
* `NSFetchedResultsController` now available on macOS
* `NSEntityDescription` now class method on `NSManagedObject` subclass (`.entity()`)
* Class method for fully typed fetch request (`NSManagedObjectSubclass.fetchRequest()`)
* `NSManagedObject` has new initializer for creating new objects (`Subclass(context: managedObjectContext)`)

---
## Swift

* `NSFetchRequestResult` adopted by
  * `NSMangedObject` and subclasses
  * `NSManagedObjectID`
  * `NSDictionary`
  * `NSNumber`
* `NSFetchRequest` now uses generics: `NSFetchRequest<ResultType>`
  * This also affects `fetch` method and `NSFetchResultsController`
* `NSFetchedResultsController` works great in conjunction with `UICollectionViewDataSourcePrefetching`

---
## Xcode Integration

* Xcode 8 can now generate `NSManagedObject` subclasses
  * Configured per entity
  * Stored in DerivedData, so project will not be polluted
  * Automatically regenerated
  * Model is always up to date
  * Can also create a category or extension, so class can be implemented manually (has to be named `Subclass.h`)
  * Works out of the box in Swift
  * In Objective-C import `MyApp+CoreDataModel.h`
  * Xcode creates `Subclass+CoreDataClass.h` and `Subclass+CoreDataProperties.h`
