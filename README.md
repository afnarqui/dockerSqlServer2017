# dockerSqlServer2017
install docker with sql server 2017

exec command

docker run -it --name volumes -v c:/Users/afnarqui/proyectos:/local busybox

docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=quintero1." -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1439:1433 --volumes-from volumes -v c:/users/afnarqui/proyectos:/c --name SQLDOCKER -d microsoft/mssql-server-linux

docker exec -it SQLDOCKER bash
apt-get update
apt-get install sudo
sudo apt-get install python-pip python-dev build-essential
sudo pip install --upgrade pip 
sudo pip install --upgrade virtualenv 
pip install mssql-cli
mssql-cli
create database prueba
 use prueba
 create table persona(id int identity, nombre varchar(80))
insert into persona(nombre)values('andres naranjo')
select id,nombre from persona
docker commit -m "creo imagen con sqlserver" SQLDOCKER
docker tag a7d3 afnarqui/sqlserver
Docker push afnarqui/sqlserver
docker run -it --name developerv --link=SQLDOCKER:sql --volumes-from volumes -v c:/users/afnarqui/proyectos:/c -p 8100:8100 -p 4001:4001 -p 1434:1433 -p 3000:3000 ubuntu bash

