# Memcached - Windows Cygwin binaries #
- https://github.com/memcached/memcached
----
### version [1.6.15](https://github.com/memcached/memcached/tree/1.6.15)

> 2022-03-30 - commit
>
> 2022-07-17 - build

  - cygwin version `3.3.5`
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

 - **cygwin** `3.3.5`
   - *cygwin1.dll*
 - :point_up:  **libevent** `2.X.Y` 
   - *cygevent_core-2-X-Y.dll*
   - *cygevent_extra-2-X-Y.dll*
   - *cygevent_openssl-2-X-Y.dll*
   - *cygevent_pthreads-2-X-Y.dll*
   - *cygevent-2-X-Y.dll*

:warning: for **TLS** only
  - **openssl** `1.1.1q`
    - *cygssl-1.1.dll*
    - *cygcrypto-1.1.dll*
  - **zlib** `1.2.12`
    - *cygz.dll*  

:warning: for **x86 TLS** only
  - **libgcc** `11.3.0`
    - *cyggcc_s-1.dll*

----

### Install as a Windows service

`-d install` is not anymore available. You might use `nssm` to install memcached as a Windows service:

1. copy [nssm-2.25.0.exe corresponding to your system arch](https://github.com/nono303/memcached/tree/master/nssm) in memcached folder or somwhere in a Windows `%PATH%` folder

2. run theses command - **changing absolute path `C:\memcached`** corresponding to your config

   ```
   nssm-2.25.0.exe install memcached C:\memcached\memcached-avx.exe
   nssm-2.25.0.exe set memcached AppParameters "-vv -m 512 -I 256m"
   nssm-2.25.0.exe set memcached AppDirectory C:\memcached
   nssm-2.25.0.exe set memcached AppExit Default Restart
   nssm-2.25.0.exe set memcached AppNoConsole 1
   nssm-2.25.0.exe set memcached AppPriority ABOVE_NORMAL_PRIORITY_CLASS
   nssm-2.25.0.exe set memcached AppStderr C:\memcached\logs\memcached.log
   nssm-2.25.0.exe set memcached AppStopMethodSkip 6
   nssm-2.25.0.exe set memcached AppTimestampLog 1
   nssm-2.25.0.exe set memcached DisplayName memcached
   nssm-2.25.0.exe set memcached ObjectName LocalSystem
   nssm-2.25.0.exe set memcached Start SERVICE_AUTO_START
   nssm-2.25.0.exe set memcached Type SERVICE_WIN32_OWN_PROCESS
   ```

----
> *Older versions `1.4.25. 1.4.33 1.4.35 1.4.36 1.4.39 1.5 1.5.1 1.5.2 1.5.3` are available under **tag memcache-1.5.3**...*