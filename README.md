# GhostLeg-Pointer-Vilsualize-cpp
Using the rule of ghost leg to visualize the swapping of of multi-level Pointers<br>

A pointer is another way to access to the memory location of a variable.

<pre>
int N = 12;
int *pointer;
pointer = &N; //point to N and & means changeble because &N means the address of N.
</pre>

now if we cout pointer it will give us the address of N. Only if we cout *pointer that means the value inside the address of N, which is 12. Therefore if we change pointer we change the address, which has nothing to do with N. But if we change *Pointer what we actually change is the value of N.<br>

So when:

<pre>
int a, *b, **c, ***d, ****e;
a = 10;
b = &a;
c = &b;
d = &c;
e = &d;
cout << ****e << ***e <<  **e <<  *e <<  e << endl;</pre>

we actually made a pointer e which point to other address four time. We will cout the value of a, then the address of a, b, c, d.<br>

## Our class has a cool example:

<pre>
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
</pre>

The result is:<br>
11 22 33<br>
22 11 33<br>
22 33 11<br>
11 33 22<br>
11 22 33<br>
11 33 22<br>
22 33 11<br>

We swap some value (the value can be address) each time after cout the **c1 **c2 and **c3 ( the *b's the **c's linked to, to the a's the *b's linked to. )

![Logo](images/first.png)

When we swap b2 and b3 what we actually do is give b2 the address b3 has and give b3 the address b2 has. That is, if b2 was link to a2 (22) and b3 is link to a3 (33), now *b2 is 33 and *b3 is 22. When we swap *c2 and *c3 what we swap is b2 and b3. <br>

I think of a cool way to visualize it: using the ghost leg:

![Logo](images/leg.png)

Now instead of a b c and 1 2 3 we use (the value of a1 a2 a3) at the top and (**c1 **c2 **c3) at the bottom. For each swap we just need to draw a line between the two number. Considering the swap between a1 and a3 we actually need to make a stereoscopic version. After testing and thinking by myself, I found out that the latter changes should be draw below the former ones. For example, if we swap a1 and a2 then swap a2 and a3, now a3 has the value of orig. a1. We draw the line connecting line 3 and line 2 below the line connecting line 2 and line 1 to ensure this happens correctly.<br>

What if we swap the a's, the b's and the c's but not in the sequence of a, b, and c? Which should be placed at the bottom? They should be put in different layers. In other words, we can deal the swapping of them seperately. The swaping of c's has nothing to do with the swaping of b's and a's. Since the sequence is c to b to a, the swapping of c should be the lowest, which is near the **c1, **c2, **c3 at the bottom.<br>

The last thing that annoys me is which level and order should I place the *b or **c because they point to the address that is not on their own level. First I thought the swap of *b1 and *b2 equals to the swap of a1 and a2, which is not correct. After countless previous operations, *b1 can already be pointed to a2 or a3. As a matter of fact, we can regard **c as c though it seems incorrect. What the swapping of **c1 and **c2 actually do is to swap the a value of c1 and c2. We can regard it as equivalent to just swapping c1 and c2 because the change of value is actually the same. This can only be wrong when we ask from the sequence of *b1 *b2 *b3 after asking **c1 **c2 and **c3 because what I just did is swaping c instead of swaping a, the result is only correct if we neglect the result of b's.

![Logo](images/result.png)

