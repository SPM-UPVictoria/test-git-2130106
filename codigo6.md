# codigo 6
## como funciona
Este codigo valida el formato de un float 

## notas
necesita codigo 5

### [codigo 5](Recipes/5validInt.sh)

```bash
#!/bin/bash

validint()
{
  number="$1";      min="$2";      max="$3"

  if [ -z $number ] ; then
    echo "You didn't enter anything. Please enter a number." >&2 ; return 1
  fi

  if [ "${number%${number#?}}" = "-" ] ; then
    testvalue="${number#?}"
  else
    testvalue="$number"
  fi
  
  nodigits="$(echo $testvalue | sed 's/[[:digit:]]//g')"
  
  if [ ! -z $nodigits ] ; then
    echo "Invalid number format! Only digits, no commas, spaces, etc" >&2
    return 1
  fi
  
  if [ ! -z $min ] ; then
    if [ "$number" -lt "$min" ] ; then
      #echo "$number is too small: smallest acceptable value is $min" >&2
      return 1
    fi
  fi
  if [ ! -z $max ] ; then
    if [ "$number" -gt "$max" ] ; then
      #echo "Your value is too big: largest acceptable value is $max" >&2
      return 1
    fi
  fi
  return 0
}

```

### [codigo 6](Recipes/6validateFloat.sh)

```bash
#!/bin/bash

. validInt5.sh

validfloat()
{
  fvalue="$1"
  if [ ! -z $(echo $fvalue | sed 's/[^.]//g') ] ; then
    decimalPart="$(echo $fvalue | cut -d. -f1)"
    fractionalPart="${fvalue#*\.}"

    if [ ! -z $decimalPart ] ; then
      if ! validint "$decimalPart" "" "" ; then
        return 1
      fi 
    fi

    if [ "${fractionalPart%${fractionalPart#?}}" = "-" ] ; then
      echo "Invalid floating-point number: '-' not allowed \
        after decimal point" >&2
      return 1
    fi 
    if [ "$fractionalPart" != "" ] ; then 
      if ! validint "$fractionalPart" "0" "" ; then
        return 1
      fi
    fi
  else 
    if [ "$fvalue" = "-" ] ; then
      echo "Invalid floating-point format." >&2 ; return 1
    fi

    if ! validint "$fvalue" "" "" ; then
      return 1
    fi
  fi

  return 0
}

if validfloat $1 ; then
  echo "$1 is a valid floating-point value"
fi

exit 0

```
### salidaa 
![salida](Salidas/6.png)

[reesar](README.md)