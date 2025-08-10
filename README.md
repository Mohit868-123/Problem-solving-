# quiz_tool.py

class Question:
    def __init__(self, q_type, question, options, correct_answers, explanation):
        """
        q_type: "single", "multiple", "truefalse"
        question: The question text
        options: List of option strings (for True/False, use ["True", "False"])
        correct_answers: List of correct option indices (0-based)
        explanation: Text explaining the answer
        """
        self.q_type = q_type
        self.question = question
        self.options = options
        self.correct_answers = correct_answers
        self.explanation = explanation

def ask_question(q: Question):
    print("\n" + q.question)
    for i, opt in enumerate(q.options):
        print(f"{i+1}. {opt}")

    if q.q_type == "multiple":
        ans = input("Enter all correct option numbers separated by spaces: ")
        selected = [int(x)-1 for x in ans.split()]
    else:
        ans = input("Enter the option number: ")
        selected = [int(ans)-1]

    correct = set(selected) == set(q.correct_answers)
    if correct:
        print("✅ Correct!")
    else:
        print("❌ Wrong!")

    print("Explanation:", q.explanation)
    return correct, selected

def run_quiz():
    questions = [
        Question("single", "What is 2 + 2?", ["3", "4", "5"], [1], "2 + 2 equals 4."),
        Question("multiple", "Which are prime numbers?", ["2", "4", "7", "9"], [0, 2], "2 and 7 are prime numbers."),
        Question("truefalse", "The Earth is flat.", ["True", "False"], [1], "Scientific evidence shows the Earth is round."),
    ]

    score = 0
    review = []

    for q in questions:
        correct, selected = ask_question(q)
        if correct:
            score += 1
        review.append((q, selected, correct))

    print(f"\nFinal Score: {score}/{len(questions)}")
    print("\n--- Review ---")
    for q, selected, correct in review:
        print("\nQ:", q.question)
        print("Your answer:", [q.options[i] for i in selected])
        print("Correct answer:", [q.options[i] for i in q.correct_answers])
        print("Explanation:", q.explanation)

if __name__ == "__main__":
    run_quiz()
