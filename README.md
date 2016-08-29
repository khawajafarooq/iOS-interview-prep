# iOS-interview-prep
Hey guys! I have compiled most commonly asked interview questions related to iOS (Objective-c) based on my personal experience and research so far. 

## Basics & Advance Concepts

**Atomic:**
Its a default attribute of property. It always returns an initialized value. Atomic is thread safe (synchronized) but comes with performance cost.

**NonAtomic:**
Its not thread safe so using nonatomic on multithreading can corrupt data. Unlike atomic property its actually performance efficient.

**Synthesize:**
This keyword creates property (setter or getter) on compile time because it cannot be changed at runtime.

**Dynamic:**
It creates or change getter on runtime.

**Default attribute of a property:**
atomic, readwrite, assign

**strong vs weak:**

**strong** is used with ARC which implies that you don’t need to worry about the retain count of an object. By using strong you own the object. ARC automatically releases it for you when you are done with it.

**weak** ownership means that you don’t own the object instead you keep track of the object till the object was strongly referenced. As soon as the second object is released it loses is value.
E.g. obj.x = ObjB
obj has x as weak property, then its value will only be valid till ObjB remains in memory.

**retain vs assign:**
**retain** is used when you want to own an object (similar to strong in ARC). In MRC, retained object must be released manually inside dealloc.

**assign** will simply assign the value to the attribute. As of its basic purpose purpose, it should be used for non-pointer attributes.

**ReusableIdentifier:**
reusableIdentifier is used to reuse UITableViewCell and dequeue it instead of recreating it. So when you have large number of rows, this practice is used in order to improve tableview performance.

**Fast Enumeration:**
Fast enumeration is faster because it retrieves the element by its instance which is faster than iteration. This way the its internal implementation reduces message passing overhead.

**Frames vs Bounds:**
**Frames** coordinates are calculated w.r.t superview whereas **Bounds** coordinates relative to its own coordinate system.

**NSSet vs NSArray:**
NSSet is faster than NSArray because it uses hash tables to retrieve data.

**Category:**
It is used to enhance functionality of an existing class without subclassing it. Class+CategoryName

**Extension:**
Extension should be implemented inside Main @implementation. Private methods, properties within the class can be made readwrite whereas readonly outside

**Protocol:**
Similar to interface in java, any class can implement protocol (required/optional methods) others can send messages to class without even knowing its type.

**Delegate:**
iOS basic design pattern in which one object acts on behalf of other object. it keeps reference to the object. Its a one-to-one message passing pattern.

**NSNotificationCenter:**
Publisher/Subscriber pattern, similar to broadcaster in java, to avoid coupling. It is many-to-many message passing pattern.

**Posing:**
To replace a class at runtime with a target class. NSObject PosAsClass

**Method Swizzling:**
To replace the implementation of an existing selector at runtime. ViewWillAppear Example

**Autorelease:**
UIKit use code, it creates autorelease pool and add objects which should be autoreleased. once it completed and come back from your code, it drains the pool so memory will be released.

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

**Which method is invoked on application first launch?**
application:didFinishLaunchingWithOptions
App environments, third party lib, and other things are initialized at this stage.
Options contains the information why application was launched; e.g if app is launched directly, options would be empty.
- UIApplicationLaunchOptionsURLKey
- UIApplicationLaunchOptionsSourceApplicationKey

**Deep Linking:**
Opening any application using browser link or through another application is called deep linking. It can be achieved through defining following properties inside .plist file
###### URL types
- URL identifier - url e.g net.xmen.app
- URL Schemes - Bundle ID

**What is the best practice for async task?**

- In case of async task, UI should not be blocked, and only be update on main thread
- Download images on tableview creation instead of cell

**iOS Security Features:**
- Application transport security (iOS 9.0)
- Key chain

**Frameworks to look at:**

- CoreFoundation
- CoreGraphics
- CoreLocation
- CoreData
- CoreImage
- QuartzCore

**Sorting Techniques:**

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
**Searching Technique(s):**

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

**Framework vs Static Library:**
- The biggest advantage a framework has over static libraries is that they act as a neat way of packaging up the compiled library binary and any related headers. They can be dropped into your project (just like the SDK's built-in frameworks like Foundation and UIKit) and they should just work (most of the time).
- Static libraries are fine, but they require a bit of extra work on the part of the user. You need to link your project to the library and you need to copy the header files into your project or reference them somewhere by setting the appropriate header search paths in your build settings.

**Static vs Dynamic Framework/Library:**
- Library When dynamic libraries are linked, none of the library's code is included directly into the linked target. Instead, the libraries are loaded into memory at runtime prior to having symbols getting resolved.
- Frameworks are similar to dynamic libraries. Both are dynamically linkable libraries, except a dynamic framework is a dynamic library embedded in a bundle. This allows for versioning of a dynamic library and sorting additional assets that are used by the library's code.
- Unlike dynamic, linking static libraries includes the object file code from the library into the target's binary. This results in a larger size on disk and slower launch times. Because the library's code is added directly to the linked target's binary, it means that to update any code in the library, the linked target would also have to be rebuilt.
- A static library is a container for a set of object files. Static libraries use the file extension ".a", which comes from the (ar)chive file3 type. An archive file was designed to contain a collection of files. This is ideal for the transport and use of many object files that comprise a single code library. However the linker can only use object files of a single architecture, so there are two different container formats for static libraries based on if they support single or multiple architectures.
- A static **framework** is a bundle containing a static library file. These frameworks are just a convenient way to publish a static library that uses external assets; such as images, fonts, or language files. In addition, static frameworks behave exactly like static libraries. They are statically linked into the executable binary, not loaded at runtime.

**How to use multithreading on single core processor?**
Multi-threading is useful in a single core. If one thread in an application gets blocked waiting for something (say data from the network card or waiting for the disk to write data), the CPU can switch to another thread to keep working.

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

## Some coding challenges
**Problem-1: Find the elements from the three array which existing in atleast 2 arrays**
```
-(NSArray *)findCommonElements:(NSArray*)array1
                        array2:(NSArray*)array2
                        array3:(NSArray*)array3
{
    
    array1 = [array1 sortedArrayUsingSelector: @selector(compare:)];
    array2 = [array2 sortedArrayUsingSelector: @selector(compare:)];
    array3 = [array3 sortedArrayUsingSelector: @selector(compare:)];
    
    int size1 = (int)[array1 count];
    int size2 = (int)[array2 count];
    int size3 = (int)[array3 count];
    int i = 0;
    int j = 0;
    int k = 0;
    
    NSMutableArray *resultArray = [NSMutableArray array];
    
    while (i < size1 && j < size2 && k < size3) {
        
        int x = (int)[[array1 objectAtIndex:i] integerValue];
        int y = (int)[[array2 objectAtIndex:j] integerValue];
        int z = (int)[[array3 objectAtIndex:k] integerValue];
        
        if (x == y || y == z) {
            [resultArray addObject:[array1 objectAtIndex:i]];
            i++;j++;k++;
        }
        else if (x < y) {
            i++;
        }
        else if (y < z) {
            j++;
        }
        else {
            k++;
        }
    }

    return resultArray;
}

//calling method
NSArray *a = @[@1,@3,@4,@5];
NSArray *b = @[@-1,@3,@0,@9];
NSArray *c = @[@0,@31,@32,@22,@6];
NSArray *result = [self findCommonElements:a array2:b array3:c];

// result will contain (1, 3)
```

**Problem-2: For a given interface test.h file:**
```
@interface TestClass: NSObject

@property (atomic, readonly) NSArray *array;

- (void)addObject:(NSString*)object;

@end

// Following is the invokation of class
TestClass *obj= [[TestClass alloc] init];
[obj addObject:@"North America"];
[obj addObject:@"Asia"];
[obj addObject:@"Africa"];

/* Now obj.array will have three objects
  1. North America
  2. Asia
  3. Africa
*/
```

**write the implemention test.m**
```
@implementation TestClass

- (void)addObject:(NSString*)object {
    if(_array == nil) {
        _array = [[NSArray alloc] initWithObjects:object, nil];
    }
    else {
        NSMutableArray *mutableArray = [_array mutableCopy];
        [mutableArray addObject:object];
        _array = [mutableArray copy];
    }
}

@end
```
**Problem-3: In a view controller in a storyboard I have a simple view which has a subview image with tag 0 and a subview label with tag 1. I'm trying to get the image like this:**
```
UIImageView *myImage = (UIImageView*)[myView viewWithTag:0];
myImage.highlighted = YES;
// following exception occurs
-[UIView setHighlighted:]: unrecognized selector sent to instance
```
**It is clearly a UIImageView in the storyboard. Why would this cast not work?**
###### All views have a 0 tag as a default so if you get a 0 view it could be any view. For it to work you need to use non-zero values that you set in your program or within Interface builder.

**Problem-4: What is the output of following program?**
```
NSString * a = @“Bob”;
NSString * b = @“Bob”;
if (a == b) 
{  NSLog (@“Equal”); }
else 
{ NSLog (@“Not equal”; }
```
###### output is "Equal" because objective-c is smart enough while comparing string value instead of instances (which is normal compilor behavior).

**Problem-5: What is the value of array1 and array2 in following program?**
```
NSMutableArray* array1 = @[ @“A”, @“B” ];
NSMutableArray* array2 = array1;
[array1 setObject:@“C” atIndex:0];
```

Following would be the output because both of the arrays are pointing to same memory location. 
###### Please note: @array2 = array1 it did not created the copy of array1 inside array2.
```
array1 = @[ @“C”, @“B” ];
array2 = @[ @“C”, @“B” ];
```

###### Always open to suggestions. Enjoy! 👍
