PY-EMAIL-MONITOR 
=================
O py-send-email, é um sistema escrito em [PYTHON](https://www.python.org/), 
responsavel por enviar um e-mail contendo uma [TABLE](https://www.w3schools.com/html/html_tables.asp) 
em sentido vertircal e ou horizontal com dados inseridos em uma tabela vertical(indentificador + chave + coluna) 
num banco PostgreSQL CLOUD [ElephantSQL(AWS)](https://www.elephantsql.com/about_us.html).

O processo sedá da seguinte forma: Em cada cliente que recebe este sistema, é executado o arquivo "py_auditit.py".
Este arquivo, tem a finalidade de acessar o banco host do cliente, coletar os dados e os enviar ao banco online o 
resultado de cada consulta. Apenas na empresa que analisa esses dados, decorrente de cada cliente seu, é que usamos 
o arquivo "py_email.py", que faz o acesso ao banco online coleta e renderiza as informações as incluindo via TAGs HTMLs
no corpo do e-mail a ser recebido.


TECNOLOGIAS APLICADAS
---------------------
Ambiente de Programação: [Linux](https://br-linux.org/)

Linguagem de programação: [PYTHON](https://www.python.org/).

Ambiente virtualizado em: [VIRTUALENV](https://virtualenv.pypa.io/en/latest/).

PostgreSQL-CLOUD: [ElephantSQL(AWS)](https://www.elephantsql.com/about_us.html).

Plataforma de Imagens e Vídeos: [Cloudnay](https://cloudinary.com/)


CONTRIBUIÇÃO 
------------

[Trabin Software & Consulting](http://www.trabin.com.br/)


PROGRAMADOR RESPONSÁVEL
------------

* Marcos André Gerard Alves [E-MAIL](lgerardlucas@gmail.com) - [LINKEDIN](https://www.linkedin.com/in/marcos-andre-gerard-alves-b071211b/)


INSTALAÇÃO PARA DESENVOLVEDORES
------------
* GIT
    * $ apt install git

* VIRTUALENV 
    * $ python -m virtualenv myvenv

* PIP
    * $ pip install -r requirements.txt 

* PYTHON
    * $ py_database.py - Responsável por estabelecer comunicação e excutar instruções SQL em um ou mais bancos HOSTs e ou ONLINE
    * $ py_auditit.py - Responsável por coletar via instruições SQL enviadas ao módulo "py_database.py" ou comandos SYSTEM, 
                        dados a serem enviados para o banco de monitoramento online. Este arquivo fica em cada emrpesa a ser
                        monitorada, acessando o banco local e ou sistema operacional.
    * $ py_email.py - Módulo responsável por acessar o banco online e renderizar via HTML no corpo do email os dados 
                    coletados e enviados ao banco online pelo módulo "py_auditit.py". Este arquivo, deve ser instalado na empresa
                    que analisa os dados, com isto, instalado uma vez só em um único local
    * $ py_config.py - Módulo que retorna a todos os outros módulos configurações que se encontram no arquivo "conf.ini"

* CONFIGURAÇÃO
    * $ conf.ini - Este arquivo é responsável pelas informações necessárias para o acesso ao banco online, host e também, 
                   as configurações referente ao e-mail a ser usado para o envio do resultado das coletas de dados. 


INSTALAÇÃO NO CLIENTE
------------
* Local
    * mkdir /opt/py-audit-0   -- Pasta para instalar no servidor produção
    * mkdir /opt/py-audit-1   -- Pasta para instalar no servidor contingencia
    * mkdir /opt/py-audit-2   -- Pasta para instalar no servidor contingencia
* GIT
    * $ git clone https://github.com/lgerardlucas/py-send-email.git 

* LINUX
    * apt install python3 python-dev python3-dev
    * apt install python-psycopg2
    * apt install git.

* CONF.INI
    * Neste arquivo, configure somente o acesso ao banco online e host

EXECUTAR O SISTEMA
------------------
* Para alimentaro banco onine - Rodar em todas as empresas auditadas
    * python caminho do projeto/py_auditit.py    
    * Exemplo para uma gendamento no linux sem virtaulenv e com virtuaenv
      Sem = 00 21 * * * root python /opt/py-audit-0/py-send-email/py_auditit.py
      Com = 00 21 * * * root /opt/py-audit-0/py-send-email/myvenv/bin/python3 /opt/py-audit-0/py-send-email/py_auditit.py

* Para envio do e-mail com os dados do banco online - Rodar somente na empresa auditora
    * python caminho do projeto/py_email.py    
    * Exemplo para uma gendamento no linux com e sem virtualenv
      Sem = 00 21 * * * root python /opt/py-audit-0/py-send-email/py_email.py
      Com = 00 21 * * * root /opt/py-audit-0/py-send-email/myvenv/bin/python3 /opt/py-audit-0/py-send-email/py_email.py

* (Opcional) - Para atualização do sistema no cliente, antes do processo de auditoria.  
    * Exexmplo para uma gendamento no linux 
      00 09 * * * root sh /opt/py-audit-0/py-send-email/git_pull.sh

