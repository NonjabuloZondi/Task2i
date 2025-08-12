# Task2i
#include <iostream>
#include <string>
#include <iomanip>  // for fixed and setprecision
using namespace std;

string order_ids[50] = {
    "101","102","103","104","105","106","107","108","109","110",
    "0","0","0","0","0","0","0","0","0","0",
    "0","0","0","0","0","0","0","0","0","0",
    "0","0","0","0","0","0","0","0","0","0",
    "0","0","0","0","0","0","0","0","0","0"
};
string customer_names[50] = {"Thabo","Lerato","Nomvula","Sipho","Bongani","Lindiwe","Jabulani","Ayanda","Kgosi","Refilwe"};
int num_magwinyas[50] = {3,5,2,4,6,1,3,2,6,4};
float order_totals[50] = {15.75,30.50,10.00,22.00,40.25,5.50,18.00,12.75,28.00,24.50};
int order_count = 10;

int main(){
    int choice;
    while(true){
        cout << "\nOrder Management\n";
        cout << "1. Add a new order\n";
        cout << "2. Display all orders\n";
        cout << "3. Find an order by order ID\n";
        cout << "4. Calculate total revenue\n";
        cout << "5. Exit\n";
        cout << "Enter your choice (1-5): ";
        cin >> choice;

        if(choice == 1)
        {
            if(order_count < 50)
            {
                string id_input;
                cout << "Enter order ID: ";
                cin >> id_input;
                order_ids[order_count] = id_input;

                cout << "Enter Customer Name: ";
                cin >> customer_names[order_count];

                cout << "Enter Number of Magwinyas Ordered: ";
                cin >> num_magwinyas[order_count];

                float single_price;
                cout << "Enter single price per magwinya: ";
                cin >> single_price;

                order_totals[order_count] = num_magwinyas[order_count] * single_price;

                cout << fixed << setprecision(2);
                cout << "Total calculated automatically: " << order_totals[order_count] << endl;

                order_count++;
                cout << "Entry successful!" << endl;
            }
            else
                cout << "No more space in array" << endl;
        }
        else if(choice==2){
            cout << fixed << setprecision(2);
            for(int i=0;i<order_count;i++){
                if(order_ids[i]!="0"){
                    cout << "Order ID: " << order_ids[i] 
                         << ", Customer: " << customer_names[i] 
                         << ", number of magwinyas: " << num_magwinyas[i] 
                         << ", Total: " << order_totals[i] << endl;
                }
            }
        }
        else if(choice==3){
            string search_id;
            bool found=false;
            cout << "Enter order id to find: ";
            cin >> search_id;
            cout << fixed << setprecision(2);
            for(int i=0;i<order_count;i++){
                if(order_ids[i]==search_id){
                    cout << "Order ID: " << order_ids[i] 
                         << ", Customer: " << customer_names[i] 
                         << ", number of magwinyas: " << num_magwinyas[i] 
                         << ", Total: " << order_totals[i] << endl;
                    found=true;
                    break;
                }
            }
            if(!found){
                cout << "order with order id " << search_id << " not found\n";
            }
        }
        else if(choice==4){
            float total_revenue=0;
            for(int i=0;i<order_count;i++){
                total_revenue += order_totals[i];
            }
            cout << fixed << setprecision(2);
            cout << "total revenue : " << total_revenue << endl;
        }
        else if(choice==5){
            cout << "program closed\n";
            break;
        }
        else{
            cout << "Invalid Option, Choose (1-5)\n";
        }
    }
    return 0;
}
