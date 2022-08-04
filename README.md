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

Add `paysdk.plist` and set value of certificate and "Domain" key value pair. Value for the Domain is optinal

<img width="406" alt="Screenshot 2021-01-22 at 1 51 30 AM" src="https://user-images.githubusercontent.com/57219862/105408838-80ee2b80-5c55-11eb-8f5b-085ddbf88615.png">

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

### For UICustomization
* Swift Code
```
let customization = UiCustomization()

let submitButtonCustomization = ButtonCustomization("Courier", "#FF0000", 15, "#d3d3d3", 4)
let resendButtonCustomization = ButtonCustomization("Courier", "#FF0000", 15, "#d3d3d3", 4)
let cancelButtonCustomization = ButtonCustomization("Courier", "#FF0000", 15, "#d3d3d3", 4)
let nextButtonCustomization = ButtonCustomization("Courier", "#FF0000", 15, "#d3d3d3", 4)
let continueButtonCustomization = ButtonCustomization("Courier", "#FF0000", 15, "#d3d3d3", 4)
let labelCustomization = LabelCustomization("Courier", "FF0000", 14, "FF0000", "Courier", 20)
let textboxCustomization = TextBoxCustomization("Courier", "#FF0000", 14, 5, "#d3d3d3", 4)
let toolBarCustomization = ToolbarCustomization("Courier", "#FFFFFF", 20, "#000000", "Header Text", "Close Button Text")

try! customization.setButtonCustomization(submitButtonCustomization, .SUBMIT)
try! customization.setButtonCustomization(resendButtonCustomization, .RESEND)
try! customization.setButtonCustomization(cancelButtonCustomization, .CANCEL)
try! customization.setButtonCustomization(nextButtonCustomization, .NEXT)
try! customization.setButtonCustomization(continueButtonCustomization, .CONTINUE)
try! customization.setLabelCustomization(labelCustomization)
try! customization.setTextBoxCustomization(textboxCustomization)
try! customization.setToolbarCustomization(toolBarCustomization)

paySDK.uiCustomization = customization
```

* Objective C Code
```
UiCustomization *customization = [[UiCustomization alloc] init];

ButtonCustomization *submitButtonCustomization = [[ButtonCustomization alloc] init:@"Courier" :@"#FF0000" :15 :@"#d3d3d3" :4];
ButtonCustomization *resendButtonCustomization = [[ButtonCustomization alloc] init:@"Courier" :@"#FF0000" :15 :@"#d3d3d3" :4];
ButtonCustomization *cancelButtonCustomization = [[ButtonCustomization alloc] init:@"Courier" :@"#FF0000" :15 :@"#d3d3d3" :4];
ButtonCustomization *nextButtonCustomization = [[ButtonCustomization alloc] init:@"Courier" :@"#FF0000" :15 :@"#d3d3d3" :4];
ButtonCustomization *continueButtonCustomization = [[ButtonCustomization alloc] init:@"Courier" :@"#FF0000" :15 :@"#d3d3d3" :4];

LabelCustomization *labelCustomization = [[LabelCustomization alloc] init:@"Courier" :@"#FF0000" :14 :@"#FF0000":@"Courier" :20];
TextBoxCustomization *textBoxCustomization = [[TextBoxCustomization alloc] init:@"Courier" :@"FF0000" :14 :4 :@"FF0000" :4];
// ToolbarCustomization *toolbarCustomization = [[ToolbarCustomization alloc] init:@"Courier" :@"#FFFFFF" :20 :@"#000000" :@"Payment Page"];
NSError *err;
[customization setLabelCustomization:labelCustomization error:&err];
[customization setButtonCustomization:submitButtonCustomization : PaySDKButtonTypeSUBMIT error:&err];
[customization setButtonCustomization:resendButtonCustomization : PaySDKButtonTypeRESEND error:&err];
[customization setButtonCustomization:cancelButtonCustomization : PaySDKButtonTypeCANCEL error:&err];
[customization setButtonCustomization:nextButtonCustomization : PaySDKButtonTypeNEXT error:&err];
[customization setButtonCustomization:continueButtonCustomization : PaySDKButtonTypeCONTINUE error:&err];

[customization setLabelCustomization:labelCustomization error:&err];
[customization setTextBoxCustomization:textBoxCustomization error:&err];
//[customization setToolbarCustomization:toolbarCustomization error:&err];
[paySDK setUiCustomization:customization];
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
                                showCloseButton: true,
                                showToolbar: true,
                                webViewClosePrompt: "Do you really want to close this page?",
                                extraData: [:])

//For giving the merchant app rootviewcontroller to present webview. Its an optional parameter.
paysdk.paymentDetails.presentController = PresentViewController(presentViewController: (UIApplication.shared.keyWindow?.rootViewController)!)

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
                                         showCloseButton: true
                                         showToolbar: true
                                         webViewClosePrompt: @"Do you really want to close this page?"
                                         extraData: nil];

//For giving the merchant app rootviewcontroller to present webview. Its an optional parameter.
paysdk.paymentDetails.presentController = [[PresentViewController alloc] initWithPresentViewController:[[[UIApplication sharedApplication]keyWindow]rootViewController]];

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
                                payRef: "",
                                resultPage: "F",
                                showCloseButton: false,
                                showToolbar: false,
                                webViewClosePrompt: "",
                                extraData :[:])

paySDK.paymentDetails.cardDetails = CardDetails(cardHolderName: "abc abc",
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
                                         showCloseButton: false
                                         showToolbar: false
                                         webViewClosePrompt: @"",
                                         extraData:nil];

paySDK.paymentDetails.cardDetails = [[CardDetails alloc] initWithCardHolderName:@"Test Card"
                                                         cardNo:cardNoText.text
                                                         expMonth:expMonthText.text 
                                                         expYear:expYearText.text 
                                                         securityCode:securityCodeText.text];

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
