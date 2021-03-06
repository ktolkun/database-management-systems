# database-management-systems
## Oracle database config
In project docker is used. In `docker-compose.yml` declared container
`oracle_db` which is built from image `store/oracle/database-enterprise:12.2.0.1`.

To get access to the image you need sign in of docker hub. Then go to page of
the image and accept rules of using image oracle database. Also you need execute
command `docker login` to authorize in docker hub from your pc.

By default oracle database doesn't allow any manipulations with database.
To start work with database, f.ex. create custom table, you need create own user
and grant him special privileges. For it execute following commands:

```sh
docker exec -it oracle_db bash -c "source /home/oracle/.bashrc; cd ~; sqlplus / as sysdba"
```
Then you will be in `sqlplus` console. Execute following sql commands:
```sql
ALTER SESSION SET "_ORACLE_SCRIPT"=TRUE;
CREATE USER USER_NAME IDENTIFIED BY PASSWORD;
GRANT ALL PRIVILEGES TO USER_NAME;
```

Where `USER_NAME` is the name of user and `PASSWORD` is the password of user.
Last row grant all privileges to new user.

## Oracle database connection
To get connection string you need folowing information:
+ Host: `localhost`
+ Port: `1521`
+ SID: `ORCLDB`
+ DRIVER: `Thin`
+ User: `USER_NAME`
+ Password: `PASSWORD`

Result connection string `jdbc:oracle:thin:@localhost:1521:ORCLCDB`.