# What is Quick Tap Plus

Just shake your watch for more info.

It's an *easy* way to add weather, battery, and bluetooth pairing info to any watchface without screwing up the aesthetics. It is designed to be configurable and a drop-in addition. The 'Tap' in the name comes from the tap event. The default behavior is to show the window when the watch is shaken and then autohide after 2 seconds. This is for Pebble 2.0 only.

Have a look for yourself.

![Pebble White](http://i.imgur.com/Pz4ZRLS.png)
![Pebble Black](http://i.imgur.com/8OeSKHs.png)

# Credit where credit is do, license, etc

Weather icons are from [Alessio Atzeni](http://www.alessioatzeni.com/meteocons/) and are called "Meteocons".

Battery icon is from the [Pyconic](http://www.pyconic.com/) free set.

Bluetooth icon is from [Flaticons](http://flaticons.net/customize.php?dir=Network%20and%20Security&icon=Bluetooth.png).

Weather data is from [OpenWeatherMap.org](http://openweathermap.org/)

Examples for the Pebble team are greatly appreciated, you can find the [dev site](https://developer.getpebble.com).


Quick Tap Plus is licensed under the [*Attribution-NonCommercial-ShareAlike 3.0 Unported*](http://creativecommons.org/licenses/by-nc-sa/3.0/deed.en_US). If you have something different in mind, reach out.

# What can I configure?

Uncomment the #define in qt_config.h to enable each setting

1. `QTP_K_SHOW_TIME` *Default off.* The clock at the top is shown if this is enabled
+ `QTP_K_SHOW_WEATHER` *Default off.* Weather at the bottom is if this enabled
+ `QTP_K_AUTOHIDE` *Default off.* Automatically hide the app shade after 2 seconds if this is enabled
+ `QTP_K_DEGREES_F` *Default off.* Use farenheit if enabled, otherwise celcisus is used
+ `QTP_K_INVERT` *Default off.* White background unless enabled
+ `QTP_K_SUBSCRIBE` *Default on.* Subscribe to the bluetooth status callback. If you don't subscribe to this you *must* call `qtp_bluetooth_callback(bool connection_status)` from within your own status check.
+ `QTP_K_VIBRATE` *Default off.* Vibrate on bluetooth status change

The autotimeout length for the window is also configurable. It is an `int` and can be set like
`qtp_set_timeout(2000);` The value is in milliseconds. call this before `qtp_setup();`

# How do I use it?

I set it up to be as easy as possible to install and use.

Do not use weather if you are already using `AppMessage`. QuickTap Plus will prevent it from working. If you aren't going to use weather, don't copy the javascript over.

If you disable `QTP_K_SUBSCRIBE`, make sure to call the `qtp_bluetooth_callback(bool)` method from within your own subscription to the bluetooth connection service. Also make sure to initalize the bluetooths status of qtp by calling `qtp_init_bluetooth_status(bool)`.

## appinfo.json

Copy the array items from `resources.json` into your `appinfo.json` under the `resources.media`.

## Images

Copy the `resources/images` into your `resources/images`.

## Code

1. Copy the `QTPlus.h` and `QTPlus.c` into your `src`.
+ Copy the `js` into your src if you are planning on using weather. Do not copy the `js` if you are not going to use javascript.
+ Add `#include "QTPlus.h"`
+ Add your configuration options if any
+ Add `qtp_setup();` before your `app_event_loop()` call.
+ Add `qtp_app_deinit();` wherever you peform your deinit operations

