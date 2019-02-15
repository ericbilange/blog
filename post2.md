# How to implement the right to forget

Here is a _privacy_ requirement which is hard to implement: the "right to forget".

_Why is it hard to implement?_

Well, at the beginning of a system, it is not really hard: there is nly one database, maybe several tables that contain information about a user. So ask your DBA (database administrator) to "erase" all data for "that user". Easy.

Afer years of use, a system evolves, more tables are added, more databases, backups are made, systems are cloned to scale up, etc. And guess what: one user associated set of data is in multiple places, hard to find. And there comes the diffculty to implement the "right to forget": how can you be sure that your DBA (who is a good and competent guy) will erase **_all_** data for that specific user?

_So what shall I do?_

One simple trick, which needs to be put in place straight from the beginning, is to think that data is owned only by users. With this in mind, you want to think "privacy" and "security" in general: not only you want to implement the right to forget, but also you want to protect user data. Cryptography comes handy (and even if it requires some extra CPU cycles, we don't care anymore today as 'compute' is cheap). The trick is to generate a unique key to your users (you can make a sophisticated model or a simple one, it's all according to your taste and risk assessment) and encrypt user data with their key. Net result: data is not human readable, so if your DBA (well, who was a good guy so far) decides to open your databases and read their content, she will not be able to understand what's in there. Ah, well of course if she knows that she has to get the user key and then decipher the data for this user... ok she will be able to read it. But hey, that's not an easy step if keys are stored in a separate location only accessible by machines and trusted admins. 

Ok, we got the privacy aspect: user data is encrypted with their unique key. Now how do we implement the right to forget? That's trivial: delete the key! And you have all the time in the universe to actually delete the data; it's useless as it cannot be decrypted anymore!