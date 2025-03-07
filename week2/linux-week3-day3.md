## Operators, Arrays, and GREP Commands Along with Calculator Project

### Operators in Shell Scripting
Shell scripting supports different types of operators:

#### 1. Arithmetic Operators
Used for numeric calculations.

#### 2. Relational Operators
Used for numerical comparisons.

| Operator | Meaning |
|----------|---------|
| -eq      | Equal to |
| -ne      | Not equal to |
| -gt      | Greater than |
| -lt      | Less than |
| -ge      | Greater than or equal to |
| -le      | Less than or equal to |

#### 3. String Operators
Used for string comparisons.

| Operator | Meaning |
|----------|---------|
| =        | Equal to |
| !=       | Not equal to |
| -z       | String is empty |
| -n       | String is not empty |

#### 4. Logical Operators
Used for logical operations.

| Operator | Meaning |
|----------|---------|
| &&       | Logical AND |
| !        | Logical NOT |

![image](https://github.com/user-attachments/assets/63de2b7b-93f6-4f2e-a2e3-12932356785d)

![image](https://github.com/user-attachments/assets/2fc66675-0ef3-43a9-8860-843affecbaf8)


### Conditional Statements in Shell Scripting
Conditional statements allow decision-making in scripts.

1. if Statement
2. if-else Statement
3. if-elif-else Statement
4. Case Statement

---
![image](https://github.com/user-attachments/assets/5e631dee-6223-4fea-821d-5531188c731f)

![image](https://github.com/user-attachments/assets/6b6ad50e-1c1a-47f7-ae53-29fed2e18862)

## Building a Calculator with Shell Scripting

![image](https://github.com/user-attachments/assets/608bcd6e-b27a-46a6-bd3a-320433131afd)

```bash
while true; do
    echo "====================="
    echo "    Shell Calculator    "
    echo "====================="
    echo "1. Addition (+)"
    echo "2. Subtraction (-)"
    echo "3. Multiplication (*)"
    echo "4. Division (/)"
    echo "5. Modulus (%)"
    echo "6. Exponentiation (^)"
    echo "7. Exit"
    echo "====================="
    
    read -p "Enter your choice (1-7): " choice

    if [ "$choice" -eq 7 ]; then
        echo "Exiting the calculator. Goodbye!"
        exit 0
    fi

    read -p "Enter first number: " num1
    read -p "Enter second number: " num2

    case $choice in
        1) result=$(echo "$num1 + $num2" | bc) ;;
        2) result=$(echo "$num1 - $num2" | bc) ;;
        3) result=$(echo "$num1 * $num2" | bc) ;;
        4) 
            if [ "$num2" -eq 0 ]; then
                echo "Error: Division by zero is not allowed."
                continue
            fi
            result=$(echo "scale=2; $num1 / $num2" | bc) ;;
        5) result=$(echo "$num1 % $num2" | bc) ;;
        6) result=$(echo "$num1 ^ $num2" | bc) ;;
        *) echo "Invalid choice, please select again." 
           continue ;;
    esac

    echo "Result: $result"
    echo "====================="
done
```
![image](https://github.com/user-attachments/assets/0b114e67-a4d7-404a-a75d-104341ea1133)

![image](https://github.com/user-attachments/assets/16484edd-4621-47f8-84bb-8911abda4ef4)

---

## GREP Commands

1. Search for lines ending with "selection"
```bash
grep "selection$" case.sh
```

2. Find files containing "selection" (case-insensitive, recursive)
```bash
grep -Ril "selection" case.sh
```

3. Match "selection" with any character in place of "e"
```bash
grep "s.lection$" case.sh
```

4. Search for any line containing a number (0-9)
```bash
grep "[0-9]" case.sh
```

5. Search for any line containing a letter (A-Z or a-z)
```bash
grep "[a-zA-Z]" case.sh
```

6. Search for any line containing a vowel
```bash
grep "[aeiou]" case.sh
```

7. Match words where "s" is followed by "n" (zero or more times)
```bash
grep "s*n" case.sh
```

8. Match words where "se" is followed by "n" (zero or more "e")
```bash
grep "se*n" case.sh
```

9. Match "selecti*n" where "i" is optional
```bash
grep "selecti*n" case.sh
```

10. Match exact word "selection"
```bash
grep "selection" case.sh
```

11. Match "sel" followed by any character and "n"
```bash
grep "sel.n" case.sh
```

12. Match "selicti.n" (any character before "n")
```bash
grep "selicti.n" case.sh
```

13. Match "selecti.n" (any character before "n")
```bash
grep "selecti.n" case.sh
```

14. Match "s*n" (zero or more "s" before "n")
```bash
grep "s*n" case.sh
```

15. Match "s*on" (zero or more "s" before "on")
```bash
grep "s*on" case.sh
```

![image](https://github.com/user-attachments/assets/1b10e910-83f8-4b10-8333-56f6e1a62d24)

![image](https://github.com/user-attachments/assets/86e12929-f3e0-4782-b369-f45ce2084afa)

![image](https://github.com/user-attachments/assets/76a7cfe1-78b1-410d-b318-21ad88cffc8b)

![image](https://github.com/user-attachments/assets/cad57080-cc1a-4280-9316-8397fefc2e8d)

---

## Arrays in Shell Scripting

### 1. Declaring an Array
```bash
my_array=(10 20 30 40 50)
```

### 2. Accessing Elements
```bash
echo ${my_array[0]}   # Output: 10
echo ${my_array[2]}   # Output: 30
```

### 3. Printing All Elements
```bash
echo ${my_array[@]}   # Output: 10 20 30 40 50
echo ${my_array[*]}   # Output: 10 20 30 40 50
```

### 4. Finding Array Length
```bash
echo ${#my_array[@]}  # Output: 5
```

### 5. Adding Elements
```bash
my_array+=(60 70)
echo ${my_array[@]}   # Output: 10 20 30 40 50 60 70
```

### 6. Updating an Element
```bash
my_array[1]=99
echo ${my_array[@]}   # Output: 10 99 30 40 50 60 70
```
![image](https://github.com/user-attachments/assets/38ae71ae-a0be-49ea-92ec-f0002a6e94aa)

### 7. Removing an Element
```bash
unset my_array[2]  
echo ${my_array[@]}   # Output: 10 99 40 50 60 70
```
![image](https://github.com/user-attachments/assets/88358159-3212-4cdf-a1c4-f27e1d38b526)

### 8. Looping Through an Array
```bash
for val in "${my_array[@]}"; do
    echo "$val"
done
```
---

## Conclusion
Shell scripting provides powerful tools for automation, including operators, arrays, and grep commands. The calculator project showcases how scripting can handle computations efficiently. Understanding these concepts enhances productivity and enables effective scripting solutions.
