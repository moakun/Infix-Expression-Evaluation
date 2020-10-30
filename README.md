# Infix-Expression-Evaluation
This the code that i made for the infix algorithm in c.

#include<stdio.h> 
#include<string.h>
#include <iostream> // for C++.
#include <stack> //standard tamplate library.
using namespace std;
stack <int> OPTR; //using "stack" to define two stack types, one is operator and one is operander.
stack <char> OPND;

int Precede(char x,char y)  // using this function to define precedence. x>y,1;x=y,0;x<y,-1
{   int i,j;  
    char pre[7][7]={           
     
        {'>','>','<','<','<','>','>'},  
        {'>','>','<','<','<','>','>'},  
        {'>','>','>','>','<','>','>'},  
        {'>','>','>','>','<','>','>'},  
        {'<','<','<','<','<','=',' '},  
        {'>','>','>','>',' ','>','>'},  
        {'<','<','<','<','<',' ','='}};  
    switch(x) //this is for the first character.
 {  
        case '+': i=0; break;  // these are 7 tokens that we will input. i is for the line
        case '-': i=1; break;  
        case '*': i=2; break;  
        case '/': i=3; break;  
        case '(': i=4; break;  
        case ')': i=5; break;  
        case '#': i=6; break;  
    }  
    switch(y) // this is for the second character.
 {  
        case '+': j=0; break;  
        case '-': j=1; break;  // j is for the column.
        case '*': j=2; break;  
        case '/': j=3; break;  
        case '(': j=4; break;  
        case ')': j=5; break;  
        case '#': j=6; break;  
    }  
    // different precedence: 
    if (pre[i][j]=='>') return 1; // this one is bigger .
 else if(pre[i][j]=='=')  return 0;// this is equal.
 else return -1;// this one is shorter, less big.
}  
int Operate(int a,char b,int c) // this is for the operator to calculate the value.
{
 if(b=='+') 
 return c+a;// plus "+" operator.
 if(b=='-') return c-a;// minus "-" operator.
 if(b=='*') return c*a;// multiply "*" operator.
 if(b=='/') return c/a;// divide "/" operator.
} 
int Calculate(char S[])// this is the calculate function 
{
int a, c;
char b;
 OPTR.push('#'); // we push the "#" key before the calculation begins
 int i=0,j=0; 
 while(S[i]!='#'||OPTR.top()!='#') // if we don't meet another "#" key the loop doesn't end, that's why we have the while loop.
 {
  if(S[i]>='0'&&S[i]<='9') 
    {
         int number=0;
            while(S[i]>='0'&&S[i]<='9')
            {
                number= number*10+S[i]-'0';
                i++;
                
            }
             OPND.push(number);
   }    
   else
   switch(Precede(OPTR.top(),S[i]))
   {
    case -1:OPTR.push(S[i]);i++;break; //this means that the top operator is less than the input character and it will push the oprator
    case 0:OPTR.pop();i++;break; 
    case 1:a=OPND.top();
      OPND.pop();
      c=OPND.top();OPND.pop();b = OPTR.top();OPTR.pop();OPND.push(Operate(a,b,c));
			break;
			
		}
	}
	return OPND.top();	
	
}
int main(){
	char S[100];
	printf("What do you want to calculate?");
	gets(S);
	printf("%d\n",Calculate(S));
	return 0;
}
















