# 1. Graphical Interface and Event-Driven Programming (Java)

## What is a Graphical User Interface (GUI)?

A **Graphical User Interface (GUI)** allows users to interact with a program using:

* Buttons
* Text fields
* Labels
* Windows
* Menus

Instead of typing commands, users **click, type, or select**.

Examples:

* Calculator
* Login form
* Text editor

---

## GUI in Java

Java provides two main GUI libraries:

1. **AWT (Abstract Window Toolkit)** – older, heavyweight
2. **Swing** – newer, lightweight, more powerful

---

## What is Event-Driven Programming?

In **event-driven programming**, the program:

* Waits for user actions (events)
* Executes code when an event occurs

The program does **not run line by line** like console programs.

---

## What is an Event?

An **event** is an action performed by the user or system.

Examples:

* Button click
* Mouse movement
* Key press
* Window closing

---

## Event-Driven Flow (Concept)

```
User Action → Event Generated → Event Listener → Event Handler Code
```

---

## Components of Event-Driven Programming

### 1. Event Source

Component that generates the event
Example: `JButton`, `JTextField`

---

### 2. Event Object

Contains details of the event
Example: `ActionEvent`, `MouseEvent`

---

### 3. Event Listener

Interface that receives the event
Example: `ActionListener`

---

### 4. Event Handler

Method that executes when event occurs
Example: `actionPerformed()`

---

## Example: Button Click Event (Swing)

```java
import javax.swing.*;
import java.awt.event.*;

public class MyGUI {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Event Example");
        JButton button = new JButton("Click Me");

        button.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                System.out.println("Button clicked");
            }
        });

        frame.add(button);
        frame.setSize(300, 200);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }
}
```

---

## Important Event Listener Interfaces

| Listener       | Event          |
| -------------- | -------------- |
| ActionListener | Button click   |
| MouseListener  | Mouse actions  |
| KeyListener    | Keyboard input |
| WindowListener | Window events  |

---

## Interview Points

* GUI is user-friendly
* Event-driven programs respond to user actions
* Listeners handle events

---

# 2. Swing Toolkit

## What is Swing?

**Swing** is a **Java GUI toolkit** used to build **desktop applications**.

It is part of **Java Foundation Classes (JFC)**.

---

## Features of Swing

* Platform independent
* Lightweight components
* Customizable look and feel
* Rich set of components

---

## Swing vs AWT

| Feature     | AWT          | Swing           |
| ----------- | ------------ | --------------- |
| Components  | Heavyweight  | Lightweight     |
| Look & Feel | OS dependent | Pluggable       |
| Performance | Faster       | Slightly slower |
| Flexibility | Low          | High            |

---

## Swing Architecture

Swing follows **MVC (Model-View-Controller)** pattern.

* Model → Data
* View → Display
* Controller → User input

---

## Top-Level Containers

| Container | Purpose      |
| --------- | ------------ |
| JFrame    | Main window  |
| JDialog   | Popup window |
| JApplet   | Applet       |

---

## Common Swing Components

| Component    | Description       |
| ------------ | ----------------- |
| JLabel       | Displays text     |
| JButton      | Clickable button  |
| JTextField   | Single-line input |
| JTextArea    | Multi-line input  |
| JCheckBox    | Checkbox          |
| JRadioButton | Radio button      |
| JTable       | Table             |
| JComboBox    | Dropdown          |

---

## Layout Managers

Layout managers control component positioning.

| Layout       | Description           |
| ------------ | --------------------- |
| FlowLayout   | Left to right         |
| BorderLayout | 5 regions             |
| GridLayout   | Grid                  |
| BoxLayout    | Vertical / horizontal |

---

## Example: Simple Swing Form

```java
import javax.swing.*;

public class LoginForm {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Login");

        JLabel label = new JLabel("Username:");
        JTextField text = new JTextField(15);
        JButton button = new JButton("Login");

        JPanel panel = new JPanel();
        panel.add(label);
        panel.add(text);
        panel.add(button);

        frame.add(panel);
        frame.setSize(300, 150);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }
}
```

---

## Swing Threading Rule (Very Important)

All Swing components must be created and updated on the **Event Dispatch Thread (EDT)**.

Correct way:

```java
SwingUtilities.invokeLater(() -> {
    new LoginForm();
});
```

---

## Interview Points

* Swing is lightweight
* Uses MVC architecture
* Event handling via listeners
* Runs on EDT

---

# One-Line Viva Answers

* **GUI**: Interface using graphical components
* **Event-driven programming**: Program responds to events
* **Swing**: Java toolkit for GUI
* **Listener**: Handles events

---

# Quick Summary Table

| Topic        | Key Idea               |
| ------------ | ---------------------- |
| GUI          | Visual interaction     |
| Event-Driven | Action-based execution |
| Swing        | GUI toolkit            |
| Listener     | Event handler          |

---
