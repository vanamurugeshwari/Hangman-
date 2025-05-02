# Hangman-import random

class Hangman:
    def __init__(self, word_list):
        self.word_list = word_list
        self.word = random.choice(word_list).upper()
        self.guessed = set()
        self.lives = 6
        self.stages = [
            """
             ------
             |    |
             |    O
             |   /|\\
             |   / \\
             |
            --------
            """,
            """
             ------
             |    |
             |    O
             |   /|\\
             |   / 
             |
            --------
            """,
            """
             ------
             |    |
             |    O
             |   /|\\
             |    
             |
            --------
            """,
            """
             ------
             |    |
             |    O
             |   /|
             |    
             |
            --------
            """,
            """
             ------
             |    |
             |    O
             |    |
             |    
             |
            --------
            """,
            """
             ------
             |    |
             |    O
             |    
             |    
             |
            --------
            """,
            """
             ------
             |    |
             |    
             |    
             |    
             |
            --------
            """
        ]

    def display_word(self):
        return ' '.join([letter if letter in self.guessed else '_' for letter in self.word])

    def play(self):
        print("Welcome to Hangman!")
        while self.lives > 0 and set(self.word) != self.guessed:
            print(self.stages[6 - self.lives])
            print(f"Word: {self.display_word()}")
            print(f"Guessed letters: {', '.join(sorted(self.guessed))}")
            guess = input("Guess a letter: ").upper()

            if guess in self.guessed:
                print("You already guessed that letter.")
            elif guess in self.word:
                print("Good guess!")
                self.guessed.add(guess)
            else:
                print("Wrong guess.")
                self.guessed.add(guess)
                self.lives -= 1

        if set(self.word) == self.guessed:
            print(f"Congratulations! You guessed the word: {self.word}")
        else:
            print(self.stages[6])
            print(f"You lost. The word was: {self.word}")

# Example usage
words = ["python", "hangman", "challenge", "game"]
game = Hangman(words)
game.play()
