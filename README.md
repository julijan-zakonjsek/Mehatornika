# Mehatornika
Projekt pisanja navodil za GEMS Amethyst

## pomembni linki:
Podatkovni list: https://gems-erasmus.eu/assets/hardware/amethyst/GEMS_Amethyst.html

### spletne strani za cene komponent
https://eu.mouser.com/ <br>
https://www.tme.eu/si/sl/ <br>
https://si.farnell.com/ <br>
https://www.digikey.si/ <br>
https://octopart.com/ <br>

## 0. vaja (VP)
Izbral smo kaj hočmo od vezja (met mikrokrmilnik, 2 tipki, lučko, napajanje, bluetooth modul, senzor, ...). To smo zbral glede na spec. pa naše želje. Naslednji koraki bojo izbira komponent (glede na naše želje) in izris komponent (najprej izbira pa ne izbereš vrednosti uporov, samo veliksoti...pol pa ob izrisu vezja ugotoviš vrednosti pa spremeniš če je treba).

## 1. vaja
Obdelal smo en kup strani za iskanje komponent, jappal smo o napetosti (5V na amethyst), toku in moči krmilnika, pogledal smo vir (usb port na kompu) pa ugotovil da se bomo mogl cappat na 500mA toka (glede na povprečno moč porta) za to da bojo lah vsi kompi to uporablal. Pol smo pa šli komponente gledat pa na podatkovne liste iskat. Na podatkovnem listu najdeš komponento, pol pa še ceno na eni od spletnih strani najdeš. <br>
Dans mormo nareit kok bi stale komponente (1 al pa 100) pa probat ceno čim nižji zbit

## 2. vaja
KiCad naložit pa naredit osnovno risbo. Pol smo pa downlodal un library pa to zmetal v kicad (prefrences --> ...--glej pdf na spletni). Dal smo path do svojga unzipanga fila pa symbol definiral (path sam kopiraš pot, sybol koda je $(GEMS)/GEMS_Library.kicad_sym).
Pol nam je dau del da naredmop neko simpl komponetno z simboli gemsa. Pol smo pa se fukal s prefrenci pa tem (tist ko greš na uno črno sranje, napišeš notr v footprint $(GEMS)/GEMS_Library.pretty)
Narisat mormo celo sheo (3 opcije):
1. vse narišeš sam, veš kere kompopnente morš povezat pa mal poguglaš, mal pochetaš kaki so principi vezanja pa zvežeš (Chat ti ful fajn pomaga, rečmo začneš z USB-C portom pa pol vprašaš kaj je to pa kam more bit zvezan in zakaj. Če chat ne najde apa ne naredi smisla greš pa u datasheet pa tm notr ctrl+F typical apllication apa kej takiga).
2. prerišeš shemo
3. iz githuba jo naložiš
