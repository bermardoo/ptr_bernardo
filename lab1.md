Disciplina: **ENE0011 – Laboratório de Redes**  
Curso: **Engenharia de Redes de Comunicação**  
Instituição: **Universidade de Brasília (UnB)**  
Departamento: **Engenharia Elétrica** 

Professor Responsável: **Prof. Dr. Laerte Peotta de Melo**

# Relatório do Experimento 1
## Conceitor de Roteamento

## Identificação
- Nome: **Bernardo de Alencar Monteiro**
- Matrícula: **241008460**
- Turma: **1**

## Objetivo
O nosso objetivo nesse laboratório é compreender que redes distintas não se comunicam automaticamente, identificar o papel do roteador ou switch L3 como elemento lógico de interconexão, diferenciar falha de comunicação por ausência de roteamento e de falha física e também relacionarmos a teoria de roteamento com o comportamento real da rede.
  
## Ambiente experimental
No primeiro momento, criamos o arquivo do laboratório no PNetLab e inserimos três nós, dois PC's (escolhi o VPC) e um switch L3 ou roteador (fui com o Cisco IOL). Abaixo está disponível uma imagem da topologia (Imagem 1) e a tabela de endereçamento.

### Topologia

<img width="1071" height="427" alt="image" src="https://github.com/user-attachments/assets/23a5dfb0-c234-4854-8784-3f9c4b3f3d4c" />
Imagem 1 - Topologia feita no PNetLab

### Endereçamento

|Dispositivo|Interface|IP|Máscara|
|---|---|---|---|
|Host A|eth0|192.168.10.10|/24|
|Switch|eth0|192.168.10.1|/24|
|Switch|eth1|192.168.20.1|/24|
|Host B|eth0|192.168.20.10|/24|

## Procedimentos
1. Após inserir os dispositivos de rede no PNetLab, configuramos o ip nos hosts e no switch L3. Depois de fazermos as configurações, testamos um ping entre um host e o gateway e entre o host e o outro. Os resultados dessa parte serão demonstrados na próxima sessão (Imagens 2, 3 e 4), mas o resultado foi como esperado: entre os pcs não houve comunicação e entre o pc e o gateway funcionou.

2. Após isso ser feito, configuramos rotas para que os pcs consigam pingar entre si (Imagem 5).

3. Após esse ping funcionar, gerei as tabelas de roteamento em cada dispositivo (Imagens 6, 7 e 8).

## Resultados e evidências
Nesta sessão vamos mostrar as imagens dos terminais de cada dispositivo, indicando o que cada imagem é e mantendo a nomenclatura dada na sessão **Procedimentos**.



## Análise técnica
(interpretação dos resultados)

## Conclusão
