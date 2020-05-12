# Configurar Ambiente para Projeto Integrador - Curso DevOps - Academia Neon
Preparar um ambiente equalizado para o Projeto Integrador da Academia Neon do Curso DevOps. Como cada uma das integrantes do grupo tinham setups diferentes para realizar o trabalho, optamos por construir um mesmo ambiente para todas. Também percebemos que utilizando o vagrant + virtualbox + vscode além de ficar mais fácil de trabalhar, ficava mais leve que criar uma vm com interface gráfica direto no virtual box.


## Softwares Necessários
Para criação do ambiente, vamos utilizar os seguintes itens: [Vagrant](http://vagrantup.com/) + [VirtualBox](http://virtualbox.org/) + [VSCode](https://code.visualstudio.com/). Antes de mais nada será necessário baixar e instalar cada um deles.


## Setup
1. Realizar o clone desse projeto na sua pasta de trabalho.

2. Abrir o VSCode e via terminal acessar pasta de trabalho.

    * Comandos MacOS - Neste exemplo, a pasta de trabalho é o home do usuário.

        * `$ cd ~/AcademiaNeon_DevOps `

        * `$ pwd `

            Exemplo resultado: /home/user/AcademiaNeon_DevOps 

        * `$ ls AcademiaNeon_DevOps`

            Exemplo resultado: LICENSE       README.md       ansible.cfg         desktop-devops       install_ansible.sh  inventory       playbooks
    
    * Comandos Windows - Neste exemplo, a pasta de trabalho é desktop do usuário
        
        * `PS C:\> cd Users\NomeUsuario\Desktop\AcademiaNeon_DevOps `
        
        * `PS C:\Users\NomeUsuario\Desktop\AcademiaNeon_DevOps> dir `

            Deve listar todas as pastas e aqrquivos como no Linux.     

3. Acessar a pasta desktop-devops. Criar a VM Linux. Acessar via ssh. Setar usuário ubuntu. 
    * Comandos MacOS
        * Acessar a pasta:   
            * `$ cd desktop-devops`

        * Criar/Subir a vm: 
            * `$ vagrant up `

                ![vagrant-up](docs/vagrant-up.png)

        * Validar status vm:
            * `$ vagrant status `   

                ![vagrant-status](docs/vagrant-status.png) 

        * Desligar a VM
            * `$ vagrant suspend `

                ![vagrant-suspend](docs/vagrant-suspend.png)

        * Conectar na VM via ssh
            * `$ vagrant ssh `

                ![vagrant-ssh](docs/vagrant-ssh.png)

                ![vagrant](docs/vagrant.png)

        * Mudar para usuário ubuntu - Veja que nesse item já estamos logados na vm criado pelo arquivo Vagrantfile
            * `vagrant@ubuntu-bionic:~$ sudo su - ubuntu `

                ![sudo_su-ubuntu](docs/sudo_su-ubuntu.png)

    * Comandos Windows
        * Acessar a pasta:   
            * `PS C:\Users\NomeUsuario\Desktop\AcademiaNeon_DevOps> cd desktop-devops`

        * Criar/Subir a vm:
            * `PS C:\Users\NomeUsuario\Desktop\AcademiaNeon_DevOps\desktop-devops> vagrant up `

        * Validar status vm:
            * `PS C:\Users\NomeUsuario\Desktop\AcademiaNeon_DevOps\desktop-devops> vagrant status `

                ![vagrant-status](docs/vagrant-status.png)     

        * Desligar a VM
            * `PS C:\Users\NomeUsuario\Desktop\AcademiaNeon_DevOps\desktop-devops> vagrant suspend `

                ![vagrant-suspend](docs/vagrant-suspend.png)

        * Conectar na VM via ssh
            * `PS C:\Users\NomeUsuario\Desktop\AcademiaNeon_DevOps\desktop-devops> vagrant ssh `

                ![vagrant-ssh](docs/vagrant-ssh.png)

                ![vagrant](docs/vagrant.png)

        * Mudar para usuário ubuntu - Veja que nesse item já estamos logados na vm criado pelo arquivo Vagrantfile
            * `vagrant@ubuntu-bionic:~$ sudo su - ubuntu `

                ![sudo_su-ubuntu](docs/sudo_su-ubuntu.png)


    <b>Importante</b>: Uma vez criada a vm, sempre que desligar, ao precisar utilizar novamente, basta executar o mesmo procedimento.    


## Instalar Ansible
* Efetuar o clone do repositório dentro da vm criada.
    * `$ git clone https://github.com/andresavs/AcademiaNeon_DevOps.git `

        ![git-clone](docs/git-clone.png)

* Executar a instalação do Ansible.
    * `$ bash install_ansible.sh `

* Testar Instalação 
    * `$ ansible --help ` 
    * `$ ansible local -m ping `

* Validar Versão - Ansible 2.9.7 
    * `$ ansible --version `

        ![ansible-version](docs/ansible--version.png)


## Configuração Geral + Configurar Ansible
* Atualizar pacotes linux, instalar programas (java, python, awscli) e suas dependencias. 
    * `$ ansible-playbook playbooks/config-all.yml `

        ![config-all](docs/config-all.png)

* Configurar o Ansible.
    * `$ ansible-playbook playbooks/config-ansible.yml ` 

        ![config-ansible](docs/config-all.png)

* Validar versão do Python 
    * `$ ansible --version `
        
        <b>Importante</b>: O Python precisa estar como 3 ou superior. Caso ainda não esteja é necessário sair do usuário ubuntu (exit) e sair da VM (exit). E logo após fazer a conexão ssh novamente e validar.

        ![validar-python](docs/validando-python.png)

* Validar instalação do AWSCLI
    * `$ aws `

        ![aws](docs/aws.png)


## Instalar Docker
* O docker local não é pré-requisito para o projeto, mas se quiser instalar para utilizar esta vm para estudar, segue orientações.
    * `$ ansible-playbook playbooks/install-docker.yml ` 

* Validar Instalação
    * `$ docker --version `  
    * `$ docker ps ` 

        ![docker](docs/docker.png)

    <b>Importante</b>: Caso o docker ps dê algum erro, sair do usuário ubuntu e da vm. E logo após fazer a conexão ssh e validar, como foi feito para a validação do python.

## Instalar Jenkins
* O Jenkins local também não é pré-requisito para o projeto, mas se quiser instalar para utilizar esta vm para estudar, segue orientações.
    * `$ ansible-playbook playbooks/install-jenkins.yml ` 

* Validar Instalação
    * `$ sudo service jenkins status ` 

        ![jenkins](docs/jenkins.png)

* Comandos Úteis
    * Validar status do serviço Jenkins: `$ sudo service jenkins status ` 
    * Validar iniciar serviço Jenkins: `$ sudo service jenkins start` 
    * Validar parar serviço Jenkins:`$ sudo service jenkins stop ` 


## Configurar AWSCLI
Para ter acesso aos recursos da aws via linha de comando em nosso desktop de trabalho é necessário configurar as credenciais do seu usuário. Caso queira, por favor, seguir os passos descritos abaixo:

 1. Caso não tenha ainda será necessário criar uma conta na [AWS](https://portal.aws.amazon.com/billing/signup#/start). 

      <b>Importante</b>: Após criar a conta, sempre fazer o login com o root user.

 2. Acessar o console da AWS com o user root e ir em:

      * My Security Credentials → Access keys (access key ID and secret access key) → Create New Access Key

      
       <b>Importante</b>: Fazer o download das informações.

 3. Configurar o AWS CLI
    
    Preencher com as keys da AWS. Colocar a região de trabalho (a us-east-1 é a mais economica no momento) e o formato por padrão é json, mas você pode colocar também.

     * `$ aws configure `

       ![aws-configure](docs/aws-configure.png)            

 4. Alguns comandos para testar:
     * `$ aws iam list-access-keys` 
     * `$ aws ec2 describe-regions`


## Dicas 
1. Para resolver problemas de horário entre VM e EC2 efetuar os comandos abaixo, sair do usuário ubuntu e da vm. E logo após fazer a conexão ssh.
    * `$ sudo apt install ntpdate `
    * `$ sudo ntpdate -u pool.ntp.org `


2. Para utilizar o VSCode para atualizar seu repositório que está vm é necessário baixar e instalar um plugin chamado Remote - SSH. 

    <b>Importante</b>: Sempre estar com a vm ligada e conectada via ssh no usuario ubuntu, item 3 do Setup.

    * Primeiro Acesso:
        * Após instalar, conectar na vm com o user ubuntu e apertar F1 no vscode (ou dependendo do computador fn + F1).
            
            ![remote-ssh](docs/f1-remote.png)

        * <b>No primeiro acesso</b> será necessário configurar o host.
            
            ![configure-host](docs/configure-host.png)   
        
        * Ao selecionar o item Configure SSH Hosts...
            
            ![arquivo-conf](docs/arquivo-config.png)

        * Na pasta docs temos dois exemplos de documentos.
            * [Windows](https://github.com/andresavs/AcademiaNeon_DevOps/tree/master/docs/config-windows)
                
            * [MacOS](https://github.com/andresavs/AcademiaNeon_DevOps/tree/master/docs/config-macos)

            <b>Importante</b> : Alterar de acordo com seu sistema operacional e com o local que fez o git clone do repositório para criar a vm, ou seja, onde voê acessa para executar os comandos vagrant.

        * Selecionar o host. 
            Apertar F1 no vscode (ou dependendo do computador fn + F1) e escolher o item 127.0.0.1 ou como você chamou no arquivo config.
            
            ![remote-ssh](docs/f1-remote.png)
            
            ![host](docs/selecionar-host.png)  

        * Uma nova janela do vscode irá abrir e ficará tentando a conexão, <b>no primeiro acesso</b> algumas opções devem aparecer e será necessário selecionar.
            Para Windows escolher Linux e depois Continue, ou apenas continue, caso não apareça. 
            
            ![config-host-adicionais](docs/Linux--Continue.png) 

        * Após conectado nesta nova janela ir em "File → Open..." e escolher seu diretório de trabalho da vm.
            
            ![file](docs/file-open.png)    
            
            Sua área de trabalho no vscode ficará da seguinte forma:
            
            ![vscode-remote](docs/vscode-remote.png) 

        * Para desconectar, basta clicar no icone verde no canto inferior e ir para Close Remote Connection.

            ![close-connection](docs/close-connection.png)

            Esta janela irá fechar e você devera sair da vm na outra janela, e dar os comandos para desligar conforme item 3 do Setup.

    * Acesso após configuração inicial.   
        * Apertar F1 no vscode (ou dependendo do computador fn + F1).

            ![remote-ssh](docs/f1-remote.png)

        * Selecionar o host. 
            Escolher o item 127.0.0.1 ou como você chamou no arquivo config.

            ![host](docs/selecionar-host.png)  

        * Uma nova janela do vscode irá abrir e ficará tentando a conexão. Após conectado nesta nova janela ir em "File → Open..." e escolher seu diretório de trabalho da vm.

            ![file](docs/file-open.png)    

            Sua área de trabalho no vscode ficará da seguinte forma:

            ![vscode-remote](docs/vscode-remote.png) 

        * Para desconectar, basta clicar no icone verde no canto inferior e ir para Close Remote Connection.
            
            ![close-connection](docs/close-connection.png)
            
            Esta janela irá fechar e você devera sair da vm na outra janela, e dar os comandos para desligar conforme item 3 do Setup. 

3. Caso tenha problemas para editar os arquivos via Remote - SSH no vscode, acessar sua VM conforme item 3 do Setup.
    * Entrar no diretório de trabalho.
        `$ cd ~/AcademiaNeon_DevOps/ `
    * Executar o comando abaixo que dará permissão full para qualquer usuário em todas as pastas e arquivos do diretório que estiver.
        `$ chmod -R 777 * `     