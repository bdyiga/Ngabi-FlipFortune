# CardG-Game
This repository is for my card guessing game.

Card Guessing Game Design Document

1. Introduction
   
1.1 Purpose
This document outlines the design and implementation of a text-based Card Guessing Game. It serves as a comprehensive guide for developers, detailing the game's structure, mechanics, and features.


1.2 Scope
The Card Guessing Game is a Python-based application that offers both basic and advanced gameplay modes, challenging players to guess various attributes of playing cards.
3. Game Overview
2.1 Basic Gameplay (CardGuessingGame Class)
Players attempt to guess three attributes of a randomly drawn card:
Color (Red or Black)
Position (Higher or Lower than the previous card)
Suit (Spades, Diamonds, Hearts, or Clubs)
Points are awarded for correct guesses, and players can continue playing rounds until they choose to stop.
2.2 Advanced Gameplay (AdvancedCardGuessingGame Class)
Extends the basic game with additional features:
Multiple difficulty levels (Easy, Medium, Hard)
Lives system
Time limits for guesses and overall gameplay
Card history guessing (Hard mode only)
4. Technical Specifications
3.1 Programming Language
Python 3.x
3.2 Required Libraries
random: For generating random card selections
time: For implementing time-based features
threading: For potential future enhancements in timed input
3.3 Class Structure
3.3.1 CardGuessingGame (Base Class)
Attributes:
points: Player's score
position_list: List of card positions
suits: Dictionary of card colors and suits
current_card: Currently drawn card
Methods:
draw_card(): Generates a random card
guess_color(): Handles color guessing
guess_position(): Handles position guessing
guess_suit(): Handles suit guessing
play_round(): Manages a single round of play
play_game(): Controls the overall game flow
3.3.2 AdvancedCardGuessingGame (Derived Class)
Additional Attributes:
card_history: List of previously drawn cards
difficulty: Selected game difficulty
lives: Number of player lives
guess_time_limit: Time limit for each guess
total_game_time: Overall time limit for the game
start_time: Game start timestamp
Additional/Overridden Methods:
timed_input(): Implements time-limited user input
make_guess(): Processes guesses with timing and life management
guess_card_history(): Implements history guessing feature
play_round(): Enhanced version with difficulty features
play_game(): Advanced game flow control
5. Gameplay Mechanics
4.1 Card Representation
Colors: Red, Black
Positions: 2-10, Jack, Queen, King, Ace
Suits: Spades, Clubs, Hearts, Diamonds
4.2 Scoring System
1 point per correct guess
"SUPER WIN" achieved for all correct guesses in a round
4.3 Advanced Mode Features
Difficulty Levels:
Easy: 5 lives, 15 seconds per guess, 3 minutes total
Medium: 3 lives, 10 seconds per guess, 2 minutes total
Hard: 2 lives, 7 seconds per guess, 1 minute total
Time-limited guesses
Overall game time limit
Card history guessing (Hard mode)
6. User Interface
5.1 Input Handling
Text-based input via console
Capitalization handling for user inputs
5.2 Output Display
Clear text prompts for each guess
Immediate feedback on guess correctness
Display of current score, remaining time, and lives
7. Game Flow
6.1 Basic Mode
Initialize game
Draw a card
Player guesses color
Player guesses position (higher/lower)
Player guesses suit
Update score
Ask to play another round or end game
6.2 Advanced Mode
Select difficulty
Initialize game with difficulty settings
Play rounds with time limits and life system
Include card history guessing in Hard mode
End game when time expires or lives run out
8. Error Handling and Edge Cases
7.1 Input Validation
Capitalize user inputs for consistent comparison
Handle timeout scenarios in advanced mode
7.2 Empty Card Attributes
Error handling for potential empty card attribute lists
9. Future Enhancements
8.1 Short-term Improvements
Implement a high score system
Add more detailed statistics (e.g., guess accuracy percentages)
8.2 Long-term Goals
Develop a graphical user interface
Implement multiplayer functionality
Create mobile app versions
10. Conclusion
The Card Guessing Game provides an engaging, scalable platform for players to test their luck and intuition with playing cards. Its modular design allows for easy expansion and modification, providing a solid foundation for future development and feature additions.







