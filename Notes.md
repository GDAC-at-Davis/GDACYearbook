To return to the main file after ending a bitsy game:

At the end of this callback:

```
function startEndingDialog(ending) {
    ...

    startDialog(
        endingDialogStr,
        endingScriptId,
        function () {
            var isLocked = ending.property && ending.property.locked === true;
            if (isLocked) {
                isEnding = false;

                // if the ending was cancelled, restart the music
                // todo : should it resume from where it started? (right now it starts over)
                if (tmpTuneId && soundPlayer && !soundPlayer.isTunePlaying()) {
                    soundPlayer.playTune(tune[tmpTuneId]);
                }
            }
        },
        ending);

}
```

replace with

```

startDialog(
    endingDialogStr,
    endingScriptId,
    function () {
        var isLocked = ending.property && ending.property.locked === true;
        if (isLocked) {
            isEnding = false;

            // if the ending was cancelled, restart the music
            // todo : should it resume from where it started? (right now it starts over)
            if (tmpTuneId && soundPlayer && !soundPlayer.isTunePlaying()) {
                soundPlayer.playTune(tune[tmpTuneId]);
            }
        }
        else
        {
            // Go back to index.html when the ending dialog is finished
            console.log("GOING BACK TO INDEX");
            window.open("index.html", "_self");
        }
    },
    ending);

```

So after the bitsy game ends, it returns to the select page.
