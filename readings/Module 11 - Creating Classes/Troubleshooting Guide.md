# Troubleshooting Checklist

As programs get more complicated, getting them into a fully-working state also gets more complicated\! Here are some common tips and tricks if you get stuck writing the code.

## Compile Errors:

&emsp;&emsp;&#x27A4; Make sure you're clear on the pseudo-code for the line; compile errors sometimes happen when trying to translate too much of a problem to code at once

&emsp;&emsp;&#x27A4; Check the error message in the 'Problems' tab (remember to save the file to get this to update)

&emsp;&emsp;&#x27A4; Check the syntax template for what you're doing on that line

&emsp;&emsp;&#x27A4; Check for typos in variable names or keywords (ex: For instead of for)

&emsp;&emsp;&#x27A4; Check that variables have been declared in the appropriate scope; a variable can only be used in the set of curly braces ({}'s) where it was declared

&emsp;&emsp;&#x27A4; Check for unexpected paths through the code to find ways that return statements might be missed or variables might not be initialized

## Runtime Errors:

&emsp;&emsp;&#x27A4; When in doubt, set a breakpoint and step through the code

&emsp;&emsp;&#x27A4; If a variable or field has an unexpected value (such as 'null'), check that it was properly initialized; remember that fields are initialized in constructors

&emsp;&emsp;&#x27A4; Check loop logic: see what would happen in the program if the loop ran 0 times, 1 time, or several times
