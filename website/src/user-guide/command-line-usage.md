<!--
source_url: https://github.com/phpstan/phpstan/blob/-/website/src/user-guide/command-line-usage.md
revision: 7632b4cee8b50846e3f2cc2c2c86681cb699c22b
status: ready
-->

# Uso da linha de comando

O arquivo executável do PHPStan é instalado no diretório `bin-dir` do Composer,
cujo padrão é `vendor/bin`.

## Analisando código

Para analisar seu código, execute o comando `analyse`.
O código de saída `0` significa que não há erros.

```shell
vendor/bin/phpstan analyse [options] [<paths>...]
```

Como **`<paths>`** você pode passar um ou vários caminhos para arquivos PHP ou
diretórios separados por espaços.
Ao procurar por arquivos em diretórios, várias [opções de configuração][1] são
respeitadas.
Caminhos relativos são resolvidos com base no diretório de trabalho atual.

### `--level|-l` {: #--level-l }

Especifica o [nível de regra][2] a ser executado.

### `--configuration|-c` {: #--configuration-c }

Especifica o caminho para um [arquivo de configuração][3].
Caminhos relativos são resolvidos com base no diretório de trabalho atual.

### `--generate-baseline|-b` {: #--generate-baseline-b }

Gera o arquivo da [linha de base][4].
Aceita um caminho (`--generate-baseline foo.neon`) cujo padrão é
`phpstan-baseline.neon`.
Caminhos relativos são resolvidos com base no diretório de trabalho atual.

Se você já usa a linha de base, o caminho para o arquivo da linha de base deve
corresponder ao que já está em uso.
Isso garante que a linha de base não seja usada duas vezes e que o comando
funcione corretamente.

Observe que o código de saída é diferente neste caso.
O código de saída `0` significa que a geração da linha de base foi bem-sucedida
e a linha de base não está vazia.
Se não houver erros que resultariam na geração da linha de base, o código de
saída é `1`.

Por padrão, o PHPStan não gerará uma linha de base vazia.
No entanto, você pode passar `--allow-empty-baseline` junto com
`--generate-baseline` para permitir que um arquivo de linha de base vazio seja
gerado.

### `--pro` {: #--pro }

Inicia o [PHPStan Pro][5] que permite que você navegue por erros (incluindo
erros ignorados) em uma bela interface de pessoa usuária web.
Experimente executando o PHPStan com `--pro` ou indo para
[account.phpstan.com][6] e criando uma conta.

### `--autoload-file|-a` {: #--autoload-file-a }

Se sua aplicação usa um carregador automático personalizado, você deve
configurá-lo e registrá-lo em um arquivo PHP que é passado para esta opção da
CLI.
Caminhos relativos são resolvidos com base no diretório de trabalho atual.

[Saiba mais »][7]

### `--error-format` {: #--error-format }

Especifica um formatador de erro personalizado.
[Saiba mais sobre formatos de saída »][8]

### `--no-progress` {: #--no-progress }

Desativa a barra de progresso.
Não aceita nenhum valor.

### `--memory-limit` {: #--memory-limit }

Especifica o limite de memória no mesmo formato que o `php.ini` aceita.

Exemplo: `--memory-limit 1G`

### `--xdebug` {: #--xdebug }

O PHPStan desativa o Xdebug, se estiver habilitado, para obter melhor
desempenho.

Se você precisa depurar o próprio PHPStan ou suas
[extensões personalizadas][9] e quer executar o PHPStan com o Xdebug habilitado,
passe esta opção.
Ela não aceita nenhum valor.

### `--debug` {: #--debug }

Em vez da barra de progresso, ele emite linhas com cada arquivo analisado antes
de sua análise.

Além disso, ele para no primeiro erro interno e imprime um rastreamento de
pilha.

Esta opção também desabilita o [cache de resultados][10] e o
[processamento paralelo][11] para fins de depuração.

### `-v`, `-vv`, `-vvv` {: #-v-vv-vvv }

Aumenta a verbosidade e faz o PHPStan mostrar várias informações de depuração,
como memória consumida ou [o motivo do cache de resultados não ser usado][12].

Combinar `-vvv` com `--debug` é ótimo para [identificar arquivos lentos][13].

Executar com `-vvv` também imprimirá as mesmas informações que o comando
[`diagnose`][14].

### `--ansi, --no-ansi` {: #--ansi--no-ansi }

Substitui a detecção automática de se as cores devem ser usadas na saída e o
quão bonita a barra de progresso deve ser.

### `--quiet|-q` {: #--quiet-q }

Silencia toda a saída.
Útil se você tiver interesse apenas no código de saída.

### `--version|-V` {: #--version-v }

Em vez de executar a análise, ele exibe apenas a versão atual do PHPStan em uso.

### `--help` {: #--help }

Exibe um resumo das opções de CLI disponíveis, mas não com tantos detalhes
quanto esta página.

## Executando sem argumentos

Você pode analisar seu projeto executando apenas `vendor/bin/phpstan` se você
atender às seguintes condições:

* Você tem `phpstan.neon` ou `phpstan.neon.dist` no seu diretório de trabalho
  atual
* Este arquivo contém o parâmetro [`paths`][1] para definir uma lista de
  caminhos analisados
* Este arquivo contém o parâmetro [`level`][15] para definir o nível de regra
  atual

## Limpando o cache de resultados

Para limpar o estado atual do [cache de resultados][10], por exemplo, se você
estiver desenvolvendo [extensões personalizadas][9] e o cache de resultados
estiver ficando defasado com muita frequência.

```shell
vendor/bin/phpstan clear-result-cache [options]
```

O comando `clear-result-cache` compartilha algumas das opções com o comando
`analyse`.
O motivo é que o [arquivo de configuração][3] pode estar definindo um
[`tmpDir`][16] personalizado, que é onde o cache de resultados é salvo.

### `--configuration|-c`

Especifica o caminho para um [arquivo de configuração][3].
Caminhos relativos são resolvidos com base no diretório de trabalho atual.

### `--autoload-file|-a`

Se sua aplicação usa um carregador automático personalizado, você deve
configurá-lo e registrá-lo em um arquivo PHP que é passado para esta opção da
CLI.
Caminhos relativos são resolvidos com base no diretório de trabalho atual.

[Saiba mais »][7]

### `--memory-limit`

Especifica o limite de memória no mesmo formato que o `php.ini` aceita.

Exemplo: `--memory-limit 1G`

### `--debug`

Se o comando `clear-result-cache` estiver falhando com uma exceção não
capturada, execute-o novamente com `--debug` para ver o rastreamento de pilha.

### `--quiet|-q`

Silencia toda a saída.
Útil se você tiver interesse apenas no código de saída.

### `--version|-V`

Em vez de limpar o cache de resultados, ele apenas exibe a versão atual do
PHPStan em uso.

### `--help`

Exibe um resumo das opções de CLI disponíveis, mas não com tantos detalhes
quanto esta página.

## Diagnosticando problemas

Para diagnosticar o motivo do PHPStan estar se comportando de uma certa maneira,
você pode executar o comando `diagnose`:

```shell
vendor/bin/phpstan diagnose [options]
```

Ele gera informações úteis como a versão atual do tempo de execução do PHP, a
versão atual do PHP para análise (que pode ser diferente com base na
configuração), a versão atual do PHPStan, etc.
Extensões personalizadas também podem implementar a
[interface DiagnoseExtension][17] para adicionar suas próprias informações que
também são impressas ao executar o comando `diagnose`.

As mesmas informações também são impressas quando você executa o
[comando `analyse`][18] com `-vvv`.

### `--configuration|-c`

Especifica o caminho para um [arquivo de configuração][3].
Caminhos relativos são resolvidos com base no diretório de trabalho atual.

### `--autoload-file|-a`

Se sua aplicação usa um carregador automático personalizado, você deve
configurá-lo e registrá-lo em um arquivo PHP que é passado para esta opção da
CLI.
Caminhos relativos são resolvidos com base no diretório de trabalho atual.

### `--level|-l`

Especifica o [nível de regra][2] a ser executado.

### `--memory-limit`

Especifica o limite de memória no mesmo formato que o `php.ini` aceita.

Exemplo: `--memory-limit 1G`

### `--debug`

Exceções lançadas (erros internos) não serão capturadas e seu rastreamento de
pilha será impresso na íntegra quando esta opção for adicionada.

[1]: ../config-reference.md#analysed-files

[2]: rule-levels.md

[3]: ../config-reference.md

[4]: baseline.md

[5]: https://phpstan.org/blog/introducing-phpstan-pro

[6]: https://account.phpstan.com/

[7]: discovering-symbols.md

[8]: output-format.md

[9]: ../developing-extensions/extension-types.md

[10]: result-cache.md

[11]: ../config-reference.md#parallel-processing

[12]: result-cache.md#debugging-the-result-cache

[13]: https://phpstan.org/blog/debugging-performance-identify-slow-files

[14]: #diagnose-problems

[15]: ../config-reference.md#rule-level

[16]: ../config-reference.md#caching

[17]: https://apiref.phpstan.org/2.1.x/PHPStan.Diagnose.DiagnoseExtension.html

[18]: #analisando-codigo
