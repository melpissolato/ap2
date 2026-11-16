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

