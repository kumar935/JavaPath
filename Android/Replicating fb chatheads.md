## Replicating FB chatheads

- This [SO link](http://stackoverflow.com/questions/15975988/what-apis-in-android-is-facebook-using-to-create-chat-heads) which led to [this](http://www.piwai.info/chatheads-basics/#AndroidHead) seems interesting. But using just like that doesn't seem to be working. So now exploring android's windowManager from this [SO link](http://stackoverflow.com/questions/19846541/what-is-windowmanager-in-android).
  - wasn't working because forgot to add service in `AndroidManifest.xml` like this: <br/>
    ```
    <service android:enabled="true" android:name=".ChatHeadService" />
    ```
