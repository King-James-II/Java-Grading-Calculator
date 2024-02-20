/**
 * This program takes user input of quiz grades up to 10 total grades then computes the average.
 * It displays each quiz grade entered, the average as well as the letter grade. 
 */
// Importing necessary libraries to accomplish the tasks needed in this program.
import java.util.Arrays;
import java.util.InputMismatchException;
import java.util.Scanner;
public class GradingCalculator {
// Main method calls all methods within the program.
	public static void main(String[] args) {
		// Initialize array with the input data using the inputGrades method.
		int[] quizScores = inputGrades();
		// Print all of the input quiz score values stored within the quizScores array.
		printGrades(quizScores);
		// Only call the computeAverage method and getLetterGrade method if values were
		// entered to avoid divide by zero exception.
		if (quizScores.length > 0) {
			// Call computeAverage method and save the average value and print it.
			int average = computeAverage(quizScores);
			System.out.println("\n------------------------\nQuiz grade average:" 
					+ average);
			// Call the getLetterGrade function to determine the letterGrade of the average
			// and display it to the user. 
			char letterGrade = getLetterGrade(average);
			System.out.println("\nThis is a " + letterGrade + " average.");
		}
		// Display message and exit if user enters 999 to quit and no quiz scores were entered.
		else {
			System.out.println("No grades were entered. Quitting program.");
			System.exit(0);
		}
	}
	
	// inputGrade method takes input from user and stores it within an array.
	public static int[] inputGrades() {
		// Setting up variables needed and prompting user for input of quiz grades.
		Scanner scan = new Scanner(System.in);
		Boolean stop = false;
		int[] tempScores = new int[10];
		int count = 0;
		System.out.print("+----------------------+\n"
						+"| Test quiz Calculator |\n"
						+"+----------------------+\n\n"
						+"Please enter up to 10 quiz grades:\n"
						+"(Enter 999 when finished to quit.)\n");
		// Do this until user enters 999 to quit entering values or 10 values are entered. 
		while (stop == false) {
			// This for loop takes an input for each iteration and only increments when a valid
			// value is entered. (ie. Quiz score between 0-100)
			for (int i = 0; i < 10; i++) {
				// Try block to catch if a user enters any non integer value and display an error.
				try { 
					int score = scan.nextInt();
					// Stop processing of additional quiz grades when value is entered. 
					if (score == 999) {
						stop = true;
						break;
					}
					// Detect if score is valid and only move to the next element if so.
					if (score >= 0 && score <= 100 ) {
						tempScores[i]= score;
						count++;
					}
					else {
						System.out.println("Invalid input. Please enter a valid score");
						i--;
					}
				} catch (InputMismatchException e) {
						System.out.println("Invalid input. Please enter a valid score");
						i--;
						
				}
				if (i == 9) {
					stop = true;
					break;
				}
				// Continue scanning inputs if we haven't reached the 10th score. 
				else {
					scan.nextLine();
				}
			}
		}
		// Copy array elements for each value entered we use count so we only copy values entered.
		int [] scores = Arrays.copyOfRange(tempScores, 0, count);
		scan.close();
		return scores;
	}
	
	// printGrade method to loop through each element stored within the scores array.
	public static void printGrades (int[] scores) {
		// Print each quiz score to the console.
		for (int i = 0; i < scores.length; i++) {
			System.out.println("Quiz " + (i+1) + " grade: " + scores[i]);
		}
	}
	
	// Compute average method that adds all the grades and then divides by the number of elements
	// or grades entered by the user.
	public static int computeAverage(int[]scores) {
		int total = 0;
		int average;
		for (int i = 0; i < scores.length; i++) {
			total += scores[i];
		}
		average = total/scores.length;
		return average;
	}
	
	// getLetterGrade method returns a letter grade value based on the average score computed.
	public static char getLetterGrade(int avg) {
		// We divide the average by 10 and then return the letter grade cases shown below. 
		switch (avg / 10) {
			case 10:
			case 9:
				return 'A';
			case 8:
				return 'B';
			case 7:
				return 'C';
			case 6:
				return 'D';
			default:
				return 'F';
		}
	}
}
