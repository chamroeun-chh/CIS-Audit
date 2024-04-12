
# 1. Installation and patches 
```
# whoami  
# dnf repolist all | grep -E 'enabled$' 
# whoami  
# rpm -qa | grep postgres 
# whoami  
# dnf info $(rpm -qa|grep postgres) | grep -E '^Name|^Version|^From' 
# whoami  
# PGSETUP_INITDB_OPTIONS="-k" /usr/pgsql-16/bin/postgresql-16-setup initdb 
# whoami  
# ls -la ~postgres/16 
# whoami  
# /usr/pgsql-16/bin/postgresql-16-check-db-dir ~postgres/16/data 
# echo $?
```
# 2 Directory and File Permissions
```
# whoami  
# su - postgres                             
# whoami  
# umask 
```
# 3 Logging And Auditing
```
# show log_destination;
# show logging_collector;
# show log_directory;
# show log_filename;
# show log_file_mode;
# show log_truncate_on_rotation;
# show log_rotation_age;
# show log_rotation_size;
# show syslog_facility;
# show syslog_sequence_numbers;
# show syslog_split_messages;
# show syslog_ident;
# show log_min_messages;
# show log_min_error_statement;
# show debug_print_parse;
# show debug_print_rewritten;
# show debug_print_plan;
# show debug_pretty_print;
# show log_connections;
# show log_disconnections;
# show log_error_verbosity;
# show log_hostname;
# show log_line_prefix;
# show log_statement;
# show log_timezone;
# show shared_preload_libraries;
# show pgaudit.log;
```

# 4 User Access and Authorization
```
# whoami  
# groups 
# sudo -iu postgres 
# whoami  
# groups  
# sudo -iu postgres 
# whoami
# whoami  
# psql -c "\du+ postgres"
# whoami  
# psql -c "\du+ appuser" 
# whoami  
# psql -c "\du+ *" 
# psql -c "select * from pg_user order by usename" 
# whoami  
# sudo -iu postgres 
# psql -c "SELECT nspname, proname, proargtypes, prosecdef, rolname, proconfig FROM pg_proc p 
# -- display all users defined in the cluster postgres=
# \x 
# \du+ * 
# \x 
# \dt+ *.*            
# select t.tablename, u.usename,        has_table_privilege(u.usename, t.tablename, 'select') 
# SELECT oid, relname, relrowsecurity FROM pg_class WHERE relrowsecurity IS TRUE;
# SELECT oid, relname, relrowsecurity FROM pg_class WHERE relname = 'passwd';
# select * from pg_available_extensions where name = 'set_user';
# SELECT rolname FROM pg_authid WHERE rolsuper and rolcanlogin;
# whoami  
# psql
# select rolname from pg_roles where rolsuper is true;
# whoami 
# psql postgres
# su - user1 
# whoami  
# psql -U postgres -d postgres 
# su - user2 
# whoami  
# psql -U postgres -d postgres 
# psql -U user1 -d postgres 
# psql -U user2 -d postgres  
```
# 5 Connection and Login
```
# SHOW shared_preload_libraries;
# SHOW dynamic_library_path;
```
# 6 PostgreSQL Settings
```
# SELECT name, setting FROM pg_settings WHERE context IN ('backend','superuser-backend') ORDER BY 1;
# SELECT name, setting FROM pg_settings WHERE context = 'postmaster' ORDER BY 1;
# SELECT name, setting FROM pg_settings WHERE context = 'sighup' ORDER BY 1;
# SELECT name, setting FROM pg_settings WHERE context = 'superuser' ORDER BY 1;
# SELECT name, setting FROM pg_settings WHERE context = 'user' ORDER BY 1;
# fips-mode-setup --check
# openssl version OpenSSL 
# SHOW ssl;
# SELECT name, setting, source FROM pg_settings WHERE name = 'ssl';
```

# 7. Replication 
```
# SELECT * FROM pg_available_extensions WHERE name='pgcrypto';
# select rolname from pg_roles where rolreplication is true;
# show log_replication_commands;
# SELECT name, setting FROM pg_settings WHERE name ~ '^archive' ORDER BY 1;
# SELECT * FROM pg_stat_archiver;
```

# 8 Special Configuration Considerations
```
# select name, setting from pg_settings where (name ~ '_directory$' or name ~ '_tablespace');
# select name, setting from pg_settings where name in ('external_pid_file', 'unix_socket_directories','shared_preload_libraries','dynamic_library_path','local_preload_libraries','session_preload_libraries');
```