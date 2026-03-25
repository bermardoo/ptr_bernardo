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

<sub>Imagem 1 - Topologia feita no PNetLab</sub>

### Endereçamento

|Dispositivo|Interface|IP|Máscara|
|---|---|---|---|
|Host A|eth0|192.168.10.10|/24|
|Switch|eth0|192.168.10.1|/24|
|Switch|eth1|192.168.20.1|/24|
|Host B|eth0|192.168.20.10|/24|

## Procedimentos
1. Após inserir os dispositivos de rede no PNetLab, configuramos o ip nos hosts e no switch L3. Depois de fazermos as configurações, testamos um ping entre um host e o gateway e entre o host e o outro. Os resultados dessa parte serão demonstrados na próxima sessão (Imagens 2 e 3), mas o resultado foi como esperado: entre os pcs não houve comunicação e entre o pc e o gateway funcionou.

2. Após isso ser feito, configuramos rotas para que os pcs consigam pingar entre si (Imagem 4).

3. Após esse ping funcionar, gerei as tabelas de roteamento em cada dispositivo (Imagens 5, 6 e 7).

***

## Resultados e evidências
Nesta sessão vamos mostrar as imagens dos terminais de cada dispositivo, indicando o que cada imagem é e mantendo a nomenclatura dada na sessão **Procedimentos**.


<img width="769" height="800" alt="image" src="https://github.com/user-attachments/assets/efe2dfc0-e705-4fbf-bbcf-9ddb1d7406e2" />

<sub>Imagem 2 - Configuração do Host B e os testes de ping iniciais</sub>


<img width="936" height="936" alt="image" src="https://github.com/user-attachments/assets/d98d67ae-b9fa-4d8c-984c-09f9f9eed83b" />

<sub>Imagem 3 - Configuração do Host A e os testes de ping iniciais</sub>


<img width="913" height="251" alt="image" src="https://github.com/user-attachments/assets/e0b92fbe-0186-48a0-9d5d-cc6562f53289" />

<sub>Imagem 4 - Ping entre o Host B e Host A após configurar a rota</sub>


<img width="1125" height="621" alt="image" src="https://github.com/user-attachments/assets/2abf2044-b859-47c0-a4c1-e76105c3e4a1" />

<sub>Imagem 5 - Tabela de roteamento no Switch L3</sub>


<img width="1118" height="621" alt="image" src="https://github.com/user-attachments/assets/6d952794-476e-4f71-b456-5119172c5320" />

<sub>Imagem 6 - Tabela de IP no Host A</sub>


<img width="1123" height="621" alt="image" src="https://github.com/user-attachments/assets/336c3ff1-92be-46c8-8332-3e28b758ef5d" />

<sub>Imagem 7 - Tabela de IP no Host B</sub>


## Análise técnica

A análise dos resultados obtidos nas etapas de teste e configuração nos permite compreender o comportamento do roteamento entre redes distintas.

1.  **Comunicação Inicial e Falha de Roteamento (Imagens 2 e 3):**
    * As Imagens 2 (Host B) e 3 (Host A) mostram que a configuração de IP e máscara (`/24`) foi realizada com sucesso em ambos os hosts.
    * O teste de ping para o respectivo gateway (Switch L3) funcionou em ambos os hosts: Host A (192.168.10.10) pingou 192.168.10.1, e Host B (192.168.20.10) pingou 192.168.20.1. Isso confirma que a conectividade de Camada 2 (física e enlace) entre o host e o switch estava operacional.
    * No entanto, o ping entre os hosts (Host B tentando pingar Host A na Imagem 2, e vice-versa na Imagem 3) falhou, resultando em "GateWay not found". Isso ocorreu porque, embora o switch L3 conhecesse as duas redes por estarem diretamente conectadas (ver **Tabela de Endereçamento**), os **hosts** não tinham uma rota configurada para alcançar a rede "vizinha". Um host, por padrão, só sabe se comunicar com dispositivos na sua própria sub-rede. Para alcançar qualquer rede externa, ele precisa de uma rota padrão (Default Gateway).

2.  **Configuração do Gateway e Sucesso no Ping (Imagem 4):**
    * Para resolver a falha de comunicação, foi necessário configurar o gateway padrão nos hosts. No PNetLab, usando VPCS, isso foi feito com o comando `ip 192.168.10.10/24 192.168.10.1` (no Host A, por exemplo), onde o último IP é o gateway.
    * A Imagem 4 mostra o resultado após essa configuração: o Host B (192.168.20.10) conseguiu pingar com sucesso o Host A (192.168.10.10). Isso demonstra que o Host B enviou o pacote para o seu gateway (192.168.20.1 no Switch). O switch, agindo como roteador, consultou sua tabela de roteamento, encontrou a rede 192.168.10.0/24 como diretamente conectada na interface e0/0 e encaminhou o pacote para o Host A. O Host A, agora também com gateway configurado, pôde responder ao Host B pelo mesmo caminho inverso.

3.  **Análise das Tabelas de Roteamento (Imagens 5, 6 e 7):**
    * **Switch L3 (Imagem 5):** A tabela de roteamento do switch (comando `show ip route`) é a mais completa. Ela mostra o código 'C' (Connected) para ambas as redes: `192.168.10.0/24` via interface Ethernet0/0 e `192.168.20.0/24` via Ethernet0/1. Como ambas as redes estão diretamente conectadas ao switch e as interfaces estão 'up', o switch já sabe como rotear entre elas sem a necessidade de rotas estáticas adicionais.
    * **Host A (Imagem 6) e Host B (Imagem 7):** Nos hosts VPCS (comando `show ip`), vemos uma tabela de roteamento simplificada. No Host A, observamos a rota para a rede local (via eth0) e uma "gateway" definida como `192.168.10.1`. No Host B, o gateway é `192.168.20.1`. Essa configuração de gateway é o que permite ao host enviar pacotes para qualquer IP que não pertença à sua rede local (ex: o IP do outro host).

## Conclusão

Este experimento permitiu validar de forma prática os conceitos fundamentais de roteamento IP e interconexão de redes. Podemos notar que:

* **Necessidade de Roteamento:** Demonstrou-se que redes IP distintas (192.168.10.0 e 192.168.20.0) não se comunicam sem um dispositivo de Camada 3 (roteador ou switch L3) para interconectá-las.
* **Papel do Gateway:** O papel crítico do gateway padrão nos hosts foi evidenciado. Sem o gateway configurado, o host não sabe como enviar pacotes para fora de sua rede local, resultando em falha de comunicação mesmo que a infraestrutura física esteja operacional. A configuração correta do gateway habilitou a comunicação ponta-a-ponta.
* **Tabela de Roteamento:** A análise das tabelas de roteamento no switch e nos hosts permitiu visualizar como o switch L3 utiliza suas rotas diretamente conectadas para encaminhar tráfego entre sub-redes distintas e como os hosts dependem da rota padrão para acessar redes externas.

O uso do PNetLab proporcionou um ambiente de emulação realista, permitindo configurar dispositivos Cisco IOL e hosts VPCS de forma idêntica a um cenário real, consolidando o entendimento teórico sobre roteamento.
