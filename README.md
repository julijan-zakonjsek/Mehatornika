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

## 3. vaja
Še kr razlaga vezje (sam tk da dejansko nič ne razloži, če rabiš karkol je bolš sam chata uprašat).Posebi je šou razlagat še ambient light sensor. Povedu je da senzor deluje kt transistor (senzor je baza). Če je svetloba pol spusti napetost čez. Zvezan je čez en upor (R12) na ground. Ta ima namen da ustavi lekažo iz senzorja??? - to si še mal poglej. Mislim da je for ada daš en ful močn upor (200k) za to da kao prepreči to leakanje, pa razlagu je za različne pogoje svetlosti da more kompenzirat al kk...kao da je najboljša rešitev vzporedna vezava. Fuck it, to je chat pogruntu:
Vezje za merjenje ambientne svetlobe uporablja fototranzistor TEPT5700, ki deluje kot svetlobni senzor. Fototranzistor pretvarja svetlobo v električni tok. Ko svetloba pade na senzor, v tranzistorju nastane tok, katerega velikost je približno sorazmerna z osvetljenostjo. Ta tok teče iz napajalne napetosti 3,3 V skozi fototranzistor v skupno vozlišče vezja. Ker mikrokontroler ne more neposredno meriti toka, ga je potrebno pretvoriti v napetost. To nalogo opravlja upor R12 z vrednostjo 200 kΩ, ki je vezan proti masi. Tok, ki ga ustvari fototranzistor, teče skozi ta upor in na njem povzroči napetostni padec po zvezi V = I · R. Več svetlobe pomeni več toka skozi tranzistor in zato večjo napetost na vozlišču.

Pomembna lastnost fototranzistorjev je, da tudi v popolni temi niso popolnoma zaprti. Vedno teče majhen tok, ki ga imenujemo leakage current oziroma dark current. Če upora proti masi ne bi bilo, bi zaradi tega majhnega toka napetost na vozlišču postala nedoločena oziroma bi lahko "plavala". Upor R12 zato zagotavlja stabilno referenco proti masi in definira delovno točko senzorja. Hkrati določa tudi osnovno občutljivost senzorja, saj večji upor povzroči večjo napetost za isti tok fototranzistorja.

Napetost na tem vozlišču predstavlja analogno informacijo o svetlobi. Ta signal je na shemi označen kot LX_C. Gre za surov signal neposredno iz senzorja, ki ni dodatno filtriran. Ker je ta signal zelo občutljiv, lahko vsebuje precej šuma. Največ šuma pri takem senzorju povzroča utripanje umetnih svetlobnih virov. LED in fluorescentne luči pogosto utripajo s frekvenco okoli 100 Hz zaradi napajanja iz električnega omrežja. Fototranzistor to zazna kot majhna periodična nihanja svetlobe, zato tudi električni signal ni popolnoma stabilen. Poleg tega vsak polprevodniški element generira majhne naključne tokove zaradi toplotnega in kvantnega šuma.

Da bi dobili bolj stabilen signal za merjenje z mikrokontrolerjem, je v vezju dodan RC nizkoprepustni filter. Sestavljata ga upor R9 z vrednostjo 5,1 kΩ in kondenzator C5 z vrednostjo 0,1 µF. Ta filter duši hitre spremembe signala in prepušča predvsem počasne spremembe osvetlitve. Mejna frekvenca filtra je približno 312 Hz. To pomeni, da se hitra nihanja signala, ki nastanejo zaradi utripanja svetlobnih virov ali elektronskega šuma, precej zmanjšajo. Filtriran signal je označen kot LX_OUT in je primernejši za merjenje z analognim vhodom mikrokontrolerja.

V vezju sta prisotna tudi upora R10 (510 Ω) in R11 (10 kΩ), ki vodita signal na mikrokontroler preko signalov LX_A in LX_B. Ta dva voda omogočata, da mikrokontroler aktivno vpliva na občutljivost senzorja. Pin mikrokontrolerja je lahko nastavljen kot vhod ali kot izhod na nizkem potencialu. Če je pin nastavljen kot vhod, praktično ne vpliva na vezje. Če pa je nastavljen na logično ničlo, se preko ustreznega upora ustvari dodatna pot proti masi. S tem se efektivni upor proti masi zmanjša.

Ko je aktiviran samo upor R12, je skupni upor proti masi zelo velik (200 kΩ), zato je občutljivost senzorja visoka in lahko zaznamo tudi zelo majhne svetlobne tokove. Če mikrokontroler nastavi LX_B na nizko stanje, se upor R11 poveže proti masi in efektivni upor postane približno 9,5 kΩ. S tem se občutljivost zmanjša, ker za isti tok fototranzistorja nastane manjša napetost. Če bi mikrokontroler nastavil LX_A na nizko stanje, bi se v vezje vključil še upor R10 z vrednostjo 510 Ω in občutljivost bi postala še precej manjša. Na ta način lahko sistem prilagaja merilno območje senzorja in omogoča merjenje svetlobe v zelo širokem razponu osvetlitve.

Celotno vezje torej deluje tako, da fototranzistor pretvori svetlobo v tok, upor R12 ta tok pretvori v napetost, RC filter zgladi signal in mikrokontroler izmeri končno napetost. Z dodatnima uporoma R10 in R11 lahko mikrokontroler po potrebi spremeni efektivni upor proti masi in s tem prilagodi občutljivost merjenja svetlobe.


Okej zdej pa zadnjič smo kao risal shemo, dans pa dejansko delamo PCB konfiguracijo (kako bo dejansko zvezal - fizični bakcside kontrolerja). Ofnu si preko sheme pa projecta pcb, nastavu board settings kkr so na spletni (če naložiš iz gita so že po defaultu ok). Najprej smo itak pobrisal vse kar smo naredl, pol smo dal pa update pcb pa je nekak se že kr vse izrisal. Ne me uprašat kk kr ni peb nč razložu, si je pa Rok zapisu kaj morš mnde nareit:<br>
Vaja 3 kaj narediš v kicadu

Odpreš .pro file tvojega projekta, pol odpreš .sch in greš switch to pcb editor (čist desno gor tista zelena ikonca)...
tm če maš že kej zbrišeš vse in pritisneš F8 -> update pcb. to ti vrže ven vse komponente. Pol greš v board setup in daš physical stackup -> ok. in še design rules in tam noter vpišeš vrednosti iz spletne.
Izbereš na desni strani edge cuts pa izbereš da boš linije risu. Uzgori pod orodno vrstico nastaviš mrežo na 1mm (ker to ni tk ko autocad ko zna sam zrihtat). Narisal smo okvir pa zaokrožitve (kr to je najbolj pomembn valda).Ko narišeš closed loop (za ploščo) maš v orodni vrstici 3d viewer pa lah pogledaš če si kej zafuku. pol pa vzameš vse elemente pcb-ja (ki si jih odbu ko si dau update pcb) pa jih namečeš notr pravilno. Zdej pa še nastavimo kere dele bo avtomatsko zalil z bakrom. To bo pa rok povedu kaj so klikal.
