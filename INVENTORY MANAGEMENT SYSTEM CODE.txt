#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_ITEMS 100

// Define the item structure
typedef struct {
    char name[50];
    int quantity;
    float price;
} item;

// Declare the inventory array
item inventory[MAX_ITEMS];

// Declare the current number of items in the inventory
int num_items = 0;

// Add a new item to the inventory
void add_item() {
    if (num_items == MAX_ITEMS) {
        printf("Inventory is full. Cannot add any more items.\n");
        return;
    }
    
    item new_item;
    
    printf("Enter the name of the item: ");
    scanf("%s", new_item.name);
    
    printf("Enter the quantity of the item: ");
    scanf("%d", &new_item.quantity);
    
    printf("Enter the price of the item: ");
    scanf("%f", &new_item.price);
    
    inventory[num_items] = new_item;
    num_items++;
    
    printf("Item added successfully.\n");
}

// Remove an item from the inventory
void remove_item() {
    if (num_items == 0) {
        printf("Inventory is empty. Cannot remove any items.\n");
        return;
    }
    
    char item_name[50];
    
    printf("Enter the name of the item to remove: ");
    scanf("%s", item_name);
    
    int index = -1;
    
    for (int i = 0; i < num_items; i++) {
        if (strcmp(inventory[i].name, item_name) == 0) {
            index = i;
            break;
        }
    }
    
    if (index == -1) {
        printf("Item not found in inventory.\n");
        return;
    }
    
    for (int i = index; i < num_items - 1; i++) {
        inventory[i] = inventory[i + 1];
    }
    
    num_items--;
    
    printf("Item removed successfully.\n");
}

// Display the current inventory
void display_inventory() {
    if (num_items == 0) {
        printf("Inventory is empty.\n");
        return;
    }
    
    printf("Current inventory:\n");
    printf("Name\tQuantity\tPrice\n");
    
    for (int i = 0; i < num_items; i++) {
        printf("%s\t%d\t\t%.2f\n", inventory[i].name, inventory[i].quantity, inventory[i].price);
    }
}

int main() {
    int choice;
    
    do {
        printf("\n1. Add item to inventory\n");
        printf("2. Remove item from inventory\n");
        printf("3. Display inventory\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        
        switch (choice) {
            case 1:
                add_item();
                break;
            case 2:
                remove_item();
                break;
            case 3:
                display_inventory();
                break;
            case 4:
                printf("Exiting program.\n");
                break;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    } while (choice != 4);
    
    return 0;
}