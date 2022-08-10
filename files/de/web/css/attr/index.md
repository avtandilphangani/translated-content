---
title: attr
slug: Web/CSS/attr
tags:
  - CSS
  - CSS Funktion
  - Layout
  - Referenz
  - Web
translation_of: Web/CSS/attr()
original_slug: Web/CSS/attr()
---
{{ CSSRef() }}

## Übersicht

Die `attr()` [CSS](/de/docs/Web/CSS) Funktion wird verwendet, um einen Wert eines Attributs des ausgewählten Elements abzurufen und innerhalb des Stylesheets zu verwenden. Sie kann auch für [Pseudoelemente](/de/docs/Web/CSS/Pseudo-elements) verwendet werden. In diesem Fall wird der Wert des Attributs seines ursprünglichen Elements zurückgegeben.

Die `attr()` Funktion kann innerhalb jeder CSS Eigenschaft verwendet werden. {{ experimental_inline() }}

## Syntax

    Formale Syntax: attr( attribute-name <type-or-unit>? [, <fallback> ]? )

### Werte

- `attribute-name`
  - : Entspricht dem Namen des Attributs des HTML Elements, das durch CSS referenziert wird.
- `<type-`or-unit>
  - | : Ist ein Schlüsselwort, das den Typ oder die Einheit des Attributwerts angibt, da in HTML einige Attribute implizite Einheiten haben. Falls die Verwendung von `<type-or-unit>` als Wert für das angegebene Attribut ungültig ist, ist der `attr()` Ausdruck ebenfalls ungültig. Falls nicht angegeben, wird standardmäßig `string` verwendet. Nachfolgend ist eine Liste aller Werte aufgeführt: | Schlüsselwort                                | Assoziierter Typ                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Anmerkung                                                                                                       | Standardwert |
    | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------- | ------------ |
    | `string`                                                                                                                                                                                                                                                                                                                                                                                           | {{cssxref("&lt;string&gt;")}}     | Der Attributwert wird als CSS {{cssxref("&lt;string&gt;")}} Wert behandelt. Er wird nicht erneut geparst, insbesondere werden die Zeichen wie angegeben verwendet, anstatt dass CSS Escapes zu anderen Zeichen umgewandelt werden.                                                                                                                                                                                                                                                                                                    | An empty string                                                                                                 |
    | `color` {{ experimental_inline() }}                                                                                                                                                                                                                                                                                                                                                       | {{cssxref("&lt;color&gt;")}}         | Der Attributwert wird als Hash (3- oder 6-Werthash) oder als Schlüsselwort interpretiert. Er muss ein gültiger CSS {{cssxref("&lt;string&gt;")}} Wert sein. Voran- und nachgestellte Leerzeichen werden abgeschnitten.                                                                                                                                                                                                                                                                                                                | `currentColor`                                                                                                  |
    | `url` {{ experimental_inline() }}                                                                                                                                                                                                                                                                                                                                                         | {{ cssxref("&lt;uri&gt;") }}         | Der Attributwert wird als ein String interpretiert, wie er in einer `url()` Funktion verwendet wird. Relative URLs werden relativ zum ursprünglichen Dokument interpretiert, nicht relativ zum Stylesheet. Voran- und nachgestellte Leerzeichen werden abgeschnitten.                                                                                                                                                                                                                                                                            | Die URL `about:invalid`, die auf ein nicht existierendes Dokument mit einer allgemeinen Fehlermeldung verweist. |
    | `integer` {{ experimental_inline() }}                                                                                                                                                                                                                                                                                                                                                     | {{cssxref("&lt;integer&gt;")}}     | Der Attributwert wird als CSS {{cssxref("&lt;integer&gt;")}} Wert interpretiert. Falls er nicht gültig ist, d. h. keine Ganzzahl oder außerhalb des Bereichs, der von der CSS Eigenschaft akzeptiert wird, wird der Standardwert verwendet. Voran- und nachgestellte Leerzeichen werden abgeschnitten.                                                                                                                                                                                                                                 | `0` oder, falls `0` kein gültiger Wert für die Eigenschaft ist, der Minimalwert der Eigenschaft.                |
    | `number` {{ experimental_inline() }}                                                                                                                                                                                                                                                                                                                                                      | {{cssxref("&lt;number&gt;")}}     | Der Attributwert wird als CSS {{cssxref("&lt;number&gt;")}} Wertinterpretiert. Falls er nicht gültig ist, d. h. keine Zahl oder außerhalb des Bereichs, der von der CSS Eigenschaft akzeptiert wird, wird der Standardwert verwendet. Voran- und nachgestellte Leerzeichen werden abgeschnitten.                                                                                                                                                                                                                                      | `0` oder, falls `0` kein gültiger Wert für die Eigenschaft ist, der Minimalwert der Eigenschaft.                |
    | `length` {{ experimental_inline() }}                                                                                                                                                                                                                                                                                                                                                      | {{cssxref("&lt;length&gt;")}}     | Der Attributwert wird als CSS {{cssxref("&lt;length&gt;")}} Wert interpretiert, der die Einheit beinhaltet (z. B. `12.5em`). Falls er ungültig ist, d. h. keine Länge oder außerhalb des Bereichs, der von der CSS Eigenschaft akzeptiert wird, wird der Standardwert verwendet. Falls die angegebene Einheit eine relative Länge ist, wandelt `attr()`sie in eine absolute Länge um. Voran- und nachgestellte Leerzeichen werden abgeschnitten.                                                                                      | `0` oder, falls `0` kein gültiger Wert für die Eigenschaft ist, der Minimalwert der Eigenschaft.                |
    | `em`, `ex`, `px`, `rem`, `vw`, `vh`, `vmin`, `vmax`, `mm`, `cm`, `in`, `pt`, oder `pc` {{ experimental_inline() }}                                                                                                                                                                                                                                                                        | {{cssxref("&lt;length&gt;")}}     | Der Attributwert wird als CSS {{cssxref("&lt;number&gt;")}} Wert ohne Einheit interpretiert (z. B. `12.5`) und in einen {{cssxref("&lt;length&gt;")}} Wert mit der angegebenen Einheit umgewandelt. Falls er nicht gültig ist, d. h. keine Zahl oder außerhalb des Bereichs, der von der CSS Eigenschaft akzeptiert wird, wird der Standardwert verwendet. Falls die angegebene Einheit eine relative Länge ist, wandelt `attr()`sie in eine absolute Länge um. Voran- und nachgestellte Leerzeichen werden abgeschnitten. | `0` oder, falls `0` kein gültiger Wert für die Eigenschaft ist, der Minimalwert der Eigenschaft.                |
    | `angle` {{ experimental_inline() }}                                                                                                                                                                                                                                                                                                                                                       | {{ cssxref("&lt;angle&gt;") }}     | Der Attributwert wird als CSS {{ cssxref("&lt;angle&gt;") }} Wert interpretiert, der die Einheit beinhaltet (z. B. `30.5deg`). Falls er ungültig ist, d. h. kein Winkel oder außerhalb des Bereichs, der von der CSS Eigenschaft akzeptiert wird, wird der Standardwert verwendet. Voran- und nachgestellte Leerzeichen werden abgeschnitten.                                                                                                                                                                                          | `0deg` oder, falls `0deg` kein gültiger Wert für die Eigenschaft ist, der Minimalwert der Eigenschaft.          |
    | `deg`, `grad`, `rad` {{ experimental_inline() }}                                                                                                                                                                                                                                                                                                                                          | {{ cssxref("&lt;angle&gt;") }}     | Der Attributwert wird als CSS {{cssxref("&lt;number&gt;")}} Wert ohne Einheit interpretiert (z. B. `12.5`) und in einen {{ cssxref("&lt;angle&gt;") }} Wert mit der angegebenen Einheit umgewandelt. Falls er nicht gültig ist, d. h. keine Zahl oder außerhalb des Bereichs, der von der CSS Eigenschaft akzeptiert wird, wird der Standardwert verwendet. Voran- und nachgestellte Leerzeichen werden abgeschnitten.                                                                                                      | `0deg` oder, falls `0deg` kein gültiger Wert für die Eigenschaft ist, der Minimalwert der Eigenschaft.          |
    | `time` {{ experimental_inline() }}                                                                                                                                                                                                                                                                                                                                                        | {{cssxref("&lt;time&gt;")}}         | Der Attributwert wird als CSS {{cssxref("&lt;time&gt;")}} Wert interpretiert, der die Einheit beinhaltet (z. B. `30.5ms`). Falls er ungültig ist, d. h. keine Zeit oder außerhalb des Bereichs, der von der CSS Eigenschaft akzeptiert wird, wird der Standardwert verwendet. Voran- und nachgestellte Leerzeichen werden abgeschnitten.                                                                                                                                                                                                | `0s` oder, falls `0s` kein gültiger Wert für die Eigenschaft ist, der Minimalwert der Eigenschaft.              |
    | `s`, `ms` {{ experimental_inline() }}                                                                                                                                                                                                                                                                                                                                                     | {{cssxref("&lt;time&gt;")}}         | Der Attributwert wird als CSS {{cssxref("&lt;number&gt;")}} Wert ohne Einheit interpretiert (z. B. `12.5`) und in einen {{cssxref("&lt;time&gt;")}} Wert mit der angegebenen Einheit umgewandelt. Falls er nicht gültig ist, d. h. keine Zeit oder außerhalb des Bereichs, der von der CSS Eigenschaft akzeptiert wird, wird der Standardwert verwendet. Voran- und nachgestellte Leerzeichen werden abgeschnitten.                                                                                                          | `0s` oder, falls `0s` kein gültiger Wert für die Eigenschaft ist, der Minimalwert der Eigenschaft.              |
    | `frequency` {{ experimental_inline() }}                                                                                                                                                                                                                                                                                                                                                   | {{cssxref("&lt;frequency&gt;")}} | Der Attributwert wird als CSS {{cssxref("&lt;frequency&gt;")}} Wert interpretiert, der die Einheit beinhaltet (z. B. `30.5kHz`). Falls er ungültig ist, d. h. keine Frequenz oder außerhalb des Bereichs, der von der CSS Eigenschaft akzeptiert wird, wird der Standardwert verwendet. Voran- und nachgestellte Leerzeichen werden abgeschnitten.                                                                                                                                                                                   | `0Hz` oder, falls `0Hz` kein gültiger Wert für die Eigenschaft ist, der Minimalwert der Eigenschaft.            |
    | `Hz`, `kHz` {{ experimental_inline() }}                                                                                                                                                                                                                                                                                                                                                   | {{cssxref("&lt;frequency&gt;")}} | Der Attributwert wird als CSS {{cssxref("&lt;number&gt;")}} Wert ohne Einheit interpretiert (z. B. `12.5`) und in einen {{cssxref("&lt;frequency&gt;")}} Wert mit der angegebenen Einheit umgewandelt. Falls er nicht gültig ist, d. h. keine Frequenz oder außerhalb des Bereichs, der von der CSS Eigenschaft akzeptiert wird, wird der Standardwert verwendet. Voran- und nachgestellte Leerzeichen werden abgeschnitten.                                                                                              | `0Hz` oder, falls `0Hz` kein gültiger Wert für die Eigenschaft ist, der Minimalwert der Eigenschaft.            |
    | `%` {{ experimental_inline() }}                                                                                                                                                                                                                                                                                                                                                           | {{cssxref("&lt;percentage&gt;")}} | Der Attributwert wird als CSS {{cssxref("&lt;number&gt;")}} Wert ohne Einheit interpretiert (z. B. `12.5`) und in einen {{cssxref("&lt;percentage&gt;")}} Wert umgewandelt. Falls er nicht gültig ist, d. h. keine Zahl oder außerhalb des Bereichs, der von der CSS Eigenschaft akzeptiert wird, wird der Standardwert verwendet. Falls der Wert als Länge verwendet wird, wandelt `attr()`ihn in eine absolute Länge um. Voran- und nachgestellte Leerzeichen werden abgeschnitten.                                      | `0%` oder, falls `0%` kein gültiger Wert für die Eigenschaft ist, der Minimalwert der Eigenschaft.              |
- `<fallback>`
  - : Der Wert, der verwendet wird, falls das zugehörige Attribut fehlt oder einen ungültigen Wert beinhaltet. Der Fallbackwert muss gültig sein, auch wenn er nicht verwendet wird, und darf keinen weiteren `attr()` Ausdruck beinhalten. Falls `attr()` nicht der einzige Wert einer Eigenschaft ist, muss dessen `<fallback>` Wert von dem Typ sein, der durch `<type-or-unit>` definiert wird. Falls nicht angegeben, wird CSS den Standardwert verwenden, der für jeden `<type-or-unit>` Wert angegeben ist.

## Beispiele

```css
p:before {
  content:attr(data-foo) " ";
}
```

```html
<p data-foo="Hallo">Welt</p>
```

### Ergebnis

{{ EmbedLiveSample("Beispiele", '100%', '60') }}

## Spezifikationen

| Spezifikation                                                            | Status                               | Anmerkung                                                                                                                                                                                                                                                                                                                                                               |
| ------------------------------------------------------------------------ | ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| {{ SpecName('CSS3 Values', '#attr', 'attr()') }}         | {{ Spec2('CSS3 Values') }} | Fügt zwei optionale Parameter hinzu; kann in allen Eigenschaften verwendet werden; kann andere Werte als {{cssxref("&lt;string&gt;")}} zurückliefern. Diese Änderungen sind als experimentell {{ experimental_inline() }} markiert und können jederzeit während der CR Phase verworfen werden, falls die Browserunterstützung nicht groß genug ist. |
| {{ SpecName('CSS2.1', 'generate.html#x18', 'attr()') }} | {{ Spec2('CSS2.1') }}         | Beschränkt auf die {{ cssxref("content") }} Eigenschaft; gibt immer {{cssxref("&lt;string&gt;")}} zurück.                                                                                                                                                                                                                                            |

## Browser Kompatibilität

{{Compat("css.types.attr")}}