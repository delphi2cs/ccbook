.intel_syntax noprefix.global mainmain:        mov rax, 42        ret
mov rbp, rsp   // Intelmov %rsp, %rbp // AT&Tmov rax, 8     // Intelmov $8, %rax   // AT&Tmov [rbp + rcx * 4 - 8], rax // Intelmov %rax, -8(rbp, rcx, 4)    // AT&T
{% tabs %}
{% tab title="9cc.c" %}
#include <stdio.h>#include <stdlib.h>int main(int argc, char **argv) {  if (argc != 2) {    fprintf(stderr, "引數數量錯誤\n");    return 1;  }  printf(".intel_syntax noprefix\n");  printf(".global main\n");  printf("main:\n");  printf("  mov rax, %d\n", atoi(argv[1]));  printf("  ret\n");  return 0;}
{% endtab %}
{% endtabs %}
$ gcc -o 9cc 9cc.c$ ./9cc 123 > tmp.s
$ cat tmp.s.intel_syntax noprefix.global mainmain:  mov rax, 123  ret
$ gcc -o tmp tmp.s$ ./tmp$ echo $?123
{% tabs %}
{% tab title="test.sh" %}
#!/bin/bashtry() {
{% endtab %}
{% endtabs %}
$ ./test.sh0 => 042 => 42OK
$ ./test.sh0 => 042 expected, but got 123
$ bash -x test.sh+ try 0 0+ expected=0+ input=0+ gcc -o 9cc 9cc.c+ ./9cc 0+ gcc -o tmp tmp.s+ ./tmp+ actual=0+ '[' 0 '!=' 0 ']'+ try 42 42+ expected=42+ input=42+ gcc -o 9cc 9cc.c+ ./9cc 42+ gcc -o tmp tmp.s+ ./tmp+ actual=42+ '[' 42 '!=' 42 ']'+ echo OKOK
{% tabs %}
{% tab title="Makefile" %}
CFLAGS=-std=c11 -g -static9cc: 9cc.c
{% endtab %}
{% endtabs %}
{% tabs %}
{% tab title=".gitignore" %}

{% endtab %}
{% endtabs %}
$ git config --global user.name "Rui Ueyama"$ git config --global user.email "ruiu@cs.stanford.edu"
$ git initInitialized empty Git repository in /home/ruiu/9cc$ git add 9cc.c test.sh Makefile .gitignore
$ git log -pcommit 0942e68a98a048503eadfee46add3b8b9c7ae8b1 (HEAD -> master)Author: Rui Ueyama <ruiu@cs.stanford.edu>Date:   Sat Aug 4 23:12:31 2018 +0000    做出可以編譯一個整數的編譯器diff --git a/9cc.c b/9cc.cnew file mode 100644index 0000000..e6e4599--- /dev/null+++ b/9cc.c@@ -0,0 +1,16 @@+#include <stdio.h>+#include <stdlib.h>++int main(int argc, char **argv) {+  if (argc != 2) {...