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

- (void)nameOfMyMethod:(NSString*)str forUser:(User*)user withPermissions:(NSArray*)permissions
{
	NSString*	arg1 = @"Arg1";
	NSArray*	arg2 = @[@"1", @"2", @"3", @"4"];
	SomeType*	arg3 = nil;

	if (user != nil) {
		arg3 = SomeValue;
		// ...
	} else if ([str isEqualToString:@"str"]) {
		// ...
	} else {
		// ...
	}
}

```

* Braces are put after new line for `class`, method, function declaration.
* Braces are put on the same line for `if` `else if` `else`, `for`, `switch` statements
* Arguments are aligned according to the longest type name, so the names always start on the same column
* Whether you put the `*` after the type name or before the name of the var doesn't matter as long as it's the same in the whole function
* Arguments are preferably set at the beginning of the function if possible, even if they have to be set to nil, and set later, like `arg3`
* Jump a ligne after arguments declaration

### Code

* Use subscript when possible

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

self.someAction;	// Wrong!
[self someAction];	// Right!

```




