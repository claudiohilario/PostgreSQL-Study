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
