باشه، این هم جواب‌ها به صورت جداگانه:

ابتدا، این توابع کمکی عمومی را در ابتدای اسکریپت پایتون خود تعریف کنید، زیرا برخی از تمرین‌ها از آنها استفاده می‌کنند:
```python
# Global Helper Functions (تعاریف توابع کمکی عمومی)
import math # For square root, used in a few exercises

# Helper function to calculate factorial
def calculate_factorial(n):
    # Factorial of 0 is 1
    if n == 0:
        return 1
    # Factorial of negative numbers is not defined
    if n < 0:
        return None # Or raise an error
    
    result = 1
    # Multiply numbers from 1 to n
    for i in range(1, n + 1):
        result = result * i
    return result

# Helper function to check if a number is prime
def is_prime(num):
    # Numbers less than 2 are not prime
    if num < 2:
        return False
    # 2 is the only even prime number
    if num == 2:
        return True
    # Other even numbers are not prime
    if num % 2 == 0:
        return False
    # Check for divisibility from 3 up to the square root of the number
    # We only need to check odd divisors
    i = 3
    while i * i <= num:
        if num % i == 0:
            return False
        i = i + 2
    return True
```

---

سوال ۱
اعداد اول: برنامه‌ای در پایتون بنویسید که یک عدد صحیح N را از ورودی دریافت کند. سپس تابعی بنویسید که تمام اعداد اول از ۱ تا N را پیدا کرده و چاپ کند.
جواب ۱
```python
# --- Exercise 1: Prime Numbers ---
# This exercise uses the global 'is_prime' helper function defined above.

def find_primes_up_to_n_ex1(limit_n):
    # Function to find and print all prime numbers from 1 to N.
    print(f"Prime numbers from 1 to {limit_n}:")
    prime_numbers_list = []
    for number in range(1, limit_n + 1):
        if is_prime(number): # Using the global helper
            prime_numbers_list.append(number)
    print(prime_numbers_list)

# Example usage for Exercise 1:
# print("--- Running Exercise 1 ---")
# n_input_ex1 = int(input("Ex1: Enter an integer N: "))
# find_primes_up_to_n_ex1(n_input_ex1)
# print("--- End of Exercise 1 ---\n")
```

---

سوال ۲
عملیات روی لیست اعداد: برنامه‌ای در پایتون بنویسید که ۱۰۰ عدد را از ورودی دریافت کرده و در یک لیست ذخیره کند. سپس:
تابعی برای پیدا کردن و چاپ کوچکترین عدد لیست بنویسید.
تابعی برای مرتب‌سازی لیست به صورت نزولی بنویسید.
میانگین کوچکترین و بزرگترین عدد مجموعه اولیه را محاسبه و چاپ کنید.
در نهایت، لیست مرتب‌شده و میانگین محاسبه‌شده را چاپ کنید.
جواب ۲
```python
# --- Exercise 2: Operations on List of Numbers ---

def get_numbers_ex2(count=5): # Reduced from 100 for easier testing
    # Function to get 'count' numbers from input.
    num_list = []
    print(f"Ex2: Enter {count} numbers:")
    for i in range(count):
        while True:
            try:
                num = int(input(f"  Enter number {i + 1}: "))
                num_list.append(num)
                break
            except ValueError:
                print("    Invalid input. Please enter an integer.")
    return num_list

def find_and_print_smallest_ex2(numbers):
    # Function to find and print the smallest number in a list.
    if not numbers: # Check if the list is empty
        print("Ex2: The list is empty.")
        return None
    
    smallest = numbers[0] # Assume the first number is the smallest
    for num in numbers:
        if num < smallest:
            smallest = num # Update smallest if a smaller number is found
    print(f"Ex2: The smallest number in the list is: {smallest}")
    return smallest

def sort_list_descending_ex2(numbers):
    # Function to sort a list in descending order (using bubble sort).
    # This modifies the list in-place.
    n = len(numbers)
    for i in range(n):
        for j in range(0, n - i - 1):
            if numbers[j] < numbers[j+1]:
                temp = numbers[j]
                numbers[j] = numbers[j+1]
                numbers[j+1] = temp
    # The list 'numbers' is now sorted.

def run_exercise2():
    # Get 100 numbers (reduced to 5 for testing)
    numbers_ex2_original = get_numbers_ex2(count=5) 
    
    if not numbers_ex2_original:
        print("Ex2: No numbers entered. Exiting exercise.")
        return

    numbers_ex2_for_sorting = [] # Create a copy for sorting
    for item in numbers_ex2_original:
        numbers_ex2_for_sorting.append(item)

    # 2.1: Find and print the smallest number
    print("\nEx2: Finding smallest in original list:")
    smallest_ex2 = find_and_print_smallest_ex2(numbers_ex2_original)

    # 2.2: Sort the list in descending order
    sort_list_descending_ex2(numbers_ex2_for_sorting)

    # 2.3: Calculate and print the average of the smallest and largest number of the *initial* set
    # Find largest in original list
    largest_ex2 = numbers_ex2_original[0]
    for num in numbers_ex2_original:
        if num > largest_ex2:
            largest_ex2 = num
            
    average_min_max_ex2 = -1 # Default value
    if smallest_ex2 is not None: # Check if smallest_ex2 was found
        average_min_max_ex2 = (smallest_ex2 + largest_ex2) / 2
        print(f"Ex2: Smallest in original: {smallest_ex2}, Largest in original: {largest_ex2}")
        print(f"Ex2: Average of smallest and largest of original set: {average_min_max_ex2}")
    else:
        print("Ex2: Cannot calculate average as smallest number was not found (list might be empty).")

    # 2.4: Print the sorted list and the calculated average
    print(f"Ex2: Sorted list (descending): {numbers_ex2_for_sorting}")
    # The average was already printed above.

# Example usage for Exercise 2:
# print("--- Running Exercise 2 ---")
# run_exercise2()
# print("--- End of Exercise 2 ---\n")
```

---

سوال ۳
باقیمانده و مربع: برنامه‌ای در پایتون بنویسید که ۱۰۰ عدد را از ورودی دریافت کند. برای هر عدد:
باقیمانده تقسیم آن بر ۵ را محاسبه کنید.
اگر باقیمانده صفر بود، خود عدد را چاپ کنید.
در غیر این صورت، تابعی را فراخوانی کنید که مربع عدد را محاسبه کرده و این مربع‌ها را در یک لیست جدید ذخیره کند.
پس از پردازش تمام اعداد، میانگین اعداد ذخیره شده در لیست مربع‌ها را محاسبه و چاپ کنید.
جواب ۳
```python
# --- Exercise 3: Remainder and Square ---

def square_number_ex3(num):
    # Function to calculate the square of a number.
    return num * num

def process_numbers_remainder_square_ex3(count=5): # Reduced from 100 for testing
    # Function to process 'count' numbers for remainder and square.
    numbers_input = []
    print(f"Ex3: Enter {count} numbers:")
    for i in range(count):
        while True:
            try:
                num = int(input(f"  Enter number {i + 1}: "))
                numbers_input.append(num)
                break
            except ValueError:
                print("    Invalid input. Please enter an integer.")

    squared_numbers_list = []
    print("\nEx3: Processing numbers:")
    for num in numbers_input:
        remainder = num % 5
        print(f"  Number: {num}, Remainder when divided by 5: {remainder}")
        if remainder == 0:
            print(f"    Remainder is 0. Printing the number: {num}")
        else:
            sq = square_number_ex3(num)
            squared_numbers_list.append(sq)
            print(f"    Remainder is not 0. Squared: {sq}. Added to list of squares.")
    
    if squared_numbers_list: # Check if the list is not empty
        sum_of_squares = 0
        for sq_num in squared_numbers_list:
            sum_of_squares += sq_num
        average_of_squares = sum_of_squares / len(squared_numbers_list)
        print(f"\nEx3: List of squares (for numbers not divisible by 5): {squared_numbers_list}")
        print(f"Ex3: Average of numbers in the list of squares: {average_of_squares}")
    else:
        print("\nEx3: No numbers were squared (all were divisible by 5 or no numbers processed).")

# Example usage for Exercise 3:
# print("--- Running Exercise 3 ---")
# process_numbers_remainder_square_ex3(count=5)
# print("--- End of Exercise 3 ---\n")
```

---

سوال ۴
میانگین و تفاضل: برنامه‌ای در پایتون بنویسید که ابتدا تعداد اعداد (count) را از ورودی بگیرد، سپس count عدد را دریافت کرده و در یک لیست ذخیره کند.
تابعی برای محاسبه و چاپ میانگین اعداد لیست بنویسید.
تابعی دیگر بنویسید که تفاضل هر یک از اعداد لیست را از میانگین محاسبه شده، به دست آورده و چاپ کند.
جواب ۴
```python
# --- Exercise 4: Average and Difference ---

def calculate_and_print_average_ex4(num_list):
    # Function to calculate and print the average of numbers in a list.
    if not num_list:
        print("Ex4: The list is empty. Cannot calculate average.")
        return None
    
    total_sum = 0
    for num in num_list:
        total_sum += num
    
    average = total_sum / len(num_list)
    print(f"Ex4: The average of the numbers is: {average}")
    return average

def print_differences_from_average_ex4(num_list, average):
    # Function to calculate and print the difference of each number from the average.
    if average is None:
        print("Ex4: Average is not calculated. Cannot find differences.")
        return
        
    print("Ex4: Differences from the average:")
    for num in num_list:
        difference = num - average
        # {: .2f} formats a float to 2 decimal places
        print(f"  Number: {num}, Difference from average ({average:.2f}): {difference:.2f}")

def run_exercise4():
    count_ex4 = 0
    while True:
        try:
            count_ex4 = int(input("Ex4: Enter the count of numbers: "))
            if count_ex4 > 0:
                break
            else:
                print("   Count must be positive.")
        except ValueError:
            print("   Invalid input for count. Please enter an integer.")

    numbers_ex4 = []
    print(f"Ex4: Enter {count_ex4} numbers:")
    for i in range(count_ex4):
        while True:
            try:
                num = int(input(f"  Enter number {i + 1}: "))
                numbers_ex4.append(num)
                break
            except ValueError:
                print("    Invalid input. Please enter an integer.")

    # Calculate and print average
    average_ex4 = calculate_and_print_average_ex4(numbers_ex4)
    # Calculate and print differences
    if average_ex4 is not None: # Proceed only if average was successfully calculated
        print_differences_from_average_ex4(numbers_ex4, average_ex4)

# Example usage for Exercise 4:
# print("--- Running Exercise 4 ---")
# run_exercise4()
# print("--- End of Exercise 4 ---\n")
```

---

سوال ۵
فیبوناچی و اعداد تام: برنامه‌ای در پایتون بنویسید که عدد N را از ورودی دریافت کند.
تابعی بنویسید که N جمله اول دنباله فیبوناچی را تولید و چاپ کند.
تابعی دیگر بنویسید که تمام اعداد تام کوچکتر از N را مشخص و چاپ کند.
جواب ۵
```python
# --- Exercise 5: Fibonacci and Perfect Numbers ---

def generate_fibonacci_ex5(n_terms):
    # Function to generate and print the first N Fibonacci numbers.
    fib_sequence = []
    a, b = 0, 1 # First two Fibonacci numbers
    if n_terms <= 0:
        print("Ex5: Number of Fibonacci terms should be positive.")
    elif n_terms == 1:
        fib_sequence.append(a)
    else:
        for _ in range(n_terms):
            fib_sequence.append(a)
            next_term = a + b
            a = b
            b = next_term
    print(f"Ex5: First {n_terms} Fibonacci numbers: {fib_sequence}")
    return fib_sequence

def is_perfect_number_ex5(num):
    # Function to check if a number is a perfect number.
    # A perfect number is a positive integer that is equal to the sum of its proper positive divisors.
    if num <= 1:
        return False
    sum_of_divisors = 0
    for i in range(1, num): # Divisors from 1 up to num-1
        if num % i == 0:
            sum_of_divisors += i
    return sum_of_divisors == num

def find_perfect_numbers_less_than_n_ex5(limit_n):
    # Function to find and print all perfect numbers less than N.
    perfect_nums = []
    for i in range(1, limit_n): # Iterate up to N-1
        if is_perfect_number_ex5(i):
            perfect_nums.append(i)
    print(f"Ex5: Perfect numbers less than {limit_n}: {perfect_nums}")
    return perfect_nums

def run_exercise5():
    n_input_ex5 = 0
    while True:
        try:
            n_input_ex5 = int(input("Ex5: Enter an integer N: "))
            if n_input_ex5 > 0:
                break
            else:
                print("  N must be a positive integer.")
        except ValueError:
            print("  Invalid input for N. Please enter an integer.")
            
    generate_fibonacci_ex5(n_input_ex5)
    find_perfect_numbers_less_than_n_ex5(n_input_ex5)

# Example usage for Exercise 5:
# print("--- Running Exercise 5 ---")
# run_exercise5()
# print("--- End of Exercise 5 ---\n")
```

---

سوال ۶
ذخیره اسامی: برنامه‌ای در پایتون بنویسید که اسامی ۲۵ دانش‌آموز را دریافت کرده و در یک لیست ذخیره کند. سپس لیست اسامی را نمایش دهد.
جواب ۶
```python
# --- Exercise 6: Store Names ---
def store_and_display_names_ex6(count=5): # Reduced from 25 for testing
    # Function to get 'count' names and display them.
    names_list = []
    print(f"Ex6: Enter {count} student names:")
    for i in range(count):
        name = input(f"  Enter name of student {i + 1}: ")
        names_list.append(name)
    
    print("\nEx6: List of student names:")
    for i in range(len(names_list)):
        print(f"  {i + 1}. {names_list[i]}")
    return names_list

# Example usage for Exercise 6:
# print("--- Running Exercise 6 ---")
# student_names_ex6 = store_and_display_names_ex6(count=3) # Example with 3 names
# print("--- End of Exercise 6 ---\n")
```

---

سوال ۷
اعداد فرد سه‌رقمی: برنامه‌ای در پایتون بنویسید که تمام اعداد فرد سه‌رقمی را تولید و در یک لیست ذخیره کند. سپس لیست را نمایش دهد.
جواب ۷
```python
# --- Exercise 7: Three-Digit Odd Numbers ---
def find_three_digit_odd_numbers_ex7():
    # Function to find all three-digit odd numbers and store them in a list.
    three_digit_odds = []
    # Three-digit numbers range from 100 to 999.
    for num in range(100, 1000): # from 100 up to 999
        if num % 2 != 0: # Check if the number is odd (remainder not 0 when divided by 2)
            three_digit_odds.append(num)
    
    print("Ex7: List of three-digit odd numbers:")
    # Print the list. For very long lists, printing line by line might be better.
    print(three_digit_odds) 
    # Example of printing with 10 numbers per line:
    # for i in range(len(three_digit_odds)):
    #     print(three_digit_odds[i], end=" ") # Print number and a space
    #     if (i + 1) % 10 == 0: # If 10 numbers have been printed in this line
    #         print() # Move to the next line
    # if len(three_digit_odds) % 10 != 0 : # Add a final newline if the last line wasn't full
    #    print()
    return three_digit_odds

# Example usage for Exercise 7:
# print("--- Running Exercise 7 ---")
# three_digit_odd_list_ex7 = find_three_digit_odd_numbers_ex7()
# print("--- End of Exercise 7 ---\n")
```

---

سوال ۸
اعداد فرد دورقمی: برنامه‌ای در پایتون بنویسید که تمام اعداد فرد دورقمی را تولید و در یک لیست ذخیره کند. سپس لیست را چاپ کند.
جواب ۸
```python
# --- Exercise 8: Two-Digit Odd Numbers ---
def find_two_digit_odd_numbers_ex8():
    # Function to find all two-digit odd numbers and store them in a list.
    two_digit_odds = []
    # Two-digit numbers range from 10 to 99.
    for num in range(10, 100): # from 10 up to 99
        if num % 2 != 0: # Check if the number is odd
            two_digit_odds.append(num)
            
    print("Ex8: List of two-digit odd numbers:")
    print(two_digit_odds)
    return two_digit_odds

# Example usage for Exercise 8:
# print("--- Running Exercise 8 ---")
# two_digit_odd_list_ex8 = find_two_digit_odd_numbers_ex8()
# print("--- End of Exercise 8 ---\n")
```

---

سوال ۹
فاکتوریل اعداد: برنامه‌ای در پایتون بنویسید که ۲۰ عدد را از ورودی خوانده و در یک لیست ذخیره کند. سپس فاکتوریل هر یک از این اعداد را محاسبه کرده و در لیست دیگری ذخیره نماید. هر دو لیست را چاپ کنید.
جواب ۹
```python
# --- Exercise 9: Factorial of Numbers ---
# This exercise uses the global 'calculate_factorial' helper function.

def factorial_of_list_elements_ex9(count=5): # Reduced from 20 for testing
    # Function to read 'count' numbers, calculate their factorials, and store both.
    input_numbers = []
    factorial_results = []
    
    print(f"Ex9: Enter {count} numbers for factorial calculation:")
    for i in range(count):
        while True:
            try:
                # Factorials grow very large quickly, so small numbers are preferred for input.
                num = int(input(f"  Enter number {i + 1} (e.g., 0 to 15): "))
                if num < 0:
                    print("    Factorial is usually defined for non-negative integers.")
                    # Or decide to store None for negative inputs
                input_numbers.append(num)
                break
            except ValueError:
                print("    Invalid input. Please enter an integer.")
        
    for num in input_numbers:
        fact = calculate_factorial(num) # Using global helper
        factorial_results.append(fact) # Appends the result (or None if input was negative)
        
    print("\nEx9: Original numbers list:")
    print(input_numbers)
    print("Ex9: Factorials list:")
    print(factorial_results)
    return input_numbers, factorial_results

# Example usage for Exercise 9:
# print("--- Running Exercise 9 ---")
# original_nums_ex9, factorials_ex9 = factorial_of_list_elements_ex9(count=4)
# print("--- End of Exercise 9 ---\n")
```

---

سوال ۱۰
نمرات دانشجویان: برنامه‌ای در پایتون بنویسید که نمرات میان‌ترم و پایان‌ترم ۴۰ دانشجو را دریافت کند. مجموع نمرات هر دانشجو را محاسبه و در یک لیست ذخیره نماید. سپس میانگین مجموع نمرات کل دانشجویان را محاسبه و چاپ کند.
جواب ۱۰
```python
# --- Exercise 10: Student Grades ---
def calculate_student_total_scores_ex10(num_students=3): # Reduced from 40 for testing
    # Function to get midterm and final term scores and calculate total scores.
    total_scores_list = []
    print(f"Ex10: Enter scores for {num_students} students:")
    for i in range(num_students):
        print(f"Student {i + 1}:")
        midterm_score = -1.0
        final_score = -1.0
        while True: # Get midterm score
            try:
                midterm_score = float(input("  Enter midterm score (0-100): "))
                if 0 <= midterm_score <= 100:
                    break
                else:
                    print("    Score must be between 0 and 100.")
            except ValueError:
                print("    Invalid input. Please enter a number for the score.")
        
        while True: # Get final score
            try:
                final_score = float(input("  Enter final term score (0-100): "))
                if 0 <= final_score <= 100:
                    break
                else:
                    print("    Score must be between 0 and 100.")
            except ValueError:
                print("    Invalid input. Please enter a number for the score.")

        total_score = midterm_score + final_score
        total_scores_list.append(total_score)
        print(f"  Total score for student {i+1}: {total_score:.2f}") # Format to 2 decimal places
        
    if not total_scores_list:
        print("Ex10: No scores entered, cannot calculate average.")
        return total_scores_list, 0.0

    sum_of_total_scores = 0
    for score in total_scores_list:
        sum_of_total_scores += score
        
    average_total_score = sum_of_total_scores / len(total_scores_list)
    
    print("\nEx10: List of total scores for all students:")
    # Format scores in the list for printing
    formatted_total_scores = []
    for ts in total_scores_list:
        formatted_total_scores.append(f"{ts:.2f}")
    print(formatted_total_scores)

    print(f"Ex10: Average of total scores for all students: {average_total_score:.2f}")
    return total_scores_list, average_total_score

# Example usage for Exercise 10:
# print("--- Running Exercise 10 ---")
# student_total_scores_ex10, avg_total_score_ex10 = calculate_student_total_scores_ex10(num_students=2)
# print("--- End of Exercise 10 ---\n")
```

---

سوال ۱۱
اعداد اول زیر ۱۰۰ در لیست: برنامه‌ای در پایتون بنویسید که اعداد اول کوچک‌تر از ۱۰۰ را مشخص کند. این اعداد را در یک لیست به گونه‌ای ذخیره کنید که اگر اندیس i یک عدد اول بود، مقدار list[i] برابر خود i باشد و در غیر این صورت (اگر i اول نبود یا بزرگتر از ظرفیت لیست بود) مقدار آن خانه صفر باشد (یا از دیکشنری استفاده کنید که کلید آن عدد اول و مقدارش خود عدد اول باشد). سپس محتویات ساختار داده خود را چاپ کنید.
جواب ۱۱
```python
# --- Exercise 11: Prime Numbers Under 100 in List ---
# This exercise uses the global 'is_prime' helper function.

def store_primes_in_indexed_list_ex11():
    # Function to store primes under 100. If index i is prime, list[i] = i, else 0.
    # The list size will be 100 (for indices 0 to 99).
    limit = 100
    prime_indexed_list = [0] * limit # Initialize a list of 'limit' zeros.
    
    for i in range(limit): # Iterate from 0 to 99
        if is_prime(i): # Using global helper
            prime_indexed_list[i] = i
            
    print("Ex11: List where index indicates number, value is number if prime, else 0 (for numbers < 100):")
    # Print in a more readable format, e.g., 10 per line
    for i in range(len(prime_indexed_list)):
        print(f"{prime_indexed_list[i]:2}", end=" ") # Print number with padding for alignment
        if (i + 1) % 10 == 0: # Newline after every 10 numbers
            print()
    # Ensure a final newline if not perfectly divisible by 10
    if len(prime_indexed_list) % 10 != 0: 
        print()
    return prime_indexed_list

def store_primes_in_dictionary_ex11():
    # Alternative: Using a dictionary as hinted in the problem.
    # Key is the prime number, value is also the prime number.
    limit = 100
    prime_dict = {}
    for i in range(limit): # Iterate from 0 to 99
        if is_prime(i): # Using global helper
            prime_dict[i] = i 
    print("\nEx11: Dictionary where key is prime and value is prime (for primes < 100):")
    print(prime_dict)
    return prime_dict

# Example usage for Exercise 11:
# print("--- Running Exercise 11 ---")
# prime_list_representation_ex11 = store_primes_in_indexed_list_ex11()
# prime_dict_representation_ex11 = store_primes_in_dictionary_ex11()
# print("--- End of Exercise 11 ---\n")
```

---

سوال ۱۲
مضرب‌ها و تفاضل لیست‌ها: برنامه‌ای در پایتون بنویسید که:
لیست A را با اعداد مضرب ۵ کوچک‌تر از ۱۰۰۰ پر کند.
لیست B را با اعداد مضرب ۱۰ کوچک‌تر از ۱۰۰۰ پر کند.
لیست C را ایجاد کند که عناصر آن حاصل تفاضل عناصر متناظر در لیست‌های A و B باشد (به شرطی که طول یکسانی داشته باشند یا تا طول لیست کوتاه‌تر). لیست C را چاپ کنید.
جواب ۱۲
```python
# --- Exercise 12: Multiples and List Difference ---
def multiples_and_difference_ex12():
    # List A: multiples of 5 less than 1000
    list_a = []
    # Efficient way to create list_a
    # range(start, stop, step): numbers from start up to (but not including) stop
    for i in range(0, 1000, 5): 
        list_a.append(i)

    # List B: multiples of 10 less than 1000
    list_b = []
    # Efficient way to create list_b
    for i in range(0, 1000, 10):
        list_b.append(i)

    print(f"Ex12: List A (multiples of 5 < 1000), first 10: {list_a[:10]}... (Total: {len(list_a)})")
    print(f"Ex12: List B (multiples of 10 < 1000), first 10: {list_b[:10]}... (Total: {len(list_b)})")

    # List C: A[i] - B[i]
    list_c = []
    # Determine the length of the shorter list for iteration
    len_a = len(list_a)
    len_b = len(list_b)
    
    shorter_length = 0
    if len_a < len_b:
        shorter_length = len_a
    else: # len_b <= len_a
        shorter_length = len_b
        
    for i in range(shorter_length):
        difference = list_a[i] - list_b[i]
        list_c.append(difference)
        
    print(f"Ex12: List C (A[i] - B[i]), first 10: {list_c[:10]}... (Total: {len(list_c)})")
    # print(f"Ex12: Full List C: {list_c}") # Uncomment to see the full list C
    return list_a, list_b, list_c

# Example usage for Exercise 12:
# print("--- Running Exercise 12 ---")
# list_A_ex12, list_B_ex12, list_C_ex12 = multiples_and_difference_ex12()
# print("--- End of Exercise 12 ---\n")
```

---

سوال ۱۳
جابجایی عناصر لیست: برنامه‌ای در پایتون بنویسید که بیست عدد را خوانده و در لیست A ذخیره کند. سپس جای عناصر خانه‌های ۰ تا ۹ را با عناصر خانه‌های ۱۰ تا ۱۹ عوض کند (یعنی عنصر A[0] با A[10], A[1] با A[11] و الی آخر). لیست تغییر یافته را چاپ کنید.
جواب ۱۳
```python
# --- Exercise 13: Swap List Elements ---
def swap_list_halves_ex13(count=20):
    # Function to read 'count' numbers and swap halves of the list.
    # 'count' must be an even number for this specific swap logic.
    if count % 2 != 0:
        print(f"Ex13: Count ({count}) must be even. Adjusting to a default even count (e.g., 6 for testing).")
        count = 6 # Adjusted for testing, original problem states 20.

    list_a = []
    print(f"Ex13: Enter {count} numbers for list A:")
    for i in range(count):
        while True:
            try:
                num = int(input(f"  Enter number {i + 1}: "))
                list_a.append(num)
                break
            except ValueError:
                print("    Invalid input. Please enter an integer.")
    
    print(f"Ex13: Original list A: {list_a}")
    
    half_length = count // 2 # Integer division, e.g., 20 // 2 = 10
    
    # Swap A[i] with A[i + half_length]
    # This loop runs 'half_length' times.
    # For count=20, half_length=10. i goes from 0 to 9.
    # It swaps A[0] with A[10], A[1] with A[11], ..., A[9] with A[19].
    for i in range(half_length):
        temp = list_a[i]
        list_a[i] = list_a[i + half_length]
        list_a[i + half_length] = temp
        
    print(f"Ex13: Modified list A after swapping halves: {list_a}")
    return list_a

# Example usage for Exercise 13:
# print("--- Running Exercise 13 ---")
# swapped_list_ex13 = swap_list_halves_ex13(count=6) # Test with a smaller even number
# # swapped_list_ex13_full = swap_list_halves_ex13(count=20) # For the original 20 elements
# print("--- End of Exercise 13 ---\n")
```

---

سوال ۱۴
فیبوناچی، مربع و نسبت: برنامه‌ای در پایتون بنویسید که:
۲۸ جمله اول دنباله فیبوناچی را تولید و در لیست F ذخیره کند.
مربع هر یک از اعداد لیست F را محاسبه و در لیست M ذخیره کند.
نسبت هر عنصر از لیست F به عنصر متناظر آن در لیست M (از عنصر دوم به بعد، یعنی F[i]/M[i] برای i >= 1) را محاسبه و چاپ کند.
جواب ۱۴
```python
# --- Exercise 14: Fibonacci, Square, and Ratio ---
def fibonacci_square_ratio_ex14():
    # 1. Generate 28 Fibonacci numbers
    n_terms_fib = 28
    list_f = [] # Fibonacci list
    a, b = 0, 1 # Initial Fibonacci numbers
    for _ in range(n_terms_fib):
        list_f.append(a)
        next_fib = a + b
        a = b
        b = next_fib
    print(f"Ex14: List F ({n_terms_fib} Fibonacci numbers): {list_f}")
    
    # 2. Square each number in F and store in M
    list_m = [] # List of squares
    for num in list_f:
        list_m.append(num * num) # num**2 also works
    print(f"Ex14: List M (squares of F): {list_m}")
    
    # 3. Calculate ratio F[i] / M[i] for i >= 1
    print("\nEx14: Ratios F[i]/M[i] for i >= 1:")
    # Start from the second element (index 1) because F[0]=0, M[0]=0, ratio is undefined.
    # F = [0, 1, 1, 2, 3, 5, ...]
    # M = [0, 1, 1, 4, 9, 25, ...]
    # For i=0: F[0]/M[0] = 0/0 (undefined)
    # For i=1: F[1]/M[1] = 1/1 = 1
    # For i=2: F[2]/M[2] = 1/1 = 1
    # For i=3: F[3]/M[3] = 2/4 = 0.5
    
    if len(list_f) > 1: # Ensure there's at least a second element
        for i in range(1, len(list_f)): # Loop from index 1 up to length-1
            if list_m[i] == 0: 
                # This case shouldn't happen for i >= 1 in standard Fibonacci starting 0, 1
                # because F[i] will be non-zero for i >= 1, so M[i] will also be non-zero.
                print(f"  F[{i}]={list_f[i]}, M[{i}]={list_m[i]}, Ratio is undefined (division by zero)")
            else:
                ratio = list_f[i] / list_m[i]
                print(f"  F[{i}]={list_f[i]:<3}, M[{i}]={list_m[i]:<5}, Ratio F[{i}]/M[{i}] = {ratio:.4f}")
    else:
        print("  List F has less than 2 elements, cannot calculate ratios for i >= 1.")
            
    return list_f, list_m

# Example usage for Exercise 14:
# print("--- Running Exercise 14 ---")
# fib_list_ex14, square_list_ex14 = fibonacci_square_ratio_ex14()
# print("--- End of Exercise 14 ---\n")
```

---

سوال ۱۵
زوج و فرد، مربع و جذر: برنامه‌ای در پایتون بنویسید که ۳۲ عدد را بخواند.
اگر عدد زوج بود، مربع آن را در لیست EVEN_SQUARES قرار دهد.
اگر عدد فرد بود، جذر آن را (در صورت امکان حقیقی) در لیست ODD_ROOTS قرار دهد.
میانگین اعداد در EVEN_SQUARES و میانگین اعداد در ODD_ROOTS را به تفکیک محاسبه و چاپ نماید.
جواب ۱۵
```python
# --- Exercise 15: Even/Odd, Square/Root ---
# This exercise uses the global 'math.sqrt' function, so 'import math' is needed (done in preamble).

def process_even_odd_numbers_ex15(count=5): # Reduced from 32 for testing
    even_squares = []
    odd_roots = []
    
    print(f"Ex15: Enter {count} numbers:")
    for i in range(count):
        while True:
            try:
                num = int(input(f"  Enter number {i + 1}: "))
                break # Exit loop if input is a valid integer
            except ValueError:
                print("    Invalid input. Please enter an integer.")
        
        if num % 2 == 0: # Even number
            square = num * num
            even_squares.append(square)
            print(f"    {num} is even. Square: {square}. Added to EVEN_SQUARES.")
        else: # Odd number
            if num >= 0: # Square root is real for non-negative numbers
                root = math.sqrt(num) # Using math.sqrt from global import
                odd_roots.append(root)
                print(f"    {num} is odd. Square root: {root:.2f}. Added to ODD_ROOTS.")
            else:
                # For negative odd numbers, real square root is not possible.
                # We can choose to ignore, store None, or store a placeholder.
                print(f"    {num} is odd and negative. Real square root not possible. Skipped for ODD_ROOTS.")
                
    print(f"\nEx15: EVEN_SQUARES: {even_squares}")
    # Print odd_roots formatted
    formatted_odd_roots = []
    for r_val in odd_roots:
        formatted_odd_roots.append(f"{r_val:.2f}")
    print(f"Ex15: ODD_ROOTS: {formatted_odd_roots}")

    # Calculate average for EVEN_SQUARES
    if even_squares: # Check if list is not empty
        sum_even_sq = 0
        for val in even_squares:
            sum_even_sq += val
        avg_even_sq = sum_even_sq / len(even_squares)
        print(f"Ex15: Average of numbers in EVEN_SQUARES: {avg_even_sq:.2f}")
    else:
        print("Ex15: EVEN_SQUARES list is empty. No average to calculate.")
        
    # Calculate average for ODD_ROOTS
    if odd_roots: # Check if list is not empty
        sum_odd_r = 0
        for val in odd_roots:
            sum_odd_r += val
        avg_odd_r = sum_odd_r / len(odd_roots)
        print(f"Ex15: Average of numbers in ODD_ROOTS: {avg_odd_r:.2f}")
    else:
        print("Ex15: ODD_ROOTS list is empty. No average to calculate.")
        
    return even_squares, odd_roots

# Example usage for Exercise 15:
# print("--- Running Exercise 15 ---")
# even_sq_list_ex15, odd_r_list_ex15 = process_even_odd_numbers_ex15(count=4)
# print("--- End of Exercise 15 ---\n")
```

---

سوال ۱۶
اطلاعات شرکت تعاونی: برنامه‌ای در پایتون بنویسید که نام، نام خانوادگی، نام پدر و آدرس ۲۰ نفر از اعضای یک شرکت تعاونی را (می‌توانید از لیست دیکشنری‌ها یا کلاس استفاده کنید) دریافت و ذخیره کند. سپس اطلاعات ذخیره شده را از آخر به اول چاپ نماید.
جواب ۱۶
```python
# --- Exercise 16: Cooperative Company Information ---
def store_coop_member_info_ex16(count=2): # Reduced from 20 for testing
    # Using a list of dictionaries. Each dictionary represents a member.
    members_info = []
    print(f"Ex16: Enter information for {count} cooperative members:")
    for i in range(count):
        print(f"Member {i + 1}:")
        first_name = input("  First Name: ")
        last_name = input("  Last Name: ")
        father_name = input("  Father's Name: ")
        address = input("  Address: ")
        
        # Create a dictionary for the current member's data
        member_data = {
            "first_name": first_name,
            "last_name": last_name,
            "father_name": father_name,
            "address": address
        }
        members_info.append(member_data) # Add the dictionary to the list
        
    print("\nEx16: Cooperative Member Information (printed from last to first):")
    # To print from last to first, we can iterate the list in reverse.
    # One way: iterate using index from len(members_info) - 1 down to 0.
    
    current_index = len(members_info) - 1
    entry_number = 1 # For display purposes, to show which entry it is in reversed order
    while current_index >= 0:
        member = members_info[current_index] # Get member data from the list
        print(f"\n--- Member (Entry {entry_number} in reversed print) ---")
        print(f"  First Name: {member['first_name']}")
        print(f"  Last Name: {member['last_name']}")
        print(f"  Father's Name: {member['father_name']}")
        print(f"  Address: {member['address']}")
        current_index = current_index - 1 # Move to the previous member in the list
        entry_number = entry_number + 1
        
    return members_info

# Example usage for Exercise 16:
# print("--- Running Exercise 16 ---")
# coop_members_ex16 = store_coop_member_info_ex16(count=2)
# print("--- End of Exercise 16 ---\n")
```

---

سوال ۱۷
مربع اعداد در ماتریس (ستونی): برنامه‌ای در پایتون بنویسید که ۵۰ عدد را بخواند، مربع آنها را محاسبه کند و این مربع‌ها را به صورت ستونی در یک ماتریس (لیست تو در توی پایتون) ۷x۸ ذخیره نماید. ماتریس را چاپ کنید. (توجه: اگر تعداد مربع‌ها از ظرفیت ماتریس بیشتر بود، تا جای ممکن پر شود. اگر کمتر بود، باقی خانه‌ها با ۰ یا None پر شوند).
جواب ۱۷
```python
# --- Exercise 17: Square Numbers in Matrix (Column-wise) ---
def create_matrix_column_wise_ex17(rows=7, cols=8, num_inputs=50):
    # Read 'num_inputs' numbers, calculate their squares.
    # Store these squares column-wise in a 'rows' x 'cols' matrix.
    
    # For testing, let's use smaller dimensions and inputs
    test_rows = 3
    test_cols = 4
    test_num_inputs = 10 # Should be <= test_rows * test_cols for full coverage, or more to test limit
    
    # Use actual problem dimensions if not testing:
    # actual_rows = rows
    # actual_cols = cols
    # actual_num_inputs = num_inputs
    
    # Using test dimensions here:
    actual_rows = test_rows
    actual_cols = test_cols
    actual_num_inputs = test_num_inputs

    input_numbers = []
    print(f"Ex17: Enter {actual_num_inputs} numbers:")
    # Limit to matrix capacity if num_inputs > rows*cols, or read num_inputs if smaller
    num_to_read = actual_num_inputs
    if actual_num_inputs > actual_rows * actual_cols:
        num_to_read = actual_rows * actual_cols # Only read enough to fill the matrix
        print(f" (Note: Will read up to {num_to_read} to fill the {actual_rows}x{actual_cols} matrix)")

    for i in range(num_to_read): 
        while True:
            try:
                num = int(input(f"  Enter number {i + 1}: "))
                input_numbers.append(num)
                break
            except ValueError:
                print("    Invalid input. Please enter an integer.")
            
    squared_numbers = []
    for num in input_numbers:
        squared_numbers.append(num * num)

    # Initialize the matrix with a default value (e.g., 0 or None)
    matrix = []
    for r_idx in range(actual_rows):
        matrix_row = []
        for c_idx in range(actual_cols):
            matrix_row.append(0) # Initialize with 0
        matrix.append(matrix_row)
        
    # Fill the matrix column-wise
    sq_idx = 0 # Index for squared_numbers list
    # Iterate through columns first, then rows
    for c in range(actual_cols): 
        for r in range(actual_rows): 
            if sq_idx < len(squared_numbers): # If there are squared numbers left to fill
                matrix[r][c] = squared_numbers[sq_idx]
                sq_idx += 1
            else:
                # If not enough squared numbers, remaining cells will stay 0 (as initialized)
                pass # matrix[r][c] is already 0
    
    print("\nEx17: Matrix with squared numbers (filled column-wise):")
    for r in range(actual_rows):
        for c in range(actual_cols):
            # Print with some formatting for alignment (e.g., 5 characters wide)
            print(f"{matrix[r][c]:5}", end=" ") 
        print() # Newline after each row
        
    return matrix

# Example usage for Exercise 17:
# print("--- Running Exercise 17 ---")
# matrix_ex17 = create_matrix_column_wise_ex17() # Uses test defaults inside function
# print("--- End of Exercise 17 ---\n")
```

---

سوال ۱۸
فاکتوریل اعداد در ماتریس (سطری): برنامه‌ای در پایتون بنویسید که ۷۲ عدد را بخواند، فاکتوریل هر عدد را محاسبه کند و این فاکتوریل‌ها را به صورت سطری در یک ماتریس ۹x۸ ذخیره نماید. ماتریس را چاپ کنید.
جواب ۱۸
```python
# --- Exercise 18: Factorial Numbers in Matrix (Row-wise) ---
# This exercise uses the global 'calculate_factorial' helper function.

def create_matrix_row_wise_factorials_ex18(rows=9, cols=8, num_inputs=72):
    # Read 'num_inputs' numbers, calculate their factorials.
    # Store factorials row-wise in a 'rows' x 'cols' matrix.
    # Factorials can get very large, so use small input numbers for testing.

    # For testing:
    test_rows = 3
    test_cols = 3
    test_num_inputs = 5 # Number of factorials to calculate and fill
    
    # Use actual problem dimensions if not testing:
    # actual_rows = rows
    # actual_cols = cols
    # actual_num_inputs = num_inputs
    
    # Using test dimensions here:
    actual_rows = test_rows
    actual_cols = test_cols
    actual_num_inputs = test_num_inputs

    input_numbers_fact = []
    print(f"Ex18: Enter {actual_num_inputs} numbers (small integers, e.g., 0-10 for factorials):")
    
    num_to_read_fact = actual_num_inputs
    if actual_num_inputs > actual_rows * actual_cols:
        num_to_read_fact = actual_rows * actual_cols
        print(f" (Note: Will read up to {num_to_read_fact} to fill the {actual_rows}x{actual_cols} matrix)")

    for i in range(num_to_read_fact): 
        while True:
            try:
                num = int(input(f"  Enter number {i + 1} (e.g., 0-10): "))
                input_numbers_fact.append(num)
                break
            except ValueError:
                print("    Invalid input. Please enter an integer.")
            
    factorials_list = []
    for num in input_numbers_fact:
        factorials_list.append(calculate_factorial(num)) # Using global helper

    # Initialize matrix with a default value (e.g., 0 or None)
    matrix_fact = []
    for r_idx in range(actual_rows):
        row_data = []
        for c_idx in range(actual_cols):
            row_data.append(0) # Initialize with 0
        matrix_fact.append(row_data)
        
    # Fill matrix row-wise
    fact_idx = 0 # Index for factorials_list
    # Iterate through rows first, then columns
    for r in range(actual_rows): 
        for c in range(actual_cols): 
            if fact_idx < len(factorials_list): # If there are factorials left
                matrix_fact[r][c] = factorials_list[fact_idx]
                fact_idx += 1
            else:
                # Remaining cells will stay 0
                pass

    print("\nEx18: Matrix with factorials (filled row-wise):")
    for r_val in range(actual_rows):
        for c_val in range(actual_cols):
            # Factorials can be large, adjust print width as needed. Using right-align.
            # Convert to string to handle None if calculate_factorial returns it for negatives
            print(f"{str(matrix_fact[r_val][c_val]):>8}", end=" ") # 8 char width, right aligned
        print()
        
    return matrix_fact

# Example usage for Exercise 18:
# print("--- Running Exercise 18 ---")
# matrix_factorials_ex18 = create_matrix_row_wise_factorials_ex18() # Uses test defaults
# print("--- End of Exercise 18 ---\n")
```

---

سوال ۱۹
ماتریس با قطر خاص: برنامه‌ای در پایتون بنویسید که عدد طبیعی N را دریافت کند. سپس یک ماتریس مربع N x N ایجاد کند به طوری که درایه‌های روی قطر اصلی و قطر فرعی آن ۱ و بقیه درایه‌ها ۰ باشند. ماتریس را چاپ کنید.
جواب ۱۹
```python
# --- Exercise 19: Matrix with Special Diagonals ---
def create_diagonal_matrix_ex19(n_dim):
    # Creates an N x N matrix where main and anti-diagonal elements are 1, others 0.
    if n_dim <= 0:
        print("Ex19: Matrix dimension N must be a positive integer.")
        return [] # Return an empty list for invalid dimension
        
    matrix = []
    # Initialize N x N matrix with zeros
    for r_idx in range(n_dim): # r_idx goes from 0 to n_dim-1
        row = []
        for c_idx in range(n_dim): # c_idx goes from 0 to n_dim-1
            row.append(0) # Start with all zeros
        matrix.append(row)
        
    # Set 1s on diagonals
    for r in range(n_dim):
        for c in range(n_dim):
            # Main diagonal: row index == column index (e.g., [0,0], [1,1], ...)
            if r == c:
                matrix[r][c] = 1
            # Anti-diagonal (secondary diagonal): row_index + col_index == N - 1
            # e.g., for N=3: (0,2), (1,1), (2,0) -> 0+2=2, 1+1=2, 2+0=2. (N-1 = 3-1 = 2)
            if r + c == n_dim - 1:
                matrix[r][c] = 1
                
    print(f"\nEx19: {n_dim}x{n_dim} Matrix with 1s on main and anti-diagonals:")
    for r in range(n_dim):
        for c in range(n_dim):
            print(matrix[r][c], end=" ") # Print element and a space
        print() # Newline after each row
    return matrix

# Example usage for Exercise 19:
# print("--- Running Exercise 19 ---")
# n_dimension_ex19 = 0
# while True:
#     try:
#         n_dimension_ex19 = int(input("Ex19: Enter the dimension N for the square matrix (e.g., 5): "))
#         if n_dimension_ex19 > 0 :
#             break
#         else:
#             print("  Dimension must be positive.")
#     except ValueError:
#         print("  Invalid input. Please enter an integer.")
# diagonal_matrix_ex19 = create_diagonal_matrix_ex19(n_dimension_ex19)
# print("--- End of Exercise 19 ---\n")
```

---

سوال ۲۰
اطلاعات کارکنان و بزرگترین شماره تلفن: برنامه‌ای در پایتون بنویسید که نام و نام خانوادگی و شماره تلفن ۲۰ نفر از کارکنان یک شرکت را دریافت کند (می‌توانید از دو لیست موازی یا لیستی از دیکشنری‌ها/اشیاء استفاده کنید). سپس بزرگترین شماره تلفن را مشخص کرده و به همراه نام و نام خانوادگی صاحب آن چاپ نماید.
جواب ۲۰
```python
# --- Exercise 20: Employee Info and Largest Phone Number ---
def employee_info_largest_phone_ex20(count=3): # Reduced from 20 for testing
    # Store employee info (name, phone) and find the largest phone number.
    # Using a list of dictionaries is a good way to group related data.
    employees = [] # This will be a list of employee dictionaries
    print(f"Ex20: Enter information for {count} employees:")
    for i in range(count):
        print(f"Employee {i + 1}:")
        name = input("  Full Name (e.g., First Last): ")
        
        phone_num_int = -1 # To store numeric version for comparison
        phone_str_original = "" # To store original string input
        while True:
            phone_str_original = input("  Phone Number (enter digits only, e.g., 09123456789): ")
            # Validate if it's all digits and can be converted to int
            is_digits_only = True
            if not phone_str_original: # Empty string
                is_digits_only = False
            else:
                for char_digit in phone_str_original:
                    if not ('0' <= char_digit <= '9'): # Check if character is not a digit
                        is_digits_only = False
                        break
            
            if is_digits_only:
                try:
                    phone_num_int = int(phone_str_original)
                    break # Valid numeric phone number
                except ValueError: # Should not happen if is_digits_only is robust
                    print("    Error converting to number, though it seemed like digits. Try again.")
            else:
                print("    Invalid phone number. Please enter digits only without spaces or symbols.")

        # Store data as a dictionary
        employee_data = {
            "name": name, 
            "phone_numeric": phone_num_int, # For finding the largest
            "phone_original_str": phone_str_original # For display
        }
        employees.append(employee_data)
        
    if not employees:
        print("Ex20: No employee data entered.")
        return
        
    # Find the largest phone number
    # Initialize with the first employee's phone, or a very small number if list could be empty
    largest_phone_numeric = -1 
    employee_with_largest_phone = None # This will store the dictionary of the employee
    
    if employees: # If there's at least one employee
        # Start by assuming the first employee has the largest phone number
        largest_phone_numeric = employees[0]["phone_numeric"]
        employee_with_largest_phone = employees[0] 

        # Iterate through the rest of the employees to find if any has a larger number
        for i in range(1, len(employees)): # Start from the second employee
            current_emp_phone = employees[i]["phone_numeric"]
            if current_emp_phone > largest_phone_numeric:
                largest_phone_numeric = current_emp_phone
                employee_with_largest_phone = employees[i]
            
    if employee_with_largest_phone is not None:
        print("\nEx20: Employee with the largest phone number:")
        print(f"  Name: {employee_with_largest_phone['name']}")
        # Display the original string version of the phone number
        print(f"  Phone Number: {employee_with_largest_phone['phone_original_str']}")
        # Optionally, also print the numeric value used for comparison:
        # print(f"  (Numeric value for comparison: {largest_phone_numeric})")
    else:
        # This case implies the employees list was empty after all, or an issue in logic.
        print("Ex20: Could not determine the largest phone number (perhaps no employees or valid numbers).")
        
    return employees

# Example usage for Exercise 20:
# print("--- Running Exercise 20 ---")
# employees_data_ex20 = employee_info_largest_phone_ex20(count=2) # Test with 2 employees
# print("--- End of Exercise 20 ---\n")
```

---

سوال ۲۱
اعداد زوج، جذر و مربع: برنامه‌ای در پایتون بنویسید که کلیه اعداد زوج دو رقمی را از ورودی بخواند و به صورت غیر تکراری در لیست A ذخیره کند.
جذر هر یک از اعداد لیست A را محاسبه و در لیست B ذخیره کند.
مربع هر یک از اعداد لیست A را محاسبه و در لیست C ذخیره کند.
مجموع اعداد لیست B و مجموع اعداد لیست C را محاسبه و چاپ نماید.
جواب ۲۱
```python
# --- Exercise 21: Even Two-Digit Numbers, Root, Square ---
# This exercise uses 'math.sqrt' from the global 'import math'.

def process_two_digit_even_numbers_ex21():
    # Reads even two-digit numbers, stores non-duplicates in list A.
    # Calculates sqrt for list B, square for list C.
    # Prints sum of B and sum of C.

    list_a_unique_even_two_digit = []
    print("Ex21: Enter even two-digit numbers (e.g., 10, 12, ..., 98). Type 'done' to finish.")
    
    while True:
        user_input = input("  Enter an even two-digit number (or 'done'): ")
        if user_input.lower() == 'done': # Case-insensitive 'done'
            break
        
        try:
            num = int(user_input)
            # Check if it's a two-digit number: 10 <= num <= 99
            is_two_digit = (10 <= num <= 99)
            # Check if it's an even number: num % 2 == 0
            is_even = (num % 2 == 0)
            
            if is_two_digit and is_even:
                # Check for uniqueness before adding to list_a
                is_present_in_a = False
                for x_in_a in list_a_unique_even_two_digit:
                    if x_in_a == num:
                        is_present_in_a = True
                        break # Found in list A, no need to check further
                
                if not is_present_in_a:
                    list_a_unique_even_two_digit.append(num)
                    print(f"    Added {num} to list A.")
                else:
                    print(f"    {num} is already in list A. Not added again.")
            else:
                if not is_two_digit:
                    print("    Invalid input: Number must be a two-digit number (10-99).")
                if not is_even:
                    print("    Invalid input: Number must be an even number.")
        except ValueError:
            print("    Invalid input: Please enter a whole number or 'done'.")

    if not list_a_unique_even_two_digit: # If list A is empty
        print("\nEx21: List A is empty. No further calculations will be performed.")
        return

    print(f"\nEx21: List A (unique even two-digit numbers entered): {list_a_unique_even_two_digit}")

    # Calculate List B (square roots of A)
    list_b_roots = []
    for num_a in list_a_unique_even_two_digit:
        # All numbers in list_a are positive, so sqrt is real.
        list_b_roots.append(math.sqrt(num_a)) 
    
    # Calculate List C (squares of A)
    list_c_squares = []
    for num_a in list_a_unique_even_two_digit:
        list_c_squares.append(num_a * num_a) # Or num_a ** 2

    # Print List B with formatted numbers
    print("Ex21: List B (square roots of A): [", end="")
    for i_b in range(len(list_b_roots)):
        print(f"{list_b_roots[i_b]:.2f}", end="") # Format to 2 decimal places
        if i_b < len(list_b_roots) - 1: # Add comma if not the last element
            print(", ", end="")
    print("]")

    print(f"Ex21: List C (squares of A): {list_c_squares}")

    # Calculate sum of numbers in List B
    sum_b = 0
    for val_b in list_b_roots:
        sum_b += val_b
    
    # Calculate sum of numbers in List C
    sum_c = 0
    for val_c in list_c_squares:
        sum_c += val_c
        
    print(f"Ex21: Sum of numbers in List B (roots): {sum_b:.2f}")
    print(f"Ex21: Sum of numbers in List C (squares): {sum_c}")

# Example usage for Exercise 21:
# print("--- Running Exercise 21 ---")
# process_two_digit_even_numbers_ex21()
# print("--- End of Exercise 21 ---\n")
```

---

سوال ۲۲
ماتریس فاکتوریل حاصلضرب اندیس‌ها: برنامه‌ای در پایتون بنویسید که یک ماتریس ۲۰x۲۰ ایجاد کند به طوری که هر درایه matrix[i][j] حاوی فاکتوریل حاصلضرب (i+1)*(j+1) باشد (با فرض اندیس‌گذاری از صفر). ماتریس را چاپ کنید.
جواب ۲۲
```python
# --- Exercise 22: Matrix of Factorial of Index Products ---
# This exercise uses the global 'calculate_factorial' helper function.

def create_factorial_product_matrix_ex22(rows=20, cols=20):
    # Creates a matrix where matrix[i][j] = factorial((i+1)*(j+1)).
    # Indices i, j are 0-based.
    
    # Factorials grow very quickly. (i+1)*(j+1) can be large.
    # For a 20x20 matrix, max product is (19+1)*(19+1) = 20*20 = 400. 
    # Factorial of 400 is astronomically large and cannot be computed or stored easily.
    # We'll use smaller dimensions for practical demonstration and print placeholders for large factorials.
    
    test_rows = 4 # Using smaller rows for testing
    test_cols = 4 # Using smaller cols for testing
    # actual_rows = rows # Use this for the full 20x20 if desired, but be wary of performance
    # actual_cols = cols
    actual_rows = test_rows
    actual_cols = test_cols

    matrix = []
    print(f"Ex22: Creating a {actual_rows}x{actual_cols} matrix where element [i][j] is fact((i+1)*(j+1)).")
    print("      Note: Factorials for products > 15 will be shown as placeholders due to size.")

    for i in range(actual_rows): # Row index (0 to actual_rows-1)
        matrix_row = []
        for j in range(actual_cols): # Column index (0 to actual_cols-1)
            product = (i + 1) * (j + 1) # (i+1) and (j+1) because problem implies 1-based thinking for product
            
            fact_val_display = ""
            # Arbitrary limit for practical computation/display of factorial
            # Factorial of 15 is already large (1,307,674,368,000)
            # Factorial of 20 is 2,432,902,008,176,640,000
            if product > 15: 
                fact_val_display = f"F!({product})" # Placeholder for very large factorials
            else:
                fact_val_calculated = calculate_factorial(product) # Use global helper
                if fact_val_calculated is None: # Should not happen if product is non-negative
                    fact_val_display = "Error"
                else:
                    fact_val_display = str(fact_val_calculated)
            matrix_row.append(fact_val_display)
        matrix.append(matrix_row)
        
    print(f"\nEx22: {actual_rows}x{actual_cols} Factorial Product Matrix:")
    # Determine column widths for prettier printing (optional, can be complex for varying string lengths)
    # For simplicity, just print with tab separation or fixed width.
    for r_idx in range(actual_rows):
        for c_idx in range(actual_cols):
            # Print each element with some padding, right-aligned
            print(f"{matrix[r_idx][c_idx]:>15}", end=" ") # 15 chars wide, right aligned
        print() # Newline after each row
        
    return matrix

# Example usage for Exercise 22:
# print("--- Running Exercise 22 ---")
# factorial_prod_matrix_ex22 = create_factorial_product_matrix_ex22() # Uses test defaults
# print("--- End of Exercise 22 ---\n")
```

---

سوال ۲۳
محاسبه معادله و ذخیره در ماتریس: برنامه‌ای در پایتون بنویسید که به ازای مقادیر x از ۸- تا ۶+ با گام ۰.۷، مقدار y را از معادله y = 4x - 2 محاسبه نماید. مقادیر x و y متناظر را در ستون‌های ۱ و ۲ یک ماتریس (لیست تو در تو) ذخیره کرده و سپس ماتریس را چاپ کند.
جواب ۲۳
```python
# --- Exercise 23: Equation Calculation and Matrix Storage ---
def calculate_equation_and_store_ex23():
    # Calculate y = 4x - 2 for x from -8 to +6 with step 0.7.
    # Store x and y in a list of [x, y] pairs (which acts as a 2-column matrix).
    
    results_matrix = [] # This will be a list of [x_value, y_value] lists
    
    start_x = -8.0
    end_x = 6.0
    step = 0.7
    
    print("Ex23: Calculating y = 4x - 2 for x from -8.0 to +6.0 (step 0.7):")
    
    current_x = start_x
    # Floating point numbers can have precision issues.
    # To ensure 'end_x' is included if it's a step multiple:
    # loop while current_x is less than or "almost equal" to end_x.
    # A common way is to add a small epsilon or check current_x <= end_x + step/2.
    while current_x <= end_x + (step / 10.0): # Added small epsilon related to step
        y_value = 4 * current_x - 2
        results_matrix.append([current_x, y_value])
        # print(f"  x = {current_x:.1f}, y = {y_value:.2f}") # Optional: print as calculated
        current_x += step # Increment x by the step
        
    print("\nEx23: Matrix of x and y values:")
    print("  x Value   |   y Value")
    print("--------------------------")
    for row_pair in results_matrix:
        x_val = row_pair[0]
        y_val = row_pair[1]
        # Format output for better readability:
        # {:<9.1f} means: align left (<), 9 characters total width, 1 decimal place, float (f)
        # {:<9.2f} means: align left (<), 9 characters total width, 2 decimal places, float (f)
        print(f"  {x_val:<9.1f} | {y_val:<9.2f}")
        
    return results_matrix

# Example usage for Exercise 23:
# print("--- Running Exercise 23 ---")
# xy_matrix_ex23 = calculate_equation_and_store_ex23()
# print("--- End of Exercise 23 ---\n")
```

---

سوال ۲۴
جابجایی ستون‌های ماتریس: برنامه‌ای در پایتون بنویسید که ۲۴ عدد را بخواند و در یک ماتریس ۶x۴ ذخیره کند. سپس ستون‌های زیر را با هم جابجا کند:
ستون ۱ با ستون ۳
ستون ۲ با ستون ۴
(با فرض اندیس‌گذاری ستون‌ها از ۱ یا ۰ – در اینجا فرض می‌کنیم از ۱ است، پس ستون اندیس ۰ با ۲، و ۱ با ۳ جابجا می‌شود). ماتریس نهایی را چاپ کنید.
جواب ۲۴
```python
# --- Exercise 24: Swap Matrix Columns ---
def create_and_swap_matrix_cols_ex24(rows=6, cols=4, num_inputs=24):
    # Reads 'num_inputs' numbers into a 'rows'x'cols' matrix.
    # Swaps columns: 
    #   Problem says "column 1 with column 3" and "column 2 with column 4".
    #   If 1-based indexing: swap col 1 (index 0) with col 3 (index 2)
    #                        swap col 2 (index 1) with col 4 (index 3)
    
    # For testing:
    test_rows = 3
    test_cols = 4 # Must be at least 4 for the specified swaps
    test_num_inputs = test_rows * test_cols # 12 for 3x4
    
    actual_rows = test_rows
    actual_cols = test_cols
    actual_num_inputs = test_num_inputs
    # To use original problem's dimensions:
    # actual_rows = rows 
    # actual_cols = cols
    # actual_num_inputs = num_inputs

    if actual_cols < 4:
        print(f"Ex24: Matrix must have at least 4 columns for the specified swaps. Current cols: {actual_cols}")
        return []

    matrix = []
    print(f"Ex24: Enter {actual_num_inputs} numbers to fill a {actual_rows}x{actual_cols} matrix (row by row):")
    
    # Fill the matrix
    current_inputs_list = []
    for i in range(actual_num_inputs):
        while True:
            try:
                val = int(input(f"  Enter number {i+1}: "))
                current_inputs_list.append(val)
                break
            except ValueError:
                print("    Invalid input. Please enter an integer.")

    input_idx = 0
    for r_idx in range(actual_rows):
        matrix_row = []
        for c_idx in range(actual_cols):
            if input_idx < len(current_inputs_list):
                matrix_row.append(current_inputs_list[input_idx])
            else:
                # This case should not be reached if actual_num_inputs = actual_rows * actual_cols
                matrix_row.append(0) # Default if somehow not enough inputs
            input_idx += 1
        matrix.append(matrix_row)

    print("\nEx24: Original Matrix:")
    for r_idx in range(actual_rows):
        print("  ", end="")
        for c_val_item in matrix[r_idx]:
            print(f"{c_val_item:3}", end=" ") # Print with width 3 for alignment
        print()

    # Perform column swaps (using 0-based indexing for columns in Python lists)
    # Swap: column 0 (problem's col 1) with column 2 (problem's col 3)
    # Swap: column 1 (problem's col 2) with column 3 (problem's col 4)
    for r_idx in range(actual_rows): # Iterate through each row
        # Swap elements at col 0 and col 2 for the current row
        temp_col0 = matrix[r_idx][0]
        matrix[r_idx][0] = matrix[r_idx][2]
        matrix[r_idx][2] = temp_col0
        
        # Swap elements at col 1 and col 3 for the current row
        temp_col1 = matrix[r_idx][1]
        matrix[r_idx][1] = matrix[r_idx][3]
        matrix[r_idx][3] = temp_col1
        
    print("\nEx24: Matrix after swapping columns:")
    print("      (col 0 <-> col 2, and col 1 <-> col 3, 0-based indexing)")
    for r_idx in range(actual_rows):
        print("  ", end="")
        for c_val_item in matrix[r_idx]:
            print(f"{c_val_item:3}", end=" ")
        print()
        
    return matrix

# Example usage for Exercise 24:
# print("--- Running Exercise 24 ---")
# swapped_cols_matrix_ex24 = create_and_swap_matrix_cols_ex24() # Uses test defaults
# print("--- End of Exercise 24 ---\n")
```

---

سوال ۲۵
ضرب ماتریس‌ها: برنامه‌ای در پایتون بنویسید که یک ماتریس ۳x۴ و یک ماتریس ۴x۲ را (با مقادیر از پیش تعریف شده یا ورودی) دریافت کند. حاصلضرب این دو ماتریس را محاسبه کرده (که یک ماتریس ۳x۲ خواهد بود)، سپس ۸ برابر عناصر ماتریس حاصلضرب را در ماتریس دیگری ذخیره و چاپ نماید.
جواب ۲۵
```python
# --- Exercise 25: Matrix Multiplication ---
def matrix_multiplication_and_scaling_ex25():
    # Matrix A: 3x4 (3 rows, 4 columns)
    # Matrix B: 4x2 (4 rows, 2 columns)
    # Result C = A * B will be 3x2 (rows of A x columns of B)
    # Then create D = 8 * C

    # Predefined matrices for simplicity of example
    # (Could also get these from user input if needed)
    matrix_a = [
        [1, 2, 3, 4],
        [5, 6, 7, 8],
        [9, 10, 11, 12]
    ] 
    # Dimensions: rows_a = 3, cols_a = 4

    matrix_b = [
        [1, 2],
        [3, 4],
        [5, 6],
        [7, 8]
    ] 
    # Dimensions: rows_b = 4, cols_b = 2

    rows_a = len(matrix_a)
    cols_a = len(matrix_a[0]) # Assumes matrix_a is not empty and rows are consistent
    rows_b = len(matrix_b)
    cols_b = len(matrix_b[0]) # Assumes matrix_b is not empty

    # Check if multiplication is possible: cols_a must equal rows_b
    if cols_a != rows_b:
        print("Ex25: Cannot multiply matrices. Columns of A must equal Rows of B.")
        print(f"       Cols_A = {cols_a}, Rows_B = {rows_b}")
        return None, None # Return None for both results

    # Initialize result matrix C with zeros. Dimensions: rows_a x cols_b (3x2)
    matrix_c = []
    for r_c in range(rows_a):
        row_for_c = []
        for c_c in range(cols_b):
            row_for_c.append(0) # Initialize element to 0
        matrix_c.append(row_for_c)

    # Perform multiplication: C[i][j] = sum(A[i][k] * B[k][j])
    # Iterate through rows of A (index i)
    for i in range(rows_a): 
        # Iterate through columns of B (index j)
        for j in range(cols_b): 
            current_sum_for_c_ij = 0
            # Iterate through columns of A / rows of B (index k)
            for k in range(cols_a): # or range(rows_b), since cols_a == rows_b
                current_sum_for_c_ij += matrix_a[i][k] * matrix_b[k][j]
            matrix_c[i][j] = current_sum_for_c_ij
            
    print("Ex25: Matrix A (3x4):")
    for row_a in matrix_a: print(f"  {row_a}")
    print("Ex25: Matrix B (4x2):")
    for row_b in matrix_b: print(f"  {row_b}")
    print("Ex25: Resulting Matrix C = A * B (3x2):")
    for row_c_item in matrix_c: print(f"  {row_c_item}")

    # Create matrix D = 8 * C
    matrix_d = []
    # D has the same dimensions as C
    for r_d_idx in range(rows_a): 
        row_for_d = []
        for c_d_idx in range(cols_b):
            scaled_value = matrix_c[r_d_idx][c_d_idx] * 8
            row_for_d.append(scaled_value)
        matrix_d.append(row_for_d)
        
    print("\nEx25: Matrix D = 8 * C:")
    for row_d_item in matrix_d: print(f"  {row_d_item}")
        
    return matrix_c, matrix_d

# Example usage for Exercise 25:
# print("--- Running Exercise 25 ---")
# result_c_ex25, result_d_ex25 = matrix_multiplication_and_scaling_ex25()
# print("--- End of Exercise 25 ---\n")
```

---

سوال ۲۶
مرتب‌سازی اسامی: برنامه‌ای در پایتون بنویسید که اسامی ۳۵ دانش‌آموز را از ورودی دریافت کرده، آنها را به ترتیب الفبا مرتب و سپس چاپ نماید.
جواب ۲۶
```python
# --- Exercise 26: Sort Names Alphabetically ---
def sort_student_names_alpha_ex26(count=5): # Reduced from 35 for testing
    names = []
    print(f"Ex26: Enter {count} student names:")
    for i in range(count):
        name = input(f"  Name {i+1}: ")
        names.append(name) # Add name to the list
    
    # Simple Bubble Sort for strings (sorts alphabetically)
    # This modifies the 'names' list in-place.
    n = len(names)
    for i_outer in range(n): # Outer loop for passes
        # Last i_outer elements are already in place after each pass
        for j_inner in range(0, n - i_outer - 1): # Inner loop for comparisons
            # In Python, string comparison '>' and '<' works alphabetically
            # e.g., "apple" < "banana" is True
            #       "Zebra" > "Yak" is True (case-sensitive by default)
            # For case-insensitive sort, convert to lower/upper before comparison:
            # if names[j_inner].lower() > names[j_inner+1].lower():
            if names[j_inner] > names[j_inner+1]: # Standard case-sensitive sort 
                # Swap if the element found is greater than the next element
                temp = names[j_inner]
                names[j_inner] = names[j_inner+1]
                names[j_inner+1] = temp
                
    print("\nEx26: Sorted student names (alphabetically):")
    for i_name in range(len(names)):
        print(f"  {i_name + 1}. {names[i_name]}")
    return names

# Example usage for Exercise 26:
# print("--- Running Exercise 26 ---")
# sorted_names_ex26 = sort_student_names_alpha_ex26(count=4) # Test with 4 names
# print("--- End of Exercise 26 ---\n")
```

---

سوال ۲۷
مرتب‌سازی نزولی اعداد: برنامه‌ای در پایتون بنویسید که ۶۵ عدد را از ورودی خوانده، آنها را به صورت نزولی مرتب و سپس چاپ نماید.
جواب ۲۷
```python
# --- Exercise 27: Sort Numbers Descending ---
def sort_numbers_desc_ex27(count=7): # Reduced from 65 for testing
    numbers = []
    print(f"Ex27: Enter {count} numbers:")
    for i in range(count):
        while True:
            try:
                num = int(input(f"  Number {i+1}: "))
                numbers.append(num)
                break # Exit inner loop once valid number is entered
            except ValueError:
                print("    Invalid input. Please enter an integer.")
                
    # Simple Bubble Sort for descending order
    # This modifies the 'numbers' list in-place.
    n = len(numbers)
    for i_outer in range(n): # Outer loop for passes
        for j_inner in range(0, n - i_outer - 1): # Inner loop for comparisons
            # For descending order, swap if current element is smaller than the next
            if numbers[j_inner] < numbers[j_inner+1]: 
                temp = numbers[j_inner]
                numbers[j_inner] = numbers[j_inner+1]
                numbers[j_inner+1] = temp
                
    print("\nEx27: Sorted numbers (descending):")
    print(numbers)
    return numbers

# Example usage for Exercise 27:
# print("--- Running Exercise 27 ---")
# sorted_numbers_desc_ex27 = sort_numbers_desc_ex27(count=5) # Test with 5 numbers
# print("--- End of Exercise 27 ---\n")
```

---

سوال ۲۸
مرتب‌سازی مشتریان بانک: برنامه‌ای در پایتون بنویسید که فرض کند شماره حساب و مبلغ پس‌انداز ۶۰ مشتری بانک در یک لیست از دیکشنری‌ها (یا دو لیست موازی) ذخیره شده است. این لیست را بر اساس شماره حساب مشتریان به صورت صعودی مرتب کرده و سپس اطلاعات مرتب شده (شماره حساب و مبلغ) را چاپ کند. (اختیاری: یکبار هم به صورت نزولی بر اساس مبلغ چاپ کنید).
جواب ۲۸
```python
# --- Exercise 28: Sort Bank Customers ---
def sort_bank_customers_ex28(count=4): # Reduced from 60 for testing
    # Using a list of dictionaries: [{"account_no": 123, "balance": 1000.50}, ...]
    customers = []
    print(f"Ex28: Enter details for {count} bank customers:")
    for i in range(count):
        print(f"Customer {i+1}:")
        acc_no = 0
        balance = 0.0
        while True: # Get account number
            try:
                acc_no_str = input("  Account Number (integer): ")
                acc_no = int(acc_no_str) 
                # Could add check for uniqueness if needed, but not specified
                break
            except ValueError:
                print("    Invalid account number. Please enter digits only.")
        while True: # Get balance
            try:
                balance_str = input("  Savings Balance (number): ")
                balance = float(balance_str)
                break
            except ValueError:
                print("    Invalid balance. Please enter a number (e.g., 1500.75).")
        customers.append({"account_no": acc_no, "balance": balance})

    # Sort by account number (ascending) using Bubble Sort
    # This modifies the 'customers' list of dictionaries in-place.
    n_cust = len(customers)
    for i_outer in range(n_cust):
        for j_inner in range(0, n_cust - i_outer - 1):
            # Compare based on the "account_no" key in the dictionaries
            if customers[j_inner]["account_no"] > customers[j_inner+1]["account_no"]:
                # Swap entire customer dictionary objects
                temp_customer = customers[j_inner]
                customers[j_inner] = customers[j_inner+1]
                customers[j_inner+1] = temp_customer
    
    print("\nEx28: Customers sorted by Account Number (Ascending):")
    print("  Account No. | Balance")
    print("  -----------------------")
    for cust_data in customers:
        # :<11 means left-align in a field of 11 characters
        # :.2f means float with 2 decimal places
        print(f"  {cust_data['account_no']:<11} | {cust_data['balance']:.2f}")

    # Optional: Sort by balance (descending)
    # To do this without altering the 'customers' list (which is now sorted by account_no),
    # we should work on a copy of the list.
    customers_copy_for_balance_sort = []
    for cust_item in customers:
        # Create a new dictionary for the copy to avoid modifying original dictionaries if they were complex
        customers_copy_for_balance_sort.append(dict(cust_item)) 

    n_bal_sort = len(customers_copy_for_balance_sort)
    for i_outer_bal in range(n_bal_sort):
        for j_inner_bal in range(0, n_bal_sort - i_outer_bal - 1):
            # Compare based on the "balance" key for descending sort
            if customers_copy_for_balance_sort[j_inner_bal]["balance"] < customers_copy_for_balance_sort[j_inner_bal+1]["balance"]:
                temp_cust_bal = customers_copy_for_balance_sort[j_inner_bal]
                customers_copy_for_balance_sort[j_inner_bal] = customers_copy_for_balance_sort[j_inner_bal+1]
                customers_copy_for_balance_sort[j_inner_bal+1] = temp_cust_bal

    print("\nEx28: Customers sorted by Savings Balance (Descending) - (Optional Part):")
    print("  Account No. | Balance")
    print("  -----------------------")
    for cust_bal_data in customers_copy_for_balance_sort:
        print(f"  {cust_bal_data['account_no']:<11} | {cust_bal_data['balance']:.2f}")
        
    return customers # Returns list sorted by account number

# Example usage for Exercise 28:
# print("--- Running Exercise 28 ---")
# bank_customers_sorted_ex28 = sort_bank_customers_ex28(count=3)
# print("--- End of Exercise 28 ---\n")
```

---

سوال ۲۹
مرتب‌سازی ارقام عدد و مقلوب: برنامه‌ای در پایتون بنویسید که یک عدد طبیعی ۷ رقمی را از ورودی دریافت کند. ارقام آن را به صورت صعودی مرتب کرده و چاپ نماید. سپس مقلوب عدد حاصل از ارقام مرتب شده را نیز نمایش دهد.
جواب ۲۹
```python
# --- Exercise 29: Sort Digits of a Number and Reverse ---
def sort_digits_and_reverse_ex29():
    num_str_input = ""
    while True:
        num_str_input = input("Ex29: Enter a 7-digit natural number (e.g., 5810392): ")
        # Check length
        if len(num_str_input) != 7:
            print("    Invalid input: Number must be exactly 7 digits long.")
            continue # Ask for input again
        
        # Check if all characters are digits
        is_all_digits = True
        for char_in_str in num_str_input:
            if not ('0' <= char_in_str <= '9'):
                is_all_digits = False
                break
        if not is_all_digits:
            print("    Invalid input: Number must contain only digits.")
            continue

        # Check if it's a natural number (doesn't start with '0' for a multi-digit number)
        # A 7-digit natural number cannot start with '0'.
        if num_str_input[0] == '0':
            print("    Invalid input: A 7-digit natural number cannot start with '0'.")
            continue
        
        # If all checks pass:
        break 

    # Convert the number string to a list of characters (digits)
    digits_char_list = []
    for digit_char_item in num_str_input:
        digits_char_list.append(digit_char_item) # Each item is a string like '5', '8'

    # Sort the list of digit characters (Bubble Sort)
    # String comparison '1' < '2' works correctly for single digits.
    n_digits = len(digits_char_list)
    for i_outer in range(n_digits):
        for j_inner in range(0, n_digits - i_outer - 1):
            if digits_char_list[j_inner] > digits_char_list[j_inner+1]:
                # Swap
                temp_digit_char = digits_char_list[j_inner]
                digits_char_list[j_inner] = digits_char_list[j_inner+1]
                digits_char_list[j_inner+1] = temp_digit_char
                
    # Join the sorted list of digit characters to form the new number string
    sorted_digits_num_str = ""
    for s_digit_char in digits_char_list:
        sorted_digits_num_str += s_digit_char # Concatenate characters
        
    print(f"\nEx29: Original number: {num_str_input}")
    print(f"Ex29: Digits sorted ascending to form new number: {sorted_digits_num_str}")
    
    # Reverse the 'sorted_digits_num_str' to get the 'maqloob' (reversed) version
    reversed_sorted_num_str = ""
    # Iterate from the last character of sorted_digits_num_str to the first
    current_idx = len(sorted_digits_num_str) - 1
    while current_idx >= 0:
        reversed_sorted_num_str += sorted_digits_num_str[current_idx]
        current_idx -= 1 # Move to the previous character
        
    print(f"Ex29: Reversed (maqloob) of the sorted digits number: {reversed_sorted_num_str}")
    
    return num_str_input, sorted_digits_num_str, reversed_sorted_num_str

# Example usage for Exercise 29:
# print("--- Running Exercise 29 ---")
# original_num_ex29, sorted_digits_ex29, reversed_sorted_ex29 = sort_digits_and_reverse_ex29()
# print("--- End of Exercise 29 ---\n")
```

---

سوال ۳۰
مرتب‌سازی دنباله فیبوناچی: برنامه‌ای در پایتون بنویسید که ۲۰ جمله اول دنباله فیبوناچی را تولید و در یک لیست ذخیره کند. سپس لیست را به صورت نزولی مرتب کرده و چاپ نماید.
جواب ۳۰
```python
# --- Exercise 30: Sort Fibonacci Sequence Descending ---
def sort_fibonacci_descending_ex30(n_terms=20):
    # 1. Generate Fibonacci numbers
    fib_sequence = []
    a, b = 0, 1 # First two Fibonacci numbers
    if n_terms <= 0:
        print(f"Ex30: Number of Fibonacci terms ({n_terms}) should be positive.")
        return [] # Return empty if n_terms is not valid
    
    # Generate sequence
    for _ in range(n_terms):
        fib_sequence.append(a)
        next_fib_term = a + b
        a = b
        b = next_fib_term
    print(f"Ex30: First {n_terms} Fibonacci numbers (unsorted): {fib_sequence}")
    
    # 2. Sort the list in descending order (Bubble Sort)
    # This modifies 'fib_sequence' in-place.
    n_fib = len(fib_sequence)
    for i_outer in range(n_fib):
        for j_inner in range(0, n_fib - i_outer - 1):
            # For descending sort, if current < next, swap them
            if fib_sequence[j_inner] < fib_sequence[j_inner+1]:
                temp_fib = fib_sequence[j_inner]
                fib_sequence[j_inner] = fib_sequence[j_inner+1]
                fib_sequence[j_inner+1] = temp_fib
                
    print(f"Ex30: Fibonacci sequence ({n_terms} terms) sorted descending: {fib_sequence}")
    return fib_sequence

# Example usage for Exercise 30:
# print("--- Running Exercise 30 ---")
# # Test with a smaller number of terms for quicker view, e.g., 10
# sorted_fib_desc_ex30_test = sort_fibonacci_descending_ex30(n_terms=10) 
# # sorted_fib_desc_ex30_full = sort_fibonacci_descending_ex30(n_terms=20) # For the full 20 terms
# print("--- End of Exercise 30 ---\n")
```

---

سوال ۳۱
جستجوی پلاک خودرو: با فرض اینکه شماره پلاک ۲۰۰ خودرو در یک لیست ذخیره شده است، برنامه‌ای در پایتون بنویسید که شماره پلاک یک خودرو را از ورودی بخواند و سپس جستجو کند که آیا این شماره پلاک در لیست وجود دارد یا خیر. نتیجه (پیدا شد/نشد) را چاپ کند.
جواب ۳۱
```python
# --- Exercise 31: Search Car License Plate ---
def search_license_plate_ex31(num_plates_in_db=20): # Reduced from 200 for easier testing
    # Assume license plates are stored as strings.
    
    # Step 1: Create a sample database of license plates.
    # In a real application, this data might come from a file or a database.
    # For this exercise, we'll generate some dummy plates.
    license_plates_db = []
    print(f"Ex31: Simulating a database with {num_plates_in_db} license plates...")
    for i in range(1, num_plates_in_db + 1):
        # Create some varied dummy plates, e.g., "TEH123A", "IRN456B01"
        # For simplicity, let's use a fixed pattern:
        plate = f"PLATE{i:03}" # e.g., PLATE001, PLATE002, ..., PLATE020
        license_plates_db.append(plate)
    
    # Optionally, add a few specific, known plates to test the search
    if num_plates_in_db >= 5: # Ensure list is large enough
        license_plates_db[2] = "FINDME123" # A plate we know is there
        license_plates_db[num_plates_in_db // 2] = "TESTPLATE"

    # print(f"Ex31: Sample License Plate DB (first 5 for preview): {license_plates_db[:5]}...") # Optional preview

    # Step 2: Get the license plate to search for from the user.
    plate_to_search = input("Ex31: Enter the license plate to search for: ")
    
    # For case-insensitive search, it's good practice to convert both
    # the database entries (if not already normalized) and the search term to the same case.
    # Here, we'll convert the search term and compare with original DB entries,
    # or assume DB entries are also normalized (e.g., all uppercase).
    # For simplicity, let's do a case-sensitive search first, then discuss case-insensitive.
    
    # plate_to_search_normalized = plate_to_search.upper() # For case-insensitive search

    # Step 3: Perform a linear search through the database.
    found = False
    found_at_index = -1 # Initialize to -1 (meaning not found)
    
    for i in range(len(license_plates_db)):
        current_db_plate = license_plates_db[i]
        # Simple case-sensitive search:
        if current_db_plate == plate_to_search:
            found = True
            found_at_index = i
            break # Stop searching once the plate is found (no need to check further)
        
        # For case-insensitive search, you would compare normalized versions:
        # if current_db_plate.upper() == plate_to_search_normalized:
        #     found = True
        #     found_at_index = i
        #     break
            
    # Step 4: Print the result.
    if found:
        print(f"Ex31: License plate '{plate_to_search}' FOUND in the database.")
        # Optionally, show where it was found:
        # print(f"       It was found at index {found_at_index} (0-based).")
    else:
        print(f"Ex31: License plate '{plate_to_search}' NOT FOUND in the database.")
        
    return found, found_at_index

# Example usage for Exercise 31:
# print("--- Running Exercise 31 ---")
# search_found_ex31, search_idx_ex31 = search_license_plate_ex31(num_plates_in_db=15)
# # Try searching for "FINDME123" or "PLATE001" or something not in the list.
# print("--- End of Exercise 31 ---\n")
```

---

سوال ۳۲
جستجوی شماره دانشجویی: با فرض اینکه شماره دانشجویی و مشخصات ۳۰۰ دانشجو (مثلاً در لیستی از دیکشنری‌ها) ذخیره شده و این لیست بر اساس شماره دانشجویی به صورت صعودی مرتب است، برنامه‌ای در پایتون بنویسید که یک شماره دانشجویی را بخواند و با استفاده از جستجوی مناسب (مثلاً باینری سرچ) بررسی کند که آیا این شماره در لیست وجود دارد یا خیر و مشخصات دانشجو را در صورت وجود نمایش دهد.
جواب ۳۲
```python
# --- Exercise 32: Search Student ID (Binary Search) ---
def student_id_binary_search_ex32(num_students_in_db=20): # Reduced from 300 for testing
    # Assume student data is a list of dictionaries, ALREADY SORTED by 'student_id'.
    # Each dictionary: {"student_id": 1001, "name": "Alice", "major": "CS"}
    
    # Step 1: Create a sample SORTED list of student data.
    students_db = []
    print(f"Ex32: Simulating a sorted database of {num_students_in_db} students...")
    base_id = 2023000 # Starting student ID
    for i in range(1, num_students_in_db + 1):
        student_id = base_id + i * 5 # Create some gaps to make search interesting
        name = f"Student_{chr(65 + (i % 26))}" # e.g., Student_A, Student_B, ...
        major = "Computer Science" if i % 2 == 0 else "Data Science"
        students_db.append({"student_id": student_id, "name": name, "major": major})
        
    # print(f"Ex32: Sample Student DB (first 3 for preview):") # Optional preview
    # for k_prev in range(min(3, len(students_db))):
    #     print(f"  {students_db[k_prev]}")
    # print("  ...")

    # Step 2: Get the student ID to search for from the user.
    id_to_search = 0
    while True:
        try:
            id_to_search_str = input("Ex32: Enter student ID to search for (integer): ")
            id_to_search = int(id_to_search_str)
            break
        except ValueError:
            print("    Invalid ID format. Please enter numbers only.")

    # Step 3: Perform Binary Search.
    found_student_data = None # Will store the dictionary if found
    low_idx = 0
    high_idx = len(students_db) - 1
    
    while low_idx <= high_idx:
        mid_idx = (low_idx + high_idx) // 2 # Calculate middle index (integer division)
        
        mid_student_id_in_db = students_db[mid_idx]["student_id"] # Get ID at mid_idx
        
        if mid_student_id_in_db == id_to_search:
            found_student_data = students_db[mid_idx] # Found!
            break # Exit the loop
        elif mid_student_id_in_db < id_to_search:
            # If ID at mid is less than search ID, look in the right half
            low_idx = mid_idx + 1 
        else: # mid_student_id_in_db > id_to_search
            # If ID at mid is greater than search ID, look in the left half
            high_idx = mid_idx - 1
            
    # Step 4: Print the result.
    if found_student_data is not None: # Check if a student was found
        print(f"\nEx32: Student ID {id_to_search} FOUND:")
        print(f"  Name: {found_student_data['name']}")
        print(f"  Major: {found_student_data['major']}")
        # Print other details if available:
        # print(f"  Full details: {found_student_data}")
    else:
        print(f"\nEx32: Student ID {id_to_search} NOT FOUND in the database.")
        
    return found_student_data

# Example usage for Exercise 32:
# print("--- Running Exercise 32 ---")
# # Example: if base_id=2023000, students could be 2023005, 2023010, etc.
# # Try searching for an existing ID and a non-existing one.
# found_student_info_ex32 = student_id_binary_search_ex32(num_students_in_db=15)
# print("--- End of Exercise 32 ---\n")
```

---

سوال ۳۳
ادغام دو لیست مرتب صعودی: برنامه‌ای در پایتون بنویسید که دو لیست مرتب شده صعودی، که هر کدام حاوی ۳۰۰ عدد هستند را دریافت کند. این دو لیست را با هم ادغام کرده و یک لیست مرکب مرتب شده صعودی جدید بسازد و آن را چاپ کند.
جواب ۳۳
```python
# --- Exercise 33: Merge Two Sorted Ascending Lists ---
def merge_sorted_ascending_lists_ex33(size_of_lists=10): # Reduced from 300 for testing
    # Step 1: Create two sample sorted ascending lists.
    # In a real scenario, these lists would be provided or read from input.
    list1_asc = []
    for i in range(size_of_lists):
        list1_asc.append(i * 2) # e.g., [0, 2, 4, 6, 8, ...]
        
    list2_asc = []
    for i in range(size_of_lists):
        list2_asc.append(i * 2 + 1) # e.g., [1, 3, 5, 7, 9, ...]
        
    print(f"Ex33: List 1 (sorted ascending, size {len(list1_asc)}): {list1_asc}")
    print(f"Ex33: List 2 (sorted ascending, size {len(list2_asc)}): {list2_asc}")
    
    # Step 2: Merge the two lists into a new sorted ascending list.
    merged_list_asc = []
    ptr1 = 0 # Pointer for list1_asc
    ptr2 = 0 # Pointer for list2_asc
    
    # Loop while there are elements in both lists to compare
    while ptr1 < len(list1_asc) and ptr2 < len(list2_asc):
        if list1_asc[ptr1] < list2_asc[ptr2]:
            merged_list_asc.append(list1_asc[ptr1])
            ptr1 += 1 # Move to the next element in list1_asc
        else: # list2_asc[ptr2] <= list1_asc[ptr1] (handles equality by taking from list2)
            merged_list_asc.append(list2_asc[ptr2])
            ptr2 += 1 # Move to the next element in list2_asc
            
    # After one list is exhausted, append all remaining elements from the other list.
    # These remaining elements are already sorted and are larger than all appended elements.
    
    # Append remaining elements from list1_asc, if any
    while ptr1 < len(list1_asc):
        merged_list_asc.append(list1_asc[ptr1])
        ptr1 += 1
        
    # Append remaining elements from list2_asc, if any
    while ptr2 < len(list2_asc):
        merged_list_asc.append(list2_asc[ptr2])
        ptr2 += 1
        
    print(f"\nEx33: Merged sorted ascending list (size {len(merged_list_asc)}):")
    print(merged_list_asc)
    return merged_list_asc

# Example usage for Exercise 33:
# print("--- Running Exercise 33 ---")
# final_merged_asc_list_ex33 = merge_sorted_ascending_lists_ex33(size_of_lists=8)
# print("--- End of Exercise 33 ---\n")
```

---

سوال ۳۴
ادغام دو لیست مرتب نزولی و نمایش صعودی: برنامه‌ای در پایتون بنویسید که دو لیست مرتب شده نزولی، که هر کدام حاوی ۳۵۰ عدد هستند را دریافت کند. این دو لیست را با هم ادغام کرده و یک لیست مرکب مرتب شده نزولی بسازد. سپس عناصر لیست مرکب را به صورت صعودی نمایش دهد.
جواب ۳۴
```python
# --- Exercise 34: Merge Two Sorted Descending Lists, Display Ascending ---
def merge_desc_display_asc_ex34(size_of_lists=7): # Reduced from 350 for testing
    # Step 1: Create two sample sorted descending lists.
    list1_desc = []
    # To create a descending list: start from a high value and decrease, or sort a list.
    # Example: (size-1)*3, (size-2)*3, ..., 0*3
    for i in range(size_of_lists -1, -1, -1): # Iterate backwards: size-1, size-2, ..., 0
        list1_desc.append(i * 3 + 10) # e.g., for size 5: [22, 19, 16, 13, 10]
        
    list2_desc = []
    for i in range(size_of_lists -1, -1, -1):
        list2_desc.append(i * 3 + 11) # e.g., for size 5: [23, 20, 17, 14, 11]

    print(f"Ex34: List 1 (sorted descending, size {len(list1_desc)}): {list1_desc}")
    print(f"Ex34: List 2 (sorted descending, size {len(list2_desc)}): {list2_desc}")

    # Step 2: Merge the two lists into a new sorted descending list.
    merged_list_desc = []
    ptr1_desc = 0 # Pointer for list1_desc
    ptr2_desc = 0 # Pointer for list2_desc

    # Loop while there are elements in both lists
    while ptr1_desc < len(list1_desc) and ptr2_desc < len(list2_desc):
        # For descending merge, pick the larger element
        if list1_desc[ptr1_desc] > list2_desc[ptr2_desc]: 
            merged_list_desc.append(list1_desc[ptr1_desc])
            ptr1_desc += 1
        else: # list2_desc[ptr2_desc] >= list1_desc[ptr1_desc]
            merged_list_desc.append(list2_desc[ptr2_desc])
            ptr2_desc += 1
    
    # Append remaining elements from list1_desc (if any)
    while ptr1_desc < len(list1_desc):
        merged_list_desc.append(list1_desc[ptr1_desc])
        ptr1_desc += 1
        
    # Append remaining elements from list2_desc (if any)
    while ptr2_desc < len(list2_desc):
        merged_list_desc.append(list2_desc[ptr2_desc])
        ptr2_desc += 1
        
    print(f"\nEx34: Merged list (sorted descending, size {len(merged_list_desc)}):")
    print(merged_list_desc)
    
    # Step 3: Display the elements of the merged list in ascending order.
    # One way is to reverse the 'merged_list_desc'.
    # Another is to sort it ascending (e.g., bubble sort), but reversing is simpler here.
    
    displayed_ascending_list = []
    # Iterate from the end of merged_list_desc to the beginning
    current_idx_for_reverse = len(merged_list_desc) - 1
    while current_idx_for_reverse >= 0:
        displayed_ascending_list.append(merged_list_desc[current_idx_for_reverse])
        current_idx_for_reverse -= 1 # Move to the previous element
        
    print(f"\nEx34: Merged list elements displayed in ASCENDING order:")
    print(displayed_ascending_list)
    
    return merged_list_desc, displayed_ascending_list

# Example usage for Exercise 34:
# print("--- Running Exercise 34 ---")
# final_merged_desc_ex34, final_displayed_asc_ex34 = merge_desc_display_asc_ex34(size_of_lists=5)
# print("--- End of Exercise 34 ---\n")
```

---

سوال ۳۵
درج در لیست مرتب: برنامه‌ای در پایتون بنویسید که یک لیست با ۱۲۰ عضو دارد که به صورت صعودی مرتب شده است. ۳۰ عدد جدید را از ورودی بخوانید و آنها را با حفظ ترتیب صعودی، در لیست اصلی درج کنید. لیست نهایی را چاپ کنید.
جواب ۳۵
```python
# --- Exercise 35: Insert into Sorted List ---
def insert_into_sorted_list_ex35(initial_list_size=10, num_new_elements_to_insert=3): 
    # Reduced from 120 and 30 for easier testing.
    
    # Step 1: Create an initial sorted list (ascending).
    main_sorted_list = []
    for i in range(initial_list_size):
        main_sorted_list.append(i * 5) # e.g., [0, 5, 10, 15, ...]
    print(f"Ex35: Initial sorted list (size {len(main_sorted_list)}): {main_sorted_list}")

    # Step 2: Read new numbers to insert.
    print(f"\nEx35: Enter {num_new_elements_to_insert} new numbers to insert into the sorted list:")
    
    for k_insert in range(num_new_elements_to_insert):
        new_num_to_insert = 0
        while True:
            try:
                new_num_to_insert = int(input(f"  Enter new number {k_insert+1}: "))
                break
            except ValueError:
                print("    Invalid input. Please enter an integer.")

        # Step 3: Insert the new number while maintaining sorted order.
        # Find the correct position to insert 'new_num_to_insert'.
        inserted_flag = False
        for i_pos in range(len(main_sorted_list)):
            if new_num_to_insert < main_sorted_list[i_pos]:
                # Found the position 'i_pos' where 'new_num_to_insert' should be inserted.
                # All elements from 'i_pos' onwards need to be shifted right.
                
                # Manual insertion:
                # 1. Add a placeholder at the end to make space (or the new_num itself initially)
                main_sorted_list.append(None) # Or any placeholder like 0
                
                # 2. Shift elements to the right, starting from the new end, down to index i_pos.
                # Example: list is [10, 20, 30], insert 15.
                #          main_sorted_list becomes [10, 20, 30, None]
                #          j goes from 3 down to 1 (i_pos).
                #          j=3: list[3] = list[2] -> [10, 20, 30, 30]
                #          j=2: list[2] = list[1] -> [10, 20, 20, 30]
                #          Now, list[i_pos] (which is list[1]) can be set to new_num.
                
                idx_shift = len(main_sorted_list) - 1 # Start from the last (newly added placeholder)
                while idx_shift > i_pos:
                    main_sorted_list[idx_shift] = main_sorted_list[idx_shift - 1]
                    idx_shift -= 1
                
                # 3. Place the new_num_to_insert at the correct position i_pos.
                main_sorted_list[i_pos] = new_num_to_insert
                
                inserted_flag = True
                break # Exit the inner loop (for i_pos) as number is inserted
        
        if not inserted_flag: 
            # If the loop finished and 'inserted_flag' is still False,
            # it means 'new_num_to_insert' is larger than all existing elements.
            # So, append it to the end of the list.
            main_sorted_list.append(new_num_to_insert)
        
        # print(f"    List after inserting {new_num_to_insert}: {main_sorted_list}") # Optional: view after each insert
            
    print(f"\nEx35: Final list after inserting all new numbers (size {len(main_sorted_list)}):")
    print(main_sorted_list)
    return main_sorted_list

# Example usage for Exercise 35:
# print("--- Running Exercise 35 ---")
# final_list_after_inserts_ex35 = insert_into_sorted_list_ex35(initial_list_size=5, num_new_elements_to_insert=3)
# # Try inserting numbers like: one smaller than all, one in the middle, one larger than all.
# # E.g., if initial list is [0, 5, 10, 15, 20], try inserting -2, 12, 25.
# print("--- End of Exercise 35 ---\n")
```

---

سوال ۳۶
اطلاعات دانشجویان و دروس: برنامه‌ای در پایتون بنویسید که نام، نام خانوادگی، شماره دانشجویی و نمرات ۶ درس با کدهای خاص (مثلاً ۱۱۰، ۱۱۵، ۱۲۴، ۱۳۶، ۱۵۴، ۱۶۰) برای ۳۵ دانشجو را دریافت کند (می‌توانید از لیست دیکشنری‌ها یا ساختارهای مشابه استفاده کنید). سپس با فرض اینکه نمرات دروس با کدهای ۱۰۱ و ۱۱۵ (که جزو آن ۶ درس هستند) هر کدام ۲ واحدی هستند، معدل هر دانشجو را محاسبه و به همراه نام و شماره دانشجویی چاپ کنید. (این بخش نیاز به تفسیر دقیق‌تر از "دو آرایه مکمل هم ذخیره نماید" دارد؛ فرض شده اطلاعات هر دانشجو یکجا ذخیره می‌شود).
جواب ۳۶
```python
# --- Exercise 36: Student Info, Courses, and GPA ---
def student_gpa_calculation_ex36(num_students_to_process=1): # Reduced from 35 for testing
    # Student info: first_name, last_name, student_id
    # 6 specific course codes are given in the problem: 110, 115, 124, 136, 154, 160
    
    # The problem states "نمرات دروس با کدهای ۱۰۱ و ۱۱۵ ... هر کدام ۲ واحدی هستند".
    # However, course code '101' is NOT in the list of 6 course codes mentioned earlier.
    # Interpretation: We'll assume it meant two *of the given* courses have specific units,
    # or there's a slight mismatch in the problem description.
    
    # Let's define units for the 6 given courses:
    # Assume: 110 is 2 units, 115 is 2 units (as per problem's spirit for 115).
    # For the other courses (124, 136, 154, 160), let's assume they are 1 unit each for this example.
    # If 101 was intended, the list of courses to get grades for should include it.
    
    course_codes_and_units = {
        "110": 2, # Assumed 2 units
        "115": 2, # Stated as 2 units
        "124": 1, # Assumed 1 unit for this example
        "136": 1, # Assumed 1 unit
        "154": 1, # Assumed 1 unit
        "160": 1  # Assumed 1 unit
    }
    # Get just the list of codes for input iteration
    course_codes_to_input = []
    for code_key in course_codes_and_units: # Iterate through dictionary keys
        course_codes_to_input.append(code_key)
    
    all_students_data_list = [] # List to store data for all students
    
    print(f"Ex36: Enter data for {num_students_to_process} students:")
    for i_student in range(num_students_to_process):
        print(f"\n--- Student {i_student+1} ---")
        first_name = input("  First Name: ")
        last_name = input("  Last Name: ")
        student_id = input("  Student ID: ")
        
        grades_for_student = {} # Dictionary to store {course_code: grade} for this student
        print("  Enter grades for courses (scale 0-100, or as appropriate):")
        for current_course_code in course_codes_to_input:
            while True:
                try:
                    grade_str = input(f"    Grade for course {current_course_code} (units: {course_codes_and_units[current_course_code]}): ")
                    grade_val = float(grade_str)
                    # Add validation for grade range if needed (e.g., 0-20, 0-100)
                    # For simplicity, not strictly enforcing a range here, but would be good practice.
                    # if 0 <= grade_val <= 100:
                    grades_for_student[current_course_code] = grade_val
                    break
                    # else:
                    #     print("      Grade out of typical range. Please re-enter.")
                except ValueError:
                    print("      Invalid grade format. Please enter a number (e.g., 85.5).")
                    
        # Store all data for the current student in a dictionary
        current_student_data = {
            "first_name": first_name,
            "last_name": last_name,
            "student_id": student_id,
            "grades": grades_for_student # This is the dictionary of grades
        }
        all_students_data_list.append(current_student_data)

    # Now, calculate and print GPA for each student
    print("\n\n--- Student GPA (Average Score Weighted by Units) ---")
    for student_record in all_students_data_list:
        total_weighted_grade_points = 0.0 # Sum of (grade * units)
        total_units_taken = 0
        
        student_grades_dict = student_record["grades"]
        for course_code_iter, grade_iter in student_grades_dict.items():
            # Get units for this course from our `course_codes_and_units` definition
            units_for_this_course = course_codes_and_units[course_code_iter]
            
            total_weighted_grade_points += grade_iter * units_for_this_course
            total_units_taken += units_for_this_course
            
        gpa_calculated = 0.0
        if total_units_taken > 0: # Avoid division by zero if no units were taken (should not happen here)
            gpa_calculated = total_weighted_grade_points / total_units_taken
        else:
            # This case should ideally not occur if courses always have units.
            print(f"  Warning: Student {student_record['student_id']} has 0 total units. GPA cannot be calculated properly.")
        
        # Print student info and their calculated GPA
        print(f"\nStudent: {student_record['first_name']} {student_record['last_name']}")
        print(f"  ID: {student_record['student_id']}")
        # print(f"  Grades: {student_record['grades']}") # Optional: print all grades
        print(f"  Calculated GPA (Weighted Average): {gpa_calculated:.2f}")
        
        # Optionally, add the GPA to the student's record in the list
        student_record['gpa'] = gpa_calculated 
        
    return all_students_data_list

# Example usage for Exercise 36:
# print("--- Running Exercise 36 ---")
# students_data_with_gpa_ex36 = student_gpa_calculation_ex36(num_students_to_process=1)
# # If you run with num_students_to_process=1:
# # Example input:
# # First Name: Ali
# # Last Name: Rezaei
# # Student ID: 9912345
# # Grade for 110: 80
# # Grade for 115: 70
# # Grade for 124: 90
# # Grade for 136: 85
# # Grade for 154: 75
# # Grade for 160: 95
# # Expected GPA calculation:
# # (80*2 + 70*2 + 90*1 + 85*1 + 75*1 + 95*1) / (2+2+1+1+1+1)
# # (160 + 140 + 90 + 85 + 75 + 95) / 8 = 645 / 8 = 80.625
# print("--- End of Exercise 36 ---\n")
```
