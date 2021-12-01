## Proxy Hell - Acessando o github atraves de ssh

### Fonte
https://stackoverflow.com/questions/1728934/accessing-a-git-repository-via-ssh-behind-a-firewall



### Pré-requisitos
- Uma ferramenta de rede, que obrigue a solicitação ssh passar pelo proxy para atingir o github (Você pode usar o **NetCat** ou **Socat**, conforme exemplos abaixos)
- Adicionar a chamada a esta ferramenta de rede no arquivo de configuração do ssh



### Usando a ferramenta Netcat
A vantagem é que o nc (netcat) já vem instalado no ubuntu, e eu não precisei me autenticar (Provavelmente ele pega a autenticação das variáveis de ambiente)

- Crie ou edite o arquivo `~/.ssh/config`
```
Host=github.com
ProxyCommand=nc -X connect -x "proxy_host:proxy_porta" github.com 22
```



### Usando a ferramenta  Socat
- Instale o socat com o comando `apt install socat`
- Crie ou edite o arquivo `~/.ssh/config`
```
Host=github.com
ProxyCommand=socat - PROXY:proxy_host:%h:%p,proxyport=proxy_porta,proxyauth=proxy_usuario:proxy_senha*
```