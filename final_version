import random
import time
import threading

class CardGuessingGame:
    def __init__(self):
        self.points = 0
        self.position_list = [2, 3, 4, 5, 6, 7, 8, 9, 10, "Jack", "Queen", "King", "Ace"]
        self.suits = {
            "Black": ["Spades", "Clubs"],
            "Red": ["Hearts", "Diamonds"]
        }
        self.current_card = self.draw_card()

    def draw_card(self):
        try:
            color = random.choice(list(self.suits.keys()))
            suit = random.choice(self.suits[color])
            position = random.choice(self.position_list)
            return {
                'color': color,
                'position': position,
                'suit': suit
            }
        except IndexError:
            print("Error: One of the card attribute lists is empty.")
            return None
        
    def guess_color(self):
        guess = input("Red or Black? ").capitalize()
        if guess == self.current_card['color']:
            self.points += 1
            print("Correct! You earned a point.")
        else:
            print(f"Sorry, the card was {self.current_card['color']}.")
            print(f"\nThe card drawn was:")
        print(f"{self.current_card['color']} {self.current_card['position']} {self.current_card['suit']}")
        print() 

    def guess_position(self):
        next_card = self.draw_card()
        guess = input("Higher or Lower? ").lower()
        current_position = self.position_list.index(self.current_card['position'])
        next_position = self.position_list.index(next_card['position'])
        
        if (guess == 'higher' and next_position > current_position) or \
           (guess == 'lower' and next_position < current_position):
            self.points += 1
            print("Correct! You earned a point.")
        else:
            print(f"Sorry, the next card was {next_card['position']}.")
        
        self.current_card = next_card

    def guess_suit(self):
        guess = input("What suit? (Spades/Diamonds/Hearts/Clubs) ").capitalize()
        if guess == self.current_card['suit']:
            self.points += 1
            print("Correct! You earned a point.")
        else:
            print(f"Sorry, the suit was {self.current_card['suit']}.")

    def play_round(self):
        initial_points = self.points
        
        self.guess_color()
        self.guess_position()
        self.guess_suit()
        # print(f"Current points: {self.points}")
        points_earned = self.points - initial_points
    
        print(f"Points earned this round: {points_earned}")
        
        if points_earned == 3:
            print("Congratulations! That's a SUPER WIN! You got all three guesses correct!")
        elif points_earned > 0:
            print("Nice job! You scored some points.")
        else:
            print("No points earned this round. Keep trying!")

        print(f"Current total points: {self.points}")



    def play_game(self):
        while True:
            self.play_round()
            play_again = input("Do you want to play another round? (yes/no) ").lower()
            if play_again != 'yes':
                break
        print(f"Game over! Your final score is: {self.points}")

#Advanced portion 

class AdvancedCardGuessingGame(CardGuessingGame):
    def __init__(self, difficulty='medium'):
        self.card_history = []
        super().__init__()
        self.difficulty = difficulty
        self.lives = 5 if difficulty == 'easy' else (3 if difficulty == 'medium' else 2)
        self.guess_time_limit = 15 if difficulty == 'easy' else (10 if difficulty == 'medium' else 7)
        

        
        
        if difficulty == 'easy':
            self.total_game_time = 180  # 3 minutes
        elif difficulty == 'medium':
            self.total_game_time = 120  # 2 minutes
        else:
            self.total_game_time = 60   # 1 minute
        
        self.start_time = time.time()

    def draw_card(self):
        card = super().draw_card()
        self.card_history.append(card)
        return card


    def timed_input(self, prompt):
        start_time = time.time()
        user_input = input(prompt)
        end_time = time.time()
        if end_time - start_time > self.guess_time_limit:
            print(f"Time's up! You took longer than {self.guess_time_limit} seconds.")
            return None
        return user_input


    def make_guess(self, prompt, correct_answer):
        guess = self.timed_input(prompt)
        if guess is None:
            self.lives -= 1
            print(f"Time's up! You lost a life. Lives remaining: {self.lives}")
            return False
        guess = guess.capitalize()
        if guess != correct_answer:
            self.lives -= 1
            print(f"Incorrect. You lost a life. Lives remaining: {self.lives}")
            return False
        else:
            self.points += 1
            print("Correct! You earned a point.")
            return True


    def guess_color(self):
        return self.make_guess("Red or Black? ", self.current_card['color'])

    def guess_position(self):
        next_card = self.draw_card()
        current_position = self.position_list.index(self.current_card['position'])
        next_position = self.position_list.index(next_card['position'])
        correct_answer = "Higher" if next_position > current_position else "Lower"
        result = self.make_guess("Higher or Lower? ", correct_answer)
        self.current_card = next_card  # Update current_card before returning
        return result

    def guess_suit(self):
        return self.make_guess("What suit? (Spades/Diamonds/Hearts/Clubs) ", self.current_card['suit'])

    def guess_card_history(self):
        if len(self.card_history) < 3:
            return True
        index = random.randint(0, len(self.card_history) - 3)
        card = self.card_history[index]
        return self.make_guess(f"What was the suit of the card drawn {len(self.card_history) - index} rounds ago? ", card['suit'])



    def play_round(self):
        print(f"\nNew card drawn. Make your guesses!")
        
        # Guess color
        if not self.guess_color():
            if self.lives <= 0:
                print("Game over! You've run out of lives.")
                return False
        print(f"The card is: {self.current_card['color']} {self.current_card['position']} of {self.current_card['suit']}")
        
        # Guess position
        next_card = self.draw_card()
        if not self.guess_position():
            if self.lives <= 0:
                print("Game over! You've run out of lives.")
                return False
        print(f"The new card is: {self.current_card['color']} {self.current_card['position']} of {self.current_card['suit']}")
        
        # Guess suit
        if not self.guess_suit():
            if self.lives <= 0:
                print("Game over! You've run out of lives.")
                return False
        print(f"The card is: {self.current_card['color']} {self.current_card['position']} of {self.current_card['suit']}")

        # For hard difficulty, guess card history
        if self.difficulty == 'hard':
            if not self.guess_card_history():
                if self.lives <= 0:
                    print("Game over! You've run out of lives.")
                    return False

        elapsed_time = time.time() - self.start_time
        if elapsed_time >= self.total_game_time:
            print("Time's up! The game has ended.")
            return False
        
        remaining_time = max(0, self.total_game_time - elapsed_time)
        print(f"Remaining time: {int(remaining_time)} seconds")
        print(f"Current score: {self.points} points")
        
        return True

    def play_game(self):
        print(f"You have {self.total_game_time} seconds to play and {self.lives} lives. Good luck!")
        while self.lives > 0:
            if not self.play_round():
                break
            play_again = input("Continue to next round? (yes/no) ").lower()
            if play_again != 'yes':
                break
        print(f"Game over! Your final score is: {self.points}")


if __name__ == "__main__":
    difficulty = input("Choose difficulty (easy/medium/hard): ").lower()
    game = AdvancedCardGuessingGame(difficulty)
    game.play_game()