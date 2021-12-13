## Gnome

### 

### Como adicionar um programa Appimage ao menu

#### 

#### Fontes

https://dev.to/tinegagideon/manually-add-an-appimage-software-shortcut-to-application-menu-in-linux-29ok

https://askubuntu.com/questions/819782/how-do-i-associate-a-file-type-with-an-appimage

#### 

#### Procedimento

Usarei como exemplo o programa [Mark Text](https://marktext.app/) que é um editor de arquivos markdowns:



**1 - Anote o path do seu arquivo appimage**

No meu caso:
`/home/anderson/MarkText/marktext-x86_64.AppImage`



**2 - Crie um arquivo de configuração desktop**

```bash
sudo pluma /usr/share/applications/marktext.desktop

Explicando:
# O sudo é devido as permissões
# O "pluma" é o meu editor de texto (vc pode usar o da sua preferência, por exemplo vim, nano e etc..)
# O "marktext.desktop" é o nome que escolhi para o meu arquivo. Anote o nome para usar no procedimento 4
```



**3 - Preencha o arquivo criado**

```
[Desktop Entry]
Name=MarkText
MimeType=text/markdown
Exec=/home/anderson/MarkText/marktext-x86_64.AppImage
Comment=Editor de arquivos MArkdowns
Icon=/home/anderson/MarkText/logo-96px.png
Type=Application
Terminal=false
Encoding=UTF-8
Categories=Utility
```



**4 - Associe a extensão de arquivo ao aplicativo (opcional)**

No meu caso, eu quero que ao clicar em qualquer arquivo de Mark Down (.md) ele seja aberto pelo  MarkText (marktext.desktop)

- Abra o arquivo que mapeia os mimetypes com as aplicações
  `pluma ~/.config/mimeapps.list`
- Adicione a seguinte entrada ao bloco "[Default Applications]"
  `text/markdown=marktext.desktop`