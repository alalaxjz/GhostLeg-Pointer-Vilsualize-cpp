# GhostLeg-Pointer-Vilsualize-cpp
Using the rule of ghost leg to visualize the swapping of of multi-level Pointers<br>

A pointer is another way to access to the memory location of a variable.

<pre><br>
int N = 12;
int *pointer;
pointer = &N; //point to N and & means changeble because &N means the address of N.
<br></pre>

now if we cout pointer it will give us the address of N. Only if we cout *pointer that means the value inside the address of N, which is 12. Therefore if we change pointer we change the address, which has nothing to do with N. But if we change *Pointer what we actually change is the value of N.<br>

So when:

<pre><br>
int a, *b, **c, ***d, ****e;
a = 10;
b = &a;
c = &b;
d = &c;
e = &d;
cout << ****e << ***e <<  **e <<  *e <<  e << endl;<br></pre>

we actually made a pointer e which point to other address four time. We will cout the value of a, then the address of a, b, c, d.<br>

Our class has a cool example:

<pre><<br>
#include <iostream>
using namespace std;

int main() {
  int a1, a2, a3;
  a1 = 11;
  a2 = 22;
  a3 = 33;
  int *b1, *b2, *b3;
  b1 = &a1;
  b2 = &a2;
  b3 = &a3;
  int **c1, **c2, **c3;
  c1 = &b1;
  c2 = &b2;
  c3 = &b3;
  cout << **c1 << " " << **c2 << " " << **c3 << endl;
  swap(a1, a2);
  cout << **c1 << " " << **c2 << " " << **c3 << endl;
  swap(b2, b3);
  cout << **c1 << " " << **c2 << " " << **c3 << endl;
  swap(c1, c3);
  cout << **c1 << " " << **c2 << " " << **c3 << endl;
  swap(*b1, *b2);
  cout << **c1 << " " << **c2 << " " << **c3 << endl;
  swap(*c2, *c3);
  cout << **c1 << " " << **c2 << " " << **c3 << endl;
  swap(**c1, **c3);
  cout << **c1 << " " << **c2 << " " << **c3 << endl;
  return 0;
}
<br></pre>

The result is:
11 22 33
22 11 33
22 33 11
11 33 22
11 22 33
11 33 22
22 33 11
