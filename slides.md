### Yrola - A column database for random writes in Rust

Stefan O'Rear

<sorear2@gmail.com>

<stefan@gudtech.com>

https://github.com/sorear/yrola

---

# Me

 * Something TODO
 * I like turtles

---

## The Use Case

* We want Alice to be able to count the pencils that her company shipped to Uganda yesterday
* We need a database with *fast bulk reads* / she's not going to wait an hour
* We need a database with *efficient random writes* / New data is loaded constantly

---

## What we've studied

* MySQL: very reliable, fast writes, reads are too slow
* Vertica: fast, big hardware, expensive, closed source
* Several Hadoop-based options exist
* MonetDB: Actually pretty close, but…

---

## MonetDB

* Quite mature system, developed in 2002 at CWI
* Designed for science applications / post-facto analysis of constant data
* Extremely fast queries

---

## How MonetDB works
ant immutable vector memmapped to a file

=== What I'm trying to do

Analytics got you down?
"Hmm, I think this query is going to take O(2^38 years to complete)"
There's a solution:
It's called a column store

Note: asdf asdf asdf

---

=== What we do today

We use Mo

---

=== Why does that suck?

Because

<!-- Story Time - Yrola Edition:
Who Am I - I’m Stefan O’Rear, I work for a company called güdTECH.
Why
Motivated by ROP reporting requirements
We have lots of updates in our operational database
Alice wants to know how many pencils were shipped to Uganda this week
She’s eager to have up-to-the-minute numbers
But there’s a new order coming in every 50 seconds
Normal (OLTP) databases aren’t fast enough for while-you-wait reporting
OLAP databases are a thing, but prior art is kinda meh
(What’s an OLAP database?  Maybe talk briefly about columnar data)
Rather few open-source query databases (and most of them are Hadoop-based)
Proprietary OLAP databases have beastly hardware requirements, onerous license terms
We’ve been using MonetDB for a while for our system
It’s great for queries - Literally 1,000 times faster than mysql
compare and contrast example
Mysql takes 10 minutes to run this
MonetDB takes 0.5 seconds
Updates not so much, grinds to a halt on write IO
I’ve spent some of the last few months thinking about how to have our cake and eat it
What’s wrong?
How does a vector/column store work?
Make some nice pictures
Talk about memory hierarchies and performance factors
Why are updates slow?
Point writes are quite problematic (what’s a point write?)
MonetDB doubly so since it rewrites the columns…but even if it didn’t, IOPS saturation is a thing
What am I doing?
How do I make updates faster, without hurting queries too much?
Hybridize with LSM-trees
Multiple vectors
Introducing Yrola
Demo what I have
Why Rust?
Because I made a point to not spend very much time thinking about what language to use - Rust is excellent at fading into the background
In order to efficiently use memory it’s helpful to have good control over object lifetimes
Bonus: Time series
It looks like sequential append/sequential read, but if you are spreading writes between 60,000+ “tables”, it’s more random than you realize
The SAME TECHNIQUES work here!
Thank you
 -->



---

## Thanks

twitter: @tureus

email: xrlange@gmail.com

graphite-rust: https://github.com/tureus/graphite-rust
