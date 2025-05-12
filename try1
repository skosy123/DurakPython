import arcade
import random

# Screen title and size
SCREEN_WIDTH = 1024
SCREEN_HEIGHT = 768
SCREEN_TITLE = "Cards"

# Constants for sizing
CARD_SCALE = 0.6

CARD_WIDTH = 140 * CARD_SCALE
CARD_HEIGHT = 190 * CARD_SCALE

# play area size
MAT_PERCENT_OVERSIZE = 1.25
MAT_HEIGHT = int(CARD_HEIGHT * MAT_PERCENT_OVERSIZE)
MAT_WIDTH = int(CARD_WIDTH * MAT_PERCENT_OVERSIZE)

# play area margins
VERTICAL_MARGIN_PERCENT = 0.10
HORIZONTAL_MARGIN_PERCENT = 0.10


BOTTOM_Y = MAT_HEIGHT / 2 + MAT_HEIGHT * VERTICAL_MARGIN_PERCENT
START_X = MAT_WIDTH / 2 + MAT_WIDTH * HORIZONTAL_MARGIN_PERCENT

CARD_VALUES = ["A", "2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K"]
CARD_SUITS = ["Clubs", "Hearts", "Spades", "Diamonds"]


New_LIST = ["AHearts", "KHearts", "THearts", "9Hearts", "8Hearts", "7Hearts", "6Hearts", "5Hearts", "4Hearts", "3Hearts", "2Hearts", "ADiamonds", "KDiamonds", "TDiamonds", "9Diamonds", "8Diamonds", "7Diamonds", "6Diamonds", "5Diamonds", "4Diamonds", "3Diamonds", "2Diamonds", "ASpades", "KSpades", "TSpades", "9Spades", "8Spades", "7Spades", "6Spades", "5Spades", "4Spades", "3Spades", "2Spades","AClubs", "KClubs", "TClubs", "9Clubs", "8Clubs", "7Clubs", "6Clubs", "5Clubs", "4Clubs", "3Clubs", "2Clubs"]

random.shuffle(New_LIST)


class Card(arcade.Sprite):
    """ Card sprite """

    def __init__(self, suit, value, scale=1):
        self.suit = suit
        self.value = value
        self.image_file_name = f":resources:images/cards/card{self.suit}{self.value}.png"
        super().__init__(self.image_file_name, scale, hit_box_algorithm="None")
        



class MyGame(arcade.Window):
    """ Main application class. """

    def __init__(self):
        super().__init__(SCREEN_WIDTH, SCREEN_HEIGHT, SCREEN_TITLE)
        self.card_list = None
        self.background_color = arcade.color.GO_GREEN
        # List of cards we are dragging with the mouse
        self.held_cards = None

        # Original location of cards we are dragging with the mouse in case
        # they have to go back.
        self.held_cards_original_position = None

    def setup(self):
        """ Set up the game here. Call this function to restart the game. """
        
        # List of cards we are dragging with the mouse
        self.held_cards = []

        # Original location of cards we are dragging with the mouse in case
        # they have to go back.
        self.held_cards_original_position = []

        # cards list as an image list
        self.card_list = arcade.SpriteList()
        
        #i = 1
        #x = 25
        #for card_suit in CARD_SUITS:
            #for card_value in CARD_VALUES:
                #card = Card(card_suit, card_value, CARD_SCALE)
                #card.position = (START_X + x), (BOTTOM_Y)
                ##self.card_list.insert(randrange(52), card)
                #random_number = random.randrange(i)
                #self.card_list.insert(random_number, card)
                #i = i+1
                #x = x+20

        # create every card
        i = 25
        for new_cards in New_LIST:
            if new_cards[0] == "T":
                card = Card(new_cards[1:], CARD_VALUES[9], CARD_SCALE)
            else:
                card = Card(new_cards[1:], new_cards[0], CARD_SCALE)
            card.position = (START_X + i), (BOTTOM_Y + i)
            self.card_list.append(card)
            i = i+10
            
        
        
    def pull_to_top(self, card: arcade.Sprite):
        """ Pull card to top of rendering order (last to render, looks on-top) """

        # Remove, and append to the end
        self.card_list.remove(card)
        self.card_list.append(card)
        

    def on_draw(self):
        """ Render the screen. """
        # Clear the screen
        self.clear()
        #random.shuffle(self.card_list)
        self.card_list.draw()

    def on_mouse_press(self, x, y, button, key_modifiers):
        """ Called when the user presses a mouse button. """

        # Get list of cards we've clicked on
        cards = arcade.get_sprites_at_point((x, y), self.card_list)

        # Have we clicked on a card?
        if len(cards) > 0:

            # Might be a stack of cards, get the top one
            primary_card = cards[-1]

            # All other cases, grab the face-up card we are clicking on
            self.held_cards = [primary_card]
            # Save the position
            self.held_cards_original_position = [self.held_cards[0].position]
            # Put on top in drawing order
            self.pull_to_top(self.held_cards[0])

    def on_mouse_release(self, x: float, y: float, button: int,
                         modifiers: int):
        """ Called when the user presses a mouse button. """

        # If we don't have any cards, who cares
        if len(self.held_cards) == 0:
            return

        # We are no longer holding cards
        self.held_cards = []

    def on_mouse_motion(self, x: float, y: float, dx: float, dy: float):
        """ User moves mouse """

        # If we are holding cards, move them with the mouse
        for card in self.held_cards:
            card.center_x += dx
            card.center_y += dy


def main():
    """ Main function """
    window = MyGame()
    window.setup()
    arcade.run()


if __name__ == "__main__":
    main()

if __name__ == "__main__":
    main()
    
    
    
   
