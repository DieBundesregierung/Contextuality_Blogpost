# Introduction

**Daniel: an idea for the \"same\" story with different characters is to
use the plot of the book Around the world in 80 days (I never read the
book but I know that the story contains exactly the phenomenon we want
to illustrate - the guy finishes the trip around the world and then
realizes he's one day behind what he expected). I can work on that, if
you think it's a good idea.\
Ioannis: If it's ok with you I'll just change the year a bit and remove
the name.**

The year is 1530, you are a ship navigator, and, seized by the
adventurous spirit of the time, you decide to join an adventurous crew
on their quest to circumnavigate earth. Month after month, you observe
the stars to keep track of your location and count the sunrises to keep
track of time. When you finally arrive back at you home port, the crew,
to its surprise, finds no consensus with the locals on what day it is --
the locals seem to be one day ahead. As their navigator, you educate
them about how circumnavigating the planet leads to a one-day offset.
But there is something about your explanation that you yourself cannot
quite wrap your head around: while interacting with the tribes,
kingdoms, and empires you passed on your voyage, you realized that they
had no trouble communicating about time with the cultures adjacent to
them -- everywhere on earth, people seemed to agree that their neighbors
to the east are a bit ahead in their day, while the neighbors to the
west are behind. In each local patch, this way of modeling date and time
was coherent, yet it could not be extended globally. Congratulations,
you just discovered a contextual model, i.e. a model that is locally
coherent everywhere, but is not consistent globally. [^1]. Ultimately,
the introduction of the international dateline eliminated contextuality
from global time-keeping and thus paved the way for global
communication. It would thus take many more centuries until the concept
of contextuality gained attention when it appeared in quantum mechanics,
where it has now been declared to be one of the magical, and impossible
to grasp quantum effects. In this blog post, we attempt to demystify the
concept of contextuality. We do that by describing two contextual
models 1) a very intuitive model of time zones for you the navigator, 2)
an artificial minimal contextual model. For that purpose we adopt the
perspective presented in the paper \"Closing Bell: Boxing black box
simulations in the resource theory of contextuality\" by R. S. Barbosa,
M. Karvonen, and S. Mansfield. We describe their category in which
contextual and non-contextual models live and construct our desired
examples as objects of it. In the end we go on to elaborate on
connections between their framework and game theory.

# Measurement Scenarios and Events

To have a precise notion of a contextual model, we need to describe the
*measurement scenario* in which such a model can appear. A measurement
scenario $S$ consists of a finite set of possible measurements $X_S$, a
finite set of outcomes $(O_{S,x})_{x\in X_S}$ for each measurement
$x \in X_S$, and a set $\Sigma_S \subseteq \mathcal{P}(X_S)$ that
contains precisely the sets of measurements $\sigma \subseteq X_S$ that
can be performed simultaneously. Let us take a closer look at what
structure $\Sigma_S$ must have. Surely we can always do only a single
measurement or even no measurement at all, meaning that $\Sigma_S$
definitely contains all the singletons as well as the empty set.
Furthermore, if we have a set of measurements that can be performed
simultaneously, then any subset of it is also a set of measurements that
can be carried out at the same time, i.e.
$\sigma\in \Sigma_S \land \sigma'\subseteq \sigma \Longrightarrow \sigma'\in \Sigma_S$.
These conditions on $\Sigma_S$ are exactly the axioms of a simplicial
complex. Now an event in a scenario $S$ can be modeled with the *event
sheaf* $$\begin{align*}
    \mathcal{E}_S : \mathcal{P}(X_S)^{op} &\longrightarrow \mathrm{FinSet}\\
    U &\longmapsto \prod_{x \in U} O_{S,x}\\
    U \subseteq V & \longmapsto \left(\prod_{x \in V} \!\!O_{S,x}\, \xrightarrow{\pi} \,\prod_{x \in U}\!\! O_{S,x}\! \right)
\end{align*}$$

Now let's formally build scenarios for each of our desired example
models. We build our contextual time-zone model in a measurement
scenario $T\!Z = (X_{TZ}, \Sigma_{TZ}, (O_{TZ,x})_{x\in X_{TZ}})$. As
the set of measurements we choose the set of $24$ time zones that you
cross on your voyage $$X_{TZ} = \{0,..,23\}.$$ For the set of outcomes,
we choose the possible days and time
$$O_{TZ,x} = \{0,...,364\} \times \{0,...,23\}.$$ Note that the possible
outcomes are the same for each measurement, which amounts to assuming
that everyone divides their year into $365$ days and a day into $24$
hours, a simplifying assumption. Our contexts are sets of neighboring
time zones (and their subsets):
$$\Sigma_{TZ} = \big\{\, \sigma~ \big|~ \exists n\in X_{TZ}.~\sigma \subseteq \{n,n+1\}\big\},$$
where $n+1$ is understood to be modulo $24$. Let it be clear that there
are many alternative ways this could have been set up, we attempted to
pick a intuitive one.

Our minimal contextual model occurs in a measurement scenario we name
$M = (X_{M}, \Sigma_{M}, (O_{M,x})_{x\in X_{M}})$. It consists of merely
three measurements $$X_M = \{a,b,c\}$$ with two possible outcomes
respectively $$O_{M,x} = \{0,1\}.$$ You can perform each combination of
measurements, but not all three at the same time, i.e.
$$\Sigma_M = \mathcal{P}(X_M)\setminus \{a,b,c\}.$$

Having fixed scenarios $T\!Z$ and $M$, we can go on to describe the
actual models.

# Empirical models

The next step is to encode the outcomes that are actually observed once
the measurements are performed simultaneously within each given context.
This is captured by the notion of an *empirical model*.

Let's consider again our time zone example, to understand what we
actually want an empirical model to be. Imagine two cultures, $(A)$ the
culture of the Alice's and in their neighboring time zone to the east
$(B)$ the culture of the Bob's. Upon first contact with each other, they
decide to create a mutual time system: at any moment, they can look at
their clock-calendar and see an ordered pair
$$(d,h) \in \{0,...,364\} \times \{0,...,23\}\,.$$ However, the fact
that they're in neighboring time zones puts a constraint on the
outcomes! If they check the time simultaneously, the only possible joint
outcomes are the ones where the Bob's are one hour ahead, i.e. pairs
$((d_A,h_A),(d_B,h_B))$ such that

- either $0 \le h_A = h_B - 1 \le 22$ and $d_A = d_B$,

- or $h_A = 23$, $h_B = 0$, and $d_B = d_A + 1$ (modulo $365$).

An empirical model is a set of distributions over the outcomes of the
contexts, that captures such compatibility conditions. To formalize
this, consider the functor $D:\text{FinSet} \rightarrow \text{Set}$ that
sends a set $X$ to the set $D(X)$ of all probability distributions on it
-- maps $e:X \rightarrow [0,1]$ such that $\sum_{x \in X}e(x) = 1$ --,
and sends $f:X \rightarrow Y$ to the marginalization function
$f_*:D(X) \rightarrow D(Y)$ given by
$f_*(e)(y) = \sum_{x \in f^{-1}(y)}e(x)$. A *(probabilistic) empirical
model* on a measurement scenario
$S = (X_S,\Sigma_S, (O_{S,x})_{x \in X_S})$ is a global section $e$ of
the composite functor
$$D \circ \mathcal E_S: \mathcal P(X_S)^{op} \longrightarrow \text{FinSet}.$$
In other words, it specifies for each context $U$ a probability
distribution $e_U$ on the set of joint outcomes
$\prod_{x \in U}O_{S,x}$, subject to the condition that $e_U, e_{U'}$
always coincide when marginalized to $U \cap U'$.

Analogously, a *possibilistic empirical model* in a scenario $S$, is a
section $e$ of the composite functor
$$D_{\mathbb{B}} \circ \mathcal E_S: \mathcal P(X_S)^{op} \longrightarrow \text{FinSet}.$$
where $D_\mathbb{B}$ is the Boolean distribution functor (a Boolean
distribution on a set $X$ is a function $e : X \rightarrow \{0,1\}$,
such that $\lor_{x\in X}e(x) = 1$).

We now build the possibilistic contextual model of our time zone
example. Given a context $\{n,n+1\}\in \Sigma_{TZ}$, i.e. a pair of
neighboring time zones, then the boolean distribution $e_{\{n,n+1\}}$ is
defined as: $$\begin{align*}
    e_{\{n,n+1\}}\left((d_A,h_A),(d_B,h_B)\right) = 1 &&:\Longleftrightarrow && \begin{cases}
        d_B = d_A \;\land\; h_B = h_A+1, &h_A < 23\\
        d_B = d_A+1\; \land\; h_B = 0,& h_A = 23.
    \end{cases}
\end{align*}$$

So what makes this a *contextual* model? Contextuality is the
impossibility of the distributions to glue together to a global one.
More precisely, a model $e$ in a scenario $S$ is contextual, if there is
no global distribution $d$ on global outcomes
$\prod_{x\in X_S} O_{S,x}$, such that
$d_\sigma = e_\sigma\,\forall \sigma \in \Sigma_S$. Clearly our time
zone model is contextual, since there is no global arrangement of date
and time, such that neighboring time-zones are always one hour apart.
This example exhibits an extreme notion of contextuality, namely
*strong* contextuality. We will see a weaker notion of contextuality in
our next example.

Let's build a probabilistic model on our measurement scenario $M$. We
need to specify compatible probability distributions on the contexts. We
display the three distributions in the following table.

      $e$      $(0,0)$   $(0,1)$   $(1,0)$   $(1,1)$
  ----------- --------- --------- --------- ---------
   $\{a,b\}$    $1/2$      $0$       $0$      $1/2$
   $\{b,c\}$    $3/8$     $1/8$     $1/8$     $3/8$
   $\{c,a\}$    $1/8$     $3/8$     $3/8$     $1/8$

Note that they are indeed compatible, the probability that e.g. $a=0$ is
$1/2\,$ according to both $e_{\{a,b\}}$ and $e_{\{c,a\}}$. Taking a
closer look at the distributions, we can note the following:
distribution $e_{\{a,b\}}$ is such that $a$ and $b$ are always equal and
$e_{\{b,c\}}$ is such that $b$ is very likely to be equal to be equal.
However, $e_{\{c,a\}}$ is such that $a$ and $c$ are very likely to be
unequal. Obviously, there is no global distribution on the outcomes of
$\{a,b,c\}$ that can capture that. This is a weak notion of
contextuality, since it appears only on the level of probabilities.
There are globally consistent outcomes, like $(0,0,0)$, it is just that
the three distributions cannot agree on the probability with which they
occur. This is in contrast to the time zone model, where a globally
consistent outcome, i.e. a global assignment of date and time, was not
even possible.

With this section we hope to have demystified the concept of
contextuality for you the navigator. It is a property of a collection of
distributions and can occur even in intuitive settings like time zones.

# Maps of scenarios

For two scenarios $S$ and $T$, a *deterministic map*
$f = (\pi_f,\alpha_f):S \rightarrow T$ consists of

- a relation $\pi_f \subset X_T \times X_S$ that is simplicial in the
  sense that for all $U \in \Sigma_S$,
  $$\pi_f(U) := \{x \in X_S \mid (y,x) \in \pi_f \text{ for some } y \in X_T\}$$
  belongs to $\Sigma_T$;

- for each $y \in X_T$, a function
  $\alpha_{f,y}:\mathcal E_S(\pi_f(y)) \rightarrow \mathcal E_T(y)$.

These data can be used to transport empirical models from $S$ to $T$,
or, from another perspective, to simulate a model of $S$ from a model of
$T$. Writing $\text{EMP}(-)$ for the set of empirical models of a given
scenario, we have a map
$\text{EMP}(f):\text{EMP}(S) \rightarrow \text{EMP}(T)$ given by
$$(\text{EMP}(f)e)_U = \alpha_{f,U*}(e_{\pi_f(U)}).$$ That is, in order
to obtain a probability distribution on a context $U \in \Sigma_T$, we
take the distribution on $\mathcal E_S(\pi_f(U))$ provided by $e$ and
push it forward along
$\alpha_{f,U}:\mathcal E_S(\pi_f(U)) \rightarrow \mathcal E_T(U)$. In
fact, since empirical models on a given scenario form a convex set, we
can transport them along any formal convex combination of deterministic
maps via the formula
$$\text{EMP}(\sum_{i} a_if_i)e = \sum_{i \in I}a_i\text{EMP}(f_i)(e).$$
Such a $f = \sum_i a_i f_i$ is called a *probabilistic map*.

This language allows us, for example, to view contextuality in a
relative way: writing $Z$ for the scenario with an empty set of
measurements, thus with a unique empirical model $z$, it can be shown
that a model $e$ of $S$ is *not* contextual if and only if there exists
a probabilistic map $f:Z \rightarrow S$ such that
$\text{EMP}(f)(z) = e$. That is, contextuality is equivalent to
non-simulability from $z$.

# Encoding non-local games as simulations

As a neat application of the category of scenarios, the authors of LINK
describe *non-local games* as certain probabilistic maps. Picture the
following situation: a number of players -- say $n$, but often one
considers $2$ -- are collaboratively trying to win a game posed by a
referee. For $i = 1$, \..., $n$, the referee sends to the $i$-th player
a question drawn from a set $Q_i$, and this is done according to a
probability distribution on $Q_1 \times \cdots \times Q_n$. The $i$-th
player must provide an answer from a set $A_i$, and the game's result is
determined by a "rule\" function
$$Q_1 \times \cdots \times Q_n \times A_1 \times \cdots \times A_n \rightarrow \{0,1\}$$
where $1$ means that they win, and $0$ that they lose. The players, who
have access to both the distribution on tuples of questions and the rule
function, can agree on a strategy before the game starts, but they
cannot communicate afterwards; each of them doesn't know what questions
were asked to other players or what they answered. Their goal is to
maximize the probability of winning.

A strategy in a classical sense is given by just choosing a map
$Q_i \rightarrow A_i$ for each $i$, and this leads to the *classical
value* of the game: the highest winning probability among all classical
strategies. However (and this is how non-local games connect with
quantum information theory!), we can consider a kind of strategy where
there can be correlations between the answers given by different
players, even though the probability of a player giving a certain answer
to a certain question doesn't depend on what others have been asked. In
this broader sense, a strategy can be encoded by a probability
distribution $$e_{q_1, ..., q_n} \in D(A_1 \times \cdots \times A_n)$$
for each tuple of questions $(q_1, ..., q_n)$ in a way that is
compatible with marginalizing to smaller tuples of questions: for
$I \subset \{1, ..., n\}$ and tuples $(q_1, ..., q_n)$,
$(q'_1, ..., q'_n)$ such that $q_i = q'_i$ for $i \in I$, we have
$$\sum_{(a_i)_{i \notin I} \in \prod_{i \notin I} A_i} e_{q_1, ..., q_n}(a_1, ..., a_n) = \sum_{(a'_i)_{i \notin I} \in \prod_{i \notin I} A_i} e_{q'_1, ..., q'_n}(a'_1, ..., a'_n)$$
provided that $a_i = a'_i$ for $i \in I$. An interesting point is that
there exist games that admit a strategy in the generalized sense whose
winning probability is higher than that of any classical strategy. This
can be used, in certain cases, to obtain numerical values attesting that
a quantum-mechanical system is behaving in a non-classical way. LINK
HERE

We express a non-local game as a probabilistic map of scenarios in the
following way:

- let $S$ be the scenario whose set of measurements is
  $Q_1 \sqcup \cdots \sqcup Q_n$, whose maximal contexts are the sets
  $\{q_1, ..., q_n\}$ containing exactly one question for each player,
  and whose set of outcomes for each $q \in Q_i$ is the set of answers
  $A_i$;

- let $[2]$ be the scenario with a single measurement and two possible
  outcomes, $0$ and $1$.

The probability distribution on $Q_1 \times \cdots \times Q_n$ and the
rule function can be described as a probabilistic map
$g:S \rightarrow [2]$. Moreover, a strategy can be encoded as an
empirical model $e \in \text{EMP}(S)$, and its push-forward
$\text{EMP}(g)(e)$ (which is a probability distribution on $\{0, 1\}$,
and therefore corresponds to a value $p \in [0,1]$) gives the winning
probability of the strategy.

This approach suggests considering the slice category $\text{Scen}/[2]$
-- where $\text{Scen}$ consists of scenarios and probabilistic maps --
as a candidate "category of non-local games\". Informally, we can think
of a morphism
$$\bigg(g:S \rightarrow [2]\bigg) \longrightarrow \bigg(g':T \rightarrow [2] \bigg)$$
MAYBE REPLACE THIS BY JUST A COMMUTATIVE TRIANGLE a form of
communication between the players from the two scenarios that allows
those in $T$ to obtain a strategy for their own game by translating, in
a way that preserves the winning probability, any strategy that the
players in $S$ might have. The definition of a map of scenarios tells us
that questions in $T$ are sent to convex mixtures of questions in $S$,
and tuples of answers in $S$ are sent to convex mixtures of answers in
$T$ compatibly with the map on questions; compatibility of
$S \rightarrow T$ with $g$ and $g'$ means that the former respects, in a
certain sense, the rule functions and the distributions on sets of
tuples of questions. On the other hand, functoriality of
$S \mapsto \text{EMP}(S)$ allows us to transport strategies.

This way of expressing non-local games suggests many questions. For
example, how does this connect with the theory of synchronous games
(where the possible questions and answers are the same for all players)
and the construction of \*-algebras from those? Does synchronicity admit
a categorical formulation, and is the passage to \*-algebras part of an
adjunction? Also, can we give a categorical description of algebraic
operations on games, such as parallel repetition and Boolean operations?

It's worth mentioning that the candidate category of games
$\text{Scen}/[2]$ includes structures more general than the ones we
considered earlier. Indeed, the maps $g:S \rightarrow [2]$ obtained via
our explicit construction are far from arbitrary: $S$ is determined by a
complete $n$-partite graph (where $n$ is the number of players), and $g$
is constrained by (1) the rule function being two-valued (win or lose,
nothing in between), and (2) the fact that the referee always asks a
question to *every* player. It would be nice to explore what the extra
flexibility given by $\text{Scen}/[2]$ buys us, both in terms of
categorical structure and the possibility of regarding further
structures as games of a generalized kind.

---------------------------------------------------------- DELETE BELOW
(JUST SKETCH)

Tentative checklist of ideas to be covered:

- contextual models

- different forms of contextuality

- morphisms of scenarios (+ \"black box\" point of view)

- describing contextuality in terms of simulability

- non-local games -- some example of quantum strategy whose winning
  probability is higher than any classical strategy

- suggest the definition of category of non-local games (slice over
  $[2]$)

- questions to be addressed:

  - desirable properties/constructions to be expressible in a
    categorical way

  - is it interesting to restrict to special subcategories (like
    restricting to coherence spaces)?

\*\*\*possible question to state at the end\*\*\*\
Is there a formalism that refines the one of measurement scenarios in
the sense that we can actually encode to what extent a set of
measurements fails to be a scenario, and where we can actually encode
how taking a particular measurement affects others?

\*\*\*\* another question \*\*\*\*\
what concepts other than simulability can be expressed in a relative
way?

[^1]: This tale, while loosely tied to actual historical events, is not
    based on a real story; you are indeed not a ship navigator in the
    16th century.