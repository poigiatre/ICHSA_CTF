# ICHSA_CTF_Super_Super_Mario
This is the first time I write writeup so hope you forgive my carelessness.

So there are the letters of the flag are found in the end of each level and are made of coins (one letter in the end of each level)
And we will play this game and find the flag(I enjoy this way than find the coin position in the code when disassemble the program in Ghidra)
The problems when we played the game are number of lives, time and we can be easily killed.
So I will resolve the 3 problems to make this much easier.

First is the number of lives. When we play the game we can see we got 3 lives.

![numofLives](https://github.com/poigiatre/ICHSA_CTF/blob/Super_Super_Mario/NumberofLives1.jpg)

and when the mario died, the number of lives reduced by 1 until we got no lives and game over.
So we won't let the game reduces our lives.
In Ghidra there are 2 times the getNumOfLives and setNumOfLives are called when playerDeath

![getnumofLive1](https://github.com/poigiatre/ICHSA_CTF/blob/Super_Super_Mario/Get_SetNumofLives2.jpg)

![getnumofLive2](https://github.com/poigiatre/ICHSA_CTF/blob/Super_Super_Mario/Get_SetNumofLives3.jpg)

It gets the number of lives to eax then subtracts it by 1 and then set the numbers of lives with that eax.

So we just need to modified the 0x1 to 0x0

I use r2 for this (remember to make a copy of the original file just in case we mess up)

Modified those 0x1. Use this tutorial if you don't know how to patch binary, it helps me a lot (https://www.youtube.com/watch?v=o-Y0KffWgQI)

The first problem solved.

Now the time. So when we out of time, the Mario dies. It is implemented here.

![time](https://github.com/poigiatre/ICHSA_CTF/blob/Super_Super_Mario/Time1.jpg)

It jumps if greater and if it smaller or equal, it will continue to call the playerDeath

So we just need to make it jump even it smaller or equal by change the jg to jmp.
Again, r2 for this.

We can play the game much easier now but to make it even easier, Mario will not die unless he falls into a hole.
This can be done thanks to the given hint.

As I noticed, there is a variable call unKillAble in Player.cpp:

![unkill1](https://github.com/poigiatre/ICHSA_CTF/blob/Super_Super_Mario/unKillAble1.jpg)

Why don't we change it to true.

This is the variable but in Ghidra:

![unkill2](https://github.com/poigiatre/ICHSA_CTF/blob/Super_Super_Mario/unKillAble2.jpg)

0 = false so 1 = true.
Change it into 1 will solve the problem.

So there we go.
