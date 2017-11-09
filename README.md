# Fluid Slider

A slider control inspired by [Virgil Pana](https://dribbble.com/shots/3868232-Fluid-Slider)

## Usage

### Slider

The slider can be inserted in a view hierarchy as a subview. Appearance can be configured with a number of public attributes:

```swift
let slider = Slider()
slider.attributedTextForFraction = { fraction in
    let formatter = NumberFormatter()
    formatter.maximumIntegerDigits = 3
    formatter.maximumFractionDigits = 0
    let string = formatter.string(from: (fraction * 500) as NSNumber) ?? ""
    return NSAttributedString(string: string)
}
slider.setMinimumLabelAttributedText(NSAttributedString(string: "0"))
slider.setMaximumLabelAttributedText(NSAttributedString(string: "500"))
slider.fraction = 0.5
slider.shadowOffset = CGSize(width: 0, height: 10)
slider.shadowBlur = 5
slider.shadowColor = UIColor(white: 0, alpha: 0.1)
slider.contentViewColor = UIColor(red: 78/255.0, green: 77/255.0, blue: 224/255.0, alpha: 1)
slider.valueViewColor = .white
view.addSubview(slider)
```

Take a look at the `Example` project for an integration example.

Since `Slider` is a subclass of `UIControl`, it inherits target-action mechanics and it's possible to listen for user-triggered value changes:
```swift
slider.addTarget(self, action: #selector(sliderValueChanged), for: .valueChanged)
```
### Tracking Behavior

There are a couple of callbacks which allow you to listen to the slider's tracking events:
```swift
    var didBeginTracking: ((Slider) -> ())?
    var didEndTracking: ((Slider) -> ())?
```

## Animation Performance

This control is designed to use device CPU resources with care. The fluid-style animation will be disabled when low power mode is enabled or the system is under heavy load.
