# Biometrics Authentication in Android #

[![Android-Studio](https://img.shields.io/badge/Android%20Studio-4.0+-orange.svg?style=flat)](https://developer.android.com/studio/)
[![Kotlin Version](https://img.shields.io/badge/Kotlin-v1.4.10-blue.svg)](https://kotlinlang.org)
[![API](https://img.shields.io/badge/API-16%2B-brightgreen.svg?style=flat)](https://android-arsenal.com/api?level=19)

### Biometrics API
* With the launch of Android 10 (API level 29), developers can now use the Biometric API, part of the AndroidX Biometric Library, for all their on-device user authentication needs.
* The Android Framework and Security team has added a number of significant features to the AndroidX Biometric Library, which makes all of the biometric behavior from Android 10 available to all devices that run Android 6.0 (API level 23) or higher.
* In addition to supporting multiple biometric authentication form factors, the API has made it much easier for developers to check whether a given device has biometric sensors. And if there are no biometric sensors present, the API allows developers to specify whether they want to use device credentials in their apps.

### About this project:
This applications is sample for Biometrics Authentication in Android using Biometrics API

![](biometrics.gif)

### This application provides the below feature

* Fingerprint Authentication
* PIN/Password/Pattern Authentication

### How it works:
1. Add the Gradle dependency to your app module
```
	def biometric_version=  '1.0.0-rc02'
	implementation "androidx.biometric:biometric:$biometric_version"
```
2. Check whether the device supports biometric authentication
```
    val biometricManager =  BiometricManager.from(context)
    if(biometricManager.canAuthenticate()  ==  BiometricManager.BIOMETRIC_SUCCESS){
	    // you can authenticate with biometrics
    }
```
3. Create an instance of BiometricPrompt
```
	private fun instanceOfBiometricPrompt():  BiometricPrompt  {
		val executor =  ContextCompat.getmainExecutor(context)
		val callback =  object:BiometricPrompt.AuthenticationCallback()  {
			override fun onAuthenticationError(errorCode:  Int, errString:  CharSequence) {
				super.onAuthenticationError(errorCode, errString)
				showMessage("$errorCode :: $errString")
			}
			override fun onAuthenticationFailed()  {
				super.onAuthenticationFailed()
				showMessage("Authentication failed for an unknown reason")
			}
			override fun onAuthenticationSucceeded(result:  BiometricPrompt.AuthenticationResult{
				super.onAuthenticationSucceeded(result)
				showMessage("Authentication was successful")
			}
		}
	val biometricPrompt =  BiometricPrompt(context, executor, callback)
	return biometricPrompt
	}
```
4. Build a PromptInfo object
```
	promptInfo =  BiometricPrompt.PromptInfo.Builder()
		.setTitle("Biometric login for my app")
		.setSubtitle("Log in using your biometric credential")
		// Can't call setNegativeButtonText() and  // setAllowedAuthenticators(... or DEVICE_CREDENTIAL) at the same time.//
		//.setNegativeButtonText("Use account password") //
		.setAllowedAuthenticators(BIOMETRIC_WEAK or DEVICE_CREDENTIAL)
		.build()
```
5.  Ask the user to authenticate
```
	biometricPrompt.authenticate(promptInfo)
```
For more info go to __[Android Biometric Blog](https://android-developers.googleblog.com/2019/10/one-biometric-api-over-all-android.html)__

## Find this example useful? :heart:
Support it by joining __[stargazers](https://github.com/SimformSolutionsPvtLtd/SSBiometricsAuthentication/stargazers)__ for this repository. :star:
## License

```
Copyright 2020 Simform Solutions

 Licensed under the Apache License, Version 2.0 (the "License");
 you may not use this file except in compliance with the License.
 You may obtain a copy of the License at
    http://www.apache.org/licenses/LICENSE-2.0
 Unless required by applicable law or agreed to in writing, software
 distributed under the License is distributed on an "AS IS" BASIS,
 WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 See the License for the specific language governing permissions and limitations under the License.
```
