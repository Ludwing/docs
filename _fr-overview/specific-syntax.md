---
layout: base
title:  'Syntax'
permalink: fr/overview/specific-syntax.html
udver: '2'
---

# Specific constructions

## Cleft sentences

FrenchSpoken analyzes cleft sentences with [fr-dep/acl:cleft]() when the clefted element is a nominal subject or object. All other clefted elements are analyzed with [fr-dep/ccomp:cleft]().
For cleft sentences constructed with a _c'est_ (or _ce sont_, _c'était_ etc.), the clefted element is the head of the whole cleft sentence and the syntactical subject _c'_ receives a [fr-dep/nsubj:expl]() link.

~~~ sdparse
Notre jardin est vraiment magnifique. C' est notre jardinier qui a tout fait seul ! \n Our garden is truly beautiful. It's our gardener who did everything on his own!
nsubj:expl(jardinier,C')
acl:cleft(jardinier,fait)
nsubj(fait,qui)
~~~

~~~ sdparse
Les temps sont durs. C' est en faisant des compromis qu' on s'en sortira. \n Times are tough. That's by making compromises that we will be able to find a way out of misery.
nusbj:expl(faisant,C')
cop(faisant,est)
ccomp:cleft(faisant,sortira.)
advcl(sortira.,qu')
~~~

~~~ sdparse
Je n'entends pas la télévision. Il y a mon père qui passe l'aspirateur. \n I can't hear the television. My father is vaccuuming the room.
nsubj:expl(a,Il)
advmod(a,y)
obj(a,père)
acl:cleft(père,passe)
nsubj(passe,qui)
~~~ 

N.B.: Presentative constructions must not be mistaken for cleft sentences. FrenchSpoken annotates those two constructions differently.
In a presentative construction the pronoun _c'_ has an antecedent whereas the _c'_ in a cleft sentence does not have one. The _c'_ of a presentative will thus be annotated with a standard [fr-dep/nsubj]() relation and the _c'_ of a cleft sentence will be annotated with the `nsubj:expl` subrelation (see above).
In the following example, _C'_ has an obvious antecedent: _notre jardinier_. The relative clause of the presentative construction is governed by _lui_ with a [fr-dep/acl:relcl]() relation (and not an `acl:cleft` relation).

~~~ sdparse
Notre jardin est vraiment magnifique. C' est un endroit où j' aime venir lire. \n Our garden is truly beautiful. It's a place where I like to come reading.
nsubj(endroit,C')
acl:relcl(endroit,aime)
obl:mod(aime,où)
~~~ 

## Qu'est-ce que ... ?

_qu'est-ce que ..._ is actually a cleft construction. 
For example the sentence _Qu'est-ce que tu lis ?_ (_What are you reading?_) corresponds to the sentence _C'est quoi que tu lis ?_. In the second sentence the cleft construction clearly appears: _quoi_ is the clefted element and _que tu lis_ the clause attached to it.
_Qu'est-ce que ..._ is thus analyzed as a cleft sentence. The first _qu'_ (i.e. the clefted element) is the head of the whole sentence and governs the right part with an [fr-dep/acl:cleft]() link.

~~~ sdparse
Qu' est - ce qu' il a fait ? \n What did he do ?
root(ROOT-0,Qu'-8)
cop(Qu',est)
nsubj:expl(Qu',ce)
acl:cleft(Qu',fait)
obj(fait,qu')
nsubj(fait,il)
~~~

~~~ sdparse
Qu' est - ce que tu as acheté au magasin ? \n What did you buy in the shop?
cop(Qu',est)
nsubj:expl(Qu',ce)
acl:cleft(Qu',acheté)
obj(acheté,que)
nsubj(acheté,tu)
~~~


## Pseudo-cleft sentences

To stay consistent with the analysis made for the cleft sentences, and thus to show the similarities between the two types of constructions, the head of a pseudo-cleft sentence is the element that follows the _c'est_ (or _c'était_ etc.).
This head governs the left part of the pseudo-cleft construction with a [fr-dep/dislocated:cleft]() link. 
However the pronoun _c'_ is not annotated with [fr-dep/nsubj:expl]() (like it is done for clefts). In the case of a pseudo-cleft sentence, it may be considered that _c'_ stands for dislocated complement (i.e. that _c'_ has an antecedent and is not an expletiv), this pronoun is thus annotated with the standard [fr-dep/nsubj]().
The pronoun _ce_ is the head of the left part of the pseudo-cleft and governs the relative clause with a standard [fr-dep/acl:relcl]() link.

~~~ sdparse
Ce que j' aime , c' est le chocolat. \n Chocolate is what I like.
cop(chocolat.,est)
nsubj(chocolat.,c')
dislocated:cleft(chocolat.,Ce)
acl:relcl(Ce,aime)
~~~

~~~ sdparse
Ce qui me fait peur, c' est que tu te casses une jambe. \n What scares me is that you break your leg.
mark(casses,que)
cop(casses,est)
nsubj(casses,c')
dislocated:cleft(casses,Ce)
acl:relcl(Ce,fait)
~~~

### Causative

In French causatives are typically constructed with the verb _faire_. 
The new argument, the causer, which is the subject of the construction is annotated [nsubj:caus](), while the initial subject/agent of the verb is demoted and becomes either an object, an indirect object or an oblique complement of the causative construction.
The head of a causative construction is the infinitive verb, which governs _faire_ with a [fr-dep/aux:caus]() link. The syntactical subject of the sentence (i.e. the causer) is annotated with [fr-dep/nsubj:caus](). The true agent of the action described by the causative will be linked to the infinitive verb by an [fr-dep/obj:agent](), an [fr-dep/iobj:agent]() or an [fr-dep/obl:agent]() relation, depending on the syntactical function it has in the sentence.

~~~ sdparse
J' ai fait changer les roues de la voiture par le garagiste. \n I made the mechanic change the car's wheels.
aux:caus(changer,fait)
nsubj:caus(changer,J')
obj(changer,roues)
obl:agent(changer,garagiste.)
~~~

~~~ sdparse
Ce magicien fait vraiment rêver les enfants. \n This magician really makes the kids dream.
aux:caus(rêver,fait)
nsubj:caus(rêver,magicien)
obj:agent(rêver,enfants.)
~~~

~~~ sdparse
Jean-Jacques n'était jamais venu donc je lui ai fait visiter toute ma maison. \n Jean-Jacques had never been to my place before so I showed him around.
aux:caus(visiter,fait)
nsubj:caus(visiter,je)
iobj:agent(visiter,lui)
obj(visiter,maison.)
~~~

N.B.: For more details about the analysis of causatives, see [this discussion](https://gitlab.inria.fr/sequoia/deep-sequoia/issues/153#) (which is partly in English and partly in French).

### Superlatives

Superlative constructions, _le/la/les plus ADJ_, are annotated as follows:
The head of the construction is the noun. It governs the adjective with the usual [fr-dep/amod]() link and the determiner with a [fr-dep/det]() link. The _plus_ is annotated with an [fr-dep/advmod]() and is a dependant of the adjective.
The noun modifier introduced by the preposition _de_ is attached to the noun even though the noun modifier seems more attached to the superlative: _la plus haute tour du château_ can easily become _la tour la plus haute du château_.

~~~ sdparse
Dans ce rayon se trouvent les plus beaux livres de la bibliothèque. \n On this shelf one can find the most beautiful books in the whole library.
det(livres,les)
amod(livres,beaux)
advmod(beaux,plus)
nmod(livres,bibliothèque.)
case(bibliothèque,de)
~~~

When the superlative is post-posed, the determiner is a dependant of the adjective:

~~~ sdparse
Il aime manger dans les restaurants les plus réputés. \n He likes to eat in the most renowned restaurants.
det(restaurants-6,les-5)
amod(restaurants-6,réputés.-9)
advmod(plus,réputés.)
det(les-7,réputés._9)
~~~ 

When the superlative is in a [fr-dep/cop]() relation (and the noun is not present in the superlative construction), the head of the superlative construction is the adjective:

~~~ sdparse
Ces produits sont les plus vendus. \n These products are best-sellers
det(vendus.,les)
cop(vendus.,sont)
nsubj(vvendus.,produits)
~~~

### Comparatives

In comparative constructions, the adjective is the head. It governs the comparative adverb (_plus_, _moins_, _aussi_ etc.) with an [fr-dep/advmod]() link. The comparison element introduced by _que_ is analyzed with [fr-dep/advcl] and is a dependent of the adjective. _que_ is analyzed with [fr-dep/mark]().
N.B.: Here is the [universal page](http://universaldependencies.org/u/overview/specific-syntax.html#comparatives) for the analysis of comparatives

~~~ sdparse
Mathilde est plus gentille que tu ne le penses. \n Mathilde is kinder than you think.
nsubj(gentille,Mathilde)
cop(gentille,est)
advmod(gentille,plus)
advcl(gentille,penses.)
mark(penses.,que)
~~~

~~~ sdparse
Patrick est aussi courageux que Pierre. \n Patrick is as brave as Pierre.
nsubj(courageux,Patrick)
cop(courageux,est)
advmod(courageux,aussi)
advcl(courageux,Pierre)
mark(Pierre,que)
~~~ 


