Debug Macros for Objective-c
============================

Debuggify is a collection of shortcut macros for quickly adding debugging output
to Objective-C methods. See below for examples.

## How to get started
Just add the `debuggify.h` header to your project (for example #import
"debuggify.h" in your project's .pch) and set the `DEBUG` flag.

## Examples
Here's a couple of simple examples to give an idea of how debuggify works:

Just add the @debuggify() macro at the beginning of the method you want to debug
and pass it any interesting objects you want to log. Optionally add
@debuggify_time at the end to print the time it took to execute the method.


```objective-c
@interface SomeClass
@property NSString *someState;
@end

@implementation SomeClass
- (id)init
{
  self = [super init];
  if (self) {
    self.someState = @"I'm doing something..."
  }
  return self;
}

- (void)doSomethingWith:(SomeClass *)someone
{
  @debuggify(self, someone)

  sleep(10); // d`oh

  @debuggify_time
}

- (NSString *)description
{
  return self.someState;
}
@end
```

Now running this code...

```objective-c
SomeClass *sc = [SomeClass new];
sc.someState = @"I'm doing something else!";
[[SomeClass new] doSomethingWith:sc];
```

...will print the following message:

```
> -[SomeClass doSomethingWith:]:
>      0: self = I'm doing something...
>      1: someone = I'm doing something else!
> Execution time: 10.001630ms
```

## Contributions
Pull requests are very welcome. It would be nice to make this thing more
advanced. One particular thing would be to add support for method paramters.
There is already a lot of code out there that does this, but I wanted to keep
this short and without any compiled code (i.e. just a header to drop in).

## Issues
Please report any issues to the GitHub issuetracker.

## Thanks
Thank you to Jake Wharton for the inspiration by creating something
[similiar](https://github.com/JakeWharton/hugo) (but way more advanced) for
Java.

