## cron / cron job / crontab


### Fontes
https://ironlinux.com.br/crontab-aprenda-a-agendar-tarefas/
https://www.infowester.com/linuxcron.php
https://www.cyberciti.biz/faq/how-do-i-add-jobs-to-cron-under-linux-or-unix-oses/
https://www.cyberciti.biz/faq/run-crontab-job-every-minute-on-linux-unix-bsd/
https://www.cyberciti.biz/faq/where-is-the-crontab-file/
https://www.cyberciti.biz/faq/linux-unix-crontab-change-mailto-settings/
https://www.cyberciti.biz/faq/linux-show-what-cron-jobs-are-setup/
https://itsfoss.com/cron-job/



### Definições

**cron vs cron job vs crontab**
- cron: É o nome do programa, que roda como um daemon
- cron job: É o programa/script que está agendado para ser disparado pelo cron
- crontab: É o arquivo (e comando) onde vc agenda os cron jobs



### CLI - Linha de comando
```txt
# Sintaxe
contab [-u usuario] [opcao]

# Opções:
-u ---> O root ou sudo afeta a crontab de OUTRO usuário
-e ---> Editar o arquivo atual do crontab OU criar um, caso não exista
-l ---> Listar o conteúdo atual do crontab
-r ---> Remove o arquivo atual do crontab
```



### Arquivo  CronTab


#### Sintaxe para cada linha do arquivo
```
[minutos] [horas] [dia_mês] [mês] [dia_semana] [usuário] [cmd/script]


Limite de valores para cada parâmetro
- minuto: (0 - 59)
- hora:  (0 - 23)
- dia do mês: (1 - 31)
- mês: (1 - 12)
- dia da semana: (0 - 7) (Domingo=0 or 7)

# Múltiplos Valores
Sintaxe: Use "," (vírgula)
Exemplo de três valores: 2,4,6 

# Intervalo de Valores
Sintaxe: Use o "-" (traço)
Exemplo de intervalo do 1 ao 5:  1-5 

# Each (A cada)
Sintaxe: Use "*/" (asterisco e barra)
Exemplo de uma ação a cada 10 unidades: */10

```



### Exemplos 

#### Exemplo Básico
```
# Roda às 00h05 todos os dias no mês de Agosto
5 0 * 8 * command

# Roda às 22h00, de todos os meses, de segunda a sexta-feira
0 22 * * 1-5 command

# Roda às 04h05, de todos os domingos (ao invés do 0 poderíamos usar o 7 também)
5 4 * * 0 command

# Roda em todo minuto, do dia 14, no mês de Janeiro
* * 14 1 * command

# Roda às 12h em todos os dias da semana
* 12 * * 1-5 command
```


#### Exemplo com vírgula
```
# Insira a frase "Não entre em pânico" no arquivo infowester.txt, às 22 horas e 30 minutos, nos dias 3 e 14, em todos os meses e em todos os dias da semana.
30 22 3,14 * * echo "Não entre em pânico" > /home/alecrim/infowester.txt
```


#### Exemplo com each
```
# Roda a cada 1 minuto
# OBS: Ao vc usar apenas asteriscos ele repetirá essa ação a cada minuto
* * * * * comando
# Roda a cada 10 minutos
*/10 * * * * comando
```



### Testar
Para ver se seu comando realmente foi executado, vc deve visualizar o arquivo de log: /var/log/syslog

