# ServiceNow Access Control Rules (ACLs)

Access Control Rules (ACLs) in ServiceNow are used to control access to records, fields, and tables. They determine what users can and cannot do with data in the system.

## What role is needed to create ACLs?

To create ACLs, you need to have the `security-admin` role. 

## Where do I add ACLs? 

You add ACLs from the System Security > Access Control Rules [sys_acl_list] table. 

## A useful analogy

Let's say you are going to an Airbnb. The host has a computer with no passcode, and open Wifi. 

As long as you have the address of the place, you can go to the place, and use the Wifi. 

When you create a custom table -- it will create four ACLs for you:

- Read
- Write
- Delete
- Create

These will have the same name and will have the same role name. So if you wanted to give a new user access to your table, you will add the role to your user, and they will be able to see your table, and add, edit and delete records in it. 

Now, when I saw this the first time, I thought the next logical thing is to create  read-only user for the table, and this turned out to be a little trickier than I expected. 

If you go back to our analogy of the Airbnb, you can say that I will put a passcode on the computer, and then only the people who have the passcode will be able to use the computer. 

So, this may feel a bit weird at first but create a new role for the write operation to all fields with a new role, and then assign this role to only the users who you want to have write access to the table. 

By doing this you will ensure that all other users who don't have this role now become read-only users. 

You can test this out by giving creating an ACL with the following attributes:

- Operation - write 
- Name and field - any name and use * to apply to all fields
- Role - create a new role exclusively for this ACL 

And then assign this role to only the users who you want to have write access to the table. 

Now, assign this role to a user and you will see that they have the entire access to the table but then impersonate with another user and you'll see that while they can access the table, they can't write to it. 

Now, what if you wanted to restrict creation of trees. You can create a new ACL with the following attributes:

- Operation - create
- Name and field - any name and use * to apply to all fields
- Role - create a new role exclusively for this ACL

And then assign this role to only the users who you want to have create access to the table. 

Now, assign this role to a user and you will see that they can create records in the table but then impersonate with another user and you'll see that while they can access the table, and edit records, they can't create records in it. 


