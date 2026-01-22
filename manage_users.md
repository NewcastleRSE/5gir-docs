# Manage Users

Administrators can manage other users. They can create new users, delete any other users, change the passwords of any
other users, change any other users' permission to the data. Administrators can also make some users administrators.

## Monitor Users
Display all users and their attributes with:
```postgresql
\du
```
Show the username you are logged in as with:
```postgresql
select * from current_user;
```

## Create a New Regular User (Role)

To create a user `james_smith` that is valid until the end of September 2026, run the below. Note that the username
should not be in quotations while the password should be in single quotations. Also, note to that you need to replace
`jw8s0F4` with an appropriate password for `james_smith`:
```postgresql
CREATE ROLE james_smith WITH LOGIN PASSWORD 'jw8s0F4' VALID UNTIL '2026-10-01';
```
To create a user `james_smith` with no expiration date, run this:
```postgresql
CREATE ROLE james_smith WITH LOGIN PASSWORD 'jw8s0F4';
```

## Create a New Administrator
To create a user `james_smith` that can manage other users (create and remove users) and is valid until the end of
September 2026, run the following:
```postgresql
CREATE ROLE james_smith WITH LOGIN PASSWORD 'jw8s0F4' VALID UNTIL '2026-10-01' CREATEROLE;
```

To create a user `james_smith` that can manage other users and does not expire, run this:
```postgresql
CREATE ROLE james_smith WITH LOGIN PASSWORD 'jw8s0F4' CREATEROLE;
```

## Change a User's Password

Change the password of the existing user `james_smith` with:

```postgresql
ALTER USER james_smith WITH PASSWORD 'hr9k7zg';
```


## Change the Expiration Date of a User

Change the date when the existing user `james_smith` expires, run this:

```postgresql
ALTER USER james_smith WITH VALID UNTIL '2030-10-01';
```

## Give User's Permission to Manage Other Users

To give the existing user `james_smith` the permission to manage other users (create and remove other users), run this:
```postgresql
ALTER USER james_smith WITH CREATEROLE;
```

To remove the permission to manage other users of the existing user `james_smith`, run this:
```postgresql
ALTER USER james_smith WITH NOCREATEROLE;
```

## Give Read and Write Permission to a User

If you want to give `james_smith` read-only permission to the DW, then add `james_smith` to the user group
`data_warehouse_read_only` by running:
```postgresql
GRANT data_warehouse_read_only TO james_smith;
```

If you want to give the user `james_smith` read and write permission to the DW, then add `james_smith` to the user group
`data_warehouse_read_write` by running the below:
```postgresql
GRANT data_warehouse_read_write TO james_smith;
```

## Remove a User

To remove the existing user `james_smith`, run this:
```postgresql
DROP ROLE james_smith;
```
