#[barcen, `|%`, %brcn](#brcn)

[Short description]

#Syntax

`|%`, `barcen`, `[%brcn p=(map term foot)]` is a natural rune that produces a
`%gold` core (cores, link). `|%` takes an associative array of names (++term)
and expressions (++foot), each pair of which is called an arm. A dry, or %ash,
arm is denoted with `++`, a wet, or %elm, arm is denoted with `+-`. `|%` can
take an arbitrary number of arms, but the arm array must be terminated with a
`--`

##Produces

[Twig or tile]

##Sample

[`p` is a _
`q` is a _]

##Tall form

|%  
    ++  p.n.q
      q.n.q
    +-  p.n.l.q
      q.n.l.q
    --

##Wide form

None

##Irregular form

None

##Examples

++  yo
      |%  ++  cet  36.524                 ::  (add 24 (mul 100 365))
          ++  day  86.400                 ::  (mul 24 hor)
          ++  era  146.097                ::  (add 1 (mul 4 cet))
          ++  hor  3.600                  ::  (mul 60 mit)
          ++  jes  106.751.991.084.417    ::  (mul 730.692.561 era)
          ++  mit  60
          ++  moh  `(list ,@ud)`[31 28 31 30 31 30 31 31 30 31 30 31 ~]
          ++  moy  `(list ,@ud)`[31 29 31 30 31 30 31 31 30 31 30 31 ~]
          ++  qad  126.144.001            ::  (add 1 (mul 4 yer))
          ++  yer  31.536.000             ::  (mul 365 day)
      --

In ++yo, `|%` creates a core whose arms contain useful constant data for calculating time.

    ++  si                                                  ::  signed integer
      |%
      ++  abs  |=(a=@s (add (end 0 1 a) (rsh 0 1 a)))
      ++  dif  |=([a=@s b=@s] (sum a (new !(syn b) (abs b))))
      ++  dul  |=([a=@s b=@] =+(c=(old a) ?:(-.c (mod +.c b) (sub b +.c))))
      ++  fra  |=  [a=@s b=@s]
               (new =(0 (mix (syn a) (syn b))) (div (abs a) (abs b)))
      ++  new  |=([a=? b=@] `@s`?:(a (mul 2 b) ?:(=(0 b) 0 +((mul 2 (dec b))))))
      ++  old  |=(a=@s [(syn a) (abs a)])
      ++  pro  |=  [a=@s b=@s]
               (new =(0 (mix (syn a) (syn b))) (mul (abs a) (abs b)))
      ++  rem  |=([a=@s b=@s] (dif a (pro b (fra a b))))
      ++  sum  |=  [a=@s b=@s]
               ~|  %si-sum
               =+  [c=(old a) d=(old b)]
               ?:  -.c
                 ?:  -.d
                   (new & (add +.c +.d))
                 ?:  (gte +.c +.d)
                   (new & (sub +.c +.d))
                 (new | (sub +.d +.c))
               ?:  -.d
                 ?:  (gte +.c +.d)
                   (new | (sub +.c +.d))
                 (new & (sub +.d +.c))
               (new | (add +.c +.d))
      ++  sun  |=(a=@u (mul 2 a))
      ++  syn  |=(a=@s =(0 (end 0 1 a)))
      --

In ++si, `|%` creates a core whose arms contain gates used to calculate with signed integers (@s, link).

