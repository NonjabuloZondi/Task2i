# Task2i
#include <iostream>
#include <algorithm>
#include <ctime>
#include <cstdlib>
#include <sstream>
#include <iomanip>
#include <cctype>

using namespace std;

string dec2bin(int decimal);
int bin2dec(string binary);
int hex2dec(string hexadecimal);
string dec2hex(int decimal);

// Convert Decimal to Binary
string dec2bin(int decimal) {
    if (decimal == 0) return "0";

    bool isNegative = false;
    if (decimal < 0) {
        isNegative = true;
        decimal = -decimal;
    }

    string binary;
    while (decimal > 0) {
        binary = (decimal % 2 ? "1" : "0") + binary;
        decimal /= 2;
    }

    if (isNegative) {
        binary = "-" + binary;
    }

    return binary;
}

// Convert Binary to Decimal
int bin2dec(string binary) {
    int decimal = 0;
    int power = 1;

    for (int i = binary.length() - 1; i >= 0; i--) {
        if (binary[i] == '1') {
            decimal += power;
        }
        else if (binary[i] != '0') {
            cerr << "Error: Invalid binary digit '" << binary[i] << "' found." << endl;
            return -1;
        }
        power *= 2;
    }

    return decimal;
}

// Convert Hexadecimal to Decimal
int hex2dec(string hexadecimal) {
    int decimal = 0;
    int power = 1;

    for (int i = hexadecimal.length() - 1; i >= 0; i--) {
        char c = toupper(hexadecimal[i]);

        if (c >= '0' && c <= '9') {
            decimal += (c - '0') * power;
        }
        else if (c >= 'A' && c <= 'F') {
            decimal += (c - 'A' + 10) * power;
        }
        else if (i == 0 && c == '-') {
            decimal = -decimal;
        }
        else {
            cerr << "Error: Invalid hexadecimal digit '" << hexadecimal[i] << "'" << endl;
            return -1;
        }

        power *= 16;
    }

    return decimal;
}

// Convert Decimal to Hexadecimal
string dec2hex(int decimal) {
    if (decimal == 0) return "0";

    bool isNegative = false;
    if (decimal < 0) {
        isNegative = true;
        decimal = -decimal;
    }

    stringstream ss;
    ss << hex << uppercase << decimal;
    string hexStr = ss.str();

    if (isNegative)
        hexStr = "-" + hexStr;

    return hexStr;
}

// Main Program
int main() {
    int menuselection = 0;

    // Seed random number generator once
    srand(static_cast<unsigned int>(time(0)));

    cout << "Conversion Menu:\n";
    cout << "1. Convert Decimal to Binary\n";
    cout << "2. Convert Binary to Decimal\n";
    cout << "3. Convert Hexadecimal to Decimal\n";
    cout << "4. Convert Decimal to Hexadecimal\n";
    cout << "5. Demo (Generate and convert random integers to binary)\n";
    cout << "6. Exit\n";

    while (true) {
        cout << "\nEnter your choice (1-6): ";
        cin >> menuselection;

        // Handle invalid input type
        if (cin.fail()) {
            cin.clear();
            cin.ignore(1000, '\n');
            cout << "Invalid input. Please enter a number between 1 and 6." << endl;
            continue;
        }

        if (menuselection == 1) {
            int decimal;
            cout << "Enter a decimal number: ";
            cin >> decimal;
            cout << "Binary representation: " << dec2bin(decimal) << endl;

        } else if (menuselection == 2) {
            string binary;
            cout << "Enter a binary number: ";
            cin >> binary;
            int result = bin2dec(binary);
            if (result != -1)
                cout << "Decimal representation: " << result << endl;

        } else if (menuselection == 3) {
            string hexadecimal;
            cout << "Enter a hexadecimal number: ";
            cin >> hexadecimal;
            int result = hex2dec(hexadecimal);
            if (result != -1)
                cout << "Decimal representation: " << result << endl;

        } else if (menuselection == 4) {
            int decimal;
            cout << "Enter a decimal number: ";
            cin >> decimal;
            cout << "Hexadecimal representation: " << dec2hex(decimal) << endl;

        } else if (menuselection == 5) {
            int randomNumber = rand() % 100000;
            cout << "Generated random number: " << randomNumber << endl;
            cout << "Binary representation: " << dec2bin(randomNumber) << endl;

        } else if (menuselection == 6) {
            cout << "Exiting the program." << endl;
            break;

        } else {
            cout << "Invalid option. Please choose between 1 and 6." << endl;
        }
    }

    return 0;
}
