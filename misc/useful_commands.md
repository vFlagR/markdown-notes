<html><link rel="stylesheet" href="../css/air.css"></html>

# Useful Commands

##### Find all applications installed in Ubuntu ##### 

~~~shell
sudo apt-get install aptitude
aptitude -F' * %p -> %d ' --no-gui --disable-columns search '?and(~i,!?section(libs), !?section(kernel), !?section(devel))'
~~~

##### Find and Delete Wildcard

~~~shell
find . -maxdepth 1 -name "all.log.*" -print0 | xargs -0 rm
~~~

##### Run commands in Screen

+ Run a single command in Screen

~~~shell
screen -dm COMMAND
~~~

* Run a script in Screen

~~~shell
screen -dm bash -c "script.sh" 
~~~

##### Find the PHP.ini file in use

~~~shell
php -i | grep 'Loaded Configuration File'
~~~

