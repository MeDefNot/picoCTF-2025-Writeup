
# Description #
Try to decrypt the secret cheese password to prove you're not the imposter!
Connect to the program on our server: nc verbal-sleep.picoctf.net 59244

# Hints #
Remember that cipher we devised together Squeexy? The one that incorporates your affinity for linear equations???

# Solution #
```
*******************************************
***             Part 1                  ***
***    The Mystery of the CLONED RAT    ***
*******************************************

The super evil Dr. Lacktoes Inn Tolerant told me he kidnapped my best friend, Squeexy, and replaced him with an evil clone! You look JUST LIKE SQUEEXY, but I'm not sure if you're him or THE CLONE. I've devised a plan to find out if YOU'RE the REAL SQUEEXY! If you're Squeexy, I'll give you the key to the cloning room so you can maul the imposter...

Here's my secret cheese -- if you're Squeexy, you'll be able to guess it:  FUBLOPDFV
Hint: The cheeses are top secret and limited edition, so they might look different from cheeses you're used to!
Commands: (g)uess my cheese or (e)ncrypt a cheese
What would you like to do?
```

`e` encrypts the name of cheeses like blue, cheddar, etc
```
What cheese would you like to encrypt? blue
Here's your encrypted cheese:  HPEM
Not sure why you want it though...*squeak* - oh well!

I don't wanna talk to you too much if you're some suspicious character and not my BFF Squeexy!
You have 2 more chances to prove yourself to me!

Commands: (g)uess my cheese or (e)ncrypt a cheese
What would you like to do?
e

What cheese would you like to encrypt? cheddar
Here's your encrypted cheese:  ARMTTOZ
Not sure why you want it though...*squeak* - oh well!

I don't wanna talk to you too much if you're some suspicious character and not my BFF Squeexy!
You have 1 more chances to prove yourself to me!
```

BLUE = HPEM
#
CHEDDAR = ARMTTOZ

We can see `E` is `M`. Similarly `B` is `H`, `L` is `P` and so on. Affin cyphers have the following formula
#
`(ax + b)%n = cipher_character`
#
Here `a` and `b` being integers. `x` is the original text alphabet's number/sequence (A is 1, B is 2 and so on). `n` is the total number of available characters in the cipher, Which would be 26 here as there are only alphabets ; lower and upper case are treated the same. Also, `a` needs to be coprime with `n(26)`. Which means `a` can be either 2 oe 13.

#
Applying this, In the word CHEDDAR , A(1) became O(15). Let, a = 2,
#
`(2\*1 + b)%26 = 15`
The smallest value of `b` would be `39`. Checking if our formula is correct. We'll try to find the cipher of B and check it with what we have
#
`(2\*2 + 39)%26 = 17(Q)`
But `B` is `H`, not `Q`. Here, `(Q(17) + 17)%26` would give H(8).
#
Checking for `C`,
#
`(2\*3 + 39)%26 = 19(S)`
But `C` is `A`, not `S`. Here, `(S(19) + 2*17)%26 = A(1)`

SO, there seems to be a correction in our formula. The correct one would be,
#
`((ax + b)%n + (a-1)*17)*26 = cipher_character`
#
Coding this in any programming language to find all the cipher characters, (to prevent errors) ,

```
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int a,b;

    a = 2;
    b = 47;

    for(int i = 0; i < 26 ;i++)
    {
        int a = (((i+1)*2+39)%26+i*17)+'A'-1;
        while(a>'Z')
        {
            a = a-('Z'-'A')-1;
        }
        cout<<" |||"<<(char)(i+'A')<<" : "<<char(a);
    }
    return 0;
}
```

Output
```
 |||A : O |||B : H |||C : A |||D : T |||E : M |||F : F |||G : Y |||H : R |||I : K |||J : D |||K : W |||L : P |||M : I |||N : B |||O : U |||P : N |||Q : G |||R : Z |||S : S |||T : L |||U : E |||V : X |||W : Q |||X : J |||Y : C |||Z : V
```

Now, 
```
Commands: (g)uess my cheese or (e)ncrypt a cheese
What would you like to do?
g


   _   _
  (q\_/p)
   /. .\.-.....-.     ___,
  =\_t_/=     /  `\  (
    )\ ))__ __\   |___)
   (/-(/`  `nn---'

SQUEAK SQUEAK SQUEAK

         _   _
        (q\_/p)
         /. .\
  ,__   =\_t_/=
     )   /   \
    (   ((   ))
     \  /\) (/\
      `-\  Y  /
         nn^nn


Is that you, Squeexy? Are you ready to GUESS...MY...CHEEEEEEESE?
Remember, this is my encrypted cheese:  FUBLOPDFV
So...what's my cheese?
```

FUBLOPDFV
Mathing it with our code output, FONTALJFZ

```
So...what's my cheese?
FONTALJFZ

         _   _
        (q\_/p)
         /. .\         __
  ,__   =\_t_/=      .'o O'-.
     )   /   \      / O o_.-`|
    (   ((   ))    /O_.-'  O |
     \  /\) (/\    | o   o  o|
      `-\  Y  /    |o   o O.-`
         nn^nn     | O _.-'
                   '--`

munch...

         _   _
        (q\_/p)
         /. .\         __
  ,__   =\_t_/=      .'o O'-.
     )   /   \      / O o_.-`|
    (   ((   ))      ).-'  O |
     \  /\) (/\      )   o  o|
      `-\  Y  /    |o   o O.-`
         nn^nn     | O _.-'
                   '--`

munch...

         _   _
        (q\_/p)
         /. .\         __
  ,__   =\_t_/=      .'o O'-.
     )   /   \      / O o_.-`|
    (   ((   ))        )'  O |
     \  /\) (/\          )  o|
      `-\  Y  /         ) O.-`
         nn^nn        ) _.-'
                   '--`

MUNCH.............

YUM! MMMMmmmmMMMMmmmMMM!!! Yes...yesssss! That's my cheese!
Here's the password to the cloning room:  picoCTF{ChE...}
```
