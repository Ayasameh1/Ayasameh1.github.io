# const and the "&" usage in c++ 

## first, const keyword usage

const keyword is used to make an element const in the program; 
- 1: const variables; if we set a variable to be const, we aren't allowed to change its value later, we also have to initialize it while declaration.

ex :

```
 const char c= "z"; //cannot be changed later 
c = "r"; ERROR!!!

```


- 2: const pointers; 1st; the pointer is pointing to a const variable, used to make array elements or a string immutable or in another meaning cannot be changed; this type can be writtin as:

```

const int* i; 

```

//or 

```
int const* i;

```

; both give the same meaning/ same result.
2nd; const pointer, we can make a pointer const by adding the word "const" to the right of "*" as the following; 

```

int x=0;
int* const ptr= &x; 

```

when the pointer is constant that means we can't change it later to point to other value than, it's set to 
point to x only, if we tried (ptr =&o ) for ex later, that would give us an error, note that we can change the 
value of x and the val the pointer has would change, but we cannot replace x itself with another variable. 
as: if we redefined x to be x=20;
so ptr now points to a value of 20 not 0; but it still the val of x not another var.
note that:we also can have a const pointer points to a const var as const int* const x;.



- 3rd; function arguments and return types as following 

```

const int z() { return 1;}

```

some notes: -in user defined data types, returning const will prevent any modification in it, -temp obj that 
creadted during execution are always of type const, -we cannot pass const argument in a finstion of nin const 
parameter while making a call, -a function of const parameter can be passed const or non const argument -->  

```

void g (const int*){ }.

```

- 4th; const class data members--> in this case the vriables are not initialized during declaration but it's 
done in the constructor. 

```

class meo(){
    const int i; 
    .....
}

```

- 5th; defining class obj as const--> data members of the object can never be changed

```

const class_name object 

```

- 6th; defining class's member function as const--> const member functions never modifies data members in an 
object

```

return_type function_name() const; 

```

+THIS IS ALL WE HAVE FOR THE CONST KEYWORD, NOW LET'S DISCUSS THE & OPERATOR+
##  "&" usage
- as a conditional exp;
&& operator is a logical operator, it gives true only if all operands are true ,else, its result is false -->  
the logical AND represented as ‘&&’ operator in C or C++ returns true when both the conditions under 
consideration are satisfied. Otherwise, it returns false. Therefore, a && b returns true when both a and b are 
true
- ampersand symbol & is used in C++ as a reference declarator in addition to being the address operator

```

int target;
int &rTarg = target;  // rTarg is a reference to an integer.
 // The reference is initialized to refer to target.

void f(int*& p);      // p is a reference to a pointer

```


- You can use the & operator with overloaded functions only in an initialization or assignment where the left 
side uniquely determines which version of the overloaded function is used.


- & to declare a reference to a type
if & is at the left of var(in this case it must be used in variable declaration), that means you expect a 
refrence to the declared type.

```

std::string batman ("notmarvel");
std::string& hero = batman;

```

batman and hero have the same value, also points to the same place in the memory

- & to get the address of a variable
if the & is on the right side of var, it's known as the "address-of operator", it can be used in assignments 
too in this case, anyway, if we put it in front of var, it will return the address of this var in the memory,
not the value.

```

std::string batman("notmarvel");
std::string* hero;

hero = &batman; 

```

//next part is copied just as more info about the &&
- && for declaring rvalue ref.
"An lvalue (locator value) represents an object that occupies some identifiable location in memory (i.e. has an address).
rvalues are defined by exclusion, by saying that every expression is either an lvalue or an rvalue. Therefore, from the above definition of lvalue, an rvalue is an expression that does not represent an object occupying some identifiable location in memory." 
both declaring rvalue and universal ref should have && after type, but,if type deduction takes place, you declare a universal reference, if not an rvalue reference.

- && for declaring a universal ref 

```

Vehicle car;
auto&& car2 = car; // type deduction! this is a universal reference!
Vehicle&& car3 = car; // no type deduction, so it's an rvalue reference
another possibility
template<typename T>
void f(std::vector<T>&& param);     // rvalue reference

template<typename T>
void f(T&& param); // type deduction occurs, so this is a universal reference!

```

- & or && for function overloading
it's used when you'd like to optimize your memory footprint by taking advantage of move semantics. 
ex 

```

class Tool {
public:
  // ...
  void doSomething() &; // used when *this is a lvalue
  void doSomething() &&; // used when *this is a rvalue
};

Tool makeTool(); //a factory function returning an rvalue

Tool t; // t is an lvalue

t.doSomething(); // Tool::doSomething & is called


makeTool().doSomething(); // Tool::doSomething && is called

```




# references :
https://dev.to/sandordargo/how-to-use-ampersands-in-c-3kga
https://www.tutorialcup.com/cprogramming/constant-pointers.htm
https://www.studytonight.com/cpp/const-keyword.php
https://www.opensourceforu.com/2015/01/constant-pointers-and-pointers-to-constant-a-subtle-difference-in-c-programming/
https://www.google.com/url?sa=i&url=https%3A%2F%2Fslideplayer.com%2Fslide%2F9761222%2F&psig=AOvVaw3J62DNt1K5XBCjAbp9ETaH&ust=1639324022480000&source=images&cd=vfe&ved=0CAwQjhxqFwoTCMCZwYWM3PQCFQAAAAAdAAAAABBe
