# iOS-interview-prep
Hey guys! I have compiled most commonly asked interview questions related to iOS (Objective-c, Swift) based on my personal experience and research so far. 

## Basics & Advance Concepts

**ReusableIdentifier:**
To re-use UITableViewCell and dequeue it instead of recreating, in order to improve performance.

**Atomic:**
Initialized value, thread safe, synchronized, performance costly

**NonAtomic:**
Performance efficient but not recommended for multithreading.

**Synthesize:**
Creates property setter/getter on compile time because they won't be changing.

**Dynamic:**
Creates/change getter on runtime.

**Fast Enumeration:**
It retrieves the element by its instance which is faster than iteration because its internal implementation reduces message passing overhead.

**Posing:**
To replace a class at runtime with a target class. NSObject PosAsClass

**Method Swizzling:**
To replace the implementation of an existing selector at runtime. ViewWillAppear Example

**Frames vs Bounds:**
Frames (x,y) (width,height) w.r.t superview while Bounds (x,y) (width,height) relative to its own coordinates

**NSSet vs NSArray:**
NSSet is faster than NSArray because it uses hash tables to retrieve data.

**Category:**
Enhance functionality of existing class without subclassing. Class+CategoryName

**Extension:**
Should be implemented inside Main @implementation. Private methods, properties within the class can be made readwrite whereas readonly outside

**Protocol:**
Similar to interface in java, any class can implement protocol (required/optional methods) others can send messages to class without even knowing its type.

**Delegate:**
iOS basic design pattern in which one object acts on behalf of other object. it keeps reference to the object

**NSNotificationCenter:**
Publisher Subscriber pattern, similar to broadcaster in java, to avoid coupling.

**Apple Pay:**

- Payment Request Initiated
- PaymentAuthViewController then interact with user e.g taking shipping address etc
- Once done, PR sends to Secure Element (it sends data like merchant, card to create payment token)
- Pass payment token to Apple Servers
- Payment Token is return to app

**APNS:**

- App register for PN
- App receives device token
- Register token on your server
- Server sends push notification request to APNS
- APNS sends notification to your device

**Cocoa:**

- Foundation & AppKit Framework
- Mac App Development

**Cocoa Touch:**

- Foundation & UIKit Framework
- iOS App Development

**Autorelease:**
UIKit use code it creates autorelease pool and add objects which should be autoreleased. once it completed and come back from your code, it drains the pool so memory will be released.

**App States:**

- Not Running
- In Active
- Active
- Background
- Suspended

**KVC:**
Key Value Coding,  get property using string

**KVO:**
Key Value Observing, add observer to a property change

**Blocks:**
Function pointer, language level feature like lambda expression.

**Threading:**
- GCD (Grand Central Dispatch)
- NSOperationQueue

**GCD:**
GCD provides following types of quesues to perform async tasks:
- **Serial Queues**
  - Guaranteed serialized access to a shared resource that avoids race condition.
  - Tasks are executed in a predictable order which means it will execute in same order as they are inserted.
  - You can create any number of serial queues.
- **Concurrent Queues**
  - Executes multiple tasks in parallel
  - Again tasks are started in the order in which they were added to the queue. However, the execution time and finish time vary

**NSOperationQueue:**
GCD is a low-level C API that enables developers to execute tasks concurrently. Operation queues, on the other hand, are high level abstraction of the queue model, and is built on top of GCD. Some common characteristics are below:
- Don’t follow FIFO: in operation queues, you can set an execution priority for operations.
- By default, they operate concurrently: there is still a workaround to execute tasks in operation queues in sequence by using dependencies between operations.
- Operation queues are instances of class NSOperationQueue and its tasks are encapsulated in instances of NSOperation.

**NSOperation:**
Tasks submitted to operation queues are in the form of NSOperation instances.
- NSBlockOperation – Use this class to initiate operation with one or more blocks.
- NSInvocationOperation – Use this class to initiate an operation that consists of invoking a selector on a specified object.

**App Thinning:**
The store and operating system optimize the installation of iOS apps by tailoring app delivery to the capabilities of the user’s particular device, with minimal footprint. This optimization, called app thinning.

- **App Slicing:** Process of creating and delivering variants of the app bundle for different target devices.
- **Bitcode:** It is an intermediate representation of a compiled program. Apps you upload to iTunes Connect that contain bitcode will be compiled and linked on the store. Including bitcode will allow Apple to re-optimize your app binary in the future without the need to submit a new version of your app to the store.
- **On-Demand Resources:** Resources that you can tag with keywords and request in groups, by tag. The store hosts the resources on Apple servers and manages the downloads for you.

**On Application Launch:**
application:didFinishLaunchingWithOptions
App environments, third party lib, and other things are initialized at this stage.
Options contains the information why application was launched; e.g if app is launched directly, options would be empty.

UIApplicationLaunchOptionsURLKey
UIApplicationLaunchOptionsSourceApplicationKey

**Deep Linking:**
###### URL types
- URL identifier - url e.g net.xmen.app
- URL Schemes - Bundle ID

**Async Downloading:**

- In case of async task, UI should not be blocked, and only be update on main thread
- Download images on tableview creation instead of cell

**Frameworks:**

- CoreFoundation
- CoreGraphics
- CoreLocation
- CoreData
- CoreImage
- QuartzCore

**iOS Security:**
Application transport security (iOS 9.0)
Key chain

**Sorting:**

**Compare Method**
```
- (NSComparisonResult)compare:(Person *)otherObject {
    return [self.birthDate compare:otherObject.birthDate];
}

NSArray *sortedArray = [drinkDetails sortedArrayUsingSelector:@selector(compare:)];
```
**Sort Descriptor**
```
NSSortDescriptor *sortDescriptor = [[NSSortDescriptor alloc] initWithKey:@"birthDate" ascending:YES];
NSArray *sortDescriptors = [NSArray arrayWithObject:sortDescriptor];
NSArray *sortedArray = [drinkDetails sortedArrayUsingDescriptors:sortDescriptors];
```

**Blocks**
```
NSArray *sortedArray = [drinkDetails sortedArrayUsingComparator:^NSComparisonResult(id a, id b) {
    NSDate *first = [(Person*)a birthDate];
    NSDate *second = [(Person*)b birthDate];
    return [first compare:second];
}];
```
**Searching:**

**Using Predicate**
```
// For number kind of values:
NSPredicate *predicate = [NSPredicate predicateWithFormat:@"SELF = %@", value];
NSArray *results = [array_to_search filteredArrayUsingPredicate:predicate];

// For string kind of values:
NSPredicate *predicate = [NSPredicate predicateWithFormat:@"SELF contains[cd] %@", value];
NSArray *results = [array_to_search filteredArrayUsingPredicate:predicate];

// For any object kind of value (yes, you can search objects also):
NSPredicate *predicate = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", value];
NSArray *results = [array_to_search filteredArrayUsingPredicate:predicate];
```

**Static vs Dynamic Framework/Library**

**CoreData**

Persistent framework, use ORM, wrapper on SQLite, stores data in sql, xml, json, text format, comes with schema migration tool.

**Managed Object:**
Objects created by applications to store data in core data db used MO. Its direct mapping on table.

**Managed Object Context:**
Managed object models are contained and managed by Managed Object Context. App directly interact with MOC. MOC managed relation between MOM.

**Persistence Store Coordinator:**
Responsible for coordinating access to multiple persistence object stores. Usually application don't directly interact with PSC.

**Data Concurrency:**
Concurrency is the ability to work with the data on more than one queue at the same time. There are two types to achieve this:
- NSMainQueueConcurrencyType
- NSPrivateQueueConcurrencyType.

**CoreData Migration:**

**Light Weight Migration**
Enabling few checks will do the migration automatically.

**Manual Migration**
It involves some work on coding part for mapping data sets etc.

**Custom Manual Migration**
It involves more work on coding part to apply transformation logic. Custom entity transform logic involves subclassing NSEntityMigrationPolicy.

**Fully Manual Migration**
Fully manual migrations are for those times when even specifying custom transformation logic isn’t enough to fully migrate data from one model version to another. E.g. update data across non-sequential versions, such as jumping from version 1 to 4.

###### Always open to suggestions. Enjoy! 👍
