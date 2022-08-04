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

- iOS 11.0+
- Xcode 10.0+
- Swift version 4+
-Objective C



## Pre-requisites

Merchant need to integrate certificate. This certificate is provided in [PayDollar Dashboard](https://www.paydollar.com/b2c2/eng/merchant/index.jsp).

Add `paysdk.plist` and set value of certificate.

<img width="406" alt="Screenshot 2019-11-07 at 7 01 41 PM" src="https://user-images.githubusercontent.com/57219745/68393070-29b78480-0191-11ea-923a-19445f25fe52.png">

## Installation

### Framework file 

Add `AP_PaySDK.framework` file into your project by adding the dependencies in Build Phases / Link Binary With Libraries
and also add `Material.framework` file into your project by adding the dependencies in Build Phases / Link Binary With Libraries or add using  cocoapods as 

```
pod 'Material'

```


### CocoaPods

[CocoaPods](https://cocoapods.org) is a dependency manager for Cocoa projects. For usage and installation instructions, visit their website. To integrate PayDollarSDK into your Xcode project using CocoaPods, specify it in your `Podfile`:

```
pod 'AP_PaySDK', '2.6.16'

```

### Implementation

Add implementation of PaySDK

* Swift Code
```
@import AP_PaySDK

class ViewController: UIViewController {
    let paySDK = PaySDK.shared
    paySDK.delegate = self
    .
    .
    .
    
```
* Objective C Code
```
#import <AP_PaySDK/AP_PaySDK.h>
#import <AP_PaySDK/AP_PaySDK-Swift.h>
@import AP_PaySDK

- (void)viewDidLoad {
    [super viewDidLoad];
    paySDK = [PaySDK shared];
    paySDK.delegate = self;
    .
    .
    .
```
### Payment Channel Types

Creating PayData for payment and process.


#### WebView Payment

* Swift Code 
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
                                payRef: "",
                                resultPage: "F",
                                extraData: [:])

paySDK.process()

```
* Objective C Code
```
paySDK.paymentDetails = [[PayData alloc] initWithChannelType: PayChannelWEBVIEW                                                            envType: EnvTypeSANDBOX 
                                         amount: @"10" 
                                         payGate: PayGatePAYDOLLAR 
                                         currCode: CurrencyCodeHKD 
                                         payType: payTypeNORMAL_PAYMENT 
                                         orderRef: @"abcde12345" 
                                         payMethod: @"CC" 
                                         lang: LanguageENGLISH 
                                         merchantId: @"1" 
                                         remark: @"" 
                                         payRef: @"" 
                                         resultpage: @"F" 
                                         extraData: nil];

[paySDK process];
```

#### Direct Payment

* Swift Code
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
                                payRef: "","
                                extraData :[:])

paySDK. paymentDetails.cardDetails = CardDetails(cardHolderName: "abc abc",
                                                 cardNo: "1234567890123456”,
                                                 expMonth: "11",
                                                 expYear: "2011",
                                                 securityCode: "123")
paySDK.process()

```

* Objective C Code
```
paySDK.paymentDetails = [[PayData alloc] initWithChannelType:PayChannelDIRECT                                                              envType:EnvTypeSANDBOX 
                                         amount:amountText.text 
                                         payGate:PayGatePAYDOLLAR 
                                         currCode:CurrencyCodeHKD 
                                         payType:payTypeNORMAL_PAYMENT 
                                         orderRef: orderRef 
                                         payMethod:@"VISA" 
                                         lang:LanguageENGLISH 
                                         merchantId: merchantId 
                                         remark:@"" 
                                         payRef:@"" 
                                         resultpage:resultPage 
                                         extraData:nil];

paySDK.paymentDetails.cardDetails = [[CardDetails alloc] initWithCardHolderName:@"Test Card"                                                               cardNo:cardNoText.text                                                                            expMonth:expMonthText.text 
                                                         expYear:expYearText.text securityCode:securityCodeText.text];

[paySDK process];
```
### Payment response
* Swift Code
```
extension ViewController : PaySDKDelegate {
    func paymentResult(result: PayResult) {
        \\Code here
    }
}

```
*Objective C Code
```
-(void)paymentResultWithResult:(PayResult * _Nonnull)result {
        \\Code here
}
```
For detailed description kindly follow [PayDollar Guide](http://paydollar.com/pdf/op/enpdintguide.pdf).
                
# Related Sample
- [DeepLink Demo](https://github.com/asiapay-lib/ios-deeplink-demo)
- [Demo for all services](https://github.com/asiapay-lib/paysdk-ios-demo)
