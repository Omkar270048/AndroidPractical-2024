# Create an android application to generate two notifications, one notification will be non-clickable and another is clickable (it will reload the current application)

```java
package com.client.notification;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.NotificationCompat;
import android.app.NotificationChannel;
import android.app.NotificationManager;
import android.app.PendingIntent;
import android.content.Context;
import android.content.Intent;
import android.os.Build;
import android.os.Bundle;
import android.view.View;

public class MainActivity extends AppCompatActivity {
    private static final String CHANNEL_ID = "notification_channel";
    private static final int NOTIFICATION_ID_1 = 1;
    private static final int NOTIFICATION_ID_2 = 2;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    public void generateNotifications(View view) {
        switch (view.getId()) {
            case R.id.btn_generate_notification1:
                showNonClickableNotification();
                break;
            case R.id.btn_generate_notification2:
                showClickableNotification();
                break;
        }
    }

    private void showNonClickableNotification() {
        NotificationManager notificationManager = (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);

        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            NotificationChannel channel = new NotificationChannel(CHANNEL_ID, "Notification Channel", NotificationManager.IMPORTANCE_DEFAULT);
            notificationManager.createNotificationChannel(channel);
        }

        NotificationCompat.Builder builder = new NotificationCompat.Builder(this, CHANNEL_ID)
                .setSmallIcon(R.drawable.ic_notification)
                .setContentTitle("Non-clickable Notification")
                .setContentText("This is a non-clickable notification")
                .setAutoCancel(true);

        notificationManager.notify(NOTIFICATION_ID_1, builder.build());
    }

    private void showClickableNotification() {
        Intent intent = new Intent(this, MainActivity.class);
        intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
        PendingIntent pendingIntent = PendingIntent.getActivity(this, 0, intent, PendingIntent.FLAG_IMMUTABLE); // Specify FLAG_IMMUTABLE

        NotificationManager notificationManager = (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);

        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            NotificationChannel channel = new NotificationChannel(CHANNEL_ID, "Notification Channel", NotificationManager.IMPORTANCE_DEFAULT);
            notificationManager.createNotificationChannel(channel);
        }

        NotificationCompat.Builder builder = new NotificationCompat.Builder(this, CHANNEL_ID)
                .setSmallIcon(R.drawable.ic_notification)
                .setContentTitle("Clickable Notification")
                .setContentText("Click to reload the application")
                .setAutoCancel(true)
                .setContentIntent(pendingIntent);

        notificationManager.notify(NOTIFICATION_ID_2, builder.build());
    }

}

```

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">


    <Button
        android:id="@+id/btn_generate_notification1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Generate Non-clickable Notification"
        android:onClick="generateNotifications"
        android:layout_marginBottom="16dp"
        android:layout_alignParentTop="true"/>

    <Button
        android:id="@+id/btn_generate_notification2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Generate Clickable Notification"
        android:onClick="generateNotifications"
        android:layout_below="@id/btn_generate_notification1"/>
</RelativeLayout>
```
