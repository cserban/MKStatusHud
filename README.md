# MKStatusHud

[![Version](https://img.shields.io/cocoapods/v/MKStatusHud.svg?style=flat)](http://cocoapods.org/pods/MKStatusHud)
[![License](https://img.shields.io/cocoapods/l/MKStatusHud.svg?style=flat)](http://cocoapods.org/pods/MKStatusHud)
[![Platform](https://img.shields.io/cocoapods/p/MKStatusHud.svg?style=flat)](http://cocoapods.org/pods/MKStatusHud)

## Demo
![Gif](https://media.giphy.com/media/xUOxf1ItNMsnX81aNy/giphy.gif)
![Gif](https://media.giphy.com/media/3o6fJ4mwrIOtfer8yY/giphy.gif)
![Gif](https://media.giphy.com/media/xT0xeGvx6mOeN124eI/giphy.gif)
![Gif](https://media.giphy.com/media/l2QEcfghWUBnO7kTm/giphy.gif)

## Requirements
- iOS 9.+ 
- Xcode 9.0+
- Swift 4.0+

## Installation

MKStatusHud is available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
pod 'MKStatusHud'
```
## Usage
After adding the framework to your project, you need to import the modules
```ruby
import MKStatusHud
import Lottie
```
Now, you can proceed to create  an arbitrary HUD with image like this:
```swift
let hud = HUD(withImage: UIImage()), title: "Please wait!", subtitle: "While download proccess completes.")
```
or you can create HUD with adobe After Efect animation like this:
```swift
let hud = HUD(withAnimation: LOTAnimationView(name: "loader-success-failed"), title: "Please wait!", subtitle: "While download proccess completes.")
```
alternatively you can customize the hud and animation behavior with lots of "plumbing" API:
```swift
hud.rotation            // rotates  hud image
hud.presentOnView       // if provided will present hud on that view, other ways it will use UIApplication.keywindow
```
Animation quick settings, you can use those, or you can manipulate animation directly:
```swift
hud.animateToProgress   // plays animation to the given progress
hud.animationLoop       // loops the animation
hud.animationScale      // scales the animation
```
When you done setting up the hud, you can present it:
```swift
   hud.show({(_) in
            // start network request and wait for response
            // some time later update the hud with the response status 
            //...//
            hud.update(withImage: UIImage(), title: "Done!", subtitle: "Download completed.",rotation: false,dismiss:10)
            //or if its a hud with vector animation you can update animation in realtime
            hud.animateToProgress = 0.47
            hud.animationLoop = false
            hud.update()
            
        }, progress: { (progress) in
            // progres block calls recieved in every 0.5s.
        }, animation: { (isCompleted) in
            // calls when vector animation stops and indicates if it is finished or not
            if isCompleted {
                hud.updateWith(title: "Done!", subtitle: "Process completed.")
                hud.close(hideAfter: 2)
            }
        }) { (isClosed) in
            // calls when the hud gets dissmissed
        }
```



## Example
To run the example project, clone the repo, and run `pod install` from the Example directory first.

## Author

ro6lyo, roshlyo@icloud.com

## License

MKStatusHud is available under the MIT license. See the LICENSE file for more info.
