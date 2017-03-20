# simpe-coffee-app
package com.example.android.justjava;



import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.view.View;
import android.widget.CheckBox;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;


public class MainActivity extends AppCompatActivity {
    int quantity = 1;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }


    public void submitOrder(View view) {

        EditText editText = (EditText) findViewById(R.id.editTextName);
        String inputName = editText.getText().toString();


        CheckBox chocolateCheckBox = (CheckBox) findViewById(R.id.chocolate_checkbox);
        boolean hasChocolate = chocolateCheckBox.isChecked();

        CheckBox whippedCreamCheckBox = (CheckBox) findViewById(R.id.whipped_cream_checkbox);
        boolean hasWhippedCream = whippedCreamCheckBox.isChecked();


        int price = calculatePrice(quantity, 5, hasWhippedCream, hasChocolate);
        String message = createOrderSummary(quantity, price, hasWhippedCream, hasChocolate, inputName);
        displayMessage(message);
   


    }

    public void increment(View view) {
        if (quantity < 100) {
            quantity = quantity + 1;


        }
        displayQuantity(quantity);
        if (quantity >= 100) {
            Toast toast1 = Toast.makeText(getApplicationContext(), "You cannot have more than 100 cups of coffee", Toast.LENGTH_SHORT);
            toast1.show();
        }
    }

    public void decrement(View view) {

        if (quantity > 1) {
            quantity = quantity - 1;


        }
        displayQuantity(quantity);
        if ((quantity == 1) && quantity > 0) {
            Toast toast2 = Toast.makeText(getApplicationContext(), "You cannot have less than 1 cup of coffee", Toast.LENGTH_SHORT);
            toast2.show();
        }
    }


    private void displayQuantity(int liczba) {
        TextView quantityTextView = (TextView) findViewById(R.id.quantity_text_view);
        quantityTextView.setText("" + liczba);
    }



    private void displayMessage(String message) {
        TextView orderSummaryTextView = (TextView) findViewById(R.id.order_summary_text_view);
        orderSummaryTextView.setText(message);
    }

    private int calculatePrice(int quantity, int priceForOneCoffee, boolean hasWhippedCream, boolean hasChocolate) {
        int price = quantity * priceForOneCoffee;
        if (hasChocolate && hasWhippedCream) {
            price = quantity * (priceForOneCoffee + 2 + 1);
        } else if (hasWhippedCream) {
            price = quantity * (priceForOneCoffee + 1);
        } else if (hasChocolate) {
            price = quantity * (priceForOneCoffee + 2);
        }

        return price;

    }


    private String createOrderSummary(int quantity, int price, boolean addWhippedCream, boolean addChocolate, String addName) {
        String message = "Name: " + addName +
                '\n' + "Add whipped cream? " + addWhippedCream +
                '\n' + "Add chocolate? " + addChocolate +
                '\n' + "Quantity: " + quantity +
                '\n' + "Total: $" + price +
                '\n' + getString(R.string.thank_you);
        return message;

    }

}
