# memcached cygwin builds x86 & x64 
## standalone runtime
####  - gcc version 7.4.0
####  - cygwin1.dll version 3.0.0
####  - cygevent.dll version 2.0.5

## PATCH memcached.c
### 1.4.25

    5087c5087
    <             if (('0' <= (unsigned char)ever[2] && (unsigned char)ever[2] < '3') && !isdigit((unsigned char)ever[3])) {
    ---
    >             if (('0' <= ever[2] && ever[2] < '3') && !isdigit(ever[3])) {

### 1.4.33

    322c322
    <                    fprintf(stderr, "idle timeout thread sleeping for %ldus\n",
    ---
    >                    fprintf(stderr, "idle timeout thread sleeping for d%us\n",

### 1.4.35

    322c322
    <                    fprintf(stderr, "idle timeout thread sleeping for %ldus\n",
    ---
    >                    fprintf(stderr, "idle timeout thread sleeping for %ulus\n",

### 1.4.36

    328c328
    <                    fprintf(stderr, "idle timeout thread sleeping for %ldus\n",
    ---
    >                    fprintf(stderr, "idle timeout thread sleeping for %ulus\n", 