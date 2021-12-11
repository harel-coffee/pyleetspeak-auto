# LeetTransformer :one::three::three::seven::robot:

Under development! Only Basic Leet is available which consists of substituting every vowel for a number. 

- [Installation](#installation)
- [Examples of How to Use](#exmaples-of-how-to-use)
## Installation

```
pip install pyleetspeak
```

## Examples of How To Use

The only required argument that the user has to provide is the `text_in` argument which represent the casual text to transform to leetspeak. Nonetheless, there are other optional arguments that control the behaviour of the transformation:`
* `change_prb` determines the probability of a transformation to take place (i.e, if it is equal 1 all the possible transformation will be applied).  
* `change_frq` is affects how frequently a transformation will occur (i.e, if it is equal 1 all the letters of this transformation type will be changed)
* `mode` controls the level of leetspeak transformation. Currently only `basic` mode is available. We are working on more modes. Stay tuned.
* `seed` controls the reproducibility of the results. By default no seed is applied.
* `verbose` controls the verbosity of the proccess.

Let's see a simple working example:

```
from pyleetspeak import LeetSpeaker
text_in = "I speak leetspeak"
leeter = LeetSpeaker(text_in, change_prb=0.8,  change_frq=0.6, mode = "basic", seed = None, verbose=False)
leet_result = leeter.text2leet()
print(leet_result)
# "1 spe4k l33tsp34k"
```



For the sake of reproducibility you can set a random seed:

```
from pyleetspeak import LeetSpeaker
leeter = LeetSpeaker(text_in, change_prb=0.8,  change_frq=0.5, mode = "basic", seed = 42, verbose=False)
leet_result = leeter.text2leet()
print(leet_result)
# "1 sp34k l3etspeak"
```

Minor concerns about the package behaviour: accents are deleted using `Unidecode`. This is important for languages like Spanish, where the word "melocotón" is preprocessed as "melocoton" and finally transformed to leetspeak. 
