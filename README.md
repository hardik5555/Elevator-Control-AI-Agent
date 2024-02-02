class Elevator:
    def __init__(self, num_floors):
        self.current_floor = 1
        self.num_floors = num_floors
        self.destination_floors = set()
        self.direction = 0  # 0 for stationary, 1 for up, -1 for down

    def request_floor(self, floor):
        if 1 <= floor <= self.num_floors:
            self.destination_floors.add(floor)
            self.move_elevator()

    def move_elevator(self):
        if self.direction == 0:
            if self.current_floor < min(self.destination_floors):
                self.direction = 1
            elif self.current_floor > max(self.destination_floors):
                self.direction = -1
            else:
                return

        self.current_floor += self.direction
        print(f"Elevator moving to floor {self.current_floor}")

        if self.current_floor in self.destination_floors:
            print(f"Elevator reached floor {self.current_floor}")
            self.destination_floors.remove(self.current_floor)

        if not self.destination_floors:
            self.direction = 0


def main():
    num_floors = 10  # Change this to the number of floors in your building
    elevator = Elevator(num_floors)

    while True:
        print("\nOptions:")
        print("1. Request floor")
        print("2. Quit")

        choice = input("Enter your choice: ")

        if choice == "1":
            floor = int(input("Enter the floor to go to: "))
            elevator.request_floor(floor)
        elif choice == "2":
            break
        else:
            print("Invalid choice. Try again.")


if __name__ == "__main__":
    main()
