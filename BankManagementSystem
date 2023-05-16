import java.io.*;
import java.util.*;

class User  {
    String username;
    String password;
    double balance;
    double fixedDeposit;

}

public class BankManagementSystem {
    static Scanner sc = new Scanner(System.in);
    static ArrayList<User> users = new ArrayList<>();
    static User currentUser;

    public static void main(String[] args) {
        createFile("users.txt");
        loadData(); // load existing user data from file
        login(); // ask for username and password
        while (true) {
            printMenu(); // display options
            int choice = sc.nextInt();
            switch (choice) {
                case 1:
                    viewBalance();
                    break;
                case 2:
                    withdraw();
                    break;
                case 3:
                    deposit();
                    break;
                case 4:
                    transferToFD();
                    break;
                case 5:
                    saveData(); // save user data to file and exit
                    return;
                default:
                    System.out.println("Invalid choice!");
            }
        }
    }

    // Load existing user data from file
    static void loadData() {
        try {
            File file = new File("users.txt");
            Scanner scanner = new Scanner(file);
            // skip the first line with column names

            while (scanner.hasNextLine()) {
                String line = scanner.nextLine();
                String[] tokens = line.split(",");
                User user = new User();
                user.username = tokens[0];
                user.password = tokens[1];
                user.balance = Double.parseDouble(tokens[2]);
                user.fixedDeposit = Double.parseDouble(tokens[3]);
                users.add(user);
            }
            scanner.close();
            System.out.println("User data loaded from file.");
        } catch (IOException e) {
            System.out.println("Error while loading user data: " + e.getMessage());
        } catch (NumberFormatException e) {
            System.out.println("Error while parsing user data: " + e.getMessage());
        }
    }


    // Save user data to file
    static void saveData() {
        try {
            PrintWriter writer = new PrintWriter("users.txt");
            writer.println("username,password,balance,fixedDeposit");
            for (User user : users) {
                writer.println(user.username + "," + user.password + "," + user.balance + "," + user.fixedDeposit);
            }
            writer.close();
            System.out.println("User data saved to file.");
            System.out.println(" Thank you for using our password generator system. Goodbye!");
        } catch (IOException e) {
            System.out.println("Error while saving user data: " + e.getMessage());
        }
    }


    // Ask for username and password and login
    static void login() {
        System.out.println("Enter username:");
        String username = sc.next();
        System.out.println("Enter password:");
        String password = sc.next();
        boolean found = false;
        for (User user : users) {
            if (user.username.equals(username) && user.password.equals(password)) {
                currentUser = user;
                System.out.println("Welcome, " + currentUser.username + "!");
                found = true;
                break;
            }
        }
        if (!found) {
            System.out.println("User not found. Creating new account.");
            createUser(username, password);
        }
    }

    // Create new user account with initial balance
    static void createUser(String username, String password) {
        User newUser = new User();
        newUser.username = username;
        newUser.password = password;
        System.out.println("Enter initial balance:");
        newUser.balance = sc.nextDouble();
        users.add(newUser);
        currentUser = newUser;
    }

    // Display account balance with interest
    static void viewBalance() {
        double interestRate = 0.01; // 1% per annum
        double interest = currentUser.balance * interestRate / 12; // monthly interest
        currentUser.balance += interest;
        System.out.println("Account balance: " + currentUser.balance);
    }

    // Withdraw money from account
    static void withdraw() {
        System.out.println("Enter amount to withdraw:");
        double amount = sc.nextDouble();
        if (amount <= currentUser.balance) {
            currentUser.balance -= amount;
            System.out.println("Withdrawn successfully.");
            System.out.println("Remaining balance: " + currentUser.balance);
        } else {
            System.out.println("Insufficient balance.");
        }
    }
    static void createFile(String filename) {
        try {
            File file = new File(filename);
            file.createNewFile();
        } catch (IOException e) {
            System.out.println("An error occurred while creating the file: " + filename);
            e.printStackTrace();
        }
    }

    // Deposit money into account
    static void deposit() {
        System.out.println("Enter amount to deposit:");
        double amount = sc.nextDouble();
        currentUser.balance += amount;
        System.out.println("Deposited successfully.");
        System.out.println("Updated balance: " + currentUser.balance);
    }

    // Transfer money from balance to fixed deposit
    static void transferToFD() {
        System.out.println("Enter amount to transfer:");
        double amount = sc.nextDouble();
        if (amount <= currentUser.balance) {
            currentUser.balance -= amount;
            currentUser.fixedDeposit += amount;
            System.out.println("Transferred successfully.");
            System.out.println("Remaining balance: " + currentUser.balance);
        } else {
            System.out.println("Insufficient balance.");
        }
    }

    // Display menu of options
    static void printMenu() {
        System.out.println("Select an option:");
        System.out.println("1. View balance");
        System.out.println("2. Withdraw money");
        System.out.println("3. Deposit money");
        System.out.println("4. Transfer money to fixed deposit");
        System.out.println("5. Exit");
    }
}
