```c
#include <stdio.h>
  
const char *p;
void dont_do_this(void) {
  const char c_str[] = "This will change";
  p = c_str; /* Dangerous */
}
 
void innocuous(void) {
  printf("%s\n", p);
}
 
int main(void) {
  dont_do_this();
  innocuous();
  return 0;
}
```



```c
void squirrel_away(char **ptr_param) {
  char local[10];
  /* Initialize array */
  *ptr_param = local;
}
 
void rodent(void) {
  char *ptr;
  squirrel_away(&ptr);
  /* ptr is live but invalid here */
}
```

if malloc() is not declared, either explicitly or by including stdlib.h, a compiler that conforms only to C90 may implicitly declare malloc() as int malloc(). If the platform's size of int is 32 bits, but the size of pointers is 64 bits, the resulting pointer would likely be truncated as a result of the implicit declaration of malloc(), returning a 32-bit integer.
```c
#include <stddef.h>
/* #include <stdlib.h> is missing */
  
int main(void) {
  for (size_t i = 0; i < 100; ++i) {
    /* int malloc() assumed */
    char *ptr = (char *)malloc(0x10000000);
    *ptr = 'a';
  }
  return 0;
}
```

compiler assume return regular int when not return
```c
#include <limits.h>
#include <stdio.h>
  
foo(void) {
  return UINT_MAX;
}
 
int main(void) {
  long long int c = foo();
  printf("%lld\n", c);
  return 0;
}
```
