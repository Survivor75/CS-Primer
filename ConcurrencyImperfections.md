## Concurrency Imperfections

I came across imperfections caused by race conditions that might occur when we work with databases, while reading Designing Data-Intensive Applications (DDIA), by Martin Kleppmann. It turns out that if we aren’t careful, concurrent transactions can cause a lot of headaches, to say the least. Finding it easy to forget or confuse these defects for each other, I decided to catalogue them here so they might help others and future me.

