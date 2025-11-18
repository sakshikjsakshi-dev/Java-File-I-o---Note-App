# Java-File-I-o---Note-App
import java.io.*;
import java.util.Scanner;

public class NotesApp {
    private static final String FILE_NAME = "notes.txt";

   public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int choice;

  do {
          System.out.println("\n==== Notes App ====");
            System.out.println("1. Write Note");
            System.out.println("2. View Notes");
            System.out.println("3. Exit");
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();
            scanner.nextLine();  

  switch (choice) {
                case 1: writeNotes(scanner); break;
                case 2: viewNotes(); break;
              case 3: System.out.println("Exiting..."); break;
                default: System.out.println("Invalid choice!");
            }
        } while (choice != 3);
        
  scanner.close();
    }
    private static void writeNotes(Scanner scanner) {
        System.out.print("Enter your note: ");
        String note = scanner.nextLine();

  try (FileWriter writer = new FileWriter(FILE_NAME, true)) {
            writer.write(note + "\n");
            System.out.println("Note saved successfully!");
        } catch (IOException e) {
            System.out.println("Error writing to file!");
        }
    }
    private static void viewNotes() {
        try (FileReader reader = new FileReader(FILE_NAME);
             BufferedReader br = new BufferedReader(reader)) {

 System.out.println("\n--- Your Notes ---");
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println("- " + line);
            }
        } catch (FileNotFoundException e) {
            System.out.println("No notes found! Write a note first.");
        } catch (IOException e) {
            System.out.println("Error reading file!");
        }
    }
}
