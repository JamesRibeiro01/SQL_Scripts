# SQL_Scripts


EXEC sp_configure 'show advanced options', 1
RECONFIGURE


EXEC sp_configure 'xp_cmdshell', 1

RECONFIGURE


CREATE TABLE tblgetFileList
(
   id integer identity(1,1),
   nome varchar(max)
);

CREATE TABLE teste
(
   nome varchar(max)
);

INSERT INTO tblgetFileList 
EXEC xp_cmdshell 'dir /B "C:#diretorio_dos_arquivos"';

--select * from tblgetFileList
--where nome is not null;


DECLARE @nome_arquivo VARCHAR(MAX);
DECLARE @COUNT INTEGER = 1;

while @COUNT <= (SELECT COUNT(*) FROM tblgetFileList WHERE nome is not null)
BEGIN
     set @nome_arquivo = (SELECT NOME FROM tblgetFileList WHERE id = @COUNT);
	 insert into teste values('D:\DIRETORIO_TESTE\PASTA\'+@nome_arquivo);
	SET @COUNT = @COUNT + 1;
end;

EXEC sp_configure 'show advanced options', 1
RECONFIGURE

EXEC sp_configure 'xp_cmdshell', 0
RECONFIGURE
