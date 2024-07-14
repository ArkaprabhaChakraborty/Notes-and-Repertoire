---
description: How to use metasploit database effectively
---

# Working with Metasploit Database

## Setting it up

Metasploit has a database function to simplify project management and avoid confusion when setting up parameter values.&#x20;

You will first need to start the PostgreSQL database, which Metasploit will use with the following command:&#x20;

`systemctl start postgresql`

Then you will need to initialize the Metasploit Database using the `msfdb init` command.

```
root@ip-10-10-46-245:~# systemctl start postgresql
root@ip-10-10-46-245:~# msfdb init
```

To check if the database has been initiated properly we can troubleshoot using `db_status` command in msfconsole.

```
msf6 > db_status
[*] Connected to msfdb. Connection type: postgresql.
```

## Workspace management

The database feature will allow you to create workspaces to isolate different projects. When first launched, you should be in the default workspace. You can list available workspaces using the `workspace` command.&#x20;

```
msf6 > workspace
* default
```

### Adding a new workspace

Add a workspace using the `-a` parameter.&#x20;

```
msf6 > workspace -a <workspace_name>
```

### Deleting a workspace

Delete a workspace using the `-d` parameter, respectively.&#x20;

```
sf6 > workspace -d new_workspace
[*] Deleted workspace: new_workspace
```

### Switching workspaces

You can switch workspaces using the workspace name

```
msf6 > workspace new
[*] Workspace: new
```

### List all hosts

```
msf6 > hosts

Hosts
=====

address        mac                name     os_name  os_flavor  os_sp  purpose  info  comments
-------        ---                ----     -------  ---------  -----  -------  ----  --------
10.10.170.76   02:a0:d8:c5:80:23  target1  Linux               3.X    server
10.10.205.0
10.10.224.231
```

### Adding new hosts

```
msf6 > hosts -a <ip_address> -n <new_name>
```

The hostname can also be left blank, which can be auto-populated by commands like `db_nmap`.

### Deleting hosts

```
msf6 > hosts -d 10.10.170.76

Hosts
=====

address  mac  name  os_name  os_flavor  os_sp  purpose  info  comments
-------  ---  ----  -------  ---------  -----  -------  ----  --------
```

### Nmap scanning with db\_nmap

The db\_nmap command can be useful for scanning hosts and services

## Database Commands cheatsheet

| Command            | Description                                                                     |
| ------------------ | ------------------------------------------------------------------------------- |
| analyze            | Analyze database information about a specific address or address range          |
| db\_connect        | Connect to an existing data service                                             |
| db\_disconnect     | Disconnect from the current data service                                        |
| db\_export         | Export a file containing the contents of the database                           |
| db\_import         | Import a scan result file (filetype will be auto-detected)                      |
| db\_nmap           | Executes nmap and records the output automatically                              |
| db\_rebuild\_cache | Rebuilds the database-stored module cache (deprecated)                          |
| db\_remove         | Remove the saved data service entry                                             |
| db\_save           | Save the current data service connection as the default to reconnect on startup |
| db\_status         | Show the current data service status                                            |
| hosts              | List all hosts in the database                                                  |
| klist              | List Kerberos tickets in the database                                           |
| loot               | List all loot in the database                                                   |
| notes              | List all notes in the database                                                  |
| services           | List all services in the database                                               |
| vulns              | List all vulnerabilities in the database                                        |
| workspace          | Switch between database workspaces                                              |
