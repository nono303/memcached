# Memcached - Windows Cygwin binaries #
- https://github.com/memcached/memcached
- https://github.com/nono303/win-build-scripts
---
### Get the good version
:bangbang: **Libevent**  

There is currently a runtime issue using libevent **2.1** (Cygwin build) on old Windows versions : `_WIN32_WINNT <= 0X601`  
> `*** fatal error - couldn't dynamically determine load address for 'QueryUnbiasedInterruptTime' (handle 0x7FEFD430000), Win32 error 127`  
*see https://gitter.im/msys2/msys2?at=5ce7e6578f019114aeab45c0*  

So, I provide memcached with both libevent versions:  
- `2.0.22` <= Windows 7 & **cygwin x64** `3.4.10`
- `2.1.12` > Windows 7 & **cygwin x64** `3.5.1`

*Don't hesitate to test both of them on your system and give me some feedback because I didn't find a lot of topics on it!*

:warning: **AVX / AVX2**  or not (**SSE2**)

- Check your cpu supported instructions with [CPU-Z](https://www.cpuid.com/softwares/cpu-z.html)

  >  ![](https://github.com/nono303/PHP-memcache-dll/raw/master/avx.png)

:fast_forward: **TLS support**

- Ff you need tls support, just choose `*-tls.exe` version

----

### Release

  > _:warning: Only **x64 libevent 2.1** is maintained_  
  > *Older versions `1.4.25. 1.4.33 1.4.35 1.4.36 1.4.39 1.5 1.5.1 1.5.2 1.5.3` are available under **tag memcache-1.5.3**...*

  - **x64**
    - **1.6.26**: libevent `2.1.12` ​_2024-04-07_
    - **1.6.24**: libevent `2.0.22` _2024-02-29_ 

  - **x86**
    - **1.6.21**: libevent `2.1.12` _2023-07-03_
    - **1.6.21**: libevent `2.0.22` _2023-07-23_

-----
### Exec Dependencies

 **x64**

 - **:point_up: cygwin** `3.X.X`
   - *cygwin1.dll*
 - :point_up:  **libevent** `2.X.Y` 
   - *cygevent_core-2-X-Y.dll*
   - *cygevent_extra-2-X-Y.dll*
   - *cygevent_openssl-2-X-Y.dll*
   - *cygevent_pthreads-2-X-Y.dll*
   - *cygevent-2-X-Y.dll*

:warning: for **TLS** only
  - **openssl** `1.1.1w`
    - *cygssl-1.1.dll*
    - *cygcrypto-1.1.dll*
  - **zlib** `1.3.1`
    - *cygz.dll*  

 **x86**

- **cygwin** `3.3.6`
  - *cygwin1.dll*
  
 - :point_up:  **libevent** `2.X.Y` 
   - *cygevent_core-2-X-Y.dll*
   - *cygevent_extra-2-X-Y.dll*
   - *cygevent_openssl-2-X-Y.dll*
   - *cygevent_pthreads-2-X-Y.dll*
   - *cygevent-2-X-Y.dll*

:warning: for **TLS** only
  - **openssl** `1.1.1s`
    - *cygssl-1.1.dll*
    - *cygcrypto-1.1.dll*
  - **zlib** `1.2.13`
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
