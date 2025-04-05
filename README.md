# quiz_app
import pandas as pd

# Load quiz data
df = pd.read_csv('quiz_data.csv')

# Function to ask a question
def ask_question(question_data, question_number):
    print(f"\nQuestion {question_number + 1}: {question_data['question']}")
    options = [
        question_data['option_1'],
        question_data['option_2'],
        question_data['option_3'],
        question_data['option_4']
    ]
    
    # Display options
    for i, option in enumerate(options, 1):
        print(f"{i}. {option}")

    answer = input("Choose the correct answer (1/2/3/4): ")

    # Check if the answer is correct
    if options[int(answer) - 1] == question_data['correct_answer']:
        return True
    return False

# Function to run the quiz
def run_quiz():
    score = 0
    total_questions = len(df)

    # Ask each question
    for idx, row in df.iterrows():
        if ask_question(row, idx):
            print("Correct!")
            score += 1
        else:
            print(f"Wrong! The correct answer was: {row['correct_answer']}")

    print(f"\nQuiz Over! Your score: {score}/{total_questions}")

# Run the quiz
if __name__ == "__main__":
    print("Welcome to the Python Quiz!")
    run_quiz()
