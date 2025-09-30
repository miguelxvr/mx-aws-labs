
## Lançar instâncias de VM a partir de imagens AMIs

1. Criar uma imagem (AMI) da VM configurada na [etapa anterior](https://github.com/mvneves/Flask-AWS-Example/wiki/Cria%C3%A7%C3%A3o-de-buckets-para-armazenamento-escal%C3%A1vel-no-S3#parte-4-utilizar-o-servi%C3%A7o-s3-via-python). Para isso, clique com o botão direito sobre instância no serviço EC2 e escolha a opção Image and templates > Create image.
2. Lançar duas instâncias de máquina virtual (uma em cada zona de disponibilidade) a partir da imagem criada
    1. Acessar a opção IMAGES > AMIs no menu lateral do serviço EC2
    2. Selecionar a imagem criada e clicar no botão Launch
    3. Escolher a instância do tipo t2.micro (Free tier eligible) e clicar no botão Next
    4. Selecionar uma Subnet em uma zona de disponibilidade diferente (ex: us-east-1a, us-east-1b, etc.) para cada VM criada
3. Testar o acesso ao serviço em cada VM criada via browser do computador local.

http://[ip-publico-vm]:8080

## Configurar um balanceador de cargas para usar as múltiplas VMs

1. Criar "Target Group" (através do menu LOAD BALANCING > Target Groups) e adicionar as duas instâncias criadas;
    1. Escolher o "target type" do tipo Instances
    2. Definir um no qualquer
    3. Configurar o procolo HTTP com porta 8080 e cliar em Next
    4. Na próxima tela, selecionar todas as instâncias da lista e clicar no botão "Include as pending bellow"
    5. Por fim, cliar em "Create target group"

2. Criar um balanceador de cargas (através do menu LOAD BALANCING > Load Balancers) e adicionar o target group criado no passo anterior:
    1. Escolher o tipo Application Load Balancer
    2. Definir um nome qualquer para o balanceador de cargas
    3. Configurar um Listener para o procolo HTTP e porta 8080
    4. Selecionar todas as zonas de disponibilidade e clicar em Next e Next novamente
    5. Selecionar o mesmo security group usado na criação das VMs e clicar em Next
    6. Selecionar o target group criado anteriormente e configurar a porta como 8080
3. Testar o balanceador de cargas pelo browser usando nome (DNS name) do balanceador recém criado (ex: meuLoadbalancer-1745797999.us-east-1.elb.amazonaws.com);

http://[dns-name-elb]:8080

Obs: o balanceador pode demorar alguns minutos para ser provisionado. Verifique se o estado está como active antes de executar o teste.

## Configurar a resolução de nomes no Route 53

Obs: essa etapa não é possível no ambiente do AWS Educate, pois o serviço Route 53 não é disponibilizado.

1. Acessar o serviço Route 53 (necessário ter um dominio registrado)
2. Adicionar o endereço (DNS name) do balanceador de cargas criado em um novo registro DNS
3. Testar acessando o nome via browser da máquina local
