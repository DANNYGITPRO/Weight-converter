# Weight-converter
import ttkbootstrap as ttk
from ttkbootstrap.constants import *
from tkinter import messagebox

# Conversion factors (relative to kg)
conversion_factors = {
    "Kg": 1,  # Base unit
    "Lbs": 2.20462,  # 1 kg = 2.20462 lbs
    "g": 1000,  # 1 kg = 1000 g
    "Oz": 35.274,  # 1 kg = 35.274 oz
    "St": 0.157473  # 1 kg = 0.157473 st (stones)
}


def convert_weight():
    """Convert weight from one unit to another."""
    try:
        weight = float(entry_weight.get())  # Get input weight
        from_unit = from_unit_var.get()  # Get source unit
        to_unit = to_unit_var.get()  # Get target unit

        # Convert input weight to Kg first, then to target unit
        weight_in_kg = weight / conversion_factors[from_unit]
        converted = weight_in_kg * conversion_factors[to_unit]

        result_label.config(text=f"{weight:.2f} {from_unit} = {converted:.2f} {to_unit}", foreground="blue")

    except ValueError:
        messagebox.showerror("Invalid Input", "Please enter a valid number.")


# Create main window
root = ttk.Window(themename="superhero")  # Try "cosmo", "flatly", "darkly" for different styles
root.title("Weight Converter")
root.geometry("400x300")
root.resizable(False, False)

# Title Label
title_label = ttk.Label(root, text="Weight Converter", font=("Arial", 16, "bold"))
title_label.pack(pady=10)

# Input Field
input_frame = ttk.Frame(root)
input_frame.pack(pady=5)

ttk.Label(input_frame, text="Enter Weight:", font=("Arial", 12)).grid(row=0, column=0, padx=5)
entry_weight = ttk.Entry(input_frame, font=("Arial", 12), width=10)
entry_weight.grid(row=0, column=1, padx=5)

# Dropdown for "From" Unit
ttk.Label(input_frame, text="From:", font=("Arial", 12)).grid(row=1, column=0, padx=5)
from_unit_var = ttk.StringVar(value="Kg")
from_unit_menu = ttk.Combobox(input_frame, textvariable=from_unit_var, values=list(conversion_factors.keys()),
                              state="readonly", width=8)
from_unit_menu.grid(row=1, column=1, padx=5)

# Dropdown for "To" Unit
ttk.Label(input_frame, text="To:", font=("Arial", 12)).grid(row=2, column=0, padx=5)
to_unit_var = ttk.StringVar(value="Lbs")
to_unit_menu = ttk.Combobox(input_frame, textvariable=to_unit_var, values=list(conversion_factors.keys()),
                            state="readonly", width=8)
to_unit_menu.grid(row=2, column=1, padx=5)

# Convert Button
convert_button = ttk.Button(root, text="Convert", bootstyle="success", command=convert_weight)
convert_button.pack(pady=10)

# Result Label
result_label = ttk.Label(root, text="", font=("Arial", 14, "bold"))
result_label.pack(pady=5)

# Run the GUI
root.mainloop()


