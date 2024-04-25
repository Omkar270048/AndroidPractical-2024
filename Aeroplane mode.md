# Create an  android  application  which  automatically  notify  the  user  when
Aeroplane mode is turned on or off using broadcast receiver.


manifest
```xml
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>
<uses-permission android:name="android.permission.READ_PHONE_STATE"/>
```

manifest
```xml
<receiver android:name=".AirplaneModeReceiver" android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.AIRPLANE_MODE"/>
            </intent-filter>
</receiver>
```

mainActivity.java
```java
package com.client.aeroplanemode;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;

import androidx.appcompat.app.AppCompatActivity;
import android.content.IntentFilter;
import android.os.Bundle;

public class MainActivity extends AppCompatActivity {

    private AirplaneModeReceiver airplaneModeReceiver;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Initialize the receiver
        airplaneModeReceiver = new AirplaneModeReceiver();
    }

    @Override
    protected void onStart() {
        super.onStart();
        // Register the receiver when the activity starts
        IntentFilter filter = new IntentFilter(Intent.ACTION_AIRPLANE_MODE_CHANGED);
        registerReceiver(airplaneModeReceiver, filter);
    }

    @Override
    protected void onStop() {
        super.onStop();
        // Unregister the receiver when the activity stops
        unregisterReceiver(airplaneModeReceiver);
    }
}

```
AirplaneModeReceiver.java
```java
package com.client.aeroplanemode;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.widget.Toast;

public class AirplaneModeReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        if (intent.getAction().equals(Intent.ACTION_AIRPLANE_MODE_CHANGED)) {
            boolean isAirplaneModeOn = intent.getBooleanExtra("state", false);
            if (isAirplaneModeOn) {
                // Airplane mode turned on
                Toast.makeText(context, "Airplane mode turned on", Toast.LENGTH_SHORT).show();
            } else {
                // Airplane mode turned off
                Toast.makeText(context, "Airplane mode turned off", Toast.LENGTH_SHORT).show();
            }
        }
    }
}


```
