# Module 1: Security Mindset

- Security mindset
- Case study: Mat Honan

# Module 2 : Processes, address space, stack, Control Hijacking

- What is a process?
- Address Space
- Buffer overflow
- return address vs return value
- Format string and integer overflows
- Useful gdb commands
- Memory safety Attacks and Defenses
- Creating your own shellcode

# Module 3: Control hijacking defenses and advanced attacks

- Stack canaries
- Bounds checking
- NX-bit/DEP
- Return-oriented programming
- ASLR

# Module 4: Privilege  

# Module 7

## Semantic Security
* Definition SS: Ciphertext indistinguishability against chosen plaintext attackers (IND-CPA)

## IND-CPA

* __"Security Game"__ = Challenger vs Adversary (where challenger knows k)

* __Advantage Formula__ = Adv<sub>IND-CPA</sub>[A,E] = Pr[A guesses b' = b] - 1/2
