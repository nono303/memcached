# Memcached - Windows Cygwin binaries #
- https://github.com/memcached/memcached
----
2021-04-01

> **version [1.6.9](https://github.com/memcached/memcached/tree/1.6.9)**

  - cygwin version `3.2.0`
  - gcc version `10.2.0`

**Released versions**

  - **x86 & x64**
  - **[AVX](https://msdn.microsoft.com/fr-fr/library/jj620901.aspx)**
  - **TLS**
-----
**Build Scripts** 

- [@nono303/win-build-scripts](https://github.com/nono303/win-build-scripts)

**Exec Dependencies**
 - **cygwin** `3.2.0`
   - *cygwin1.dll*
 - **libevent** `2.0.22`
   - *cygevent_core-2-0-5.dll*
   - *cygevent_extra-2-0-5.dll*
   - *cygevent_openssl-2-0-5.dll*
   - *cygevent_pthreads-2-0-5.dll*
   - *cygevent-2-0-5.dll*

![](https://placehold.it/15/FFA500/000000?text=+) for **TLS** only
  - **openssl** `1.1.1f`
    - *cygssl-1.1.dll*
    - *cygcrypto-1.1.dll*
  - **zlib** `1.2.11`
    - *cygz.dll*

![](https://placehold.it/15/FFA500/000000?text=+) for **x86 TLS** only
  - **libgcc** `10.2.0`
    - *cyggcc_s-1.dll*
----
> *Older versions `1.4.25. 1.4.33 1.4.35 1.4.36 1.4.39 1.5 1.5.1 1.5.2 1.5.3` are available under **tag memcache-1.5.3**...*