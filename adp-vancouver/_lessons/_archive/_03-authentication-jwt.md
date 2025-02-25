# User Sessions and Accounts (3.5 hrs)

## Discussion (5)

1. ( client ) < ------ > (server)
  - what is public / private? (// only server can be private)
  - how does authentication work? Keywords: "session", "cookie", "token"

## Game (20)

1. Start with a Cryptogram.

Show a cryptogram (./cryptogram.png) and have students discuss how they might solve.

Look for them to use the word "key".

2. Show some basic math.

Key + Encrypted Code = Message

3. Communication puzzle.

"A" wants to communicate a number with "B", while "C" is listening in between. How can they securely communicate?
(// answer: give each a secret shared key (a number both know) and add that number to your secret number)
(The transaction is a handshake)

4. A computer could guess this number.

How long would it take a computer with 1 GHz/Sec to solve a 3 letter code.
1000 / 1 000 000 000 = around 0.000001 seconds
We can make passwords longer so it takes a computer longer to crack them.
128 bit encryption refers to a password about 128/30 = 38 characters long = 1e29 seconds
We cannot make a secret "impossible" to crack, but we can make it take a really, really long time to solve.

3. Encryption paint game. Public and private key example.

Let's use a clearer example:

Two people want to communicate a **secret** color, but they can only do so by passing visible colors across the room.

```
Private    Public   Private
         |        |
  A      |        |     B  
         |        |
```

Remind students the goal is to create a "shared key".

A) Both A & B choose a PRIVATE color
B) A & B together choose a PUBLIC color
C) key = PRIVATE_A * PUBLIC * PRIVATE_B

```
Private    Public    Private
         |         |
  "red"  | "white" |  "blue" = key (all 3 mixed)  
         |         |
```

A sends "pink", B mixes pink with blue for the secret key.

4. Encryption as multiplication example. Public and private key example.

```
Private    Public    Private
         |         |
  3      |    4    |     5  
         |         |
```

key = 60

A sends (3 * 4 = 12), B multiplies her secret key (12 * 5 = 60) 

5. It's important that the math is easy to do one way, and hard to do the other way. Like mixing paint.

Imagine we live in a world without division, or that division took a lot of trial and error. This is how encryption works.

## Tokens vs. Cookies (20)

Show a "cookie" and a "token" from Chrome Dev Tools.

Group 1: draw an example of how cookies work.
Group 2: draw an example of how tokens work

Discussion: Which method would you prefer? Why?

JWT Advantages:

1. Tokens are stateless. No need for backend records. Each token contains all the data necessary to validate.
2. Cookies can be accessed by other domains. These can be used by other sites to identify who you are.
3. Cookies only store session id. These ids must be looked up to find the permissions. JWT's can store any valid JSON, For example, storing the users role "admin", etc.
4. JWT's are faster. Cookies store a session id which must be looked up.
5. Cookies are a browser thing, but JWT's work on mobile, IoT, etc.

JWT Disadvantages:

- size: JWT may be large. Each request to the client must include the JWT.

## JWT Demo (30)

Code: Setup a project with JWT's to authenticate the client.


## Login/Password Demo (40)

Code: Setup your project with login and password.

## On Storing Passwords (20)

Discussion: How should you store passwords in your database?

Read: [Hashing Security](https://crackstation.net/hashing-security.htm)
Discussion: Which **hashing algorithm** should you use? Why?

Test your password hash at https://crackstation.net/.

## Authentication as a Service (20)

Read: [An Introduction to OAuth2](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2)
Discussion: How does OAuth2 work?

## OAuth2 Demo (40)

Code: Setup your project with OAuth2 authentication using Github.


## If Time: HTTPS (20)

1. Talk about HTTPS. What is the S? How do you enable it?
2. What is a "certificate authority"? Should we trust a certificate authority?
3. Talk about [Let's Encrypt](https://letsencrypt.org/).

## If Time: 2 Factor Auth
