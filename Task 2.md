###SECOND TASK###
----
As we know that when we type the following code, we get the required output.
```
gcc Koutilya.o
```
And to execute it we write the following:
```
./a.out
```

![task 2 2](https://github.com/user-attachments/assets/5d9699a6-fc9f-480e-aee4-a4f938e4331e)



We get the same thing using 'spike'. All we need to do is run the following code:
``
spike pk Koutilya.o

![task 2 3](https://github.com/user-attachments/assets/65698c20-6da0-48f9-b7a8-be8d36c7448b)


Now after we got the verification that the code is working we will now try to debug the dumped assembly. The following code is written to dump the assembly:
```
riscv64-unknown-elf-objdump -d Koutilya.o
```
NOTE: This can be done using any of '-O1' or 'Ofast'

![task 2 4](https://github.com/user-attachments/assets/b1246370-b636-4c9e-a58d-4f3c6a694aa1)



To open the Debugger write the following command:
```
spike -d pk Koutilya.o
```
Now once the debugger is executed, we want the whole assembly to run automatically until '100B0' which is the memory address, after which we shall run it manually. The command to make the pc run own of own till some place is
```
until pc 0 100b0
```
![task 2 5](https://github.com/user-attachments/assets/68498a3e-dd72-45d1-9cc2-f86ad934334c)



To check the register content, we write the following command where 'a2' is the register
```
reg 0 a2
```
After which we get a 64 bit assembly and to run next instruction, we press enter.
![task 2 6](https://github.com/user-attachments/assets/400bc4a2-942b-4a52-924d-aba0a7affb79)
)


Then again to run the next assembly, we write the following code.
```
reg 0 a2
```
Once 'sp' comes, which stands for spike pointer, we now need to perform 'addi', which adds an immediate value to a source register and stores the result in the destination register. In my case, `ADDI SP, SP, -16` subtracts `0x10` (hexadecimal 16) from the stack pointer (`SP`).

![task2 7](https://github.com/user-attachments/assets/88a2eae6-d320-420d-8944-b614f4a2aede)


calculation for sp
IN binary
![Screenshot 2024-12-27 021321](https://github.com/user-attachments/assets/0bd25619-3bf9-45ed-9b1a-89e544071cc3)

----
*EXAMPLE*
-----
```
#include <stdio.h>

// C Program to Convert Kelvin to Fahrenheit
#include <stdio.h>
int main(){
    float kel, F;  
    // Taking input
    printf("Enter the temperature in Kelvin: ");
    scanf("%f", &kel);
    // Kelvin to fahrenheit conversion
    F = ((9.0 / 5) * (kel - 273.15)) + 32;
    // Display output
    printf("%.2f Kelvin = %.2f Fahrenheit", kel, F);
    return 0;
}
```
