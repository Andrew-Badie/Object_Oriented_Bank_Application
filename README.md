# JavaFX Bank Application

[![Build](https://github.com/Andrew-Badie/Object_Oriented_Bank_Application/actions/workflows/build.yml/badge.svg)](https://github.com/Andrew-Badie/Object_Oriented_Bank_Application/actions/workflows/build.yml)

A JavaFX desktop banking application built to practise object-oriented design. A manager can create and delete customer accounts; customers can deposit, withdraw, make purchases and check their balance. Account tiers (Silver, Gold, Platinum) are derived from the balance and change the fee charged on purchases.

**Tech:** Java 21, JavaFX 21, FXML, Maven, file-based persistence

## Features

- Role-based login for managers and customers
- Manager screen: create and delete customer accounts
- Customer screen: deposit, withdraw, purchase, and check balance
- Tiered accounts: Silver (< 10,000), Gold (10,000 – 19,999), Platinum (20,000+), with purchase fees of 20, 10 and 0 respectively
- Account data saved to local text files between sessions

## Requirements

- JDK 21
- Maven 3.9 or later
- A desktop graphical session on Windows, macOS, or Linux
- Internet access for the initial Maven dependency download

JavaFX 21.0.2 is declared in the POM. A separate JavaFX SDK installation or IDE module-path setup is not required for the Maven launch command.

## Build and run

```bash
git clone https://github.com/Andrew-Badie/Object_Oriented_Bank_Application.git
cd Object_Oriented_Bank_Application
java -version
mvn -version
mvn clean compile
mvn javafx:run
```

Check that both version commands identify JDK 21. Maven launches `hellofx.BankApplication`, which loads the login view from `/hellofx/hellofx.fxml`.

## Try it

Use synthetic data only.

1. Start the application. Enter username `admin`, password `admin`, and role `manager`. These are fixed educational demo credentials.
2. Create a customer named `demo_customer` with a disposable password. The initial balance is 100.
3. Log out, then log in using those customer credentials and role `customer`.
4. In the customer screen, enter the same credentials in the confirmation fields.
5. Select Get Balance, deposit 50, and check for a balance of 150.
6. Withdraw 20 and check for a balance of 130.
7. Use a purchase of 50 to explore purchase fees; for a Silver account the current code charges an additional 20.
8. Log out and close the application.

The program writes a file named after the customer in the process working directory (normally the repository root when launched as above). Use `demo_customer` for this walkthrough; do not use filenames, paths, or real personal data as usernames. The demo file is ignored by Git. Close the application before deleting it to reset the demonstration.

## Source layout

```text
pom.xml
src/main/java/hellofx/
    BankApplication.java    JavaFX launcher
    Controller.java         Login and navigation
    Controller2.java        Manager actions
    Customer.java           Customer actions
src/main/resources/hellofx/
    hellofx.fxml             Login view
    hellofx2.fxml            Manager view
    addCustomer.fxml        Customer view
```

FXML resources share the controllers' package path so the existing relative resource lookups continue to work.

## Design

Each FXML view has its own controller: `Controller` handles login and navigation, `Controller2` handles manager actions, and `Customer` handles customer transactions and the tier/fee rules. Each customer's record (credentials, balance, tier) is persisted to a local text file.

## Known limitations

This is a coursework project, not a production banking system: credentials are stored in plaintext local files, demo login is hard-coded for the manager, non-numeric amounts are not yet validated, and usernames are used directly as file names.

## Troubleshooting

- If `mvn` is not recognized, install Maven and add its executable directory to PATH.
- If Maven reports an unsupported Java release, configure JAVA_HOME/PATH for JDK 21 and check `mvn -version` again.
- A graphical display is required; compilation alone does not validate JavaFX screens.
- Run Maven from the directory containing `pom.xml`.

## AI assistance

The application code is my original coursework. The Maven build, CI workflow and this README were updated later with AI assistance and are recorded in the commit history.
