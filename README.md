# SQL-SERVER
 Teste de requisições utilizando a linguagem SQL.

# Create
 Script de criação do DataBase.

```Code

CREATE DATABASE [Curso]
GO

USE [Curso]
GO

CREATE TABLE [Student]
(

    [Id]  uniqueidentifier NOT NULL,
    [Name]  NVARCHAR(120) NOT NULL,
    [Email]  NVARCHAR(180) NOT NULL,
    [Document]  NVARCHAR(20) NULL,
    [Phone] NVARCHAR(20) NULL,
    [Birthdate] DATETIME NULL,
    [Createdate] DATETIME NOT NULL DEFAULT(GETDATE()),
    CONSTRAINT [PK_Student] PRIMARY KEY ([Id])
);
GO

CREATE TABLE [Author]
(

    [Id]  uniqueidentifier NOT NULL,
    [Name]  NVARCHAR(80) NOT NULL,
    [Title]  NVARCHAR(80) NOT NULL,
    [Image]  NVARCHAR(1024) NOT NULL,
    [Bio] NVARCHAR(2000) NOT NULL,
    [Url] NVARCHAR(450) NULL,
    [Email] NVARCHAR(180) NOT NULL,
    [Type] TINYINT NOT NULL,
    CONSTRAINT [PK_Author] PRIMARY KEY ([Id])

);
GO

CREATE TABLE [Career]
(

    [Id]  uniqueidentifier NOT NULL,
    [Summary]  NVARCHAR(2000) NOT NULL,
    [Title]  NVARCHAR(80) NOT NULL,
    [DurationInMinute]  INT  NOT NULL,
    [Active] BIT NOT NULL,
    [Url] NVARCHAR(450) NULL,
    [Feature] BIT NOT NULL,
    [Tags] NVARCHAR(160) NOT NULL,
    CONSTRAINT [PK_Career] PRIMARY KEY ([Id])

);
GO

CREATE TABLE [Category]
(

    [Id]  uniqueidentifier NOT NULL,
    [Summary]  NVARCHAR(2000) NOT NULL,
    [Title]  NVARCHAR(80) NOT NULL,
    [Order]  INT  NOT NULL,
    [Description] TEXT NOT NULL,
    [Url] NVARCHAR(450) NULL,
    [Feature] BIT NOT NULL,   
    CONSTRAINT [PK_Category] PRIMARY KEY ([Id])

);
GO

CREATE TABLE [Course]
(

    [Id]  uniqueidentifier NOT NULL,
    [Summary]  NVARCHAR(2000) NOT NULL,
    [Title]  NVARCHAR(80) NOT NULL,
    [DurationInMinute]  INT  NOT NULL,
    [Active] BIT NOT NULL,
    [Url] NVARCHAR(450) NULL,
    [Feature] BIT NOT NULL,
    [Tags] NVARCHAR(160) NOT NULL,
    [Tag] NVARCHAR(20) NOT NULL,
    [Level] TINYINT NOT NULL,
    [DurationInMinutes] INT NOT NULL,
    [CreateDate] DATETIME NOT NULL,
    [UpdateDate] DATETIME NOT NULL,
    [Free] BIT NOT NULL,
    [AuthorId] UNIQUEIDENTIFIER NOT NULL,
    [CategoryId] UNIQUEIDENTIFIER  NOT NULL,
    CONSTRAINT [PK_Course] PRIMARY KEY ([Id]),
    CONSTRAINT [FK_Course_Author_AuthorId] FOREIGN KEY ([AuthorId]) REFERENCES [Author] ([Id]),
    CONSTRAINT [FK_Course_Category_CategoryId] FOREIGN KEY ([CategoryId]) REFERENCES [Category] ([Id]) 
    
);
GO

CREATE TABLE [CareerItem]
(

    [CareerId]  uniqueidentifier NOT NULL,
    [CourseId]  uniqueidentifier NOT NULL,
    [Title]  NVARCHAR(160) NOT NULL,
    
    [Description] TEXT  NOT NULL,
    [Order] TINYINT  NOT NULL,
    CONSTRAINT [PK_CareerItem] PRIMARY KEY ([CareerId], [CourseId]),
    CONSTRAINT [FK_CareerItem_Career_CareerId] FOREIGN KEY ([CareerId]) REFERENCES [Career] ([Id]),
    CONSTRAINT [FK_CareerItem_Course_CourseId] FOREIGN KEY ([CourseId]) REFERENCES [Course] ([Id]) 
    
);
GO

CREATE TABLE [StudentCourse]
(

    [CourseId]  uniqueidentifier NOT NULL,
    [StudentId]  uniqueidentifier NOT NULL,
    [Progress]  TINYINT NOT NULL,
    [Favorite] BIT NOT NULL,
    [StartDate] DATETIME NOT NULL,
    [LastUpdateDate] DATETIME NOT NULL,
    CONSTRAINT [PK_StudentCourse] PRIMARY KEY ([CourseId], [StudentId]),
    CONSTRAINT [FK_StudentCourse_Student_StudentId] FOREIGN KEY ([StudentId]) REFERENCES [Student] ([Id]),
    CONSTRAINT [FK_StudentCourse_Course_CourseId] FOREIGN KEY ([CourseId]) REFERENCES [Course] ([Id]) 
    
);
GO
```
# INSERT 
 Script para selecionar a tabela e inserir dados(Neste caso foi utilizado tabela Author e Student como exemplo).
```Code
SELECT  *  FROM  [Author]

INSERT INTO 
    [Author]
VALUES(
    '79b82071-80a8-4e78-a79c-92c8cd1fd052',
    'Ian César Silva Nascimento',
    'Fundamentos de SQL Server',
    '',
    '',
    '',
    'emailteste@cursosqlserver.com',
    10
)        

SELECT * FROM [Student]

INSERT INTO 
    [Student]
VALUES(
    '5f5a33f8-4ff3-7e10-cc6e-3fa000000000',
    'Aluno Teste',
    'hello@alunoteste.com',
    'CPF0123456789',
    '55719874561230',
    '1990-01-01 00:59',
    GETDATE()
)

```
# Utilização
 Importe o arquivo bacpac na sua plataforma de execução do banco de dados e execute.
