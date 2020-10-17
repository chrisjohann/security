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

#### No pot of gold at the end of the rainbow.  

   You can only use rainbow tables to reverse the hashes you calculated when you created the table, not any arbitrary hash. In other words, you can’t expect the table to store 
   information that you never put there in the first place. Since the input space of server_secret||password is disjoint from the space of possible unsalted passwords, you 
   cannot use the original rainbow table (which only accounted for plain 8-byte passwords) to extract server_secret||password. What’s more, if you could, then you could easily            extract both the server_secret and the password (remember, || means concatenation), which would render the server_secret useless.

#### A hash, by any other name, would smell as sweet.

A hash is basically a function that maps a variable-length input to a fixed length output. A cryptographic hash has some extra properties (first pre-image resistance, second pre-image resistance, collision resistance), but the fundamental nature of the function is the same. So: using SHA-256 twice is still a hash function. Using SHA-256 three times is still a hash function. Even using SHA-256 ten times is still a hash function. All of these would have fairly similar properties, with some slight differences in processing time (though not as significant, as, say, SHA-256 vs Bcrypt, which is many thousands of times slower). So, using a double SHA-256 hash instead of a single one does not make rainbow tables impossible – the attacker would just need to use a double hash as well when creating the table.

#### Salt is salt!

A fair number of people’s suggested security improvements essentially boiled down to the phrase “use a salt” – but the server_secret is technically a salt as well, so we already are! The important part is that it’s better to use a per-user salt than a per-server salt. So be sure to specify exactly what you mean – miscommunications can lead to serious security flaws…

#### Salty secrets.

The beauty of using a salt is that the salt itself does not really need to stay secret to help protect the password. It will still be a thorn in the side of the attacker, even if the attacker knows what it is, because it invalidates any precomputed unsalted hashes. As such, storing the salt in a separate server or database from the password hashes is not especially helpful; in fact, any server that performs password verification will need to have simultaneous access to both the hashes and the salts – how else would it compare the password provided by the user against the stored hash? This means that any meaningful separation (such as an air gap) is not practical. It is fine to just store salts in plaintext alongside hashes.

#### Too fast, too furious.

The rainbow table attack assumes that the hacker has already obtained a list of password hashes, and is trying to reverse-engineer the passwords themselves. Under this assumption, measures like website login rate-limiting will have no effect, since we cannot slow down the attacker’s local computations once they have obtained the hash database.

#### No going back now.

Once you have salted and hashed a password, you cannot simply decide to update the hash by periodically rehashing the password with a different salt. This would mean you have to unhash the hashed & salted password to get back the original password||salt, switch out the salt, and rehash. The whole point of hashes is that they are very difficult to reverse, so the only way to do this would be to essentially launch a rainbow attack against your own hash database. Of course, this is assuming you are not storing the original password – if you are, then shame on you, and what is the point of hashing & salting then anyway?

#### Rainbows, sunshine, and daisy chains.

Rainbow tables allow simultaneously checking all chains (columns)! No need to recompute for each chain. Note that in a rainbow table that consists of k chains (columns), there is no need to recompute hash/reduction functions for each chain. Instead, the attacker computes R_last(target-digest), and checks that against all the endpoints of all chains. If it matches any endpoint, then that chain likely has the corresponding password. Otherwise, compute R_last(H(R_second_to_last(target-digest))), and compare the result with all endpoints. Rinse and repeat. In the worst case, you have to compute as many hash/reduction functions as there are links in 1 chain (regardless of the number of chains since all chains use the same hash and reduction functions).

# Module 7

## Semantic Security
* Definition SS: Ciphertext indistinguishability against chosen plaintext attackers (IND-CPA)

### $\forall$m<sub>0</sub>,m<sub>1</sub> $\in$ M, {k }

## IND-CPA

* __"Security Game"__ = Challenger vs Adversary (where challenger knows k)

* __Advantage Formula__ = Adv<sub>IND-CPA</sub>[A,E] = |Pr[A guesses b' = b] - 1/2| 

