# Desafio 2: Rode o Script Python e Obtenha a Flag

## 🧪 Desafio

Você recebeu as instruções:

> "Run the attached Python script and it will output your flag."

E o seguinte código:

```python
import sys
# import this

if sys.version_info.major == 2:
    print("You are running Python 2, which is no longer supported. Please update to Python 3.")

ords = [81, 64, 75, 66, 70, 93, 73, 72, 1, 92, 109, 2, 84, 109, 66, 75, 70, 90, 2, 92, 79]

print("Here is your flag:")
print("".join(chr(o ^ 0x32) for o in ords))
```

**Objetivo:** Executar o script (ou analisar estaticamente) e recuperar a *flag* escondida.

### 🔎 Dicas para o Participante

1. Observe a lista de números `ords`.
2. Veja que cada número é transformado em um caractere após uma operação XOR: `o ^ 0x32`.
3. Lembre que `chr()` converte um número (código ASCII) em caractere.
4. Você pode reproduzir a lógica manualmente ou simplesmente rodar o script.

> *Escreva aqui a flag encontrada.*

---

## ✅ Explicação da Solução

O script percorre a lista `ords` e, para cada número `o`, aplica **XOR** com `0x32` (decimal 50), obtendo um novo código numérico que representa um caractere ASCII. A concatenação desses caracteres gera a flag final.

Expressão central:

```python
"".join(chr(o ^ 0x32) for o in ords)
```

Lê-se: *“para cada `o` em `ords`, faz `o ^ 0x32`, converte em caractere (`chr`) e junta tudo em uma string”*.

### 🔐 O que é XOR Aqui?

* XOR funciona como um “interruptor” bit a bit.
* É **simétrico**: se `c = o ^ k`, então `o = c ^ k`.
* Logo, a lista foi ofuscada aplicando XOR com a mesma chave `0x32`; o script apenas desfaz.

### 🧬 Decodificando Passo a Passo (Verificação de Alguns Bytes)

| o (dec) | o (hex) | o ^ 0x32 (dec) | Resultado (hex) | Char |
| ------: | ------- | -------------: | --------------- | ---- |
|      81 | 0x51    |             99 | 0x63            | c    |
|      64 | 0x40    |            114 | 0x72            | r    |
|      75 | 0x4B    |            121 | 0x79            | y    |
|      66 | 0x42    |            116 | 0x74            | t    |
|      70 | 0x46    |            116 | 0x74            | t    |
|      93 | 0x5D    |            111 | 0x6F            | o    |
|      73 | 0x49    |            123 | 0x7B            | {    |
|      72 | 0x48    |            122 | 0x7A            | z    |
|       1 | 0x01    |             51 | 0x33            | 3    |

Prosseguindo, obtemos a flag completa:

```
crypto{z3n_0f_pyth0n}
```

### 🧵 Pista Escondida

A linha comentada `# import this` aponta para o *Zen of Python*; por isso a flag contém `z3n_0f_pyth0n`.

### 🧠 Conceitos Reforçados

* Ofuscação simples via XOR.
* Reversibilidade do XOR com a mesma chave.
* Conversão número → caractere com `chr`.
* Reconhecimento do formato de flag.

---

## 🧮 Apêndice: Fazendo Manualmente na Calculadora de Programador

Se quiser repetir sem rodar o script:

1. Abra a Calculadora do Windows em modo **Programador** (`Ctrl+Shift+3`).
2. Trabalhe em **DEC** (decimal) ou **HEX** — escolha um modo e mantenha consistência.
3. Para cada número `o` da lista:

   * Digite `o`.
   * Pressione `Xor`.
   * Digite `50` (ou, em HEX, `32`).
   * Pressione `=`. O resultado é o código ASCII do caractere.
4. Converta o número resultante em caractere (tabela ASCII, memória ou ferramenta online) e anote.
5. Junte todos os caracteres.

### Exemplos Rápidos

* `81 XOR 50 = 99 → c`
* `64 XOR 50 = 114 → r`
* `75 XOR 50 = 121 → y`

### Versão em HEX

Equivalente: `0x51 ^ 0x32 = 0x63 (c)`.

### Processo Reverso

Quer gerar `ords` a partir da flag? Faça `ord(char) ^ 0x32` para cada caractere.

---

**Resumo em 1 frase:** O script desfaz uma ofuscação XOR (chave 0x32) sobre uma lista de inteiros para reconstruir a string `crypto{z3n_0f_pyth0n}`.

*Pronto! Se quiser, posso adicionar mais desafios.*
