# CODEALPHA_TASKS
#include <iostream>
#include <vector>
#include <iomanip>
using namespace std;

int main() {
    int numCourses;
    vector<double> grades;
    vector<int> creditHours;

    cout << "Enter the number of courses: ";
    cin >> numCourses;

    // Input grades and credit hours
    for (int i = 0; i < numCourses; ++i) {
        double grade;
        int credits;
        cout << "Enter grade for course " << i + 1 << ": ";
        cin >> grade;
        cout << "Enter credit hours for course " << i + 1 << ": ";
        cin >> credits;

        grades.push_back(grade);
        creditHours.push_back(credits);
    }

    // Calculate total credits and grade points
    double totalGradePoints = 0;
    int totalCredits = 0;

    for (int i = 0; i < numCourses; ++i) {
        totalGradePoints += grades[i] * creditHours[i];
        totalCredits += creditHours[i];
    }

    // Compute CGPA
    double cgpa = totalGradePoints / totalCredits;

    // Display grades and CGPA
    cout << "\nCourse Details:\n";
    cout << "--------------------------\n";
    cout << "Course\tGrade\tCredits\n";
    for (int i = 0; i < numCourses; ++i) {
        cout << i + 1 << "\t" << grades[i] << "\t" << creditHours[i] << "\n";
    }

    cout << "--------------------------\n";
    cout << fixed << setprecision(2);
    cout << "Final CGPA: " << cgpa << endl;

    return 0;
}
Q2
#include <iostream>
#include <vector>
#include <iomanip>
using namespace std;

int main() {
    int numCourses;
    vector<double> grades;
    vector<int> creditHours;

    cout << "Enter the number of courses: ";
    cin >> numCourses;

    // Input grades and credit hours
    for (int i = 0; i < numCourses; ++i) {
        double grade;
        int credits;
        cout << "Enter grade for course " << i + 1 << ": ";
        cin >> grade;
        cout << "Enter credit hours for course " << i + 1 << ": ";
        cin >> credits;

        grades.push_back(grade);
        creditHours.push_back(credits);
    }

    // Calculate total credits and grade points
    double totalGradePoints = 0;
    int totalCredits = 0;

    for (int i = 0; i < numCourses; ++i) {
        totalGradePoints += grades[i] * creditHours[i];
        totalCredits += creditHours[i];
    }

    // Compute CGPA
    double cgpa = totalGradePoints / totalCredits;

    // Display grades and CGPA
    cout << "\nCourse Details:\n";
    cout << "--------------------------\n";
    cout << "Course\tGrade\tCredits\n";
    for (int i = 0; i < numCourses; ++i) {
        cout << i + 1 << "\t" << grades[i] << "\t" << creditHours[i] << "\n";
    }

    cout << "--------------------------\n";
    cout << fixed << setprecision(2);
    cout << "Final CGPA: " << cgpa << endl;

    return 0;
}
Q3
#include <iostream>
using namespace std;

const int SIZE = 9;

// Function to print the Sudoku board
void printBoard(int board[SIZE][SIZE]) {
    for (int row = 0; row < SIZE; row++) {
        for (int col = 0; col < SIZE; col++) {
            cout << board[row][col] << " ";
        }
        cout << endl;
    }
}

// Check if it's safe to place a number in a given cell
bool isSafe(int board[SIZE][SIZE], int row, int col, int num) {
    // Check row and column
    for (int i = 0; i < SIZE; i++) {
        if (board[row][i] == num || board[i][col] == num)
            return false;
    }

    // Check 3x3 subgrid
    int startRow = row - row % 3;
    int startCol = col - col % 3;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i + startRow][j + startCol] == num)
                return false;
        }
    }

    return true;
}

// Backtracking function to solve the Sudoku
bool solveSudoku(int board[SIZE][SIZE]) {
    for (int row = 0; row < SIZE; row++) {
        for (int col = 0; col < SIZE; col++) {
            // Find empty cell
            if (board[row][col] == 0) {
                for (int num = 1; num <= 9; num++) {
                    // Check if placing num is safe
                    if (isSafe(board, row, col, num)) {
                        board[row][col] = num;  // Place number

                        if (solveSudoku(board))  // Recurse
                            return true;

                        board[row][col] = 0;     // Backtrack
                    }
                }
                return false;  // No valid number found
            }
        }
    }
    return true;  // No empty cells left (solved)
}

int main() {
    int board[SIZE][SIZE] = {
        {5, 3, 0, 0, 7, 0, 0, 0, 0},
        {6, 0, 0, 1, 9, 5, 0, 0, 0},
        {0, 9, 8, 0, 0, 0, 0, 6, 0},
        {8, 0, 0, 0, 6, 0, 0, 0, 3},
        {4, 0, 0, 8, 0, 3, 0, 0, 1},
        {7, 0, 0, 0, 2, 0, 0, 0, 6},
        {0, 6, 0, 0, 0, 0, 2, 8, 0},
        {0, 0, 0, 4, 1, 9, 0, 0, 5},
        {0, 0, 0, 0, 8, 0, 0, 7, 9}
    };

    if (solveSudoku(board)) {
        cout << "✅ Sudoku Solved Successfully:\n";
        printBoard(board);
    } else {
        cout << " No solution exists for this Sudoku.\n";
    }

    return 0;
}
Q4
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

class Account {
public:
    string name;
    int accountNumber;
    double balance;

    void createAccount() {
        cout << "\nEnter Account Holder Name: ";
        cin.ignore();
        getline(cin, name);
        cout << "Enter Account Number: ";
        cin >> accountNumber;
        cout << "Enter Initial Balance: ";
        cin >> balance;

        ofstream file("bank.txt", ios::app);
        file << name << " " << accountNumber << " " << balance << endl;
        file.close();

        cout << "✅ Account created successfully!\n";
    }

    void displayAccounts() {
        ifstream file("bank.txt");
        cout << "\n=== All Bank Accounts ===\n";
        cout << "Name\tAccount No\tBalance\n";
        cout << "---------------------------------\n";

        while (file >> name >> accountNumber >> balance) {
            cout << name << "\t" << accountNumber << "\t\t" << balance << endl;
        }
        file.close();
    }

    void depositMoney() {
        int accNo;
        double amount;
        bool found = false;

        cout << "\nEnter Account Number: ";
        cin >> accNo;
        cout << "Enter Amount to Deposit: ";
        cin >> amount;

        ifstream inFile("bank.txt");
        ofstream tempFile("temp.txt");

        while (inFile >> name >> accountNumber >> balance) {
            if (accountNumber == accNo) {
                balance += amount;
                found = true;
            }
            tempFile << name << " " << accountNumber << " " << balance << endl;
        }

        inFile.close();
        tempFile.close();

        remove("bank.txt");
        rename("temp.txt", "bank.txt");

        if (found)
            cout << "✅ Amount deposited successfully!\n";
        else
            cout << "❌ Account not found!\n";
    }

    void withdrawMoney() {
        int accNo;
        double amount;
        bool found = false;

        cout << "\nEnter Account Number: ";
        cin >> accNo;
        cout << "Enter Amount to Withdraw: ";
        cin >> amount;

        ifstream inFile("bank.txt");
        ofstream tempFile("temp.txt");

        while (inFile >> name >> accountNumber >> balance) {
            if (accountNumber == accNo) {
                if (balance >= amount) {
                    balance -= amount;
                    found = true;
                } else {
                    cout << "❌ Insufficient Balance!\n";
                }
            }
            tempFile << name << " " << accountNumber << " " << balance << endl;
        }

        inFile.close();
        tempFile.close();

        remove("bank.txt");
        rename("temp.txt", "bank.txt");

        if (found)
            cout << "✅ Amount withdrawn successfully!\n";
        else
            cout << "❌ Account not found!\n";
    }
};

int main() {
    Account acc;
    int choice;

    do {
        cout << "\n=========== BANK MENU ===========\n";
        cout << "1. Create Account\n";
        cout << "2. Display All Accounts\n";
        cout << "3. Deposit Money\n";
        cout << "4. Withdraw Money\n";
        cout << "5. Exit\n";
        cout << "=================================\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1: acc.createAccount(); break;
            case 2: acc.displayAccounts(); break;
            case 3: acc.depositMoney(); break;
            case 4: acc.withdrawMoney(); break;
            case 5: cout << "\nThank you for using the banking system!\n"; break;
            default: cout << " Invalid choice! Try again.\n";
        }
    } while (choice != 5);

    return 0;
}

