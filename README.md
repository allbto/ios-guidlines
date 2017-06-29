GUIDELINES
==========

Inspired by [those guidelines](https://github.com/futurice/ios-good-practices) and [Ray Wenderlich Swift Style Guide](https://github.com/raywenderlich/swift-style-guide).        
So here is how I stucture my code.

SWIFT
=====

### Syntax

#### A `class` is declared `final` unless designed to be overriden

```swift
class MyClassToOverride {
    ...
}

final class MyFinalClass: MyClassToOverride {
    ...
}
```

#### Properties are declared with `let` unless designed to be mutable

```swift
// Immutable
let bestFriends = [userA, userB]

// Mutable
var primeNumbers = [2, 3, 5, 7, 11]

primeNumbers.append(13)
primeNumbers.append(17)
```

#### Braces are put on the same line as the statement

```swift
// Protocol
protocol MyClassProtocol {
    ...
}

// Class
final class MyClass {

	// Enum
    enum MyClassEnum {
        ...
    }
    
    // Func
    func doSomethingInteresting() {
        ...
    }

}

// Extension
extension MyClass: MyClassProtocol {
    ...
}

// Computed properties
var color: UIColor {
    return .black
}

// Variable with getter/setter
var color: UIColor {
    get {
        return someColor
    }
    
    set {
        someColor = newValue
    }
}

// if, else
if something {
    ...
} else if somethingElse {
    ...
} else {
    ...
}

// Complexe switch
switch type {
    case .SomeType:
        doSomething()
        ...
        
    case .SomeOtherType:
        doSomethingElse()
        ...
        
    default:
        break
}

// Simple switch
switch color {
    case .White:    return "FFFFFF"
    case .Black:    return "000000"
    case .Red:      return "FF0000"
    default:        return nil
}

// do, catch
do {
    try somethingDangerous()
} catch e {
    print(e)
}
```

#### Private function and variables are marked with an underscore before the name

```swift
final class MyClass {
    // MARK: Properties

    var showUser: Bool

    // MARK: Private Properties
    
    private var _isUser: Bool
    
    // MARK: Actions
    
    func doSomething() {
        ...
    }
    
    // MARK: Private
    
    func _doSomethingPrivately() {
        ...
    }
}
```

#### A function that only return a value without taking parameters should be written as computed property

```swift
// Simple accessor
var color: UIColor {
    return .black
}

// Accessor with parameter
func color(alpha alpha: CGFloat) -> UIColor {
    return UIColor.black.withAlphaComponent(alpha)
}
```

#### Other rules

* Protocol are always implemented in an extension. It can be in the same file or separated file, in this case it should be named `MyClassNameOfProtocol.swift`

#### So a proper `class` should look like this :

```swift

final class Person: ParentClass {

	// MARK: Properties

	let firstName: String
	let lastName: String

	// MARK: Lazy properties
	
	// Auto-closured lazy property
	lazy var friends: [Friend] = user.friends()
	
	// Normal lazy property
	lazy var filteredFriends = {
	    let friends = user.friends()
	    
	    return friends.filter { $0.isActive == true }
	}()

	// MARK: Private properties

	private let _isUser: Bool

	// MARK: Getters

	var fullName: String { return "\(firstName) \(lastName)" }

	var isCurrentUser: Bool {
		// Computing
		return result
	}

	// MARK: Life cycle

	init(firstName: String, lastName: String, isUser: Bool) {
		self.firstName = firstName
		self.lastName = lastName
		self._isUser = isUser
	}

	deinit {
		...
	}

	// MARK: Actions

	func doSomethingGreat() {
		...
	}

	// MARK: Private

	private func _doSomethingPrivately() {
		...
	}

}

// MARK: NameOfProtocol
extension Person: NameOfProtocol {

	func protocolFunction() {
		...
	}

}
```

#### View Controller

```swift
final class MyViewController: UIViewController {

	// MARK: Properties

	var onComplete: (() -> Void)?

	var name: String? {
		didSet {
			_nameLabel.text = name
		}
	}

	// MARK: Subviews

	private var _nameLabel: UILabel!

	// MARK: Life cycle

	override func viewDidLoad() {
        super.viewDidLoad()

        // Name label
        _nameLabel = UILabel()
        ...
    }

	// MARK: Private

	private func _privateAction() {
		...
	}

}
```

OBJECTIVE-C
===========

### Header

* Provide full path for libraries header
* Separate libraries headers from local headers

```objective-c

#import <Underscore.m/Underscore.h>

#import "MyViewController.h"

```

### Syntax

#### A proper method should look like this :

```objective-c

- (void)nameOfMyMethod:(NSString *)str forUser:(User *)user withPermissions:(NSArray *)permissions
{
	NSString	*arg1 = @"Arg1";
	NSArray		*arg2 = @[@"1", @"2", @"3", @"4"];
	SomeType	*arg3 = nil;

	if (user != nil) {
		arg3 = SomeValue;
		// ...
	} else if ( [str isEqualToString:@"str"] &&
				([self someAction:str] || [self someOtherAction:str]) ) {
		// ...
	} else {
		// ...
	}
}

```

* Braces are put after new line for `class`, method, function declaration.
* Braces are put on the same line for `if` `else if` `else`, `for`, `switch` statements
* Arguments are aligned according to the longest type name, so the names always start on the same column
* Arguments are preferably set at the beginning of the function if possible, even if they have to be set to nil, and set later, like `arg3`
* Jump a ligne after arguments declaration

### Code

* Use Objective-C Literals when possible

```objective-c

// String
str = @"Some string";

// Array
array = @[@"1", @"2", @"3"];
array[0] = @"0";

// Dictionary
dict = @{
	@"key": @"Value",
	@"key2": @"Value 2"
};
dict[@"key"] = @"New value"

// Numbers as NSNumber
num = @(3.14);
// Use () Preferably

// Bool as NSNumber
isTrue = @YES // Or @NO

```

* Use `.` when using accessor

```objective-c

@property (nonatomic, assign) BOOL foo;

- (BOOL)isFoo
{
	return foo || someExpression;
}

// Usage

self.foo = YES;
[object method:self.foo];

[object method:self.isFoo];

// But not for action method :

- (void)someAction
{
	// ...
	// Method does some action and is not accessor
	// ...
}

self.someAction;	// Wrong
[self someAction];	// Right

```

