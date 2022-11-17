# Protocol Documentation
<a name="top"></a>

## Table of Contents

- [Skyle.proto](#Skyle-proto)
    - [BinocularGaze](#Skyle-BinocularGaze)
    - [Button](#Skyle-Button)
    - [ButtonActions](#Skyle-ButtonActions)
    - [CalibConfirm](#Skyle-CalibConfirm)
    - [CalibControl](#Skyle-CalibControl)
    - [CalibImprove](#Skyle-CalibImprove)
    - [CalibMessages](#Skyle-CalibMessages)
    - [CalibPoint](#Skyle-CalibPoint)
    - [CalibQuality](#Skyle-CalibQuality)
    - [DeviceVersions](#Skyle-DeviceVersions)
    - [FilterOptions](#Skyle-FilterOptions)
    - [IPadOptions](#Skyle-IPadOptions)
    - [OptionMessage](#Skyle-OptionMessage)
    - [Options](#Skyle-Options)
    - [Point](#Skyle-Point)
    - [PositioningMessage](#Skyle-PositioningMessage)
    - [Profile](#Skyle-Profile)
    - [RawImage](#Skyle-RawImage)
    - [ResetMessage](#Skyle-ResetMessage)
    - [ScreenResolution](#Skyle-ScreenResolution)
    - [StatusMessage](#Skyle-StatusMessage)
    - [TriggerMessage](#Skyle-TriggerMessage)
    - [calibControlMessages](#Skyle-calibControlMessages)
    - [calibCursorMessages](#Skyle-calibCursorMessages)
  
    - [IPadOptions.iPadModel](#Skyle-IPadOptions-iPadModel)
    - [Options.eyeUse](#Skyle-Options-eyeUse)
    - [Profile.Skill](#Skyle-Profile-Skill)
  
    - [Skyle](#Skyle-Skyle)
  
- [Scalar Value Types](#scalar-value-types)



<a name="Skyle-proto"></a>
<p align="right"><a href="#top">Top</a></p>

## Skyle.proto
Full protocol that is used to interface with the Skyle eye tracker with gRPC

(c) 2020 - 2022 eyeV GmbH, written by Mathias Anhalt

https://eyev.de/


<a name="Skyle-BinocularGaze"></a>

### BinocularGaze
Message for binocular gaze points


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| leftGaze | [Point](#Skyle-Point) |  | left gaze point |
| rightGaze | [Point](#Skyle-Point) |  | right gaze point |






<a name="Skyle-Button"></a>

### Button
Button message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| isPresent | [bool](#bool) |  | Indicates if a button is connected to the eye tracker |
| buttonActions | [ButtonActions](#Skyle-ButtonActions) |  | Configured button actions |
| availableActions | [string](#string) | repeated | List with available actions, currently: &#34;none&#34;, &#34;unknown&#34;, &#34;leftClick&#34;, &#34;rightClick&#34;, &#34;scroll&#34;, &#34;calibrate&#34; |






<a name="Skyle-ButtonActions"></a>

### ButtonActions
Representing the three available button actions


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| singleClick | [string](#string) |  | Action to trigger, when a single click on the button is performed |
| doubleClick | [string](#string) |  | Action to trigger, when a double click on the button is performed |
| holdClick | [string](#string) |  | Action to trigger when the button is constantly pushed |






<a name="Skyle-CalibConfirm"></a>

### CalibConfirm
Message to confirm a calibration point


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| confirmed | [bool](#bool) |  | confirmed this point |






<a name="Skyle-CalibControl"></a>

### CalibControl
Message describing the calibration status


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| calibrate | [bool](#bool) |  | Indicates a running calibration or requests a calibration |
| numberOfPoints | [int32](#int32) |  | Number of calibration points, currently 5 and 9 is accepted |
| abort | [bool](#bool) |  | Indicates an aborted calibration or request an abort |
| stopHID | [bool](#bool) |  | If connected to an iPad or tablet, this will indicate if the native cursor should move or not |
| res | [ScreenResolution](#Skyle-ScreenResolution) |  | Screen resolution of the client: set this to the native client resolution (if unset, internal resolutions will be used) |
| stepByStep | [bool](#bool) |  | Indicates a manual step by step calib (each point gets confirmed by client or button) |






<a name="Skyle-CalibImprove"></a>

### CalibImprove
Message to improve a calibration


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| rating | [int32](#int32) |  | Improve points that are worse than this rating (1-5) |
| stopHID | [bool](#bool) |  | If connected to an iPad or tablet, this will indicate if the native cursor should move or not |






<a name="Skyle-CalibMessages"></a>

### CalibMessages
Message wrapping calibration host messages


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| calibControl | [CalibControl](#Skyle-CalibControl) |  | Message describing the calibration status, gets sent on change |
| calibPoint | [CalibPoint](#Skyle-CalibPoint) |  | Calibration point that gets sent on change |
| calibQuality | [CalibQuality](#Skyle-CalibQuality) |  | Calibration quality, gets sent when calibration is done |






<a name="Skyle-CalibPoint"></a>

### CalibPoint
Message describing a calibration point


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| count | [int32](#int32) |  | Number of calibration point: 0 to 8 for 9 point calibration, 0 to 4 for 5 point calibration |
| currentPoint | [Point](#Skyle-Point) |  | 2D point with coordinates |






<a name="Skyle-CalibQuality"></a>

### CalibQuality
Message describing the quality of a calibration


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| quality | [double](#double) |  | Overall quality: 1 is worst, 5 is best |
| qualities | [double](#double) | repeated | List of quality per calibration point: 1 is worst, 5 is best |






<a name="Skyle-DeviceVersions"></a>

### DeviceVersions
Message containing all build versions


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| firmware | [string](#string) |  | Version of the firmware |
| eyetracker | [string](#string) |  | Version of the eye tracking software |
| calib | [string](#string) |  | Version of the calibration software |
| base | [string](#string) |  | Version of the base system |
| serial | [uint64](#uint64) |  | Unique serial of this device |
| skyleType | [int32](#int32) |  | Product type: 4 means iPad version, 1 means developer or windows version |
| isDemo | [bool](#bool) |  | Indicator if this is a demo device |






<a name="Skyle-FilterOptions"></a>

### FilterOptions
Filter configuration message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| fixationFilter | [int32](#int32) |  | Filter for fixations. range is 3 to 33 (3 high speed, less filtering and 33 low speed, hard filtering) |
| gazeFilter | [int32](#int32) |  | Filter for gaze. range is 3 to 33 (3 high speed, less filtering and 33 low speed, hard filtering) |






<a name="Skyle-IPadOptions"></a>

### IPadOptions
iPad Option message for configuration


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| isOldiOS | [bool](#bool) |  | Set this to true if iOS 13 to 13.3 is used, otherwise false (&gt;= 13.4) |
| isNotZoomed | [bool](#bool) |  | Set this to true if screen zoom is not enabled. It is recommended to use zoom! |
| model | [IPadOptions.iPadModel](#Skyle-IPadOptions-iPadModel) |  |  |






<a name="Skyle-OptionMessage"></a>

### OptionMessage
Message to wrap the options message: either empty or filled with options


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| empty | [google.protobuf.Empty](#google-protobuf-Empty) |  | Empty message |
| options | [Options](#Skyle-Options) |  | Options |






<a name="Skyle-Options"></a>

### Options
Option message for configuration


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| stream | [bool](#bool) |  | Turn on an image stream @ http:// skyle.local:8080 |
| enablePause | [bool](#bool) |  | Allow pause by API or by looking into the camera for 5 seconds |
| pause | [bool](#bool) |  | Pause the eye tracker - enablePause needs to be true |
| guidance | [bool](#bool) |  | Deprecated: stream a positioning stream instead of an image stream (DO NOT USE) |
| enableStandby | [bool](#bool) |  | Enable standby mode if the host (iPad) is not reachable / turned off |
| disableMouse | [bool](#bool) |  | Disable mouse on windows or testing systems |
| filter | [FilterOptions](#Skyle-FilterOptions) |  | Filter options for high skilled users, leave empty if skill is not high! |
| iPadOptions | [IPadOptions](#Skyle-IPadOptions) |  | Optional iPad Pro Settings, leave empty when unused / not sending |
| res | [ScreenResolution](#Skyle-ScreenResolution) |  | Screen resolution of the client: set this to the native client resolution (if unset, internal resolutions will be used) |
| hp | [bool](#bool) |  | Reserved bool (DO NOT USE) |
| eyeUsage | [Options.eyeUse](#Skyle-Options-eyeUse) |  | Select which eyes to track and to use for gaze (default: both) |






<a name="Skyle-Point"></a>

### Point
Message for a 2D point


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| x | [double](#double) |  | Precise X value |
| y | [double](#double) |  | Precise Y value |






<a name="Skyle-PositioningMessage"></a>

### PositioningMessage
Message with eye positions and quality indicators


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| leftEye | [Point](#Skyle-Point) |  | 2D position of the left eye |
| rightEye | [Point](#Skyle-Point) |  | 2D position of the right eye |
| distanceQuality | [int32](#int32) |  | Quality indicator for depth positioning. range is -50 to &#43;50. 0 is the best, -50 to far away and 50 to close |
| positioningQuality | [int32](#int32) |  | Quality indicator for overall horizontal and vertical positioning : range is -50 to &#43;50. 0 is the best |
| horizontalQuality | [int32](#int32) |  | Quality indicator for horizontal positioning. range is -50 to &#43;50. 0 is the best, -50 to far left and 50 to far right |
| verticalQuality | [int32](#int32) |  | Quality indicator for vertical positioning. range is -50 to &#43;50. 0 is the best, -50 to far down and 50 to far up |






<a name="Skyle-Profile"></a>

### Profile
Message describing a user profile


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| id | [int32](#int32) |  | Unique ID for a user (on this eye tracker) |
| name | [string](#string) |  | Name or nickname for the profile |
| skill | [Profile.Skill](#Skyle-Profile-Skill) |  | Skill of user |






<a name="Skyle-RawImage"></a>

### RawImage
Single image in grayscale raw bytes


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| width | [int32](#int32) |  | pixel width |
| height | [int32](#int32) |  | pixel height |
| data | [bytes](#bytes) |  | bytes of image |






<a name="Skyle-ResetMessage"></a>

### ResetMessage
Message to request resets


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| services | [bool](#bool) |  | restart services (including gRPC server) |
| device | [bool](#bool) |  | restart the whole device (takes up to 30 secs) |
| data | [bool](#bool) |  | reset saved user data and calibs. WARNING! ONLY DO THIS WHEN YOU REALLY WANT TO DELETE ALL USER DATA! |






<a name="Skyle-ScreenResolution"></a>

### ScreenResolution
Message with screen resolution of the client


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| width | [int32](#int32) |  | Width in pixel |
| height | [int32](#int32) |  | Height in pixel |
| widthInMM | [int32](#int32) |  | Width in mm |
| heightInMM | [int32](#int32) |  | Height in mm |






<a name="Skyle-StatusMessage"></a>

### StatusMessage
General status message


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| success | [bool](#bool) |  | True on success, false on failure |






<a name="Skyle-TriggerMessage"></a>

### TriggerMessage
Message to indicate a trigger


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| singleClick | [bool](#bool) |  | indicates single click on attached button |
| doubleClick | [bool](#bool) |  | indicates double click on attached button |
| holdClick | [bool](#bool) |  | indicates that attached button is constantly pushed |
| fixation | [bool](#bool) |  | indicates that a user is fixating a point |






<a name="Skyle-calibControlMessages"></a>

### calibControlMessages
Message wrapping possible calibration control messages for a client


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| calibControl | [CalibControl](#Skyle-CalibControl) |  | Message describing the calibration status |
| calibImprove | [CalibImprove](#Skyle-CalibImprove) |  | Message to improve a calibration |
| calibConfirm | [CalibConfirm](#Skyle-CalibConfirm) |  | Message to confirm this point on a step by step calib |






<a name="Skyle-calibCursorMessages"></a>

### calibCursorMessages
Message wrapping possible cursor calibration messages for a client


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| empty | [google.protobuf.Empty](#google-protobuf-Empty) |  | Empty message (start) |
| calibConfirm | [CalibConfirm](#Skyle-CalibConfirm) |  | Message to confirm the next point |





 


<a name="Skyle-IPadOptions-iPadModel"></a>

### IPadOptions.iPadModel
Set this to the iPad model you are using. If the device isn&#39;t an iPad, this value will be ignored.

| Name | Number | Description |
| ---- | ------ | ----------- |
| iPad8_5 | 0 | iPad Pro (12.9-inch) (3rd generation) |
| iPad8_6 | 1 | iPad Pro (12.9-inch) (3rd generation) |
| iPad8_7 | 2 | iPad Pro (12.9-inch) (3rd generation) |
| iPad8_8 | 3 | iPad Pro (12.9-inch) (3rd generation) |
| iPad8_11 | 4 | iPad Pro (12.9-inch) (4th generation) |
| iPad8_12 | 5 | iPad Pro (12.9-inch) (4th generation) |
| iPad13_1 | 6 | iPad Air (4th generation) |
| iPad13_2 | 7 | iPad Air (4th generation) |
| iPad13_8 | 8 | iPad Pro (12.9-inch) (5th generation) |
| iPad13_9 | 9 | iPad Pro (12.9-inch) (5th generation) |
| iPad13_10 | 10 | iPad Pro (12.9-inch) (5th generation) |
| iPad13_11 | 11 | iPad Pro (12.9-inch) (5th generation) |
| iPad13_16 | 12 | iPad Air (5th generation) |
| iPad13_17 | 13 | iPad Air (5th generation) |



<a name="Skyle-Options-eyeUse"></a>

### Options.eyeUse


| Name | Number | Description |
| ---- | ------ | ----------- |
| both | 0 | Both eyes (default) |
| left | 1 | Only left eye |
| right | 2 | Only right eye |



<a name="Skyle-Profile-Skill"></a>

### Profile.Skill


| Name | Number | Description |
| ---- | ------ | ----------- |
| low | 0 | User is unpractised and has maybe cognitive impairment. this will cause the eye tracker to filter gaze data harder (less precision) |
| medium | 1 | User that understands the operation. Default filtering will take place |
| high | 2 | User that is experienced with eye tracking and wants to control the filtering himself |


 

 


<a name="Skyle-Skyle"></a>

### Skyle
Skyle service to use the eye tracker

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| Calibrate | [calibControlMessages](#Skyle-calibControlMessages) stream | [CalibMessages](#Skyle-CalibMessages) stream | Used to calibrate for the current user. Streams in both directions with given message types. Client needs to close the stream when done |
| Positioning | [.google.protobuf.Empty](#google-protobuf-Empty) | [PositioningMessage](#Skyle-PositioningMessage) stream | Subscribe a stream sending eye positions and quality indicators to achieve good positioning of a user. Client needs to close the stream when done |
| Gaze | [.google.protobuf.Empty](#google-protobuf-Empty) | [Point](#Skyle-Point) stream | Subscribe a gaze stream, that sends coordinates of the current user gaze on a screen. Client needs to close the stream when done |
| Trigger | [.google.protobuf.Empty](#google-protobuf-Empty) | [TriggerMessage](#Skyle-TriggerMessage) stream | Subscribe a trigger stream, that sends trigger messages, when a user fixates a point or clicks. Client needs to close the stream when done |
| GetButton | [.google.protobuf.Empty](#google-protobuf-Empty) | [Button](#Skyle-Button) | Unary call to get the button status |
| SetButton | [ButtonActions](#Skyle-ButtonActions) | [ButtonActions](#Skyle-ButtonActions) | Unary call to configure the button actions, answers with the resulting configuration |
| Configure | [OptionMessage](#Skyle-OptionMessage) | [Options](#Skyle-Options) | Unary call to get (OptionMessage -&gt; empty) or set options (OptionMessage -&gt; Options). Answers with the resulting options. Options are saved to the current user profile |
| GetVersions | [.google.protobuf.Empty](#google-protobuf-Empty) | [DeviceVersions](#Skyle-DeviceVersions) | Unary call to get software versions |
| GetProfiles | [.google.protobuf.Empty](#google-protobuf-Empty) | [Profile](#Skyle-Profile) stream | Subscribe a profile stream of all available profiles. Host ends stream when all results are sent |
| CurrentProfile | [.google.protobuf.Empty](#google-protobuf-Empty) | [Profile](#Skyle-Profile) | Unary call to get the current profile |
| SetProfile | [Profile](#Skyle-Profile) | [StatusMessage](#Skyle-StatusMessage) | Unary call to set or create a profile. Answers with a status message (success or failure) |
| DeleteProfile | [Profile](#Skyle-Profile) | [StatusMessage](#Skyle-StatusMessage) | Unary call to delete a profile. Answers with a status message (success or failure) |
| Reset | [ResetMessage](#Skyle-ResetMessage) | [StatusMessage](#Skyle-StatusMessage) | Unary call to reset specific parts |
| CursorCalibration | [calibCursorMessages](#Skyle-calibCursorMessages) stream | [Point](#Skyle-Point) stream | Used to calibrate / test cursor. Streams in both directions with given message types. Client needs to close the stream when done |
| RawImages | [.google.protobuf.Empty](#google-protobuf-Empty) | [RawImage](#Skyle-RawImage) stream | Subscribe a raw image stream that sends unencoded frames. Client needs to close the stream when done |
| RawBinocularGaze | [.google.protobuf.Empty](#google-protobuf-Empty) | [BinocularGaze](#Skyle-BinocularGaze) stream | Subscribe a unfiltered binocular gaze stream, that sends coordinates of the current user gaze per eye. Client needs to close the stream when done |

 



## Scalar Value Types

| .proto Type | Notes | C++ | Java | Python | Go | C# | PHP | Ruby |
| ----------- | ----- | --- | ---- | ------ | -- | -- | --- | ---- |
| <a name="double" /> double |  | double | double | float | float64 | double | float | Float |
| <a name="float" /> float |  | float | float | float | float32 | float | float | Float |
| <a name="int32" /> int32 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint32 instead. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="int64" /> int64 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint64 instead. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="uint32" /> uint32 | Uses variable-length encoding. | uint32 | int | int/long | uint32 | uint | integer | Bignum or Fixnum (as required) |
| <a name="uint64" /> uint64 | Uses variable-length encoding. | uint64 | long | int/long | uint64 | ulong | integer/string | Bignum or Fixnum (as required) |
| <a name="sint32" /> sint32 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int32s. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="sint64" /> sint64 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int64s. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="fixed32" /> fixed32 | Always four bytes. More efficient than uint32 if values are often greater than 2^28. | uint32 | int | int | uint32 | uint | integer | Bignum or Fixnum (as required) |
| <a name="fixed64" /> fixed64 | Always eight bytes. More efficient than uint64 if values are often greater than 2^56. | uint64 | long | int/long | uint64 | ulong | integer/string | Bignum |
| <a name="sfixed32" /> sfixed32 | Always four bytes. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="sfixed64" /> sfixed64 | Always eight bytes. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="bool" /> bool |  | bool | boolean | boolean | bool | bool | boolean | TrueClass/FalseClass |
| <a name="string" /> string | A string must always contain UTF-8 encoded or 7-bit ASCII text. | string | String | str/unicode | string | string | string | String (UTF-8) |
| <a name="bytes" /> bytes | May contain any arbitrary sequence of bytes. | string | ByteString | str | []byte | ByteString | string | String (ASCII-8BIT) |

