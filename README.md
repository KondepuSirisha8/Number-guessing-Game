# Number-guessing-Game
The number guessing game is a simple interactive game where the player tries to guess a randomly generated number within a specified range. The game provides feedback on whether the guess is too high , or too low , correct.
#Code :
import streamlit as st
import random
if 'number' not in st.session_state:
    st.session_state.number = random.randint(1, 100)
if 'guesses' not in st.session_state:
    st.session_state.guesses = 0
if 'message' not in st.session_state:
    st.session_state.message = ""
if 'game_over' not in st.session_state:
    st.session_state.game_over = False
if 'user_guess' not in st.session_state:
    st.session_state.user_guess = ""

st.title("🎮 Number Guessing Game")
st.write("Guess the number between **1 and 100**. Type your guess and press **Enter**.")
def check_guess():
    try:
        guess = int(st.session_state.user_guess)
        st.session_state.guesses += 1
        if guess < st.session_state.number:
            st.session_state.message = "🔼 Try a higher number!"
        elif guess > st.session_state.number:
            st.session_state.message = "🔽 Try a lower number!"
        else:
            st.session_state.message = (
                f"🎉 You guessed it! The number was {st.session_state.number}.\n"
                f"It took you {st.session_state.guesses} attempts."
            )
            st.session_state.game_over = True
    except ValueError:
        st.session_state.message = "❌ Please enter a valid number."
    
    # Clear the input field
    st.session_state.user_guess = ""

if not st.session_state.game_over:
    st.text_input("Your Guess:", key="user_guess", on_change=check_guess)
    st.write(st.session_state.message)
else:
    st.success(st.session_state.message)
    if st.button("🔁 Play Again"):
        st.session_state.number = random.randint(1, 100)
        st.session_state.guesses = 0
        st.session_state.message = ""
        st.session_state.game_over = False
        st.session_state.user_guess = ""
