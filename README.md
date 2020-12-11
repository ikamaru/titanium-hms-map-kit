# titanium-hms-map-kit
A Titanium Module to use the following [HUAWEI Map Kit](https://developer.huawei.com/consumer/en/hms/huawei-MapKit)

## Preparations for Integrating HUAWEI HMS Core
##### 1- Console preparation
- Run the keytool command to get the SHA256 fingerprint from the keystore: 
>keytool -list -v -keystore hms_test.jks

Note: Replace **hms_test.jks** with your keystore path
- Obtain the SHA256 fingerprint from the result:
![key](https://user-images.githubusercontent.com/61454003/101916607-7a38b700-3bc7-11eb-8ddb-c7746432dea8.png)

- On the AppGallery Connect (AGC) console of [HUAWEI Developer](https://developer.huawei.com/consumer/en/), Select your project or create a new one if you didn't do yet, then:
    -    Enable Map api by going to the tab **Project Setting** > **Manage APIs**:
![image](https://user-images.githubusercontent.com/61454003/101917818-ee278f00-3bc8-11eb-98b6-a6373e88d072.png)
![image](https://user-images.githubusercontent.com/61454003/101917897-04354f80-3bc9-11eb-96df-7c3736ce5293.png)
    -    Go back to **General information** and past the obtained SHA256 fingerprint, Click √ to save the fingerprint and download then the **agconnect-services.json** file.
![image](https://user-images.githubusercontent.com/61454003/101918101-3f378300-3bc9-11eb-9633-73beedb855b3.png)

##### 2- Titanium environment preparation
###### Titanium SDK side:
-   Add the following lines in the **root.build.gradle** file **C:\ProgramData\Titanium\mobilesdk\win32\9.0.3.GA\android\templates\build\root.build.gradle**
![image](https://user-images.githubusercontent.com/61454003/101933545-a6aafe00-3bdc-11eb-8647-4c95f4c8401e.png)
```
buildscript {
	repositories {
	    //
		maven { url 'https://developer.huawei.com/repo/' } // HUAWEI Maven repository
	}
	dependencies {
	    //
	    classpath 'com.huawei.agconnect:agcp:1.4.1.300'  // HUAWEI agcp plugin
	}
}
allprojects {
	repositories {
		//
		maven { url 'https://developer.huawei.com/repo/' } // HUAWEI Maven repository
	}
}
```
-   Add the following lines in **app.build.gradle** file **C:\ProgramData\Titanium\mobilesdk\win32\9.0.3.GA\android\templates\build\app.build.gradle**
![image](https://user-images.githubusercontent.com/61454003/101934612-1ec5f380-3bde-11eb-9832-19cbf4e32c5a.png)
```
// Apply the Huawei plugin if included
if (file("${projectDir}/agconnect-services.json").exists()) {
	apply plugin: 'com.huawei.agconnect'
}
```
-   In the same **app.build.gradle** file change inside the signingConfig the config with the  following
![image](https://user-images.githubusercontent.com/61454003/101944465-0f01db80-3bed-11eb-9ec9-d288cd063058.png)
```
config {
	storeFile file("D:\\0-Programming\\18-Titanium\\new\\CreateModule\\DemoMapHms\\hms_test.jks")
	storePassword "xxxxxx"
	keyAlias "xxxxxx"
	keyPassword "xxxxxxx"
}
```
Note: make sure to update this whenever you want to build a different project with the correspending keystore
-   Add the following lines responsible for copying the **agconnect-services.json** file we downloaded using HUAWEI Developer Console from your Titanium project to the app-level of the generated Android project: **C:\ProgramData\Titanium\mobilesdk\win32\9.0.3.GA\android\cli\commands\_build.js**
![image](https://user-images.githubusercontent.com/61454003/101935025-b3c8ec80-3bde-11eb-9f86-a382f944c05f.png)
```
//huawei services
	const huaweiServicesFile = path.join(this.projectDir, 'platform', 'android', 'agconnect-services.json');
	if (await fs.exists(huaweiServicesFile)) {
		afs.copyFileSync(huaweiServicesFile, path.join(this.buildAppDir, 'agconnect-services.json'), {
			logger: this.logger.debug
		});
	}
```
-  **Don't forget** to download the **dist\modules\android\ti.map\5.3.0** from this repo and past the **ti.map** folder inside **C:\ProgramData\Titanium\modules\android\\** or replace it with the old **ti.map** module if exists. 
###### Titanium App side:
-   Create a Titanium Project using the following command:
> titanium create --type app --platforms android
-   Create a **platform\android** folder in your Titanium project's root path, inside of this folder create a **build.gradle** file and put the **agconnect-services.json** file downloaded using HUAWEI Developer Console:
![image](https://user-images.githubusercontent.com/61454003/101936459-e1169a00-3be0-11eb-8738-a19f2ee7dd53.png)
-   Inside **tiapp.xml** add the **ti.map** module we downloaded before:
```
<modules>
	<module version="5.3.0" platform="android">ti.map</module>
</modules>
```
## ti.map Module Usage
-  You can test the demo existing in this repo by replacing the **DemoMapHms\Resources\\** folder with the **Resources folder** inside your Titanium app that we created with the previous command, then build the project:
>    titanium build --platform android