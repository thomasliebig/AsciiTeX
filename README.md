```text
                             AsciiTeX — TeX-like documents for monospaced output                              
                                                                                                              
                                                                                                              
                                                                                                              
                          Typesetting monospaced documents in python using AsciiTeX                           
                          ═════════════════════════════════════════════════════════                           
                                                                                                              
  ╭────────────────────────────────────────────────────────────────────────────────────────────────────────╮  
  │ AsciiTeX is a small TeX-like compiler for plain-text layouts. It is useful when a document should stay │  
  │ readable  as source, render cleanly in a terminal, and still support structure, references, equations, │  
  │ diagrams, and bibliography entries.                                                                    │  
  ╰────────────────────────────────────────────────────────────────────────────────────────────────────────╯  
                                                                                                              
  ──────────────────────────────────────────────────────────────────────────────────────────────────────────  
                                                                                                              
  1 WHAT ASCIITEX IS                                                                                          
  ──────────────────                                                                                          
  AsciiTeX  turns structured source into a monospaced document. The syntax is intentionally familiar to any-  
  one who has seen TeX-like markup.                                                                           
                                                                                                              
  A typical workflow is simple.                                                                               
                                                                                                              
  1. Write a source string or text file.                                                                      
                                                                                                              
  2. Register the extensions you need.                                                                        
                                                                                                              
  3. Compile the document to fixed-width output.                                                              
                                                                                                              
  This document itself demonstrates sections, references, display equations, a generated diagram, an includ-  
  ed image, a two-column block, and a bibliography. See Section 2, Equation 1, Diagram 1, and Figure 1.       
                                                                                                              
  2 CORE IDEAS                                                                                                
  ────────────                                                                                                
  AsciiTeX focuses on text-first technical documents.                                                         
                                                                                                              
  • readable source                                                                                           
                                                                                                              
  • monospaced rendering                                                                                      
                                                                                                              
  • automatic numbering for sections, figures, diagrams, and equations                                        
                                                                                                              
  • labels and cross references                                                                               
                                                                                                              
  • layout helpers for quotes, lists, rules, headers, and footers                                             
                                                                                                              
  • optional extensions for math, diagrams, and richer layout blocks                                          
                                                                                                              
  A  simple  paragraph  scoring  function  can be used to explain why line breaking is a natural example for  
  AsciiTeX.                                                                                                   
                                                                                                              
                                                                                                              
         m                                                                                                    
   C =   ∑   pᵢ                                                                                               
       i = 1                                                                                            (1)   
                                                                                                              
                                                                                                              
  Equation  1  is intentionally simple. The point here is not a full typesetting theory but a compact demon-  
  stration of numbered display equations.                                                                     
                                                                                                              
  ┌──────────────────────────────────────────────────────────────────────────────────────────────────────────┐
  │                                           Compilation pipeline                                           │
  │         • pipeline                                                                                       │
  │                                                                                                          │
  │     4.5 ┼────────────────────────────────────────────────────────────────────────────•••••••••••••••───┐ │
  │     3.5 ┼┄┄┄┆┄┄┄┄┄┄┄┄┄┄┄┄┄┄┆┄┄┄┄┄┄┄┄┄┄┄┄┄┆┄┄┄┄┄┄┄┄┄┄┄┄┄┄┆┄┄┄┄┄┄••••••••••••••••••••••┄┄┄┄┄┄┄┄┄┄┄┄┄┄┆┄┄┄│ │
  │progress ├┄┄┄┆┄┄┄┄┄┄┄┄┄┄┄┄┄┄┆┄┄┄┄┄┄┄┄┄┄┄┄┄┆┄┄┄┄┄┄┄••••••••••••••┄┄┄┄┄┄┄┆┄┄┄┄┄┄┄┄┄┄┄┄┄┆┄┄┄┄┄┄┄┄┄┄┄┄┄┄┆┄┄┄│ │
  │     1.2 ┼┄┄┄┆┄┄┄┄┄┄┄┄┄┄┄┄┄┄••••••••••••••••••••••┄┄┄┄┄┄┄┆┄┄┄┄┄┄┄┄┄┄┄┄┄┆┄┄┄┄┄┄┄┄┄┄┄┄┄┆┄┄┄┄┄┄┄┄┄┄┄┄┄┄┆┄┄┄│ │
  │     0.1 ┼───•••••••••••••••┴─────────────┴──────────────┴─────────────┴─────────────┴──────────────┴───┼ │
  │         -0.50             0.5            1             1.5            2            2.5             33.5  │
  │                                                      stage                                               │
  │                                                                                                          │
  │                                                                                                          │
  │Compilation pipeline                                                                                      │
  └──────────────────────────────────────────────────────────────────────────────────────────────────────────┘
                                                                                                              
  Diagram  1  summarizes  the high-level idea: structured source goes through parsing, numbering, and layout  
  before plain-text output is produced.                                                                       
                                                                                                              
  3 INCLUDED ASSET                                                                                            
  ────────────────                                                                                            
  AsciiTeX also supports an image inclusion command.                                                          
                                                                                                              
  ┌──────────────────────────────────────────────────────────────────────────────────────────────────────────┐
  │                                                                                                          │
  │                     ..                                                                                   │
  │       .-:        .:-@*:.      :--=-:.     .::.         :::     .:::::..::::.   --------   -:      :-.    │
  │      :@%@+     -#*+#@++-    =%#+===*-  .+**#@+     .=**#@*     :++++*@#++++-  .++++++++.  =@#.  .*@+     │
  │      %%.*@-    %@- *%      +@+         .=: =@+     .=: -@*          .@=                    .#@--%%:      │
  │     *@: .%%.   :+##@%-.   .@%              +@+         =@*          :@=        -******-      +@@*        │
  │    =@=   -@#      =@+*%*: .@%              +@+         -@*          :@=        .::::::.     :%%#%-       │
  │   :@#     +@+     +%  *@=  +@*.            +@+         =@*          :@=                    +@*. *@*.     │
  │  .#%.      #%:.***@%***-    -*#*****=  .####%%*#=  .*###%%*#+       :%=       .********. :#%-    -%#:    │
  │   .         ..  .-@=.          .::..    .........   .........        .         ........  ..        ..    │
  │                   .                                                                                      │
  │                                                                                                          │
  │Figure 1: image.png                                                                                       │
  └──────────────────────────────────────────────────────────────────────────────────────────────────────────┘
                                                                                                              
  4 TWO-COLUMN BLOCK                                                                                          
  ──────────────────                                                                                          
  4.1 Why it is useful                                   4.4 Related work                                     
  AsciiTeX  is  a good fit for repositories that want    Classic  references  for line breaking and document  
  examples  which  are: easy to diff, easy to inspect    preparation include [1], [2], and [3].               
  in raw form, and easy to render in a terminal.                                                              
                                                         5 BIBLIOGRAPHY                                       
  • no binary document format                            ──────────────                                       
                                                         The  bibliography  below is loaded from an external  
  • source stays compact                                 file.                                                
                                                                                                              
  • generated output stays text-based                    REFERENCES                                           
                                                         ──────────                                           
  4.2 Typical use cases                                  [1]  Knuth,  D. E. and Plass, M. F.. Breaking Para-  
  Typical  use  cases  include  tutorials,  technical    graphs  into  Lines. Software: Practice and Experi-  
  notes, CLI demos, test fixtures, and reference doc-    ence. 11. pp. 1119--1184. 1981.                      
  uments that should remain readable without a GUI.                                                           
                                                         [2] Lamport, L.. LaTeX: A Document Preparation Sys-  
  4.3 A tiny source fragment                             tem. Addison-Wesley. 1994.                           
                                                                                                              
    \section{Example}                                    [3]  Bringhurst,  R..  The  Elements of Typographic  
    A small paragraph.                                   Style. Hartley and Marks. 2004.                      
                                                                                                              
    \begin{equation}                                     6 LICENSE                                            
      a^2 + b^2 = c^2                                    ─────────                                            
    \end{equation}                                       Asciitex is released under the MIT License.          
                                                                                                              
                                              README-style demo                                               
```

