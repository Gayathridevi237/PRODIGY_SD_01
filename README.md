import tkinter as tk
from tkinter import messagebox

def celsius_to_fahrenheit(celsius):
    return (celsius * 9/5) + 32

def celsius_to_kelvin(celsius):
    return celsius + 273.15

def fahrenheit_to_celsius(fahrenheit):
    return (fahrenheit - 32) * 5/9

def fahrenheit_to_kelvin(fahrenheit):
    return (fahrenheit - 32) * 5/9 + 273.15

def kelvin_to_celsius(kelvin):
    return kelvin - 273.15

def kelvin_to_fahrenheit(kelvin):
    return (kelvin - 273.15) * 9/5 + 32

def convert_temperature():
    try:
        temperature = float(entry_temp.get())
        unit = var_unit.get()

        if unit == 'Celsius':
            fahrenheit = celsius_to_fahrenheit(temperature)
            kelvin = celsius_to_kelvin(temperature)
            result.set(f"{temperature:.2f}°C is equal to {fahrenheit:.2f}°F and {kelvin:.2f}K")
        elif unit == 'Fahrenheit':
            celsius = fahrenheit_to_celsius(temperature)
            kelvin = fahrenheit_to_kelvin(temperature)
            result.set(f"{temperature:.2f}°F is equal to {celsius:.2f}°C and {kelvin:.2f}K")
        elif unit == 'Kelvin':
            celsius = kelvin_to_celsius(temperature)
            fahrenheit = kelvin_to_fahrenheit(temperature)
            result.set(f"{temperature:.2f}K is equal to {celsius:.2f}°C and {fahrenheit:.2f}°F")
        else:
            messagebox.showerror("Error", "Invalid unit. Please select Celsius, Fahrenheit, or Kelvin.")
    except ValueError:
        messagebox.showerror("Error", "Please enter a valid temperature.")


root = tk.Tk()
root.title("Temperature Converter")


frame_input = tk.Frame(root)
frame_input.pack(pady=10)

label_temp = tk.Label(frame_input, text="Enter a temperature value: ")
label_temp.pack(side=tk.LEFT)

entry_temp = tk.Entry(frame_input)
entry_temp.pack(side=tk.LEFT)


frame_unit = tk.Frame(root)
frame_unit.pack(pady=10)

label_unit = tk.Label(frame_unit, text="Select the original unit: ")
label_unit.pack(side=tk.LEFT)

var_unit = tk.StringVar(value="Celsius")

radio_celsius = tk.Radiobutton(frame_unit, text="Celsius (C)", variable=var_unit, value="Celsius")
radio_celsius.pack(side=tk.LEFT)

radio_fahrenheit = tk.Radiobutton(frame_unit, text="Fahrenheit (F)", variable=var_unit, value="Fahrenheit")
radio_fahrenheit.pack(side=tk.LEFT)

radio_kelvin = tk.Radiobutton(frame_unit, text="Kelvin (K)", variable=var_unit, value="Kelvin")
radio_kelvin.pack(side=tk.LEFT)


button_convert = tk.Button(root, text="Convert", command=convert_temperature)
button_convert.pack(pady=10)


result = tk.StringVar()
label_result = tk.Label(root, textvariable=result, font=("Helvetica", 14))
label_result.pack(pady=10)


root.mainloop()
