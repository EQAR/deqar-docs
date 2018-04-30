### Report  

   |ELEMENT NAME                                 |REQUIRED     |ONE/MANY  |EXAMPLE                 |      
   |:--------------------------------------------|:------------|:---------|:-----------------------|
   |**Agency\***                                 |yes          |one       |*AAQ*<br>*33*           |  
   |DEQAR Report ID                              |no           |one       |*000786*                |
   |Local Identifier                             |no           |one       |*QAA1153-March15*       |
   |**Activity(\*)**                             |conditionally|one       |*institutional audit*<br>*programme evaluation*<br>*2*<br>*8*|   
   |**Activity Local Identifier(\*)**            |conditionally|one       |*inst_aud*              |
   |**Status\***                                 |yes          |one       |*1 - part of obligatory EQA system*<br>*2 - voluntary*|
   |**Decision\***                               |yes	       |one       |*1 - positive*<br>*2 - positive with conditions or restrictions*<br>*3 - negative*<br>*4 - not applicable*|
   |**Valid from\***                             |yes          |one       |*2015-01-15*            |
   |Valid to                                     |no           |one       |*2020-01-15*            |
   |**Date Format\***                            |yes          |one       |*%d/%m/%y*              |
   |Link                                         |no           |many      |*http://srv.aneca.es/ListadoTitulos/node/1182321350*|
   |Link Display Name                            |no           |many      |*General information on this programme.*|
 
### Existing Institution Record  

   |ELEMENT NAME                                 |REQUIRED     |ONE/MANY  |EXAMPLE                 |       
   |:--------------------------------------------|:------------|:---------|:-----------------------|
   |**DEQARINST ID(\*)**                         |conditionally|one (per) |*DEQARINST0034*         |
   |**ETER ID(\*)**                              |conditionally|one (per) |*BG0001*                |
   |**Local Institutional Identifier(\*)**       |conditionally|many (per)|*HCERES21*<br>*AT0004*  |

### New Institution Record 

   |ELEMENT NAME                                 |REQUIRED     |ONE/MANY  |EXAMPLE                 |        
   |:--------------------------------------------|:------------|:---------|:-----------------------|
   |**Official Institution Name(\*)**            |conditionally|one (per) |*Graz University of Technology*<br>*Югозападен университет "Неофит Рилски"*<br>*Πληροφορίες για τους αλλοδαπούς φοιτητές: Είσοδος και προγράμματα*|
   |Official Institution Name, transliterated    |no           |one (per) |*Yugo-zapaden universitet "Neofit Rilski”*<br>*Plirophoríes yia tous allodapoús phitités:  Ísodos kai prográmmata*|
   |English Institution Name                     |no           |one (per) |*South-West University "Neofit Rilski", Blagoevgrad*|
   |Institution Acronym                          |no           |one (per) |*SWU*                   |
   |**Institution Country(\*)**                  |conditionally|many (per)|*BG*<br>*BGR*           |
   |Institution City                             |no           |many (per)|*Sofia*                 |
   |Institution Latitude<br>Institution Longitude|no           |many (per)|*48,208,356; 1,636,776* |
   |Institution QF-EHEA Level                    |no           |many (per)|*0 - short cycle*<br>*1 - first cycle*<br>*2 - second cycle*<br>*3 - third cycle*|
   |**Institutional Website(\*)**                |conditionally|one (per) |*http://www.swu.bg*     |  

### Programme

   |ELEMENT NAME                                 |REQUIRED     |ONE/MANY  |EXAMPLE                 |       
   |:--------------------------------------------|:------------|:---------|:-----------------------|
   |Local Programme Identifier                   |no           |many (per)|*61*<br>*60800*         |
   |**Primary Programme Name(\*)**               |conditionally|one (per) |*Arts-specialist in opleiding*|
   |Programme Qualification                      |no           |one (per) |*Master in de specialistische geneeskunde*|
   |Programme Name Alternative                   |no           |many (per)|*Medical Natural Sciences*|
   |Programme Qualification Alternative          |no           |many (per)|*Master of Medicine*    |
   |Programme Country                            |no           |many (per)|*BE*<br>*BEL*           |
   |Programme NQF Level                          |no           |one (per) |*level 6*<br>*level 7*  |
   |Programme QF-EHEA Level                      |no           |one (per) |*0 - short cycle*<br>*1 - first cycle*<br>*2 - second cycle*<br>*3 - third cycle*|

### Report Files  

   |ELEMENT NAME                                 |REQUIRED     |ONE/MANY  |EXAMPLE                 |      
   |:--------------------------------------------|:------------|:---------|:-----------------------|
   |**File Original Location(\*)**               |conditionally|many      |*http://estudis.aqu.cat/MAD2014_UPC_es.pdf*|
   |File Display Name                            |no           |one (per) |*Report*<br>*Evaluation*<br>*MAD2014_UPC_es.pdf*|
   |**Report Language\***                        |yes          |many (per)|*es*<br>*spa*           | 