import java.util.HashMap;

class Account {
    private String accountNumber;
    private double balance;

    public Account(String accountNumber) {
        this.accountNumber = accountNumber;
        this.balance = 0.0;
    }

    public double getBalance() { return balance; }

    public void deposit(double amount) { balance += amount; }

    public boolean withdraw(double amount) {
        if (amount <= balance) {
            balance -= amount;
            return true;
        }
        return false;
    }
}

class User {
   private String name;
   private String pin;

   public User(String name, String pin) { 
       this.name = name; 
       this.pin = pin; 
   }

   public boolean validatePin(String pin) { 
       return this.pin.equals(pin); 
   }

   public String getName() { return name; }
}

class ATM {
   private HashMap<String, Account> accounts = new HashMap<>();

   public void addAccount(Account account) { accounts.put(account.accountNumber(), account); }

   public Account getAccount(String accountNumber) { return accounts.get(accountNumber); }

   public void deposit(String accountNumber, double amount) { 
       Account account = getAccount(accountNumber); 
       if (account != null) account.deposit(amount); 
   }

   public boolean withdraw(String accountNumber, double amount) { 
       Account account = getAccount(accountNumber); 
       return account != null && account.withdraw(amount); 
   }

   public double checkBalance(String accountNumber) { 
       Account account = getAccount(accountNumber); 
       return account != null ? account.getBalance() : -1; 
   }
}

public class ATMSystem {
   public static void main(String[] args){
       ATM atm = new ATM();
       
       Account acc1 = new Account("12345");
       atm.addAccount(acc1);

       User user = new User("Bob", "1234");
       
       atm.deposit("12345", 500.0);
       System.out.println("Balance: $" + atm.checkBalance("12345")); // Output: Balance: $500.0

       if(atm.withdraw("12345", 200.0)){
           System.out.println("Withdrawal successful.");
       } else{
           System.out.println("Insufficient funds.");
       }
       
       System.out.println("Balance after withdrawal: $" + atm.checkBalance("12345")); // Output: Balance after withdrawal: $300.0
   }
}
