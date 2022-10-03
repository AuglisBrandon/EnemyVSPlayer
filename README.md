# EnemyVSPlayer
This code allows users to create there own "Hero" and face off against a "Enemy" of their choice. A fun little project I worked on with a teammate in college.





Here is the initial code. <br/>
#!/usr/bin/env python
# Program By: Micah Lemoine & Brandon Auglis
# File Name: H6_Player_Vs_Enemy.py
# Function: This program creates Player and Enemy classes and has objects from each class interact

class Player:
    """Allow user to create a player fighter object, and to interact with an object of the Enemy subclass.

    Instance attributes:
    name : str
        object name
    health : int
        object health -- the amount of damage that can be sustained
    damage : int
        object damage inflicted
    defense : int
        object defense against damage

    Methods:
    __init__(self):
        Create object and set attributes to default values.
    character_create(self):
        Prompt user to input values for class attributes and instantiate new object.
    attack(self, enemy):
        Take in object of Enemy subclass and calculate an outcome based on the attributes of Enemy and Player objects.
        Print the outcome of the objects' interaction to the screen.
    """

    def __init__(self, name='Default', health=75, damage=20, defense=10):
        """Instantiate Player object with default values."""
        self.name, self.health, self.damage, self.defense = name, health, damage, defense

    def character_create(self):
        """Take in user input and assign to class attributes, then instantiate new Player object.

        Input validation performed to ensure inputted values are greater than zero and less than specified value.
        Print a message confirming character creation to the user.
        """
        self.name = input("Please enter your player's name: ")
        # Ensure user input is numeric and is within the specified range
        self.health = input("Please enter your player’s health (from 1 to 100): >")
        while not self.health.isnumeric():
            print(f"Invalid health input. {self.health} is not a number from 1 to 100")
            self.health = input("Please enter your player’s health (from 1 to 100): >")
        self.health = int(self.health)
        while self.health not in range(1, 101):
            print(f"Invalid health input. {self.health} is not a number from 1 to 100")
            self.health = int(input("Please enter your player’s health (from 1 to 100): >"))
        self.damage = input("Please enter your player’s damage (from 1 to 25): >")
        while not self.damage.isnumeric():
            print(f"Invalid damage input. {self.damage} is not a number from 1 to 25")
            self.damage = input("Please enter your player’s damage (from 1 to 25): >")
        self.damage = int(self.damage)
        while self.damage not in range(1, 26):
            print(f"Invalid damage input. {self.damage} is not a number from 1 to 25")
            self.damage = int(input("Please enter your player’s damage (from 1 to 25): >"))
        self.defense = input("Please enter your player’s defense (from 1 to 15): >")
        while not self.defense.isnumeric():
            print(f"Invalid defense input. {self.defense} is not a number from 1 to 15")
            self.defense = input("Please enter your player’s defense (from 1 to 15): >")
        self.defense = int(self.defense)
        while self.defense not in range(1, 16):
            print(f"Invalid defense input. {self.defense} is not a number from 1 to 15")
            self.defense = int(input("Please enter your player’s defense (from 1 to 15): >"))
        # Create Player object based on user input
        player_1 = Player(self.name, self.health, self.damage, self.defense)

        # Display the created Player object to the user
        print("\nYour Player has been saved with the following information:")
        print(f"Name:    {player_1.name:>10}\nHealth:  {player_1.health:>10}"
              f"\nDamage:  {player_1.damage:>10}\nDefense: {player_1.defense:>10}")

    def attack(self, enemy):
        """Take in object of Enemy subclass, calculate and print the outcome of an interaction between parent and child objects.

        Enemy defense is converted to a percentage, and damage inflicted upon enemy is reduced by this percentage. Damage
        inflicted is then subtracted from enemy health to yield updated enemy health.
        The outcome of the objects' interaction is printed to the screen.
        """
        enemy.health = int(enemy.health - (self.damage * (1 - enemy.defense / 100)))
        if enemy.health > 0:
            print(f"\n{self.name} attacked the enemy, causing {self.damage} damage!\nEnemy's health is now "
                  f"{enemy.health}")
        elif enemy.health <= 0:
            print(f"\n{self.name} attacked the enemy, causing {self.damage} damage!\nEnemy is dead!")


# In[17]:


class Enemy(Player):
    """Allows users to create and toggle different aspects of the enemy object which will in turn,
    interact with the created player object"""

    def __init__(self, name='Enemy', health=30, damage=10, defense=5, enemy_type='Demigorgan'):
        self.enemy_type = enemy_type
        super().__init__(name, health, damage, defense)

    def character_create(self):
        """Overload parent method to create one of three Enemy object variants based on user choice."""
        self.enemy_type = input("\nEnemy types: Vecna (hard), Demigorgan (normal), Demidog (easy)"
                                "\nPlease enter your enemy's type: >")
        self.enemy_type = self.enemy_type.lower()
        while self.enemy_type != 'vecna' and self.enemy_type != 'demigorgan' and self.enemy_type != 'demidog':
            print("\nInvalid enemy type. Please try again.")
            self.enemy_type = input("Enemy types: Vecna (hard), Demigorgan (normal), Demidog (easy)"
                                    "\nPlease enter your enemy's type: >")
            self.enemy_type = self.enemy_type.lower()
        if self.enemy_type == 'vecna':
            self.name, self.health, self.damage, self.defense, self.enemy_type = 'Enemy', 100, 30, 30, 'Vecna'
            elite = Enemy(self.name, self.health, self.damage, self.defense, self.enemy_type)
            print("\nYour enemy has been saved with the following information:")
            print(f"Type:    {self.enemy_type:>10}\nHealth:  {self.health:>10}\nDamage:  "
                  f"{self.damage:>10}\nDefense: {self.defense:>10}")
        elif self.enemy_type == 'demigorgan':
            self.name, self.health, self.damage, self.defense, self.enemy_type = 'Enemy', 40, 10, 5, 'Demigorgan'
            brawler = Enemy(self.name, self.health, self.damage, self.defense, self.enemy_type)
            print("\nYour enemy has been saved with the following information:")
            print(f"Type:    {self.enemy_type:>10}\nHealth:  {self.health:>10}\nDamage:  "
                  f"{self.damage:>10}\nDefense: {self.defense:>10}")
        elif self.enemy_type == 'demidog':
            self.name, self.health, self.damage, self.defense, self.enemy_type = 'Enemy', 20, 7, 5, 'Demidog'
            minion = Enemy(self.name, self.health, self.damage, self.defense, self.enemy_type)
            print("\nYour enemy has been saved with the following information:")
            print(f"Type:    {self.enemy_type:>10}\nHealth:  {self.health:>10}\nDamage:  "
                  f"{self.damage:>10}\nDefense: {self.defense:>10}")

    def attack(self, player):
        """Take in object of Player class, calculate and print the outcome of an interaction between parent and child objects.

        Player defense is converted to a percentage, and damage inflicted upon player is reduced by this percentage. Damage
        inflicted is then subtracted from enemy health to yield updated player health.
        The outcome of the objects' interaction is printed to the screen."""
        player.health = int(player.health - (self.damage - player.defense))
        if player.health > 0 and self.health > 0:
            print(f"Enemy attacked {player.name}, causing {self.damage} damage!\n"
                  f"{player.name}'s health is now {player.health}.")
        elif player.health <= 0:
            print(f"\nEnemy attacked {player.name}, causing {self.damage} damage!\n"
                  f"{player.name} is now dead!")
        else:
            print("Enemy has been neutralized. Game over!")


# In[18]:


def main():
    print("Player VS Enemy!")

    player1 = Player()
    player1.character_create()

    enemy1 = Enemy()
    enemy1.character_create()

    player1.attack(enemy1)
    enemy1.attack(player1)


if __name__ == '__main__':
    main()
