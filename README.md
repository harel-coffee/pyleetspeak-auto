# LeetTransformer :one::three::three::seven::robot:

Under development! Only Basic Leet is available which consists of substituting every vowel for a number. 

- [Installation](#installation)
- [Examples of How to Use](#exmaples-of-how-to-use)


    - [Basic Use](#basic-use)
    - [Get all changes](#get-all-changes)
    - [Define your own changes](#define-your-own-changes)





https://user-images.githubusercontent.com/56938752/147962824-c347e184-14b6-41fe-8b05-ef670ac0a5f9.mp4



## Installation

````
pip install pyleetspeak
````

## Examples of How To Use

The only required argument that the user has to provide is the `text_in` argument which represent the casual text to transform to leetspeak. Nonetheless, there are other optional arguments that control the behaviour of the transformation:`
* `change_prb` determines the probability of a transformation to take place (i.e, if it is equal 1 all the possible transformation will be applied).  
* `change_frq` is affects how frequently a transformation will occur (i.e, if it is equal 1 all the letters of this transformation type will be changed)
* `mode` controls the level of leetspeak transformation. Currently only `basic` mode is available. We are working on more modes. Stay tuned.
* `seed` controls the reproducibility of the results. By default no seed is applied.
* `verbose` controls the verbosity of the proccess.

### Basic Use

Let's see a simple working example:

````python
from pyleetspeak import LeetSpeaker
text_in = "I speak leetspeak"
leeter = LeetSpeaker(text_in, change_prb=0.8,  change_frq=0.6, mode = "basic", seed = None, verbose=False)
leet_result = leeter.text2leet()
print(leet_result)
# "1 spe4k l33tsp34k"
````





For the sake of reproducibility you can set a random seed:

````python
from pyleetspeak import LeetSpeaker
leeter = LeetSpeaker(text_in, change_prb=0.8,  change_frq=0.5, mode = "basic", seed = 42, verbose=False)
leet_result = leeter.text2leet()
print(leet_result)
# "1 sp34k l3etspeak"
````

Minor concerns about the package behaviour: accents are deleted using `Unidecode`. This is important for languages like Spanish, where the word "melocotón" is preprocessed as "melocoton" and finally transformed to leetspeak. 

### Get all changes

You can also obtain all the possible versions of a leetspeak text using the `get_all_combs` parameter like this:

````python
from pyleetspeak import LeetSpeaker
text_in = "leetspeak"
leeter = LeetSpeaker(text_in, mode = "basic", get_all_combs = True)
leet_result = leeter.text2leet()
assert len(leet_result) == 32 # all possible combinations
print(leet_result)
````

### Define your own changes

`pyleetspeak` is prepared to apply substitutions defined by the user. It is essential to highlight that these new user-defined changes have to follow two possible formats, dictionary or List of tuples. Here we show a toy example to add two new target characters from the original text to be replaced by two different characters and one, respectively:

* Dictionary type: {"target_chr_1": ["sub_chr_1", "sub_chr_1"], "target_chr_2": ["sub_chr_1"]}
* List[Tuple] type: [("target_chr_1", ["sub_chr_1", "sub_chr_1"]), (("target_chr_2", ["sub_chr_1"])]

You can add new user-defined substitutions:

````python
from pyleetspeak import LeetSpeaker
text_in = "New changes Leetspeak"
obj = LeetSpeaker(
    text_in,
    change_prb=1,
    change_frq=0.8,
    mode="basic",
    seed=21,
    verbose=False,
    get_all_combs=False,
    user_changes = [("a", "#"), ("s", "$")], # user-defined changes
)
print(obj.text2leet())
# N3w ch@ng3$ L33t$pe4k
````

Moreover, you can use only the user-defined substitutions:

````python
from pyleetspeak import LeetSpeaker
# Only user changes
text_in = "Only user changes: Leetspeak"
obj = LeetSpeaker(
    text_in,
    change_prb=1,
    change_frq=0.8,
    mode=None, # None pre-defined changes will be applied
    seed=21,
    verbose=False,
    get_all_combs=False,
    user_changes = [("a", "#"), ("s", "$")], # user-defined changes
)
print(obj.text2leet())
# Only u$er ch#nge$: Leet$pe#k
````


