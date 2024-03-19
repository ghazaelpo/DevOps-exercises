# Working with Loops

Create a new playbook that add users: user1 and user2 to group wheel:

![Screen Shot 2021-10-20 at 17.46.02.png](Working%20with%20Loops%20c1a3c66c07284bad85d5483e8cce99eb/Screen_Shot_2021-10-20_at_17.46.02.png)

The command for execute this playbook is the below:

```bash
ansible-playbook addusers.yml -i myfirstin.in -u adminuser
# Our playbook file is called addusers.yml
# Our inventory file is called myfirstin.in
# We used -u flag to specify the user for our VM
```

As you can see our playbook is connecting to an IP direction, this is our Ubuntu VM.

This information is specified in inventory file called myfirstin.in:

![Screen Shot 2021-10-20 at 17.54.27.png](Working%20with%20Loops%20c1a3c66c07284bad85d5483e8cce99eb/Screen_Shot_2021-10-20_at_17.54.27.png)

Output after executed the playbook:

![Screen Shot 2021-10-20 at 17.48.14.png](Working%20with%20Loops%20c1a3c66c07284bad85d5483e8cce99eb/Screen_Shot_2021-10-20_at_17.48.14.png)

Even if we run again we will see OK, that is mean that users are already created:

![Screen Shot 2021-10-20 at 17.49.26.png](Working%20with%20Loops%20c1a3c66c07284bad85d5483e8cce99eb/Screen_Shot_2021-10-20_at_17.49.26.png)

[Adhoc Commands](Working%20with%20Loops%20c1a3c66c07284bad85d5483e8cce99eb/Adhoc%20Commands%20faffe5de47344610868a695edf4903e1.md)

[Working with loops and systemd module](Working%20with%20Loops%20c1a3c66c07284bad85d5483e8cce99eb/Working%20with%20loops%20and%20systemd%20module%20d9897e40340449bea4d39145a75a5a9e.md)