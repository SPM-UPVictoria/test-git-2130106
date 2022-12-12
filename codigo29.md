# codigo 29
## como funciona
muestra contenido e informacion de un documento

## notas
necesitas seleccionar un documento

### [codigo 29](Recipes/29fileDetalles.sh)

```bash
#!/bin/bash

width=72
for input
do
  echo $input
  lines="$(wc -l < $input | sed 's/ //g')"
  chars="$(wc -c < $input | sed 's/ //g')"
  owner="$(ls -ld $input | awk '{print $3}')"
  echo "-----------------------------------------------------------------"
  echo "File $input ($lines lines, $chars characters, owned by $owner):"
  echo "-----------------------------------------------------------------"
  while read line 
  do
    if [ ${#line} -gt $width ] ; then
      echo "$line" | fmt | sed -e '1s/^/  /' -e '2,$s/^/+ /'
    else
      echo "  $line"
    fi
  done < $input

  echo "-----------------------------------------------------------------"

done | ${PAGER:more}

exit 0
```

[regresar](README.md)