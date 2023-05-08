---
layout: post
title: "Store Password Safely in Database"
description: "How to Store Password Safely in Database"
comments: true
keywords: "password, security, authentication, database"
---
### Introduction

- Storing password for users is an essential part of any application which provides access user access to the application. Storing passwords securely becomes very crucial to protect user’s sensitive information.

### Ways to store passwords

There are many ways to store passwords.

1. Storing them as plain text. This is least secure.
2. Hashing the password: In this we would hash the plain-text password with a hashing algorithm which generates a random irreversible string that can be store.
3. Using salt: A salt is random string that is appended to the password before hashing. This prevents attacker from using precomputed rainbow tables to crack the hashed password.

### Store a password

1. The password is provided by the client during sign-up.
2. A salt is appended to the password. The salt is stored as plain text in the database.
3. The combination of password and salt is hashed with a hashing function and stored in the database.

   ![Store a password](https://github.com/sanjeevpr/sanjeevpr.github.io/raw/main/assets/images/store-a-password.png)


### Validate a password

1. User enters the password to be validated.
2. The combination of the password and salt is hashed, say H1.
3. The previously stored hash of password and salt, say H2, is retrieved from the database and is compared with the H1.
4. If H1 is equal to H2, then the password is valid. Otherwise it is not.

![Validate a password](https://github.com/sanjeevpr/sanjeevpr.github.io/raw/main/assets/images/validate-a-password.png)

### Reference

- [https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html)
