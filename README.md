import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class SimpleQuizGame {
    // Inner class to represent a quiz question
    static class QuizQuestion {
        String question;
        List<String> options;
        int correctAnswerIndex;

        QuizQuestion(String question, List<String> options, int correctAnswerIndex) {
            this.question = question;
            this.options = options;
            this.correctAnswerIndex = correctAnswerIndex;
        }

        // Check if the user's answer is correct
        boolean isCorrect(int answerIndex) {
            return answerIndex == correctAnswerIndex;
        }
    }

    // Main class to handle quiz game logic
    public static void main(String[] args) {
        // Initialize quiz questions
        List<QuizQuestion> questions = new ArrayList<>();
        questions.add(new QuizQuestion(
            "What is the capital of France?",
            List.of("Berlin", "Madrid", "Paris", "Lisbon"),
            2
        ));
        questions.add(new QuizQuestion(
            "Which planet is known as the Red Planet?",
            List.of("Earth", "Mars", "Jupiter", "Saturn"),
            1
        ));
        questions.add(new QuizQuestion(
            "What is the chemical symbol for gold?",
            List.of("Au", "Ag", "Pb", "Fe"),
            0
        ));

        Scanner scanner = new Scanner(System.in);
        int score = 0;

        // Iterate over each question
        for (int i = 0; i < questions.size(); i++) {
            QuizQuestion q = questions.get(i);

            System.out.println("Question " + (i + 1) + ": " + q.question);
            for (int j = 0; j < q.options.size(); j++) {
                System.out.println((j + 1) + ". " + q.options.get(j));
            }

            System.out.print("Your answer (1-" + q.options.size() + "): ");
            int userAnswer = scanner.nextInt() - 1; // Convert to 0-based index

            // Check if the answer is correct
            if (q.isCorrect(userAnswer)) {
                System.out.println("Correct!");
                score++;
            } else {
                System.out.println("Incorrect. The correct answer was option " + (q.correctAnswerIndex + 1));
            }
            System.out.println();
        }

        // Display the final score
        System.out.println("Quiz Finished!");
        System.out.println("Your score: " + score + "/" + questions.size());

        scanner.close();
    }
}
