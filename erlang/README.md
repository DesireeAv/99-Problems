# 99-ErlangProblems   
This file has the purpose of studying the [`99 erlang Problems`](https://www.ic.unicamp.br/~meidanis/courses/mc336/problemas-lisp/L-99_Ninety-Nine_Lisp_Problems.html).
They are the following:

- ## Working with lists

### First problem:
```erlang
mylast([]) -> [];
mylast([N]) -> N;
mylast([_H|T]) -> mylast(T).
```

### Second problem:
```erlang
mybutlast([]) -> [];
mybutlast([T, _]) -> T;
mybutlast([_H1|T]) -> mybutlast(T).
```

### Third problem:
```erlang
elementat([], _) -> [];
elementat([H|_T], 1) -> H;
elementat([_H|T], N) when N > 1 -> elementat(T, N-1).
```

### Fourth problem:
```erlang
mylength([]) -> 0;
mylength([_]) -> 1;
mylength([_H|T]) -> 1 + mylength(T).
```

### Fifth problem:
```erlang
lreverse([]) -> [];
lreverse([H|T]) -> lreverse(T) ++ [H].
```

### Sixth problem:
```erlang
palindrome([]) -> true;
palindrome([_L]) -> true;
palindrome(List) -> List == lreverse(List).
```

### Seventh problem:
```erlang
myflatten([]) -> [];
myflatten([[H|T]| TG]) -> myflatten([H|T]) ++ myflatten(TG);
myflatten([H|T]) ->[H|myflatten(T)];
myflatten([[]|T]) -> myflatten(T).
```

### Eighth problem:
```erlang
compress([])->[];
compress([H, H|T]) -> compress([H|T]);
compress([H|T]) -> [H] ++ compress(T).
```

### Nineth problem:
```erlang
pack([])->[];
pack([H|T])->pack(T,[H]).

pack([H|T],[H|P])->pack(T,[H,H|P]);
pack([H|T],Pack)->[Pack|pack(T,[H])];
pack([],Pack)->[Pack].
```

### Tenth problem:
```erlang
encode([])->[];
encode(L) -> [{length(Pack), hd(Pack)} || Pack <- pack(L)].
% la funcion hd() retorna el primer elemento de la lista que le entre
```

### Eleventh problem:
```erlang
tuple([X])->X;
tuple([H|T])->{H,1+length(T)}.

encodemodified(L)->[tuple(X)||X<-pack(L)].
```

### Twelfth problem:
```erlang
detuple({_E, 0}) -> [];
detuple({E, N}) -> [E] ++ detuple({E, N-1}).

decode([]) -> [];
decode([H | T]) when is_tuple(H) -> detuple(H) ++ decode(T);
decode([H | T]) -> [H| decode(T)].
```

### Fourteenth problem:
```erlang
dupli([]) -> [];
dupli([H|T]) -> [H, H | dupli(T)].
```

### Fifteenth problem:
```erlang
repli([], _N)->[];
repli([H|T], N) -> detuple({H, N}) ++ repli(T, N).
```

### Sixteenth problem:
```erlang
drop1([], _N) -> [];
drop1(L, N) -> drop2(L, N, N).

drop2([_H|T], 1, N) -> drop2(T, N, N);
drop2([H|T], A, N) -> [H|drop2(T, A-1, N)];
drop2([], _A, _N) -> [].
```

### Seventeenth problem:
```erlang
split(L,N) -> split(L, N, []).
split(L, 0, A) -> [A, L];
split([H|T], N, A)->split(T, N-1, A++[H]).
```

### Eighteenth problem:
```erlang

```

### Nineteenth problem: 
```erlang

```

### Twentyth problem:
```erlang

```

### Twenty-first problem:
```erlang

```

### Twenty-second problem:
```erlang
range(M, M) -> [M];
range(N, M) -> [N|range(N+1, M)].
```

### Twenty-third problem:
```erlang

```

### Twenty-fifth problem:
```erlang
rndpermu(L) -> [Y || {_,Y} <- lists:sort([ {rand:uniform(), X} || X <- L])].
```



### Twenty-sixth problem:
```erlang
combination(_N, []) -> [];
combination(0, _L) -> [[]];
combination(N, L) when length(L) == N -> [L];
combination(N, [H|T]) -> [[H|C] || C <- combination1(N-1, T)] ++ combination1(N, T).
```

### Twenty-seventh problem:
```erlang

```
### Twenty-eighth problem:
```erlang
lsort(LL) -> [Y || {_Length, Y} <- lists:sort([{length(X), X} || X <- LL])].
```
- ## Arithmetic

### Thirty-first problem:
```erlang
prime(1) -> false;
prime(2) -> true;
prime(N) when N rem 2 =:= 0 -> false;
prime(3) -> true;
prime(Odd) -> prime(Odd, 3).

prime(N, I) when N rem I =:= 0 -> false;
prime(N, I) when I*I > N -> true;
prime(N, I) -> prime(N, I+2).
```

### Thirty-second problem:
```erlang
gcd(A, 0) -> A;
gcd(A, B) -> gcd(B, mod(A, B)).
```

### Thirty-third problem:
```erlang

```

### Thirty-fourth problem:
```erlang

```

### Thirty-fifth problem:
```erlang
primefactors(N) -> primefactors(N, N, 3).

primefactors(1, _M, _I) -> [];
primefactors(N, M, I) when N rem 2 =:= 0 -> [2| primefactors(N div 2, M, I)];
primefactors(N, M, I) when N rem I =:= 0 -> [I| primefactors(N div I, M, I)];
primefactors(N, M, I) -> primefactors (N, M, I + 2).
```

### Thirty-sixth problem:
```erlang

```

### Thirty-seventh problem:
```erlang

```

### Thirty-eighth problem:


### Thirty-nineth problem:
```erlang
rangeprimes(N, M) -> [X || X <- lists:seq(N, M), prime(X)].
```
### Fortyth problem:
```erlang
numsum(_N, []) -> [];
numsum(N, [H|T]) ->
    case lists:member(N-H, T) of
        true -> {H, N-H};
        false -> numsum(N, T)
    end.

goldbach(N) when N rem 2 =:= 0 -> numsum(N, rangeprimes(2, N)).
```
### Forty-one problem:
```erlang

```

- ## Logic and Codes
- ## Binary Trees
Their representation: {3, 
    					{2,{},{}},
    					{8,{5,{},
    						  {6,{},{}}},
    					   {9,{},{}}}}
### Fifty-fourth problem:
```erlang
istree({}) -> true;
istree({_, I, D}) -> istree(I) and istree(D);
istree(I) -> false.
```


### Fifty-fifth problem:
```erlang
cbaltree(0) -> {};
cbaltree(N)  -> {N, cbaltree(N-1), cbaltree(N-1)}.
```

### Fifty-sixth problem:
```erlang
symetric({}, {}) -> true;
symetric({_X, _Y, _Y}, {}) -> false;
symetric({}, {_X, _Y, _Y}) -> false;
symetric({_R1, I1, D1}, {_R2, I2, D2}) -> symetric(I1, I2) and symetric(D1, D2).
```

### Fifty-seventh problem:
```erlang
construct([N]) -> {N, {}, {}};
construct([H|T]) -> construct(T, {H, {}, {}}).

insert(N, {}) -> {N, {}, {}};
insert(N, {Root, L, R}) when N =< Root -> {Root, insert(N, L), R};
insert(N, {Root, L, R}) when N > Root -> {Root, L, insert(N, R)}.

construct([], Tree) -> Tree;
construct([H|T], Tree) -> construct(T, insert(H, Tree)).
```

### Fifty-eighth problem:
(Its the same function as the problem 55)
```erlang

```

### Fifty-ninth problem:
```erlang

```

### Sixtieth problem:
```erlang
minnodes(-1) -> 0;
minnodes(0) -> 1;
minnodes(N) -> 1 + minnodes(N-1) + minnodes(N-2). 

maxheight(N) ->  round(math:floor(math:log2(N+1)) - 1).


```
### Sixty-first problem:
```erlang
countleaves({}) -> 0;
countleaves({_X, {}, {}}) -> 1;
countleaves({_R, I, D}) -> countleaves(I) + countleaves(D).
```
### Sixty-first-A problem:
```erlang
leaves({X, {}, {}}) -> [X];
leaves({_R, I, D}) -> leaves(I) ++ leaves(D).
```
### Sixty-second problem:
```erlang
internals({}) -> [];
internals({R, I, D}) -> [R | internals(I) ++ internals(D)].
```
### Sixty-second-B problem:
```erlang
atlevel({}, N) -> [];
atlevel({R, _I, _D}, 1) -> [R];
atlevel({_R, I, D}, N) -> atlevel(I, N-1) ++ atlevel(D, N-1).
```
### Sixty-third problem:
```erlang

``` 
### Sixty-fourth problem:
```erlang

``` 
### Sixty-fifth problem:
```erlang

```
### Sixty-sixth problem:
```erlang

```
### Sixty-seventh problem:
```erlang

```
### Sixty-eighth problem:
a)
```erlang
inorder(Tree) -> inorder(Tree, []).
inorder({}, Acc) -> Acc;
inorder({R, I, D}, Acc) -> inorder(I, [R | inorder(D, Acc)]).

preorder(Tree) -> preorder(Tree, []).
preorder({}, Acc) -> Acc;
preorder({R, I, D}, Acc) -> [R | preorder(I, preorder(D, Acc))].
```
### Sixty-ninth problem:
```erlang

```

- ## Multiway Trees
Their erlang representation: {r, [{s, []}, {m, []}]}

### Seventieth-B problem: 
``` erlang
isMtree([]) -> true;
isMtree({R, L}) -> 
    is_list(L) andalso lists:foldl(fun(H, Acc) -> Acc andalso isMtree(H) end, true, L).
```
### Seventieth-C problem:
```erlang
nMnodes([]) -> 0;
nMnodes({_R, []}) -> 1;
nMnodes({_R, L}) -> 1 + lists:foldl(fun(H, Acc) -> Acc + nMnodes(H) end, 0, L).
```
### Seventieth problem:
```erlang

```
###  problem:
```erlang

```
###  problem:
```erlang

```
###  problem:
```erlang

```


- ## Graphs
- ## Miscellaneous Problems
