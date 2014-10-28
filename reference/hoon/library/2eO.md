##section 2eO, virtualization

---

###++mack

```
++  mack
  |=  [sub=* fol=*]
  ^-  (unit)
  =+  ton=(mink [sub fol] |=(* ~))
  ?.(?=([0 *] ton) ~ [~ p.ton])
::
```

Accpet a nock subject-formula cell.
Produce a unit result, treating 11 as a crash (i.e. pure nock).

    ~zod/try=> (mack [[1 2 3] [0 1]])
    [~ [1 2 3]]
    ~zod/try=> (mack [41 4 0 1])
    [~ 42]
    ~zod/try=> (mack [4 0 4])
    ~
    ~zod/try=> (mack [[[0 2] [1 3]] 4 4 4 4 0 5])
    [~ 6]
    ~zod/try=> ;;((unit ,@tas) (mack [[1 %yes %no] 6 [0 2] [0 6] 0 7]))
    [~ %no]
    

---

###++mink

```
++  mink
  ~/  %mink
  |=  [[sub=* fol=*] sky=$+(* (unit))]
  =+  tax=*(list ,[@ta *])
  |-  ^-  tone
  ?@  fol
    [%2 tax]
  ?:  ?=(^ -.fol)
    =+  hed=$(fol -.fol)
    ?:  ?=(%2 -.hed)
      hed
    =+  tal=$(fol +.fol)
    ?-  -.tal
      %0  ?-(-.hed %0 [%0 p.hed p.tal], %1 hed)
      %1  ?-(-.hed %0 tal, %1 [%1 (weld p.hed p.tal)])
      %2  tal
    ==
  ?+    fol
    [%2 tax]
  ::
      [0 b=@]
    ?:  =(0 b.fol)  [%2 tax]
    ?:  =(1 b.fol)  [%0 sub]
    ?:  ?=(@ sub)   [%2 tax]
    =+  [now=(cap b.fol) lat=(mas b.fol)]
    $(b.fol lat, sub ?:(=(2 now) -.sub +.sub))
  ::
      [1 b=*]
    [%0 b.fol]
  ::
      [2 b=[^ *]]
    =+  ben=$(fol b.fol)
    ?.  ?=(%0 -.ben)  ben
    ?>(?=(^ p.ben) $(sub -.p.ben, fol +.p.ben))
    ::?>(?=(^ p.ben) $([sub fol] p.ben)
  ::
      [3 b=*]
    =+  ben=$(fol b.fol)
    ?.  ?=(%0 -.ben)  ben
    [%0 .?(p.ben)]
  ::
      [4 b=*]
    =+  ben=$(fol b.fol)
    ?.  ?=(%0 -.ben)  ben
    ?.  ?=(@ p.ben)  [%2 tax]
    [%0 .+(p.ben)]
  ::
      [5 b=*]
    =+  ben=$(fol b.fol)
    ?.  ?=(%0 -.ben)  ben
    ?.  ?=(^ p.ben)  [%2 tax]
    [%0 =(-.p.ben +.p.ben)]
  ::
      [6 b=* c=* d=*]
    $(fol =>(fol [2 [0 1] 2 [1 c d] [1 0] 2 [1 2 3] [1 0] 4 4 b]))
  ::
      [7 b=* c=*]       $(fol =>(fol [2 b 1 c]))
      [8 b=* c=*]       $(fol =>(fol [7 [[0 1] b] c]))
      [9 b=* c=*]       $(fol =>(fol [7 c 0 b]))
      [10 @ c=*]        $(fol c.fol)
      [10 [b=* c=*] d=*]
    =+  ben=$(fol c.fol)
    ?.  ?=(%0 -.ben)  ben
    ?:  ?=(?(%hunk %lose %mean %spot) b.fol)
      $(fol d.fol, tax [[b.fol p.ben] tax])
    $(fol d.fol)
  ::
      [11 b=*]
    =+  ben=$(fol b.fol)
    ?.  ?=(%0 -.ben)  ben
    =+  val=(sky p.ben)
    ?~(val [%1 p.ben ~] [%0 u.val])
  ::
  ==
::
```

Bottom-level mock (virtual nock) interpreter.

    ~zod/try=> (mink [20 [4 0 1]] ,~)
    [%0 p=21]
    ~zod/try=> (mink [[90 5 3] [0 3]] ,~)
    [%0 p=[5 3]]
    ~zod/try=> (mink 20^[4 0 1] ,~)
    [%0 p=21]
    ~zod/try=> (mink [90 5 3]^[0 3] ,~)
    [%0 p=[5 3]]
    ~zod/try=> (mink [0]^[11 1 20] ,~)
    [%1 p=~[20]]
    ~zod/try=> (mink [0]^[11 1 20] |=(a=* `[40 a]))
    [%0 p=[40 20]]
    ~zod/try=> (mink [5]^[0 2] ,~)
    [%2 p=~]
    ~zod/try=> (mink [5]^[10 yelp/[0 1] 0 0] ,~)
    [%2 p=~[[~.yelp 5]]]

---

###++mock

```
++  mock
  |=  [[sub=* fol=*] sky=$+(* (unit))]
  (mook (mink [sub fol] sky))
::
```

Accepts a nock subject-formula cell and an %iron gate which
accepts any noun and produces a unit (this is used as nock 11).
Produces a ++toon, which is a sucesful, blocked, or crashed result.

    ~zod/try=> (mock [5 4 0 1] ,~)
    [%0 p=6]
    ~zod/try=> (mock [~ 11 1 0] |=(* `999))
    [%0 p=999]
    ~zod/try=> (mock [~ 0 1.337] ,~)
    [%2 p=~]
    ~zod/try=> (mock [~ 11 1 1.337] ,~)
    [%1 p=~[1.337]]
    ~zod/try=> (mock [[[4 4 4 4 0 3] 10] 11 9 2 0 1] |=(* `[+<]))
    [%0 p=14]
    ~zod/try=> (mock [[[4 4 4 4 0 3] 10] 11 9 2 0 1] |=(* `[<+<>]))
    [%0 p=[49 52 0]]
    ~zod/try=> ;;(tape +:(mock [[[4 4 4 4 0 3] 10] 11 9 2 0 1] |=(* `[<+<>])))
    "14"

---

###++mook

```
++  mook
  |=  ton=tone
  ^-  toon
  ?.  ?=([2 *] ton)  ton
  :-  %2
  =+  yel=(lent p.ton)
  =.  p.ton
    ?.  (gth yel 256)  p.ton
    %+  weld
      (scag 128 p.ton)
    ^-  (list ,[@ta *])
    :_  (slag (sub yel 128) p.ton)
    :-  %lose
    %+  rap  3
    ;:  weld
      "[skipped "
      ~(rend co %$ %ud (sub yel 256))
      " frames]"
    ==
  |-  ^-  (list tank)
  ?~  p.ton  ~
  =+  rex=$(p.ton t.p.ton)
  ?+    -.i.p.ton  rex
      %hunk  [(tank +.i.p.ton) rex]
      %lose  [[%leaf (rip 3 (,@ +.i.p.ton))] rex]
      %mean  :_  rex
             ?@  +.i.p.ton  [%leaf (rip 3 (,@ +.i.p.ton))]
             =+  mac=(mack +.i.p.ton +<.i.p.ton)
             ?~(mac [%leaf "####"] (tank u.mac))
      %spot  :_  rex
             =+  sot=(spot +.i.p.ton)
             :-  %leaf
             ;:  weld
               ~(ram re (smyt p.sot))
               ":<["
               ~(rend co ~ %ud p.p.q.sot)
               " "
               ~(rend co ~ %ud q.p.q.sot)
               "].["
               ~(rend co ~ %ud p.q.q.sot)
               " "
               ~(rend co ~ %ud q.q.q.sot)
               "]>"
             ==
  ==
::
```

Intelligently render crash annotation.

    ~zod/try=> (mook [%0 5 4 5 1])
    [%0 p=[5 4 5 1]]
    ~zod/try=> (mook [%2 ~[[%hunk %rose ["<" "," ">"] ~[[%leaf "err"]]]]])
    [%2 p=~[[%rose p=[p="<" q="," r=">"] q=[i=[%leaf p="err"] t=~]]]]
    ~zod/try=> (mook [%2 ~[[%malformed %elem] [%lose 'do print']]])
    [%2 p=~[[%leaf p="do print"]]]
    ~zod/try=> (mook [%2 ~[[%mean |.(>(add 5 6)<)]]])
    [%2 p=~[[%leaf p="11"]]]
    ~zod/try=> (mook [%2 ~[[%spot /b/repl [1 1]^[1 2]] [%mean |.(!!)]]])
    [%2 p=~[[%leaf p="/b/repl/:<[1 1].[1 2]>"] [%leaf p="####"]]]

---

###++mang

```
++  mang
  |=  [[gat=* sam=*] sky=$+(* (unit))]
  ^-  (unit)
  =+  ton=(mong [[gat sam] sky])
  ?.(?=([0 *] ton) ~ [~ p.ton])
::
```

Work just like in `++makc`, but accept a `++sky`.
Produce a unit computation result.

    ~zod/try=> (mang [|=(@ 20) ~] ,~)
    [~ 20]
    ~zod/try=> (mang [|=(@ !!) ~] ,~)
    ~
    ~zod/try=> (mang [|=(a=@ (add 20 a)) ~] ,~)
    [~ 20]
    ~zod/try=> (mang [|=(a=[@ @] (add 20 -.a)) ~] ,~)
    ~
    ~zod/try=> (mang [|=(a=[@ @] (add 20 -.a)) [4 6]] ,~)
    [~ 24]
    ~zod/try=> (mang [|=(a=@ .^(a)) ~] ,~)
    ~
    ~zod/try=> (mang [|=(a=@ .^(a)) ~] ,[~ %42])
    [~ 42]
    ~zod/try=> (mang [|=(a=@ .^(a)) ~] |=(a=* [~ a 6]))
    [~ [0 6]]
    ~zod/try=> (mang [|=(a=@ .^(a)) 8] |=(a=* [~ a 6]))
    [~ [8 6]]

---

###++mong

```
++  mong
  |=  [[gat=* sam=*] sky=$+(* (unit))]
  ^-  toon
  ?.  &(?=(^ gat) ?=(^ +.gat))
    [%2 ~]
  (mock [[-.gat [sam +>.gat]] -.gat] sky)
::
```

Work just like in `++mung`, but for `++mink`
Produce a unit computation result.

    ~zod/try=> (mong [|=(@ 20) ~] ,~)
    [%0 p=20]
    ~zod/try=> (mong [|=(@ !!) ~] ,~)
    [%2 p=~]
    ~zod/try=> (mong [|=(a=@ (add 20 a)) ~] ,~)
    [%0 p=20]
    ~zod/try=> (mong [|=(a=[@ @] (add 20 -.a)) ~] ,~)
    [%2 p=~]
    ~zod/try=> (mong [|=(a=[@ @] (add 20 -.a)) [4 6]] ,~)
    [%0 p=24]
    ~zod/try=> (mong [|=(a=@ .^(a)) ~] ,~)
    [%1 p=~[0]]
    ~zod/try=> (mong [|=(a=@ .^(a)) ~] ,[~ %42])
    [%0 p=42]
    ~zod/try=> (mong [|=(a=@ .^(a)) ~] |=(a=* [~ a 6]))
    [%0 p=[0 6]]
    ~zod/try=> (mong [|=(a=@ .^(a)) 8] |=(a=* [~ a 6]))
    [%0 p=[8 6]]

---

###++mung

```
++  mung
  |=  [[gat=* sam=*] sky=$+(* (unit))]
  ^-  tone
  ?.  &(?=(^ gat) ?=(^ +.gat))
    [%2 ~]
  (mink [[-.gat [sam +>.gat]] -.gat] sky)
::
```

Virtualize slamming of gate

    ~zod/try=> (mung [|=(@ 20) ~] ,~)
    [%0 p=20]
    ~zod/try=> (mung [|=(@ !!) ~] ,~)
    [%2 p=~]
    ~zod/try=> (mung [|=(a=@ (add 20 a)) ~] ,~)
    [%0 p=20]
    ~zod/try=> (mung [|=(a=[@ @] (add 20 -.a)) ~] ,~)
    [%2 p=~]
    ~zod/try=> (mung [|=(a=[@ @] (add 20 -.a)) [4 6]] ,~)
    [%0 p=24]
    ~zod/try=> (mung [|=(a=@ .^(a)) ~] ,~)
    [%1 p=~[0]]
    ~zod/try=> (mung [|=(a=@ .^(a)) ~] ,[~ %42])
    [%0 p=42]
    ~zod/try=> (mung [|=(a=@ .^(a)) ~] |=(a=* [~ a 6]))
    [%0 p=[0 6]]
    ~zod/try=> (mung [|=(a=@ .^(a)) 8] |=(a=* [~ a 6]))
    [%0 p=[8 6]]

---

###++mule 

```
++  mule                                                ::  typed virtual
  ~/  %mule
  |*  taq=_|.(_*)
  =+  mud=(mute taq)
  ?-  -.mud
    &  [%& p=$:taq]
    |  [%| p=p.mud]
  ==
::
```

Kick error trap, producing its results or any erros that occur along the way.

~zod/try=> (mule |.(leaf/"hello"))
[%.y p=[%leaf "hello"]]
~zod/try=> (mule |.(!!))
[%.n p=~]
~zod/try=> (mule |.(.^(a//=pals/1)))
[ %.n
    p
  ~[
    [ %rose
      p=[p="/" q="/" r="/"]
        q
      [ i=[%leaf p="a"] 
        t=[i=[%leaf p="~zod"] t=[i=[%leaf p="pals"] t=[i=[%leaf p="1"] t=~]]]
      ]
    ]
  ]
]


---

###++mute 

```
++  mute                                                ::  untyped virtual
  |=  taq=_^?(|.(_*))
  ^-  (each ,* (list tank))
  =+  ton=(mock [taq 9 2 0 1] |=(* ~))
  ?-  -.ton
    %0  [%& p.ton]
    %1  [%| (turn p.ton |=(a=* (smyt (path a))))]
    %2  [%| p.ton]
  ==
```

Kick error trap, and produce its result or the tanks of any errors it itself
incurred.

    ~zod/try=>  (mute |.(leaf/"hello"))
    [%.y p=[1.717.658.988 104 101 108 108 111 0]]
    ~zod/try=> (mute |.(!!))
    [%.n p=~]
    ~zod/try=> (mute |.(.^(a//=pals/1)))
    [ %.n
        p
      ~[
        [ %rose
          p=[p="/" q="/" r="/"]
          q=[i=[%leaf p="a"] t=[i=[%leaf p="~zod"] t=[i=[%leaf p="pals"] t=[i=[%leaf p="1"] t=~]]]]
        ]
      ]
    ]


---
