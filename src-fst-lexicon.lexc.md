
INTRODUCTION TO MORPHOLOGICAL ANALYSER OF Hungarian LANGUAGE.

# Definitions for Multichar_Symbols

## Analysis symbols
The morphological analyses of wordforms for the Hungarian
language are presented in this system in terms of the following symbols.
(It is highly suggested to follow existing standards when adding new tags).

The parts-of-speech are:

The parts of speech are further split up into:

The Usage extents are marked using following tags:

The nominals are inflected in the following Case and Number

*  +Abl	  Ablative
*  +Acc	  Accusative
*  +Ade	  Adessive
*  +All	  Allative
*  +Cau	  Causative
*  +Del	  Delative
*  +Ela	  Elative
*  +Ess/F	  Formal-Essive
*  +Ess/M	  Modal-Essive
*  +Ill 	  Illative
*  +Ine	  Inessive
*  +Ins	  Instrumental
*  +Nom	  Nominative
*  +Ses	  Superessive
*  +Sla	  Sublative
*  +Ter	  Terminative
*  +Tra	  Translative

The possession is marked as such:
The comparative forms are:
Numerals are classified under:
Verb moods are:
Verb personal forms are:
Other verb forms are

Special symbols are classified with:
The verbs are syntactically split according to transitivity:
Special multiword units are analysed with:
Non-dictionary words can be recognised with:

Question and Focus particles:

Semantics are classified with

Derivations are classified under the morphophonetic form of the suffix, the
source and target part-of-speech.

Morphophonology
To represent phonologic variations in word forms we use the following
symbols in the lexicon files:
*  %^Ö2		 h%^Ö2z
*  %^V2          ház%>%^V2al : házzal
And following triggers to control variation
*  %^Hist          historic documents
*  %^Pen          penultimate position
*  %^RmVow        remove vowel
*  %^V2VV         lengthen vowel
*  %^VV2V         shorten vowel

## Flag diacritics
POSSESSOR INDICES or POSSESSIVE SUFFIXES
FRONT/BACK VOWEL HARMONY
|  @C.VOWEL-HARMONY@ | used at word boundary

We have manually optimised the structure of our lexicon using following
flag diacritics to restrict morhpological combinatorics - only allow compounds
with verbs if the verb is further derived into a noun again:
|  @P.NeedNoun.ON@ | (Dis)allow compounds with verbs unless nominalised
|  @D.NeedNoun.ON@ | (Dis)allow compounds with verbs unless nominalised
|  @C.NeedNoun@ | (Dis)allow compounds with verbs unless nominalised

For languages that allow compounding, the following flag diacritics are needed
to control position-based compounding restrictions for nominals. Their use is
handled automatically if combined with +CmpN/xxx tags. If not used, they will
do no harm.
|  @P.CmpFrst.FALSE@ | Require that words tagged as such only appear first
|  @D.CmpPref.TRUE@ | Block such words from entering ENDLEX
|  @P.CmpPref.FALSE@ | Block these words from making further compounds
|  @D.CmpLast.TRUE@ | Block such words from entering R
|  @D.CmpNone.TRUE@ | Combines with the next tag to prohibit compounding
|  @U.CmpNone.FALSE@ | Combines with the prev tag to prohibit compounding
|  @P.CmpOnly.TRUE@ | Sets a flag to indicate that the word has passed R
|  @D.CmpOnly.FALSE@ | Disallow words coming directly from root.

Use the following flag diacritics to control downcasing of derived proper
nouns (e.g. Finnish Pariisi -> pariisilainen). See e.g. North Sámi for how to use
these flags. There exists a ready-made regex that will do the actual down-casing
given the proper use of these flags.
|  @U.Cap.Obl@ | Allowing downcasing of derived names: deatnulasj.
|  @U.Cap.Opt@ | Allowing downcasing of derived names: deatnulasj.

The word forms in UNDEFINED language start from the lexeme roots of basic
word classes, or optionally from prefixes:

Adjective inflection
The UNDEFINED language adjectives compare.

Noun inflection
The HUNGARIAN language nouns inflect in cases.

Proper noun inflection
The HUNGARIAN language proper nouns inflect in the same cases as regular
nouns, but with a colon (':') as separator.

Verb inflection
The UNDEFINED language verbs inflect in persons.

Adjectives
Adjectives in UNDEFINED language describe things.

Nouns
Nouns in HUNGARIAN language are things.

new code

Numerals
Numerals in UNDEFINED language are numbers.

Prefixes
Prefixes in UNDEFINED language are bound to beginning of other words.

Pronouns
Pronouns in UNDEFINED language are references to things.

Proper nouns
Proper nouns in the HUNGARIAN language are references to things.

Verbs
Verbs in UNDEFINED language are actions.

* * *

<small>This (part of) documentation was generated from [src/fst/lexicon.lexc](https://github.com/giellalt/lang-hun/blob/main/src/fst/lexicon.lexc)</small>
