import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;
import java.util.Timer;
import java.util.TimerTask;

public class SimpleQuizGame {
    static class QuizQuestion {
        String question;
        List<String> options;
        int correctAnswerIndex;

        QuizQuestion(String question, List<String> options, int correctAnswerIndex) {
            this.question = question;
            this.options = options;
            this.correctAnswerIndex = correctAnswerIndex;
        }
        boolean isCorrect(int answerIndex) {
            return answerIndex == correctAnswerIndex;
        }
    }
    public static void main(String[] args) {
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
        for (int i = 0; i < questions.size(); i++) {
            QuizQuestion q = questions.get(i);

            System.out.println("Question " + (i + 1) + ": " + q.question);
            for (int j = 0; j < q.options.size(); j++) {
                System.out.println((j + 1) + ". " + q.options.get(j));
            }
            Timer timer = new Timer();
            TimerTask task = new TimerTask() {
                @Override
                public void run() {
                    System.out.println("\nTime's up!");
                }
            };
            timer.schedule(task, 10000); 

            System.out.print("Your answer (1-" + q.options.size() + "): ");
            int userAnswer = scanner.nextInt();
            timer.cancel();
            if (q.isCorrect(userAnswer - 1)) {
                System.out.println("Correct!");
                score++;
            } else {
                System.out.println("Incorrect.");
            }
            System.out.println();
        }
        System.out.println("Quiz Finished!");
        System.out.println("Your score: " + score + "/" + questions.size());

        scanner.close();
    }
}
