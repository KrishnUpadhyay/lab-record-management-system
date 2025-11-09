# Lab Record Management System 🧪

A full-stack web application built using PHP, MySQL, and vanilla JavaScript. Its primary purpose is to manage and track the process of issuing and returning electronic components in a college or university laboratory.

This system replaces manual, paper-based record-keeping with an automated, role-based digital solution.

---

## 🚀 Key Features

* **Secure Authentication:** A complete Login and Registration system for users and administrators.
* **Role-Based Access Control:**
    * **Admin:** Can issue components, manage inventory, and send system alerts.
    * **User (Student):** Can only view dashboards and existing records.
* **Dynamic Dashboard:** Provides a real-time overview of key statistics, including "Total Issued" and "Overdue" items.
* **Inventory Management:** A full CRUD (Create, Read, Update, Delete) system for adding new components to the lab stock or managing existing items.
* **Issue & Return System:** A streamlined workflow for lab assistants to issue components to students and log their returns.
* **Telegram Alert System:** Allows the Admin to click a button ("Send Overdue Alerts") to instantly receive a summary report of all overdue items via a private Telegram bot.

---

## 🛠️ Technology Stack

* **Frontend:** HTML5, Tailwind CSS, JavaScript (using the Fetch API for asynchronous requests)
* **Backend:** PHP (with PDO for secure database interactions)
* **Database:** MySQL
* **Alerts:** Telegram Bot API

---

## ⚙️ Setup and Installation

Follow these steps to run this project on your local machine.

### 1. Clone the Project
Clone or download this repository and place all files inside a new folder named `lab_system` within your XAMPP or WAMP `htdocs` directory.
* **Path:** `C:\xampp\htdocs\lab_system\`

### 2. Set Up the Database
1.  Open phpMyAdmin by navigating to `http://localhost/phpmyadmin/`.
2.  Create a new database named `lab_db`.
3.  Click on the `lab_db` database, go to the **SQL** tab, and execute the following SQL script to create the required tables:

```sql
CREATE TABLE users (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(100) NOT NULL UNIQUE,
    password_hash VARCHAR(255) NOT NULL,
    role ENUM('admin', 'user') NOT NULL
);

CREATE TABLE components (
    component_id INT AUTO_INCREMENT PRIMARY KEY,
    component_name VARCHAR(255) NOT NULL,
    total_stock INT NOT NULL
);

CREATE TABLE issued_records (
    record_id INT AUTO_INCREMENT PRIMARY KEY,
    component_id INT NOT NULL,
    student_name VARCHAR(255) NOT NULL,
    student_email VARCHAR(255) NOT NULL,
    student_phone VARCHAR(20) NOT NULL,
    issue_date DATE NOT NULL,
    return_date DATE NOT NULL,
    issued_by_assistant VARCHAR(255) NOT NULL,
    is_returned BOOLEAN DEFAULT 0,
    actual_return_date DATE DEFAULT NULL,
    FOREIGN KEY (component_id) REFERENCES components(component_id)
);
```

3. Configure the api.php File
Open the api.php file in your code editor and update the following configurations:

Database Connection (Lines 18-21):

$db_host = 'localhost';

$db_user = 'root';

$db_pass = ''; (Enter your MySQL password here if you have one)

$db_name = 'lab_db';

Telegram Configuration (Lines 12-13):

$telegram_bot_token: Enter your private Telegram Bot token here.

$telegram_chat_id: Enter your personal Admin Chat ID here.

4. Run the Project
Start your XAMPP Control Panel (ensure Apache and MySQL are running).

Open your browser and navigate to: http://localhost/lab_system/lab_management_system.html

5. How to Use
First, click "Register Here" and register a new account with the Admin role.

Log in with your new Admin account.

Navigate to the Inventory tab and add a few components (e.g., Arduino Uno, Stock: 10).

Return to the Dashboard tab and click "Issue New Component".

To test the alert system, select a past date for the "Expected Return Date" and issue the item.

Click the "SEND OVERDUE ALERTS" button on the dashboard and check your Telegram for the alert!

👤 Author
Krishn Upadhyay
