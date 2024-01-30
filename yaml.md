To write a parsetree browser in typescript, we need a readable and concise way to dump the parsetree.
The parsetree browser is written in typescript to run within a web browser, and eventually in vscode.

A parse tree is a tree of match. A match is a hash with values being submatches or an array of submatches.


As an example we discuss the parse tree of the nqp expression `-0`, a negative zero.
It is obtained by the command :

```bash
nqp  --target=parse -e '-0'
````

The current format is verbose and does not include the span of the match.

```
- statementlist: -0
  - statement: 1 matches
    - EXPR: -0
      - value: -0
        - number: -0
          - integer: 0
            - VALUE: 0
            - decint: 0
```

Very often some parse tree path have the same span. A maximal such path is
named same span path (SSP). The `statement` rule within the `statementlist` rule
is gives an array of matches. This array belongs to the SSP because its unique
element has the same span. We bundle the keys of a SSP separating them with slashes
or @ for one element arrays of match. We name this key bundler SSSB for SSP Bundle.

The yaml format of a match is a map of two elements if there submatche(s) or
two elements if there is none. The first element is the SSPB. The second
element has a key of `%` if the associated value a map of submatches. Otherwise
the key of `@` for an array of submatches. The keys are mnemonic because they
are raku sigils for variable of kind map (hash) or array respectively..


Optionally  the string matched are given or part of it if too long.


```yaml
TOP/statementlist@statement/EXPR/value/number : { from: 0, to: 2}  # -0
% :
    sign : { from: 0, to: 1}             # -
    integer/VALUE : { from: 1, to: 2}    # 0
```

The same in equivalently formatted json would be :

```json
{
  "TOP/statementlist@statement/EXPR/value/number": { "from": 0, "to": 2   },
  "%": {
    "sign": { "from": 0, "to": 1 },
    "integer/VALUE": { "from": 1,  "to": 2   }
  }
}
```

To illustrate a case of use of the `@` key. We partially unbundle the SSPB.

```yaml
TOP/statementlist : { from: 0, to: 2}
@ :
  - statement: { from: 0, to: 2}
    % :
       EXPR/value/number :  { from: 0, to: 2}
       % :
         sign : { from: 0, to: 1}
         integer/VALUE : { from: 1, to: 2}
```

`yaml` npm does not like the @ chars which is reserved. We replace `@` and `%` repectively by `a` and `@h`.

