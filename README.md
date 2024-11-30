import java.util.HashMap;
import java.util.Scanner;

public class UserManagementSystem {
    private static HashMap<String, String> users = new HashMap<>();
    private static String loggedInUser = null;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int choice;

        do {
            System.out.println("\n=== User Management System ===");
            System.out.println("1. Register");
            System.out.println("2. Login");
            System.out.println("3. Logout");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1 -> registerUser(scanner);
                case 2 -> loginUser(scanner);
                case 3 -> logoutUser();
                case 4 -> System.out.println("Exiting the system. Goodbye!");
                default -> System.out.println("Invalid choice! Please try again.");
            }
        } while (choice != 4);

        scanner.close();
    }

    private static void registerUser(Scanner scanner) {
        System.out.print("Enter university email address: ");
        String email = scanner.nextLine();
        if (!email.endsWith("@university.edu")) {
            System.out.println("Invalid email! Please use your university email.");
            return;
        }

        if (users.containsKey(email)) {
            System.out.println("Email is already registered!");
            return;
        }

        System.out.print("Enter password: ");
        String password = scanner.nextLine();
        users.put(email, password);
        System.out.println("Registration successful!");
    }

    private static void loginUser(Scanner scanner) {
        if (loggedInUser != null) {
            System.out.println("Already logged in as " + loggedInUser);
            return;
        }

        System.out.print("Enter university email address: ");
        String email = scanner.nextLine();

        System.out.print("Enter password: ");
        String password = scanner.nextLine();

        if (users.containsKey(email) && users.get(email).equals(password)) {
            loggedInUser = email;
            System.out.println("Login successful! Welcome, " + email);
        } else {
            System.out.println("Invalid credentials! Please try again.");
        }
    }

    private static void logoutUser() {
        if (loggedInUser == null) {
            System.out.println("No user is logged in!");
        } else {
            System.out.println("Goodbye, " + loggedInUser);
            loggedInUser = null;
        }
    }
}
