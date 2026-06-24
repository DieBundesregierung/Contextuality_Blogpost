# Introduction

The year is 1519, you are a ship navigator, and, seized by the
adventurous spirit of the time, you decide to join Magellan's crew on
their quest to circumnavigate the planet. Month after month you observe
the stars to keep track of your location and count the sunrises to keep
track of time. When you finally arrive back in Spain, the crew, to its
surprise, finds no consensus with the locals on what day it is -- the
locals seem to be one day ahead. As their navigator, you educate them
about how circumnavigating the planet leads to a one-day offset. But
there is something about your explanation that you yourself cannot quite
wrap your head around: While interacting with the tribes, kingdoms, and
empires you passed on your voyage, you realized that they had no trouble
communicating about time with the cultures adjacent to them --
everywhere on earth, people seemed to agree that their neighbors to the
east are a bit ahead in their day, while the neighbors to the west are
behind. In each local patch, this way of modeling date and time was
coherent, yet it could not be extended globally. Congratulations, you
just discovered a contextual model [^1]. Ultimately, the introduction of
the international dateline eliminated contextuality from global
time-keeping and thus paved the way for global communication. It would
thus take many more centuries until the concept of contextuality gained
attention when it appeared in quantum mechanics, where it has now been
declared to be one of the magical, and impossible to grasp quantum
effects. In this blog post, we attempt to demystify the concept of
contextuality. For that we adopt the perspective presented in the paper
\"Closing Bell: Boxing black box simulations in the resource theory of
contextuality\" by R. S. Barbosa, M. Karvonen, and S. Mansfield. We go
over their categorical framework and as an instance of it create two
contextual models, 1) a very intuitive model of time zones for you the
navigator, 2) an artificial minimal non-trivial contextual model.

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

We will build our contextual time-zone model in a measurement scenario
$T\!Z = (X_{TZ}, \Sigma_{TZ}, (O_{TZ,x})_{x\in X_{TZ}})$. Its set of
measurements is the set of $24$ time zones that you cross on your voyage
$$X_{TZ} = \{0,..,23\}.$$ For the set of outcomes, we choose the
possible days and time $$O_{TZ,x} = \{0,...,364\} \times \{0,...,23\}.$$
Note that the possible outcomes are the same for each measurement, which
amounts to assuming that everyone divides their year into $365$ days and
a day into $24$ hours, a simplifying assumption. The maximal contexts
that $\Sigma_{TZ}$ could contain are the sets consisting of $12$
consecutive time zones; we will however go with a simpler option where
the contexts are sets of neighboring zones (and their subsets):
$$\Sigma_{TZ} = \big\{\, \sigma~ \big|~ \exists t\in X_{TZ}.~\sigma \subseteq \{t,t+1\}\big\},$$
where $t+1$ is understood to be modulo $24$.

Our minimal non-trivial model occurs in a measurement scenario we name
$M = (X_{M}, \Sigma_{M}, (O_{M,x})_{x\in X_{M}})$. It consists of three
measurements $$X_M = \{a,b,c\}$$ with two possible outcomes respectively
$$O_{M,x} = \{0,1\}.$$ You can perform each combination of measurements,
but not all three at the same time, i.e.
$$\Sigma_M = \mathcal{P}(X_M)\setminus \{a,b,c\}.$$

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

Let's build a probabilistic model on our measurement scenario $M$.

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

Another neat application of the category of scenarios is the description
of *non-local games* as certain probabilistic maps. Picture the
following situation: a number of players -- say $n$, but often one
considers $2$ -- are collaboratively trying to win a game posed by a
referee. For $i = 1$, \..., $n$, the referee sends to the $i$-th player
a question drawn from a set $Q_i$, and this is done according to a
probability distribution on $Q_1 \times \cdots \times Q_n$. The $i$-th
player must provide an answer from a set $A_i$, and the result of the
game is determined by a "rule\" function,
$$Q_1 \times \cdots \times Q_n \times A_1 \times \cdots \times A_n \rightarrow \{0,1\}$$
$1$ means that they win, and $0$ that they lose. The players, which have
access to both the distribution on tuples of questions and the rule
function, can agree on a strategy before the game starts, but they
cannot communicate afterwards (so each of them doesn't know what
questions were asked to other players or what they answered). Their goal
is to maximize the probability of winning. A strategy in a classical
sense is simply given by choosing a map $Q_i \rightarrow A_i$ for each
$i$, and this leads to the *classical value* of the game: the highest
winning probability among all classical strategies. However -- and this
is how non-local games connect with quantum information theory --, we
can consider a kind of strategy where there can be correlations between
the answers given by different players, even though the probability of a
player giving a certain answer to a certain question doesn't depend on
what others have been asked. A strategy in this broader sense can be
encoded by a probability distribution
$e_{q_1, ..., q_n} \in D(A_1 \times \cdots \times A_n)$ to each tuple of
questions $(q_1, ..., q_n)$ in a way that is compatible with
marginalizing to smaller tuples of questions: for
$I \subset \{1, ..., n\}$ and tuples $(q_1, ..., q_n)$,
$(q'_1, ..., q'_n)$ such that $q_i = q'_i$ for $i \in I$, we have
$$\sum_{(a_i)_{i \notin I} \in \prod_{i \notin I} A_i} e_{q_1, ..., q_n}(a_1, ..., a_n) = \sum_{(a'_i)_{i \notin I} \in \prod_{i \notin I} A_i} e_{q'_1, ..., q'_n}(a'_1, ..., a'_n)$$
provided that $a_i = a'_i$ for $i \in I$. An interesting point is that
there exist games that admit a strategy in the generalized sense whose
winning probability is higher that of any classical strategy. This can
be used, in certain cases, to encode numerical values attesting that a
quantum-mechanical system is behaving in a non-classical way. LINK HERE

Such games and strategies for them can be expressed using the category
of scenarios discussed before:

- let $S$ be the scenario whose set of measurements is
  $Q_1 \sqcup \cdots \sqcup Q_n$, whose maximal contexts are sets
  $\{q_1, ..., q_n\}$ containing exactly one question for each player,
  and whose set of outcomes for each $q \in Q_i$ is the set of answers
  $A_i$;

- let $[2]$ be the scenario that has a single measurement and two
  possible outcomes, $0$ and $1$;

The probability distribution on tuples of questions and the rule
function can then be described as a probabilistic map
$g:S \rightarrow [2]$. Moreover, a strategy can be encoded as an
empirical model $e \in \text{EMP}(S)$, and the push-forward model
$\text{EMP}(g)(e)$ -- which is a probability distribution on $\{0, 1\}$,
and thus corresponds to a value $p \in [0,1]$ -- gives the winning
probability of the strategy.

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

[^1]: This story, while loosely tied to actual historical events, is not
    based on a real story; you are indeed not a ship navigator in the
    16th century.