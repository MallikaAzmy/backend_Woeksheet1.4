# backend_Worksheet1.4
# Aim : The aim of this experiment conveys  learning about how to write node.js file using fs(File System) module  and to implement the process of copying data from source file to destination file using stream.

# Step1: 
Let’s create a Node.js file in nodepad to calculate a salary of an employee .
# Backend.js:

const readline = require('readline');
const fs = require('fs');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

function calculateSalary() {
  rl.question('Enter the employee name: ', (name) => {
    rl.question('Enter the number of hours worked: ', (hours) => {
      rl.question('Enter the hourly rate: ', (rate) => {
        const salary = hours * rate;
        rl.question('Enter the address of the employee: ', (address) => {
          const output = `Employee details:
            Name: ${name}
            Salary: $${salary.toFixed(2)}
            Address: ${address}`;

          // Write the output to a file
          fs.writeFile('empdetails.txt', output, (err) => {
            if (err) {
              console.error('Error writing to file:', err);
            } else {
              console.log('Employee details saved to empdetails.txt');
            }
            rl.close();
          });
        });
      });
    });
  });
}

calculateSalary();


Explaination :

# I. Import necessary modules:
   - The code starts by importing two Node.js modules: `readline` and `fs`.
   - `readline` is used to interact with the user via the command line by taking input from the user and displaying output.
   - `fs` (file system) is used to write data to a text file.

# II. Create a readline interface:
   - `rl` is created as a readline interface using `readline.createInterface()`. It takes `process.stdin` as input (to read from the command line) and `process.stdout` as output (to display output to the console).

# III. Define a function named `calculateSalary()`:
   - This function is defined to perform the following tasks:

# IV. Prompt the user for the employee's name,hours workes and hourly rate and address.
   - It uses `rl.question()` to ask the user to enter the employee's name and other details.

# V- Calculate the salary:
   - After collecting the necessary input (name, hours, and rate), the code calculates the employee's salary by multiplying the hours worked by the hourly rate.

# VI. Write the employee details to a file:
    - The `fs.writeFile()` method is used to write the output string to a text file named 'empdetails.txt'. It includes error handling to check if the file write operation encounters any errors.

# VII. Close the readline interface:
    - Finally, the readline interface is closed using `rl.close()` to indicate that the interaction with the user is complete.

# VIII. Call the `calculateSalary()` function:
    - The code concludes by invoking the `calculateSalary()` function, which initiates the entire process of collecting employee information and saving it to a file.



# Step2 :  Open File that stored output of backend.js  file in the command prompt
                                 -----  Notepad empdetails.txt
     Employee details:
            Name: mallika
            Salary: $48.00
            Address: assam


# Step3:Create a New File name copy.txt (keep it empty) 
----Notepad  copy1.txt


# Step4:Create a New  JS File name trans.js .This file will contain the code to transfer data from empdetails.txt to copy1.txt
# trans.js 
const fs = require('fs');

const readableStream = fs.createReadStream('empdetails.txt');
const writableStream = fs.createWriteStream('copy1.txt');

readableStream.pipe(writableStream);

readableStream.on('end', () => {
  console.log('Data transfer complete.');
});

