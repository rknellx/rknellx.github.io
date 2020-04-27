<h1>Compiling Hydra with SMB2 Support</h1>

<p>While attempting to use Hydra against a HTB system, I discovered Hydra 9.0 did not support SMB2.</p>
<br>
<h3>In order to get SMB2 support, perform the following steps:</h3>
<ol>
  <li> git clone https://github.com/vanhauser-thc/thc-hydra.git</li>
  <li> run ./configure </li>
</ol>

Ensure you have downloaded as many of the following packages as you can, according to the Hydra compilation instructions:
```
apt-get install libssl-dev libssh-dev libidn11-dev libpcre3-dev \
                 libgtk2.0-dev libmysqlclient-dev libpq-dev libsvn-dev \
                 firebird-dev libmemcached-dev libgpg-error-dev \
                 libgcrypt11-dev libgcrypt20-dev
 ```
                 
For Debian based systems, such as Kali, some packages may not be accessible. I did not install libmysqlclient-dev, but I did locate the package libgcryp11-dev package here: https://packages.debian.org/stretch/libgcrypt11-dev

To install the missing package for SMB2 support, run:
```sudo apt install libsmbclient-dev```

<br>
Keep running ./configure to verify your libraries are installed before running make.

<h3 id="theres-a-horizontal-rule-below-this">Your output should be similar to the following:</h3>
<hr />
```
$ ./configure

Starting hydra auto configuration ...
Detected 64 Bit Linux OS

Checking for zlib (libz.so, zlib.h) ...
                                        ... found
Checking for openssl (libssl, libcrypto, ssl.h, sha.h) ...
                                                       ... found
Checking for gcrypt (libgcrypt.so, gpg-error.h) ...
                                        ... found
Checking for idn (libidn.so) ...
                             ... found
Checking for curses (libcurses.so / term.h) ...
                                            ... found, color output enabled
Checking for pcre (libpcre.so, pcre.h) ...
                                       ... found
Checking for Postgres (libpq.so, libpq-fe.h) ...
                                             ... found
Checking for SVN (libsvn_client-1 libapr-1.so libaprutil-1.so) ...
                                                               ... found
Checking for firebird (libfbclient.so) ...
                                       ... found
Checking for MYSQL client (libmysqlclient.so, math.h) ...
                                                      ... NOT found, module Mysql will not support version > 4.x
Checking for AFP (libafpclient.so) ...
                                   ... NOT found, module Apple Filing Protocol disabled - Apple sucks anyway
Checking for NCP (libncp.so / nwcalls.h) ...
                                         ... NOT found, module NCP disabled
Checking for SAP/R3 (librfc/saprfc.h) ...
                                      ... NOT found, module sapr3 disabled
Get it from http://www.sap.com/solutions/netweaver/linux/eval/index.asp
Checking for libssh (libssh/libssh.h) ...
                                      ... found
Checking for Oracle (libocci.so libclntsh.so / oci.h and libaio.so / liboci.a and oci.dll) ...
                                                                    ... NOT found, module Oracle disabled
Get basic and sdk package from http://www.oracle.com/technetwork/database/features/instant-client/index.html
Checking for Memcached (libmemcached.so, memcached.h) ...
                                             ... found                                                                                                                                                       
Checking for Freerdp2 (libfreerdp2.so, freerdp/*.h, libwinpr2.so, winpr/*.h) ...                                                                                                                             
                                             ... found                                                                                                                                                       
Checking for Mongodb (libmongoc-1.0.so, mongoc.h, libbson-1.0.so, bson.h) ...                                                                                                                                
                                             ... found                                                                                                                                                       
Checking for smbclient (libsmbclient.so, libsmbclient.h) ...                                                                                                                                                 
                                             ... found                                                                                                                                                       
Checking for GUI req's (pkg-config, gtk+-2.0) ...                                                                                                                                                            
                                              ... NOT found, optional anyway                                                                                                                                 
Checking for Android specialities ...                                                                                                                                                                        
                                  ... strrchr() found                                                                                                                                                        
                                  ... RSA_generate_key() found                                                                                                                                               
Checking for secure compile option support in gcc ...                                                                                                                                                        
                                                  Compiling... yes                                                                                                                                           
                                                  Linking... yes                                                                                                                                             
                                                                                                                                                                                                             
Hydra will be installed into .../bin of: /usr/local                                                                                                                                                          
  (change this by running ./configure --prefix=path)    
```  
 <hr /> 
<br>

Next, run

```
make
sudo make install
```

<h2>Running Hydra with SMB2</h2>
```
/tools/thc-hydra/hydra -L users.txt -P pass.txt -v <ip> smb2
```
