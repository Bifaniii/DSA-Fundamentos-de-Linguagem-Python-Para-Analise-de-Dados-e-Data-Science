**OBS.:** É importante sempre utilizar a expressão **WITH**, pois caso seja feito um **OPEN()** e não tenha um **CLOSE()**, há o risco de corromper o arquivo.


```python
with open('arquivos/cientista.txt', 'r') as arquivo:
    conteudo = arquivo.read()
    print(conteudo)
```

    Cientista de dados pode ser uma excelente alternativa de carreira. Esses profissionais precisam saber como programar em Python. E, claro, devem ser proficientes em Data Science.
    

**----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------**

**Biblioteca CSV** --> Permite a manipulação do arquivo CSV como se fosse um objeto


```python
import csv  # Antes de tudo, nunca esquecer da importação da biblioteca
```


```python
with open('arquivos/teste.csv', 'w') as arquivo:
    writer = csv.writer(arquivo)        #Cria o objeto de escrita                      
    writer.writerow(('nota1', 'nota2', 'nota3'))
    writer.writerow(('2', '2', '2'))
    writer.writerow(('3', '3', '3'))
    writer.writerow(('1', '1', '1'))
```

Explicação do código:
```
1 - Importa-se a biblioteca CSV
2 - Cria-se então o arquivo e da-se o 'apelido' de arquivo
3 - Cria-se a variável WRITER para ter a funcionalidade de uma FUNÇÃO. Neste caso, a de escrever --> CSV.WRITER(X), da própria biblioteca
4 - Usa-se a variável criada para escrever dentro do arquivo criado, linha a linha. Utilizando a função X.writerow(parâmetros separado por vírgulas)
5 - Por ter utilizado a expressão WITH, o arquivo fecha sozinho após a finalização e não é necessário utilizar close()

**Leitura do arquivo**


```python
with open('arquivos/teste.csv', 'r', encoding='utf8', newline = '\r\n') as arquivo:
    leitor = csv.reader(arquivo)
    for x in leitor:
        print(x)
```

    ['nota1', 'nota2', 'nota3']
    ['2', '2', '2']
    ['3', '3', '3']
    ['1', '1', '1']
    

Explicação do código:
```
1 - Abertura de teste.csv como objeto arquivo. Parâmetro de caracteres utf8 e quebras de linhas com \r\n
2 - Criação da variável Leitor para armazenar a função csv.reader(x)
3 - Criação do loop que passa armazenando os dados em listas, separando-os por vírgulas, linha a linha

**Leitura do arquivo em listas**


```python
with open('arquivos/teste.csv', 'r', newline ="\r\n") as arquivo:
    leitor = csv.reader(arquivo)
    dados = list(leitor)
```


```python
print(dados)
```

    [['nota1', 'nota2', 'nota3'], ['2', '2', '2'], ['3', '3', '3'], ['1', '1', '1']]
    

Explicação do código:
```
1 - Abertura de teste.csv como objeto arquivo
2 - Criação da variável Leitor para armazenar a função csv.reader(x)
3 - Armazenamento dos dados em listas

NÃO ESQUECER DO NEWLINE. Pois, quando tentei sem o parâmetro criava-se listas vazias entre as litas. No vídeo do curso funcionou por que era outro SO (MacOS).

**Leitura do arquivo em listas, retirando o cabeçalho, obtendo-se somente os dados**


```python
for linha in dados[1:]:
    print(linha)
```

    ['2', '2', '2']
    ['3', '3', '3']
    ['1', '1', '1']
    

Explicação do loop:

```
Para cada elemento (i), ou seja, linha, em 'dados' (que foram armazenados em listas). Imprima linha.
Porém, foi utilizado a indexação [1:] na variável dados. Visto que indexações de listas começam por 0 e, neste caso pertence ao cabeçalho que não é interessante para o que foi pedido. Então, aplica-se a indexação 1:, sem nada após porque queremos ler todos os dados, sem impor um limite.
