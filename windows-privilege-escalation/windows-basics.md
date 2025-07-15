---
description: Bare bones basics about windows management
---

# Windows Basics

## Permissions in Windows

### User Accounts

User accounts are used to log into a Windows System.  User accounts are basically a collection of settings bound to a particular unique identity.

There are several default user accounts like **Guest** and **Administrator**.

### Managing user accounts

#### The net user command

The `net user` command is used to manage Windows user accounts.&#x20;

*   To list all users:

    ```
    net user
    ```
*   To add a user named "John" with password "Pass123":

    ```
    net user John Pass123 /add
    ```
*   To disable user "John":

    ```
    net user John /active:no
    ```
*   To delete user "John":

    ```
    net user John /delete
    ```

#### Using wmic&#x20;

List users

```
wmic useraccount get name,sid
```





