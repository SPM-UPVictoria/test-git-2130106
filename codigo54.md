# codigo 54
## como funciona
muestra links dentro de una pagina

## notas
necesita internet

### [codigo 54](Recipes/54getLinks.sh)

```bash
#!/bin/bash

if [ $# -eq 0 ] ; then
  echo "Usage: $0 [-d|-i|-x] url"  >&2
  echo "-d=domains only, -i=internal refs only, -x=external only" >&2
  exit 1
fi

if [ $# -gt 1 ] ; then
  case "$1" in
    -d) lastcmd="cut -d/ -f3 | sort | uniq"
        shift
        ;;
    -r) basedomain="http://$(echo $2 | cut -d/ -f3)/"
        lastcmd="grep \"^$basedomain\" | sed \"s|$basedomain||g\" | sort |\
	     uniq"
        shift
        ;;
    -a) basedomain="http://$(echo $2 | cut -d/ -f3)/"
        lastcmd="grep -v \"^$basedomain\" | sort | uniq"
        shift
        ;;
     *) echo "$0: unknown option specified: $1" >&2; exit 1
  esac
else
  lastcmd="sort | uniq"
fi

lynx -dump "$1" | \
sed -n '/^References$/,$p' | \
  grep -E '[[:digit:]]+\.' | \
  awk '{print $2}' | \
  cut -d\? -f1 | \
eval $lastcmd

exit 0
```
### salidaa 
![salida](Salidas/54.png)

[reesar](README.md)