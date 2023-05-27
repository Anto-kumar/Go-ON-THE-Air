# Go-ON-THE-Air
#include <bits/stdc++.h>
using namespace std;

class Airline
{
private:
    int flightNO;
    float price;
    string time;
    string flightname;
    string date;

public:
    void menu();
    void administrator();
    void passenger();
    void add();
    void edit();
    void rem();
    void list();
    void ticket();
};

void Airline ::menu()
{
m:
    int choice;
    string email;
    string password;

    cout << "\n\t\t\t ________________X_______________\n"
         << endl;
    cout << "\t\t\t            Air line          " << endl;
    cout << "\t\t\t ________________________________" << endl;
    cout << "\t\t\t 1. Administrator \n";
    cout << "\t\t\t 2. Passenger \n";
    cout << "\t\t\t 3. Exit \n";
    cout << "\t\t\t         \n";
    cout << "\t\t\t Please select :";

    cin >> choice;
    switch (choice)
    {
    case 1:
        cout << "\t\t\t Please Login \n";
        cout << "\t\t\t Enter Email :";
        cin >> email;
        cout << "\t\t\t Password :";
        cin >> password;
        if (email == "admin@gmail.com" && password == "admin")
        {
            administrator();
        }
        else
        {
            cout << "Invalid email / password ";
        }
        break;
    case 2:
    {
        passenger();
        break;
    }
    case 3:
    {
        exit(0);
    }
    default:
    {
        cout << "Please select from the given options";
    }
    }
    goto m;
}

void Airline::administrator()
{
m:
    int choice;
    cout << "\n\n\n \t\t\t ***Administrator menu ***\n";
    cout << "\n\t\t\t   |1. Add ticket           |";
    cout << "\n\t\t\t   |                        |";
    cout << "\n\t\t\t   |2. Modify the ticket    |";
    cout << "\n\t\t\t   |                        |";
    cout << "\n\t\t\t   |3.Delete the ticket     |";
    cout << "\n\t\t\t   |                        |";
    cout << "\n\t\t\t   |4.Back to the main menu |";

    cout << "\n\n\t\t\t   Please enter your choice : ";
    cin >> choice;
    switch (choice)
    {
    case 1:
        add();
        break;

    case 2:
        edit();
        break;

    case 3:
        rem();
        break;

    case 4:
        menu();
        break;

    default:
        cout << "Invalid choice!";
    }
    goto m;
}
void Airline::passenger()
{
m:
    int choice;
    cout << "\n\n\t\t\t    Passenger      \n";
    cout << "\t\t\t ________________\n";
    cout << "                     \n";
    cout << "\t\t\t 1. Buy airticket \n"<< endl;
    cout << "\t\t\t 2. Go back   \n"<< endl;
    cout << "\t\t\t Enter your choice: ";

    cin >> choice;

    switch (choice)
    {
    case 1:
        ticket();
        break;

    case 2:
        menu();
        break;

    default:
        cout << "Invalid choice ";
    }
    goto m;
}

void Airline::add()
{
m:
    fstream data;
    int c;
    int token = 0;
    float p;
    string t;
    string n;
    string s;

    cout << " \n \t\t______ Add new ticket_____\n ";
    cout << " \n\t\t Flight no            : ";
    cin >> flightNO;
    cout << "\n\t\tFlight destinaton      :";
    cin >> flightname;
    cout << "\n\t\tTicket price           : ";
    cin >> price;
    cout << "\n\t\tFlight Date(1th-july)  :";
    cin >> date;
    cout << "\n\t\tFlight time            :";
    cin >> time;

    data.open("airfile.txt", ios::in);
    if (!data)
    {
        data.open("airfile.txt", ios::app | ios::out);
        // data <<" "<< flightNO << " " << flightname << " " << price << " " << date << " " << time << "\n";
        data.close();
    }
    else
    {
        data >> c >> n >> p >> s >> t;
        while (!data.eof())
        {
            if (c == flightNO)
            {
                token++;
            }
            data >> c >> n >> p >> s >> t;
        }
        data.close();
    }
    if (token == 1)
    {
        goto m;
    }
    else
    {
        data.open("airfile.txt", ios::app | ios::out);
        data << " " << flightNO << " " << flightname << " " << price << " " << date << " " << time << "\n";
        data.close();
    }

    cout << "\n\nl\t\t Record inserted !";
}

void Airline ::edit()
{
    fstream data, data1;
    int pkey;
    int token = 0;
    int c;
    float p;
    string t;
    string s;
    string n;
    list();
    cout << "\n\t\t\t Modify the record ";
    cout << "\n\t\t\t Enter the flight code :";
    cin >> pkey;

    data.open("airfile.txt", ios::in);
    if (!data)
    {
        cout << "\n\n File doesn't exist ";
    }
    else
    {
        data1.open("airfile1.txt", ios::app | ios::out);

        data >> flightNO >> flightname >> price >> date >> time;
        while (!data.eof())
        {
            if (pkey == flightNO)
            {
                cout << " \n\t\t Flight no : ";
                cin >> c;
                cout << "\n\t\tFlight destinaton :";
                cin >> n;
                cout << "\n\t\tTicket price      : ";
                cin >> p;
                cout << "\n\t\tFlight time       :";
                cin >> t;
                cout << "\n\t\tFlight Date        :";
                cin >> s;
                data1 << c << " " << n << " " << p << " " << s << " " << t << "\n";
                cout << "\n\n\t\t Record edited ";
                token++;
            }
            else
            {
                data1 << flightNO << " " << flightname << " " << price << " " << date << " " << time << "\n";
            }
            data >> flightNO >> flightname >> price >> date >> time;
        }
        data.close();
        data1.close();

        remove("airfile.txt");
        rename("airfile1.txt", "airfile.txt");
        if (token == 0)
        {
            cout << "\n\n Record not found sorry !";
        }
    }
}

void Airline ::rem()
{
    fstream data, data1;
    int fNO;
    int token = 0;
    list();
    cout << " \n\n\t << Delete Air Flight >>  ";
    cout << "\n\n\t  Enter air ticket number :";
    cin >> fNO;

    data.open("airfile.txt", ios::in);
    if (!data)
    {
        cout << "File doesn't exist";
    }
    else
    {
        data1.open("airfile1.txt", ios::app | ios::out);
        data >> flightNO >> flightname >> price >> date >> time;
        while (!data.eof())
        {
            if (flightNO == fNO)
            {
                cout << "\n\n \t Ticket deletdd succesfully";
                token++;
            }
            else

            {
                data1 << flightNO << " " << flightname << " " << price << " " << date << " " << time << "\n";
            }
            data >> flightNO >> flightname >> price >> date >> time;
        }
        data.close();
        data1.close();
        remove("airfile.txt");
        rename("airfile1.txt", "airfile.txt");
        if (token == 0)
        {
            cout << "\n\n Record not found ";
        }
    }
}
void Airline::list()
{
    fstream data;
    data.open("airfile.txt", ios::in);
    if (!data)
    {
        cout << "Air File doesn't exist";
        administrator();
    }
    else
    {
        cout << "\n_________________________________________________________________________\n";
        cout << "Flight NO\tDestination (Dhaka to )\t  Price \tdate  \tTime  ";
        cout << "\n_________________________________________________________________________\n";
        data >> flightNO >> flightname >> price >> date >> time;
        while (!data.eof())
        {
            cout << flightNO << "\t\t" << flightname << "\t\t\t  " << price << "\t\t" << date << "\t" << time << endl;
            data >> flightNO >> flightname >> price >> date >> time;
        }
        data.close();
    }
}
void Airline::ticket()
{
m:
    fstream data;
    int arrc[100];
    int q,i=0;
    char choice;
    int c = 0;
    float total = 0;
    cout << "\n\n\t    Available Flight  ";
    data.open("airfile.txt", ios::in);
    if (!data)
    {
        cout << "\n\n Empty airfile , NO ticket availble ...";
        return;
    }
    else
    {
        data.close();
        list();
        cout << "\n_______________________________\n";
        cout << "\n     Buy AirTicket From Here     \n";
        cout << "\n_______________________________\n";
        do
        {
            cout << "Enter Flight   number : ";
            cin >> arrc[c];
            cout << "\n\n Quantity of ticket  :";
            cin >> q;
            cout << "\n\n DO you want to change anything else  ? If yes then press y else n : ";
            cin >> choice;
        } while (choice == 'y');
        string p[q];
        string g[q];
       if(q>1)
       for(i=0; i<q ; i++)
       {
        cout << " \n\t\t Enter passanger name "  << i +1  << " : ";
        cin >> p[i];
        cout << " \n\t\t Enter Gender p       "<<i+1<< " :";
        cin>> g[i];
       }
       else
       {
        cout << " \n\t\t Enter passanger name " << " : ";
        cin >> p[i];
       }

        cout << " \n\n\t\t\t ________________Print ticket_____________\n\n";
        int i = 0;
        data.open("airfile.txt", ios::in);
        data >> flightNO >> flightname >> price >> date >> time;

        while (!data.eof())
        {
            if (flightNO == arrc[i])

            {
                if(q>1)
                for(int i=0; i<q ; i++)
                {
                cout << "\nPassanger name    "<<i+1<<" : ";
                cout<< p[i];
                cout << "\n Gender p        "<<i+1<<"  :";
                cout<< g[i];
                }
                else
                {
                cout << "\nPassanger name " <<": ";
                cout << p[0];
                cout << "\nGender              : \t";
                }
                cout << "\nFlight destination  : \t" << flightname;
                cout << "\nTicket No           : \t" << flightNO;
                cout << "\nTime                : \t" << time;
                cout << "\nDate                : \t" << date;
                cout << "\n\nTotal paid        : \t" << price * q;
            }
            data >> flightNO >> flightname >> price >> date >> time;
        }

        data.close();
    }
}
int main()
{
    Airline s;
    s.menu();
}
