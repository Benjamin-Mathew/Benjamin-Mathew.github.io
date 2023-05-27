---
layout: post
title:  The Fascination of Reversibility in Quantum Computing
date:   2023-05-20
description: Boolean Circuits to Quantum Circuits
tags: quantum quantum-lecture
categories: research-posts
---

In the realm of quantum computing, there exists an intriguing fondness for reversible operations. Simply put, every quantum computation or operation must possess the property of reversibility. You might wonder why this is the case. Interestingly, reversibility is not a requirement in classical computing. Consider, for instance, the AND gate. Merely knowing that the output is 0 does not allow us to confidently determine the input with complete certainty.

Therefore, when it comes to performing computations on a quantum computer, the foremost consideration is that they must be invertible. Let's take a step back and examine the classical setting. We know that NAND is a universal gate, meaning any circuit comprising of AND, NOT, and OR gates can be efficiently transformed into an equivalent circuit consisting solely of NAND gates. However, there's an important aspect we often overlook in classical circuits, and that is the ability to copy a wire. To delve deeper into this, let's introduce a new gate called COPY, which generates an additional copy of the input. Consequently, we can assert that the NAND gate, in conjunction with the COPY gate, is universal. Nevertheless, it's worth noting that NAND gate is not reversible.

Enter the CCNOT gate, coming to the rescue. This gate takes three inputs, denoted as  $$x_1, x_2, x_3$$ and produces three outputs, denoted as $$y_1, y_2, y_3$$ with the following description.

$$y_1 = x_1, y_2 = x_2, y_3 = (x_1 \cdot x_2) \oplus x_3$$

Observe that this is invertible (reversible) as demonstrated below.

$$x_1 = y_1, x_2 = y_2, x_3 = (y_1 \cdot y_2) \oplus y_3$$

Now, for the twist. The CCNOT gate can simulate both NAND and COPY gates in the following manner:

$$NAND: (x_1, x_2, 1) \xrightarrow{CCNOT} (x_1, x_2, \overline{x_1 \cdot x_2})$$

$$COPY: (1, x, 0) \xrightarrow{CCNOT} (1, x, x)$$

The only caveat is that additional inputs (ancillas) and outputs (garbage) need to be taken into account. This cannot be avoided because the requirement of invertibility mandates that the number of inputs be equal to the number of outputs. Nevertheless, we can now convert any classical circuit into an (almost) equivalent circuit that is reversible.

Voilà! We can simulate any classical circuit on a quantum computer. This is due to the existence of an equivalent quantum CCNOT gate with the same description. If we combine this with the Hadamard gate (which will be described in the next paragraph), the pair becomes universal in the quantum setting.

But, what about randomized computation? There is a simple trick to address this as wekk. We only need a quantum means of generating random coins. Enter the Hadamard gate, which possesses the following description:

$$H \ket{0} = \dfrac{1}{\sqrt{2}} (\ket{0} + \ket{1})$$

$$H \ket{1} = \dfrac{1}{\sqrt{2}} (\ket{0} - \ket{1})$$

To randomly generate a single classical bit, we simply start with $$\ket{0}$$ state, apply H gate and measure the output. Notice that the output of the H gate is $$\dfrac{1}{\sqrt{2}} (\ket{0} + \ket{1})$$, and upon measuring this state, we get $$\ket{0}$$ with probability $$\dfrac{1}{2}$$ and $$\ket{1}$$ with probability $$\dfrac{1}{2}$$.


**References**
1. Nielsen, M. A., & Chuang, I. (2002). Classical computations on a quantum computer. *Quantum computation and quantum information*.
2. <a href="https://www.cs.cmu.edu/~odonnell/quantum15/homework/homework1.pdf">https://www.cs.cmu.edu/~odonnell/quantum15/homework/homework1.pdf </a>
