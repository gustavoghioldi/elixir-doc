# elixir-doc

## Introducción
### Modo Interactivo
Una vez instalado Elixir, temos 2 nuevos ejecutables: iex, elixir and elixirc

iex --> abre la consola interactiva

```bash
Erlang/OTP 18 [erts-7.3] [source] [64-bit] [smp:4:4] [async-threads:10] [kernel-poll:false]

Interactive Elixir (1.1.0-dev) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)> 2+10
12
iex(2)>"hola"<>" mundo"
"hola mundo"
```
### Corriendo un script

```elixir
IO.puts "Hola mundo desde un script"
```

salvamoms como introduccion.exs, y se ejecuta: 
```bash
elixir introduccion.exs
Hola mundo desde un script
```

## Tipos Básicos
```bash

```
### Aritmetica básica
```bash
Erlang/OTP 18 [erts-7.3] [source] [64-bit] [smp:4:4] [async-threads:10] [kernel-poll:false]

Interactive Elixir (1.1.0-dev) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)> 1 + 45
46
iex(2)> 23 -34
-11
iex(3)> 5 * 8
40
iex(4)> 8/3
2.6666666666666665
iex(5)> div 8, 3
2
iex(6)> rem 8, 3
2
iex(7)> round 3.45
3
iex(8)> round 3.55
4
iex(9)> trunc 3.55
3
```
### Identificando funciones

### Booleans
Soporta true y false
```bash
iex(1)> true == false
false
iex(2)> false == false 
true
iex(3)> is_boolean(false)
true
iex(4)> is_integer(1)
true
iex(5)> is_integer(1.0)
false
```
### Atoms
Son constantes donde su nombre es un unico valor
```bash
iex> :hola
:hola
iex> :hola == :hello
false
```

los boleanos son atom:
```bash
iex> true == :true
true
iex> is_atom(false)
true
iex> is_boolean(:false)
true
```
### Strings
Documentación oficial: https://hexdocs.pm/elixir/String.html

```bash
iex(1)> "Moño"
"Moño"
iex(2)> "Hola #{:mundo}"
"Hola mundo"
iex(3)> byte_size("moño")
5
iex(4)> String.length("moño")
4
iex(5)> byte_size("mono")    
4
iex(6)> String.upcase("moño")   
"MOÑO"
iex(7)> "hola" == 'hola' ##las comillas influyen sobre la igualdad
false
```

### funciones Anonimas
```bash
iex> suma = fn a, b -> a + b end
#Function<12.71889879/2 in :erl_eval.expr/5>
iex> suma.(1, 2)
3
iex> is_function(suma)
true
iex> is_function(suma, 2) # checkea si suma espera 2 argumentos
true
iex> is_function(suma, 1) # checkea si suma espera 1 argumento
false
iex> x2 = fn a -> suma.(a, a) end
#Function<6.71889879/1 in :erl_eval.expr/5>
iex> x2.(2)
4
```
### Listas
documentación oficial: https://hexdocs.pm/elixir/List.html
```bash
iex> ["hola", :ok, 1, true]
["hola", :ok, 1, true]
iex> length [1, 2, 3, :false]
4
iex> lista = [1, 2, :x, false]
[1, 2, :x, false]
iex> hd lista
1
iex> tl lista
[2, :x, false]
iex> ["hola", :tail, 1.23] ++ [22, "moño"]
["hola", :tail, 1.23, 22, "moño"]
iex> ["hola", :tail, 1.23] -- [22, :tail] 
["hola", 1.23]
```
### Tuplas
documentación oficial: https://hexdocs.pm/elixir/Tuple.html
como las tuplas las listas aceptan cualquier valor:
```bash
iex> {:ok, "hola"}
{:ok, "hola"}
iex> tuple_size {:ok, "hola"}
2
iex> elem({:ok, "hola"}, 1)
"hola"
iex> log = File.read("/var/log/mysql/error.log")
{:ok,
 "2017-05-17T19:37:12.615916Z 0 [Note] InnoDB: page_cleaner: 1000ms intended loop took 274882ms. The settings might not be optimal. (flushed=0 and evicted=0, during the time.)\n2017-05-17T20:58:07.784705Z 0 [Note] InnoDB: page_cleaner: 1000ms intended loop took 518550ms. The settings might not be optimal. (flushed=0 and evicted=0, during the time.)\n2017-05-18T00:04:12.759178Z 0 [Note] InnoDB: page_cleaner: 1000ms intended loop took 1935978ms. The settings might not be optimal. (flushed=0 and evicted=0, during the time.)\n"}
iex> elem(log, 1)
"2017-05-17T19:37:12.615916Z 0 [Note] InnoDB: page_cleaner: 1000ms intended loop took 274882ms. The settings might not be optimal. (flushed=0 and evicted=0, during the time.)\n2017-05-17T20:58:07.784705Z 0 [Note] InnoDB: page_cleaner: 1000ms intended loop took 518550ms. The settings might not be optimal. (flushed=0 and evicted=0, during the time.)\n2017-05-18T00:04:12.759178Z 0 [Note] InnoDB: page_cleaner: 1000ms intended loop took 1935978ms. The settings might not be optimal. (flushed=0 and evicted=0, during the time.)\n"
iex> elem(log, 0)
:ok
```
### Listas o Tuplas?
//TODO

## Operaciones básicas

***Manipulación de listas***

```elixir
iex> [1, 2, 3, 5] ++ [4, 3]
[1, 2, 3, 5, 4, 3]
iex> [1, 2, 5] -- [1, 2, 3]
[5]
```
***Concatenación de Strings con "<>"***
```elixir
iex> "foo" <> "bar"
"foobar"
```

***Operadores booleanos***
and(&&), or(||), not(!):

```elixir
# or
iex> 1 || true
1
iex> false || 11
11

# and
iex> nil && 13
nil
iex> true && 17
17

# !
iex> !true
false
iex> !1
false
iex> !nil
true
iex> 1 == 1
true
iex> 1 != 2
true
iex> 1 < 2
true
iex> 1 == 1.0
true
iex> 1 === 1.0
false
```

para tener en cuenta:

```elixir
number < atom < reference < function < port < pid < tuple < map < list < bitstring
```


