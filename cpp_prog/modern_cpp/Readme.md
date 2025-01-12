________________________________________________________________________________
Modern CPP(C++11/14)
====================
--> Language improvements
	>> General features
	   -> constexpr
	   -> auto type
	   -> decltype
	   -> range based for loop
	   -> static_assert
	   -> nullptr
	   -> Scoped/strongly typed Enums
	   -> strict initializer with {}
	   -> 'using' keyword for aliasing
	   -> user defined literals
	   -> binary literals
	   -> digit separation
	   -> User defined literal 
	   -> raw string literal
	>> classes & object improvement
	   -> Default controls
	   -> Constructor delegating 
	   -> In class initializer 
	   -> uniform initializer
	   -> Initializer list
	   -> Explicit conversion operator
	   -> Read only objects
	   -> Explicit type conversion
	   -> type traits
	>> inheritance
	   -> final, override keyword
	   -> explicit inheritance of base class members

--> Move semantics
	>> object model & Move semantics
	   -> types (Trivial ,POD ,standard layout)
	   -> move constructor, move operator=
	   -> R-value references, compatibility, casting(std::move)
	   -> Rule of three/five/zero
	   -> Universal references, perfect forwarding(std::forward)

--> Lambda and callable elements
	>> Callable elements
	   -> lambda expression usage
	   -> Capture syntax
	   -> Generic Lamdas
	   -> std::function
	   -> std::bind
	>> Templates
	   -> Right angled parenthesis
	   -> Aliasing Templates
	   -> Extern Templates
	   -> Variadic Templates
 	>> exception handling
	   -> no except keyword
 
--> STL Improvements
 	>> new containers
	   -> std::array ,std::forward_list ,unorder map, sets
	>> new operations
	   -> emplace_back, shrink_to_fit, data
	>> new algorithms
	   -> std::for each, Tuples, Regular expressions

--> Smart pointers
--> Concurrency & IPC
_________________________________________________________________________________

<1> constexpr:
==============
  >> constexpr was introduced in C++11 and improved in C++14. It means
     constant expression
  >> constexpr variables are evaluated at comile time, must be initiailised with
     comile time known values.
  >> constexpr functions are evaluated at compile time, if all arguments are
     compile time known.
  >> The return value can be assigned to constexpr variables.
  >> constexpr improves ROMability of the code
  >> constexpr variables are eligible as - size of global arrays, a better choice
     than const variable, nontype templates parameter
  >> Read only objects can be modeled using constexpr
  >> macros are error-prone and difficult to debug constexpr can be used.
  >> const objects and constexpr objects have internal linkage by default
     To give a const object external linkage(extern const int value = 42;).
  >> A constexpr function or constructor is implicitly inline .
  >> The primary difference between const and constexpr variables is that the
     initialization of a const variable can be deferred until run time. A
     constexpr variable must be initialized at compile time. All constexpr   
     variables are const .
  >> When a constexpr function is called with one or more values that are not
known during compilation, it acts like a normal function, computing its result at
runtime. This means you don’t need two functions to perform the same opera‐
tion, one for compile-time constants and one for all other values. The constexpr
function does it all.


  >> Syntax & examples
  --------------------------------------------------------<< 
constexpr int maxval=100;
constexpr double pi=22.0/7.0;
constexpr double area(int radius)
{  		
  return pi*radius*radius;
}
  --------------------------------------------------------<<
int sz; // non-constexpr variable
…
constexpr auto arraySize1 = sz; // error! sz's value not
 // known at compilation
std::array<int, sz> data1; // error! same problem
constexpr auto arraySize2 = 10; // fine, 10 is a compile-time constant
std::array<int, arraySize2> data2; // fine, arraySize2
 // is constexpr
  --------------------------------------------------------<<
int sz; // as before
…
const auto arraySize = sz; // fine, arraySize is
 // const copy of sz
std::array<int, arraySize> data; // error! arraySize's value
 // not known at compilation
  --------------------------------------------------------<<
1. can constructors and other member functions(getters/setters) be constexpr?
2. Check the symbol state of constexpr variables using nm/objdump command

3. Can you assign a runtime expression to constexpr variables?

4. Can you pass a non constexpr value to a function with constexpr return type? E.g. 

constexpr int square(int val) {
  return val * val;
}
int x=10;
int y=square(x);
5. Can you assign square(x) to constexpr variables, i.e. what if y is declared as constexpr



<2> auto keyword:
=================
  >>
  >>	





