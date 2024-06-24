package sectiona.customerrelationshipmanagement;

import java.util.Scanner;
import java.util.ArrayList;
import java.util.List;

class Customer {
    private int id;
    private String name;
    private String email;
    private String phone;
    private List<String> interactions;
    private List<String> feedbacks;

    public Customer(int id, String name, String email, String phone) {
        this.id = id;
        this.name = name;
        this.email = email;
        this.phone = phone;
        this.interactions = new ArrayList<>();
        this.feedbacks = new ArrayList<>();
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public String getEmail() {
        return email;
    }

    public String getPhone() {
        return phone;
    }

    public void addInteraction(String interaction) {
        interactions.add(interaction);
    }

    public List<String> getInteractions() {
        return interactions;
    }

    public void addFeedback(String feedback) {
        feedbacks.add(feedback);
    }

    public List<String> getFeedbacks() {
        return feedbacks;
    }

    @Override
    public String toString() {
        return "Customer ID: " + id + ", Name: " + name + ", Email: " + email + ", Phone: " + phone;
    }
}

class InteractionHistory {
    public void recordInteraction(Customer customer, String interaction) {
        customer.addInteraction(interaction);
        System.out.println("Interaction recorded for customer " + customer.getId() + ": " + interaction);
    }

    public void displayInteractions(Customer customer) {
        List<String> interactions = customer.getInteractions();
        if (interactions.isEmpty()) {
            System.out.println("No interactions found for customer " + customer.getId());
        } else {
            System.out.println("Interactions for customer " + customer.getId() + ":");
            for (String interaction : interactions) {
                System.out.println(interaction);
            }
        }
    }
}

class FeedbackManager {
    public void addFeedback(Customer customer, String feedback) {
        customer.addFeedback(feedback);
        System.out.println("Feedback added for customer " + customer.getId() + ": " + feedback);
    }

    public void displayFeedbacks(Customer customer) {
        List<String> feedbacks = customer.getFeedbacks();
        if (feedbacks.isEmpty()) {
            System.out.println("No feedbacks found for customer " + customer.getId());
        } else {
            System.out.println("Feedbacks for customer " + customer.getId() + ":");
            for (String feedback : feedbacks) {
                System.out.println(feedback);
            }
        }
    }
}

class CRMSystem {
    private List<Customer> customers;
    private int nextId;
    private InteractionHistory interactionHistory;
    private FeedbackManager feedbackManager;

    public CRMSystem() {
        customers = new ArrayList<>();
        nextId = 1;
        interactionHistory = new InteractionHistory();
        feedbackManager = new FeedbackManager();
    }

    public void addCustomer(String name, String email, String phone) {
        Customer customer = new Customer(nextId++, name, email, phone);
        customers.add(customer);
        System.out.println("Customer added: " + customer);
    }

    public void removeCustomer(int id) {
        customers.removeIf(customer -> customer.getId() == id);
        System.out.println("Customer with ID " + id + " removed.");
    }

    public void listCustomers() {
        if (customers.isEmpty()) {
            System.out.println("No customers found.");
        } else {
            for (Customer customer : customers) {
                System.out.println(customer);
            }
        }
    }

    public void findCustomerById(int id) {
        for (Customer customer : customers) {
            if (customer.getId() == id) {
                System.out.println("Customer found: " + customer);
                return;
            }
        }
        System.out.println("Customer with ID " + id + " not found.");
    }

    public void recordInteraction(int id, String interaction) {
        for (Customer customer : customers) {
            if (customer.getId() == id) {
                interactionHistory.recordInteraction(customer, interaction);
                return;
            }
        }
        System.out.println("Customer with ID " + id + " not found.");
    }

    public void displayInteractions(int id) {
        for (Customer customer : customers) {
            if (customer.getId() == id) {
                interactionHistory.displayInteractions(customer);
                return;
            }
        }
        System.out.println("Customer with ID " + id + " not found.");
    }

    public void addFeedback(int id, String feedback) {
        for (Customer customer : customers) {
            if (customer.getId() == id) {
                feedbackManager.addFeedback(customer, feedback);
                return;
            }
        }
        System.out.println("Customer with ID " + id + " not found.");
    }

    public void displayFeedbacks(int id) {
        for (Customer customer : customers) {
            if (customer.getId() == id) {
                feedbackManager.displayFeedbacks(customer);
                return;
            }
        }
        System.out.println("Customer with ID " + id + " not found.");
    }
}

public class CustomerRelationshipManagement {
    private static CRMSystem crmSystem = new CRMSystem();
    private static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        while (true) {
            showMenu();
            int choice = Integer.parseInt(scanner.nextLine());
            switch (choice) {
                case 1:
                    addCustomer();
                    break;
                case 2:
                    removeCustomer();
                    break;
                case 3:
                    listCustomers();
                    break;
                case 4:
                    findCustomerById();
                    break;
                case 5:
                    recordInteraction();
                    break;
                case 6:
                    displayInteractions();
                    break;
                case 7:
                    addFeedback();
                    break;
                case 8:
                    displayFeedbacks();
                    break;
                case 9:
                    System.out.println("Exiting...");
                    System.exit(0);
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }

    private static void showMenu() {
        System.out.println("\n--- CRM System Menu ---");
        System.out.println("1. Add Customer");
        System.out.println("2. Remove Customer");
        System.out.println("3. List Customers");
        System.out.println("4. Find Customer by ID");
        System.out.println("5. Record Interaction");
        System.out.println("6. Display Interactions");
        System.out.println("7. Add Feedback");
        System.out.println("8. Display Feedbacks");
        System.out.println("9. Exit");
        System.out.print("Enter your choice: ");
    }

    private static void addCustomer() {
        System.out.print("Enter customer name: ");
        String name = scanner.nextLine();
        System.out.print("Enter customer email: ");
        String email = scanner.nextLine();
        System.out.print("Enter customer phone: ");
        String phone = scanner.nextLine();
        crmSystem.addCustomer(name, email, phone);
    }

    private static void removeCustomer() {
        System.out.print("Enter customer ID to remove: ");
        int id = Integer.parseInt(scanner.nextLine());
        crmSystem.removeCustomer(id);
    }

    private static void listCustomers() {
        crmSystem.listCustomers();
    }

    private static void findCustomerById() {
        System.out.print("Enter customer ID to find: ");
        int id = Integer.parseInt(scanner.nextLine());
        crmSystem.findCustomerById(id);
    }

    private static void recordInteraction() {
        System.out.print("Enter customer ID to record interaction: ");
        int id = Integer.parseInt(scanner.nextLine());
        System.out.print("Enter interaction details: ");
        String interaction = scanner.nextLine();
        crmSystem.recordInteraction(id, interaction);
    }

    private static void displayInteractions() {
        System.out.print("Enter customer ID to display interactions: ");
        int id = Integer.parseInt(scanner.nextLine());
        crmSystem.displayInteractions(id);
    }

    private static void addFeedback() {
        System.out.print("Enter customer ID to add feedback: ");
        int id = Integer.parseInt(scanner.nextLine());
        System.out.print("Enter feedback: ");
        String feedback = scanner.nextLine();
        crmSystem.addFeedback(id, feedback);
    }

    private static void displayFeedbacks() {
        System.out.print("Enter customer ID to display feedbacks: ");
        int id = Integer.parseInt(scanner.nextLine());
        crmSystem.displayFeedbacks(id);
    }
}
