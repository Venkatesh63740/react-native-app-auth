<activity
    android:name=".MainActivity"
    android:label="@string/app_name"
    android:exported="true"
    android:configChanges="keyboard|keyboardHidden|orientation|screenSize|uiMode"
    android:launchMode="singleTask"
    android:windowSoftInputMode="adjustResize">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>

<activity
    android:name="net.openid.appauth.AuthorizationManagementActivity"
   >
    <intent-filter >
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="com.example.appname" android:host="callback" />
    </intent-filter>
</activity>
build.gradle:
manifestPlaceholders = [appAuthRedirectScheme: "com.example.appname"]

my config:
{
"additionalParameters": {
"grant_type": "authorization_code"
},
"clientId": "{clientid}",
"clientSecret": "{secretkey}",
"issuer": "https://{myoktasiteurl}/oauth2/default",
"redirectUrl": "com.example.appname:/callback",
"responseTypes": "code",
"scopes": [
"openid",
"profile",
"offline_access"
],
"serviceConfiguration": {
"authorizationEndpoint": "https://{myoktasiteurl}/oauth2/default/v1/authorize",
"endSessionEndpoint": "https:/{myoktasiteurl}/oauth2/default/v1/logout",
"tokenEndpoint": "https://{myoktasiteurl}/oauth2/default/v1/token"
},
"useNonce": false,
"usePKCE": true
}

working fine in iOS but android, it was not redirecting to my app after the login and after while login the okta site from the app if we close and open the app it shows {"nativeStackAndroid":[],"userInfo":null,"message":"User cancelled flow","code":"authentication_error"}

This is iOS config:

CFBundleURLName $(PRODUCT_BUNDLE_IDENTIFIER) CFBundleURLSchemes {myoktasiteurl}
