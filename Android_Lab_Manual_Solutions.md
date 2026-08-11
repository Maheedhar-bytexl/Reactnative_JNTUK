# Android Development Lab Manual — Solutions
### Diploma | JNTUK | List of Exercises

Each exercise below is a **separate, standalone mini-project** — create a new **Empty Views Activity** project (Language: **Java**) for each one, unless the exercise says otherwise. Every program uses only `MainActivity.java` + `activity_main.xml` unless a second Activity is needed.

---

## 1. Display "Hello World"

**`activity_main.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:text="Hello World!"
        android:textSize="24sp" />

</RelativeLayout>
```

**`MainActivity.java`**
```java
package com.example.helloworld;

import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```
**Output:** Screen shows "Hello World!" centered.

---

## 2. Display a Toast Message

**`activity_main.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center">

    <Button
        android:id="@+id/btnShowToast"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Show Toast" />

</LinearLayout>
```

**`MainActivity.java`**
```java
package com.example.toastdemo;

import android.os.Bundle;
import android.widget.Button;
import android.widget.Toast;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button btnShowToast = findViewById(R.id.btnShowToast);
        btnShowToast.setOnClickListener(v ->
                Toast.makeText(this, "This is a Toast message!", Toast.LENGTH_SHORT).show());
    }
}
```
**Output:** Tapping the button shows a short popup message at the bottom of the screen.

---

## 3. Factorial of a Number (EditText + Button + Toast)

**`activity_main.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <EditText
        android:id="@+id/etNumber"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter a number"
        android:inputType="number" />

    <Button
        android:id="@+id/btnFactorial"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:text="Find Factorial" />

</LinearLayout>
```

**`MainActivity.java`**
```java
package com.example.factorialdemo;

import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        EditText etNumber = findViewById(R.id.etNumber);
        Button btnFactorial = findViewById(R.id.btnFactorial);

        btnFactorial.setOnClickListener(v -> {
            String input = etNumber.getText().toString();
            if (input.isEmpty()) {
                Toast.makeText(this, "Please enter a number", Toast.LENGTH_SHORT).show();
                return;
            }
            int number = Integer.parseInt(input);
            long factorial = 1;
            for (int i = 1; i <= number; i++) {
                factorial *= i;
            }
            Toast.makeText(this, "Factorial of " + number + " = " + factorial, Toast.LENGTH_LONG).show();
        });
    }
}
```
**Output:** Entering `5` and tapping the button shows "Factorial of 5 = 120".

---

## 4. Check Box Widget

**`activity_main.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Select your hobbies:" />

    <CheckBox
        android:id="@+id/cbReading"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Reading" />

    <CheckBox
        android:id="@+id/cbMusic"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Music" />

    <CheckBox
        android:id="@+id/cbSports"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Sports" />

    <Button
        android:id="@+id/btnSubmit"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:text="Submit" />

</LinearLayout>
```

**`MainActivity.java`**
```java
package com.example.checkboxdemo;

import android.os.Bundle;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.Toast;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        CheckBox cbReading = findViewById(R.id.cbReading);
        CheckBox cbMusic = findViewById(R.id.cbMusic);
        CheckBox cbSports = findViewById(R.id.cbSports);
        Button btnSubmit = findViewById(R.id.btnSubmit);

        btnSubmit.setOnClickListener(v -> {
            StringBuilder result = new StringBuilder("Selected: ");
            if (cbReading.isChecked()) result.append("Reading ");
            if (cbMusic.isChecked()) result.append("Music ");
            if (cbSports.isChecked()) result.append("Sports ");
            Toast.makeText(this, result.toString(), Toast.LENGTH_LONG).show();
        });
    }
}
```
**Output:** Checking "Reading" and "Sports", then tapping Submit shows "Selected: Reading Sports".

---

## 5. Spinner (Combo Box) Widget

**`activity_main.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Select your branch:" />

    <Spinner
        android:id="@+id/spinnerBranch"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />

    <TextView
        android:id="@+id/tvSelected"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:textSize="16sp" />

</LinearLayout>
```

**`MainActivity.java`**
```java
package com.example.spinnerdemo;

import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.Spinner;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Spinner spinnerBranch = findViewById(R.id.spinnerBranch);
        TextView tvSelected = findViewById(R.id.tvSelected);

        String[] branches = {"CSE", "ECE", "MECH", "CIVIL", "EEE"};
        ArrayAdapter<String> adapter = new ArrayAdapter<>(this,
                android.R.layout.simple_spinner_dropdown_item, branches);
        spinnerBranch.setAdapter(adapter);

        spinnerBranch.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
            @Override
            public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
                tvSelected.setText("You selected: " + branches[position]);
            }

            @Override
            public void onNothingSelected(AdapterView<?> parent) { }
        });
    }
}
```
**Output:** Selecting "ECE" from the dropdown shows "You selected: ECE" below it.

---

## 6. Date Picker and Time Picker Widgets

**`activity_main.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <Button
        android:id="@+id/btnPickDate"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Pick Date" />

    <TextView
        android:id="@+id/tvDate"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="20dp" />

    <Button
        android:id="@+id/btnPickTime"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Pick Time" />

    <TextView
        android:id="@+id/tvTime"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />

</LinearLayout>
```

**`MainActivity.java`**
```java
package com.example.datetimedemo;

import android.app.DatePickerDialog;
import android.app.TimePickerDialog;
import android.os.Bundle;
import android.widget.Button;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;
import java.util.Calendar;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button btnPickDate = findViewById(R.id.btnPickDate);
        TextView tvDate = findViewById(R.id.tvDate);
        Button btnPickTime = findViewById(R.id.btnPickTime);
        TextView tvTime = findViewById(R.id.tvTime);

        Calendar calendar = Calendar.getInstance();

        btnPickDate.setOnClickListener(v -> {
            new DatePickerDialog(this, (view, year, month, day) ->
                    tvDate.setText("Selected Date: " + day + "/" + (month + 1) + "/" + year),
                    calendar.get(Calendar.YEAR),
                    calendar.get(Calendar.MONTH),
                    calendar.get(Calendar.DAY_OF_MONTH)).show();
        });

        btnPickTime.setOnClickListener(v -> {
            new TimePickerDialog(this, (view, hour, minute) ->
                    tvTime.setText("Selected Time: " + hour + ":" + minute),
                    calendar.get(Calendar.HOUR_OF_DAY),
                    calendar.get(Calendar.MINUTE), true).show();
        });
    }
}
```
**Output:** Tapping "Pick Date"/"Pick Time" opens the respective picker dialog; the chosen value is displayed below the button.

---

## 7. Multiple UI Controls Together (EditText, CheckBox, Spinner, Buttons)

**`activity_main.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <EditText
        android:id="@+id/etName"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter your name" />

    <CheckBox
        android:id="@+id/cbSubscribe"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Subscribe to newsletter" />

    <Spinner
        android:id="@+id/spinnerCity"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />

    <Button
        android:id="@+id/btnRegister"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:text="Register" />

</LinearLayout>
```

**`MainActivity.java`**
```java
package com.example.multiuidemo;

import android.os.Bundle;
import android.widget.*;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        EditText etName = findViewById(R.id.etName);
        CheckBox cbSubscribe = findViewById(R.id.cbSubscribe);
        Spinner spinnerCity = findViewById(R.id.spinnerCity);
        Button btnRegister = findViewById(R.id.btnRegister);

        String[] cities = {"Vijayawada", "Guntur", "Hyderabad", "Visakhapatnam"};
        spinnerCity.setAdapter(new ArrayAdapter<>(this,
                android.R.layout.simple_spinner_dropdown_item, cities));

        btnRegister.setOnClickListener(v -> {
            String name = etName.getText().toString();
            boolean subscribed = cbSubscribe.isChecked();
            String city = spinnerCity.getSelectedItem().toString();

            String message = "Name: " + name +
                    "\nCity: " + city +
                    "\nSubscribed: " + subscribed;
            Toast.makeText(this, message, Toast.LENGTH_LONG).show();
        });
    }
}
```
**Output:** Filling the form and tapping Register shows a summary Toast combining all four control values.

---

## 8. Navigate From One Activity to Another Using a Button

**`activity_main.xml`** (first screen)
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center">

    <Button
        android:id="@+id/btnGoToSecond"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Go to Second Activity" />

</LinearLayout>
```

**`activity_second.xml`** (second screen)
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="This is the Second Activity"
        android:textSize="20sp" />

</LinearLayout>
```

**`MainActivity.java`**
```java
package com.example.navigationdemo;

import android.content.Intent;
import android.os.Bundle;
import android.widget.Button;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button btnGoToSecond = findViewById(R.id.btnGoToSecond);
        btnGoToSecond.setOnClickListener(v -> {
            Intent intent = new Intent(MainActivity.this, SecondActivity.class);
            startActivity(intent);
        });
    }
}
```

**`SecondActivity.java`** *(File \u2192 New \u2192 Activity \u2192 Empty Views Activity, name it SecondActivity)*
```java
package com.example.navigationdemo;

import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;

public class SecondActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
    }
}
```
**Output:** Tapping the button on screen 1 opens screen 2. *(Android Studio auto-registers `SecondActivity` in the Manifest when created via the New Activity wizard — check `AndroidManifest.xml` if it doesn't.)*

---

## 9. Image Effects (Grayscale / Brightness using ColorMatrix)

**`activity_main.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center">

    <ImageView
        android:id="@+id/imageView"
        android:layout_width="250dp"
        android:layout_height="250dp"
        android:src="@drawable/sample_image" />

    <Button
        android:id="@+id/btnGrayscale"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:text="Apply Grayscale" />

    <Button
        android:id="@+id/btnOriginal"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Reset to Original" />

</LinearLayout>
```
*(Add any image to `res/drawable/` and name it `sample_image.png` or `.jpg`.)*

**`MainActivity.java`**
```java
package com.example.imageeffectsdemo;

import android.graphics.ColorMatrix;
import android.graphics.ColorMatrixColorFilter;
import android.os.Bundle;
import android.widget.Button;
import android.widget.ImageView;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        ImageView imageView = findViewById(R.id.imageView);
        Button btnGrayscale = findViewById(R.id.btnGrayscale);
        Button btnOriginal = findViewById(R.id.btnOriginal);

        btnGrayscale.setOnClickListener(v -> {
            ColorMatrix matrix = new ColorMatrix();
            matrix.setSaturation(0); // 0 = grayscale, 1 = original colors
            imageView.setColorFilter(new ColorMatrixColorFilter(matrix));
        });

        btnOriginal.setOnClickListener(v -> imageView.clearColorFilter());
    }
}
```
**Output:** Tapping "Apply Grayscale" converts the image to black-and-white live; "Reset" restores original colors.

---

## 10. Image Switcher

**`activity_main.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center">

    <ImageSwitcher
        android:id="@+id/imageSwitcher"
        android:layout_width="250dp"
        android:layout_height="250dp" />

    <Button
        android:id="@+id/btnNext"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:text="Next Image" />

</LinearLayout>
```

**`MainActivity.java`**
```java
package com.example.imageswitcherdemo;

import android.os.Bundle;
import android.widget.Button;
import android.widget.ImageSwitcher;
import android.widget.ImageView;
import android.widget.ViewSwitcher;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private final int[] images = {
            android.R.drawable.ic_menu_gallery,
            android.R.drawable.ic_menu_camera,
            android.R.drawable.ic_menu_compass
    };
    private int currentIndex = 0;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        ImageSwitcher imageSwitcher = findViewById(R.id.imageSwitcher);
        imageSwitcher.setFactory(() -> {
            ImageView imageView = new ImageView(this);
            imageView.setScaleType(ImageView.ScaleType.FIT_CENTER);
            return imageView;
        });
        imageSwitcher.setImageResource(images[currentIndex]);

        Button btnNext = findViewById(R.id.btnNext);
        btnNext.setOnClickListener(v -> {
            currentIndex = (currentIndex + 1) % images.length;
            imageSwitcher.setImageResource(images[currentIndex]);
        });
    }
}
```
**Output:** Tapping "Next Image" animates a transition to the next image in the array. *(Uses built-in Android icons so it runs with zero extra drawables — swap in your own images from `res/drawable/` for the lab record.)*

---

## 11. Alert Dialog

**`activity_main.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center">

    <Button
        android:id="@+id/btnShowDialog"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Delete Item" />

</LinearLayout>
```

**`MainActivity.java`**
```java
package com.example.alertdialogdemo;

import android.app.AlertDialog;
import android.os.Bundle;
import android.widget.Button;
import android.widget.Toast;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Button btnShowDialog = findViewById(R.id.btnShowDialog);
        btnShowDialog.setOnClickListener(v -> {
            new AlertDialog.Builder(this)
                    .setTitle("Confirm Delete")
                    .setMessage("Are you sure you want to delete this item?")
                    .setPositiveButton("YES", (dialog, which) ->
                            Toast.makeText(this, "Item deleted", Toast.LENGTH_SHORT).show())
                    .setNegativeButton("NO", (dialog, which) -> dialog.dismiss())
                    .show();
        });
    }
}
```
**Output:** Tapping the button shows a Yes/No confirmation dialog.

---

## 12. Integrate Google Maps

**One-time setup (do this before writing code):**
1. Get a **Google Maps API key**: Google Cloud Console → create a project → enable "Maps SDK for Android" → generate an API key.
2. In `build.gradle (Module: app)`, add: `implementation 'com.google.android.gms:play-services-maps:18.2.0'`
3. In `AndroidManifest.xml`, inside `<application>`:
```xml
<meta-data
    android:name="com.google.android.geo.API_KEY"
    android:value="YOUR_API_KEY_HERE" />
```

**`activity_main.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<fragment xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/map"
    android:name="com.google.android.gms.maps.SupportMapFragment"
    android:layout_width="match_parent"
    android:layout_height="match_parent" />
```

**`MainActivity.java`**
```java
package com.example.mapsdemo;

import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;
import androidx.fragment.app.FragmentActivity;
import com.google.android.gms.maps.CameraUpdateFactory;
import com.google.android.gms.maps.GoogleMap;
import com.google.android.gms.maps.OnMapReadyCallback;
import com.google.android.gms.maps.SupportMapFragment;
import com.google.android.gms.maps.model.LatLng;
import com.google.android.gms.maps.model.MarkerOptions;

public class MainActivity extends FragmentActivity implements OnMapReadyCallback {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        SupportMapFragment mapFragment = (SupportMapFragment)
                getSupportFragmentManager().findFragmentById(R.id.map);
        mapFragment.getMapAsync(this);
    }

    @Override
    public void onMapReady(GoogleMap googleMap) {
        LatLng collegeLocation = new LatLng(16.5062, 80.6480); // example: Vijayawada
        googleMap.addMarker(new MarkerOptions().position(collegeLocation).title("My College"));
        googleMap.moveCamera(CameraUpdateFactory.newLatLngZoom(collegeLocation, 12));
    }
}
```
**Output:** Shows an interactive Google Map centered on the given coordinates, with a marker. *(`MainActivity` must extend `FragmentActivity` — not `AppCompatActivity` — for `getSupportFragmentManager()` used this way; `AppCompatActivity` also works since it extends `FragmentActivity`, so either is fine.)*

---

## 13. Send SMS

**`AndroidManifest.xml`** — add before `<application>`:
```xml
<uses-permission android:name="android.permission.SEND_SMS" />
```

**`activity_main.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <EditText
        android:id="@+id/etPhoneNumber"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Phone Number"
        android:inputType="phone" />

    <EditText
        android:id="@+id/etMessage"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Message" />

    <Button
        android:id="@+id/btnSendSms"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:text="Send SMS" />

</LinearLayout>
```

**`MainActivity.java`**
```java
package com.example.smsdemo;

import android.Manifest;
import android.content.pm.PackageManager;
import android.os.Bundle;
import android.telephony.SmsManager;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

public class MainActivity extends AppCompatActivity {

    private static final int SMS_PERMISSION_CODE = 100;
    EditText etPhoneNumber, etMessage;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        etPhoneNumber = findViewById(R.id.etPhoneNumber);
        etMessage = findViewById(R.id.etMessage);
        Button btnSendSms = findViewById(R.id.btnSendSms);

        btnSendSms.setOnClickListener(v -> {
            if (ContextCompat.checkSelfPermission(this, Manifest.permission.SEND_SMS)
                    != PackageManager.PERMISSION_GRANTED) {
                ActivityCompat.requestPermissions(this,
                        new String[]{Manifest.permission.SEND_SMS}, SMS_PERMISSION_CODE);
            } else {
                sendSms();
            }
        });
    }

    private void sendSms() {
        String phoneNumber = etPhoneNumber.getText().toString();
        String message = etMessage.getText().toString();
        SmsManager smsManager = SmsManager.getDefault();
        smsManager.sendTextMessage(phoneNumber, null, message, null, null);
        Toast.makeText(this, "SMS sent", Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        if (requestCode == SMS_PERMISSION_CODE && grantResults.length > 0
                && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
            sendSms();
        } else {
            Toast.makeText(this, "SMS permission denied", Toast.LENGTH_SHORT).show();
        }
    }
}
```
**Output:** Sends an SMS directly from the app (asks for `SEND_SMS` permission the first time). **Only works on a real device with an active SIM — emulators cannot send real SMS.**

---

## 14. Calling a Number

**`AndroidManifest.xml`** — add:
```xml
<uses-permission android:name="android.permission.CALL_PHONE" />
```

**`activity_main.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <EditText
        android:id="@+id/etPhoneNumber"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Phone Number"
        android:inputType="phone" />

    <Button
        android:id="@+id/btnCall"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:text="Call" />

</LinearLayout>
```

**`MainActivity.java`**
```java
package com.example.calldemo;

import android.Manifest;
import android.content.Intent;
import android.content.pm.PackageManager;
import android.net.Uri;
import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

public class MainActivity extends AppCompatActivity {

    private static final int CALL_PERMISSION_CODE = 101;
    EditText etPhoneNumber;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        etPhoneNumber = findViewById(R.id.etPhoneNumber);
        Button btnCall = findViewById(R.id.btnCall);

        btnCall.setOnClickListener(v -> {
            if (ContextCompat.checkSelfPermission(this, Manifest.permission.CALL_PHONE)
                    != PackageManager.PERMISSION_GRANTED) {
                ActivityCompat.requestPermissions(this,
                        new String[]{Manifest.permission.CALL_PHONE}, CALL_PERMISSION_CODE);
            } else {
                makeCall();
            }
        });
    }

    private void makeCall() {
        String phoneNumber = etPhoneNumber.getText().toString();
        Intent callIntent = new Intent(Intent.ACTION_CALL);
        callIntent.setData(Uri.parse("tel:" + phoneNumber));
        startActivity(callIntent);
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        if (requestCode == CALL_PERMISSION_CODE && grantResults.length > 0
                && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
            makeCall();
        }
    }
}
```
**Output:** Dials and initiates a call directly to the entered number. *(For a safer classroom demo without the `CALL_PHONE` permission, swap `ACTION_CALL` for `ACTION_DIAL` — it just opens the dialer pre-filled instead of calling immediately.)*

---

## 15. Send E-mail

**`activity_main.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <EditText
        android:id="@+id/etEmail"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Recipient Email"
        android:inputType="textEmailAddress" />

    <EditText
        android:id="@+id/etSubject"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Subject" />

    <EditText
        android:id="@+id/etBody"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Message" />

    <Button
        android:id="@+id/btnSendEmail"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:text="Send Email" />

</LinearLayout>
```

**`MainActivity.java`**
```java
package com.example.emaildemo;

import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        EditText etEmail = findViewById(R.id.etEmail);
        EditText etSubject = findViewById(R.id.etSubject);
        EditText etBody = findViewById(R.id.etBody);
        Button btnSendEmail = findViewById(R.id.btnSendEmail);

        btnSendEmail.setOnClickListener(v -> {
            Intent emailIntent = new Intent(Intent.ACTION_SENDTO);
            emailIntent.setData(Uri.parse("mailto:"));
            emailIntent.putExtra(Intent.EXTRA_EMAIL, new String[]{etEmail.getText().toString()});
            emailIntent.putExtra(Intent.EXTRA_SUBJECT, etSubject.getText().toString());
            emailIntent.putExtra(Intent.EXTRA_TEXT, etBody.getText().toString());
            startActivity(Intent.createChooser(emailIntent, "Send Email using:"));
        });
    }
}
```
**Output:** Opens an email app (Gmail etc.) with recipient, subject, and body pre-filled. No special permission needed — this hands off to another app rather than sending directly.

---

## 16. Using Database (SQLite)

**`activity_main.xml`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <EditText
        android:id="@+id/etNote"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter a note" />

    <Button
        android:id="@+id/btnAddNote"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="10dp"
        android:text="Add Note" />

    <ListView
        android:id="@+id/lvNotes"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_marginTop="16dp" />

</LinearLayout>
```

**`NotesDbHelper.java`**
```java
package com.example.databasedemo;

import android.content.ContentValues;
import android.content.Context;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;
import java.util.ArrayList;
import java.util.List;

public class NotesDbHelper extends SQLiteOpenHelper {

    public NotesDbHelper(Context context) {
        super(context, "notes.db", null, 1);
    }

    @Override
    public void onCreate(SQLiteDatabase db) {
        db.execSQL("CREATE TABLE notes (id INTEGER PRIMARY KEY AUTOINCREMENT, note TEXT)");
    }

    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
        db.execSQL("DROP TABLE IF EXISTS notes");
        onCreate(db);
    }

    public void addNote(String note) {
        SQLiteDatabase db = getWritableDatabase();
        ContentValues values = new ContentValues();
        values.put("note", note);
        db.insert("notes", null, values);
    }

    public List<String> getAllNotes() {
        List<String> notes = new ArrayList<>();
        SQLiteDatabase db = getReadableDatabase();
        Cursor cursor = db.query("notes", new String[]{"note"}, null, null, null, null, "id DESC");
        while (cursor.moveToNext()) {
            notes.add(cursor.getString(cursor.getColumnIndexOrThrow("note")));
        }
        cursor.close();
        return notes;
    }
}
```

**`MainActivity.java`**
```java
package com.example.databasedemo;

import android.os.Bundle;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ListView;
import androidx.appcompat.app.AppCompatActivity;
import java.util.List;

public class MainActivity extends AppCompatActivity {

    NotesDbHelper dbHelper;
    ArrayAdapter<String> adapter;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        dbHelper = new NotesDbHelper(this);
        EditText etNote = findViewById(R.id.etNote);
        Button btnAddNote = findViewById(R.id.btnAddNote);
        ListView lvNotes = findViewById(R.id.lvNotes);

        refreshList(lvNotes);

        btnAddNote.setOnClickListener(v -> {
            String note = etNote.getText().toString();
            if (!note.isEmpty()) {
                dbHelper.addNote(note);
                etNote.setText("");
                refreshList(lvNotes);
            }
        });
    }

    private void refreshList(ListView lvNotes) {
        List<String> notes = dbHelper.getAllNotes();
        adapter = new ArrayAdapter<>(this, android.R.layout.simple_list_item_1, notes);
        lvNotes.setAdapter(adapter);
    }
}
```
**Output:** Typing a note and tapping "Add Note" saves it to SQLite and immediately shows it in the list below — the list still shows all notes even after closing and reopening the app.

---

## 17. Publish Android Application

Already covered in full in **Unit 5, section 5.8**. Quick recap:
1. **Build → Generate Signed Bundle / APK**
2. Choose **APK** or **Android App Bundle (AAB)**
3. Create/select a **Keystore** (signing key)
4. Choose **release** build type → triggers ProGuard/R8 optimization
5. Upload the resulting AAB to **Google Play Console** for public release

---

## 18. Deploy Android Application

Already covered in full in **Unit 1, section 1.9** and **Unit 5, section 5.8**. Quick recap:
1. Enable **Developer Options** + **USB Debugging** on the physical device
2. Connect via USB, accept the debugging prompt
3. Select the device in Android Studio → **Run ▶** (installs a debug build directly), **or**
4. Install a release APK manually via `adb install app-release.apk`

---

### Notes for the Lab Record

- Every exercise above uses **only Java + XML** — no third-party libraries except Exercise 12 (Google Maps), which needs the Play Services dependency and an API key as noted.
- Each exercise is written as its **own standalone project** (separate package name) so they can be submitted as 16 individual lab record entries, matching the syllabus list exactly.
- All permission-based exercises (13, 14) use the classic `ActivityCompat.requestPermissions()` + `onRequestPermissionsResult()` pattern, since that's what's most commonly expected in diploma practical exams — the same permission concept from Unit 4's `[EXAM FOCUS]` notes.
