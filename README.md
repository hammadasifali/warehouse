#include<iostream>
#include<string>
#include<fstream>
using namespace std;

struct warehouse {
	string name, supplier, brand;
	int price, quantity;
};

warehouse product[5];

void savedata() {
	ofstream myfile;
	myfile.open("product data.txt");
	if (!myfile.is_open()) {
		cout << "Error Opening File" << endl;
	}

	for (int i = 0; i < 5; i++) {
		myfile << "\t\t\tProduct Detail " << i + 1 << endl;
		myfile << "Product Name: " << product[i].name << endl;
		myfile << "Product Price: " << product[i].price << endl;
		myfile << "Product Supplier: " << product[i].supplier << endl;
		myfile << "Product Quantity: " << product[i].quantity << endl;
		myfile << "Product Brand: " << product[i].brand << endl;
		myfile << endl;
	}
	myfile.close();
}

void adddata() {
	for (int i = 0; i < 5; i++) {
		cin.ignore();
		cout << "Enter Product name: ";
		getline(cin, product[i].name);
		cout << "Enter Product price: ";
		cin >> product[i].price;
		cin.ignore();
		cout << "Enter The Supplier name: ";
		getline(cin, product[i].supplier);
		cout << "Enter Quantity: ";
		cin >> product[i].quantity;
		cin.ignore();
		cout << "Enter Brand name: ";
		getline(cin, product[i].brand);
		cout << endl;
	}
}

void search() {
	string search;
	cout << "Enter Product name for detail: ";
	cin.ignore();
	getline(cin, search);
	bool found = false;
	for (int i = 0; i < 5; i++) {
		if (product[i].name == search) {
			cout << "Product Name: " << product[i].name << endl;
			cout << "Product Price: " << product[i].price << endl;
			cout << "Product Supplier: " << product[i].supplier << endl;
			cout << "Product Quantity: " << product[i].quantity << endl;
			cout << "Product Brand: " << product[i].brand << endl;
			found = true;
			break;
		}
	}
	if (!found) {
		cout << "Data Not Found" << endl;
	}
}

void update() {
	string update;
	cout << "Enter Product Name to Update: ";
	cin.ignore();
	getline(cin, update);
	bool found = false;
	for (int i = 0; i < 5; i++) {
		if (product[i].name == update) {
			cout << "Enter Product price: ";
			cin >> product[i].price;
			cin.ignore();
			cout << "Enter The Supplier name: ";
			getline(cin, product[i].supplier);
			cout << "Enter Quantity: ";
			cin >> product[i].quantity;
			cin.ignore();
			cout << "Enter Brand name: ";
			getline(cin, product[i].brand);
			cout << endl;
			cout << "\t\t\t Updated Record" << endl;
			cout << "Product Name: " << product[i].name << endl;
			cout << "Product Price: " << product[i].price << endl;
			cout << "Product Supplier: " << product[i].supplier << endl;
			cout << "Product Quantity: " << product[i].quantity << endl;
			cout << "Product Brand: " << product[i].brand << endl;
			found = true;
			break;
		}
	}
	if (!found) {
		cout << "Data Not Found" << endl;
	}
}

void deleterecord() {
	string Delete;
	cout << "Enter Product Name to Delete: ";
	cin.ignore();
	getline(cin, Delete);
	bool found = false;
	for (int i = 0; i < 5; i++) {
		if (product[i].name == Delete) {
			for (int j = i; j < 4; j++) {
				product[j].name = product[j + 1].name;
				product[j].price = product[j + 1].price;
				product[j].supplier = product[j + 1].supplier;
				product[j].quantity = product[j + 1].quantity;
				product[j].brand = product[j + 1].brand;
			}
			cout << "Record Has Been Deleted" << endl;
			found = true;
			break;
		}
	}
	if (!found) {
		cout << "Record not Found" << endl;
	}
}

void display() {
	ifstream myfile;
	myfile.open("product data.txt");
	if (!myfile.is_open()) {
		cout << "Error Opening File" << endl;
	}
	else {
		string line;
		while (getline(myfile, line)) {
			cout << line << endl;
		}
		myfile.close();
	}
}

int main() {
	int choice;
	cout << "Welcome to The Ware House" << endl;
	do {
		cout << "1. To Enter data for Product" << endl;
		cout << "2. To Search for Specific Data" << endl;
		cout << "3. To Display The Record" << endl;
		cout << "4. To Update The Specific Data" << endl;
		cout << "5. To Delete The Specific Data" << endl;
		cout << "6. To Save Data permanently" << endl;
		cout << "7. To Exit" << endl;
		cout << "Enter Your Choice from 1-7: ";
		cin >> choice;
		switch (choice) {
		case 1:
			adddata();
			break;
		case 2:
			search();
			break;
		case 3:
			display();
			break;
		case 4:
			update();
			break;
		case 5:
			deleterecord();
			break;
		case 6:
			savedata();
			break;
		case 7:
			cout << "Exiting......" << endl;
			break;
		default:
			cout << "Invalid Choice!" << endl;
			break;
		}
	} while (choice != 7);

	return 0;
}
