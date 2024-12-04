java c
CMPINF 0401 -- Intermediate Programming 
Assignment 4 
Topics: Interfaces and implementing new data types
Online: Monday, November   11, 2024
Due: All source (.java) files plus a completed Assignment   Information   Sheet   zipped   into   a   single   .zip file and submitted via   Canvas   by   11:59PM   on
Wednesday, December 4, 2024. 
Late Due Date: 11:59PM on Friday, December 6, 2024
Submission note: Your   .zip file should contain only   .java   files   and your   Assignment   Information   Sheet.   There   should be no project files or project subdirectories in the   .zip file.   Also, your   TA   must be   able   to compile your program from the command line using the   javac command. Test your files to   make   sure   this   will work (especially if   you use an IDE such as NetBeans for   development).   If   the   TA   cannot   compile your program you will receive minimal credit!
Introduction: 
This term in lecture we have looked at building new Java classes using   composition.    In particular,   we have looked at simple array-based data   structures (SimpleAList)   and   simple   linked-based   data   structures   (SimpleLList).    Recently we have also looked at using interfaces to access   objects that   implement those interfaces (see Lectures 21 and 22 and Lab   10).    Furthermore,   earlier   in   the   term   we   did   a   simple   in-class   exercise   in   which   we   implemented   a   simple   decimal   "counter" - representing   the   number   of   times   the "increment()" method was called using an array of   ints to represent the digits.    For   details   on   this   exercise,   see the following   files: 
InClass4   .java- driver   program   to   demonstrate   class
Counter.java- simple   implementation   of   a   counter   (my   solution   - you   may   prefer   yours)
These files are both available on Canvas at Files/InClass/InClass4/.      Before   starting   this   exercise, read over both of   these files carefully, noting all of   the comments.      Be   sure   you understand what the   Counter class is doing and how it is implemented   in   the   simple   solution. 
Details: 
In this exercise you will implement 2 classes:
ArrayCounter in file ArrayCounter.java
LinkedCounter in file LinkedCounter.java
Both of   these classes will implement the interface CountInterface   (in   file   CountInterface.java).      Note the   methods within CountInterface:
public void   increment()
// Add   1 to the counter value, increasing the values of   all affected digits.   This method   may   cause   the
// number   of   digits   to   increase, if   the   new   value   cannot   be   represented   with   the   previous   digits.
public void decrement()
// Remove one from the counter value, decreasing the values   of   all   affected   digits.      This method may
// cause the number of   digits to decrease, if   the leftmost   digit would   change   from   1   to   0   (since   we   will
// not show leading 0s).    If   the value of   the counter   is   0   prior   to   this   call,   this   method   should   output   an
// error and not change the   counter value.
public void   reset()
// Reset the counter back to its initial state (and   value   of   0).   After   this   call   the   counter   should have   only
// a   single   digit.
public   int digits()
// Return the number of   digits being represented by the CountInterface.    This should NOT include   any
// leading   0s.
public   int   radix()
// Return   the   radix   value   for   this   CountInterface.    For   a   given   radix,r, the   digits   in   the   CountInterface   will
// have values from 0 to   (r-1),   inclusive.
public String   toString()
// Return a   String representation of   the counter with the digits shown   correctly.      It   should   contain no
// extra characters – only the   digits   in   order.
Important Note on Implementations: The functionality of the CountInterface can be implemented in many ways. For this assignment you are required to implement it in the two ways specified below. If you do not implement it precisely as specified, even if it gives the correct output, you will receive minimal credit. 
Class ArrayCounter: 
Class ArrayCounter must have the following header:
public class ArrayCounter implements CountInterface 
It should implement the methods in CountInterface as   specified, with the   following requirements:
1)       The   underlying   data   for   your   ArrayCounter   must   bean array of int. You   may   not   use   any   Java collection class for this   data.
2)       The increment() method should always   work   and   the   count   should   always   increase.      In   order   to   allow this, you must resize the underlying array when necessary to twice its previous   size   and         copy the data to the new array.    Resizing is demonstrated   in handout   SimpleAList.java – your         resizing will be similar to that.
3)       The constructor for the   class will allow   the   radix   and   initial   array   size   to be   specified:
public ArrayCounter(int rad, int asize) 
The   rad   value represents the radix, or base value for your counter and   should be <= 10. Note that for a given value of rad, your actual digit values will be from 0 to (rad-1). If additional digits are required, you should automatically resize the   array as   specified   above   in   the   increment()   method – so despite the asize value above your ArrayCounter   should never   “run   out”   of   digits. 
4)       A second constructor for the class will take   an argument of   the   interface   type   (CountInterface)
and produce a copy of   that object as a new ArrayCounter.    Note that the   interface   contains   all   of   the methods necessary to make a copy of   the object – consider the   methods   and   how   they   can   be   used to make a copy.    The header   should be as   follows:
public ArrayCounter(CountInterface orig) 
Note that the orig reference 代 写CMPINF 0401 -- Intermediate Programming Assignment 4Java
代做程序编程语言could be accessing either an ArrayCounter object   or a   LinkedCounter object (see more details below).    This should not matter and the   constructor   should work   regardless   of   the   object   type   of   orig. 
Note that some of   the code for ArrayCounter   is already provided   for you   in   file   Counter.java.    Use   that   class (either my code or yours) as a   starting point   and   enhance   the   class as   stated   above.
Class LinkedCounter: As an alternative to an array-based counter, we could   store   the   digits   in   a   linked-list.      If   you   think   about   how the counter works, the access is always sequential   from beginning to   end   and   so   direct access   of   an   individual   count   is   not   required – this   lends   itself   to   an   effective   linked-list   implementation.
Class LinkedCounter must have the following header:
public class LinkedCounter implements CountInterface 
This class will have the same functionality as ArrayCounter,   since   it   implements the   same   interface.
However, the data is stored in a very   different manner.      Class   LinkedCounter   should   meet   the   following   requirements:
1)       Your linked list should be singly linked, with   a Node   inner   class,   and with   a   structure   similar   to that discussed in   SimpleLList.java from the CMPINF 0401 Handouts.      In LinkedCounter   the   data   within each Node   should be an int, to represent a single   digit.      See   file   SimpleLList.java   for   more   details on the general linked list   structure.
2)       For efficient access in the increment()   and   decrement()   methods, your   linked   list   should   have   the   least significant (i.e. ones) digit   at the   front   of   the   list.
3)       The counter should always have   the   exact number   of   digits   needed   to   store   the   count   value   in   the      current radix.    Whenever a new digit is needed (i.e. during   increment()), a   Node   should be   added      to the end of   the list.    Whenever a leading   0   is   generated   (i.e.   during   decrement()),   a Node   should   be   removed.
4)       In order to get the toString() method to   show the   digits   in   the   correct   order,   you   should   not
"append()" each digit to a   StringBuilder – this will show them in   reverse   since   the   smallest   digit   is in the front of   your list.    Look at the   StringBuilder   class and   see   how   you   can   get   the   digits   in      the correct   order.
5)       The constructor for LinkedCounter will   simply   set the   radix   (which will be   <= 10) and initialize front to a single Node with the value 0:
public LinkedCounter(int rad) 
The   rad   value represents the radix for your LinkedCounter,   in the same way as   explained   for   ArrayCounter above.
6)       A second constructor for the class will take   an argument of   the   interface   type   (CountInterface)   and produce a copy of   that object as a new LinkedCounter.    Note   (as   above   for ArrayCounter)      that   the   interface   contains   all   of   the   methods   necessary   to   make   a   copy   of   the   object – consider the methods and how they can be used to make a copy.    The   header   should be   as   follows:
public LinkedCounter(CountInterface orig) 
Note that the orig reference could be accessing either an ArrayCounter object   or   a   LinkedCounter   object.    This should not matter and the constructor should work regardless of   the   object type   of orig.
7)       Be careful to handle special cases.      Remember to   test   for null   appropriately!
Testing and Submission; 
Your ArrayCounter and LinkedCounter classes must work with the provided main program Assig4Test.java and the output must match that shown in file   a4out.txt. Both   of   these   files   can be   found   in   Canvas at Files/Assignments/Assignment4/. Read over Assig4Test.java very carefully – the comments will   be   helpful.    If   you   cannot   get   something   to   work   (ex: copy   constructor)   comment   that   part   out   of Assig4Test.java so that you can still get credit   for the   rest of   the   functionality.      Note   that as   you   are developing your classes you may also want to write your own, simple test program to   check the   various   methods as you complete them. 
−         Don't forget your Assignment Information Sheet -- you will lose points without it.
−         Don't forget to comment your code – you will lose points without them.
−       Note that you   must have   5   files   in   your   .zip   submission   file   for   this   assignment:
1)       ArrayCounter.java (written by you)
2)       LinkedCounter.java   (written   by   you)
3)       CountInterface.java   (provided)
4)       Assig4Test.java   (provided)
5)       Your assignment information   sheet
Make sure all of   these files are present – if   the   TA   cannot   compile   the   program   from your   submission,   it   will be graded as though it does not work.
Extra Credit Option 
1)       As specified in this assignment, the   radix value   for   your   counters   must be   less than   or   equal   to   10.   In computer science, counting   is sometimes   done   in hexadecimal – which has   16   digits.
Typically, the hexadecimal digits are: 0,   1, 2, 3,   4,   5,   6,   7,   8,   9, A,   B,   C,   D,   E,   F.      Enhance   your classes to allow them to have a radix of   up to   16, with   the   digits   after   9 being   as   shown above.      If   you do this you should think about the digits in   two   different ways:   1)   How will they be   stored   in   your class in order to do the math and 2)   How   will   they be   shown   to   the   user.      This   will   require perhaps some extra data and some   extra logic   in   your   classes.      If   you   do   this   option, provide   a   second driver program that tests the radix values above   10. 





         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
