# CODSOFT-3
import random
import string

def generate_password(length, use_uppercase, use_digits, use_special):
    # Define character sets
    lowercase_letters = string.ascii_lowercase
    uppercase_letters = string.ascii_uppercase if use_uppercase else ''
    digits = string.digits if use_digits else ''
    special_characters = string.punctuation if use_special else ''
    
    # Combine all character sets based on user preferences
    all_characters = lowercase_letters + uppercase_letters + digits + special_characters

    # Ensure the password includes at least one character from each selected set
    password = []
    if use_uppercase:
        password.append(random.choice(uppercase_letters))
    if use_digits:
        password.append(random.choice(digits))
    if use_special:
        password.append(random.choice(special_characters))
    
    # Fill the rest of the password length with random characters from the combined set
    password += random.choices(all_characters, k=length - len(password))
    
    # Shuffle the list to prevent predictable patterns
    random.shuffle(password)
    
    # Convert the list to a string
    return ''.join(password)

def main():
    print("Password Generator")
    try:
        length = int(input("Enter the desired length of the password: "))
        if length < 1:
            print("Password length must be at least 1.")
            return
    except ValueError:
        print("Invalid input. Please enter a numeric value.")
        return

    use_uppercase = input("Include uppercase letters? (yes/no): ").strip().lower() == 'yes'
    use_digits = input("Include digits? (yes/no): ").strip().lower() == 'yes'
    use_special = input("Include special characters? (yes/no): ").strip().lower() == 'yes'

    password = generate_password(length, use_uppercase, use_digits, use_special)
    print(f"Generated password: {password}")

if __name__ == "__main__":
    main()
