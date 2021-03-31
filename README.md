# Agoric-Validator-Jail-Alerter
This is a simple shell script to continuously poll your Agoric Validator status and alert you (both with audio and text) when your validator is jailed.

Simply change <YOUR-MONIKER> to your agoric testnet moniker, then copy and paste the block of code into your terminal, and let it run continuously with the terminal window open.


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
