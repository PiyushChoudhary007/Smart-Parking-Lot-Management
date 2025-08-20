class Car:
    def __init__(self, reg_no, owner):
        self.reg_no = reg_no
        self.owner = owner
        self.next = None   # Self-referential link

class ParkingLot:
    def __init__(self, capacity):
        self.capacity = capacity
        self.size = 0
        self.head = None

    def park_car(self, reg_no, owner):
        if self.size >= self.capacity:
            print("Parking Lot Full! Cannot add new car.")
            return

        new_car = Car(reg_no, owner)
        if not self.head:
            self.head = new_car
        else:
            current = self.head
            while current.next:
                current = current.next
            current.next = new_car
        self.size += 1
        print(f"Car {reg_no} parked successfully.")

    def exit_car(self, reg_no):
        if not self.head:
            print("Parking Lot is empty.")
            return

        if self.head.reg_no == reg_no:
            self.head = self.head.next
            self.size -= 1
            print(f"Car {reg_no} exited successfully.")
            return

        current = self.head
        while current.next and current.next.reg_no != reg_no:
            current = current.next

        if current.next:
            current.next = current.next.next
            self.size -= 1
            print(f"Car {reg_no} exited successfully.")
        else:
            print(f"Car {reg_no} not found in the lot.")

    def display_parking_lot(self):
        if not self.head:
            print("Parking Lot is empty.")
            return
        print("\n🚘 Current Parked Cars:")
        current = self.head
        slot = 1
        while current:
            print(f"Slot {slot}: {current.reg_no} (Owner: {current.owner})")
            current = current.next
            slot += 1
        print(f"📊 Total Occupied: {self.size}/{self.capacity}")


# -------- MENU BASED PROGRAM --------
if __name__ == "__main__":
    capacity = int(input("Enter total parking slots: "))
    lot = ParkingLot(capacity)

    while True:
        print("\n====== Smart Parking Lot Manager ======")
        print("1. Park Car")
        print("2. Exit Car")
        print("3. Show Parked Cars")
        print("4. Exit")

        choice = input("Choose option: ")

        if choice == "1":
            reg_no = input("Enter Car Registration Number: ")
            owner = input("Enter Owner Name: ")
            lot.park_car(reg_no, owner)

        elif choice == "2":
            reg_no = input("Enter Car Registration Number to Exit: ")
            lot.exit_car(reg_no)

        elif choice == "3":
            lot.display_parking_lot()

        elif choice == "4":
            print("Exiting Smart Parking Manager...")
            break

        else:
            print("Invalid choice! Please try again.")
