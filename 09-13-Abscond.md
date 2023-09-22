# Abscond

Syntax: The entire program is a single integer literals.
Comments and whitespace allowed, but nothing else.

- In Racket, `(read)` will let you input an S-expression (allows comments and whitespace)
  - Can use `read` to do all the hard work for us
  - Will need to verify if the read S-expression is a number or not
- `(readline)` will read a line as a string (until the newline)


`parse` function can use `exact-integer?` to check if input is an integer

```racket
;; S-Expr -> Expr
(define (parse s)
  (match s
    [(? exact-integer?) (Lit s)]
    [_ (error "Parse error")]))

;; Expr -> Asm
(define (compile e)
  (match e
    [(Lit i)
     (prog (Global 'entry)
           (Label 'entry)
           (Mov 'rax i)
           (Ret))]))
```

Leave result of each step in `rax` register

To take from stdin, compile, and display:
```racket
(define (main)
  (read-line)
  (asm-display (compile (parse (read)))))
```

