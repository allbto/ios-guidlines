GUIDELINES
==========

Inspired by [those guidelines](https://github.com/futurice/ios-good-practices), here is how I stucture my code.

SWIFT
=====

### Syntax

#### A proper class should look like this :

```swift

class Person: ParentClass
{
	// MARK: Properties

	var firstName: String
	var lastName: String
	//...

	// MARK: Convenience

	var name: String { return "\(firstName) \(lastName)" }

	var isCurrentUser: Bool {
		// Computing
		return result
	}

	//...

	// MARK: Private properties

	private var _isUser: Bool
	//...

	// MARK: Life cycle

	init(firstName: String, lastName: String, isUser: Bool)
	{
		self.firstName = firstName
		self.lastName = lastName
		self._isUser = isUser
	}

	deinit
	{
		//...
	}

	//...

	// MARK: Actions

	func doSomethingGreat()
	{
		//...
	}

	//...

	// MARK: Private

	private func _doSomethingPrivately()
	{
		//...
	}

	//...
}

// MARK: NameOfProtocol
extension Person: NameOfProtocol
{
	func protocolFunction()
	{
		//...
	}

	//...
}

```

* Braces are put after a new line for `class`, `struct`, `enum`, `extension` and `func` declaration.
* Braces are put on the same line for variable with convenience getter/setter/setter notifications, `if` `else if` `else`, `for`, `while`, `do catch`, `switch` statements
* Private function and variables are marked with an underscore before the name
* Functions that only return a value without taking parameters should be written as variable with convenience getter. Like `name` in the example
* Protocol are always implemented in an extension, can be in the same file or separated file, should then be named `MyClass+NameOfProtocol.swift`



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






