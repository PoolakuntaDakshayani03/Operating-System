#Exp1: basics of unix commands
general commands
  date
  Used to display the current system date and time.
  date +%D
  Displays date only
  date +%T
  Displays time only
  date +% Y
  Displays the year part of date
  date +% H
  Displays the hour part of time
  cal
  Calendar of the current month
  cal year
  Displays calendar for all months of the specified year
  cal month year
  Displays calendar for the specified month of the year
  who
  Login details of all users such as their IP, Terminal No, User name,
  who am i
  Used to display the login details of the user
  tty
  Used to display the terminal name
  uname
  Displays the Operating System
  unameOperating System Lab Manual Department of CSE, SRIT, ATP
  Prepared by Mr. M. Narasimhulu, 4
  Shows version number of the OS (kernel).
  uname –n
  Displays domain name of the server
  echo "txt"
  Displays the given text on the screen
  echo $HOME
  Displays the user's home directory
  bc
  Basic calculator. Press Ctrl+d to quit
  lpfile
  Allows the user to spool a job along with others in a print queue.
  man cmdname
  Manual for the given command. Press q to exit
  history
  To display the commands used by the user since log on.
  exit
  Exit from a process. If shell is the only process then logs out
  
# Simulate UNIX commands like cp, ls, grep, etc
# Cp simulate command Source code
```c
#include <stdio.h>
#include <stdlib.h>
void simulate_cp(const char *source, const char *destination) {
FILE *src = fopen(source, "r");
FILE *dest = fopen(destination, "w");
if (!src || !dest) {
perror(!src ? "Error opening source file" : "Error opening destination file");
if (src) fclose(src);
return;
}
char buffer[1024];
size_t bytes;
while ((bytes = fread(buffer, 1, sizeof(buffer), src)) > 0) {
fwrite(buffer, 1, bytes, dest);
}
printf("File '%s' copied to '%s'\n", source, destination);
fclose(src);
fclose(dest);
}
int main(int argc, char *argv[]) {
if (argc != 3) {
fprintf(stderr, "Usage: %s <source_file> <destination_file>\n", argv[0]);
return EXIT_FAILURE;
}
simulate_cp(argv[1], argv[2]);
return EXIT_SUCCESS;
}
```
# Simulation command for ls command
~~~ c
#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>
void simulate_ls(const char *path) {
struct dirent *entry;
DIR *dir = opendir(path);
if (!dir) {
perror("Error opening directory");
return;
}
while ((entry = readdir(dir)) != NULL) {
if (entry->d_name[0] != '.') {
printf("%s ", entry->d_name);
}
}
printf("\n");
closedir(dir);
}int main(int argc, char *argv[]) {
const char *path = argc > 1 ? argv[1] : ".";
simulate_ls(path);
return 0;
}
~~~
# simulation command for grep command
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
void simulate_grep(const char *pattern, const char *filename) {
FILE *file = fopen(filename, "r");
if (!file) {
perror("Error opening file");
return;
}
char line[1024];
while (fgets(line, sizeof(line), file)) {
if (strstr(line, pattern)) { // Check if pattern exists in the line
printf("%s", line);
}
}
fclose(file);
}int main(int argc, char *argv[]) {
if (argc != 3) {
fprintf(stderr, "Usage: %s <pattern> <filename>\n", argv[0]);
return EXIT_FAILURE;
}
simulate_grep(argv[1], argv[2]);
return EXIT_SUCCESS;
}
```c
