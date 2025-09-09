# Tutorial per tradurre Crusader Kings 3

> Istruzioni operative e codici d’esempio. Copia-incolla dove serve.

---

```txt
# --------------------------------  Tutorial per tradurre Crusader Kings 3 --------------------------------------------------------------

# Ogni codice è costituito da 2 parti. La prima parte, [ROOT.Char. [target. [secondary. ecc, si riferisce sempre al soggetto della frase. [ROOT.Char. si riferisce sempre al nostro personaggio
# la seconda parte del codice invece è la richiesta. Ad esempio .GetFirstName], (ossia .OttieniPrimoNome) ci permette di ottenere il nome proprio di persona del bersaglio.

# Codice per maschile e femminile

# [Select_CString(personaggio.IsFemale,'a','o')]
# Esempio:
# Mi chiamo [Character.GetName]. Ieri sono andata al mare e mi sono fatta il bagno.
# Mi chiamo Emma. Ieri sono andat[Select_CString(Character.IsFemale,'a','o')] al mare e mi sono fatt[Select_CString(Character.IsFemale,'a','o')] il bagno.
# Oppure: Mi chiamo Emma. Ieri sono [Select_CString(Character.IsFemale,'andata','andato')] al mare e mi sono [Select_CString(Character.IsFemale,'fatta','fatto')] il bagno.

# Quand'è che non possiamo usare questo codice custom?
# Tutte quelle volte in cui dobbiamo mettere l'apostrofo.
# Ad esempio se dovessimo scrivere un'amica/un amico non potremmo usare questo codice, visto che ci sarebbero 3 apostrofi.
# [Select_CString(Character.IsFemale,'un'amica','un amico')]
# In questo caso vi invito a guardare gli esempi più in basso, così da fare dei semplici copia e incolla.
# Intanto ecco un esempio:
# un[personaggio.Custom('DE_PRO_PER_P_3P_G')]amica

# Alcuni codici terminano con lettere particolari. |E], |U] ecc; cosa vuol dire?
# |E] --> questo codice corrisponde alle parole in blu in gioco, sulle quali, passandoci sopra il mouse, ti compare la spiegazione.
# Quando la E è maiuscola, la parola comparirà in maiuscolo. Se ad esempio scrivessimo |e] comparirebbe in minuscolo.
# |U] --> questo codice fa comparire il maiuscolo sugli altri codici. Ad esempio [Character.GetSheHe] significa lei/lui, ma se scriviamo [Character.GetSheHe|U] comparirà Lei/Lui

# Quando ci troviamo di fronte ad un personaggio nobile ce ne accorgiamo dalla seconda parte del codice, ad esempio [host.GetTitleAsNameNoTooltip]
 # Quel "GetTitle" sta a significare che il codice sta cercando di richiamare il titolo del personaggio. Conte Jon, Duca Robert ecc. 
 # In questo caso bisogna usare il codice custom IT_NAM_COL. Ecco come
 # [host.Custom('IT_NAM_COL2')][host.GetTitleAsNameNoTooltip]

 # Notate come non c'è spazio tra ] e Conte, va scritto tutto attaccato
 # [CHARACTER.Custom('IT_NAM_COL')]    sul conte
 # [CHARACTER.Custom('IT_NAM_COL2')]  del conte
 # [CHARACTER.Custom('IT_NAM_COL3')]  il conte        [CHARACTER.Custom('IT_NAM_COL3')|U]   all'inizio delle frasi per far comparire "Il" in maiuscolo anziché "il"
 # [CHARACTER.Custom('IT_NAM_COL4')]  al conte
 # [CHARACTER.Custom('IT_NAM_COL5')]  dal conte

#------------------------------------------------------------------------------
 
 # Codici da mettere davanti ai titoli
 # [titolo.Custom('IT_COU_COL4')]     il titolo                 #      esempio: "Conquista La Contea di Cosenza, l'Earldom del Wessex" 
 # [titolo.Custom('IT_COU_COL')]       del titolo              #   2ndo esempio: "Jon possiede una rivendicazione sulla Contea di Cosenza            [exceptional_guest.GetShortUIName|U] possiede una [claim|E] [guest_claim.Custom('IT_COU_COL3')][guest_claim.GetName]"
 # [titolo.Custom('IT_COU_COL2')]     nel titolo
 # [titolo.Custom('IT_COU_COL3')]     sul titolo
 # [titolo.Custom('IT_COU_COL5')]     dal titolo
 # [titolo.Custom('IT_COU_COL7')]     al titolo 

 # ---------------------- ELENCO DEI CODICI ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 # --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 # Essendoci questo nuovo condice per il maschile e femminile, i vecchi codici astrusi come DE_ART_DEF_P_D sono ormai inutili. Li lasciamo in questo file in caso di necessità.

 # ARTICOLI DETERMINATIVI - Frase dell'esempio "Il mio/La mia"          [ROOT.Char.Custom('DE_ART_DEF_P_A')]
 # Il/La    Maiuscolo         [personaggio.Custom('DE_ART_DEF_P_D')] mi[personaggio.Custom('DE_END_PRO_S_N')] ---> Il mio       
 # il/la                               [personaggio.Custom('DE_ART_DEF_P_A')] mi[personaggio.Custom('DE_END_PRO_S_N')]  il mio
 # NUOVO CODICE         [Select_CString(personaggio.IsFemale,'La','Il')]

 ###################################################################################################################
 # MASCHILE / FEMMINILE o/a                                                 [Select_CString(CHARACTER.IsFemale,'a','o')]                [Select_CString(TARGET_CHARACTER.IsFemale,'a','o')] 
 # Il codice per noi è ROOT.Char quindi sarà:                        [ROOT.Char.Custom('DE_END_PRO_S_N')] o/a             [Select_CString(ROOT.Char.IsFemale,'a','o')]
 # Il codice per un personaggio qualsiasi -->                           [CHARACTER.Custom('DE_END_PRO_S_N')] o/a           [Select_CString(personaggio.IsFemale,'a','o')]
 #                                                                                                                                                                                                        [Select_CString(personaggio.IsFemale,'mia','mio')]
 ####################################################################################################################

 # Lei/lui                   [personaggio.GetSheHe]
 # egli/lei                  [personaggio.Custom('DE_ART_IND_A')]
 # oppure Egli          [personaggio.Custom('DE_ART_IND_A')|U]
 
 # SIGNORE / SIGNORA
 # [Select_CString(ROOT.Char.IsFemale,'mia Signora','mio Signore')]
 # [Select_CString(ROOT.Char.IsFemale,'Mia Signora','Mio Signore')]

 # TUTORE E TUTRICE, Lavoratore e Lavoratrice ecc.
 # tore/trice    [Select_CString(personaggio.IsFemale,'tutrice','tutore')]
 
 # ETA - ESSA [Select_CString(personaggio.IsFemale,'poetessa','poeta')]
 
 # gli/le  [personaggio.Custom('DE_PRO_DEM')]                 [Select_CString(personaggio.IsFemale,'le','gli')]
 # i/e   Servi / Serve [personaggio.Custom('DE_END_NOU_S_G')] [Select_CString(personaggio.IsFemale,'serve','servi')]
 
 # CODICE PER MODIFICARE LOCALMENTE UN TERMINE DELL'ENCICLOPEDIA
 # A sinistra lasciate il termine vecchio, nello spazio dove sta scritto english, a destra invece scrivete la traduzione che volete far apparire solo ed esclusivamente in quel rigo, per quella determinata frase.
 # [Concept('english','italiano')|E]
 # [Concept( 'english', 'italiano' )|E]
 # la |E] indica che la prima lettera apparirà in maiuscolo, quindi in gioco vedrete scritto "Italiano", se invece c'è la |e] vuol dire che gli sviluppatori vogliono che appaia in minuscolo.
 
 #Vi presento il conte Jon -> "[CHARACTER.Custom('IT_NAM_COL3')]Conte" non c'è spazio tra ] e Conte, va scritto tutto attaccato
 #          [CHARACTER.Custom('IT_NAM_COL')]    sul conte
 #          [CHARACTER.Custom('IT_NAM_COL2')]  del conte
 #          [CHARACTER.Custom('IT_NAM_COL3')]  il conte        [CHARACTER.Custom('IT_NAM_COL3')|U]   all'inizio delle frasi per far comparire "Il" in maiuscolo anziché "il"
 #          [CHARACTER.Custom('IT_NAM_COL4')]  al conte
 #          [CHARACTER.Custom('IT_NAM_COL5')]  dal conte

#------------------------------------------------------------------------------
 
 # Codici da mettere davanti ai titoli
 # [titolo.Custom('IT_COU_COL4')]     il titolo                 #      esempio: "Conquista La Contea di Cosenza, l'Earldom del Wessex" 
 # [titolo.Custom('IT_COU_COL')]       del titolo              #   2ndo esempio: "Jon possiede una rivendicazione sulla Contea di Cosenza            [exceptional_guest.GetShortUIName|U] possiede una [claim|E] [guest_claim.Custom('IT_COU_COL3')][guest_claim.GetName]"
 # [titolo.Custom('IT_COU_COL2')]     nel titolo
 # [titolo.Custom('IT_COU_COL3')]     sul titolo
 # [titolo.Custom('IT_COU_COL5')]     dal titolo
 # [titolo.Custom('IT_COU_COL7')]     al titolo 
 

  # PREPOSIZIONI (Ricorda di mettere )|U] alla fine del codice se la preposizione è all'inizio del rigo. Esempio [ROOT.Char.Custom('DE_END_ADJ_DEF_P_A')|U]
  # al   / alla        [personaggio.Custom('DE_END_ADJ_DEF_P_A')]       questo codice è già al/alla, non c'è bisogno di scrivere al[  
  # all' / alla     all[personaggio.Custom('DE_PRO_PER_S_3P_N')]  ['/a ]
  
 # dal  / dalla (oppure sul/sulla o quel/quella)  dal[personaggio.Custom('DE_END_ADJ_NUL_S_N')]
 # del  / della       [personaggio.Custom('DE_PRO_PER_P_3P_A')] con questo codice non va scritto del[ perché il codice dice direttamente [del] o [della]
 # dell'/ della   dell[personaggio.Custom('DE_PRO_PER_S_3P_N')]  ['/a ]

 # quel   / quella  quel[personaggio.Custom('DE_END_ADJ_NUL_S_N')] ossia [ /la] staccato
 # sul     / sulla  sul[personaggio.Custom('DE_END_ADJ_NUL_S_N')]        ossia [ /la]
 # quest' / questa   quest[personaggio.Custom('DE_PRO_PER_S_3P_N')]  ossia ['/a ] tutto attaccato
  
 # UN UOMO / DONNA 
 # un/una, un[personaggio.Custom('DE_PRO_POS_P_2P')] [personaggio.GetWomanMan] uomo   [/a]       [un] uomo          --> qui tra ] e "uomo" va uno spazio, a differenza di quanto avviene per [un/un']amica
 
 # un/un', un[personaggio.Custom('DE_PRO_PER_P_3P_G')]amica    tutto attaccato
 # la donna, l'uomo  l[ROOT.Char.Custom('DE_PRO_PER_S_3P_N')][ROOT.Char.GetWomanMan] ['/a ] tutto attaccato
 # quest'uomo    quest[personaggio.Custom('DE_PRO_PER_S_3P_N')]   ['/a ] tutto attaccato
 

 # VARI CODICI
 # Nome del Consigliere [councillor_liege.GetFirstName]
 # Titolo del consigliere [councillor_liege.GetTitleTierName]
 # Titolo al posto del nome [ROOT.Char.GetTitleAsNameNoTooltip] esempio "Oh possente Duca!"   [owner.GetTitleAsNameNoTooltip] 
 
 #CULTURA ITALIANA/gli ITALIANI 
 #cultura italiana [ROOT.Char.GetCulture.GetNameNoTooltip]
 #gli italiani     [ROOT.Char.GetCulture.GetCollectiveNounNoTooltip]
 
 
 #RICHIAMO DEL NOME DEL PERSONAGGIO CON E SENZA TOOLTIP
 # [personaggio.GetFirstNameNoTooltip]
 # [personaggio.GetFirstName]
 # [personaggio.GetName] apparirà --> Re William d'Inghilterra sottolineato
 
 
 
 #Quando la frase inizia per [CHARACTER.GetShortUIName] potrebbe riferirsi a noi o a un personaggio casuale. Per evitare che compaia la parola "Te" usiamo questo codice:

 # [Select_CString(CHARACTER.IsLocalPlayer,'Tu',CHARACTER.GetShortUIName)] [Select_CString( CHARACTER.IsLocalPlayer, 'sei', 'è' )]
 # [Select_CString(CHARACTER.IsLocalPlayer,'',CHARACTER.GetShortUIName)] [Select_CString( CHARACTER.IsLocalPlayer, 'Sei', 'è' )]
 
 # [Select_CString(CHARACTER.IsLocalPlayer,'Tu',CHARACTER.GetShortUIName)] [Select_CString( CHARACTER.IsLocalPlayer, 'hai', 'ha' )]
 # [Select_CString(CHARACTER.IsLocalPlayer,'',CHARACTER.GetShortUIName)] [Select_CString( CHARACTER.IsLocalPlayer, 'Hai', 'ha' )]
 
 # [Select_CString(TARGET_CHARACTER.IsLocalPlayer,'Tu',TARGET_CHARACTER.GetShortUIName)] [Select_CString( TARGET_CHARACTER.IsLocalPlayer, 'sei', 'è' )]
 # [Select_CString(TARGET_CHARACTER.IsLocalPlayer,'',TARGET_CHARACTER.GetShortUIName)] [Select_CString( TARGET_CHARACTER.IsLocalPlayer, 'Sei', 'è' )]
 
 # [Select_CString(TARGET_CHARACTER.IsLocalPlayer,'Tu',TARGET_CHARACTER.GetShortUIName)] [Select_CString( TARGET_CHARACTER.IsLocalPlayer, 'hai', 'ha' )]
 # [Select_CString(TARGET_CHARACTER.IsLocalPlayer,'',TARGET_CHARACTER.GetShortUIName)] [Select_CString( TARGET_CHARACTER.IsLocalPlayer, 'Hai', 'ha' )]
 
 # Jon e te [Select_CString( TARGET_CHARACTER.IsLocalPlayer, 'avete', 'hanno' )]
 # Jon e te [Select_CString( CHARACTER.IsLocalPlayer, 'avete', 'hanno' )]
 
 # nuovo esempio [Select_CString( attacker.IsLocalPlayer, '', attacker.GetShortUIName )][Select_CString( attacker.IsLocalPlayer, 'Ti sei', ' si è' )]
 
 # indipendentemente da chi sia il personaggio, Character o Target_Character, questo codice dice: se uno dei due è il nostro protagonista, fai comparire la prima frase, nell'esempio qua sotto è 'vi siete'.
 # [Select_CString(Or(CHARACTER.IsLocalPlayer, TARGET_CHARACTER.IsLocalPlayer), 'vi siete', 'si sono')]


 # ------------------------------------------------------------------ 
 # a volte ci troviamo a dover scrivere ad esempio "Con la tua famiglia" oppure "Con la famiglia di CHARACTER"
 # In questo caso, faremo come nell'esempio  
 # "Un matrimonio con la [Select_CString( CHARACTER.IsLocalPlayer, 'tua', 'famiglia di' )][Select_CString( CHARACTER.IsLocalPlayer, 'famiglia',CHARACTER.GetShortUIName)]."
 # "Un tempio nel [Select_CString( CHARACTER.IsLocalPlayer, 'tuo', 'villaggio di' )][Select_CString( CHARACTER.IsLocalPlayer, 'villaggio',CHARACTER.GetShortUIName)]".

 #"Vuole sposare uno dei [Select_CString( TARGET_CHARACTER.IsLocalPlayer, 'tuoi ', '' )]figli di umili natali [Select_CString( CHARACTER.IsLocalPlayer, '',TARGET_CHARACTER.GetShortUIName)]".
 # ------------------------------------------------------------------ 
 
 # questo è un altro modo di usare questo codice [personaggio.LocalPlayerString( 'sei', 'è' )] 
 # [personaggio.LocalPlayerString('Tuo ', 'Il ')] marito
 # [personaggio.LocalPlayerString( 'tuo ', '' )]
 
 # CODICE PER IL FILE DEI DUELLI
 #il mio avversario IO PERDENTE [sc_loser.Custom('DE_ART_DEF_P_A')] mi[sc_loser.Custom('DE_END_PRO_S_N')] avversari[sc_loser.Custom('DE_END_PRO_S_N')]
 #il mio avversario VINCENTE [sc_victor.Custom('DE_ART_DEF_P_A')] mi[sc_victor.Custom('DE_END_PRO_S_N')] avversari[sc_victor.Custom('DE_END_PRO_S_N')]


# NUOVO CODICE

#              [Select_CString(Or(first.IsLocalPlayer, second.IsLocalPlayer),'avete', 'hanno')] mangiato bene

# Codice Nome e Cognome = [ROOT.Char.GetFirstNameNoTooltip] [ROOT.Char.GetHouse.GetNameNoTooltip] (ossia nome e casata)
# Si possono usare gli operatori logici Or(condizione1, condizione2) e And(condizione1, condizione2) 
