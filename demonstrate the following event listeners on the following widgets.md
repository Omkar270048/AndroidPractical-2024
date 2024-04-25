# Create an android application to demonstrate the following event listeners on the following widgets Button: on click listener, long click listener Image: Touch listener with these motion events =>Action up, action down and action pointer down Edit Text : key listener on Enter key The Appropriate message should be displayed in text view.

main_activity.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Button" />
    <ImageView
        android:id="@+id/imageView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:srcCompat="@drawable/ic_launcher_background" />

    <EditText
        android:id="@+id/editText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:ems="10"
        android:inputType="textPersonName"
        android:text="Name" />

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!"/>
    
</LinearLayout>
```

mainActivity.java
```java

package com.client.eventlisteners;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.KeyEvent;
import android.view.MotionEvent;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ImageView;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    private TextView textView;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Initialize views
        Button button = findViewById(R.id.button);
        ImageView imageView = findViewById(R.id.imageView);
        EditText editText = findViewById(R.id.editText);
        textView = findViewById(R.id.textView);

        // Button click listener
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                textView.setText("Button clicked");
            }
        });

        // Button long click listener
        button.setOnLongClickListener(new View.OnLongClickListener() {
            @Override
            public boolean onLongClick(View v) {
                textView.setText("Button long clicked");
                return true;
            }
        });

        // Image touch listener
        imageView.setOnTouchListener(new View.OnTouchListener() {
            @Override
            public boolean onTouch(View v, MotionEvent event) {
                switch (event.getAction()) {
                    case MotionEvent.ACTION_DOWN:
                        textView.setText("Image: Action Down");
                        break;
                    case MotionEvent.ACTION_UP:
                        textView.setText("Image: Action Up");
                        break;
                    case MotionEvent.ACTION_POINTER_DOWN:
                        textView.setText("Image: Action Pointer Down");
                        break;
                }
                return true;
            }
        });

        // EditText key listener
        editText.setOnKeyListener(new View.OnKeyListener() {
            @Override
            public boolean onKey(View v, int keyCode, KeyEvent event) {
                if ((event.getAction() == KeyEvent.ACTION_DOWN) && (keyCode == KeyEvent.KEYCODE_ENTER)) {
                    textView.setText("Enter key pressed");
                    return true;
                }
                return false;
            }
        });
    }
}
```
