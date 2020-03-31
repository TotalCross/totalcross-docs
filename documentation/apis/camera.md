# Camera

### Overview

This class is used to enable the camera of the underlying device. The following platforms are supported: Android and iOS. It is not possible to use the webcam on PC platforms \(JavaSE, Windows XP, Vista, Seven, 8, and Linux\).

Note that you can easily rotate the image to put it in portrait mode, using the **Image.getRotatedScaledInstance\( \)** method, after retrieving the image. You may change the following options: **initialDir**, **defaultFileName** \(must end with .jpg\), and **resolutionWidth** x **resolutionHeight** \(possible values are 320x240, 640x480, 1024x768, 2048x1536; different values defaults to 640x480\). All other options are ignored.

On Android you can set the **defaultFileName**, **stillQuality**, **resolutionWidth** and **resolutionHeight**. All other options are ignored. You can call the **getSupportedResolutions\( \)** method to see the resolutions that are available on the device.

On iOS there’s no way to return the supported resolutions; it will take a photo using the default camera’s resolution, and then will resize to the resolution defined in **resolutionWidth** x **resolutionHeight**, keeping the camera’s aspect ratio. On iOS you can specify the **defaultFileName** with a path or just the name, or use a system-generated name. On iOS it is not possible to record a movie, only to take pictures.

**This class only has de default constructor. The other interesting fields are:**

* title The title to display in the window opened for the camera. 
* stillQuality Defines the quality of the image. It can be equal to CAMERACAPTURE\_STILLQUALITY\_DEFAULT \(default quality\), CAMERACAPTURE\_STILLQUALITY\_LOW \(low quality\), CAMERACAPTURE\_STILLQUALITY\_NORMAL \(normal quality\), or CAMERACAPTURE\_STILLQUALITY\_HIGH \(high quality\). 
* videoType Can be one of CAMERACAPTURE\_VIDEOTYPE\_ALL \(produces video clips that match video profiles, using just the video resolution for the match criteria, the default value\) CAMERACAPTURE\_VIDEOTYPE\_STANDARD \(produces high-quality video clips used for home movies and e-mail video messaging, using a video encoder such as the Windows Media encoder\), or CAMERACAPTURE\_VIDEOTYPE\_MESSAGING \(Produces video clips used for Multimedia Messaging Service \(MMS\) video messaging, which require a video encoder that conforms to the 3rd Generation Partnership Project \(3GPP\) specification on http://go.microsoft.com/fwlink/?LinkId=32710\). 
* videoTimeLimit Maximum time limit for recording a video. 
* captureMode Can be one of CAMERACAPTURE\_MODE\_STILL \(only picture, the default value\), CAMERACAPTURE\_MODE\_VIDEOONLY \(no sound\), or CAMERACAPTURE\_MODE\_VIDEOWITHAUDIO \(video and sound\). 
* allowRotation Use this on Android only. If false, the camera buttons will be on landscape. If true, the camera buttons will follow the device current rotation when the camera is opened. 

![](https://totalcross.com/documentation/en/api/img/xcamera.png.pagespeed.ic.fAne0JJDiH.png)

### The class **Camera** only has one method:

| Type | Name | Description |
| :--- | :--- | :--- |
| **String** | click\( \) | Takes a photo or records a video based on the members set. It returns a string with the file name where the image or video is located, or null if the user canceled. |
| **static String\[ \]** | getSupportedResolutions\( \) | Gets the supported resolutions on the current device. |

## References

* To know more details read its [JavaDocs](https://rs.totalcross.com/doc/totalcross/ui/media/Camera.html).
* For more details, check in [Github project](https://github.com/TotalCross/TCSample/blob/master/src/main/java/totalcross/sample/components/ui/CameraSample.java).



