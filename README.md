# Task2i
#include <iostream>
using namespace std;
#include <string>
using namespace std;

string orders[50] = {
        "101", "102", "103", "104", "105", "106", "107", "108", "109", "110",
        "0", "0", "0", "0", "0", "0", "0", "0", "0", "0",
        "0", "0", "0", "0", "0", "0", "0", "0", "0", "0",
        "0", "0", "0", "0", "0", "0", "0", "0", "0", "0",
        "0", "0", "0", "0", "0", "0", "0", "0", "0", "0"
};
string cnames[50] = {"Thabo","Lerato","Nomvula","Sipho","Bongani","Lindiwe","Jabulani","Ayanda","Kgosi","Refilwe"};
int noofmag[50] = {3,5,2,4,6,1,3,2,6,4};
float torders[50] = {15.75,30.50,10.00,22.00,40.25,5.50,18.00,12.75,28.00,24.50};
int len = 10;
int main() {
    int option = 0;
    while (true){
        cout << "Order Management" << endl;
        cout << "1. Add a new order" << endl;
        cout << "2. Display all orders" << endl;
        cout << "3. Find an order by order ID" << endl;
        cout << "4. Calculate total revenue" << endl;
        cout << "5. Exit" << endl;
        cout << "Enter you choice(1-5): ";
        cin >> option;
        if(option == 1)
        {int idnumber;
        if (len != 50)
        {
            idnumber = stoi(orders[len-1])+1;
            cout << "Enter ID: "<<idnumber<<endl;
            orders[len] = to_string(idnumber);

            cout << "Enter Customer Name: ";
            cin>> cnames[len];

            cout << "Enter Number of Magwinyas Ordered: ";
            cin>> noofmag[len];

            cout << "total: ";
            cin>> torders[len];
            cout<<"Entry successful!"<<endl;

            len = len +1;
        } else
            cout << "No more space in array"<< endl;
        }
        else if (option == 2 )
        {cout<<"All oders";
        for (int i = 0; i <=49; i++){
            if (orders[i] != "0"){
                cout<<"ID: "<<orders[i],
                cout<<"Customer Name: "<<cnames[i],
                cout<<"No of mag"<<noofmag[i],
                cout<<"Total: "<<torders[i];
                cout<<""<<endl;
            }
        }
        }
        else if (option == 3 )
        {}
        else if (option == 4 )
        {}
        else if (option == 5 ) {
            cout << "program closed" << endl;
            exit(0);
        }

        else
            cout << "Invalid Option, Choose (1-5)"<<endl;
    }
    return 0;
}
