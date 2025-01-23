<!--
source_url: https://github.com/phpstan/phpstan/blob/-/website/src/user-guide/getting-started.md
revision: 65dc199c3c137db0ee1b05cf94c8fe65d53fedbd
status: ready
-->

# Começando

PHPStan requer o PHP >= 7.4.
Você precisa executá-lo em um ambiente com PHP 7.x, mas o código real não
precisa usar os recursos do PHP 7.x.
(Código escrito para PHP 5.6 e anteriores pode ser executado no 7.x praticamente
sem modificações.)

O PHPStan funciona melhor com código moderno orientado a objetos.
Quanto mais fortemente tipado for seu código, mais informações você dará ao
PHPStan para trabalhar.

Código devidamente anotado e com declaração de tipo (propriedades de classes,
argumentos de funções e métodos, tipos de retorno) ajuda não apenas ferramentas
de análise estática, mas também outras pessoas que trabalham com o código a
entendê-lo.

## Instalação

Para começar a executar a análise no seu código, instale o PHPStan com o
[Composer][1]:

```bash
composer require --dev phpstan/phpstan
```

O Composer instalará o executável do PHPStan em seu `bin-dir`, cujo padrão é
`vendor/bin`.

Você também pode baixar o [PHAR mais recente][2] e usá-lo.
Mas sem o Composer, você não poderá instalar e usar as
[extensões do PHPStan][3].

[Acesse aqui][4] se quiser usar o PHPStan no Docker.

## Primeira execução

Para deixar o PHPStan analisar sua base de código, você precisa usar o comando
`analyse` e apontá-lo para os diretórios certos.

Então, por exemplo, se você tem suas classes nos diretórios `src` e `tests`,
você pode executar o PHPStan assim:

```shell
vendor/bin/phpstan analyse src tests
```

> **Info**:
> Você deve analisar apenas arquivos com o código que você escreveu.
> Não há necessidade de analisar o diretório `vendor` com dependências de
> terceiros porque não está em seu poder corrigir todos os erros cometidos pelas
> pessoas desenvolvedoras com as quais você não trabalha diretamente.
>
> Sim, o PHPStan precisa saber sobre todas as classes, interfaces, traits e
> funções que seu código usa, mas isso é obtido por meio da
> [descoberta de símbolos][5], não pela inclusão dos arquivos na análise.

[Saiba mais sobre as opções de linha de comando.][6]

O PHPStan provavelmente encontrará alguns erros, mas não se preocupe, pode estar
tudo bem com seu código.
Erros encontrados na primeira execução tendem a ser:

* Argumentos extras passados para funções (por exemplo, a função requer dois
  argumentos, o código passa três)
* Argumentos extras passados para funções `print`/`sprintf` (por exemplo, a
  string de formato contém um espaço reservado, o código passa dois valores para
  substituir)
* Erros óbvios em código morto
* Símbolos desconhecidos - como "classe não encontrada".
  Consulte [Descobrindo símbolos][7] para mais detalhes.

**Por padrão, o PHPStan executa apenas as verificações mais básicas.
Acesse [Níveis de regras][8] para aprender como ativar verificações mais
rigorosas.**

**Aprenda sobre todas as opções de configuração na
[Referência de configuração][9].**

[1]: https://getcomposer.org/

[2]: https://github.com/phpstan/phpstan/releases

[3]: extension-library.md

[4]: docker.md

[5]: discovering-symbols.md

[6]: command-line-usage.md

[7]: discovering-symbols.md

[8]: rule-levels.md

[9]: ../config-reference.md
