# iOS Addon

An iOS static library to recognize advanced gestures on iOS apps.

***

## Compatibility
- Any device that supports iOS 6+

***

##Usage

</br>

### 1- Import the GestureKit static library into your project.
- Download [URL] unzip it and drag and drop the folder into your project.
- Select “copy items into…” option. 
- Add “-ObjC” to “Other linker flags”.

</br>

### 2- Instance a GestureKit object.
Import `GestureKit.h` and instantiate it using your keyWindow and your GestureKit `GID`. A good place to do this is on you Application Delegate.

```c
#import "GestureKit.h"
...
(BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
...
[GestureKit runInWindow:self.window withGID:@”YOUR_GK_GID”];
}
```
</br>

### 3- Setup GestureKit.
You should declare on your AppDelegate a method with the same name of the defined GestureKit method. For example, you define the "PLAY" action, then you should declare:
```c
(void) PLAY{
...
}
```

```c
(void) PLAY:(NSString*) metadata{
...
}
```
In case you care about the metadata associated to the gesture.

</br>

### 4- Customizing GKVisor [optional].
GestureKit has a default visor called `GestureKitVisor`, it's responsible of show GestureKit status as `loading`, `drawing gestures`, `ready` and `warning`.

It can be replaced by your own Visor just implementing GK_VisorProtocol and then instantiating the GestureKit object with it’s alternative methods:

```c
(void) runInWindow:(UIWindow*) window withGID:(NSString*) gid withVisor:(id<GK_VisorProtocol>) visor;
```

The protocol is available on “GestureKit.h” and it’s the following:

```c
//Protocol for implementing custom visors
@protocol GK_VisorProtocol <NSObject>

@required

//To draw the gesture in your visor
- (void) touchEvent:(NSInteger) pointID beganFromPoint:(CGPoint) point;
- (void) touchEvent:(NSInteger) pointID movedToPoint:(CGPoint) point;
- (void) touchEvent:(NSInteger) pointID endedAtPoint:(CGPoint) point;

//For showing the status of the addon to the end user.
- (void) showStaticLogo;
- (void) showErrorLogo;
- (void) showLoadingLogo;

@end
```

`touchEvent:beganFromPoint:`, `touchEvent:movedToPoint:` and `touchEvent:endedAtPoint:` Are for handling the drawing of the touches on the device, each touch/finger is has an touchID associated for grouping purposes.

`showErrorLogo` method is called after an error or warning are occured. For example, if you are offline or your GID is not valid.

`showLoadingLogo` method is called while a background process is executing. For example when GestueKit is downloading data.

`showOkLogo` method is called every time GestureKit is ready.

## Maintained by
- Julio Carrettoni ()
- Twitter: [@dev_jac](http://twitter.com/dev_jac)

## Credits

<img src="http://www.gesturekit.com/assets/img/roamtouch.png" width="200" alt="RoamTouch logo">

## License
Licensed under Apache v2 License.

Copyright (c) 2014 [RoamTouch](http://github.com/RoamTouch).
