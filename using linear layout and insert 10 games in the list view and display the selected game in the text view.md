# using linear layout and insert 10 games in the list

```java
package com.client.insert10game;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.ListView;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    private ListView gamesListView;
    private TextView selectedGameTextView;

    private String[] games = {
            "Game 1", "Game 2", "Game 3", "Game 4", "Game 5",
            "Game 6", "Game 7", "Game 8", "Game 9", "Game 10"
    };
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        gamesListView = findViewById(R.id.gamesListView);
        selectedGameTextView = findViewById(R.id.selectedGameTextView);

        ArrayAdapter<String> adapter = new ArrayAdapter<>(this, android.R.layout.simple_list_item_1, games);
        gamesListView.setAdapter(adapter);

        gamesListView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                String selectedGame = games[position];
                selectedGameTextView.setText("Selected Game: " + selectedGame);
            }
        });
    }
}
```
