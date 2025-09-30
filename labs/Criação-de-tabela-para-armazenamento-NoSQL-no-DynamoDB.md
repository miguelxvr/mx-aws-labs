
## Criar uma tabela no serviço DynamoDB

1. Entrar na console do AWS;
2. Acessar a opção DynamoDB na lista de serviços;
3. Criar uma nova tabela:
   * Definir um nome qualquer para a tabela;
   * Definir o "Partition key" com o nome "name" no formato String;
   * Definir o "Sort key" com nome "date" no formato Number.

## Utilizar serviço DynamoDB via API Python

1. Conectar via SSH na instância do EC2 criada anteriormente;
2. Entrar no Virtualenv criado anteriormente:
```
source venv/bin/activate
```

3. Clonar repositório e alterar branch para dynamodb:

```
rm -rf Flask-AWS-Example
git clone https://github.com/mvneves/Flask-AWS-Example.git --branch dynamodb
cd Flask-AWS-Example
pip install -r requirements.txt
```

4. Editar os fontes (ver arquivo config.py) para enviar arquivos para o bucket do S3 criado anteriormente e o nome da tabela do DynamoDB récem criada; 
    * Observação: nesse ponto será necessário obter credenciais de acesso para a API do AWS. Para usuário AWS Educate, essas credenciais podem ser obtidas no botão Account Details;

5. Configure as chaves de autenticação da AWS usando variáveis de ambiente conforme abaixo e execute o servidor:

```
export AWS_ACCESS_KEY_ID=""
export AWS_SECRET_ACCESS_KEY=""
export AWS_SESSION_TOKEN=""

export FLASK_APP=app.py
flask run --host=0.0.0.0 --port 8080
```

* Você pode verificar se as chaves estão corretamente registradas com o comando `aws configure list`. Que mostram a `ACCESS_KEY` e a `SECRET_ACCESS_KEY`.

6. Testar o acesso ao serviço via browser do computador local e fazer upload de algumas imagens para popular a tabela:

http://[ip-publico-vm]:8080

Obs: necessário liberar a porta TCP 8080 no Security Group (firewall) da máquina virtual.


7. Entrar novamente na console do serviço DynamoDB e listar o conteúdo da tabela através da opção "Explore table items".

