import tkinter as tk

def is_valid_credit_card(card_number):
    card_number = ''.join(card_number.split())

    if not card_number.isdigit():
        return False

    if len(card_number) != 16:
        return False

    total = 0
    for i, digit in enumerate(card_number[::-1]):
        if i % 2 == 0:
            total += int(digit)
        else:
            doubled_digit = int(digit) * 2
            if doubled_digit > 9:
                total += doubled_digit - 9
            else:
                total += doubled_digit
    return total % 10 == 0

def validate_card():
    card_number = entry.get()
    if is_valid_credit_card(card_number):
        result_label.config(text="This credit card number is valid.")
    else:
        result_label.config(text="This credit card number is invalid.")

root = tk.Tk()
root.title("Credit card number verification")
root.geometry("1000x250")

entry = tk.Entry(root, width=150)
entry.pack(pady=5)
validate_button = tk.Button(root, text="Verify", command=validate_card)
validate_button.pack(pady=5)
result_label = tk.Label(root, text="")
result_label.pack(pady=5)

root.mainloop()
