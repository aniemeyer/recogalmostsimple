Die Hauptfunktion AnBB_Recognise( <grp>, <N>, <eps> ) bekommt eine black-box-Gruppe <grp>, eine natürliche Zahl <N> und eine reelle Zahl <eps>.
Erkannt werden Gruppen <grp> isomorph zu einer A_n oder S_n vom Grad 9 \leq n \leq <N>.
Der Algorithmus ist einseitig Monte-Carlo: Wenn er aufgibt, dann mit Wahrscheinlichkeit mind. 1-<eps> zu recht.
Die Laufzeit skaliert fast linear mit <N>, man kann die Gradschranke also ruhig zu groß wählen, aber auch nicht übertreiben.

Output:
fail – Alg. hat aufgegeben, <grp> ist mit Wahrscheinlichkeit 1-<eps> nicht AnSn für n \leq <N>
false – Alg. hat Beweis, dass <grp> nicht AnSn für n \leq <N>

Ist der Output weder fail noch false, so wird eine Liste
[ <name>, <deg>, <s>, <t>, <iso> ]
zurückgegeben:
<name> ist der String "An" oder "Sn".
<deg> ist der Grad der Gruppe.
<s> und <t> sind Standarderzeuger; <s> der mit großem support, <t> Transposition falls S_n, Dreizykel falls A_n.
<iso> ist eine unübersichtliche Liste, die Daten zur Auswertung des Isomorphismus \lambda enthält, wobei
der Iso definiert ist über \lambda( <s> ) = \sigma, \lambda( <t> ) = \tau, mit \sigma und \tau Standarderzeuger
von S_n bzw. A_n.
Es gibt eine Funktion, die mithilfe dieser Liste das Bild eines Elements von <grp> unter \lambda ausrechnet.

gap> Read( "AnBB.gi" );
gap> data := AnBB_Recognise( AlternatingGroup( 1500 ), 2000, 1/20 );;
gap> time;
634
gap> data[1];
"An"
gap> data[2];
1500
gap> CycleStructurePerm( data[3] );
[ 1,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
  ,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
  ,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
  ,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
  ,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
  ,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
  ,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
  ,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,, 1 ]
gap> Positions( last, 1 );
[ 1, 1497 ]
gap> data[4];
(1081,1228,1243)
gap> isoData := data[5];;

Oben genannte Funktion trägt den Namen AnBB_EvaluateIso und bekommt zwei Argumente:
Ein Elemente <gpelt> der Gruppe <grp> und die Liste <iso>, die AnBB_Recognise ausgespuckt hat.

gap> AnBB_EvaluateIso( data[4], isoData );                           
(1,2,3)
gap> AnBB_EvaluateIso( data[3], isoData );          
(1,2)(3,4,5,6,7,...)
gap> AnBB_EvaluateIso( data[4] ^ ( data[3]^2 ), isoData );
(1,2,5)

Die Datei enthält außerdem Funktionen zur Berechnung von SLPs in A_n und S_n:
AnBB_SLPForAn( <perm>, <degree> ) und AnBB_SLPForSn( <perm>, <degree> ).
Die SLPs sind in den Erzeugern \tau, \sigma (in dieser Reihenfolge!) auszuwerten.

gap> slp := AnBB_SLPForAn( (1,2,3,4,5), 1500 );
<straight line program>
gap> ResultOfStraightLineProgram( slp, [ data[4], data[3] ] );
(753,1243,1081,1228,1175)
gap> ResultOfStraightLineProgram( slp, [ (1,2,3), (1,2)*Product( [4..1500], i -> (i-1,i) )^-1 ] );   
(1,2,3,4,5)

Natürlich kann man damit auch Urbilder unter \lambda ausrechnen:

gap> preimage := ResultOfStraightLineProgram( AnBB_SLPForAn( (1,2,3,99,101), 1500 ), [ data[4], data[3] ] );
(7,114,64,49,313)
gap> AnBB_EvaluateIso( preimage, isoData );
(1,2,3,99,101)

