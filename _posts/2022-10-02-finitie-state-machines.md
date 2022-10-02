---
layout: post
title: "Finite State Machines"
author: rohan
categories: [computer science, programming]
image: assets/images/le4joppdnt631.png
featured: true
---

# Finite State Machines

## Motivation

State machines can be used in a diverse range of scenarios such as

### Explaining why you are a procrastinator

<!--<img src="file:///C:/Users/rohan/Downloads/le4joppdnt631.png" title="" alt="le4joppdnt631.png" data-align="center">-->
![img1](/assets/images/le4joppdnt631.png)

[Source](https://www.reddit.com/r/uwaterloo/comments/c60obb/the_six_states_of_a_waterloo_student_in_the_form/?utm_source=share&utm_medium=web2x&context=3)

### Designing the Enemy AI in your open-world game

<!--<img title="" src="file:///C:/Users/rohan/Downloads/fsm_enemy_brain.png" alt="fsm_enemy_brain.png" data-align="center">-->
![img1](/assets/images/fsm_enemy_brain.png)

[Source](https://gamedevelopment.tutsplus.com/tutorials/finite-state-machines-theory-and-implementation--gamedev-11867)

### Or Planning out your fanfic plot...

<!--<img src="file:///C:/Users/rohan/AppData/Roaming/marktext/images/2022-07-31-18-21-44-image.png" title="" alt="" data-align="center">-->
![img1](/assets/images/2022-07-31-18-21-44-image.png)

[Source](https://www.tumblr.com/blog/view/prokopetz/168234312947?source=share)

Now that we know that state machines is the hammer that we ought to use on every programming nail(xD), we are ready to run headfirst into situations like...

<!--<img title="" src="file:///C:/Users/rohan/Downloads/download.jpg" alt="download.jpg" width="405" data-align="center">-->
![img1](/assets/images/download.jpg)

[Source](http://www.quickmeme.com/meme/367p2f)

In order to avoid this, let us see where they are actually needed.

Consider a classic example. You are game testing an endless runner where you press space to jump. To your surprise, when you did not lift your finger from space, your character kept jumping infinitely until it exited the map and you were in the void. 

This glitch occurred because the programmer coded the logic using a simple 

```
if(keystroke == space)
    character.y_coordinate += 10
```

This did not account for the fact that the jump should trigger only if the player is on the ground. While this is a simple example and can be easily prevented while visualising the program, it becomes obvious when formulated as a state machine.

![img](/assets/images/2022-07-29-19-50-27-image.png)

Source: [GameplayKit Programming Guide: State Machines](https://developer.apple.com/library/archive/documentation/General/Conceptual/GameplayKit_Guide/StateMachine.html)

Thus a simple abstraction into states has ensured that the game engine does not violate Newton's third law and you can now jump only from the ground.

As your program becomes more and more complex, it is better to separate your code into states and "listen" for a valid input that would cause a transition from the current state. 

## Mathematical Definition

Mathematically, a deterministic finite state machine or a deterministic finite automaton is a quintuple

$$
<\Sigma, S, s_0, \delta, F>
$$

> Well that's scary, let us unpack the tuple

1. $\Sigma$ is the input alphabet (a finite nonempty set of symbols).

2. $S$ is a finite nonempty set of states.

3. $s_0$ is the start (or initial) state, an element of $S$.

4. $\delta$ is the state transition function; $\delta : S \times \Sigma \to S$

5. $F$ is the set of final (or accepting) states, a (possibly empty) subset of s.

> While Greek's still scary, that is still the convention. Let's try to understand these terms better with a few examples

## Revisiting the Jump example

In our jumping example, $\Sigma$ is all possible keystrokes that can be inputted and are parsed by the game. $S$ consists of the states $Running, \ Jumping, \ and \ Falling$. $s_0$ is Running. $\delta$ is illustrated in the figure. The entries of $\delta$ would look like $\delta (Running, space) = Jumping$. 

Since we are not presently discussing the termination of the game, we don't have a final state and $F = \phi$.

Thus, a deterministic finite automaton(DFA) is a mathematical model of a machine that accepts a particular set of words $F$ over some alphabet $\Sigma$. In other words, each input would represent a transition from the current state to some other state, and particular states would represent the end of the game. It is also called an acceptor as the game terminates on accepting a valid sequence(or a word) of inputs(made up of the elements of the alphabet $\Sigma$). An invalid sequence won't terminate the machine.

A state machine can be implemented in a circuit using a sequential circuit consisting of latches. Readers familiar with Digital Electronics may recollect Melay and Moore machines.

## String Acceptor

In the previous section, we hinted at DFAs being acceptors. Let us see another example where this perspective becomes more obvious.

Consider a string acceptor or a regex matcher. Let us assume our regex pattern to be matched is "a*e" and our target string is "apple". 

Here, each state may represent one character in the regex pattern and the transitions represent the characters in the target string. The string is terminated by '\0'.

![](/assets/images/index.png)

As the string "APPLE\0" is read the states followed are A(s1) -> P(s2) - > P(s2) -> L(s2) -> E(s3) -> \0(string accepted).

Here,

1. $\Sigma$ is the characters a...z, '\0'. 

2. $S$ is states $S1$ to $S5$.  

3. $so = \{S1\}$. 

4. $\delta$ is shown in the above figure as $\delta(S1,a) = S2, \delta(S2, e) = S3, ...$.

5. $F = \{S4, S5\}$.

Thus, a finite walk(sequence of states and state-transitions) from the source $S1$ to one of the destinations in $F$ along a word terminating with '\0' signify whether the input matches the regex pattern(terminating at $S4$) or does not (terminating at $S5$). 

> Well, that was a mouthful

![6ohigq.jpg](/assets/images/6ohigq.jpg)

Now that we have gotten an idea of what a Finite State Machine is, look out for the upcoming post on the other classes of Automata.

![JerryJumbo3-1-.jpg](assets/images/JerryJumbo3-1-.jpg)

_Thanks for reading! I hope you’ve enjoyed reading this article. You can find me on_ [_Linkedin_](https://www.linkedin.com/in/s-rohan/) _and_ [_GitHub_](http://github.com/Rohan-Witty).
