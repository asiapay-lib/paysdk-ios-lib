![paydollar2](https://user-images.githubusercontent.com/57220911/68009559-4000a480-fca8-11e9-8ed1-545a4b6e4cfd.png)

#### PayDollar is a global payment gateway that accepts payments from more than 200 countries.The PaySDK ensures payment is authorised by 3DS 2.0

- [Features](#features)
- [Requirements](#requirements)
- [Integration](#integration)
- [Installation](#installation)


## Features
- Direct Client Side Connection
- Client Post through Browser Side Connection
- Payment via Alipay

## Requirements

- iOS 10.0+
- Xcode 10.0+
- Swift version 4+



## Integration

Merchant need to integrate certificate. This certificate will be provided when merchant apply for the SDK service from [PayDollar Dashboard](https://www.paydollar.com/b2c2/eng/merchant/index.jsp).

Add paysdk.plist and set value of certificate.


## Installation

### CocoaPods

[CocoaPods](https://cocoapods.org) is a dependency manager for Cocoa projects. For usage and installation instructions, visit their website. To integrate PayDollarSDK into your Xcode project using CocoaPods, specify it in your `Podfile`:

```ruby
pod 'AP_PaySDK', '1.0'
```
Different version of Swift

swift 4.0
```ruby
pod 'AP_PaySDK', '1.0'
```
swift 4.2
```ruby
pod 'AP_PaySDK-swift4.2', '1.0'
```
swift 5.0
```ruby
pod 'AP_PaySDK-swift5.0', '1.0'
```

### Add implementation

Add implementation of PaySDK

```
#import AP_PaySDK

class ViewController: UIViewController {
    var paySDK = PaySDK.shared
    paySDK.delegate = self
    .
    .
    .
```

### Payment method 

```
paySDK.paymentDetails = PayData(channelType: PayChannel.DIRECT,
                                envType: EnvType.SANDBOX,
                                amount : “10”,
                                payGate: PayGate.PAYDOLLAR,
                                currCode: currencyCode.HKD, 
                                payType: payType.NORMAL_PAYMENT, 
                                orderRef: "2018102409220001”, 
                                payMethod: payMethod.VISA,
                                lang: Language.ENGLISH,
                                merchantId: "1",
                                remark: "",
                                extraData :[:])

paySDK. paymentDetails.cardDetails = CardDetails(cardHolderName: “abc abc”,
                                                 cardNo: "4918914107195011”,
                                                 expMonth: “11”,
                                                 expYear: “2011”,
                                                 securityCode: “123”)
paySDK.process()

```

### Payment response

```
extension ViewController : PaySDKDelegate {
    func paymentResult(result: PayResult) {

    }
}
```
For detailed description kindly follow [PayDollar Guide](http://www.paydollar.com/pdf/op/enpdintguide.pdf).
                
                
