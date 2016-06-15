## 403 - Swift API Design Guidelines

* Clarity at point of use
* Omit needless words (`persons.removeItem(ted)` < `persons.remove(ted)`)
* Clarity is more important than brevity
* Concise code is a consequence of using contextual cues
* Option-Click in Xcode to see inferred type
* Do not remove words that clarify a parameter role, behavior or hierarchy
* Only use overloading when operation works the same
* If first argument is part of prepositional phrase --> label
* If first argument is **not** part of a grammatical phrase --> label
* Otherwise --> no label
* If method has side effects --> name it with a verb
* See (Swift.org API Design Guidelines)[https://swift.org/documentation/api-design-guidelines/]
* One API, two Names (Swift and Objective-C) - different names with `@objc`
* `#keyPath` (like `#selector`)
* `NS_SWIFT_NAME` to expose a Objective-C method to swift with different name
* `NS_EXTENSIBLE_STRING_ENUM` to expose `NSString` constants as static `struct` properties
* `NS_SWIFT_NAME` make `C` code better in swift, for example: `CFStringRef kCGColorWhite NS_SWIFT_NAME(CGColor.white)`
