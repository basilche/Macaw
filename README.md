<img src="https://image.ibb.co/jHXuWK/macaw_cover.png" alt="macaw_cover" border="0">

[![CI Status](https://travis-ci.org/exyte/Macaw.svg?style=flat)](https://travis-ci.org/exyte/Macaw) [![Version](https://img.shields.io/cocoapods/v/Macaw.svg?style=flat)](http://cocoapods.org/pods/Macaw) [![Carthage Compatible](https://img.shields.io/badge/Carthage-compatible-0473B3.svg?style=flat)](https://github.com/Carthage/Carthage) [![License](https://img.shields.io/cocoapods/l/Macaw.svg?style=flat)](http://cocoapods.org/pods/Macaw) [![Platform](https://img.shields.io/cocoapods/p/Macaw.svg?style=flat)](http://cocoapods.org/pods/Macaw)

Macaw provides primitives, visual effects, and animations for two-dimensional drawing across macOS and iOS.  It allows you to convert designs into scalable native views, fitting different screens. It is also open source (surprise-surprise) and regularly updated.

### Key Features

* SVG rendering
* scene serialization and scene deserialization into an SVG or Macaw file
* scene may include multiple responsive objects
* creating shapes in CGGraphicContext in a reasonably easy way
* friendly interface for CAAnimation 
* Macaw carefully handles changes in public API, which insures compiling even of a very old code you'd written with Macaw

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

* iOS 8.0+
* Mac OS X 10.11+
* Xcode 7.3+

### Installing

#### [with CocoaPods](http://cocoapods.org)

Add the following line to your Podfile: `pod "Macaw", "0.9.2" `

#### [with Carthage](http://github.com/Carthage/Carthage)

Add the following dependency to the Cartfile: `github "Exyte/Macaw" ~> 0.9.2`

For more details refer to [Getting Started Tutorial](https://github.com/exyte/Macaw/wiki/Getting-started)

#### Example:

```override func viewDidAppear() {
        super.viewDidAppear()
        
        view.window?.setFrame(NSRect(x: 0, y: 0, width: 1000, height: 1000), display: true)
        
        let svgView = SVGView(frame: NSRect(x: 0, y: 0, width: view.frame.width, height: view.frame.height))
        svgView.backgroundColor = .white
        svgView.contentLayout = .none
        view.addSubview(svgView)
        
        let hex = MoveTo(x: 15, y: -26)
            .L(-15, -26)
            .L(-30, 0)
            .L(-15, 26)
            .L(15, 26)
            .L(30, 0).build()
        
        let red = Color(val: 0xFF0000).with(a: 0.5)
        let pink = Color(val: 0xCC1496).with(a: 0.5)
        let purple = Color(val: 0x993D7E).with(a: 0.5)
        let green = Color(val: 0x40FFB7).with(a: 0.5)
        let blue = Color(val: 0x14CCCC).with(a: 0.5)
        let swamp = Color(val: 0x3D9999).with(a: 0.5)
        
        let wStep = 60.0
        let hStep = 10.0
        let delta = 20.0
        
        let shapes = [Shape(form: hex, fill: red, place: .move(dx: 0, dy: hStep)),
                      Shape(form: hex, fill: pink, place: .move(dx: delta, dy: 0)),
                      Shape(form: hex, fill: purple, place: .move(dx: wStep, dy: hStep)),
                      Shape(form: hex, fill: green, place: .move(dx: delta + wStep, dy: 0)),
                      Shape(form: hex, fill: blue, place: .move(dx: 2*wStep, dy: hStep)),
                      Shape(form: hex, fill: swamp, place: .move(dx: delta + 2*wStep, dy: 0)),
                      Shape(form: hex, fill: red, place: .move(dx: 3*wStep, dy: hStep)),
                      Shape(form: hex, fill: pink, place: .move(dx: delta + 3*wStep, dy: 0))]
        
        let g = Group(contents: shapes, place: .move(dx: 100, dy: 100))
        
        svgView.node = g
    }
```

<img src="https://image.ibb.co/eCPWfp/Screen_Shot_2018_08_16_at_12_16_56.png" alt="Screen_Shot_2018_08_16_at_12_16_56" border="0" align="middle" alt="Macaw_example_hexagons">

#### Build from sources
* clone the repo `git@github.com:exyte/Macaw.git`
* open terminal and run `cd <MacawRepo>/Example/`
* run `pod install` to install all dependencies
* run `open Example.xcworkspace/` to open project in the Xcodesage 

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Authors

This project is created and maintained by [exyte](http://www.exyte.com), a ditital agency focused on mobile and VR.
We truly appreciate your feedback and use cases. Please share your story or opinion at info@exyte.com.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

### Areas for Improvements / involvement
* tvOS, watchOS support
* SVG parcing
