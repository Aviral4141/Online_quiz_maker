
# Quiz Maker Web Application

## Project Summary

Quiz Maker is a simple, modern web application that allows users to create, take, and manage quizzes online. Built with PHP, MySQL, HTML, CSS, JavaScript, and Bootstrap, it features a clean blue/white theme throughout. The platform supports two types of users: **Examiners** (who create quizzes) and **Participants** (who take quizzes). It includes a leaderboard, analytics for examiners, and user authentication.

---

## Features

- **User Authentication**: Secure registration and login for all users.
- **Role-based Access**: Examiners can create quizzes; participants can take quizzes.
- **Quiz Creation**: Examiners can add questions and multiple-choice answers, with support for marking correct options.
- **Quiz Attempting**: Participants can attempt quizzes and receive instant scores.
- **Leaderboard**: Displays top scores and recent attempts.
- **Analytics**: Examiners can view statistics on their quizzes (attempts, average scores).
- **Consistent Theme**: Modern, responsive blue/white interface using Bootstrap.
- **Error Handling**: User-friendly error messages and validation throughout.

---

## Installation & Running Guide

### 1. **Clone or Download the Repository**

```
git clone https://github.com/aviral4141/quiz-maker.git
```
Or download and extract the ZIP.

### 2. **Database Setup**

- Open **phpMyAdmin** or your favorite MySQL client.
- Import the provided SQL file or run the following commands to create the database and tables:

```sql
CREATE DATABASE quiz_app;
USE quiz_app;

CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    role ENUM('examiner', 'participant') DEFAULT 'participant',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE quizzes (
    id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(255) NOT NULL,
    creator_id INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (creator_id) REFERENCES users(id)
);

CREATE TABLE questions (
    id INT PRIMARY KEY AUTO_INCREMENT,
    quiz_id INT NOT NULL,
    question_text TEXT NOT NULL,
    FOREIGN KEY (quiz_id) REFERENCES quizzes(id)
);

CREATE TABLE options (
    id INT PRIMARY KEY AUTO_INCREMENT,
    question_id INT NOT NULL,
    option_text VARCHAR(255) NOT NULL,
    is_correct BOOLEAN DEFAULT FALSE,
    FOREIGN KEY (question_id) REFERENCES questions(id)
);

CREATE TABLE attempts (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    quiz_id INT NOT NULL,
    score INT DEFAULT 0,
    attempted_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (quiz_id) REFERENCES quizzes(id)
);
```

### 3. **Configuration**

- Edit `includes/config.php` with your MySQL credentials:
    ```php
    $host = 'localhost';
    $db   = 'quiz_app';
    $user = 'root'; // or your MySQL username
    $pass = '';     // or your MySQL password
    ```

### 4. **Run the Application**

- Place the project folder in your web server’s root (e.g., `htdocs` for XAMPP).
- Start Apache and MySQL from XAMPP/WAMP/MAMP.
- Visit [http://localhost/quiz-app/index.php](http://localhost/quiz-app/index.php) in your browser.

---

## User Manual

### **For All Users**
- **Register:** Click "Register" on the navbar, fill in your details, and select your role (Examiner or Participant).
- **Login:** Use your credentials to log in.

### **For Examiners**
- **Create Quiz:** After login, click "Create Quiz" on your dashboard. Add a title, questions, and multiple options (mark at least one as correct).
- **View Analytics:** See statistics for your quizzes from the Analytics section.
- **Leaderboard:** View top performers from the Leaderboard link.

### **For Participants**
- **Take Quiz:** After login, select a quiz from the dashboard and answer the questions. Submit to see your score.
- **Leaderboard:** Check your ranking and others’ scores on the Leaderboard.

### **General Navigation**
- Use the navbar to access Dashboard, Leaderboard, Analytics, Login, or Register.
- Log out from the dropdown under your role badge.
