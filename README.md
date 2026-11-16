-- Questão 04
SELECT evento_id, capacidade, CASE WHEN capacidade < 10 THEN 'Evento pequeno' WHEN capacidade BETWEEN 10 AND 12 THEN 'Evento médio' WHEN capacidade > 12 THEN 'Evento grande' END AS classificacao FROM evento;

-- Questão 05
SELECT p.nome, i.data_inscricao, pag.valor FROM participante p JOIN inscricao i ON p.participante_id = i.participante_id JOIN pagamento pag ON i.inscricao_id = pag.inscricao_id WHERE pag.status_pagamento = 'PENDENTE';

-- Questão 06
SELECT le.nome AS nome_local, COUNT(i.inscricao_id) AS total_inscricoes FROM local_evento le JOIN evento e ON le.local_id = e.local_id LEFT JOIN inscricao i ON e.evento_id = i.evento_id GROUP BY le.local_id, le.nome HAVING COUNT(i.inscricao_id) > 0 ORDER BY total_inscricoes DESC, nome_local ASC;

-- Questão 07
SELECT p.nome, pag.valor FROM participante p JOIN inscricao i ON p.participante_id = i.participante_id JOIN pagamento pag ON i.inscricao_id = pag.inscricao_id WHERE pag.valor > (SELECT AVG(valor) FROM pagamento);

-- Questão 08
SELECT e.titulo AS titulo_evento, o.nome AS nome_organizador, COUNT(i.inscricao_id) AS total_confirmadas FROM evento e JOIN organizador o ON e.organizador_id = o.organizador_id JOIN inscricao i ON e.evento_id = i.evento_id WHERE e.status_evento = 'ENCERRADO' AND i.status_inscricao = 'CONFIRMADA' GROUP BY e.evento_id, e.titulo, o.nome HAVING COUNT(i.inscricao_id) >= 2 ORDER BY total_confirmadas DESC, titulo_evento -- Questão 01
CREATE TABLE palestrante (palestrante_id INT NOT NULL AUTO_INCREMENT, nome VARCHAR(100) NOT NULL, email VARCHAR(100), area_atuacao VARCHAR(100), PRIMARY KEY (palestrante_id));
CREATE TABLE evento_palestrante (evento_id INT NOT NULL, palestrante_id INT NOT NULL, tema_palestra VARCHAR(150) NOT NULL, data_palestra DATE NOT NULL, duracao_minutos INT NOT NULL, PRIMARY KEY (evento_id, palestrante_id), CONSTRAINT fk_ep_evento FOREIGN KEY (evento_id) REFERENCES evento (evento_id), CONSTRAINT fk_ep_palestrante FOREIGN KEY (palestrante_id) REFERENCES palestrante (palestrante_id));

-- Questão 02
INSERT INTO palestrante (nome, email, area_atuacao) VALUES ('Marcelo Vasconcelos', 'marcelo.vasconcelos@gmail.com', 'Investimento e Capital de Risco'), ('Patricia Lemos', 'patricia.lemos@outlook.com', 'Inteligência Artificial'), ('Renato Figueiredo', 'renato.figueiredo@gmail.com', 'Marketing Digital e Growth');
INSERT INTO evento_palestrante (evento_id, palestrante_id, tema_palestra, data_palestra, duracao_minutos) VALUES (4, 1, 'Como captar a primeira rodada de investimento', '2026-11-20', 45), (4, 2, 'IA aplicada a startups em estágio inicial', '2026-11-20', 60), (4, 3, 'Métricas que importam: do MVP à escala', '2026-11-20', 30);

-- Questão 03
SELECT e.titulo AS titulo_evento, p.nome AS nome_palestrante, p.area_atuacao, ep.tema_palestra, ep.data_palestra, ep.duracao_minutos FROM evento_palestrante ep JOIN evento e ON ep.evento_id = e.evento_id JOIN palestrante p ON ep.palestrante_id = p.palestrante_id WHERE e.titulo = 'Feira de Startups' ORDER BY p.nome ASC;

-- Questão 04
SELECT evento_id, capacidade, CASE WHEN capacidade < 10 THEN 'Evento pequeno' WHEN capacidade BETWEEN 10 AND 12 THEN 'Evento médio' WHEN capacidade > 12 THEN 'Evento grande' END AS classificacao FROM evento;

-- Questão 05
SELECT p.nome, i.data_inscricao, pag.valor FROM participante p JOIN inscricao i ON p.participante_id = i.participante_id JOIN pagamento pag ON i.inscricao_id = pag.inscricao_id WHERE pag.status_pagamento = 'PENDENTE';

-- Questão 06
SELECT le.nome AS nome_local, COUNT(i.inscricao_id) AS total_inscricoes FROM local_evento le JOIN evento e ON le.local_id = e.local_id LEFT JOIN inscricao i ON e.evento_id = i.evento_id GROUP BY le.local_id, le.nome HAVING COUNT(i.inscricao_id) > 0 ORDER BY total_inscricoes DESC, nome_local ASC;

-- Questão 07
SELECT p.nome, pag.valor FROM participante p JOIN inscricao i ON p.participante_id = i.participante_id JOIN pagamento pag ON i.inscricao_id = pag.inscricao_id WHERE pag.valor > (SELECT AVG(valor) FROM pagamento);

-- Questão 08
SELECT e.titulo AS titulo_evento, o.nome AS nome_organizador, COUNT(i.inscricao_id) AS total_confirmadas FROM evento e JOIN organizador o ON e.organizador_id = o.organizador_id JOIN inscricao i ON e.evento_id = i.evento_id WHERE e.status_evento = 'ENCERRADO' AND i.status_inscricao = 'CONFIRMADA' GROUP BY e.evento_id, e.titulo, o.nome HAVING COUNT(i.inscricao_id) >= 2 ORDER BY total_confirmadas DESC, titulo_evento ASC;





-- Questão 01
CREATE TABLE palestrante (palestrante_id INT NOT NULL AUTO_INCREMENT, nome VARCHAR(100) NOT NULL, email VARCHAR(100), area_atuacao VARCHAR(100), PRIMARY KEY (palestrante_id));
CREATE TABLE evento_palestrante (evento_id INT NOT NULL, palestrante_id INT NOT NULL, tema_palestra VARCHAR(150) NOT NULL, data_palestra DATE NOT NULL, duracao_minutos INT NOT NULL, PRIMARY KEY (evento_id, palestrante_id), CONSTRAINT fk_ep_evento FOREIGN KEY (evento_id) REFERENCES evento (evento_id), CONSTRAINT fk_ep_palestrante FOREIGN KEY (palestrante_id) REFERENCES palestrante (palestrante_id));

-- Questão 02
INSERT INTO palestrante (nome, email, area_atuacao) VALUES ('Marcelo Vasconcelos', 'marcelo.vasconcelos@gmail.com', 'Investimento e Capital de Risco'), ('Patricia Lemos', 'patricia.lemos@outlook.com', 'Inteligência Artificial'), ('Renato Figueiredo', 'renato.figueiredo@gmail.com', 'Marketing Digital e Growth');
INSERT INTO evento_palestrante (evento_id, palestrante_id, tema_palestra, data_palestra, duracao_minutos) VALUES (4, 1, 'Como captar a primeira rodada de investimento', '2026-11-20', 45), (4, 2, 'IA aplicada a startups em estágio inicial', '2026-11-20', 60), (4, 3, 'Métricas que importam: do MVP à escala', '2026-11-20', 30);

-- Questão 03
SELECT e.titulo AS titulo_evento, p.nome AS nome_palestrante, p.area_atuacao, ep.tema_palestra, ep.data_palestra, ep.duracao_minutos FROM evento_palestrante ep JOIN evento e ON ep.evento_id = e.evento_id JOIN palestrante p ON ep.palestrante_id = p.palestrante_id WHERE e.titulo = 'Feira de Startups' ORDER BY p.nome ASC;

-- Questão 04
SELECT evento_id, capacidade, CASE WHEN capacidade < 10 THEN 'Evento pequeno' WHEN capacidade BETWEEN 10 AND 12 THEN 'Evento médio' WHEN capacidade > 12 THEN 'Evento grande' END AS classificacao FROM evento;

-- Questão 05
SELECT p.nome, i.data_inscricao, pag.valor FROM participante p JOIN inscricao i ON p.participante_id = i.participante_id JOIN pagamento pag ON i.inscricao_id = pag.inscricao_id WHERE pag.status_pagamento = 'PENDENTE';

-- Questão 06
SELECT le.nome AS nome_local, COUNT(i.inscricao_id) AS total_inscricoes FROM local_evento le JOIN evento e ON le.local_id = e.local_id LEFT JOIN inscricao i ON e.evento_id = i.evento_id GROUP BY le.local_id, le.nome HAVING COUNT(i.inscricao_id) > 0 ORDER BY total_inscricoes DESC, nome_local ASC;

-- Questão 07
SELECT p.nome, pag.valor FROM participante p JOIN inscricao i ON p.participante_id = i.participante_id JOIN pagamento pag ON i.inscricao_id = pag.inscricao_id WHERE pag.valor > (SELECT AVG(valor) FROM pagamento);

-- Questão 08
SELECT e.titulo AS titulo_evento, o.nome AS nome_organizador, COUNT(i.inscricao_id) AS total_confirmadas FROM evento e JOIN organizador o ON e.organizador_id = o.organizador_id JOIN inscricao i ON e.evento_id = i.evento_id WHERE e.status_evento = 'ENCERRADO' AND i.status_inscricao = 'CONFIRMADA' GROUP BY e.evento_id, e.titulo, o.nome HAVING COUNT(i.inscricao_id) >= 2 ORDER BY total_confirmadas DESC, titulo_evento ASC;

