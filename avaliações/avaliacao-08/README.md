Microsoft Windows [versão 10.0.22621.2715]
(c) Microsoft Corporation. Todos os direitos reservados.

C:\Users\Alunos>mkdir avaliacao08

C:\Users\Alunos>cd avaliacao08

C:\Users\Alunos\avaliacao08>avaliacao8.db
'avaliacao8.db' não é reconhecido como um comando interno
ou externo, um programa operável ou um arquivo em lotes.

C:\Users\Alunos\avaliacao08>sqlite3 avaliacao8.db
SQLite version 3.38.2 2022-03-26 13:51:10
Enter ".help" for usage hints.
sqlite> create table TB_IF (id int primary key autoincrement, nome_if text, ano int, semestre int)
   ...> create table TB_IF (id int primary key autoincrement, nome_if text, ano int, semestre int)
   ...> ;
Parse error: AUTOINCREMENT is only allowed on an INTEGER PRIMARY KEY
sqlite> create table TB_IF (id integer primary key autoincrement, nome_if text, ano int, semestre int);
sqlite> .tables
TB_IF
sqlite> create table TB_CAMPUS (id int primary key autoincrement, nome text, foreign key(if_id) references TB_IF(id));
Parse error: AUTOINCREMENT is only allowed on an INTEGER PRIMARY KEY
sqlite> create table TB_CAMPUS (id integer primary key autoincrement, nome text, foreign key(if_id) references TB_IF(id));
Parse error: unknown column "if_id" in foreign key definition
sqlite> create table TB_CAMPUS (id integer primary key autoincrement, nome text, if_id int, foreign key(if_id) references TB_IF(id));
sqlite> create table TB_CURSOS (id integer primary key autoincrement, nome text, campus_id int, foreign key(campus_id) references TB_CAMPUS(id));
sqlite> create table TB_LABORATORIO (id integer primary key autoincrement, nome text, responsavel_email text, foreign key(curso_id) references TB_CURSOS(id));
Parse error: unknown column "curso_id" in foreign key definition
sqlite> create table TB_LABORATORIO (id integer primary key autoincrement, nome text, responsavel_email text curso_id int, foreign key(curso_id) references TB_CURSOS(id));
Parse error: unknown column "curso_id" in foreign key definition
sqlite> create table TB_LABORATORIO (id integer primary key autoincrement, nome text, responsavel_email text, curso_id int, foreign key(curso_id) references TB_CURSOS(id));
sqlite> create table TB_PROFESSOR (id integer primary key autoincrement, nome text, email text, celular text);
sqlite> create table TB_BOLSISTA (id integer primary key autoincrement, nome text, email text, celular text);
sqlite> create table TB_PROJETO (id integer primary key autoincrement, nome text, inicio date, termino date, laboratorio_id int, professor_id int, foreign key(laboratorio_id) references TB_LABORATORIO(id), foreign key (professor_id) references TB_PROFESSOR (id));
sqlite> create table TB_FAIXAHORARIA (id integer primary key autoincrement, E_Turno ENUM ('MANHÃ', 'TARDE', 'NOITE'), E_Faixa_Horaria ENUM('A_ PRIMEIRO','B_SEGUNDO','C_TERCEIRO','D_QUARTO', 'E_QUINTO'));
Parse error: near "'MANHÃ'": syntax error
   integer primary key autoincrement, E_Turno ENUM ('MANHÃ', 'TARDE', 'NOITE'),
                                      error here ---^
sqlite> create table TB_FAIXAHORARIA (id integer primary key autoincrement, E_Turno ENUM ('MANHA', 'TARDE', 'NOITE'), E_Faixa_Horaria ENUM('A_ PRIMEIRO','B_SEGUNDO','C_TERCEIRO','D_QUARTO', 'E_QUINTO'));
Parse error: near "'MANHA'": syntax error
   integer primary key autoincrement, E_Turno ENUM ('MANHA', 'TARDE', 'NOITE'),
                                      error here ---^
sqlite> create table TB_FAIXAHORARIA (id integer primary key autoincrement,CHECK (E_Turno IN ('MANHÃ', 'TARDE', 'NOITE')), CHECK(E_Faixa_Horaria IN ('A_ PRIMEIRO','B_SEGUNDO','C_TERCEIRO','D_QUARTO', 'E_QUINTO')));
Parse error: no such column: E_Turno
  ARIA (id integer primary key autoincrement,CHECK (E_Turno IN ('MANHÃ', 'TARDE
                                      error here ---^
sqlite> create table TB_FAIXAHORARIA (id integer primary key autoincrement,E_Turno text, CHECK (E_Turno IN ('MANHÃ', 'TARDE', 'NOITE')),E_Faixa_Horaria text, CHECK(E_Faixa_Horaria IN ('A_ PRIMEIRO','B_SEGUNDO','C_TERCEIRO','D_QUARTO', 'E_QUINTO')));
Parse error: near "E_Faixa_Horaria": syntax error
  , CHECK (E_Turno IN ('MANHÃ', 'TARDE', 'NOITE')),E_Faixa_Horaria text, CHECK(
                                      error here ---^
sqlite> CREATE TABLE SuaTabela (
   ...>     id INTEGER PRIMARY KEY AUTOINCREMENT,
   ...>     E_Turno VARCHAR(10),
   ...>     CHECK (E_Turno IN ('MANHÃ', 'TARDE', 'NOITE'))
   ...> );
sqlite> drop table SuaTabela;
sqlite> .tables
TB_BOLSISTA     TB_CURSOS       TB_LABORATORIO  TB_PROJETO
TB_CAMPUS       TB_IF           TB_PROFESSOR
sqlite> create table TB_FAIXAHORARIA (id integer primary key autoincrement,E_Turno text CHECK (E_Turno IN ('MANHÃ', 'TARDE', 'NOITE')),E_Faixa_Horaria text CHECK(E_Faixa_Horaria IN ('A_ PRIMEIRO','B_SEGUNDO','C_TERCEIRO','D_QUARTO', 'E_QUINTO')));
sqlite> create table TB_HORARIO_PLANEJADO(id integer primary key autoincrement, ano int, semestre int, dia int, bolsista_id int, foreign key (bolsista_id) references TB_BOLSISTA(id), faixa_horaria_id int, foreign key (faixa_horaria_id) references TB_FAIXAHORARIA(id));
Parse error: near "faixa_horaria_id": syntax error
  ign key (bolsista_id) references TB_BOLSISTA(id), faixa_horaria_id int, foreig
                                      error here ---^
sqlite> create table TB_HORARIO_PLANEJADO(id integer primary key autoincrement, ano int, semestre int, dia int, bolsista_id int,faixa_horaria_id int, foreign key (bolsista_id) references TB_BOLSISTA(id), foreign key (faixa_horaria_id) references TB_FAIXAHORARIA(id));
sqlite> create table TB_FREQUENCIA(id integer primary key autoincrement, data date, E_Frequencia_Valida text CHECK (E_Frequencia_Valida IN ('SIM', 'NAO')),bolsista_id, projeto_id int, professor_id, horario_planejado_id, foreign key (bolsista_id) references TB_BOLSISTA(id),foreign key (projeto_id) references TB_PROJETO(id),foreign key (professor_id) references TB_PRJETO(id), foreign key (horario_planejado_id) references TB_HORARIO_PLANEJADO(id));
sqlite>
