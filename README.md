# cmodular
C modular programming demo

# Example
Below is an example of wrapping c standard memory functions in a modular way.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct Memory {
  void *(*malloc)(size_t size);
  void (*free)(void *ptr);
  void *(*calloc)(size_t nmemb, size_t size);
  void *(*realloc)(void *ptr, size_t size);
}Memory;

static void *Mem_malloc(size_t size) {
  return malloc(size);
}

static void Mem_free(void *ptr) {
  free(ptr);
}

static void *Memcalloc(size_t nmemb, size_t size) {
  return calloc(nemmb, size);
}

static void *Mem_realloc(void *ptr, size_t size) {
  return realloc(ptr, size);
}

Memory iMem = {
  Mem_malloc,
  Mem_free,
  Mem_calloc,
  Mem_realloc
};

int main() {
  char *s;
  s = iMem.malloc(64);
  strcpy(s, "Hello, welcome!");
  printf("s = [%s]\n", s);
  iMem.free(s);
  s = NULL;
  exit(0);
}
```
