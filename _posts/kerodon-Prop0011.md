###Skeleton

\Proposition 0011(when we describe this proporty, we don't use condition of nondegenerate.)
1.degeneracy map must factor through on \delta^{n-1}

Remark 0013: Morphism entre deux simplicial set preserve degeneration. The converse holdf if \f :S_{\battle} --> \T_{\battle} is monomorphism.(evidement)

\Proposition 0014: every section of simlicial sets has a unique decompostion (Surjection + section nondegenerate)

Remark: all of this, we can prove in EZ category as same way.

\Prop 012R+\Execs 012S: When two simplicial sets is finite dimension. The demension of Product of these simplicial set is = sum of dimension of two simplicial sets.

Remark: here is eq. because \sigma is nondegenerate n-simplex, if two position is also degenerate, we conclude \sigma is also that.

\Prop 001B give Skeleton an decription by section. Sk_n(S) is pushout of Sk_k-1(S) and n-dimensional section in meaning S_{\buttle}
Sketch of proof: using \Prop0014 and sk_{k-1} embedding in sk_{k}. we only need to show others be same as n-dimensional section. **Reduce degenerate version to nondegenerate**

###Discrete Simplicial Sets 00FQ

\Prop 00FR : The evaluation functor X_{buttle}|--> X_{0}. {Simplicial sets of dimension<=0} eq Set. (because Section of X_{0} is **unique, non-degenerate**)

\Construction 00FS: constant functor \underline{C_{bullet}}. (prepation of nerve)

**X_n --> X_0 is unique map**

\Remark tous sont eq.
\injlim_{[n]\in\delta^{op}}X_n iso X_0

\Corollary 00FY:constant functor(\C-->Fun(\delta^{op},\C)) adj ev_0

\Notation C_{buttle} is discrete if C_{buttle} eq constant functor

\Propostion 00G3 Description of something
1. X_{buttle} iso constant functor (relation with constant functor)
2. tous les application de simplex categorie sont iso.(全,construction)
3. face map is bijection(特,construction)
4. X_{buttle} has dimension <=0 (by our def of Skeleton, Our concept.)

### Directed Graphs as Simplicial Sets 001D (preparation of nerve)

\Def 001E directed graph G 
  Vert(G), Edge(G)
  A pair of functions s,t:Edge(G)--> Vert(G). s,source; t, target
**\Warning 001F** 001e permit multiedge and loop.

\Example 001H Gr(X_{butlle}):
- Vert(Gr(X_{buttle})) is the set of 0-simplices.
- Edge(Gr(X_{buttle})) is the nondegenerate 1-simpleces.

**construction of Graph category**
\Def 001j. G and G' be directed graphs. A morphism from G to G' is a fuction f:Vert(G)\coproduct Edge(G) --> Vert(G')\coproduct Edge(G') which satifies the following conditions:
(a) Vert to Vert
(b) edge to vert or edge satify coherent of morphism s,t.

\Prop 001L Let f: X.-->Y. be a map of simplicial sets. Then the induce map is a morphism of Gr(X.)-->Gr(Y.)
this proof by s is d_1,t is d_0.

\Prop 001M(构造不懂?). canonical map: Hom_{simplicial set}(X.,Y.)-->Hom_{graph}(Gr(X.),Gr(Y.)) is bijective.

### Connected Components of Simplicial Sets

\Def 00G6 S_{buttle}' is a summand of S. if the simplicial set S. decomposes as a coproduct S_{bullet}' \coprod S_{bullet}'', for some S_{bullet}''.

Remark 00G7: S'. is summand if S\S' is same as functorial. **(The face and the degeneracy operators for simplicial set S. preserve the subsets S_n\S'_n)**

Remark 00G8 Then the collection of all summands of S. is closed under the formation of unions and intersections(by 00G7).

Remark 00G9 (Transitivity) satisfied.

Remark 00GA For inverse of summand by any morphism of simplicial set is summand.(proof by natural transformation.)

\Definition 00GB. S. is connected if ti is nonempty and every summand S.' \include S. is either emptry or coincides with S.

Example 00GC. For each n>=0, the standard n-simplex \delta^n is connected.
(proof by induction by n, and observe for n+1 there only unique section n+1 dimensional)

\Def 00GD connected summand of S. is called Connected Components. THE set of all connected components of S. Denoted by \pi_0(S.)

\Warning There are many decsription of \pi_0{S.}
So we denoted it as I.

\Corollary 00GH

\Remark












**1.1.7** The singular Simplicial Set of a Topological Space

\Consturction 1.1.7.1 Let X be a topological space. We define a simplicial set Sing_{buttle}(X) as follws:
Sing_n(X) = Hom_{top}(|\Delta^n|,X) of singular n-simplices in X.






















\Example 002J standard simplex \delta^n n>0 is not a Kan complex (because Map of two standard simplex is preserve order.)
reason: because 0-->0 1-->2 2-->1 is morphism of \Lambda -- \delta^2, can't not induce an \Delta^2 ---> \Delta^2 **(order)**

\Example 00H7 Let S_{buttle} be a simplicial set of dimension exactly 1. Then S. is not Kan complex.
Reason: because we need 2-dimension object.

generalization of 00H7, Soit S_{buttle} un simplicial set of dimension exactly n. Then s. is not Kan complex.

\Example 00H8,00h9: Product and coproduct preserve Kan Complexes, suffcient Global-local(global iff local : P)
Reason: Product by universal property of product. Coproduct by standard simplex is connect, image of connect componnent in orther unique (smallest) connect componnent.



