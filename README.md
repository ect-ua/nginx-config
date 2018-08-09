# Configuração NGINX do ECT-UA

Este repositório contém toda a configuração necessária para o NGINX para suportar o ECT-UA.

Podes clonar esta pasta diretamente para a diretória `conf.d` do NGINX (na nossa configuração: `/etc/nginx/conf.d`) usando o comando:

```git clone https://github.com/ect-ua/nginx-config.git /etc/nginx/conf.d```

Depois de clonares, não te esqueças de verificar se as tuas configurações no NGINX estão corretas usando o comando:

```nginx -t```

Estas instruções acima são apenas válidas para a máquina de produção do ECT-UA. Para a configuração do ambiente de desenvolvimento local, continua a ler este documento.

## O que é o NGINX?

O Nginx é um servidor web que também pode ser utilizado para outras funcionalidades como proxy, load balancer, proxy de e-mail ou cache de HTTP (fonte: [Wikipedia](https://en.wikipedia.org/wiki/Nginx)).

No caso do ECT-UA, estamos a usar o NGINX como [reverse proxy](https://en.wikipedia.org/wiki/Reverse_proxy) para servir publicamente as aplicações que correm no servidor. Cada aplicação no ECT UA corre sobre uma própria porta interna (eg.: 8080) e é o NGINX quem mapeia essas portas e lhes atribui um URL (eg.: https://www.ect-ua.com).

Podes instalar o nginx na tua máquina local ou em qualquer servidor onde pretendas servir websites. Basta seguires o tutorial da Digital Ocean sobre o assunto, disponível em https://www.digitalocean.com/community/tutorials/como-instalar-o-nginx-no-ubuntu-18-04-pt. Para mais informações sobre o NGINX, acede a https://www.nginx.com/.

## Configurar o servidor de produção do ECT-UA

Como foi dito acima, a configuração do nginx pode ser feita clonando diretamente os conteúdos deste repositório para a diretória `conf.d` do NGINX. Se precisares de editar estes ficheiros no servidor, nunca te esqueças de executar o comando `nginx -t`para verificar se a configuração se encontra correta.

Garante sempre que neste repositório está a última versão das configurações do NGINX do servidor. Para isso, sugiro que cries um Pull Request sempre que pretendes sugerir alterações e que não edites diretamente os ficheiros no branch master, a menos que tal faça sentido. Se não tens permissões de escrita sobre este repositório, faz um fork do mesmo e depois submete o teu Pull Request. Sabe mais aqui: https://help.github.com/articles/creating-a-pull-request-from-a-fork/.

Fizeste as tuas alterações diretamente no servidor?

Se tudo está a funcionar corretamente, já executaste o comando para testar e as tuas alterações já estão no branch master deste repositório, convém repôr tudo outra vez de novo para evitar problemas. O procedimento é o mesmo caso tenhas feito asneira e agora nada funcione, por isso estás no bom caminho.

Para voltar a sincronizar com o git, executa estes comandos por ordem diretamente na pasta `conf.d`:

1. ```git reset --hard``` -> Isto vai apagar as tuas alterações
2. ```git pull``` -> Isto vai fazer download da versão mais recente
3. ```nginx -t``` -> Nunca é demais confirmar que tudo está a funcionar corretamente
4. ```service nginx restart``` -> Reiniciar o serviço do nginx (apenas se tudo estiver a funcionar corretamente)

O comando de reiniciar o serviço do nginx pode variar com a distribuição ou Sistema Operativo. No nosso caso, Debian, o comando é o que foi escrito acima.

Se o git está todo lixado e nada funcionar, não entres em desespero. Existem formas de voltar atrás no histórico. Qualquer dúvida, pergunta a qualquer colega com mais experiência em git.


## Configurar uma máquina local de desenvolvimento

Ok, queres testar tudo direitinho na tua máquina local antes de mandares o que quer que seja para o repositório. Faz sentido, vamos a isso.

Primeiro começa por instalar o nginx na tua distribuição, seguindo as instruções acima. Depois, sugiro também que edites o teu ficheiro de hosts para que o teu computador tenha um endereço ao qual possas aceder facilmente. Para isso acede com permissões de root ao ficheiro `/etc/hosts` do teu sistema operativo (no Windows, a localização é diferente) e adiciona a seguinte linha no final do ficheiro:

```127.0.0.1 ectuadev```

Isto vai fazer com que o teu computador resolva o TLD .ectuadev localmente, permitindo-te fazer as alterações que precisas no nginx.

Ok, posto isto, edita estes ficheiros para que façam sentido para o teu caso. Não te esqueças também de ler cada um dos ficheiros individualmente, uma vez que vais precisar de fazer mais alterações.

Ah, e não te esqueças de apenas manter na tua pasta de configuração apenas os ficheiros que fazem sentido para o que queres correr. Se não o fizeres, podes ter problemas com o nginx ao dizer que o serviço na porta X, Y ou Z não está em execução. Quando fizeres um Pull Request para este repositório, não incluas ficheiros apagados nem afins. Isso depois pode ser chato para quem fizer a manutenção.

Btw, não basta o NGINX para teres o site a correr localmente no teu PC. Precisas de executar cada um dos serviços individualmente. Consulta a configuração de cada um nos respetivos repositórios.

## Disclaimer

Algumas portas definidas neste ficheiro poderão não ser as portas efetivamente usadas em produção. Para mais informações, contacta a equipa do ECT-UA pelo email `projetoectua [arroba] gmail.com`.
