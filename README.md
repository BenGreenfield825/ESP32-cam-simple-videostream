# ESP32-Cam-Simple-Videostream

## Features
- Pre-configured and easy to use basic videostreaming web page
- Capture still image or start a stream
- Toggle the flash on and off

## Instructions
- Create a file named `WifiCredentials.h` and add 
    ```
    #define SSID "your-ssid"
    #define PASSWORD "your-password"
    ```
    - Alternatively you can fill this info in on lines 8 and 9 in `ESP32-cam-simple-videostream.ino`
- Uncomment the correct board for your use case in the definition section (`CAMERA_MODEL_AI_THINKER` is selected by default and usually works the best)
### Optional
- Configure static IP settings starting on line 11
- Change clock speed on line 123
- Change camera resolution on line 157

## Tips and Tricks for Performance
The ESP32-cam is known for having performance issues in the sense of very low FPS. I have found that the trick that helped the most was reducing the clock speed from 20mhz to 8mhz. Most of the problem comes from GPIO0 which acts as both the boot pin and the clock pin. When running at a high clock speed, this pin seems to cause interference and destroys FPS. Reducing the clock speed will lose some video quality, but the FPS will be much better.

The other trick that can help is to use an external WiFi antenna. The onboard WiFi antenna also seems to cause issues with interference, so having an external antenna helps to fix this. Make sure you change the resistor! [Information on this](https://randomnerdtutorials.com/esp32-cam-connect-external-antenna/)

Another trick that some people have had luck with is [using aluminum tape](https://www.reddit.com/r/esp32/comments/r9g5jc/fixing_ymmv_the_poor_frame_rate_on_the_esp32cam/) as a grounding plane for the noisy clock pin

## Sources
- Code originally from here (didn't see a gh link): https://www.hackster.io/KDPA/esp32-cam-video-surveillance-smart-camera-7f9a63
    - That code is based off this example code: https://github.com/espressif/arduino-esp32/tree/master/libraries/ESP32/examples/Camera/CameraWebServer
- WiFi and clock interference 
    - https://www.reddit.com/r/esp32/comments/r7kqtt/esp32cam_super_fast_frame_rate_when_putting_the/?utm_source=share&utm_medium=android_app&utm_name=androidcss&utm_term=1&utm_content=share_button
    - https://github.com/espressif/arduino-esp32/issues/4655
    - https://www.reddit.com/r/esp32/comments/r9g5jc/fixing_ymmv_the_poor_frame_rate_on_the_esp32cam/
