# Adhoc Commands

Working with adhoc commands

Create a adhoc command that display the first 10 users located in /etc/passwd. Use only adhoc command, find the way to pass parameters for the module used.

The command to use is the below:

```bash
02-adhoc % ansible all -m shell -a "head -n 10 /etc/passwd" -i myfirstin.in -u adminuser
```

Output from the command **first 10 users located in /etc/passwd**

![Screen Shot 2021-10-20 at 23.25.12.png](Adhoc%20Commands%20faffe5de47344610868a695edf4903e1/Screen_Shot_2021-10-20_at_23.25.12.png)

Even you can set a variable and pass as parameter, example:

```bash
NUMERO=10
echo $NUMERO
02-adhoc % ansible all -m shell -a "head -n $NUMERO /etc/passwd" -i myfirstin.in -u adminuser
```

![Screen Shot 2021-10-20 at 23.30.55.png](Adhoc%20Commands%20faffe5de47344610868a695edf4903e1/Screen_Shot_2021-10-20_at_23.30.55.png)