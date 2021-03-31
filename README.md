# Agoric-Validator-Jail-Alerter
This is a simple shell script to continuously poll your Agoric Validator status and alert you when your validator is jailed.


```
while sleep 5; do
  info=`ag-cosmos-helper query staking validators --limit=10000 --output=json 2<&1 | jq '.validators[] | select(.description.moniker=="<YOUR-MONIKER>")'`
  if test `echo "$info" | jq -r .jailed` == true; then
    echo "VALIDATOR HAS BEEN JAILED"
    #ring bell sound from terminal
    echo -ne '\007'
  fi
done
```
