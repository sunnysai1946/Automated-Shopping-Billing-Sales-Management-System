# Automated-Shopping-Billing-Sales-Management-System in c++

#include <iostream>
#include <fstream>
using namespace std;

const int MAX = 50;
string itemName[MAX];
float itemPrice[MAX];
int itemQty[MAX];
int itemCount = 0;
float totalAmount = 0;

// ----- Overloaded Discount Functions -----
float discount(float percent) {
    return totalAmount - (totalAmount * percent / 100);
}

float discount(int couponValue) {
    return totalAmount - couponValue;
}

// ----- Add Item -----
void addItem() {
    cout << "Enter item name: ";
    cin >> itemName[itemCount];

    cout << "Enter price: ";
    cin >> itemPrice[itemCount];

    cout << "Enter quantity: ";
    cin >> itemQty[itemCount];

    totalAmount += itemPrice[itemCount] * itemQty[itemCount];
    itemCount++;
}

// ----- Generate Bill & Save to File -----
void generateBill() {
    ofstream file("bill.txt");

    cout << "\n========= SHOPPING BILL =========\n";
    file << "========= SHOPPING BILL =========\n";

    for (int i = 0; i < itemCount; i++) {
        float cost = itemPrice[i] * itemQty[i];

        cout << itemName[i] << " x" << itemQty[i] << " = Rs " << cost << endl;
        file << itemName[i] << " x" << itemQty[i] << " = Rs " << cost << endl;
    }

    cout << "\nTotal Amount: Rs " << totalAmount << endl;
    file << "\nTotal Amount: Rs " << totalAmount << endl;

    file.close();
    cout << "Bill saved to bill.txt\n";
}

// ----- Daily Sales Report -----
void salesReport() {
    cout << "\n====== DAILY SALES REPORT ======\n";
    cout << "Items Sold: " << itemCount << endl;
    cout << "Total Earnings: Rs " << totalAmount << endl;
}

// ----- MAIN -----
int main() {
    int n;

    cout << "Enter number of items: ";
    cin >> n;

    for (int i = 0; i < n; i++) {
        addItem();
    }

    // Apply discount
    int choice;
    cout << "\n1. Percentage Discount\n2. Coupon Discount\n3. No Discount\nChoose: ";
    cin >> choice;

    if (choice == 1) {
        float percent;
        cout << "Enter % discount: ";
        cin >> percent;
        cout << "Final Amount: Rs " << discount(percent) << endl;
    }
    else if (choice == 2) {
        int coupon;
        cout << "Enter coupon amount: ";
        cin >> coupon;
        cout << "Final Amount: Rs " << discount(coupon) << endl;
    }

    generateBill();
    salesReport();

    return 0;
}
