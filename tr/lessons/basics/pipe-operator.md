---
version: 1.0.1
title: Pipe Operatörü
redirect_from:
  - /lessons/basics/pipe-operator/
---

Pipe operatörü `|>` bir fonksiyonun sonucunu diğer fonksiyona ilk değer olarak geçirir.

{% include toc.html %}

## Giriş
Programlam dağınık olabilir. Gerçekten çok fazla dağınıklık ve karmaşa takip etmeyi zorlaştırı. Aşağıda iç içe geçmiş fonsiyonları inceleyelim:

```elixir
foo(bar(baz(new_function(other_function()))))
```

Burada `other_function/0` değeri `new_function/1`, ve `new_function/1` değeri `baz/1`, `baz/1` değeri `bar/1`, ve final olarak  `bar/1` değeri `foo/1` geçmektedir. Elixir  sözdizimsel kaosa pragmatik bir yaklaşım getiriyor. Pipe operatörü `|>` * fonksiyonun değeri alıve diğerine geçirir*. Pipe öperatörü ile yediden yazılan kod parçasını tekrar göz atalım.

```elixir
other_function() |> new_function() |> baz() |> bar() |> foo()
```

Pipe operatörü sonucu soldan alır sağ tarfa geçirir.

## Örnekler

bu örnek için Elixir'in String modülünü kullanacağız.

- Tokenize String (loosely)

```elixir
iex> "Elixir rocks" |> String.split()
["Elixir", "rocks"]
```

- Tokenlerin hepsini büyük harfe çevirme

```elixir
iex> "Elixir rocks" |> String.upcase() |> String.split()
["ELIXIR", "ROCKS"]
```

- Dizi sonu kontrolü

```elixir
iex> "elixir" |> String.ends_with?("ixir")
true
```

## En iyi Uygulama
Fonksiyonun argüman sayısı 1'den fazla ise parantez kullandığınızdan emin olun. Bu Elixir için önemli olmasada diğer programcıların kodunuzu yanlış yorumlamasına sebep olabilr. Ancak pipe operatörü buna sebep olmaz. Örneğin, üçüncü örneğin şu `String.ends_with?/2` alanından parantezleri kaldırısak aşağıdaki uyarı ile karşılaşırız.

```shell
iex> "elixir" |> String.ends_with? "ixir"
warning: parentheses are required when piping into a function call. For example:

  foo 1 |> bar 2 |> baz 3

is ambiguous and should be written as

  foo(1) |> bar(2) |> baz(3)

true
```