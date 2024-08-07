# library_management_easy
just a simple C++ code to add,delete,desplay,search books 
#include <iostream>
#include <string>
#include <cstring>

using namespace std;

class Library {
public:
    int choice;
    static const int maxSize = 1000;
    string title, author;
    string stringArray[maxSize] = {
        "The Great Gatsby",
        "To Kill a Mockingbird",
        "The Catcher in the Rye",
        "The Lord of the Rings"
    }; // Initializing with 4 strings
    int currentSize = 4;                                               // Current number of strings in the array
    int numberOfNewStrings;

    void add();
    void del();
    void search(const string& substring);
    void display();
    void input();
};

void Library::input() {
    do {
        cout << "Main Menu";
        cout << "\n1. Add a book by its title";
        cout << "\n2. Delete a book by its s.no";
        cout << "\n3. Search a book by its title";
        cout << "\n4. Display all books";
        cout << "\n5. Exit from menu";

        cout << "\nEnter your choice from above: ";
        cin >> choice;

        switch (choice) {
        case 1:
            add();
            break;
        case 2:
            del();
            break;
        case 3: {
            string substring;
            cout << "Enter the substring to search for: ";
            cin.ignore(); // Clear the newline character from the buffer
            getline(substring);
            search(substring);
            break;
        }
        case 4:
            display();
            break;
        case 5:
            cout << "Exiting menu.\n";
            break;
        default:
            cout << "Invalid choice, please try again.\n";
        }
    } while (choice != 5);
}

void Library::add() {
    cout << "How many new books do you want to add? ";
    cin >> numberOfNewStrings;

    // Check if adding new strings will exceed the maximum size
    if (currentSize + numberOfNewStrings > maxSize) {
        cout << "Not enough space in the array to add " << numberOfNewStrings << " new books." << endl;
        return;
    }

    // Get new strings from the user
    cin.ignore(); // Clear the newline character from the buffer
    for (int i = 0; i < numberOfNewStrings; ++i) {
        cout << "Enter new book title " << i + 1 << ": ";
        getline(cin, stringArray[currentSize + i]);
    }

    // Update the current size
    currentSize += numberOfNewStrings;
}

void Library::del() {
    // Print the initial array
    cout << "Initial array:\n";
    for (int i = 0; i < currentSize; ++i) {
        cout << i << ": " << stringArray[i] << endl;
    }

    // Ask user which string to delete
    int deleteIndex;
    cout << "Enter the index of the book you want to delete (0 to " << currentSize - 1 << "): ";
    cin >> deleteIndex;

    // Validate the index
    if (deleteIndex < 0 || deleteIndex >= currentSize) {
        cout << "Invalid index!" << endl;
        return;
    }

    // Shift elements to the left to overwrite the deleted string
    for (int i = deleteIndex; i < currentSize - 1; ++i) {
        stringArray[i] = stringArray[i + 1];
    }

    // Reduce the current size
    currentSize--;

    // Print the updated array
    cout << "\nUpdated array:\n";
    for (int i = 0; i < currentSize; ++i) {
        cout << i << ": " << stringArray[i] << endl;
    }
}

void Library::search(const string& substring) { 
    bool found = false;
    for (int i = 0; i < currentSize; i++) {
        if (stringArray[i].find(substring) != string::npos) {
            cout << stringArray[i] << endl;
            found = true;
        }
    }
    if (!found) {
        cout << "No book found containing the substring: " << substring << endl;
    }
}

void Library::display() {
    cout << "Current list of books:\n";
    for (int i = 0; i < currentSize; ++i) {
        cout << i << ": " << stringArray[i] << endl;
    }
}

int main() {
    Library ob;
    ob.input();

    return 0;
}
