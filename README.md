# Procedimento para a adição de senha no frontend de aplicações em execução no Apache utilizando o .htpasswd
> Importante ressaltar que essa ação está longe de ser um hardening de ambiente.

1. Instale a ferramenta **apache2-utils**, que inclui o comando htpasswd: <br>
`sudo apt update` <br>
`sudo apt install apache2-utils` <br>

2. Crie o arquivo **.htpasswd** e adicione o nome de usuário e senha criptografada: <br>
`sudo htpasswd -c /etc/apache2/.htpasswd user`
> Esse passo pode ser refeito 'n' vezes dependendo de quantos usuários existam no ambiente. <br>

3. Certifique-se de que o arquivo .htpasswd esteja protegido de leitura por outros usuários: <br>
`sudo chmod 640 /etc/apache2/.htpasswd`

4. No arquivo de configuração do Apache (geralmente localizado em /etc/apache2/apache2.conf ou em um arquivo de configuração específico do site), adicione as diretivas necessárias para autenticar usando o arquivo .htpasswd:
```
<Directory /path/to/your/protected/directory>
    AuthType Basic
    AuthName "Restricted Content"
    AuthUserFile /etc/apache2/.htpasswd
    Require valid-user
</Directory>
```
Substitua **/path/to/your/protected/directory** pelo caminho para o diretório que você deseja proteger com autenticação (pode ser uma página ou a aplicação inteira).

5. Reinicie o serviço do Apache para aplicar as alterações:
`sudo apt restart apache2`
6. Resultado: <br>
[![Captura-de-tela-de-2023-07-06-20-10-30.png](https://i.postimg.cc/SKfpLrfm/Captura-de-tela-de-2023-07-06-20-10-30.png)](https://postimg.cc/nsr5pqWW)
