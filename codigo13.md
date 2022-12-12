# codigo 13
## como funciona
juego de adivinar un numero, con la idea de conocer los errores comunes

## notas
no requiere nada

### codigo 13 erroneo

```bash
#!/bin/bash

biggest=100
guess=0
guesses=0
number=$(( $$ % $biggest )
echo "Guess a number between 1 and $biggest"

while [ "$guess" -ne $number ] ; do
  /bin/echo -n "Guess? " ; read answer
  if [ "$guess" -lt $number ] ; then
    echo "... bigger!"
  elif [ "$guess" -gt $number ] ; then
    echo "... smaller!
  fi
  guesses=$(( $guesses + 1 ))
done

echo "Right!! Guessed $number in $guesses guesses."

exit 0
```

### [codigo 13 correcto](Recipes/13debugging.sh)

```bash
#!/bin/bash

biggest=100
guess=0
guesses=0

number=$(( $RANDOM % $biggest+1 ))
echo "Guess a number between 1 and $biggest"

while [ "$guess" -ne $number ] ; do
    /bin/echo -n "Guess? " ; read guess
    if [ "$guess" -lt $number ] ; then
        echo "... bigger!"
    elif [ "$guess" -gt $number ] ; then
        echo "... smaller!"
    fi
    guesses=$(( $guesses + 1 ))
done

echo "Right!! Guessed $number in $guesses guesses."

exit 0
```
### salidaa 
![salida](Salidas/13.png)

[reesar](README.md)