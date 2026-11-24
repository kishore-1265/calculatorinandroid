# Ex.No:5 Develop a simple calculator using android studio.

## AIM:

To develop a program to develop a simple calculator in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as calculator and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout using UI components in activity_main.xml.

Step 6: Display the calculator operation in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the text “calculator operation”.
Developed by: Kishore R
Registeration Number : 212225040192
*/
```

#### MainActivity.java
```
package com.example.calculator;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private EditText editText;
    private TextView resultText;
    private double num1 = Double.NaN;
    private double num2;
    private char CURRENT_ACTION = '0';
    private static final char ADDITION = '+';
    private static final char SUBTRACTION = '-';
    private static final char MULTIPLICATION = '*';
    private static final char DIVISION = '/';

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editText = findViewById(R.id.editText2);
        resultText = findViewById(R.id.resultText);

        Button num0 = findViewById(R.id.zero);
        Button num1Btn = findViewById(R.id.num1);
        Button num2Btn = findViewById(R.id.num2);
        Button num3Btn = findViewById(R.id.num3);
        Button num4Btn = findViewById(R.id.num4);
        Button num5Btn = findViewById(R.id.num5);
        Button num6Btn = findViewById(R.id.num6);
        Button num7Btn = findViewById(R.id.num7);
        Button num8Btn = findViewById(R.id.num8);
        Button num9Btn = findViewById(R.id.num9);

        Button addBtn = findViewById(R.id.add);
        Button subBtn = findViewById(R.id.sub);
        Button mulBtn = findViewById(R.id.mul);
        Button divBtn = findViewById(R.id.div);
        Button equalBtn = findViewById(R.id.submit);
        Button clearBtn = findViewById(R.id.clear_text);
        Button dotBtn = findViewById(R.id.dot);

        View.OnClickListener numberListener = v -> {
            Button b = (Button) v;
            editText.append(b.getText().toString());
        };

        num0.setOnClickListener(numberListener);
        num1Btn.setOnClickListener(numberListener);
        num2Btn.setOnClickListener(numberListener);
        num3Btn.setOnClickListener(numberListener);
        num4Btn.setOnClickListener(numberListener);
        num5Btn.setOnClickListener(numberListener);
        num6Btn.setOnClickListener(numberListener);
        num7Btn.setOnClickListener(numberListener);
        num8Btn.setOnClickListener(numberListener);
        num9Btn.setOnClickListener(numberListener);
        dotBtn.setOnClickListener(v -> {
            if (!editText.getText().toString().contains(".")) {
                editText.append(".");
            }
        });

        clearBtn.setOnClickListener(v -> {
            editText.setText("");
            resultText.setText("0");
            num1 = Double.NaN;
            num2 = 0;
            CURRENT_ACTION = '0';
        });

        addBtn.setOnClickListener(v -> {
            computeCalculation();
            CURRENT_ACTION = ADDITION;
            if (!Double.isNaN(num1)) {
                editText.setText(formatResult(num1) + " + ");
            }
        });

        subBtn.setOnClickListener(v -> {
            computeCalculation();
            CURRENT_ACTION = SUBTRACTION;
            if (!Double.isNaN(num1)) {
                editText.setText(formatResult(num1) + " - ");
            }
        });

        mulBtn.setOnClickListener(v -> {
            computeCalculation();
            CURRENT_ACTION = MULTIPLICATION;
            if (!Double.isNaN(num1)) {
                editText.setText(formatResult(num1) + " × ");
            }
        });

        divBtn.setOnClickListener(v -> {
            computeCalculation();
            CURRENT_ACTION = DIVISION;
            if (!Double.isNaN(num1)) {
                editText.setText(formatResult(num1) + " ÷ ");
            }
        });

        equalBtn.setOnClickListener(v -> {
            computeCalculation();
            if (!Double.isNaN(num1)) {
                resultText.setText(formatResult(num1));
                editText.setText(formatResult(num1));
                num1 = Double.NaN;
                CURRENT_ACTION = '0';
            }
        });
    }

    private void computeCalculation() {
        String text = editText.getText().toString();
        if (text.isEmpty()) return;

        if (CURRENT_ACTION != '0') {
            String operatorStr = getOperatorString(CURRENT_ACTION);
            int lastIndex = text.lastIndexOf(operatorStr);
            if (lastIndex != -1 && lastIndex + operatorStr.length() < text.length()) {
                String num2Str = text.substring(lastIndex + operatorStr.length()).trim();
                if (!num2Str.isEmpty()) {
                    try {
                        num2 = Double.parseDouble(num2Str);
                        switch (CURRENT_ACTION) {
                            case ADDITION:
                                num1 = num1 + num2;
                                break;
                            case SUBTRACTION:
                                num1 = num1 - num2;
                                break;
                            case MULTIPLICATION:
                                num1 = num1 * num2;
                                break;
                            case DIVISION:
                                if (num2 != 0) {
                                    num1 = num1 / num2;
                                } else {
                                    resultText.setText("Error");
                                    num1 = Double.NaN;
                                }
                                break;
                        }
                    } catch (NumberFormatException e) {
                        // ignore
                    }
                }
            }
        } else {
            try {
                String cleanText = text.replaceAll("[+\\-×÷]", "").trim();
                if (!cleanText.isEmpty()) {
                    num1 = Double.parseDouble(cleanText);
                }
            } catch (NumberFormatException e) {
                // ignore
            }
        }
    }

    private String getOperatorString(char action) {
        switch (action) {
            case ADDITION: return " + ";
            case SUBTRACTION: return " - ";
            case MULTIPLICATION: return " × ";
            case DIVISION: return " ÷ ";
            default: return "";
        }
    }

    private String formatResult(double val) {
        if (Double.isInfinite(val) || Double.isNaN(val)) {
            return "Error";
        }
        if (val == (long) val) {
            return String.valueOf((long) val);
        } else {
            return String.valueOf(val);
        }
    }
}

```

#### activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:background="@color/calculator_bg"
    android:gravity="center"
    android:padding="16dp">

    <EditText
        android:id="@+id/editText2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginHorizontal="16dp"
        android:textAlignment="viewEnd"
        android:focusable="false"
        android:focusableInTouchMode="false"
        android:layout_marginTop="20dp"
        android:padding="16dp"
        android:textSize="36sp"
        android:textColor="@color/white"
        android:background="@color/display_bg"
        android:hint="0"
        android:textColorHint="@color/button_action" />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginHorizontal="16dp"
        android:layout_marginTop="16dp"
        android:gravity="end"
        android:orientation="horizontal">

        <TextView
            android:id="@+id/result"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textSize="22sp"
            android:textColor="@color/button_action"
            android:text="Result: " />

        <TextView
            android:id="@+id/resultText"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textSize="22sp"
            android:textColor="@color/white"
            android:text="0" />
    </LinearLayout>

    <TableLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="24dp"
        android:gravity="center">

        <TableRow
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginBottom="8dp"
            android:gravity="center">

            <Button
                android:id="@+id/num1"
                android:layout_width="70dp"
                android:layout_height="70dp"
                android:layout_margin="6dp"
                android:backgroundTint="@color/button_number"
                android:textSize="20sp"
                android:textColor="@color/button_text"
                android:text="1" />

            <Button
                android:id="@+id/num2"
                android:layout_width="70dp"
                android:layout_height="70dp"
                android:layout_margin="6dp"
                android:backgroundTint="@color/button_number"
                android:textSize="20sp"
                android:textColor="@color/button_text"
                android:text="2" />

            <Button
                android:id="@+id/num3"
                android:layout_width="70dp"
                android:layout_height="70dp"
                android:layout_margin="6dp"
                android:backgroundTint="@color/button_number"
                android:textSize="20sp"
                android:textColor="@color/button_text"
                android:text="3" />

            <Button
                android:id="@+id/add"
                android:layout_width="70dp"
                android:layout_height="70dp"
                android:layout_margin="6dp"
                android:backgroundTint="@color/button_operator"
                android:textSize="22sp"
                android:textColor="@color/button_text"
                android:text="+" />
        </TableRow>

        <TableRow
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginBottom="8dp"
            android:gravity="center">

            <Button
                android:id="@+id/num4"
                android:layout_width="70dp"
                android:layout_height="70dp"
                android:layout_margin="6dp"
                android:backgroundTint="@color/button_number"
                android:textSize="20sp"
                android:textColor="@color/button_text"
                android:text="4" />

            <Button
                android:id="@+id/num5"
                android:layout_width="70dp"
                android:layout_height="70dp"
                android:layout_margin="6dp"
                android:backgroundTint="@color/button_number"
                android:textSize="20sp"
                android:textColor="@color/button_text"
                android:text="5" />

            <Button
                android:id="@+id/num6"
                android:layout_width="70dp"
                android:layout_height="70dp"
                android:layout_margin="6dp"
                android:backgroundTint="@color/button_number"
                android:textSize="20sp"
                android:textColor="@color/button_text"
                android:text="6" />

            <Button
                android:id="@+id/sub"
                android:layout_width="70dp"
                android:layout_height="70dp"
                android:layout_margin="6dp"
                android:backgroundTint="@color/button_operator"
                android:textSize="22sp"
                android:textColor="@color/button_text"
                android:text="-" />
        </TableRow>

        <TableRow
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginBottom="8dp"
            android:gravity="center">

            <Button
                android:id="@+id/num7"
                android:layout_width="70dp"
                android:layout_height="70dp"
                android:layout_margin="6dp"
                android:backgroundTint="@color/button_number"
                android:textSize="20sp"
                android:textColor="@color/button_text"
                android:text="7" />

            <Button
                android:id="@+id/num8"
                android:layout_width="70dp"
                android:layout_height="70dp"
                android:layout_margin="6dp"
                android:backgroundTint="@color/button_number"
                android:textSize="20sp"
                android:textColor="@color/button_text"
                android:text="8" />

            <Button
                android:id="@+id/num9"
                android:layout_width="70dp"
                android:layout_height="70dp"
                android:layout_margin="6dp"
                android:backgroundTint="@color/button_number"
                android:textSize="20sp"
                android:textColor="@color/button_text"
                android:text="9" />

            <Button
                android:id="@+id/mul"
                android:layout_width="70dp"
                android:layout_height="70dp"
                android:layout_margin="6dp"
                android:backgroundTint="@color/button_operator"
                android:textSize="22sp"
                android:textColor="@color/button_text"
                android:text="×" />
        </TableRow>

        <TableRow
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginBottom="8dp"
            android:gravity="center">

            <Button
                android:id="@+id/dot"
                android:layout_width="70dp"
                android:layout_height="70dp"
                android:layout_margin="6dp"
                android:backgroundTint="@color/button_action"
                android:textSize="22sp"
                android:textColor="@color/button_text"
                android:text="." />

            <Button
                android:id="@+id/zero"
                android:layout_width="70dp"
                android:layout_height="70dp"
                android:layout_margin="6dp"
                android:backgroundTint="@color/button_number"
                android:textSize="20sp"
                android:textColor="@color/button_text"
                android:text="0" />

            <Button
                android:id="@+id/clear_text"
                android:layout_width="70dp"
                android:layout_height="70dp"
                android:layout_margin="6dp"
                android:backgroundTint="@color/button_action"
                android:textSize="18sp"
                android:textColor="@color/button_text"
                android:text="CE" />

            <Button
                android:id="@+id/div"
                android:layout_width="70dp"
                android:layout_height="70dp"
                android:layout_margin="6dp"
                android:backgroundTint="@color/button_operator"
                android:textSize="22sp"
                android:textColor="@color/button_text"
                android:text="÷" />
        </TableRow>

    </TableLayout>

    <Button
        android:id="@+id/submit"
        android:layout_width="match_parent"
        android:layout_height="70dp"
        android:layout_marginHorizontal="22dp"
        android:layout_marginTop="16dp"
        android:backgroundTint="@color/button_operator"
        android:textSize="26sp"
        android:textColor="@color/button_text"
        android:text="=" />
</LinearLayout>

```

## OUTPUT


<img width="1917" height="1077" alt="Screenshot 2026-11-24 084503" src="https://github.com/user-attachments/assets/204e1e1f-c0f6-4ab4-97d3-b556dcccc247" />
<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/75555ef3-e486-4e6e-a269-faaab6dd08d3" />



## RESULT
Thus a Simple Android Application develop a program to create simple calculator in Android Studio is developed and executed successfully.
