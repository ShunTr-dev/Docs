# Fechas

## Formateo de fechas con traducciones
From [Midudev](https://twitter.com/midudev/status/1758135000632017368)

```javascript
const format = (date, locale, options) => new Intl.DateTimeFormat(locale, options).format(date)
const now = new Date()

format(now, es) // -> dd/mm/yyyy
format(now, en) // -> mm/dd/yyyy

format(now, 'es', { dateStyle: 'long' }) // -> '13 de abril de 2024'

format(now, 'en', { weekday: 'short', day: 'numeric' }) // -> '13 Thu'
```

# Librerías

## [TEMPO](https://tempo.formkit.com/)
The easiest way to work with dates in JavaScript. -> Sólo ocupa 5KB