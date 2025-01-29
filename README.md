class exoplanetNode:
    # Initializer ("constructor") method
    def __init__(self, name, OrbRadius, OrbPeriod, year, numJupiters):
        # Instance attributes
        self.next = None
        self.ID = name
        self.orbital_radius = OrbRadius
        self.orbital_period = OrbPeriod
        self.discovery_date = year
        self.mass = numJupiters

    # Remove the node after this one
    def remove_after(self):
        temp = self.next
        if temp is not None:
            self.next = temp.next
        return temp

    # Insert a new node after this one
    def insert_after(self, new_node):
        if not isinstance(new_node, exoplanetNode):
            return
        new_node.next = self.next
        self.next = new_node

    # String representation of the node
    def __str__(self):
        return (
            f"id: {self.ID}\n"
            f"Orbital Radius: {self.orbital_radius}\n"
            f"Orbital Period: {self.orbital_period}\n"
            f"Discovery Date: {self.discovery_date}\n"
            f"Mass: {self.mass}"
        )

# Main program to create and traverse the linked list
def main():
    # Create exoplanet nodes
    hd = exoplanetNode("--HD-191939-e", 0.397, 101.5, 2022, 0.33981)
    comae = exoplanetNode("11 Comae Berenices b", 1.29, 326, 2007, 19.4)
    ursae = exoplanetNode("11 Ursae Minoris b", 1.08, 101.5, 2009, 14.74)
    herculis = exoplanetNode("14 Herculis b", 2.1, 116.6, 2002, 4.66)

    # Link the nodes
    hd.next = comae
    comae.next = ursae
    ursae.next = herculis

    # Display all nodes in the list
    print("Exoplanet List:")
    current = hd
    while current:
        print(current)
        print("-" * 40)  # Separator for readability
        current = current.next

    # Task: Display the total mass of all exoplanets
    current = hd
    total_mass = 0
    while current:
        total_mass += current.mass
        current = current.next
    print(f"\nTotal mass of all exoplanets: {total_mass:.2f} Jupiters")

    # Task: Find and display an exoplanet by ID
    search_id = "11 Comae Berenices b"
    current = hd
    while current:
        if current.ID == search_id:
            print(f"\nExoplanet found:\n{current}")
            break
        current = current.next
    else:
        print(f"\nExoplanet with ID '{search_id}' not found.")

if __name__ == "__main__":
    main()
