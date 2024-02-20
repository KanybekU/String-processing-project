#include <iostream>
#include <cstdlib>
#include <ctime>
#include <string>
using namespace std;

// Function to generate a random password
string generatePassword(int minLength, int maxLength, bool includeLower, bool includeUpper, bool includeNumbers, bool includeSymbols, const string& customChars = "") {
    string password = ""; //Initialize an empty password
    string allChars = ""; // Initialize an empty string for all possible characters

    // Add lowercase letters if requested
    if (includeLower)
        allChars += "abcdefghijklmnopqrstuvwxyz";

    // Add uppercase letters if requested
    if (includeUpper)
        allChars += "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

    // Add numbers if requested
    if (includeNumbers)
        allChars += "0123456789";

    // Add symbols if requested
    if (includeSymbols)
        allChars += "!@#$%^&*_";

    // Add custom characters
    allChars += customChars;

    // Check if any character set is selected
    if (allChars.empty()) {
        cerr << "Error: No character set selected!" << endl;
        return password; // Return an empty password
    }

    // Generate a random password length between minLength and maxLength
    srand(time(nullptr));
    int length = minLength + rand() % (maxLength - minLength + 1);

    // Construct the password by randomly selecting characters
    for (int i = 0; i < length; ++i) {
        password += allChars[rand() % allChars.length()];
    }

    return password; //Return the generated password
}

int main() {
    int minLength, maxLength;
    bool includeLower, includeUpper, includeNumbers, includeSymbols;
    string customChars;
    //Here i add some new function u will test it later 
    char regenerate = 'y'; // Initialize with 'y' to enter the loop

    while (regenerate == 'y' || regenerate == 'Y') {
        // Get user input for password criteria
        cout << "Enter minimum length of password: ";
        cin >> minLength;
        cout << "Enter maximum length of password: ";
        cin >> maxLength;

        cout << "Include lowercase letters? (1 for yes, 0 for no): ";
        cin >> includeLower;
        cout << "Include uppercase letters? (1 for yes, 0 for no): ";
        cin >> includeUpper;
        cout << "Include numbers? (1 for yes, 0 for no): ";
        cin >> includeNumbers;
        cout << "Include symbols? (1 for yes, 0 for no): ";
        cin >> includeSymbols;

        cin.ignore(); // Clear input buffer
        cout << "Enter custom characters (leave empty for none): ";
        getline(cin, customChars);

        // Generate and display the password
        cout << "Generated Password: " << generatePassword(minLength, maxLength, includeLower, includeUpper, includeNumbers, includeSymbols, customChars) << endl;

        // Ask the user if they want to regenerate a new password
        cout << "Would you like to regenerate a new password? (y/n): ";
        cin >> regenerate;
    }

    cout << "Ok, see you later. ( ͡° ͜ʖ ͡° )" << endl;

    return 0;
}
