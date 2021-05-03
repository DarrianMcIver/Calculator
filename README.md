# Calculator
#include <stdio.h> 
#include <string.h> 

struct Calculator {
	float num1;
	float num2;

};

union Data
{
	int i;
	float f;
	char str[];
};


float compute(struct Calculator* c, char operator) {
	//This line of code will execute the operator (+,-,*,/)
	float result;

	switch (operator)
	{
		//if user enters +
	case'+':
		result = c->num1 + c->num2;
		break;
		// if user enters -
	case'-':
		result = c->num1 - c->num2;
		break;
		//if user enters *
	case'*':
		result = c->num1 * c->num2;
		break;
		// if user enters /
	case'/':
		result = c->num1 / c->num2;
		break;
		// if the user does not enter +,-,*,/ then the following error will occur below
	default:
		printf("\n Invalid Operator");
	}
	return result;

}


int main()
{
	struct Calculator myCalc = { 5, 10 };
	char operator='*';
	float result = 0;
	union Data data;
	printf("memory size : %d\n", sizeof(data));
	printf("1");
	//Gives the user the option to what operation they would like to use

	
	printf("\n Enter a operator (+, -, *, /): ");
	scanf_s("%c", &operator, 1);
	  
	//Open file
	errno_t err;
	FILE *calculation;
	calculation = fopen_s("calc.txt", "rw");
	//fopen_s(&calculation, "calc.txt", "rw");

	printf("2");

	//This enter the value of number 1 and number 2 for the user to input. 

	printf("3");
	
	printf("\n Enter two numbers for calculations: ");
	scanf_s ("%f", &(myCalc.num1), sizeof(float));
	scanf_s ("%f", &(myCalc.num2), sizeof(float)); 

	fgets(operator,1,calculation);
	fgets(&myCalc.num1,1, calculation);
	fgets(&myCalc.num2,1, calculation); 
	result = compute(&myCalc, operator);
	printf("%s",result);
	fprintf(calculation,"answer is: %f",result);

	printf("The Result of %.2f %c %.2f = %.2f", myCalc.num1, operator, myCalc.num2, result);
	//Close the file
	int retval = 0;
	retval = fclose(calculation);
	if (retval == 0) {
		printf("File closed unseccessfully");
	}


	return 0;

}
