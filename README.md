# I m p o r t n e c e s s a r y l i b r a r i e s and modules
2 i m p o r t numpy as np
3 i m p o r t pandas as pd
4 from s k l e a r n . m o d e l s e l e c t i o n i m p o r t t r a i n t e s t s p l i t
5 from s k l e a r n . ensemble i m p o r t R a n d o m F o r e s t C l a s s i f i e r
6 from s k l e a r n . p r e p r o c e s s i n g i m p o r t S t a n d a r d S c a l e r , LabelEncoder
19
7 # Load d a t a s e t
8 d a t a s e t = pd . r e a d c s v ( ’ c r o p d a t a s e t . csv ’ )
9 # Data p r e p r o c e s s i n g
10 # Handle m i s s i n g v a l u e s , remove d u p l i c a t e s
11 d a t a s e t = d a t a s e t . d r o p d u p l i c a t e s ( ) . dropna ( )
12 # D e f i n e f e a t u r e s (X) and t a r g e t v a r i a b l e ( y )
13 X = d a t a s e t . i l o c [ : , : − 1 ] . v a l u e s
14 y = d a t a s e t . i l o c [ : , − 1 ] . v a l u e s
15 # Encode c a t e g o r i c a l l a b e l s
16 l a b e l e n c o d e r = LabelEncoder ( )
17 y = l a b e l e n c o d e r . f i t t r a n s f o r m ( y )
18 # S p l i t d a t a s e t i n t o t r a i n i n g and t e s t i n g s e t s
19 X t r a i n , X t e s t , y t r a i n , y t e s t = t r a i n t e s t s p l i t (X, y , t e s t s i z e = 0 . 2 ,
20 r a n d o m s t a t e =42)
21 # S t a n d a r d i z e f e a t u r e s
22 s c a l e r = S t a n d a r d S c a l e r ( )
23 X t r a i n = s c a l e r . f i t t r a n s f o r m ( X t r a i n )
24 X t e s t = s c a l e r . t r a n s f o r m ( X t e s t )
25 # T r a i n Random F o r e s t model
26 r a n d o m f o r e s t = R a n d o m F o r e s t C l a s s i f i e r ( n e s t i m a t o r s =100 ,
27 r a n d o m s t a t e =42)
28 r a n d o m f o r e s t . f i t ( X t r a i n , y t r a i n )
29 # E v a l u a t e model on t h e t e s t s e t
30 a c c u r a c y = r a n d o m f o r e s t . s c o r e ( X t e s t , y t e s t )
31 p r i n t ( f ” Accuracy on t e s t s e t : { a c c u r a c y }” )
32 # User i n p u t f o r p r e d i c t i o n
33 n e w i n p u t = np . a r r a y ( [ 2 4 , 59 , 18 , 2 3 . 7 0 , 5 4 . 2 1 , 6 . 6 4 , 1 2 4 . 7 7 ] )
34 n e w i n p u t s c a l e d = s c a l e r . t r a n s f o r m ( n e w i n p u t . r e s h a p e ( 1 , −1) )
35 # Make p r e d i c t i o n
36 p r e d i c t i o n = r a n d o m f o r e s t . p r e d i c t ( n e w i n p u t s c a l e d )
37 p r e d i c t e d c r o p = l a b e l e n c o d e r . i n v e r s e t r a n s f o r m ( p r e d i c t i o n )
38 p r i n t ( f ” P r e d i c t e d cr op : { p r e d i c t e d c r o p [ 0 ] } ” )
