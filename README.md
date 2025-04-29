# ExercicioFinalProg
'''
DROP TABLE IF EXISTS matriculas, alunos, cursos;

CREATE TABLE alunos (
  id SERIAL PRIMARY KEY,
  nome TEXT NOT NULL,
  turma TEXT NOT NULL,
  curso TEXT NOT NULL,
  data_nascimento DATE
);

CREATE TABLE cursos (
  id SERIAL PRIMARY KEY,
  nome TEXT NOT NULL,
  duracao_anos INT
);

CREATE TABLE matriculas (
  id SERIAL PRIMARY KEY,
  aluno_id INT REFERENCES alunos(id) ON DELETE CASCADE,
  curso_id INT REFERENCES cursos(id) ON DELETE CASCADE,
  data_matricula DATE DEFAULT CURRENT_DATE
);

-- Inserindo os dados dos alunos
INSERT INTO alunos (nome, turma, curso, data_nascimento)
VALUES 
  ('Pedro Jorge', '18', 'adm', '2007-03-22'),
  ('Raya', '15', 'RJ', '2002-11-14'),
  ('Pedro', '16', 'CC', '2003-12-10'),
  ('Tony', '13', 'adm', '2005-11-10'),
  ('Vulgo', '19', 'RJ', '2005-10-11'),
  ('Jow', '10', 'CC', '2007-09-20'),
  ('Piol', '13', 'CC', '2006-07-21'),
  ('Bigode', '18', 'EC', '2003-08-10'),
  ('Erika', '16', 'EC', '2008-07-15'),
  ('Os D', '17', 'CC', '2000-02-17');

-- Inserindo os dados dos cursos
INSERT INTO cursos (nome, duracao_anos)
VALUES
  ('adm', 4),
  ('CC', 3),
  ('RJ', 5),
  ('EC', 3);

-- Inserindo as matrículas (associando os alunos aos cursos)
-- Precisamos garantir que o ID do curso está correto. Vamos assumir:
-- adm = 1, CC = 2, RJ = 3, EC = 4
INSERT INTO matriculas (aluno_id, curso_id)
VALUES
  (1, 1),  -- Pedro Jorge → adm
  (2, 3),  -- Raya → RJ
  (3, 2),  -- Pedro → CC
  (4, 1),  -- Tony → adm
  (5, 3),  -- Vulgo → RJ
  (6, 2),  -- Jow → CC
  (7, 2),  -- Piol → CC
  (8, 4),  -- Bigode → EC
  (9, 4),  -- Erika → EC
  (10, 2); -- Os D → CC

-- Consulta com JOIN para listar alunos e seus cursos
SELECT a.nome AS aluno, c.nome AS curso, m.data_matricula
FROM matriculas m
JOIN alunos a ON m.aluno_id = a.id
JOIN cursos c ON m.curso_id = c.id;
'''
