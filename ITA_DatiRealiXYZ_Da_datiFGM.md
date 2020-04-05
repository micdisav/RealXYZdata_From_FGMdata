# Tabella dei Contenuti
<!-- MDTOC maxdepth:6 firsth1:0 numbering:1 flatten:0 bullets:1 updateOnSave:0 -->
- [Riassunto](#pRiassunto)

- [Sintesi e finalità](#pSintesi)

- [1. Componenti geomagnetiche in breve](#p1)

    - [1.1 Procedura abituale per ottenere componenti geomagnetiche continue](#p1_1)

    - [1.2 Misure assolute discrete](#p1_2)

    - [1.3 Note sulle caratteristiche costruttive dei magnetometri *flux-gate*](#p1_3)

        - [1.3.1 Meccanica del sistema di sensori](#p1_3_1)

        - [1.3.2 *Dynamic range* dei sensori](#p1_3_2)

    - [1.4 Intermezzo comune alle due tipologie di terna sensore](#p1_4)

- [2. *Flowchart* essenziale del trattamento dati in un osservatorio geomagnetico](#p2)

- [3. Sensori variometrici su terna fissa, approccio al problema](#p3)

   - [3.1 Calcolo della matrice di rotazione del sensore applicando il metodo dei minimi quadrati](#p3_1)

   - [3.2 Stima dei residui tra i valori sperimentali _X<SUB>AID</SUB>_,_Y<SUB>AID</SUB>_,_Z<SUB>AID</SUB>_ e i valori _X<SUB>VAR</SUB>_,_Y<SUB>VAR</SUB>_,_Z<SUB>VAR</SUB>_ ruotati tramite matrice del sensore](#p3_2)

   - [3.3 Stima delle interpolazioni dei residui e loro aggiunta ai valori _X<SUB>VAR</SUB>_,_Y<SUB>VAR</SUB>_,_Z<SUB>VAR</SUB>_ ruotati tramite matrice del sensore](#p3_3)

- [4. Sensori variometrici disposti su sospensione cardanica, approccio al problema](#p4)

    - [4.1 Calcolo della matrice di rotazione per le componenti _X<SUB>VAR</SUB>_ e _Y<SUB>VAR</SUB>_ ortogonali tra loro e giacenti nel piano orizzontale, applicando il metodo dei minimi quadrati](#p4_1)

    - [4.2 Stima dei residui tra i valori sperimentali _X<SUB>AID</SUB>_,_Y<SUB>AID</SUB>_ e i valori _X<SUB>VAR</SUB>_,_Y<SUB>VAR</SUB>_ ruotati tramite matrice del sensore](#p4_2)

    - [4.3 Stima delle interpolazioni dei residui e loro aggiunta ai valori _X<SUB>VAR</SUB>_,_Y<SUB>VAR</SUB>_ ruotati tramite matrice del sensore](#p4_3)

    - [4.4 Calcolo valori _Z<SUB>REA</SUB>_ continui](#p4_4)

- [5. Sistemi lineari risultanti](#p5)

- [6. Note importanti sui tempi](#p6)

    - [6.1 Tempi per sensori disposti su terna fissa](#p6_1)

        - [6.1.1 Calcolo matrice del sensore - vedi (50), (51), (52) e residuali _X<SUB>RES</SUB>_, _Y<SUB>RES</SUB>_, _Z<SUB>RES</SUB>_ - vedi (25)](#p6_1_1)

        - [6.1.2 Interpolazione delle serie discrete _X<SUB>RES</SUB>_, _Y<SUB>RES</SUB>_, _Z<SUB>RES</SUB>_ onde stimare le serie continue _X<SUB>FitRES</SUB>_, _Y<SUB>FitRES</SUB>_, _Z<SUB>FitRES</SUB>_ - vedi (26)](#p6_1_2)

    - [6.2 Tempi per sensori disposti su sospensione cardanica](#p6_2)

        - [6.2.1 Calcolo matrice del sensore - vedi (53), (54) e calcolo residuali _X<SUB>RES</SUB>_, _Y<SUB>RES</SUB>_ - vedi (46)](#p6_2_1)

        - [6.2.2 Interpolazione delle serie discrete _X<SUB>RES</SUB>_, _Y<SUB>RES</SUB>_ onde stimare le serie continue _X<SUB>FitRES</SUB>_, _Y<SUB>FitRES</SUB>_ - vedi (47)](#p6_2_2)

[7. Conclusioni](#p7)

[Ringraziamenti](#pRingraziamenti)

[Bibliografia](#pBibliografia)
<!-- /MDTOC -->

## Procedure per ottenere componenti geomagnetiche cartesiane *XYZ* da misure magnetometro _flux-gate_ (per osservatori terrestri)

sig. Michele Di Savino - <michele.disavino@ingv.it>

INGV \| Istituto Nazionale di Geofisica e Vulcanologia, Sezione Geomagnetismo, Aeronomia e Geofisica Ambientale

<a name="pRiassunto"></a>
## Riassunto
Il Campo Magnetico Terrestre complessivo, scaturisce dalla influenza di effetti multipli non separabili:<BR>variazioni ionosfera, magnetismo dipolo proprio, induzione magnetica del suolo. Esso condiziona notevolmente la vita umana negli apparati e tecnologie civili frequentemente utilizzate; come anche nella esecuzione di ricerche in contesti non invasivi come la diagnostica medica, la salvaguardia ambientale, la ricerca energetica e mineraria, l'archeologia, eccetera.<BR>
In definitiva, un numero tutt'altro che esiguo di attività umane è influenzato, direttamente o indirettamente, dalle variazioni magnetiche naturali o artificiali. Il loro monitoraggio presenta quindi una certa importanza; di solito è effettuato tramite magnetometri stanziati in siti a basso livello di rumore elettromagnetico. Sono strumenti di rilevamento che hanno seguito l'evoluzione della scienza e della tecnica divenendo sempre più semplici, stabili, compatti, precisi e risolutivi. <BR>
Questa discussione si accinge ad esporre una metodologia di trattamento dei dati forniti da un tipico sistema di sensori *flux-gate*, o comunque assimilabile ad esso, volta a calcolare gli elementi geomagnetici fondamentali nel riferimento cartesiano cercando di sfruttare in maggior misura i benefici derivanti da una migliorata strumentistica.

<a name="pSintesi"></a>
## Sintesi e finalità
Il magnetometro *flux-gate* (in seguito: *FGM*), generalmente fornisce misurazioni vettoriali dell'induzione magnetica lungo tre direzioni che sono leggermente diverse dalle tre direzioni geografiche ricercate: Nord-Sud, Est-Ovest e Verticale.<BR>
Le seguenti elaborazioni mirano ad ottenere le corrette componenti magnetiche nel riferimento geografico. <BR>
Allo stesso tempo, implementano una correzione dello sbilanciamento meccanico del sistema sensori dovuto a lente variazioni naturali del livello del suolo o al verificarsi di eventi sismici, di intensità tale da spostare casualmente la posizione originale dei sensori. <BR><BR>
Questa relazione non vuole approfondire aspetti peculiari quali forme d'onda elettroniche di eccitazione impiegate, caratteristiche ferromagnetiche sensori, filtri dei segnali, adozione di tecnologie o componenti atti a minimizzare gli effetti temperatura, eccetera. <BR>
Il *FGM* è considerato nella sua forma più generale, solo due caratteristiche verranno discusse in questa relazione:
<BR> -Sensori posizionati in terna fissa o terna dotata di sospensione cardanica; le due procedure matematiche sono ovviamente diverse, anche se concettualmente identiche.
<BR> \-*Dynamic range* dello strumento considerato. Questo è un aspetto trasparente per le elaborazioni da eseguire, è gestito inizializzando correttamente tre variabili numeriche; una per ciascuna componente registrata *X*, *Y* e *Z*

<a name="p1"></a>
## 1. Componenti geomagnetiche in breve
Il seguente diagramma mostra i principali elementi utilizzati per descrivere il campo magnetico terrestre: <BR>
<a name="Fig1"></a>
<BR> ![Figura 1](./Images/F1_AbsoluteTern.png) <BR>
**Figura 1.** Elementi campo geomagnetico

Considerando un punto _O<SUB>ABS</SUB>_ (*ABS*, i.e. riferimento assoluto) sulla superfice terrestre, il vettore induzione magnetica ![](./Images/Fabs_vec.png) per esso passante, qualunque esso sia, si può scomporre come somma vettoriale di altri tre: <BR>
![](./Images/Xabs_vec.png) diretto lungo il meridiano geografico, verso Nord positivo; <BR>
![](./Images/Yabs_vec.png) diretto lungo il parallelo geografico, verso Est positivo; <BR>
![](./Images/Zabs_vec.png) diretto lungo la verticale, verso il basso positivo. <BR>

Ne risulta la relazione: ![](./Images/Fabs=Xabs,Yabs,Zabs_vecSum.png) mentre ![](./Images/Habs_vec.png) è la proiezione di ![](./Images/Fabs_vec.png) sul piano orizzontale e quindi sussistono anche le seguenti espressioni:
![](./Images/Habs=Xabs,Yabs_vecSum.png) e ![](./Images/Fabs=Habs,Zabs_vecSum.png).

Inoltre definiamo:<BR>
![](./Images/Dec.png) angolo declinazione, è l'angolo tra nord geografico e nord magnetico; positivo se ![](./Images/Yabs_vec.png) è diretto verso Est. <BR>
![](./Images/Inc.png) angolo inclinazione, è l'angolo tra il piano orizzontale e il vettore ![](./Images/Fabs_vec.png); positivo se ![](./Images/Fabs_vec.png) è diretto verso il basso. <BR>
![](./Images/Xabs_vec.png), ![](./Images/Yabs_vec.png) e ![](./Images/Zabs_vec.png) formano una terna ortogonale di vettori orientata secondo il riferimento geografico più direzione verticale al suolo. <BR>

<a name="p1_1"></a>
## 1.1 Procedura abituale per ottenere componenti geomagnetiche continue
Le componenti assolute _X<SUB>ABS</SUB>, Y<SUB>ABS</SUB>, Z<SUB>ABS</SUB>_ rivestono il ruolo fondamentale di misure di riferimento.
Il *FGM* fornisce misurazioni continue del campo geomagnetico sempre in *set* di tre grandezze vettoriali similmente al riferimento geografico, però in un diverso riferimento pseudo-casuale detto variometrico (in seguito: *VAR*, *variometric reference*). <BR>
Per ricondurre le misurazioni continue eseguite nel riferimento *VAR* in corrispondenti valori continui e virtuali ma nel riferimento *ABS*, le differenze omologhe *ABS*-*VAR* (i.e. linee di basi) vengono calcolate ai tempi delle misurazioni assolute. <BR>
Queste differenze discrete vengono interpolate lungo l'intervallo temporale opportuno e tramite inversione matematica, i valori *ABS* virtuali sono calcolati per tutti i tempi delle letture continue nel riferimento *VAR*, per ciascuna delle tre componenti *XYZ*. <BR>

<a name="p1_2"></a>
## 1.2 Misure assolute discrete
La conoscenza delle componenti assolute geomagnetiche ![](./Images/Xabs_vec.png), ![](./Images/Yabs_vec.png) e ![](./Images/Zabs_vec.png) si ottiene generalmente misurando gli angoli ![](./Images/Dec.png) e ![](./Images/Inc.png) magnetici e conoscendo il valore ![](./Images/Fabs_absolute.png) ai tempi corrispondenti. <BR>
Queste misure sono manuali e quindi discrete. <BR>

Gli angoli magnetici ![](./Images/Dec.png) e ![](./Images/Inc.png) si trovano ruotando, mediante un teodolite smagnetizzato, lungo i cerchi orizzontale e verticale, un rivelatore vettoriale di campo magnetico alla ricerca delle posizioni in cui si trova un valore del campo nullo, (strumento chiamato *DIM*, i.e. *Declination Inclination Magnetometer*), \[[Jankowski and Sucksdorff, 1996](#bIAGA)\]. <BR>   

Il menzionato valore ![](./Images/Fabs_absolute.png) è ottenuto dalla misurazione di un magnetometro scalare, solitamente un magnetometro a precessione di protoni o magnetometro ad effetto **Overhauser** (in seguito: *SM scalar magnetometer*), permanentemente in acquisizione. <BR>

Se occorre, il modulo di ![](./Images/Fabs_vec.png) dovrebbe essere variato matematicamente tramite una costante periodicamente verificata, che tenga conto dei gradienti magnetici tra i vari punti dell\'osservatorio in cui si trovano gli strumenti di misura, vedi [Figura 2](#Fig2) successiva. <BR>

<a name="p1_3"></a>
## 1.3 Note sulle caratteristiche costruttive dei magnetometri *flux-gate*
Qui vengono presi in considerazione solo due aspetti dello strumento *VAR* impiegato; in base a queste diverse caratteristiche, cambiano le procedure matematiche adottate. <BR>

<a name="p1_3_1"></a>
## 1.3.1 Meccanica del sistema di sensori
I *FGM* possiedono delle terne sensori geomagnetici con caratteristiche costruttive di due tipi principali: <BR>
terna fissa costituita da sensori *X*,*Y*,*Z* mutuamente ortogonali <BR>
e <BR>
terna composta da sensori disposti su giunto cardanico: la direzione del sensore *Z* è sempre verticale per gravità mentre i sensori *X* e *Y*, ortogonali tra loro, sono posizionati in un piano normale rispetto alla direzione *Z*. <BR>

<a name="p1_3_2"></a>
## 1.3.2 *Dynamic range* dei sensori
I *FGM* di prima generazione avevano una *dynamic range* limitata, infatti ciascun sensore lavorava artificialmente in un campo magnetico circa nullo perché altrimenti il valore induzione magnetica presente avrebbe facilmente saturato il sensore stesso. <BR>
In tal caso i sensori *flux-gate* misuravano praticamente delle variazioni, da addizionare alle porzioni principali di componente magnetica. <BR>
Ciascun nucleo del sensore, quindi, era dotato di compensazione elettromagnetica. <BR>
Caratteristiche *FGM* di alcuni *IMO*; (i.e. *Intermagnet Magnetic Observatory*). <BR>
DYNAMIC RANGE:  +/- 5000 nT (EBR, esp) <BR>
DYNAMIC RANGE:   +/- 500 nT (SPT, esp) <BR>
DYNAMIC RANGE:      6500 nT (LZH, chn) <BR>
\[[INTERMAGNET organization, 2014](#bIntermagnetDVD2010)\]. <BR>

I *FGM* di generazione più evoluta, sono progettati con *dynamic range* tanto ampia da superare il valore induzione campo magnetico misurabile sulla superfice terrestre. <BR>
In questa circostanza, le compensazioni elettroniche artificiali dei tre nuclei dei sensori sono inutili: <BR>
DYNAMIC RANGE:   Full field (all can) <BR>
DYNAMIC RANGE: +/- 80000 nT (all usa) <BR>
DYNAMIC RANGE: +/- 70000 nT (CLF, fra) <BR>
\[[INTERMAGNET organization, 2014](#bIntermagnetDVD2010)\]. <BR>

Nel seguito, faremo riferimento a strumenti *VAR* aventi basso valore della *dynamic range*, che richiedono quindi una compensazione elettronica. <BR>
Il trattamento della tipologia di strumenti *VAR* con una *dynamic range* sufficientemente elevata è più semplice, potenzialmente più preciso e non richiede modifiche formali alle procedure. <BR>
Vedi prossimi [§§3](#p3), [§§4](#p4). <BR>

<a name="p1_4"></a>
## 1.4 Intermezzo comune alle due tipologie di terna sensore
Tenendo conto delle differenze descritte nei precedenti [§1.3.1](#p1_3_1) e [§1.3.2](#p1_3_2), fondamentalmente, le risoluzioni possono essere implementate attraverso la variazione delle coordinate magnetiche tra il riferimento *VAR* (variometrico e noto) di partenza e il riferimento *ABS* (assoluto e incognito) di arrivo, per le componenti *XYZ* omologhe.
<BR><BR> Le soluzioni per terna dotata di sensori fissi e per terna dotata di sensori posizionati su articolazione cardanica saranno discusse, rispettivamente, nei [§§3](#p3) e [§§4](#p4).
<BR> Il [§5](#p5) presenterà le soluzioni matematiche complete per i due sistemi.
<BR> I [§§6](#p6) argomenteranno delle convenzioni temporali proposte per la risoluzione dei due tipi di sensori.
<BR> Infine l'ultimo [§7](#p7), confronterà la metodologia descritta con la procedura tradizionale fondata sulla valutazione dei singoli valori baseline.

<a name="p2"></a>
## 2. *Flowchart* essenziale del trattamento dati in un osservatorio geomagnetico
Il diagramma evidenzia i diversi siti in cui sono posizionati i vari strumenti, posti a distanza sufficiente da non influenzare a vicenda le misure rilevate.
<a name="Fig2"></a>
<BR> ![Figura 2](./Images/F2_Mag_flowchart.png) <BR>
**Figura 2.** *Flowchart* elaborazione dati geomagnetici

Il termine ***static*** indica valori numerici che, sotto determinate condizioni, si possono assumere costanti. <BR>
La dicitura ***discrete*** segnala dati discreti. <BR>
La dicitura ***continuous*** indica dati continui. <BR>
Il riquadro verde delimita il nucleo delle procedure particolari.

<a name="p3"></a>
## 3. Sensori variometrici su terna fissa, approccio al problema
Ricordando la [Figura 1](#Fig1), consideriamo: <BR>
-numero _N_ terne ordinate (_X<SUB>ABS</SUB>,Y<SUB>ABS</SUB>,Z<SUB>ABS</SUB>_) composte da valori di induzione magnetica delle misurazioni assolute discrete ottenute tramite *DIM*: questo sistema di riferimento ha origine in _O<SUB>ABS</SUB>_.

Definiamo due punti magnetici: <BR>
_O<SUB>VAR</SUB>_ è l\'origine della terna variometrica delle misurazioni magnetiche continue eseguite tramite *FGM*, <BR>
_O<SUB>REA</SUB>_ è l\'origine della terna delle misurazioni magnetiche virtuali continue che si calcolano attraverso la procedura corrente.

La [Figura 3](#Fig3) mostra la situazione descritta:
<a name="Fig3"></a>
<BR> ![Figura 3](./Images/F3_Fix_Var.png) <BR>
**Figura 3.** Componenti geomagnetiche lette dal variometro *FGM* nel suo riferimento _O<SUB>VAR</SUB>_ (a sinistra), e passaggio alle componenti reali nel riferimento _O<SUB>REA</SUB>_ (a destra)

L'origine di arrivo è denominata _O<SUB>REA</SUB>_, ma le componenti _X<SUB>REA</SUB>, Y<SUB>REA</SUB>, Z<SUB>REA</SUB>_ calcolate alla fine attraverso la trasformazione sono virtuali e si riferiscono all'origine _O<SUB>ABS</SUB>_, che è il riferimento osservatorio. <BR>
Perciò, virtualmente, _O<SUB>REA</SUB>_ coincide con _O<SUB>ABS</SUB>_. <BR>

Consideriamo anche: <BR>
-terne ordinate (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_) campionate a intervalli regolari da un *set* di tre sensori *flux-gate* mutuamente ortogonali con orientamento incognito. <BR>
Il *set* di sensori è posato nel punto _O<SUB>VAR</SUB>_; quest'ultimo è distinto dal punto _O<SUB>ABS</SUB>_. <BR>

-terna ordinata (_X<SUB>INI</SUB>,Y<SUB>INI</SUB>,Z<SUB>INI</SUB>_). <BR>
Due casi devono essere distinti in base alla caratteristica del *dynamic range* dello strumento *VAR* utilizzato, vedi [§1.3.2](#p1_3_2). <BR>

Alta *dynamic range*. <BR>
In questo caso, è sufficiente annullare la terna ordinata in questione:
<BR> ![](./Images/eq1.png) <BR>
in tutte le formule successive coinvolte.

Bassa *dynamic range*. <BR>
A causa della modalità di calcolo che sarà esposta a partire dal paragrafo successivo, è necessario stimare i valori delle componenti *X*,*Y*,*Z* assolute nel punto _O<SUB>VAR</SUB>_ nel momento in cui avviene l'orientamento del *set* sensori. <BR>
Questi valori possono essere stimati abbastanza agevolmente attraverso l\'esecuzione di una misura assoluta simultanea, infatti risulta:
<BR> ![](./Images/eq2.png) <BR>

dove: <BR>
_X<SUB>ABS</SUB>,Y<SUB>ABS</SUB>,Z<SUB>ABS</SUB>_ sono i valori ottenuti dal calcolo misura assoluta,
<BR> ![](./Images/XYZgradients.png) rappresentano i gradienti di induzione magnetica tra i siti *ABS* (i.e. *DIM*) e *VAR* (i.e. *FGM*) per le tre componenti. <BR>
I gradienti ![](./Images/XYZgradients.png) sono delle quantità quasi costanti, almeno sul breve periodo, ed è buona norma controllarli periodicamente. Indubbiamente più stabili e piccole rimangono queste quantità nel tempo e migliore è la qualità dell\'osservatorio geomagnetico. <BR>

Infine, allo stesso tempo, è necessario annullare elettronicamente (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_) sullo strumento *VAR*, preferibilmente in sincronia con il misuratore sul *DIM*. <BR>

Una volta impostato il sensore, se ci sono compensazioni (i.e. strumento con bassa *dynamic range*), le stesse regolazioni non devono più essere modificate. <BR>

<a name="p3_1"></a>
## 3.1 Calcolo della matrice di rotazione del sensore applicando il metodo dei minimi quadrati
In questa prima fase, consideriamo il sottoinsieme di _N_ terne ordinate (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_) che corrisponde ai tempi delle _N_ misure assolute discrete (_X<SUB>ABS</SUB>,Y<SUB>ABS</SUB>,Z<SUB>ABS</SUB>_). <BR>

Con il contributo della terna ordinata costante (_X<SUB>INI</SUB>,Y<SUB>INI</SUB>,Z<SUB>INI</SUB>_), possiamo considerare la solita espressione matematica che lega due riferimenti magnetici tridimensionali ortogonali generici:
<BR> ![](./Images/eq3.png) <BR>

dove r<SUB>11</SUB>,r<SUB>12</SUB>,r<SUB>13</SUB>,r<SUB>21</SUB>,r<SUB>22</SUB>,r<SUB>23</SUB>,r<SUB>31</SUB>,r<SUB>32</SUB>,r<SUB>33</SUB> sono i nove elementi della matrice di rotazione _R<SUB>3x3</SUB>_; essi correlano i valori letti sul sito *VAR* con i valori reali presenti sul sito *ABS* (o *DIM*). <BR>
Per il calcolo di questa matrice _R<SUB>3x3</SUB>_ prendiamo in considerazione solo le misure assolute e letture variometro (pedice *VAR*), ad istanti discreti corrispondenti. <BR>
Tale matrice viene calcolata con il contributo dei segnali totali del *FGM* e, pertanto, tiene conto anche delle cause indesiderate che possono influenzare le misurazioni a lungo termine: derive di temperatura, derive elettroniche e persino livellamento meccanico del *set* di sensori dello strumento *VAR*. <BR>
Svolgendo si ha:
<BR> ![](./Images/eq4.png) <BR>

ai primi membri delle tre espressioni, si possono effettuare le seguenti sostituzioni: <BR>
![](./Images/eq5,6,7.png) <BR>
pedice *AID* (i.e. *Abs Ini Difference*)

<a name="eq8"></a>
e il sistema diventa:
<BR> ![](./Images/eq8.png) <BR>

Le tre equazioni che costituiscono (8) possono essere separate perché i valori numerici *AID* e *VAR* sono noti e imposti da prelievi o calcolo dati. <BR>
Si consideri solo la prima equazione inclusa in (8): <BR>
![](./Images/eq9.png) <BR>
ed esaminiamo gli _N_ valori sperimentali delle quantità riportate.

I valori di r<SUB>11</SUB>,r<SUB>12</SUB>,r<SUB>13</SUB> che meglio approssimano gli _N_ valori sperimentali di _X<SUB>AID</SUB>_, _X<SUB>VAR</SUB>_, _Y<SUB>VAR</SUB>_, _Z<SUB>VAR</SUB>_ legati dalla relazione (9) nel senso dei minimi quadrati, si ottengono nel modo usuale costruendo lo scarto:
<BR> ![](./Images/eq10.png) <BR>

ed elevandolo al quadrato:
<BR> ![](./Images/eq11.png) <BR>

L'evoluzione _E_ del quadrato dello scarto, per gli _N_ campioni di _X<SUB>AID</SUB>_, _X<SUB>VAR</SUB>_, _Y<SUB>VAR</SUB>_, _Z<SUB>VAR</SUB>_ risulta:
<BR> ![](./Images/eq12.png) <BR>

Il punto di minimo di _E(r<SUB>11</SUB>,r<SUB>12</SUB>,r<SUB>13</SUB>)_ può essere calcolato imponendo il simultaneo annullamento delle derivate parziali di _E_ nelle variabili r<SUB>11</SUB>,r<SUB>12</SUB>,r<SUB>13</SUB>:
<BR> ![](./Images/eq13.png) <BR>

La soddisfazione di questa condizione porta alla risoluzione di un sistema lineare di rango 3 in cui le incognite sono r<SUB>11</SUB>,r<SUB>12</SUB>,r<SUB>13</SUB>. <BR>

I riga sistema:
<BR> ![](./Images/eq14,15.png) <BR>

i.e.
<BR> ![](./Images/eq16.png) <BR>

II riga sistema:
<BR> ![](./Images/eq17,18.png) <BR>

i.e.
<BR> ![](./Images/eq19.png) <BR>

III riga sistema:
<BR> ![](./Images/eq20,21.png) <BR>

i.e.
<BR> ![](./Images/eq22.png) <BR>

I sei elementi rimanenti r<SUB>21</SUB>,r<SUB>22</SUB>,r<SUB>23</SUB> e r<SUB>31</SUB>,r<SUB>32</SUB>,r<SUB>33</SUB> della matrice di rotazione sono ottenuti da due procedure analoghe applicando le opportune serie di dati sperimentali alle equazioni:
<BR> ![](./Images/eq23.png) <BR>
e
<BR> ![](./Images/eq24.png) <BR>
del sistema [\(8\)](#eq8).

<a name="p3_2"></a>
## 3.2 Stima dei residui tra i valori sperimentali _X<SUB>AID</SUB>_,_Y<SUB>AID</SUB>_,_Z<SUB>AID</SUB>_ e i valori _X<SUB>VAR</SUB>_,_Y<SUB>VAR</SUB>_,_Z<SUB>VAR</SUB>_ ruotati tramite matrice del sensore
Le informazioni ottenute attraverso il calcolo della matrice di rotazione _R<SUB>3x3</SUB>_, saranno successivamente integrate utilizzando i residuali tra i valori assoluti sperimentali (_X<SUB>AID</SUB>,Y<SUB>AID</SUB>,Z<SUB>AID</SUB>_) e i valori (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_) rilevati dal variometro e successivamente ruotati, ai tempi delle misure assolute eseguite. <BR>
Questi residuali discreti, per ciascuno degli _N_ punti, sono calcolati come segue: <BR>
<a name="eq25"></a> <BR>
![](./Images/eq25.png) <BR>

<a name="p3_3"></a>
## 3.3 Stima delle interpolazioni dei residui e loro aggiunta ai valori _X<SUB>VAR</SUB>_,_Y<SUB>VAR</SUB>_,_Z<SUB>VAR</SUB>_ ruotati tramite matrice del sensore
Interpolando queste _N_ triple ordinate di residuali discreti (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>,Z<SUB>RES</SUB>_) calcolate dalla (25) con le loro adatte variabili indipendenti tempo, per l\'intero intervallo di tempo interessato, otteniamo le terne ordinate continue (_X<SUB>FitRES</SUB>,Y<SUB>FitRES</SUB>,Z<SUB>FitRES</SUB>_) che forniscono le correzioni ottimali da addizionare al contributo dei valori continui (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_) moltiplicato per la matrice di rotazione del sensore: <BR>
<a name="eq26"></a> <BR>
![](./Images/eq26.png) <BR>

I valori reali (_X<SUB>REA</SUB>,Y<SUB>REA</SUB>,Z<SUB>REA</SUB>_) calcolati sono relativi al sito *ABS* (o *DIM*), ma ottenuti fisicamente dai corrispondenti valori numerici (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_) registrati continuamente dallo strumento *flux-gate* *VAR* con orientamento casuale.

A causa dell\'esecuzione di misurazioni assolute tramite *DIM* e delle tecniche matematiche adottate, l\'implementazione pratica dei metodi esposti richiede considerazioni sui tempi sia delle misurazioni assolute eseguite *XYZF* *AID* che dei dati considerati *XYZF* *VAR*: una di queste possibilità sarà presentata negli ultimi [§§6](#p6). <BR>
Fino alla discussione di questi paragrafi, le procedure sviluppate non terranno conto di tempi precisi.

<a name="p4"></a>
## 4. Sensori variometrici disposti su sospensione cardanica, approccio al problema
Ricordando la [Figura 1](#Fig1), consideriamo: <BR>
-numero _N_ coppie ordinate (_X<SUB>ABS</SUB>,Y<SUB>ABS</SUB>_) e quantità _Z<SUB>ABS</SUB>_ composte da valori di induzione magnetica delle misurazioni assolute discrete ottenute tramite *DIM*: questo sistema di riferimento ha origine in _O<SUB>ABS</SUB>_.

Definiamo due punti magnetici: <BR>
_O<SUB>VAR</SUB>_ è l\'origine della terna variometrica delle misurazioni magnetiche continue eseguite tramite *FGM*, <BR>
_O<SUB>REA</SUB>_ è l\'origine della terna delle misurazioni magnetiche virtuali continue che vengono calcolate attraverso la procedura corrente.

La [Figura 4](#Fig4) mostra la situazione descritta:
<a name="Fig4"></a>
<BR> ![Figura 4](Images/F4_Gimbal_Var.png) <BR>
**Figura 4.** Componenti geomagnetiche lette dal variometro *FGM* nel suo riferimento _O<SUB>VAR</SUB>_ (a sinistra), e passaggio alle componenti reali nel riferimento _O<SUB>REA</SUB>_ (a destra)

L'origine di arrivo è denominata _O<SUB>REA</SUB>_, ma le componenti _X<SUB>REA</SUB>, Y<SUB>REA</SUB>, Z<SUB>REA</SUB>_ calcolate alla fine attraverso la trasformazione sono virtuali e si riferiscono all'origine _O<SUB>ABS</SUB>_, che è il riferimento osservatorio. <BR>
Perciò, virtualmente, _O<SUB>REA</SUB>_ coincide con _O<SUB>ABS</SUB>_. <BR>

Consideriamo anche: <BR>
-coppie ordinate (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>_) e quantità _Z<SUB>VAR</SUB>_ campionate a intervalli regolari da un *set* di tre sensori vettoriali *flux-gate* disposti su di una articolazione cardanica. <BR>
Il *set* di sensori è posato nel punto _O<SUB>VAR</SUB>_; quest'ultimo è distinto dal punto  _O<SUB>ABS</SUB>_. <BR>

La terna dei sensori che misura (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>_) e _Z<SUB>VAR</SUB>_ è sospesa e la verticale lungo la direzione della forza peso e la direzione sensibile della componente _Z<SUB>VAR</SUB>_ coincidono, quindi _Z<SUB>VAR</SUB>_ misura davvero una quantità proporzionale alla componente verticale reale _Z<SUB>REA</SUB>_. <BR>
Sulla base della costruzione meccanica del *set* sensori, le altre due direzioni sensibili _X<SUB>VAR</SUB>_ e _Y<SUB>VAR</SUB>_ della terna *flux-gate* sono ortogonali tra loro ed entrambe ortogonali alla direzione sensibile della componente _Z<SUB>VAR</SUB>_. <BR>
Sebbene la direzione sensibile della componente _Z<SUB>VAR</SUB>_ sia sempre verticale, il piano orizzontale può ruotare attorno all'asse verticale e pertanto le direzioni delle componenti _X<SUB>VAR</SUB>_ e _Y<SUB>VAR</SUB>_ non sono immutabili. <BR>

-terna ordinata (_X<SUB>INI</SUB>,Y<SUB>INI</SUB>,Z<SUB>INI</SUB>_). <BR>
Due casi devono essere distinti in base alla caratteristica del *dynamic range* dello strumento *VAR* utilizzato, vedi [§1.3.2](#p1_3_2). <BR>

Alta *dynamic range*. <BR>
In questo caso, è sufficiente annullare la terna ordinata in questione:
<BR> ![](./Images/eq27.png) <BR>
in tutte le formule successive coinvolte.

Bassa *dynamic range*. <BR>
A causa della modalità di calcolo che sarà esposta a partire dal paragrafo successivo, è necessario stimare i valori delle componenti *X*,*Y*,*Z* assolute nel punto _O<SUB>VAR</SUB>_ nel momento in cui avviene l'orientamento del *set* sensori. <BR>
Questi valori possono essere stimati abbastanza agevolmente attraverso l\'esecuzione di una misura assoluta simultanea, infatti risulta:
<BR> ![](./Images/eq28.png) <BR>

dove: <BR>
_X<SUB>ABS</SUB>,Y<SUB>ABS</SUB>,Z<SUB>ABS</SUB>_ sono i valori ottenuti dal calcolo misura assoluta,
<BR> ![](./Images/XYZgradients.png) rappresentano i gradienti di induzione magnetica tra i siti *ABS* (i.e. *DIM*) e *VAR* (i.e. *FGM*) per le tre componenti. <BR>
I gradienti ![](./Images/XYZgradients.png) sono delle quantità quasi costanti, almeno sul breve periodo, ed è buona norma controllarli periodicamente. Indubbiamente più stabili e piccole rimangono queste quantità nel tempo e migliore è la qualità dell\'osservatorio geomagnetico. <BR>

Infine, allo stesso tempo, è necessario annullare elettronicamente (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_) sullo strumento *VAR*, preferibilmente in sincronia con il misuratore sul *DIM*. <BR>

Una volta impostato il sensore, se ci sono compensazioni (i.e. strumento con bassa *dynamic range*), le stesse regolazioni non devono più essere modificate. <BR>

La presenza della articolazione cardanica consente di separare le elaborazioni per le coppie ordinate (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>_), vedi [§4.1](#p4_1), [§4.2](#p4_2) e [§4.3](#p4_3); dalle elaborazioni relative alle componenti _Z<SUB>VAR</SUB>_, vedi [§4.4](#p4_4). <BR>

<a name="p4_1"></a>
## 4.1 Calcolo della matrice di rotazione per le componenti _X<SUB>VAR</SUB>_ e _Y<SUB>VAR</SUB>_ ortogonali tra loro e giacenti nel piano orizzontale, applicando il metodo dei minimi quadrati
A differenza del sensore a terna fissa, l\'elaborazione per _X<SUB>AID</SUB>_, _Y<SUB>AID</SUB>_, _X<SUB>VAR</SUB>_, _Y<SUB>VAR</SUB>_ è totalmente separata da quella relativa a _Z<SUB>AID</SUB>_, _Z<SUB>VAR</SUB>_. <BR><BR>
In questa prima fase, consideriamo il sottoinsieme di _N_ coppie ordinate (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>_) che corrisponde ai tempi delle _N_ misure assolute discrete  (_X<SUB>ABS</SUB>,Y<SUB>ABS</SUB>_). <BR>

Con il contributo della coppia ordinata costante (_X<SUB>INI</SUB>,Y<SUB>INI</SUB>_), possiamo considerare la solita espressione matematica che lega due riferimenti magnetici bidimensionali ortogonali generici:
<BR> ![](./Images/eq29.png) <BR>

dove r<SUB>11</SUB>,r<SUB>12</SUB>,r<SUB>21</SUB>,r<SUB>22</SUB> sono i quattro elementi della matrice di rotazione _R<SUB>2x2</SUB>_; essi correlano i valori letti sul sito *VAR* con i valori reali presenti sul sito *ABS* (o *DIM*). <BR>
Per il calcolo di questa matrice _R<SUB>2x2</SUB>_ prendiamo in considerazione solo le misure assolute e letture variometro (pedice *VAR*), ad istanti discreti corrispondenti. <BR>
Tale matrice viene calcolata con il contributo dei segnali totali del *FGM* e, pertanto, tiene conto anche delle cause indesiderate che possono influenzare le misurazioni a lungo termine: derive di temperatura, derive elettroniche e persino livellamento meccanico del *set* di sensori dello strumento *VAR*. <BR>
Svolgendo si ha:
<BR> ![](./Images/eq30.png) <BR>

ai primi membri delle due espressioni, è possibile effettuare le seguenti sostituzioni: <BR>
![](./Images/eq31,32.png) <BR>
pedice *AID* (i.e. *Abs Ini Difference*)

<a name="eq33"></a>
e il sistema diventa:
<BR> ![](./Images/eq33.png) <BR>

Le due equazioni che costituiscono (33) possono essere separate perché i valori numerici *AID* e *VAR* sono noti e imposti da prelievi o calcolo dati. <BR>
Si consideri solo la prima equazione inclusa in (33): <BR>
![](./Images/eq34.png) <BR>
ed esaminiamo gli _N_ valori sperimentali delle quantità riportate.

I valori di r<SUB>11</SUB>,r<SUB>12</SUB> che meglio approssimano gli _N_ valori sperimentali di _X<SUB>AID</SUB>_, _X<SUB>VAR</SUB>_, _Y<SUB>VAR</SUB>_ legati dalla relazione (34) nel senso dei minimi quadrati, si ottengono nel modo usuale costruendo lo scarto:
<BR> ![](./Images/eq35.png) <BR>

ed elevandolo al quadrato:
<BR> ![](./Images/eq36.png) <BR>

L'evoluzione _E_ del quadrato dello scarto, per gli _N_ campioni di _X<SUB>AID</SUB>_, _X<SUB>VAR</SUB>_, _Y<SUB>VAR</SUB>_ risulta:
<BR> ![](./Images/eq37.png) <BR>

Il punto di minimo di _E(r<SUB>11</SUB>,r<SUB>12</SUB>)_ può essere calcolato imponendo l'annullamento simultaneo delle derivate parziali di _E_ nelle variabili r<SUB>11</SUB>,r<SUB>12</SUB>:
<BR> ![](./Images/eq38.png) <BR>

La soddisfazione di questa condizione porta alla risoluzione di un sistema lineare di rango 2 in cui le incognite sono r<SUB>11</SUB>,r<SUB>12</SUB>. <BR>

I riga sistema:
<BR> ![](./Images/eq39,40.png) <BR>

i.e.
<BR> ![](./Images/eq41.png) <BR>

II riga sistema:
<BR> ![](./Images/eq42,43.png) <BR>

i.e.
<BR> ![](./Images/eq44.png) <BR>

I due elementi rimanenti r<SUB>21</SUB>,r<SUB>22</SUB> della matrice di rotazione sono ottenuti mediante procedura analoga applicando le opportune serie di dati sperimentali alla equazione:
<BR> ![](./Images/eq45.png) <BR>
del sistema [\(33\)](#eq33).

<a name="p4_2"></a>
## 4.2 Stima dei residui tra i valori sperimentali _X<SUB>AID</SUB>_,_Y<SUB>AID</SUB>_ e i valori _X<SUB>VAR</SUB>_,_Y<SUB>VAR</SUB>_ ruotati tramite matrice del sensore
Le informazioni ottenute attraverso il calcolo della matrice di rotazione _R<SUB>2x2</SUB>_, saranno successivamente integrate utilizzando i residuali tra i valori assoluti sperimentali (_X<SUB>AID</SUB>_,_Y<SUB>AID</SUB>_) e i valori (_X<SUB>VAR</SUB>_,_Y<SUB>VAR</SUB>_) rilevati dal variometro e successivamente ruotati, ai tempi delle misure assolute eseguite. <BR>
Questi residuali discreti, per ciascuno degli _N_ punti, sono calcolati come segue: <BR>
<a name="eq46"></a> <BR>
![](./Images/eq46.png) <BR>

<a name="p4_3"></a>
## 4.3 Stima delle interpolazioni dei residui e loro aggiunta ai valori _X<SUB>VAR</SUB>_,_Y<SUB>VAR</SUB>_ ruotati tramite matrice del sensore
Interpolando queste _N_ coppie ordinate di residuali discreti (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>_) calcolate dalla (46) con le loro adatte variabili indipendenti tempo, per l'intero intervallo di tempo interessato, otteniamo le coppie ordinate continue (_X<SUB>FitRES</SUB>,Y<SUB>FitRES</SUB>_) che forniscono le correzioni ottimali da addizionare al contributo dei valori continui (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>_) moltiplicati per la matrice di rotazione del sensore: <BR>
<a name="eq47"></a> <BR>
![](./Images/eq47.png) <BR>

I valori reali (_X<SUB>REA</SUB>,Y<SUB>REA</SUB>_) calcolati sono relativi al sito *ABS* (o *DIM*), ma ottenuti fisicamente dai corrispondenti valori numerici (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>_) registrati continuamente dallo strumento *flux-gate* *VAR* con orientamento casuale.

A causa dell'esecuzione di misurazioni assolute tramite *DIM* e delle tecniche matematiche adottate, l'implementazione pratica dei metodi esposti richiede considerazioni sui tempi sia delle misurazioni assolute eseguite *XYZF* *AID* che dei dati considerati *XYZF* *VAR*: una di queste possibilità sarà presentata negli ultimi [§§6](#p6). <BR>
Fino alla discussione di questi paragrafi, le procedure sviluppate non terranno conto di tempi precisi.

<a name="p4_4"></a>
## 4.4 Calcolo valori _Z<SUB>REA</SUB>_ continui
L'elemento sensibile della componente vettoriale _Z<SUB>VAR</SUB>_ assume sempre un orientamento verticale dovuto alla costruzione meccanica della terna sensore, quindi per ogni valore del campionamento continuo _Z<SUB>VAR</SUB>_ discende immediatamente il corrispondente valore continuo:
<BR> ![](./Images/eq48.png) <BR>

Dove i valori continui _Z<SUB>FitBAS</SUB>_ sono ottenuti preventivamente dall'interpolazione dei termini *baseline* _Z<SUB>BAS</SUB>_ delle misure assolute discrete e calcolati singolarmente come:
<BR> ![](./Images/eq49.png) <BR>

Nella costruzione della serie continua _Z<SUB>FitBAS</SUB>_, è stato scelto di ripetere l'unico valore _Z<SUB>BAS</SUB>_ calcolato per ogni singolo minuto relativo alla misura di inclinazione. <BR>
Queste interpolazioni hanno variabili indipendenti rappresentate dai tempi adeguati della misura di inclinazione. <BR>

Invece, per valutare il valore discreto della (49), _Z<SUB>ABS</SUB>_ (i.e. _Z<SUB>AID</SUB>_) è l'unico valore calcolato, mentre _Z<SUB>VAR</SUB>_ si ottiene calcolando la media tra tutti i valori di _Z<SUB>VAR</SUB>_ rilevati ai tempi inclinazione della misura assoluta considerata.

<a name="p5"></a>
## 5. Sistemi lineari risultanti
I sistemi lineari per il calcolo delle matrici di rotazione, per entrambe le tipologie di sensore *VAR*, sono riportati per completezza di seguito:

sensori su terna fissa:
<a name="eq50"></a> <BR>
![](./Images/eq50.png) <BR>

<a name="eq51"></a>
<BR> ![](./Images/eq51.png) <BR>

<a name="eq52"></a> <BR>
![](./Images/eq52.png) <BR>

sensori su *gimbal*:
<a name="eq53"></a> <BR>
![](./Images/eq53.png) <BR>

<a name="eq54"></a> <BR>
![](./Images/eq54.png) <BR>

Come possiamo verificare, nei sistemi lineari di ordine 3 (o 2), le matrici incomplete rimangono inalterate, invece le matrici dei termini noti variano, in dipendenza delle righe della matrice di rotazione da calcolare.

<a name="p6"></a>
## 6. Note importanti sui tempi
Il seguente diagramma focalizza i tempi di una tipica misura assoluta \(dalla [Figura 1](#Fig1)\):
<a name="Fig5"></a>
<BR> ![Figura 5](./Images/F5_AbsoluteMeasureView.PNG) <BR>
**Figura 5.** Tempi di esecuzione misura *DIM* <BR>
<BR> \[[Jankowski and Sucksdorff, 1996](#bIAGA)\]. <BR>
Per una corretta applicazione delle metodologie, per ogni misura assoluta, devono essere presenti tutte le componenti:
<BR> Entrambe le triple ordinate (_X<SUB>AID</SUB>,Y<SUB>AID</SUB>,Z<SUB>AID</SUB>_) e (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_), per sensori su terna fissa.
<BR> Entrambe le coppie ordinate (_X<SUB>AID</SUB>,Y<SUB>AID</SUB>_) e (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>_), per terna dotata di sospensione basculante.
<BR>Questo può essere verificato osservando i dati disponibili.

Ciascuna misura assoluta considerata dovrebbe essere eseguita in un istante; questo di solito non accade, infatti per una misura assoluta, le letture di declinazione e di inclinazione possono richiedere più minuti. <BR>
Seguono alcune proposte per implementare il tempo nelle procedure.

<a name="p6_1"></a>
## 6.1 Tempi per sensori disposti su terna fissa
<a name="p6_1_1"></a>
## 6.1.1 Calcolo matrice del sensore - vedi [\(50\)](#eq50), [\(51\)](#eq51), [\(52\)](#eq52) e residuali _X<SUB>RES</SUB>_, _Y<SUB>RES</SUB>_, _Z<SUB>RES</SUB>_ - vedi [\(25\)](#eq25)
Nel calcolo di questi elementi prendono parte le _N_ terne ordinate (_X<SUB>AID</SUB>,Y<SUB>AID</SUB>,Z<SUB>AID</SUB>_) e (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_), considerate ai tempi delle misure assolute discrete. <BR>
Sia la matrice di rotazione _R<SUB>3x3</SUB>_ che le terne discrete ordinate (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>,Z<SUB>RES</SUB>_) ottenute, derivano dal calcolo minimi quadrati e non riguardano tempi specifici. <BR>

I valori che compongono (_X<SUB>AID</SUB>,Y<SUB>AID</SUB>,Z<SUB>AID</SUB>_), come visto in precedente [Figura 5](#Fig5), sono certamente misurati in intervalli di tempo non trascurabili ma, considerando che nel calcolo dei minimi quadrati i valori del tempo sono irrilevanti, assumiamo semplicemente ogni misura assoluta come unica entità.<BR>

I valori (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_), invece, possono essere scelti tra tutti quelli misurati con continuità dallo strumento *VAR*, ai tempi coinvolti nella misura assoluta e precisamente:<BR>
Calcolo della media tra tutti i valori _X<SUB>VAR</SUB>_ (o _Y<SUB>VAR</SUB>_) acquisiti nei tempi della misura di declinazione, insieme a quelli acquisiti nei tempi della misura inclinazione. <BR>
Calcolo della media tra tutti i valori _Z<SUB>VAR</SUB>_ acquisiti nei tempi di misura inclinazione. <BR>

<a name="p6_1_2"></a>
## 6.1.2 Interpolazione delle serie discrete _X<SUB>RES</SUB>_, _Y<SUB>RES</SUB>_, _Z<SUB>RES</SUB>_ onde stimare le serie continue _X<SUB>FitRES</SUB>_, _Y<SUB>FitRES</SUB>_, _Z<SUB>FitRES</SUB>_ - vedi [\(26\)](#eq26)
Le _N_ terne ordinate discrete (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>,Z<SUB>RES</SUB>_), prendono parte al calcolo di queste interpolazioni, con variabili indipendenti i tempi delle misure assolute. <BR>
Come riportato nel precedente [§6.1.1](#p6_1_1), anche le terne ordinate (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>,Z<SUB>RES</SUB>_) sono considerate come entità dipendenti dalla misura assoluta determinata, ma senza tempo associato. <BR>

Le terne ordinate continue (_X<SUB>FitRES</SUB>,Y<SUB>FitRES</SUB>,Z<SUB>FitRES</SUB>_) sono ottenute interpolando, tramite il metodo scelto, le terne ordinate discrete (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>,Z<SUB>RES</SUB>_) considerando gli intervalli di tempo appropriati. <BR>
A tal fine, tempi specifici sono stati reintrodotti coerentemente con i percorsi logici esposti nella [Figura 5](#Fig5): <BR>
Per calcolare la serie _X<SUB>FitRES</SUB>_ (o _Y<SUB>FitRES</SUB>_), i valori _X<SUB>RES</SUB>_ (o _Y<SUB>RES</SUB>_) sono stati interpolati con variabili indipendenti i tempi di declinazione uniti ai tempi di inclinazione, della particolare misura assoluta. <BR>
Per calcolare la serie _Z<SUB>FitRES</SUB>_, i valori _Z<SUB>RES</SUB>_ sono stati interpolati con variabili indipendenti i tempi inclinazione della particolare misura assoluta. <BR>

Inoltre: <BR>
Lo stesso valore di _X<SUB>RES</SUB>_ (o _Y<SUB>RES</SUB>_) associato alla misura assoluta considerata, è stato ripetuto per ogni singolo minuto che costituisce l\'intervallo di tempo della declinazione e della inclinazione. <BR>
Con politica analoga, il valore di _Z<SUB>RES</SUB>_ associato alla misura assoluta considerata, è stato ripetuto per ogni singolo minuto che costituisce l\'intervallo di tempo della inclinazione.

<a name="p6_2"></a>
## 6.2 Tempi per sensori disposti su sospensione cardanica
<a name="p6_2_1"></a>
## 6.2.1 Calcolo matrice del sensore - vedi [\(53\)](#eq53), [\(54\)](#eq54) e calcolo residuali _X<SUB>RES</SUB>_, _Y<SUB>RES</SUB>_ - vedi [\(46\)](#eq46)
Nel calcolo di questi elementi prendono parte le _N_ coppie ordinate (_X<SUB>AID</SUB>,Y<SUB>AID</SUB>_) e (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>_), considerate ai tempi delle misure assolute discrete.
<BR> Sia la matrice di rotazione _R<SUB>2x2</SUB>_ che le coppie discrete ordinate (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>_) ottenute, derivano dal calcolo minimi quadrati e non riguardano tempi specifici.

I valori che compongono (_X<SUB>AID</SUB>,Y<SUB>AID</SUB>_), come visto in precedente [Figura 5](#Fig5), sono certamente misurati in intervalli di tempo non trascurabili ma, considerando che nel calcolo dei minimi quadrati i valori del tempo sono irrilevanti, assumiamo semplicemente ogni misura assoluta come unica entità.

I valori (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>_), invece, possono essere scelti tra tutti quelli misurati con continuità dallo strumento *VAR*, ai tempi coinvolti nella misura assoluta e precisamente: <BR>
Calcolo della media tra tutti i valori _X<SUB>VAR</SUB>_ (o _Y<SUB>VAR</SUB>_) acquisiti nei tempi della misura di declinazione, insieme a quelli acquisiti nei tempi di misura inclinazione.

<a name="p6_2_2"></a>
## 6.2.2 Interpolazione delle serie discrete _X<SUB>RES</SUB>_, _Y<SUB>RES</SUB>_ onde stimare le serie continue _X<SUB>FitRES</SUB>_, _Y<SUB>FitRES</SUB>_ - vedi [\(47\)](#eq47)
Le _N_ coppie ordinate discrete (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>_) prendono parte al calcolo di queste interpolazioni, con variabili indipendenti i tempi delle misure assolute. <BR>
Come riportato nel precedente [§6.2.1](#p6_2_1), anche le coppie ordinate (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>_) sono considerate come entità dipendenti dalla misura assoluta determinata, ma senza tempo associato. <BR>

Le coppie ordinate continue (_X<SUB>FitRES</SUB>,Y<SUB>FitRES</SUB>_) sono ottenute interpolando, tramite il metodo scelto, le coppie ordinate discrete (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>_) considerando gli intervalli di tempo appropriati. <BR>
A tal fine, tempi specifici sono stati reintrodotti coerentemente con i percorsi logici esposti nella [Figura 5](#Fig5): <BR>
Per calcolare la serie _X<SUB>FitRES</SUB>_ (o _Y<SUB>FitRES</SUB>_), i valori _X<SUB>RES</SUB>_ (o _Y<SUB>RES</SUB>_) sono stati interpolati con variabili indipendenti i tempi di declinazione uniti ai tempi di inclinazione, della particolare misura assoluta. <BR>

Inoltre: <BR>
Lo stesso valore di _X<SUB>RES</SUB>_ (o _Y<SUB>RES</SUB>_) associato alla misura assoluta considerata, è stato ripetuto per ogni singolo minuto che costituisce l\'intervallo di tempo della declinazione e della inclinazione.

<a name="p7"></a>
## 7. Conclusioni
Tali metodologie di conversione possono essere usate indifferentemente per terne sensori *FGM* posate sia con orientamento *HDZ* che *XYZ* \[[Technical University of Denmark, 2014](#bDTU_Orie)\] anzi, per quanto discusso, teoricamente l'orientamento del sistema di sensori può essere casuale. <BR>

Logicamente, è utile posizionare regolarmente il *set* di sensori nell\'orientamento *HDZ* o *XYZ* e quindi combinare entrambe le procedure: <BR>
-Inizialmente quella con formule di riduzione tradizionali e calcolo di singoli valori base per una verifica preliminare delle linee di base: controllo generale dell\'acquisizione, derive elettroniche e di temperatura o per costruire dati provvisori \[[Rigler, 2015](#bUSGS_Red); [DANISH METEOROLOGICAL INSTITUTE, TECHNICAL REPORT 04-14, 2004](#bDMI_Red)\]. <BR>
-In seguito, quando saranno disponibili tutte le serie di dati, sarà conveniente applicare le tecniche descritte con l\'uso di minimi quadrati e residui. Questa operazione compensa anche il livellamento del terreno e vengono costruiti i dati definitivi. <BR>

In presenza di spostamenti noti o casuali dovuti a terremoti che interessano la terna sensore, è ovviamente consigliabile eseguire misure assolute quanto prima possibile dopo l'evento che ha modificato la posizione del sistema sensori. <BR>
Se risulta conveniente, le serie di dati possono essere opportunamente divise per aumentare l\'accuratezza dei risultati parziali. <BR>
In presenza di *FGM* aventi bassi valori di *dynamic range*, in genere non è necessario procedere con una nuova acquisizione di valori iniziali (_X<SUB>INI</SUB>,Y<SUB>INI</SUB>,Z<SUB>INI</SUB>_). <BR>
Infatti, anche se la posizione della terna sensore è cambiata formalmente, se il sito di posa possiede basso gradiente magnetico, le condizioni iniziali risultano pressoché inalterate: l'accorgimento necessario rimane quello di non modificare le regolazioni elettroniche iniziali. <BR>

Utilizzando le formule di riduzione tradizionali, vedi [§1.1](#p1_1), viene eseguita una singola interpolazione numerica sui valori *baseline* (per ciascuna componente magnetica); mentre con il metodo esposto se ne eseguono due: <BR>
-la prima calcola la matrice fissa di rotazione: vedi [§3.1](#p3_1) per _R<SUB>3x3</SUB>_ o  [§4.1](#p4_1) per _R<SUB>2x2</SUB>_. <BR>
-la seconda calcola l\'interpolazione dei residui per compensare i valori prodotti dalla rotazione effettuata tramite matrice fissa del sensore: vedi [§3.3](#p3_3) per _R<SUB>3x3</SUB>_ o [§4.3](#p4_3) per _R<SUB>2x2</SUB>_. <BR>

Evidentemente, questo porta a un incremento dell’errore computazionale. Per contro, queste procedure sono particolarmente indicate per sensori *FGM* installati in luoghi caratterizzati da una certa sismicità o soggetti a variazioni naturali lente e apprezzabili del livello del suolo perché sono basate sui valori reali “veri”.
<BR> Per esempio, permettono di minimizzare le conseguenze di uno spostamento *random* del *set* sensori a cavallo di un evento sismico importante.

<a name="pRingraziamenti"></a>
## Ringraziamenti
I risultati presentati in questo documento si basano sui dati raccolti presso osservatori magnetici. Ringraziamo gli istituti nazionali che li supportano e INTERMAGNET per la promozione di elevati standard di pratica dell\'osservatorio magnetico ([www.intermagnet.org](http://www.intermagnet.org)).

<a name="pBibliografia"></a>
## Bibliografia

<a name="bDMI_Red"></a>
DANISH METEOROLOGICAL INSTITUTE, TECHNICAL REPORT 04-14, (2004). *Magnetic Results 2003 Brorfelde, Qeqertarsuaq, Qaanaaq and Narsarsuaq Observatories.* DANISH METEOROLOGICAL INSTITUTE, Copenhagen, pp. 5. <BR>
web page: <https://www.intermagnet.org/yearbooks/Denmark_2003.pdf>

Hitchman A.P., Crosthwaite P.G., Jones W.V., Lewis A.M., Wang L., (2011). *Australian Geomagnetism Report 2010, Volume 58*. Geoscience Australia, pp. 3. <BR>
web page: <https://www.intermagnet.org/yearbooks/Australia_2010.pdf>

INTERMAGNET organization, (2012). *INTERMAGNET Technical Reference Manual Version 4.6.* <BR>
web page: <https://www.intermagnet.org/publications/intermag_4-6.pdf>

<a name="bIntermagnetDVD2010"></a>
INTERMAGNET organization, (2014). *MAGNETIC OBSERVATORY DEFINITE DATA, INTERMAGNET 2010,* Observatory Information, DVD ROM.

<a name="bIAGA"></a>
Jankowski J. and Sucksdorff C., (1996). *GUIDE FOR MAGNETIC MEASUREMENTS AND OBSERVATORY PRACTICE*. IAGA organization, Warsaw, pp. 15-16, 87-98. <BR>
web page: <http://www.iaga-aiga.org/data/uploads/pdf/guides/iaga-guide-observatories.pdf>

<a name="bUSGS_Red"></a>
Rigler E. J., (2015). *XYZ Algorithm.* U.S. Geological Survey. <BR>
github page: <https://github.com/usgs/geomag-algorithms/blob/master/docs/algorithms/XYZ.md>

<a name="bDTU_Orie"></a>
Technical University of Denmark, (2014). *FLUXGATE MAGNETOMETER Suspended version Model FGE version K2 Manual.* DTU Space, National Space Institute, pp. 12-13. <BR>
web page: <https://www.space.dtu.dk/english/-/media/Institutter/Space/English/instruments_systems_methods/3-axis_fluxgate_magnetometer_model_fgm-fge/FGEFluxgateMagnetometerManual.ashx>
<BR>
.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>.<BR>
