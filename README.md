# cust365
"Beginner CRM app to manage customer data using Python and CSV files."

import csv

FILENAME = "customers.csv"

def create_customer():
    name = input("Enter customer name: ")
    email = input("Enter customer email: ")
    phone = input("Enter customer phone: ")

    with open(FILENAME, mode='a', newline='') as file:
        writer = csv.writer(file)
        writer.writerow([name, email, phone])
    print("✅ Customer added!")

def view_customers():
    print("\n--- Customer List ---")
    try:
        with open(FILENAME, mode='r') as file:
            reader = csv.reader(file)
            for row in reader:
                print(f"Name: {row[0]}, Email: {row[1]}, Phone: {row[2]}")
    except FileNotFoundError:
        print("No customers found yet.")

def search_customer():
    keyword = input("Enter name or email to search: ").lower()
    found = False
    try:
        with open(FILENAME, mode='r') as file:
            reader = csv.reader(file)
            for row in reader:
                if keyword in row[0].lower() or keyword in row[1].lower():
                    print(f"Found: Name: {row[0]}, Email: {row[1]}, Phone: {row[2]}")
                    found = True
        if not found:
            print("❌ Customer not found.")
    except FileNotFoundError:
        print("No customers found yet.")

def menu():
    while True:
        print("\n--- Customer 365 CRM ---")
        print("1. Add Customer")
        print("2. View All Customers")
        print("3. Search Customer")
        print("4. Exit")
        choice = input("Choose an option: ")

        if choice == '1':
            create_customer()
        elif choice == '2':
            view_customers()
        elif choice == '3':
            search_customer()
        elif choice == '4':
            break
        else:
            print("Invalid choice. Try again.")

menu()
