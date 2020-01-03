![paydollar2](https://user-images.githubusercontent.com/57220911/68009559-4000a480-fca8-11e9-8ed1-545a4b6e4cfd.png)

#### PayDollar is a global payment gateway that accepts payments from more than 200 countries.The PaySDK ensures payment is authorised by 3DS 2.0

- [Features](#features)
- [Requirements](#requirements)
- [Pre-requisites](#pre-requisites)
- [Installation](#installation)
- [Implementation](#implementation)



## Features
- Direct Client Side Connection
- WebView Payment - Client Post through Browser Side Connection
- Payment via Alipay

## Requirements

- iOS 10.0+
- Xcode 10.0+
- Swift version 4+



## Pre-requisites

Merchant need to integrate certificate. This certificate is provided in [PayDollar Dashboard](https://www.paydollar.com/b2c2/eng/merchant/index.jsp).

Add `paysdk.plist` and set value of certificate.

<img width="406" alt="Screenshot 2019-11-07 at 7 01 41 PM" src="https://user-images.githubusercontent.com/57219745/68393070-29b78480-0191-11ea-923a-19445f25fe52.png">

## Installation

### Framework file 

Add `AP_PaySDK.framework` file into your project by adding the dependencies in Build Phases / Link Binary With Libraries.

### CocoaPods

[CocoaPods](https://cocoapods.org) is a dependency manager for Cocoa projects. For usage and installation instructions, visit their website. To integrate PayDollarSDK into your Xcode project using CocoaPods, specify it in your `Podfile`:

```ruby
pod 'AP_PaySDK'
```

### Implementation

Add implementation of PaySDK

```
#import AP_PaySDK

class ViewController: UIViewController {
    let paySDK = PaySDK.shared
    paySDK.delegate = self
    .
    .
    .
```

### Payment Channel Types

Creating PayData for payment and process.


#### WebView Payment
```
paySDK.paymentDetails = PayData(channelType: PayChannel.WEBVIEW,
                                envType: EnvType.SANDBOX,
                                amount : "10",
                                payGate: PayGate.PAYDOLLAR,
                                currCode: currencyCode.HKD, 
                                payType: payType.NORMAL_PAYMENT, 
                                orderRef: "abcde12345", 
                                payMethod: "VISA",
                                lang: Language.ENGLISH,
                                merchantId: "1",
                                remark: "",
                                extraData :[:])

paySDK.process()

```

#### Direct Payment
```
paySDK.paymentDetails = PayData(channelType: PayChannel.DIRECT,
                                envType: EnvType.SANDBOX,
                                amount : "10",
                                payGate: PayGate.PAYDOLLAR,
                                currCode: currencyCode.HKD, 
                                payType: payType.NORMAL_PAYMENT, 
                                orderRef: "abcde12345", 
                                payMethod: "VISA",
                                lang: Language.ENGLISH,
                                merchantId: "1",
                                remark: "",
                                extraData :[:])

paySDK. paymentDetails.cardDetails = CardDetails(cardHolderName: "abc abc",
                                                 cardNo: "1234567890123456”,
                                                 expMonth: "11",
                                                 expYear: "2011",
                                                 securityCode: "123")
paySDK.process()

```

#### Payment via AliPay.
```
paySDK.paymentDetails = PayData(channelType: PayChannel.DIRECT,
                                envType: EnvType.SANDBOX,
                                amount : “10”,
                                payGate: PayGate.PAYDOLLAR,
                                currCode: currencyCode.HKD, 
                                payType: payType.NORMAL_PAYMENT, 
                                orderRef: "abcde12345”, 
                                payMethod: "ALIPAYHKAPP",
                                //payMethod: "ALIPAYCNAPP"
                                //payMethod: "ALIPAYAPP"
                                lang: Language.ENGLISH,
                                merchantId: "1",
                                remark: "",
                                extraData :[:])

paySDK.process()

```
#### Payment via WechatPay.
```
paySDK.paymentDetails = PayData(channelType: PayChannel.DIRECT,
                                envType: EnvType.SANDBOX,
                                amount : “10”,
                                payGate: PayGate.PAYDOLLAR,
                                currCode: currencyCode.HKD, 
                                payType: payType.NORMAL_PAYMENT, 
                                orderRef: "abcde12345”, 
                                payMethod: "WECHATAPP",
                                lang: Language.ENGLISH,
                                merchantId: "1",
                                remark: "",
                                extraData :[:])

paySDK.process()

```

### Payment response

```
extension ViewController : PaySDKDelegate {
    func paymentResult(result: PayResult) {

    }
}
```
For detailed description kindly follow [PayDollar Guide](http://paydollar.com/pdf/op/enpdintguide.pdf).
                
                
