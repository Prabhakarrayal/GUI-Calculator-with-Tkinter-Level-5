# 🚀 GUI Calculator with Tkinter (Level 5)

This project is a major step up from command-line applications. It's a fully functional, graphical calculator built with Tkinter, Python's built-in library for creating desktop applications.

This demonstrates the ability to build user-friendly, interactive tools and introduces the core concept of event-driven programming.

## 🎯 Skills Demonstrated

GUI Development: Using the Tkinter library to build a complete graphical interface.

Event-Driven Programming: A fundamental concept where the program's flow is determined by user events (like button clicks).

Object-Oriented Programming (OOP): Structuring the entire application as a single class (CalculatorApp) to manage its state and functions.

Layout Management: Using the .grid() geometry manager to precisely place widgets (buttons, entry boxes) in a window.

State Management: Keeping track of the current mathematical expression in an instance variable.

## 📂 File Structure

This entire application is contained in a single, well-structured Python file.
```
python-tkinter-calculator/
└── calculator_gui.py
```

## 💻 Code (calculator_gui.py)

This is the complete, self-contained code for the application.
```python
import tkinter as tk

class CalculatorApp:
    """
    A class-based application for a simple GUI calculator.
    Using a class allows us to neatly package all the widgets
    and functions together, managing the app's state.
    """
    
    def __init__(self, root):
        """
        The constructor for our class. This is where we
        build all the UI elements.
        """
        # Set up the main window
        self.root = root
        self.root.title("Python Calculator")
        self.root.geometry("300x400") # Set window size
        self.root.resizable(False, False) # Make window non-resizable
        
        # This will hold the expression string (e.g., "5+10")
        self.expression = ""
        
        # Create the display screen
        # We use a StringVar to easily update the text
        self.display_var = tk.StringVar()
        self.display_screen = tk.Entry(
            root, 
            textvariable=self.display_var, 
            font=('Arial', 24), 
            bd=10, 
            insertwidth=2, 
            width=14, 
            borderwidth=4,
            justify='right'
        )
        self.display_screen.grid(row=0, column=0, columnspan=4)
        
        # --- Create Buttons ---
        # We define the button layout in a list of lists
        buttons = [
            ('7', 1, 0), ('8', 1, 1), ('9', 1, 2), ('/', 1, 3),
            ('4', 2, 0), ('5', 2, 1), ('6', 2, 2), ('*', 2, 3),
            ('1', 3, 0), ('2', 3, 1), ('3', 3, 2), ('-', 3, 3),
            ('0', 4, 0), ('.', 4, 1), ('C', 4, 2), ('+', 4, 3),
            ('=', 5, 0, 2) # Spanning two columns
        ]
        
        # Loop through the list to create and place each button
        for (text, row, col, *span) in buttons:
            if text == 'C':
                # Special color for the 'Clear' button
                btn = tk.Button(
                    root, 
                    text=text, 
                    font=('Arial', 18), 
                    padx=20, 
                    pady=20, 
                    command=self.clear_display,
                    bg='#ff8080' # Reddish color
                )
            elif text == '=':
                # Special color for the 'Equals' button
                btn = tk.Button(
                    root, 
                    text=text, 
                    font=('Arial', 18), 
                    padx=20, 
                    pady=20, 
                    command=self.calculate_result,
                    bg='#80c0ff' # Bluish color
                )
            else:
                # Standard number/operator buttons
                # We use a 'lambda' to pass the button's text to our function
                btn = tk.Button(
                    root, 
                    text=text, 
                    font=('Arial', 18), 
                    padx=20, 
                    pady=20, 
                    command=lambda t=text: self.on_button_click(t)
                )
            
            # Place the button on the grid
            if span:
                # Button spans multiple columns (like '=')
                btn.grid(row=row, column=col, columnspan=span[0], sticky="nsew")
            else:
                btn.grid(row=row, column=col, sticky="nsew")

        # Configure row/column weights so they expand to fill space
        for i in range(1, 6):
            self.root.grid_rowconfigure(i, weight=1)
        for i in range(4):
            self.root.grid_columnconfigure(i, weight=1)

    def on_button_click(self, char):
        """Called when a number or operator button is pressed."""
        # Append the character to our expression string
        self.expression += str(char)
        # Update the display
        self.display_var.set(self.expression)
        
    def clear_display(self):
        """Called when the 'C' button is pressed."""
        self.expression = ""
        self.display_var.set("")
        
    def calculate_result(self):
        """
        Called when the '=' button is pressed.
        This uses the 'eval()' function, which is a simple
        way to evaluate a string as a Python expression.
        
        NOTE: eval() can be a security risk in a real,
        public-facing app, but it's perfect for this simple calculator.
        """
        try:
            # Evaluate the expression string
            result = str(eval(self.expression))
            # Show the result on the display
            self.display_var.set(result)
            # Set the expression to the result so user can continue
            self.expression = result
        except ZeroDivisionError:
            self.display_var.set("Error: Div by 0")
            self.expression = ""
        except Exception as e:
            self.display_var.set("Error")
            self.expression = ""


if __name__ == "__main__":
    # This is the standard boilerplate to run a Tkinter app
    
    # 1. Create the main window
    main_window = tk.Tk()
    
    # 2. Create an instance of our app class
    app = CalculatorApp(main_window)
    
    # 3. Start the application's main loop.
    # This makes the app wait for user events.
    main_window.mainloop()
```

## 🚀 How to Run

Save the code above as 
    
    calculator_gui.py.

Open your terminal and navigate to the directory.

Run the command: 

    python calculator_gui.py

The calculator window will appear on your screen!

## 📚 What You’ll Learn

* How to build a graphical application from scratch.

* The difference between procedural programming (top-to-bottom) and event-driven programming (waiting for clicks).

* How to use Object-Oriented Programming (OOP) to structure a GUI application effectively.

* How to manage layout and widgets using Tkinter's .grid() system.

* How to handle user input and basic errors in a visual way.

## ⭐ Support

If you found this helpful, please star ⭐ the repository to support more projects like this.
