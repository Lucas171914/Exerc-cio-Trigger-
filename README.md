# Exerc-cio-Trigger-
é um objeto de banco de dados que é usado para
automatizar a execução de ações específicas em resposta a eventos ou ações que ocorrem
em um banco de dados.


Create table Pedidos ( 
ID PEDIDO INT AUTO_INCREMENT PRIMARY KEY, 
DATAPEDIDO DATETIME,
NomeCliente varchar(100) 
);
 
INSERT INTO Pedidos (DataPedido, NomeCliente) VALUES 
(NOW(), 'Cliente 1') 

DELIMITER $ 
CREATE TRIGGER RegistrodataCriacaoPedido
BEFORE INSERT ON Pedidos
FOR EACH ROW 
BEGIN SET NEW.DataPedido = NOW();
END:
$ 
DELIMITER ; 

INSERT INTO Pedidos (nomeCliente) VALUES ('Novo Cliente'); 
SELECT * FROM Pedidos; 



o trigger faz com que filmes inseridos em uma minutagem não seja aceitos.


create database Filmes;

create table Filmes ( 
Id Int primary key auto_increment,
titulo varchar(60),
minutos Int 
);
delimiter $ 

create trigger chk_minutos before insert on Filmes
for each row
begin 
  if new.minutos < 0 then 
      set new.minutos = null;
      end if;
      end$
      delimiter; 

Insert into Filmes (titulo,minutos) Values ("The terrible trigger", 120);
Insert into Filmes (titulo,minutos) Values ("O Alto da compadecida", 135);
Insert into Filmes (titulo,minutos) Values ("Faroeste caboclo", 240);
Insert into Filmes (titulo,minutos) Values ("The matrix" , 90);
Insert into Filmes (titulo,minutos) Values ("Blade runner", -88);
Insert into Filmes (titulo,minutos) Values ("O labirinto do fauno", 110);
Insert into Filmes (titulo,minutos) Values ("Metropole" , 0);
Insert into Filmes (titulo,minutos) Values ("A lista" , 120);




create trigger chk minutos before insert on FIlmes
for each row 
begin 
 if new.minutos < 0 then 

signal sqlstate '45000' 
set MESSAGE_TEXT = "valor invalido para minutos",
MYSQL_ERRNO = 2022

end if;
end$

delimiter;



create table Log_deletions (
id  int   primary key  auto_increment,
titulo varchar(60),
quando datetime,
quem Varchar(40)
);

delimiter $
create trigger log_deletions after delete on Filmes
for each row
begin 
   inser into Log_deletions values (null,old.titulo, sysdate(), user())); 
end$
delimiter


delete from FIlmes where id = 2;
delete from Filmes where id = 4; 

select * from Log deletions; 
