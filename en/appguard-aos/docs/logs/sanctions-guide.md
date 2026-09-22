<!-- pre-align:aligned sig=fbe508816555 -->

# Guide to Sanctions

<a id="a-sanctioned-by-detection-log"></a>
## A. Sanctioned by Detection Log { #a-sanctioned-by-detection-log }

It is recommended to proceed with the sanction by combining detection logs via NHN AppGuard and multiple logs in the app itself.


<a id="b-register-the-callback-function-and-proceed-with-processing-from-the-server-side"></a>
## B. Register the callback function and proceed with processing from the server side { #b-register-the-callback-function-and-proceed-with-processing-from-the-server-side }

When registering the callback function, you get the detection result of NHN AppGuard (see [the Integrated API Calls](../sdk/java.md#callback-function-register)).

<a id="recommended-sanction-method"></a>
### Recommended Sanction Method { #recommended-sanction-method }

- **When blocked**: A method to transfer detected data to the server to end the connection on the server side is recommended.
- **Not recommended**: If terminated on the client, it is not recommended because it is more likely to bypass.

When blocked via the NHN AppGuard Block feature, the callback function is also called (see [5.2 Callback Data](callback-data.md)).

<a id="c-enable-nhn-appguard-blocking"></a>
## C. Enable NHN AppGuard Blocking { #c-enable-nhn-appguard-blocking }

You can make blocking settings from the web console.

![](../assets/images/logs/sanctions-console-settings.png)

<a id="full-block"></a>
### Full Block { #full-block }
When detected by **policies set to full block**:
- NHN AppGuard Guide appears
- the app is closed

<a id="conditional-block"></a>
### Conditional Block { #conditional-block }
If detected by **the condition you set when you blocked it**:
- NHN AppGuard Guide appears  
- App is terminated

<a id="d-enable-nhn-appguard-blacklist-feature"></a>
## D. Enable NHN AppGuard blacklist feature { #d-enable-nhn-appguard-blacklist-feature }

You can set up a blacklist in the web console.

![](../assets/images/logs/blacklist-settings.png)

When you run the app with a registered blacklist ID, the NHN AppGuard guide appears for the set blocking period and the app is closed.

Below is a dialog box that will appear if you are blocked:

![](../assets/images/logs/block-dialog.png)

!!! tip "Note"
    * The number before '\_' of the code value is the callback data value.
    * The guidance message is translated according to the language of each country and displayed.

---


