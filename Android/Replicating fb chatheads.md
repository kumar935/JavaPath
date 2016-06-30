## Replicating FB chatheads

- This [SO link](http://stackoverflow.com/questions/15975988/what-apis-in-android-is-facebook-using-to-create-chat-heads) which led to [this](http://www.piwai.info/chatheads-basics/#AndroidHead) seems interesting. But using just like that doesn't seem to be working. So now exploring android's windowManager from this [SO link](http://stackoverflow.com/questions/19846541/what-is-windowmanager-in-android).
  - wasn't working because forgot to add service in `AndroidManifest.xml` like this: <br/>
    ```
    <service android:enabled="true" android:name=".ChatHeadService" />
    ```
- Floating icon like fb chathead done, but how to open the whole app in a floating container? Maybe if I open the fragment inside a view that I added in the floating window: [SO link](http://stackoverflow.com/questions/5159982/how-do-i-add-a-fragment-to-an-activity-with-a-programmatically-created-content-v)
  - When it won't let me set Id to my dynamically added frameLayout: [SO link](http://stackoverflow.com/questions/8460680/how-can-i-assign-an-id-to-a-view-programmatically), <- have to make separate resource file for ids.
