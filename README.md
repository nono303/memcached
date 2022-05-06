# Memcached - Windows Cygwin binaries #
- https://github.com/memcached/memcached
----
2022-04-05

> **version [1.6.15](https://github.com/memcached/memcached/tree/1.6.15)**

  - cygwin version `3.3.4`
  - gcc version `11.3.0`

**Released versions**

  - **x86 & x64**
  - **[AVX](https://msdn.microsoft.com/fr-fr/library/jj620901.aspx)**
  - **TLS**

---

:bangbang: **Libevent**  

There is currently a runtime issue using libevent **2.1** (Cygwin build) on old Windows versions : `_WIN32_WINNT <= 0X601`  
> `*** fatal error - couldn't dynamically determine load address for 'QueryUnbiasedInterruptTime' (handle 0x7FEFD430000), Win32 error 127`  
*see https://gitter.im/msys2/msys2?at=5ce7e6578f019114aeab45c0*  

So, I provide memcached with both libvent versions:  
- `2.0.5` <= Windows 7  
- `2.1.7` > Windows 7  

*Don't hesitate to test both of them on your system and give me some feedback because I didn't find a lot of topics on it!*

-----
**Build Scripts** 

- [@nono303/win-build-scripts](https://github.com/nono303/win-build-scripts)

**Exec Dependencies**

 - **cygwin** `3.3.4`
   - *cygwin1.dll*
 - :point_up:  **libevent** `2.X.Y` 
   - *cygevent_core-2-X-Y.dll*
   - *cygevent_extra-2-X-Y.dll*
   - *cygevent_openssl-2-X-Y.dll*
   - *cygevent_pthreads-2-X-Y.dll*
   - *cygevent-2-X-Y.dll*

:warning: for **TLS** only
  - **openssl** `1.1.1n`
    - *cygssl-1.1.dll*
    - *cygcrypto-1.1.dll*
  - **zlib** `1.2.12`
    - *cygz.dll*  

:warning: for **x86 TLS** only
  - **libgcc** `11.3.0`
    - *cyggcc_s-1.dll*
----
> *Older versions `1.4.25. 1.4.33 1.4.35 1.4.36 1.4.39 1.5 1.5.1 1.5.2 1.5.3` are available under **tag memcache-1.5.3**...*