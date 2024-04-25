# Create an android application with customised appbar. Insert search and filebuttons in it and toast the appropriate message on clicking the buttons (add new color in color.xml and use that color for appbar).

drawable/res/colors
```xml
<resources>
    <color name="customColor">#FF5722</color>
</resources>
```

menifest
```xml
<application
...
android:theme="@style/Theme.AppCompat.Light.NoActionBar">

```

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <androidx.appcompat.widget.Toolbar
        android:id="@+id/toolbar"
        android:layout_width="match_parent"
        android:layout_height="?attr/actionBarSize"
        android:background="@color/customColor"
       >

        <!-- Add your buttons here -->
        <ImageButton
            android:id="@+id/search_button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:src="@drawable/ic_search"
            android:layout_alignParentStart="true"
            android:onClick="onSearchButtonClick" />

        <ImageButton
            android:id="@+id/file_button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:src="@drawable/ic_file"
            android:layout_alignParentEnd="true"
            android:onClick="onFileButtonClick" />

    </androidx.appcompat.widget.Toolbar>

</RelativeLayout>

```

```java
package com.client.appbar;

import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.widget.Toolbar;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Toolbar toolbar = findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);

    }

    public void onSearchButtonClick(View view) {
        Toast.makeText(this, "Search button clicked", Toast.LENGTH_SHORT).show();
        // Add your search functionality here
    }

    public void onFileButtonClick(View view) {
        Toast.makeText(this, "File button clicked", Toast.LENGTH_SHORT).show();
        // Add your file functionality here
    }
}
```

