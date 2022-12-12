# codigo 63
## como funciona
muestra nuestro entorno en formato html

## notas
funciona

### [codigo 6](Recipes/63showCGIenv.sh)

```bash
#!/bin/bash

echo "Content-type: text/html"
echo ""

echo "<html><body bgcolor=\"white\"><h2>CGI Runtime Environment</h2>"
echo "<pre>"
env || printenv
echo "</pre>"
echo "<h3>Input stream is:</h3>"
echo "<pre>"
cat -
echo "(end of input stream)</pre></body></html>"

exit 0
```

[reesar](README.md)