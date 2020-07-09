# PostgreSQL Study
## Instalação do PostgreSQL no CentOS 7
```cli
sudo yum -y install https://download.postgresql.org/pub/repos/yum/10/redhat/rhel-7-x86_64/pgdg-centos10-10-2.noarch.rpm
sudo yum -y install postgresql10 postgresql10-devel postgresql10-contrib postgresql10-libs postgresql10-test postgresql10-server postgresql10-docs
sudo systemctl enable postgresql-10
sudo /usr/pgsql-10/bin/postgresql-10-setup initdb
sudo systemctl start postgresql-10
sudo systemctl status postgresql-10
sudo su - postgres
-bash-4.2$ psql
```
## Utilizando o Docker
```cli
docker pull postgres
docker run -p 5432:5432 postgres
```

## Group by time example

```sql
select
  date_trunc('minute', created_at), -- or hour, day, week, month, year
  count(1)
from users
group by 1
```

## Last sessions action example

```sql
SELECT DISTINCT ON (session_uuid) 
    session_uuid,
    session_action,
    user_uuid,
    created_at
FROM
    sessions s
ORDER BY 
    session_uuid, created_at DESC ;

```

# Example try_cast function
```sql
create function try_cast_int(p_in text, p_default int default null)
   returns int
as
$$
begin
  begin
    return $1::int;
  exception 
    when others then
       return p_default;
  end;
end;
$$
language plpgsql;

--example
select try_cast_int('999'), try_cast_int('xpto', -1000), try_cast_int('xxxx')
```

# Example data random
```sql
create table t_random as select s, md5(random()::text) from generate_Series(1,3000000) s;
EXPLAIN ANALYZE select try_cast_int(tr.md5, 1) from t_random tr;

```
