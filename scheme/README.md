# 99-SchemeProblems   
This file has the purpose of studying the [`99 Scheme Problems`](https://www.ic.unicamp.br/~meidanis/courses/mc336/problemas-lisp/L-99_Ninety-Nine_Lisp_Problems.html).
They are the following:

- ## Working with lists

### First problem:
```scheme
(define my-last
  (lambda(x)
    (cond ((null? (cdr x))
          (car x))
    (else
     (my-last(cdr x))))))
```

### Second problem:
```scheme
(define my-but-last
  (lambda(x)
    (cond ((null? (caddr x))
          x)
      (else(my-but-last (cdr x))))))
```

### Third problem:
```scheme
(define (element-at x y)
  (cond ((= 1 y)
         (car x))
        (else (element-at (cdr x) (- y 1)))))
```

### Fourth problem:
```scheme
(define number-elements
  (lambda(x)
    (cond ((null? (cdr x))
          1)
      (else(+ 1 (number-elements (cdr x)))))))
```

### Fifth problem:
```scheme
(define reverse
  (lambda(x)
    (cond ((null? (cdr x))
          (list (car x)))
      (else(append  (reverse (cdr x)) (list(car x)))))))
```

### Sixth problem:
```scheme
; Use the function from above
(define is-palindrome?
  (lambda (x)
    (cond ((null? x)
           #t)
          ((equal? x (reverse x)) ; here
           #t)
          (else #f))))
```

### Seventh problem:
```scheme
(define (flatten lst)
  (cond ((null? lst) '())                    
        ((not (pair? lst)) (list lst))       
        (else (append (flatten (car lst))    
                      (flatten (cdr lst)))))) 
```

### Eighth problem:
```scheme
(define (compress x)
  (cond ((null? x) '())               
        ((null? (cdr x)) (list (car x)))  
        ((equal? (car x) (cadr x))     ; If the current element equals the next element
         (compress (cdr x)))             ; Skip the current element and continue compressing
        (else                             ; Otherwise, keep the current element
         (cons (car x)                   
               (compress (cdr x))))))   
```

### Nineth problem:
```scheme
(define (pack x)
  (cond ((null? x) '())
        (else (cons (pega x) (pack (tira x))))))

(define (pega x)
  (cond ((null? x) '())
        ((null? (cdr x)) x)
        ((equal? (car x) (cadr x))
         (cons (car x) (pega (cdr x))))
        (else (list (car x)))))

(define (tira x)
  (cond ((null? x) '())
        ((null? (cdr x)) '())
        ((equal? (car x) (cadr x))
         (tira (cdr x)))
        (else (cdr x))))
```

### Tenth problem:
```scheme
(define (encode x)
  (map (lambda (xx) 
         (list (length xx) (car xx)))   
       (pack x))) ; uses here the problem 09                             
```

### Eleventh problem:
```scheme
(define (encode-modified lst)
  (map (lambda (sublst)
         (append (cond
                   ((= (length sublst) 1)(car sublst))
                   (else(list (length sublst) (car sublst))))))
       (pack lst)))
```

### Twelfth problem:
```scheme
(define (decode-aux n a) ;has 2 parameters, the number, and the letter to repeat the number of times in a list
  (cond ((= n 0)'())
        (else(append (list a) (decode-aux (- n 1) a)))))

(define (decode lst)
  (cond((null? lst)'())
       ((list? (car lst))  (append (decode-aux (caar lst) (cadr(car lst)))  (decode (cdr lst))  ) )
       (else(append (list(car lst))  (decode (cdr lst))  )   )))
```

### Thirteenth problem:
```scheme
(define (encode-modified lst)
  (map (lambda (sublst)
         (append (cond
                   ((= (length sublst) 1)(car sublst))
                   (else(list (length sublst) (car sublst))))))
       (pack lst)))
```

### Fourteenth problem:
```scheme
(define (dupli lst)
  (cond ((null? lst) '())
        (else (append (list (car lst)) (list (car lst)) (dupli (cdr lst))))))
```

### Fifteenth problem:
```scheme
(define (repeat-value n e)
  (cond ((= n 0) '())            
        (else (cons e             
                    (repeat-value (- n 1) e)))))  

(define (repli lst y)
  (cond ((null? lst) '())
        (else (append (repeat-value y (car lst)) (repli (cdr lst) y)))))
```

### Sixteenth problem:
```scheme
(define (drop lst y)
  (drop-aux lst y y))

(define (drop-aux lst y count)
  (cond
    ((null? lst) '())
    ((= count 1) (drop-aux (cdr lst) y y))  
    (else (cons (car lst) (drop-aux (cdr lst) y (- count 1)))))) 
```

### Seventeenth problem:
```scheme
(define (take lst n) ; returns a list of the first n elements of a list
  (cond ((or (null? lst) (= n 0))'())                              
      (else(cons (car lst) (take (cdr lst) (- n 1))))))

(define (drop2 lst n)
  (if (or (null? lst) (= n 0))
      lst                         ; if lst is empty or n is 0, return lst as it is
      (drop2 (cdr lst) (- n 1)))) ; otherwise, recursively call drop with the rest of the list and n decremented by 1

(define (split lst n)
  (cond ((null?  lst) '())                     
        (else (list (take lst n)  (drop2 lst n))) ; here it uses the problem 16
                     )) 

```

### Eighteenth problem:
```scheme
(define (slice lst i k)
  (cond((null? lst) '())
        (else (drop2 (take lst k) i)))) ; use the problem 17
```

### Nineteenth problem: *
```scheme
(define (rotate lst n)
  (define sublist lst)
  (cond((null? lst) '())
       ((< n 0) (append (cdr (split lst (+ (length lst) n))) (car (split lst (+ (length lst) n)))) )
       (else (append  (slice lst n (length lst)) (take sublist n) ))))
```

### Twentyth problem:
```scheme
(define (remove-at lst n)
  (cond
       ((null? lst)'())
       ((= n 1) (cdr lst))
       (else(append (list (car lst)) (remove-at (cdr lst) (- n 1))))))
```

### Twenty-first problem:
```scheme
(define(insert-at a lst i)
  (cond((null? lst) '())
       ((= i 1) (cons a lst))
       (else( cons (car lst) (insert-at a (cdr lst) (- i 1))))))
```

### Twenty-second problem:
```scheme
(define (range a b)
  (cond((> a b)'())
       (else(cons a (range (+ a 1) b)))))
```

### Twenty-third problem:
```scheme
(define (rnd-select-aux lst n r)
  (cond ((= 0 n) '())
        ((= r 0) (list (car lst)))
        (else(rnd-select-aux (cdr lst) n (- r 1)))))

(define(rnd-select lst n)
 
  (cond((= 0 n) '())
       (else(append  (rnd-select lst (- n 1))   (rnd-select-aux lst n (random (length lst)))  ))))
```

### Twenty-fourth problem:
```scheme
(define (lotto-select a b)
  (rnd-select (range 1 b) a))
```

### Twenty-fifth problem:
```scheme
(define (rnd-permu lst)
  (rnd-select lst (length lst)))
```

### Twenty-sixth problem:
```scheme
(define combination
  (lambda (k lst)
    (cond((= 0 k) '(()))
         ((= k (length lst))(list lst))
         (else(append(map(lambda (c) (cons (car lst) c))
                         (combination (- k 1) (cdr lst) ))
                     (combination k (cdr lst) ))))))
```

### Twenty-seventh problem:
a)
```scheme
(define (group3 lst)
  (cond((null? lst) '())
       (else(append (combination 2 lst) (combination 3 lst) (combination 4 lst) ))))
```
b)
```scheme
(define (group lst nmbrs)
  (cond((null? nmbrs) '())
       (else(append (combination (car nmbrs) lst)
                    (group lst (cdr nmbrs)  ) ))))
```
### Twenty-eighth problem:
a)
```scheme
(define (lsort lst)
  (cond ((null? lst) '())  
        (else (let ((sorted (sort lst (lambda (x y) (< (length x) (length y))))))
                sorted))))

(define (sort lst cmp)
  (cond ((null? lst)lst)
        (else(insert (car lst) (sort (cdr lst) cmp) cmp))))

(define (insert elt lst cmp)
  (cond ((null? lst) (list elt))
        ((cmp elt (car lst)) (cons elt lst))
        (else (cons (car lst) (insert elt (cdr lst) cmp)))))
```
b)
```scheme
(define (length-frequencies lst)
  (define (count-lengths lst)
    (cond ((null? lst)
        '())
        (else(let ((len (length (car lst))))
          (cons len (count-lengths (cdr lst)))))))

  (define (frequency-counter freqs lengths)
    (cond ((null? lengths)
        freqs)
        ((let ((len (car lengths)))
          (cond ((assoc len freqs)
              (frequency-counter
               (update-frequency len freqs)
               (cdr lengths)))
              (else(frequency-counter
               (cons (cons len 1) freqs)
               (cdr lengths))))))))

  (define (update-frequency len freqs)
    (map (lambda (pair)
           (if (= (car pair) len)
               (cons len (+ 1 (cdr pair)))
               pair))
         freqs))

  (let ((lengths (count-lengths lst)))
    (let ((frequencies (frequency-counter '() lengths)))
      (sort lst (lambda (x y)
                  (> (cdr (assoc (length x) frequencies))
                     (cdr (assoc (length y) frequencies))))))))
```
- ## Arithmetic

### Thirty-first problem:
```scheme
(define (is-prime? n)
  (is-prime-aux? n 2) )

(define (is-prime-aux? n i)
  (cond
       ((= n 2) #t)
       ((< n 2) #f)
       ((= (modulo n i) 0) #f)
       ((> (* i i) n) #t)
       (else (is-prime-aux? n (+ i 1)))))
```

### Thirty-second problem:
```scheme
(define (gcd a b)
  (cond((= b 0) a)
       (else (gcd b (modulo a b)))))
```

### Thirty-third problem:
```scheme
(define (coprime x y)
  (cond ((= (gcd x y) 1)#t)
        (else #f)))
```

### Thirty-fourth problem:
```scheme
(define (totient-phi m)
  (cond ((< 0 m)(phi-aux 1 m 0))
        (else -1)))

(define (phi-aux i n res)
  (cond((= i n) res)
       ((= 1 (gcd i n)) (phi-aux (+ i 1) n (+ res 1)))
       (else (phi-aux (+ i 1) n res ))))
```

### Thirty-fifth problem:
```scheme
(define (prime-factors n)
  (pf-aux n n 3))

(define (pf-aux n m i)
  (cond((= n 1) '()) ; si n es 1, termina
       ((= (modulo n 2) 0) (append (list 2) (pf-aux (/ n 2) m i))) ; condicion especial para el 2
       ((= (modulo n i) 0) (append (list i) (pf-aux (/ n i) m i))) ; si lo divide
       (else   (pf-aux n m (+ i 2))))) ; si no lo divide
```

### Thirty-sixth problem:
```scheme
(define (prime-factors-mult n)
  (encode (prime-factors n)))
```

### Thirty-seventh problem:
```scheme
(define (phi2 n)
  (phi2-aux (prime-factors-mult n)))

(define (phi2-aux lst)
  (cond((null? lst) 1) ; base case, no others prime factors left(has to be 1 as we are *) 
       (else ( *  ( * (- (car (cdr (car lst))) 1)
                    (expt (car (cdr (car lst))) (- (caar lst) 1)))
                  (phi2-aux (cdr lst))  )  )))
```

### Thirty-eighth problem:
Test 1:
```bash
> (time (phi2 10090))
cpu time: 0 real time: 0 gc time: 0
4032
> (time(totient-phi 10090))
cpu time: 5 real time: 5 gc time: 0
4032
```
This previous example didn't demonstrate the difference in time complexity between the two algorithms, so I ran two more tests:

Test 2:
```bash
> (time (phi2 100900))
cpu time: 0 real time: 0 gc time: 0
40320
> (time(totient-phi 100900))
cpu time: 62 real time: 62 gc time: 1
40320
```
Test 3:
```bash
> (time (phi2 1009000))
cpu time: 0 real time: 0 gc time: 0
403200
>  (time(totient-phi 1009000))
cpu time: 873 real time: 873 gc time: 249
403200
```
So there we can really see the difference between these two algorithms, being the problem 37 the most efficient one.


### Thirty-nineth problem:
```scheme
(define (primes-list n m)
  (cond((> n m)'())
       ((is-prime? n) (append (list n)   (primes-list (+ n 1) m))  )
       (else(primes-list (+ n 1) m))))
```
### Fortyth problem:
```scheme
(define (terms-sum k lst)
  (cond
    ((null? lst) '())
    ((member (- k (car lst)) lst)
     (list (car lst) (- k (car lst))))
    (else (terms-sum k (cdr lst)))))

(define (goldbach n)
  (cond((odd? n) 0)
       (else(terms-sum n (primes-list 2 n)))))
```
### Forty-one problem:
```scheme
(define (goldbach-list n m)
  (cond((= n m) null)
       (else(append  (goldbach (+ n 1)) (list '- ) (goldbach-list (+ n 1) m)))))
```

- ## Logic and Codes
- ## Binary Trees
In scheme, we are going to represent binary trees like this:
`'(a (b () ()) ())`, a list of 3 elements, where the root is the firt element, then the second element is the left child, and the third is the right child.


### Fifty-fourth problem:
```scheme
(define (istree? tree)
  (cond ((null? tree) #t)
        (else (and (list? tree)                    ; if it is a list
                   (= 3 (length tree))             ; is the length is 3
                   (istree? (cadr tree))           ; recursive call to the left subtree
                   (istree? (caddr tree))))))      ; recursive call to the left subtree
```
It works like this:
```bash
> (istree? '(a (b () ()) ()))
#t
```
```bash
> (istree? '(a (b () ())))
#f
```

### Fifty-fifth problem:
```scheme
(define (cbal-tree-print n)
  (cond((= n 0) '())
       (else(append (list n)  ; also works (list 'X)
                    (list (cbal-tree-print (- n 1)))
                    (list (cbal-tree-print (- n 1)))
                    ))))
```
It works like this:
```bash
> (cbal-tree-print 4)
(4 (3 (2 (1 () ()) (1 () ())) (2 (1 () ()) (1 () ()))) (3 (2 (1 () ()) (1 () ())) (2 (1 () ()) (1 () ()))))
```
Here, we can visualize better the tree levels:
```bash
(4 (3 (2 (1 () ())
         (1 () ()))
      (2 (1 () ())
         (1 () ())))
   (3 (2 (1 () ())
         (1 () ()))
      (2 (1 () ())
         (1 () ()))))
```
### Fifty-sixth problem:
```scheme
(define (symmetric tree)
  (define (mirror? left right)
    (cond ((and (null? left) (null? right)) #t)  
          ((or (null? left) (null? right)) #f)  
          (else (and (mirror? (car left) (car right))  
                     (mirror? (cdr left) (cdr right))))))
  (cond ((null? tree) #t)  
        (else (mirror? (car tree) (cdr tree)))))  
```

### Fifty-seventh problem:
```scheme
(define (construct lista)
  (define (construct-helper lst t)
    (cond ((null? lst) t)
          (else (construct-helper (cdr lst) (bst-add (car lst) t)))))
  (let ((tree '()))
    (construct-helper lista tree)))

(define (bst-add item tree)
  (cond ((null? tree) (list item '() '()))
        ((< item (car tree)) (cons (car tree)
                                   (list (bst-add item (cadr tree))
                                         (caddr tree))))
        ((> item (car tree)) (cons (car tree)
                                   (list (cadr tree)
                                         (bst-add item (caddr tree)))))
        (else tree)))
```

### Fifty-eighth problem:
(Its the same function as the problem 55)
```scheme
(define (sym-cbal-trees-print n)
  (cond((= n 0) '())
       (else(append (list n)  ; also works (list 'X)
                    (list (cbal-tree-print (- n 1)))
                    (list (cbal-tree-print (- n 1)))
                    ))))
```

### Fifty-ninth problem:
```scheme

```

### Sixtieth problem:
```scheme
(define(min-nodes H)
  (cond((= H 0) 1)
       ((= H 1) 2)
       (else(+ 1 (+ (min-nodes (- H 1)) (min-nodes (- H 2)) ))))) 

(define (max-height n)
  (max-height-aux -1 0 1 n))

(define (max-height-aux h fh fh1 n)
  (cond ((< n fh1)h)
        (else(max-height-aux (1+ h) fh1 (+ 1 fh fh1) n))))
```
### Sixty-first problem:
```scheme
(define (count-leaves tree)
  (cond((null? tree)0)
       ((null? (and (cadr tree) (caddr tree) )) 1)
       (else(+ (count-leaves (cadr tree)) (count-leaves (caddr tree))))))
```
### Sixty-first-A problem:
```scheme
(define (leaves tree)
  (cond((null? tree)'())
       ((and (null? (cadr tree)) (null?(caddr tree)) ) (list (car tree)))
       (else(append (leaves (cadr tree)) (leaves (caddr tree))))))
```
### Sixty-second problem:
```scheme
(define internals
  (lambda (tree)
    (cond((null? tree)'())
         ((and (null? (cadr tree)) (null?(caddr tree)) ) '())
         (else(append (list (car tree))
                      (internals (cadr tree))
                      (internals (caddr tree)))))))
```
### Sixty-second-B problem:
```scheme
(define (atlevel tree L)
  (cond((null? tree)'())
       ((= L 1) (list(car tree)))
       (else(append (atlevel (cadr tree) (- L 1)) (atlevel (caddr tree) (- L 1))))))
```
### Sixty-third problem:
```scheme
(define (complete-binary-tree n)
  (cbt-label n 1))

(define (cbt-label n k)
  (cond
    ((= n 0) '())
    ((= n 1) (list k '() '()))
    (else(let* ((p (floor (/ (highest-2-power n) 2)))
           (left (if (= 2 (floor (/ n p)))
                     (+ p (modulo n p))
                     (+ p (- p 1)))))
           (list k
                 (cbt-label left (* 2 k))
                 (cbt-label (- n 1 left) (+ 1 (* 2 k))))))))

(define (highest-2-power n)
  (cond ((<= n 1)1)
        (else(* 2 (highest-2-power (floor (/ n 2)))))))
``` 
### Sixty-fourth problem:
```scheme

``` 
### Sixty-fifth problem:
```scheme

```
### Sixty-sixth problem:
```scheme

```
### Sixty-seventh problem:
```scheme

```
### Sixty-eighth problem:
```scheme

```
### Sixty-ninth problem:
```scheme

```

- ## Multiway Trees
Their scheme representation:
```bash
'(a ((b ())
     (c ())
     (d ((r ())))))
```
![Example Image](texample.png)

### Seventieth-B problem: 
``` scheme
(define isntree?
  (lambda (tree)
    (cond((null? tree) #t)
         ((> (length tree) 2) #f)
         ((= (length tree) 1) #f)
         (else (andmap isntree? (cadr tree))))))
```
### Seventieth-C problem:
```scheme
(define nnodes
  (lambda(tree)
    (cond((null? tree) 0)
         (else (+ 1 (apply + (map nnodes (cadr tree))))))))
```
### Seventieth problem:
```scheme

```
###  problem:
```scheme

```
###  problem:
```scheme

```
###  problem:
```scheme

```


- ## Graphs
- ## Miscellaneous Problems
