
## DESCRIPCION
- How well can you perfom basic binary operations?

Start searching for the flag here `nc titan.picoctf.net 53894`

## SOLUCION
```

pabloval-academy@webshell:~$ nc titan.picoctf.net 53894

Welcome to the Binary Challenge!"
Your task is to perform the unique operations in the given order and find the final result in hexadecimal that yields the flag.

Binary Number 1: 00110110
Binary Number 2: 11000000


Question 1/6:
Operation 1: '<<'
Perform a left shift of Binary Number 1 by 1 bits.
Enter the binary result: 01101100
Correct!

Question 2/6:
Operation 2: '&'
Perform the operation on Binary Number 1&2.
Enter the binary result: 0
Correct!

Question 3/6:
Operation 3: '>>'
Perform a right shift of Binary Number 2 by 1 bits .
Enter the binary result: 01100000
Correct!

Question 4/6:
Operation 4: '+'
Perform the operation on Binary Number 1&2.
Enter the binary result: 011110110
Correct!

Question 5/6:
Operation 5: '|'
Perform the operation on Binary Number 1&2.
Enter the binary result: 11110110
Correct!

Question 6/6:
Operation 6: '*'
Perform the operation on Binary Number 1&2.
Enter the binary result: 10100010       
Incorrect. Try again
Enter the binary result: 10100010000000
Correct!

Enter the results of the last operation in hexadecimal: 2880

Correct answer!
The flag is: 

picoCTF{b1tw^3se_0p3eR@tI0n_su33essFuL_d6f8047e}

```

## NOTAS ADICIONALES
- Se usa el comando "nc" para poder conectarnos al servidor

## REFERENCIAS
https://miniwebtool.com/es/calculadora-binario/?number1=00110110&operate=or&number2=11000000
