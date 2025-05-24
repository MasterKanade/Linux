The environment variable : PS1

1. The PS1 environment variable stands for "Prompt String1"
2. It defines the appearance of primary shell prompt
3. Highly customizable with escape sequences and special characters
4. Enhances user experience and workflow efficiency

What happens when we change PS1
e.g.:

> PS1="bash-world $ " This will become prompt string and after dollar symbol you can place any linux command.

PS1 supports various placeholders:

1. Username: \u
2. Hostname:
   > upto the first "." : \h
   > The complete hostname : \H

for e.g.:
PS1='\u@\H$'

It will print PS1 string in the format as: Username@Hostname$

It will also provide you full path option while adding with above name as:
Current directory:
\w : full path
\W : last directory of full path

PS1='\u@\H (\w:\W) $'
i.e Username@Hostname (current_working_directory:last_working_directory)

> The time in 24h format: \t
> The time in 12h format: (with am/pm): \@

PS1='\u@\H (\w:\W) $ , (\t \@)'
e.g
Username@Hostname (current_working_directory:last_working_directory) (current_time AM/PM)

The normal and best approach we can use: This is the standard format.
PS1='\u@\h:\w$'

When new bash is opened by user and if you want that your format of PS1 should be opened with username@hostname:path$ then you have to set the PS1
into the .bashrc file as

nano ~/.bashrc
PS1='\u@\h:\w$'
save and close the file.

Everytime when new shell opens then it will be configured automatically with above PS1 string format.
