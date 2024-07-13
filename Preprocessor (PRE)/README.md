```c
#define ABS(x) (((x) < 0) ? -(x) : (x))
  
void func(int n) {
  /* Validate that n is within the desired range */
  int m = ABS(++n);
 
  /* ... */
}
```



```c
#include <assert.h>
#include <stddef.h>
   
void process(size_t index) {
  assert(index++ > 0); /* Side effect */
  /* ... */
}
```

> assert is also a Define statment

```c
#define assert(e)  \
    ((void) ((e) ? 0 : __assert (#e, __FILE__, __LINE__)))
#define __assert(e, file, line) \
    ((void)printf ("%s:%u: failed assertion `%s'\n", file, line, e), abort())
```


```c
#include <string.h>
  
void func(const char *src) {
  /* Validate the source string; calculate size */
  char *dest;
  /* malloc() destination string */
  memcpy(dest, src,
    #ifdef PLATFORM1
      12
    #else
      24
    #endif
  );
  /* ... */
}
```
