->  ArchServerCalidus is a free and open-source MMORPG server emulator written in C++. It is a fork of the ARCHLORD Server project episode 1 ready to be updated up to episode 3. To connect to the server, you can use celestia alefclient.exe or episode 3 Awakening alefclient.exe(no mobs,npc textures,and inventory trash doesnt work yet - in order to make them to work we need to change packets in it as the ceelestia alefclient.exe has them).

Getting Started

You will need :
Choose an OS and install it :Windows xp SP3 , Windows Server 2003 R2 , Windows server 2008 R2 , Windows 7 x32/x64 bits.
Install Navicat Premium - you will need to point OCI.dll to navicat to succeed connection to the database(Use Navicat:
Specify in Tools => Options => OCI => Oci library: C:\oracle\ora92\bin\oci.dll).
For other oracle version in my opinion i will use ORACLE SQL DEVELOPER database viewer and editor has more options to work with the database.
Java JDK (It installs automatically JRE)
Visual C++ redistributable 2008 x86
Visual C++ redistributable 2010 x86
Visual C++ Express 2010(you will not need net framework anymore version 4)
Install ORACLE 9i R2 (alternatives oracle 10G R2 , 11G R2 , etc) see https://www.youtube.com/watch?v=k7nZH61doHE&feature=youtu.be (use the tutorial , only the part with installation of oracle 9iR2)
Open SQL+ and log in with(this kind of installation its available only for oracle 9i R2) :
After that you will need the updated serverfiles from this GIT(put them wherever you want).


Username: system
Password: password
Host: account

create user calidus IDENTIFIED BY password;

-- Grant/Revoke role privileges
grant connect to calidus;
grant resource to calidus;

-- Grant/Revoke system privileges
grant alter session to calidus;
grant create cluster to calidus;
grant create database link to calidus;
grant create sequence to calidus;
grant create session to calidus;
grant create synonym to calidus;
grant create table to calidus;
grant create view to calidus;
grant dba to calidus;

After grant remember to restore database and procedures tables with the following command(put the SQL folder in Local Disk C to succeed restoring the database) :

@c:\sql\account.sql;
@C:\RPGWT.sql;
@C:\SERVERCONFIG.sql;
exit;    <---- SQL plus will close now after this command

After this you can connect to the database now with the following username and password using navicat:

Username: calidus
Password: password
SID: account


Edit the serverconfig table :
At the WORLD tab give for each line your server name (ex:Bruhmart) , then change your ip.
Then DBUSER + LOGDBUSER attribute is calidus
     sections, DBPWD + LOGDBPWD attribute is password
     sections, DBDSN + LOGDBDSN attribute is account
     
Edit the RPGWT table:
Change in the WORLD tab the name of server you used in serverconfig(ex:Bruhmart).


Next step we will need to edit a file of oracle:

C: \ oracle \ ora92 \ network \ admin \ tnsnames.ora.


# TNSNAMES.ORA Network Configuration File: D: \ oracle \ ora92 \ NETWORK \ ADMIN \ tnsnames.ora
# Generated by Oracle configuration tools.
ACCOUNT =
(DESCRIPTION =
(ADDRESS_LIST =
(ADDRESS = (PROTOCOL = TCP) (HOST = 127.0.0.1) (PORT = 1521))
)
(CONNECT_DATA =
(SERVICE_NAME = account)
)
)

DON'T FORGET TO ERASE DEDICATED SERVER LINE ! (Not on Windows XP)

For INST1_HTTP specify host for 127.0.0.1 ! In TNSNAMES.ORA also.   )

Now edit the serverfiles connection configuration in CFG folder for DB.ini and DBSVRINFO.ini

Changed INI/DatabaseInit/DB.ini (user: calidus, password is password, SID is account)
Changed INI/DatabaseInit/DBSVRINFO.ini (user: calidus, password is password, SID is account)


Now you will be able to start ArchSvrLogin,ArchSvrRelay,ArchSvrWorld.Wait 1 minute and server needs to be online.

To create an account go to navicat database to the AMT_ACCOUNT table and insert for username "leona" and for password "rivola"
To be able to connect next time after first login you will need to add the next line in AMT_MASTER :

     COLUMN -> (ACCOUNTID,EMAIL,SOCIALNO,CREATION_DATE,LAST_DATE, MODIFY_DATE,PHONE,MOBILE,ZIPCODE,ADDR1,ADDR2,SMS_Y N,EMAIL_YN,PENALTY_GBN,PAUSE_DATE,IP,LOGINCNT,NOMI NATOR,RPG_LEVEL,LONEY_AGREEYN,LONEY_CHARGEYN,SEX)
COLUMN DATA -> ('leona','leona@mail.com','18',to_timestamp('26/01/11','DD/MM/RR HH24:MI:SSXFF'),to_timestamp('26/01/11','DD/MM/RR HH24:MI:SSXFF'),to_timestamp('26/01/11','DD/MM/RR HH24:MI:SSXFF'),null,null,null,null,null,'N','N',' 0',null,null,null,null,null,null,null,null);

To be able to connect in game you will need to create a *txt file with this : " alefclient.exe /L192.168.1.xxx:11002 "  and save it.(192.168.1.xxx this is the local ip -> change with yours ip idk 164.54.33.1  or what ip you got)
Rename the  extension *txt file in *bat and launch the game by using it.


Have fun!


REMEMBER!
If you wanted to do a public server remember to make port forward if you had a router with the following ports UDP/TCP:11000,11002,11004,11008,4277,1521,1575,4443,4444,7777,7778,8080(if its not open yet).


©Credits: Alex,Mike0505 ∞,Feldunost, special thanks to Osiy1996(has contributing with interesting stuff that help us to continue developing).