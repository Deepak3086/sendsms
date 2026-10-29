# Ex.No: 3 Design an Android Application to Send SMS using Intent

## AIM
To create and design an Android application to send SMS using Intent using Android Studio.

## EQUIPMENTS REQUIRED
Android Studio (Latest Version)

## ALGORITHM

**Step 1:** Open Android Studio and then click on File -> New -> New Project.

**Step 2:** Then type the Application name as `smsintent` and click Next.

**Step 3:** Then select the Minimum SDK as shown below and click Next.

**Step 4:** Then select the Empty Activity and click Next. Finally click Finish.

**Step 5:** Design layout in `activity_main.xml`.

**Step 6:** Send SMS and display details given in the `MainActivity` file.

**Step 7:** Save and run the application.

## PROGRAM

```java
/*
Program to create and design an android application Send SMS using Intent.
Developed by:
Registration Number :
*/
```

### activity_main.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Send SMS using Intent"
        android:textSize="24sp"
        android:textStyle="bold"
        android:gravity="center"
        android:layout_marginBottom="20dp" />

    <EditText
        android:id="@+id/etPhone"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter phone number"
        android:inputType="phone" />

    <EditText
        android:id="@+id/etMessage"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter message"
        android:inputType="textMultiLine"
        android:minLines="3"
        android:gravity="top"
        android:layout_marginTop="10dp" />

    <Button
        android:id="@+id/btnSend"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Send SMS"
        android:layout_marginTop="20dp" />

</LinearLayout>
```

### MainActivity.java

```java
package com.example.smsintent;

import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    EditText etPhone, etMessage;
    Button btnSend;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        etPhone = findViewById(R.id.etPhone);
        etMessage = findViewById(R.id.etMessage);
        btnSend = findViewById(R.id.btnSend);

        btnSend.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String phone = etPhone.getText().toString().trim();
                String message = etMessage.getText().toString().trim();

                if (phone.isEmpty() || message.isEmpty()) {
                    Toast.makeText(MainActivity.this,
                            "Please enter phone number and message",
                            Toast.LENGTH_SHORT).show();
                    return;
                }

                Intent intent = new Intent(Intent.ACTION_SENDTO);
                intent.setData(Uri.parse("smsto:" + phone));
                intent.putExtra("sms_body", message);

                try {
                    startActivity(intent);
                } catch (Exception e) {
                    Toast.makeText(MainActivity.this,
                            "No messaging app found",
                            Toast.LENGTH_SHORT).show();
                }
            }
        });
    }
}
```

### AndroidManifest.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <!-- Needed on Android 11+ so the app can see messaging apps -->
    <queries>
        <intent>
            <action android:name="android.intent.action.SENDTO" />
            <data android:scheme="smsto" />
        </intent>
    </queries>

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="smsintent"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.Smsintent"
        tools:targetApi="31">

        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>

    </application>

</manifest>
```

> Note: No `SEND_SMS` permission is required, because the SMS is handed over to the default messaging app through an Intent.

## OUTPUT

<img width="1818" height="1142" alt="image" src="https://github.com/user-attachments/assets/374903cd-0a9f-4512-b352-3bace54f8400" />

<img width="1913" height="1190" alt="image" src="https://github.com/user-attachments/assets/eee4eb09-0a80-4f14-a82c-8ac95a0b2a3c" />


## RESULT
Thus a simple Android application to send SMS using Intent was created, designed and executed successfully using Android Studio.
