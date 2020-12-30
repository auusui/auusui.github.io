/*********************************************
// NAME: Aubrie Usui
//
/// HOMEWORK: project2
///
/// CLASS: ICS 212 Program Structure
///
/// INSTRUCTOR: Ravi Narayan
///
/// FILE: user-interface.cpp
///
/// DATE: December 2, 2020
///
/// DESCRIPTION: the user will choose the menu options and it will run the functions that are called
///
************************************************/

#include "record.h"
#include "llist.h"
#include <iostream>
#include <cstring>
using namespace std;

/******************************************
// FUNCTION NAME: main
// 
// DESCRIPTION: functions are called here and gets user input
//
// PARAMETERS: argc (int), argv (char *)
//
// RETURN VALUE: 0
*******************************************/

int main (int argc, char *argv[])
{
    int transaction, option, accountno;
    char clear[100], name[25], address[80], input[10];
    std::string str ("project_debug");
   
    transaction = 1;

    if (argc > 1)
    {
        cout << "Error.  Try ./project_debug or ./project instead.\n";
        return -1;
        transaction = 0;    
    } 
     

    /*Implementation of a copy constructor or assignment operator*/
    llist begin;
    
    /* Extra credit overloading assignment operator llist
       llist being2(begin);
       cout << begin2
    */
    
    #ifdef DEBUG
    
        cout << "Function called:\treadfile\n\n";
        cout << "Parameters:\n";
        cout << "Hardcoded txt file:\tsavedfiles.txt\n";

        cout << "Debug has ended\n";
    #endif

    cout << "\nWelcome.  Below you will see a table of options you can perform.  Please enter the word of the option you want to perform.\n";
    cout << "----------------------------------------------------------\n\n";

    while ((transaction == 1))
    {
        
        cout << "---------------------------\n";
        cout << "Type add : Add new record\n";
        cout << "Type printall : Print All records\n";
        cout << "Type find : Find a record\n";
        cout << "Type delete : Delete record\n";
        cout << "Type quit : Quit the program\n";
        cout << "---------------------------\n";

        cin.getline(input, 10);

        if (strncmp (input, "axx", 1) == 0)
        {
            option = 1;
        }
        else if (strncmp (input, "pxxxxxxx", 1) == 0)
        {
            option = 2;
        }
        else if (strncmp (input, "fxxx", 1) == 0)
        {
            option = 3;
        }
        else if (strncmp (input, "dxxxxx", 1) == 0)
        {
            option = 4;
        }
        else if (strncmp (input, "qxxx", 1) == 0)
        {
            option = 5;
        }
        else
        {
            cout << "ERROR: Please enter a valid input from the menu\n\n";
        }

               
        if (option == 1) 
        {
            cout << "You are now entering the Add Record function.\n\n";
            cout << "Please enter an account number.  Enter only numbers\n";
            
            cin >> accountno;
            
            cin.getline(clear, 100);
            cout << "Please enter the name of account\n";
            cout << "Press ENTER when finished\n";
            cin.getline(name, 25);

            cout << "Please enter the address of record\n";
            cout << "Type '$' when finished then press ENTER\n";
            cin.getline(address, 80, '$');
            cin.getline(clear, 100);
            
            #ifdef DEBUG
            cout << "Function called:\taddRecord\n\n" << endl;
            cout << "Parameters:\n";
            cout << "Account number:  " << accountno << endl;
            cout << "Name:  " << name << endl;
            cout << "Address:  " << address << endl;

            cout << "DEBUGMODE ENDING\n\n";
            #endif       

            begin.addRecord(accountno, name, address);
        }
        else if (option == 2)
        {
            cout << "You are now entering the Print All function.\n";
            cout << begin;
            cout << "All records are shown.\n\n";
        }
        else if (option == 3)
        {
            cout << "You are now entering Find Record function.\n";
            cout << "Enter the account number of the record you want to find.\n";
            cin >> accountno;
            cin.getline(clear, 100);

            #ifdef DEBUG
            cout << "Function Called:\tFind Record\n\n" << endl;
            cout << "Parameters: \n";
            cout << "Account Number:\t" << accountno << endl;
            cout << "DEBUGMODE ENDING \n\n";
            #endif

            if (begin.findRecord(accountno) != -1)
            {
                cout << "\nHere are your records.\n";
            }
        }
        else if (option == 4)
        {
            cout << "You are now entering the Delete function.\n";
            
            cout << "Please enter the account number you would like to delete,\n";
            cin >> accountno;

            cin.getline(clear, 100);


            #ifdef DEBUG
            cout << "Function called:\tdeleteRecord\n\n";
            cout << "Parameters:\n";
            cout << "Account number:\t" << accountno << endl;
            cout << "DEBUGMODE ENDING\n";
            #endif

            if (begin.deleteRecord(accountno) == 0)
            {
                cout << "\nYour record or records were successfully deleted.\n";
            }
            else 
            {
                cout << "\nThere are no records to be deleted.\n";
            }
        }
        else if (option == 5) 
        {
            #ifdef DEBUG
            cout << "Function called:\tcleanup and writefile\n\n" << endl;
            cout << "Parameters:\tnone\n" << endl;
            cout << "DEBUGMODE ENDING\n";
            #endif
            
            transaction = 0;
            cout<< "\nYou have successfully exited the program.\n";
        }
        
    }
    return 0;   
}
