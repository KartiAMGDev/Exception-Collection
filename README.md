# Exception-Collection

Q1. Ramesh is developing a student management system for a university. In this system, you have a Student class to represent student information. You are asked to help Ramesh to handle exception which can be occurred into program according to following Scenarios: class Student with attributes roll no, name, age and course. Initialize values through parameterized constructor.
If the age of the student is not between 15 and 21 then generate a user-defined exception "AgeNotWithinRangeException".
If a name contains numbers or special symbols, raise exception "NameNotValidException". Define the two exception classes.


import java.util.Scanner;

// Custom exception class for age validation
class AgeNotWithinRangeException extends Exception {
    public AgeNotWithinRangeException(String message) {
        super(message);
    }
}

// Custom exception class for name validation
class NameNotValidException extends Exception {
    public NameNotValidException(String message) {
        super(message);
    }
}

// Student class
class Student {
    private int rollNo;
    private String name;
    private int age;
    private String course;

    // Parameterized constructor to initialize student attributes
    public Student(int rollNo, String name, int age, String course) throws AgeNotWithinRangeException, NameNotValidException {
        // Validate age
        if (age < 15 || age > 21) {
            throw new AgeNotWithinRangeException("Age should be between 15 and 21.");
        }

        // Validate name
        if (!name.matches("[a-zA-Z]+")) {
            throw new NameNotValidException("Name should only contain alphabets.");
        }

        this.rollNo = rollNo;
        this.name = name;
        this.age = age;
        this.course = course;
    }

    // Getter methods
    public int getRollNo() {
        return rollNo;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public String getCourse() {
        return course;
    }
}

// Main class for testing
public class StudentManagementSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        try {
            // Valid student creation
            System.out.println("Enter details for a valid student:");
            System.out.print("Enter Roll No: ");
            int validRollNo = scanner.nextInt();
            scanner.nextLine(); // Consume newline
            System.out.print("Enter Name: ");
            String validName = scanner.nextLine();
            System.out.print("Enter Age: ");
            int validAge = scanner.nextInt();
            scanner.nextLine(); // Consume newline
            System.out.print("Enter Course: ");
            String validCourse = scanner.nextLine();

            Student validStudent = new Student(validRollNo, validName, validAge, validCourse);
            System.out.println("Valid student created:");
            displayStudentDetails(validStudent);

            // Invalid student creation with age not within range
            System.out.println("Enter details for an invalid student (Age not within range):");
            System.out.print("Enter Roll No: ");
            int invalidAgeRollNo = scanner.nextInt();
            scanner.nextLine(); // Consume newline
            System.out.print("Enter Name: ");
            String invalidAgeName = scanner.nextLine();
            System.out.print("Enter Age: ");
            int invalidAge = scanner.nextInt();
            scanner.nextLine(); // Consume newline
            System.out.print("Enter Course: ");
            String invalidAgeCourse = scanner.nextLine();

            Student invalidAgeStudent = new Student(invalidAgeRollNo, invalidAgeName, invalidAge, invalidAgeCourse);
            displayStudentDetails(invalidAgeStudent);

            // Invalid student creation with name not valid
            System.out.println("Enter details for an invalid student (Name not valid):");
            System.out.print("Enter Roll No: ");
            int invalidNameRollNo = scanner.nextInt();
            scanner.nextLine(); // Consume newline
            System.out.print("Enter Name: ");
            String invalidName = scanner.nextLine();
            System.out.print("Enter Age: ");
            int invalidNameAge = scanner.nextInt();
            scanner.nextLine(); // Consume newline
            System.out.print("Enter Course: ");
            String invalidNameCourse = scanner.nextLine();

            Student invalidNameStudent = new Student(invalidNameRollNo, invalidName, invalidNameAge, invalidNameCourse);
            displayStudentDetails(invalidNameStudent);

        } catch (AgeNotWithinRangeException | NameNotValidException e) {
            System.out.println("Exception caught: " + e.getMessage());
        }

        // Close the scanner
        scanner.close();
    }

    private static void displayStudentDetails(Student student) {
        System.out.println("Roll No: " + student.getRollNo());
        System.out.println("Name: " + student.getName());
        System.out.println("Age: " + student.getAge());
        System.out.println("Course: " + student.getCourse());
        System.out.println("----------------------------");
    }
}

Q2. Create a class Voter(voterld, name, age) with parameterized constructor. The parameterized constructor should throw a checked exception if age is less than 18. The message of exception is "invalid age for voter"

import java.util.Scanner;

// Custom checked exception class for invalid voter age
class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}

// Voter class
class Voter {
    private int voterId;
    private String name;
    private int age;

    // Parameterized constructor with checked exception
    public Voter(int voterId, String name, int age) throws InvalidAgeException {
        if (age < 18) {
            throw new InvalidAgeException("Invalid age for voter. Must be 18 or above.");
        }

        this.voterId = voterId;
        this.name = name;
        this.age = age;
    }

    // Getter methods
    public int getVoterId() {
        return voterId;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}

// Main class for testing
public class VoterManagementSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        try {
            // Input for creating a Voter object
            System.out.print("Enter Voter ID: ");
            int voterId = scanner.nextInt();
            scanner.nextLine(); // Consume newline
            System.out.print("Enter Name: ");
            String voterName = scanner.nextLine();
            System.out.print("Enter Age: ");
            int voterAge = scanner.nextInt();

            // Creating a Voter object with exception handling
            Voter voter = new Voter(voterId, voterName, voterAge);
            System.out.println("Voter created successfully:");
            displayVoterDetails(voter);

        } catch (InvalidAgeException e) {
            System.out.println("Exception caught: " + e.getMessage());
        }

        // Close the scanner
        scanner.close();
    }

    private static void displayVoterDetails(Voter voter) {
        System.out.println("Voter ID: " + voter.getVoterId());
        System.out.println("Name: " + voter.getName());
        System.out.println("Age: " + voter.getAge());
        System.out.println("----------------------------");
    }
}


Q3. Store name of weekdays in an array (starting from "Sunday" at 0 index). Ask day position from user and print day name. Handle array index out of bound exception and give proper message if user enters day index outside range (0-6).	

import java.util.Scanner;

public class WeekdaysArray {
    public static void main(String[] args) {
        String[] weekdays = {"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"};

        Scanner scanner = new Scanner(System.in);

        try {
            // Ask user for day position
            System.out.print("Enter the day position (0-6): ");
            int dayIndex = scanner.nextInt();

            // Access the array and print the day name
            String dayName = weekdays[dayIndex];
            System.out.println("The day at position " + dayIndex + " is: " + dayName);

        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Error: Invalid day position. Please enter a number between 0 and 6.");
        } finally {
            // Close the scanner
            scanner.close();
        }
    }
}

Q4. Create a HashMap where keys are student names (strings) and values are their corresponding grades (integers). Create methods to add a new student, remove a student, and Display up a student's grade by name.

import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

public class StudentGradeManager {
    private Map<String, Integer> studentGrades;

    public StudentGradeManager() {
        this.studentGrades = new HashMap<>();
    }

    // Method to add a new student
    public void addStudent(String name, int grade) {
        studentGrades.put(name, grade);
        System.out.println(name + "'s grade added successfully.");
    }

    // Method to remove a student
    public void removeStudent(String name) {
        if (studentGrades.containsKey(name)) {
            studentGrades.remove(name);
            System.out.println(name + "'s record removed successfully.");
        } else {
            System.out.println("Student not found: " + name);
        }
    }

    // Method to display a student's grade by name
    public void displayGrade(String name) {
        if (studentGrades.containsKey(name)) {
            int grade = studentGrades.get(name);
            System.out.println(name + "'s grade is: " + grade);
        } else {
            System.out.println("Student not found: " + name);
        }
    }

    public static void main(String[] args) {
        StudentGradeManager gradeManager = new StudentGradeManager();
        Scanner scanner = new Scanner(System.in);

        // Example usage
        gradeManager.addStudent("John", 85);
        gradeManager.addStudent("Alice", 92);

        // Display grades
        gradeManager.displayGrade("John");
        gradeManager.displayGrade("Alice");

        // Remove a student
        gradeManager.removeStudent("John");

        // Display grades after removal
        gradeManager.displayGrade("John");
        gradeManager.displayGrade("Alice");

        // Close the scanner
        scanner.close();
    }
}

Q5. create a stack data structure to store Integers Create some methods for following functionalities.
a. Include functions for pushing elements onto the stack.
b. popping elements from the stack.
c. checking if the stack is empty

import java.util.EmptyStackException;

public class IntStack {
    private static final int MAX_SIZE = 100; // Maximum size of the stack
    private int[] stackArray;
    private int top; // Index of the top element in the stack

    // Constructor to initialize the stack
    public IntStack() {
        stackArray = new int[MAX_SIZE];
        top = -1; // Stack is initially empty
    }

    // Method to push an element onto the stack
    public void push(int element) {
        if (top == MAX_SIZE - 1) {
            System.out.println("Error: Stack overflow. Cannot push element onto a full stack.");
        } else {
            stackArray[++top] = element;
            System.out.println("Pushed " + element + " onto the stack.");
        }
    }

    // Method to pop an element from the stack
    public int pop() {
        if (isEmpty()) {
            throw new EmptyStackException();
        } else {
            int poppedElement = stackArray[top--];
            System.out.println("Popped " + poppedElement + " from the stack.");
            return poppedElement;
        }
    }

    // Method to check if the stack is empty
    public boolean isEmpty() {
        return top == -1;
    }

    public static void main(String[] args) {
        IntStack stack = new IntStack();

        // Push elements onto the stack
        stack.push(10);
        stack.push(20);
        stack.push(30);

        // Pop elements from the stack
        stack.pop();
        stack.pop();
        stack.pop();

        // Attempt to pop from an empty stack (will throw EmptyStackException)
        // stack.pop();
    }
}


