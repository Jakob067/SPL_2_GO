# Go – Basic Types & Bit Shifting

## 1. Grundlegende Datentypen

Go ist eine statisch typisierte Programmiersprache. Jede Variable besitzt einen bestimmten Datentyp.

| Datentyp | Beschreibung | Beispiel |
|---|---|---|
| `bool` | Wahrheitswert | `true`, `false` |
| `string` | Zeichenkette | `"Hello"` |
| `int` | Ganzzahl | `42` |
| `uint` | Vorzeichenlose Ganzzahl | `42` |
| `float32` | 32-Bit-Gleitkommazahl | `3.14` |
| `float64` | 64-Bit-Gleitkommazahl | `3.14159` |
| `complex64` | Komplexe Zahl mit 64 Bit | `3 + 4i` |
| `complex128` | Komplexe Zahl mit 128 Bit | `3 + 4i` |
| `byte` | Alias für `uint8` | `65` |
| `rune` | Alias für `int32`, Unicode-Codepunkt | `'A'` |

### Integer-Datentypen

Die Zahl hinter `int` gibt die Anzahl der verwendeten Bits an.

| Typ | Speicher | Wertebereich |
|---|---|---|
| `int8` | 8 Bit | -128 bis 127 |
| `int16` | 16 Bit | -32.768 bis 32.767 |
| `int32` | 32 Bit | -2³¹ bis 2³¹ − 1 |
| `int64` | 64 Bit | -2⁶³ bis 2⁶³ − 1 |
| `uint8` | 8 Bit | 0 bis 255 |
| `uint64` | 64 Bit | 0 bis 2⁶⁴ − 1 |

**Hinweis:** `uint` bedeutet *unsigned integer* und kann keine negativen Zahlen speichern. `int` und `uint` sind je nach System 32 oder 64 Bit groß.

## 2. Komplexe Zahlen

Komplexe Zahlen bestehen aus einem Realteil und einem Imaginärteil.

**z = a + bi**

- `complex64`: 32 Bit Realteil + 32 Bit Imaginärteil
- `complex128`: 64 Bit Realteil + 64 Bit Imaginärteil

Beispiel:

```go
var z complex128 = 3 + 4i
fmt.Println(z) // (3+4i)
```

## 3. Bit Shifting (Bitverschiebung)

Bit Shifting bezeichnet das Verschieben von Bits einer Binärzahl nach links oder rechts.

Go besitzt zwei Operatoren:

- `<<` – Left Shift (Linksverschiebung)
- `>>` – Right Shift (Rechtsverschiebung)

### Left Shift (`<<`)

Beim Left Shift werden Bits nach links verschoben.

Beispiel:

```go
x := 5 << 2
fmt.Println(x) // 20
```

Binärdarstellung:

```text
5  = 00000101
20 = 00010100
```

Die Bits wurden um zwei Stellen nach links verschoben.

**Mathematische Regel:**

`x << n = x * 2^n`

Beispiel:

`5 << 2 = 5 * 2² = 20`

### Right Shift (`>>`)

Beim Right Shift werden Bits nach rechts verschoben.

```go
x := 20 >> 2
fmt.Println(x) // 5
```

Binärdarstellung:

```text
20 = 00010100
5  = 00000101
```

**Mathematische Regel für nichtnegative Ganzzahlen:**

`x >> n = x / 2^n` (ganzzahlige Division)

Beispiel:

`20 >> 2 = 20 / 4 = 5`

Bei festen Integer-Typen können Linksverschiebungen Bits verlieren, wenn das Ergebnis nicht mehr in den Typ passt.

## 4. Beispiel aus Tour of Go

```go
package main

import (
    "fmt"
    "math/cmplx"
)

var (
    ToBe   bool       = false
    MaxInt uint64     = 1<<64 - 1
    z      complex128 = cmplx.Sqrt(-5 + 12i)
)

func main() {
    fmt.Printf("Type: %T Value: %v\n", ToBe, ToBe)
    fmt.Printf("Type: %T Value: %v\n", MaxInt, MaxInt)
    fmt.Printf("Type: %T Value: %v\n", z, z)
}
```

### Erklärung von `1<<64 - 1`

Der Ausdruck berechnet den maximalen Wert eines `uint64`.

1. `1 << 64` entspricht 2⁶⁴.
2. Anschließend wird 1 abgezogen.
3. Das Ergebnis ist 18.446.744.073.709.551.615.

Das ist der größte darstellbare Wert eines `uint64`.

### Erklärung von `fmt.Printf()`

```go
fmt.Printf("Type: %T Value: %v\n", ToBe, ToBe)
```

| Bestandteil | Bedeutung |
|---|---|
| `fmt.Printf` | Formatierte Konsolenausgabe |
| `%T` | Datentyp der Variable |
| `%v` | Wert der Variable |
| `\n` | Zeilenumbruch |
| `ToBe, ToBe` | Argumente für die beiden Platzhalter |

Ausgabe:

```text
Type: bool Value: false
Type: uint64 Value: 18446744073709551615
Type: complex128 Value: (2+3i)
```

## 5. Variablendeklaration

Go unterstützt verschiedene Arten der Variablendeklaration.

```go
var x int = 10
var y = 20
z := 30
```

- `var x int = 10`: Explizite Typangabe.
- `var y = 20`: Automatische Typerkennung.
- `z := 30`: Kurzdeklaration mit automatischer Typerkennung.

**Wichtig:** `:=` funktioniert nur innerhalb von Funktionen. Außerhalb von Funktionen muss beispielsweise `var` verwendet werden.

## Zusammenfassung

- Go besitzt verschiedene Datentypen für Zahlen, Strings und Wahrheitswerte.
- `int` speichert Ganzzahlen, `uint` nur nichtnegative Ganzzahlen.
- `complex64` und `complex128` speichern komplexe Zahlen.
- `<<` verschiebt Bits nach links und entspricht bei ausreichend großem Wertebereich einer Multiplikation mit Zweierpotenzen.
- `>>` verschiebt Bits nach rechts und entspricht bei nichtnegativen Ganzzahlen einer ganzzahligen Division durch Zweierpotenzen.
- `%T` gibt den Datentyp und `%v` den Wert aus.
- `:=` ermöglicht eine kurze Variablendeklaration innerhalb von Funktionen.

**Quelle:** [A Tour of Go – Basic Types](https://go.dev/tour/basics/11)
