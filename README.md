# lapwing-fkeys
[Plover](https://www.openstenoproject.org/plover/) dictionary for F-keys using [Lapwing numbers](https://lapwing.aerick.ca/Chapter-18.html).

* Combine `#TP` with a number on the Lapwing numpad to press the corresponding F-key.

* Add `S-` for Shift, `K-` for Control, and `W-` for Alt.

* For F10, use `#TP-RS`. (This avoids conflicts with `#TPER` as in `Fermi`.) F11 is `#TP-RG`, and F12 is `#TP-RB`.

A video demonstrating the "extended numpad" with 10, 11, 12:

https://github.com/user-attachments/assets/9e5cbd52-921a-46f6-8df0-29a85b8255a0

## Python code to generate this dictionary

```py
import json

starters = [
    ("#TP", "{#f%d}{^}"),
    ("#STP", "{#shift_l(f%d)}{^}"),
    ("#TKP", "{#control_l(f%d)}{^}"),
    ("#STKP", "{#shift_l(control_l(f%d))}{^}"),
    ("#TPW", "{#alt_l(f%d)}{^}"),
    ("#STPW", "{#shift_l(alt_l(f%d))}{^}"),
    ("#TKPW", "{#control_l(alt_l(f%d))}{^}"),
    ("#STKPW", "{#shift_l(control_l(alt_l(f%d)))}{^}"),
]
ends = "-R -B -G -FR -PB -LG -F -P -L -RS -RG -RB".split()
dictionary = {l+r: f%n for (l,f) in starters for (n,r) in enumerate(ends, 1)}
print(json.dumps(dictionary))
```
