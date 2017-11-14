# Appodeal Extension Demo for Defold

This is official Appodeal Extenstion for Defold with iOS and Android support.

Included Appodeal SDK:
iOS: v.2.1.7
Android: v.2.1.7

Requirements:

Defold Editor or Defold Editor 2 Preview
Min Android API Level: 14 and above
Min iOS Target: iOS 8.0 and above

Download: [![](https://img.shields.io/badge/version-2.1.7-green.svg)](https://s3.eu-central-1.amazonaws.com/appodeal-defold/Appodeal-Defold-2.1.7-141117-all.zip)

## Demo Setup

To run demo on iOS download this [libraries](https://s3.eu-central-1.amazonaws.com/appodeal-defold/Appodeal-Defold-iOS-2.1.7-lib.zip), unzip and place it under appodeal/lib folder.

## Extenstion Integration

Extract downloaded archive and unzip it to your project root folder (files should be under [project]/appodeal folder).

### Android Configuration

Set appodeal/AndroidManifest as default manifest for your project or copy all activities under [For Appodeal 2.1.7](https://github.com/appodeal/appodeal-defold-demo/blob/master/appodeal/AndroidManifest.xml#L121) tag following to your manifest:

Appodeal Android SDK requires Google Play Services 8.5 or above, but Defold uses pretty old library, so we have included new one inside this Extension. To exclude defold ones do next:
+ Create new text file on the project root folder with name *game.appmanifest*
+ Add there following:
```platforms:
    armv7-android:
        context:
            excludeJars: ["(.*)/google-play-services.jar", "(.*)/android-support-v4.jar"]
```

### iOS Configuration

iOS part ready to use, nothing to change.

### Lua Integration

Available Ad Types to use:
+ appodeal.BANNER
+ appodeal.BANNER_BOTTOM
+ appodeal.BANNER_TOP
+ appodeal.INTERSTITIAL
+ appodeal.REWARDED_VIDEO
+ appodeal.NON_SKIPPABLE_VIDEO

To initialize Appodeal SDK use:
`appodeal.initialize("fee50c333ff3825fd6ad6d38cff78154de3025546d47a84f", appodeal.INTERSTITIAL)`
Where:
+ `fee50c333ff3825fd6ad6d38cff78154de3025546d47a84f` should be changed to your specific Appodeal app key.
+ `appodeal.INTERSTITIAL` can be changed to any other ad type.
+ ad types can be used as bitwise or, for example:  `bit.bor(appodeal.INTERSTITIAL, appodeal.BANNER)`


To show ads use:
`appodeal.show(appodeal.INTERSTITIAL)`
Where:
+ `appodeal.INTERSTITIAL` can be changed to any other ad type.
+ ad types can be used as bitwise or, for example:  `bit.bor(appodeal.INTERSTITIAL, appodeal.NON_SKIPPABLE_VIDEO)`

To disable auto caching for ads use:
`appodeal.setAutoCache(appodeal.INTERSTITIAL, false)`
Where:
+ `false` sets auto cahcing for INTERSTITIAL disabled.
+ `appodeal.INTERSTITIAL` can be changed to any other ad type.
+ ad types can be used as bitwise or, for example:  `bit.bor(appodeal.INTERSTITIAL, appodeal.NON_SKIPPABLE_VIDEO)`

To cache ads use:
`appodeal.cache(appodeal.INTERSTITIAL)`
Where:
+ `appodeal.INTERSTITIAL` can be changed to any other ad type.
+ ad types can be used as bitwise or, for example:  `bit.bor(appodeal.INTERSTITIAL, appodeal.NON_SKIPPABLE_VIDEO)`

To hide BANNER ads use:
`appodeal.hide(appodeal.BANNER)`

To disable smart banners use:
`appodeal.setSmartBanners(false)`

To enable banner background use:
`appodeal.setBannerBackground(true)`

To disable banner refresh animation use:
`appodeal.setBannerAnimation(false)`

To disable big banners use:
`appodeal.setTabletBanners(false)`

To enable additional logging for debugging use:
`appodeal.setLogLevel(appodeal.LOG_LEVEL_VERBOSE)`
Available log levels:
```
appodeal.LOG_LEVEL_NONE
appodeal.LOG_LEVEL_DEBUG
appodeal.LOG_LEVEL_VERBOSE
```

To enable test ads use:
`appodeal.setTesting(true)`

To disable not child directed ads use:
`appodeal.setChildDirectedTreatment(false)`

To enable triggering on loaded callbacks for precache ads use:
`appodeal.setTriggerOnLoadedOnPrecache(appodeal.INTERSTITIAL, true)`
Where:
+ ad types can be used as bitwise or, for example:  `bit.bor(appodeal.INTERSTITIAL, appodeal.NON_SKIPPABLE_VIDEO)`
+ `true` sets trigger for interstitial on loaded callback enabled.

To disable specific network use:
`appodeal.disableNetwork("inmobi")`
Where:
+ Available parameters: "adcolony", "admob", "amazon_ads", "applovin", "appnext", "avocarrot", "chartboost", "facebook", "flurry", "inmobi", "inner-active", "ironsource", "mailru", "mmedia", "mopub", "ogury", "openx", "pubnative", "smaato", "startapp", "tapjoy", "unity_ads", "vungle", "yandex"

To disable specific network for specific ad type use:
`appodeal.disableNetworkForAdType("adcolony", appodeal.INTERSTITIAL)`
Where:
+ Available parameters: "adcolony", "admob", "amazon_ads", "applovin", "appnext", "avocarrot", "chartboost", "facebook", "flurry", "inmobi", "inner-active", "ironsource", "mailru", "mmedia", "mopub", "ogury", "openx", "pubnative", "smaato", "startapp", "tapjoy", "unity_ads", "vungle", "yandex"
+ ad types can be used as bitwise or, for example:  `bit.bor(appodeal.INTERSTITIAL, appodeal.NON_SKIPPABLE_VIDEO)`

To disable LocationPermission check for Android use:
`appodeal.disableLocationPermissionCheck()`

To disable WriteExternalStoragePermission check for Android use:
`appodeal.disableWriteExternalStoragePermissionCheck()`

To mute video ads when calls muted on Android use:
`appodeal.muteVideosIfCallsMuted(true)`

To track in app purchase use:
`appodeal.trackInAppPurchase(50, "USD")`

To use callbacks in Appodeal SDK set it before SDK initialization with:
`appodeal.setCallback(appodeal_ads_callback)`
Where:
+ appodeal_ads_callback should be a custom function with (self, msg_type) params.
+ following callbacks available:
```
local function appodeal_ads_callback(self, msg_type)
	if msg_type == appodeal.BANNER_LOADED then
		print("BANNER_LOADED")
	elseif msg_type == appodeal.BANNER_FAILED_TO_LOAD then
		print("BANNER_FAILED_TO_LOAD")
	elseif msg_type == appodeal.BANNER_SHOWN then
		print("BANNER_FAILED_TO_LOAD")
	elseif msg_type == appodeal.BANNER_CLICKED then
		print("BANNER_CLICKED")
	elseif msg_type == appodeal.INTERSTITIAL_LOADED then
		appodeal.show(appodeal.INTERSTITIAL)
		print("INTERSTITIAL_LOADED")
	elseif msg_type == appodeal.INTERSTITIAL_FAILED_TO_LOAD then
		print("INTERSTITIAL_FAILED_TO_LOAD")
	elseif msg_type == appodeal.INTERSTITIAL_SHOWN then
		print("INTERSTITIAL_SHOWN")
	elseif msg_type == appodeal.INTERSTITIAL_CLOSED then
		print("INTERSTITIAL_CLOSED")
	elseif msg_type == appodeal.INTERSTITIAL_CLICKED then
		print("INTERSTITIAL_CLICKED")
	elseif msg_type == appodeal.REWARDED_VIDEO_LOADED then
		print("REWARDED_VIDEO_LOADED")
	elseif msg_type == appodeal.REWARDED_VIDEO_FAILED_TO_LOAD then
		print("REWARDED_VIDEO_FAILED_TO_LOAD")
	elseif msg_type == appodeal.REWARDED_VIDEO_SHOWN then
		print("REWARDED_VIDEO_SHOWN")
	elseif msg_type == appodeal.REWARDED_VIDEO_FISNIHED then
		print("REWARDED_VIDEO_FISNIHED")
	elseif msg_type == appodeal.REWARDED_VIDEO_CLOSED then
		print("REWARDED_VIDEO_CLOSED")
	elseif msg_type == appodeal.NON_SKIPPABLE_VIDEO_LOADED then
		print("NON_SKIPPABLE_VIDEO_LOADED")
	elseif msg_type == appodeal.NON_SKIPPABLE_VIDEO_FAILED_TO_LOAD then
		print("NON_SKIPPABLE_VIDEO_FAILED_TO_LOAD")
	elseif msg_type == appodeal.NON_SKIPPABLE_VIDEO_SHOWN then
		print("NON_SKIPPABLE_VIDEO_SHOWN")
	elseif msg_type == appodeal.NON_SKIPPABLE_VIDEO_FISNIHED then
		print("NON_SKIPPABLE_VIDEO_FISNIHED")
	elseif msg_type == appodeal.NON_SKIPPABLE_VIDEO_CLOSED then
		print("NON_SKIPPABLE_VIDEO_CLOSED")
	end
end
```


User settings:
```appodeal.setUserId("awesome_user")
appodeal.setUserAge(26)
appodeal.setUserGender(appodeal.GENDER_MALE)
```

Custom Rules:
```appodeal.setCustomIntRule("int_rule", 217)
appodeal.setCustomBoolRule("bool_rule", true)
appodeal.setCustomDoubleRule("double_rule", 2.17)
appodeal.setCustomStringRule("string_rule", "my_string")
```

To show ads for specific placement use:
`appodeal.showWithPlacement(appodeal.INTERSTITIAL, "my_placement")`
Where:
+ `appodeal.INTERSTITIAL` can be changed to any other ad type.
+  "my_placement" should match your placement in Appodeal Dashboard.
+ ad types can be used as bitwise or, for example:  `bit.bor(appodeal.INTERSTITIAL, appodeal.NON_SKIPPABLE_VIDEO)`

To check if ad can be shown for default placement use:
`appodeal.canShow(appodeal.INTERSTITIAL)`
Where:
+ `appodeal.INTERSTITIAL` can be changed to any other ad type.
+ ad types can be used as bitwise or, for example:  `bit.bor(appodeal.INTERSTITIAL, appodeal.NON_SKIPPABLE_VIDEO)`

To check if ad can be shown for specific placement use:
`appodeal.canShow(appodeal.INTERSTITIAL, "my_placement")`
Where:
+ `appodeal.INTERSTITIAL` can be changed to any other ad type.
+  "my_placement" should match your placement in Appodeal Dashboard.
+ ad types can be used as bitwise or, for example:  `bit.bor(appodeal.INTERSTITIAL, appodeal.NON_SKIPPABLE_VIDEO)`

To get reward amount and name for REWARDED_VIDEO:
`appodeal.getRewardName()` - for default placement
`appodeal.getRewardAmount()` - for default placement
`appodeal.getRewardNameForPlacement("my_placement")` - for specific placement
`appodeal.getRewardAmountForPlacement("my_placement")` - for specific placement

## Changelog:

2.1.7 (14/11/2017)
+ Appodeal Android SDK updated to 2.1.7
+ Appodeal iOS SDK updated to 2.1.7
+ Android Callbacks crash fix 


