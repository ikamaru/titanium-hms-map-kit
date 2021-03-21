# HUAWEI MAP Kit - Titanium Module

A Titanium Module to use the following [HUAWEI Map Kit](https://developer.huawei.com/consumer/en/hms/huawei-MapKit)


## Content
* [Requirements](#requirements)
* [Preparation](#preparation)
* [API](#api)
* [Example](#example)
* [Build from source](#build)

## Requirements
- [x] Make sure to add the following [HMS preparation](https://github.com/ikamaru/titanium-hms-env_preparation) Plugin to you project which is responsible for preparing the HMS environment in your project.

## Preparation
- [x] Download the `ti.map` folder from this repo and past it inside `C:\ProgramData\Titanium\modules\android\` then add this module to your **tiapp.xml** as the following
```xml
<modules>
 <module version="5.3.0" platform="android">ti.map</module>
</modules>
```
- [x] Before using Map Kit, enable it. For details, please refer to [Enabling Required Services](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides-V5/android-sdk-config-agc-0000001061560289-V5).
- [x] After enabling the Map Kit make sure to re-download the `agconnect-services.json` and past it to the **platform/android** folder of your project as described in the HMS preparation [HMS preparation](https://github.com/ikamaru/titanium-hms-env_preparation#structure-of-the-project) Plugin 

## API
- This module was built in a similar way to the [**ti.map** provided by Appaccelerator](https://docs.appcelerator.com/platform/latest/#!/api/Modules.Map), which means that the doc of this module is totally similar to the doc of the ti.map that you can consult by clicking on the following [link](https://docs.appcelerator.com/platform/latest/#!/api/Modules.Map).
- If you have already integrated the [**ti.map** provided by Appaccelerator](https://docs.appcelerator.com/platform/latest/#!/api/Modules.Map) in your app, there is no need to change anything in your code, just follow the previous configuration and the HUAWEI map will be ready in your project. The only difference is that you have to replace in your code the isGoogleMobileServicesAvailable method with isHuaweiMobileServicesAvailable method.
- In the **[ti.map documentation](https://docs.appcelerator.com/platform/latest/#!/api/Modules.Map)**, it is written that you must to add the API Key of the map in the **tiapp.xml** file but for us, this is not the case as we have already added the **agconnect-services.json** file to the project.

## Example
- You can test the demo existing in this repo by replacing the **Resources** folder in the **DemoMapHms** in this repo with the **Resources** folder inside your Titanium app that we created with the previously, then build.

## Build
```bash
titanium build --platform android --keystore "PATH_TO_KEY_STORE.jks" --key-password "KEY_PWS" --alias "ALIAS" --store-password "STORE_PWD" 
```
> **Note**: 
> - When building for Android, make sure you have sign the app using the keystore that you used to configure your SHA256 fingerprint of your project in AppGallery Connect 
> - you can add `-T device -C all` to the above command to run on the device directly. 

![ti map_result](https://user-images.githubusercontent.com/61454003/101955022-5abc8100-3bfd-11eb-9658-56a7b22f04ff.gif)
## Legal

(c) 2021 by *Ikamaru*
