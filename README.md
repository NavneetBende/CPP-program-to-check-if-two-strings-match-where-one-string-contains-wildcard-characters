Checking if two strings match where one String contains wild characters
In this article, we will learn how to write a C++ program to check if two strings match where one string contains wildcard characters. Wildcard characters are those that can be compared with one or more characters. ‘*’ and ‘?’ are typical wildcard characters where ‘*’ can be compared with zero or more characters (string, str*ng,s*g are same )and ‘?’ can be compared with only one character (string, str?ng are same). In this program, we will make a function check() with boolean as a return type, that will return true if the strings match else it will return false.

Cpp program to check if two strings match where one string contains wildcard characters
Algorithm:
Initialize the variables.
Accept the input.
Check both the strings character by character.
If a character of wild  string contains a ‘*’, take the next character from wild string and check for that character in string which you want to match.
If they match, continue checking the next character
Else return false.
If the character of wild string contains a ‘?’, check if the immediate next character of wild string and the next character of string to be matched.
If they match, continue checking  the next characters.
Else, return false.
Print result.
 
While loop in C
C++ program (String contains wild characters)
Run
#include<iostream>

using namespace std;
int main() {
    //Initialize the variables.
    string wild = "Prep*nsta", str = "Prepinsta";
    //Accept the inputs.

    cout << "String containing wild characters: ";
    cout << wild << endl;
    cout << "String to be matched: ";
    cout << str << endl;

    bool TRUE = true, FALSE = false;
    bool check[wild.length() + 1][str.length() + 1];
    check[0][0] = TRUE;

    for (int i = 1; i <= str.length(); i++)
        check[0][i] = FALSE;
    for (int i = 1; i <= wild.length(); i++)
        if (wild[i - 1] == '*') //Checking for wild characters.
            check[i][0] = check[i - 1][0];
        else
            check[i][0] = FALSE;

    for (int i = 1; i <= wild.length(); i++) {
        for (int j = 1; j <= wild.length(); j++) {
            if (wild[i - 1] == str[j - 1])
                check[i][j] = check[i - 1][j - 1];
            else if (wild[i - 1] == '?') //Checking for wild character '?'.
                check[i][j] = check[i - 1][j - 1];
            else if (wild[i - 1] == '*') //Checking for wild character '*'.
                check[i][j] = check[i - 1][j] || check[i][j - 1];

            else
                check[i][j] = FALSE;
        }
    }
    //Printing result.
    if (check[wild.length()][str.length()])
        cout << "TRUE";
    else
        cout << "FALSE";
}
Output
String containing wild characters: Prep*nsta
String to be matched: Prepinsta
TRUE
