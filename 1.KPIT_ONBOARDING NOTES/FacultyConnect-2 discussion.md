#kpit 
milestone 1: OOP in Java

milestone 2: Functional programming, concurrency in Java



[application] : a program designed for a specific purpose, used by end-customers and does not require developer knowledge to use

    MS word app


[libraries]: software designed for other developers to use and make new products based on the library


    ---> opencsv libraries: developers can use this library to make CSV reading software
    ---> xml, excel also have their libraries
    ---> selenium --> developers for web based automation


    /////////////////////////////////////////


    project: creating a car servicing automation software

    [some engineer in the workshop can open the library, call a function to set the routine of service and then car gets services based on engineer's program]


    workshop engineer

            designServiceRoutine() {
                checkWheelsOfTheCar();
                checkSteering();
                checkBreak()

            }

            //EVCar<--------------
            designServiceRoutine() {
                checkWheelsOfTheCar();
                checkSteering();
                checkBreak()
                checkBattery();
                checkCharging();

            }




calculator library


//Java version 8 and above has support for "Functional programming"
void performOperation(data,   logic  ){
    //apply logic on data

    logic(data);  //applying means calling "logic" by passing "data" as parameter
}

performOperation(10,     square_of_number); //100
performOperation(10,     cube_of_number); //1000
performOperation(10,     factorial_of_number); //1000



/////////////////////////////////////////////////////////////
void square(int data){
    System.out.println(data * data);
}

void cube(int data){
    System.out.println(data * data * data);
}


//user of function can only pass data

square(10);
cube(20);
factorial(5); //cannot do it because no such option




1) One input---> one output
2) Two inputs----> one inputs
3) No input ----> no output
4) one input ----> no output


void magic(){
    System.out.println("Method called");
}

void displayFactorial(int number) {
        /*
            logic for factorial
        /*
    System.out.println(ans)
}


SESSION

1) New programming style: Functional programming

"FOCUS on using "functions" as "objects" to

        - Filter data
        - apply operation data
        - consume data
        - run a logic as thread 

        etc

2) Java 8 and above have many features for this

        a) Functional interfaces (9 built-in types)
        and @FunctionalInterface to make more

        b) lambda objects
                Function<Integer, Integer> fn = x -> x + 10;

        c) lambda expressions
                    x -> x + 10  //without tagging an object name, this becomes "expression"

        d) functional composition:
                actions on output from previous step / chained functions where each function fn works on output of previous step


                    filter-----> map-------> sum()


                streams API of java has features to write composed functions



    map :  take a logic( written as a lambda object/expression and "apply" on data)

    data : 10

    logic =    x   ->      x  * 100


    [data is input] map(logic) ------>  10 * 100  = 1000




#kpit 