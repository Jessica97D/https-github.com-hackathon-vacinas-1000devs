Desafio Hackathon 2025 
1 – Objetivo 
Desenvolver um software que permite o gerenciamento das vacinas aplicadas aos integrantes de uma 
família. O software deve permitir a visualização do calendário vacinal por idade recomendada de 
aplicação (em meses), além de permitir o cadastro de quais vacinas foram aplicadas a cada integrante da 
família.  
2 – Expectativa Principal: 
É esperado que os grupos desenvolvam um software que tenha as seguintes características: -  As funcionalidades sejam acessadas através de APIs Restfull, construídas seguindo o exemplo do 
projeto Spark Web trabalhado durante os encontros da academia; -  As funcionalidades do software sejam acessadas através de um cliente API como o Thunder Client. O 
desenvolvimento de uma interface Web fica como uma possibilidade adicional caso o grupo se sinta 
confortável em desenvolver. -  Utilize o paradigma de Orientação à Objetos para representar o paciente, vacina, dose e imunizações; -  Utilize como forma de persistência dos dados o banco de dados mysql; 
3 – Modelo de Dados: 
Diagrama Entidade Relacionamento  
Descrição das Tabelas: 
 
vacina: Armazena o nome das vacinas.  
id Chave primária da tabela. 
vacina Armazena o nome conhecido da vacina. 
descricao Armazena uma breve descrição da vacina. 
limite_aplicacao Armazena o limite de idade em meses de uma pessoa que possa receber a vacina. 
Ou seja, se uma vacina tem limite de eficácia para pessoas com idade até 48 
meses, e uma pessoa já está com 60 meses, esta vacina possivelmente já não tem 
mais eficácia, sendo desnecessário a sua aplicação. Este campo tem 
preenchimento opcional. Caso o valor esteja nulo, significa que a vacina não tem 
limite de idade para aplicação, ou seja, pode ser aplicada em qualquer idade 
mesmo após a idade recomendada. 
publico_alvo 
 
Lista com o nome do público-alvo destinado esta vacina. Trata-se de uma 
enumeração com os possíveis valores: CRIANÇA, ADOLESCENTE, ADULTO, 
GESTANTE 
 
dose: Armazena o nome das doses de uma vacina.  
id Chave primária da tabela. 
id_vacina Chave estrangeira que relaciona com a tabela vacina identificando a 
qual vacina esta dose está relacionada. 
dose Descrição da dose: Exemplo: 1ª Dose, 2ª Dose, Reforço 
idade_recomenda_aplicacao Idade recomendada em meses que uma pessoa deve receber a 
aplicação da vacina.  
Exemplo:  
dose: 1ª Dose 
idade_recomendada_aplicacao: 20  
dose: 2ª Dose 
idade_recomendada_aplicacao: 26  
A interpretação correta é que uma pessoa deve tomar a 1ª dose quando 
tiver com 20 meses de idade e depois tomar a 2ª dose quando estiver 
com 26 meses de idade.  
 
paciente: Armazena os dados dos integrantes da família. 
id Chave primária da tabela. 
nome Nome completo do integrante da família. 
cpf CPF do integrante da família caso seja fornecido. Este campo é opcional não 
sendo obrigatório o preenchimento. 
Sexo Enumeração que descreve o sexo do paciente: Valores possíveis: M – Masculino e 
F - Feminino 
data_nascimento Data de nascimento do paciente. 
 
paciente: Armazena os dados das imunizações recebidas pelos integrantes da família. 
id Chave primária da tabela. 
id_paciente Chave estrangeira da tabela paciente que identifica qual paciente recebeu a 
vacina. 
id_dose Chave estrangeira da tabela dose que identifica qual foi a dose da vacina 
aplicada. 
data_aplicacao Data em que a aplicação da vacina foi efetivamente realizada 
fabricante Nome do fabricante da vacina. Este campo é opcional. 
lote Informação do lote da vacina. Este campo é opcional. 
local_aplicacao Local do estabelecimento onde a vacina foi aplicada. Exemplo: Hospital 
Santa Marta, Posto de Saúde Bairro Centro... Este campo é opcional. 
profissional_aplicador Nome do profissional que fez a aplicação da vacina. Este campo é opcional. 
4 – APIs a serem desenvolvidas 
 
Paciente 
Rota Descrição 
Adicionar Paciente 
Ex: /paciente/inserir 
Endpoint que recebe os dados do paciente e realiza o cadastro no 
banco de dados. Este endpoint deve devolver o código do usuário 
inserido no banco de dados e um status http de sucesso. Em caso de 
erro deve ser retornado uma mensagem informando o ocorrido. 
Alterar Paciente 
Ex: /paciente/alterar/:id 
Endpoint que recebe o id do paciente a ser alterado e os novos dados 
a serem atualizados. Este endpoint deve devolver uma mensagem 
informando se ocorreu sucesso ou não e um status http compatível 
com o resultado da ação. 
Excluir Paciente 
Ex: /paciente/excluir/:id 
Endpoint que recebe o id do paciente a ser excluído e realiza a 
exclusão. Este endpoint deve devolver uma mensagem informando se 
ocorreu sucesso ou não e um status http compatível com o resultado 
da ação. 
Consultar todos os pacientes 
Ex: /paciente/consultar 
Endoint que devolve os dados de todos os pacientes cadastrados. Este 
endpoint deve devolver uma mensagem de erro caso ocorra algum 
problema e um status http compatível com o resultado da ação. 
Consultar paciente por id 
Ex: /paciente/consultar/:id 
Endoint que devolve os dados de um paciente cadastrado com 
determinado id. Este endpoint deve devolver uma mensagem de erro 
caso ocorra algum problema e um status http compatível com o 
resultado da ação. 
 
Imunizações 
Rota Descrição 
Adicionar imunização 
Ex: /imunizacao/inserir 
Endpoint que recebe os dados da imunização e realiza 
o cadastro no banco de dados. Este endpoint deve 
devolver o código da imunização inserido no banco de 
dados e um status http de sucesso. Em caso de erro 
deve ser retornado uma mensagem informando o 
ocorrido. 
Alterar imunização 
Ex: /imunizacao/alterar/:id 
Endpoint que recebe o id da imunização a ser alterado 
e os novos dados a serem atualizados. Este endpoint 
deve devolver uma mensagem informando se ocorreu 
sucesso ou não e um status http compatível com o 
resultado da ação. 
Excluir imunização 
Ex: /imunizacao/excluir/:id 
Endpoint que recebe o id da imunização a ser excluída 
e realiza a exclusão. Este endpoint deve devolver uma 
mensagem informando se ocorreu sucesso ou não e 
um status http compatível com o resultado da ação. 
Excluir todas as imunizações de um 
determinado paciente 
Ex: /imunizacao/excluir/paciente/:id 
Endpoint que recebe o id do paciente e exclui todas as 
imunizações deste paciente. Este endpoint deve 
devolver uma mensagem informando se ocorreu 
sucesso ou não e um status http compatível com o 
resultado da ação. 
Consultar todas as imunizações 
Ex: /imunizacao/consultar 
Endoint que devolve os dados de todos as imunizações 
cadastrados. Este endpoint deve devolver uma 
mensagem de erro caso ocorra algum problema e um 
status http compatível com o resultado da ação. 
Consultar Imunização por id 
Ex: /imunizacao/consultar/:id 
Endoint que devolve os dados de uma imunização 
cadastrada com determinado id. Este endpoint deve 
devolver uma mensagem de erro caso ocorra algum 
problema e um status http compatível com o resultado 
da ação. 
Consultar Imunizações por id do paciente 
Ex: /imunizacao/consultar/paciente/:id 
Endoint que devolve os dados de todas as imunizações 
cadastradas com determinado id de paciente. Este 
endpoint deve devolver uma mensagem de erro caso 
ocorra algum problema e um status http compatível 
com o resultado da ação. 
Consultar Imunizações por id do paciente e 
intervalo de aplicação 
Ex: 
/imunizacao/consultar/paciente/:id/aplicacao 
/:dt_ini/:dt_fim 
Endoint que devolve os dados de todas as imunizações 
cadastradas com determinado id de paciente em um 
determinado período de datas. Este endpoint deve 
devolver uma mensagem de erro caso ocorra algum 
problema e um status http compatível com o resultado 
da ação. 
 
Vacinas 
Rota Descrição 
Consultar todas as vacinas  
Ex: /vacinas/consultar 
Endpoint que retorna todas as vacinas cadastradas. 
Este endpoint deve devolver uma mensagem de 
erro caso ocorra algum problema e um status http 
compatível com o resultado da ação. 
Consultar todas as vacinas para uma 
determinada faixa etária 
Ex: /vacinas/consultar/faixa_etaria/:faixa 
Endoint que devolve os dados de todas as vacinas 
cadastradas para uma determinada faixa etária 
conforme informado em :faixa. Lembre-se que as 
fixas etárias no banco de dados cadastradas são 
essas: CRIANÇA, ADOLESCENTE, ADULTO, 
GESTANTE. Este endpoint deve devolver uma 
mensagem de erro caso ocorra algum problema e 
um status http compatível com o resultado da ação. 
Consultar todas as vacinas recomendadas acima 
de uma idade  
Ex: /vacinas/consultar/idade_maior/:meses  
Endoint que devolve os dados de todas as vacinas 
cadastradas com recomendação de aplicação para 
uma idade em meses acima do valor informado por 
:meses. Este endpoint deve devolver uma 
mensagem de erro caso ocorra algum problema e 
um status http compatível com o resultado da ação. 
 
 
Estatísticas 
Rota Descrição 
Qtde de vacinas aplicadas por paciente 
Ex: /estatisticas/imunizacoes/paciente/:id 
Endpoint que recebe id do paciente e retorna 
apenas o número que representa a quantidade de 
vacinas aplicadas neste paciente. Este endpoint 
deve devolver uma mensagem de erro caso ocorra 
algum problema e um status http compatível com 
o resultado da ação. 
Qtde de vacinas aplicáveis no próximo mês por 
paciente 
Ex: 
/estatisticas/proximas_imunizacoes/paciente/:id 
Endpoint que recebe id do paciente e retorna 
apenas o número que representa a quantidade de 
vacinas que podem ser aplicadas neste paciente 
no próximo mês. Este endpoint deve devolver uma 
mensagem de erro caso ocorra algum problema e 
um status http compatível com o resultado da 
ação. 
Qtde de vacinas atrasadas  
Ex: 
/estatisticas/imunizacoes_atrasadas/paciente/:id 
Endpoint que recebe id do paciente e retorna 
apenas o número que representa a quantidade de 
vacinas que deveriam ter sido aplicadas com base 
na idade do paciente. Este endpoint deve devolver 
uma mensagem de erro caso ocorra algum 
problema e um status http compatível com o 
resultado da ação. 
Qtde de vacinas acima de uma determinda idade  
Ex: 
/estatisticas/imunizacoes/idade_maior/:meses 
Endpoint que devolve a quantidade de vacinas com 
recomendação de aplicação para uma idade em 
meses acima do valor informado por :meses. Este 
endpoint deve devolver uma mensagem de erro 
caso ocorra algum problema e um status http 
compatível com o resultado da ação. 
 
 
 
