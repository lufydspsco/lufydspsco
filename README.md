import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

class Customer {
    String name;
    String email;
    double balance;

    Customer(String name, String email, double balance) {
        this.name = name;
        this.email = email;
        this.balance = balance;
    }
}

class Product {
    String name;
    double price;
    int quantity;

    Product(String name, double price, int quantity) {
        this.name = name;
        this.price = price;
        this.quantity = quantity;
    }
}

public class Supermarket {
    Map<String, Customer> customers;
    Map<String, Product> products;

    Supermarket() {
        customers = new HashMap<>();
        products = new HashMap<>();
    }

    void addCustomer(Customer customer) {
        customers.put(customer.email, customer);
    }

    void addProduct(Product product) {
        products.put(product.name, product);
    }

    void listCustomers() {
        for (Customer customer : customers.values()) {
            System.out.println(customer.name);
        }
    }

    void listProducts() {
        for (Product product : products.values()) {
            System.out.println(product.name + " - R$" + product.price);
        }
    }

    double calculateTotalProducts() {
        double total = 0;
        for (Product product : products.values()) {
            total += product.price * product.quantity;
        }
        return total;
    }

    void searchProduct(String productName) {
        for (Product product : products.values()) {
            if (product.name.toLowerCase().contains(productName.toLowerCase())) {
                System.out.println(product.name + " - R$" + product.price);
            }
        }
    }

    void makePayment(String email, double amount) {
        Customer customer = customers.get(email);
        if (customer!= null) {
            if (customer.balance >= amount) {
                customer.balance -= amount;
                System.out.println("Pagamento realizado com sucesso!");
            } else {
                System.out.println("Saldo insuficiente!");
            }
        } else {
            System.out.println("Cliente não encontrado!");
        }
    }

    public static void main(String[] args) {
        Supermarket supermarket = new Supermarket();
        Scanner scanner = new Scanner(System.in);

        Customer customer1 = new Customer("Luan Silva", "luan.silva@example.com", 1000);
        Customer customer2 = new Customer("Nicolas Oliveira", "nicolas.oliveira@example.com", 500);

        supermarket.addCustomer(customer1);
        supermarket.addCustomer(customer2);

        Product product1 = new Product("Arroz", 10.99, 50);
        Product product2 = new Product("Feijão", 5.99, 20);

        supermarket.addProduct(product1);
        supermarket.addProduct(product2);

        while (true) {
            System.out.println("Opções:");
            System.out.println("1. Listar clientes");
            System.out.println("2. Listar produtos");
            System.out.println("3. Buscar produto");
            System.out.println("4. Realizar pagamento");
            System.out.println("5. Sair");

            int option = scanner.nextInt();

            switch (option) {
                case 1:
                    supermarket.listCustomers();
                    break;
                case 2:
                    supermarket.listProducts();
                    break;
                case 3:
                    System.out.println("Digite o nome do produto:");
                    String productName = scanner.next();
                    supermarket.searchProduct(productName);
                    break;
                case 4:
                    System.out.println("Digite o email do cliente:");
                    String email = scanner.next();
                    System.out.println("Digite o valor do pagamento:");
                    double amount = scanner.nextDouble();
                    supermarket.makePayment(email, amount);
                    break;
                case 5:
                    System.exit(0);
                    break;
                default:
                    System.out.println("Opção inválida!");
            }
        }
    }
}
